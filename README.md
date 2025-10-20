<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<title>CoupleSplit — ต้น & ป๋อมแป๋ม</title>
<meta name="description" content="เว็บสำหรับคู่รักช่วยบันทึกรายรับ-รายจ่ายและคำนวนการหารครึ่งอย่างเรียบง่าย">
<link rel="icon" href="icon.png" type="image/png">
<style>
  body {
    margin:0; padding:0;
    font-family: 'Prompt', sans-serif;
    background:#FFF8F0;
    display:flex; flex-direction:column; align-items:center;
    min-height:100vh;
  }
  h1 {
    margin:12px 0;
    color:#FF6B81;
    font-size:22px; text-align:center;
  }
  .container {
    background:white;
    border-radius:16px;
    padding:15px;
    width:100%; max-width:420px;
    box-shadow:0 2px 6px rgba(0,0,0,0.1);
  }
  input, select, button, textarea {
    width:100%;
    padding:10px;
    margin:5px 0;
    border:1px solid #ddd;
    border-radius:12px;
    font-size:16px;
  }
  button {
    background:#FF6B81;
    color:white;
    border:none;
    cursor:pointer;
    font-weight:bold;
    transition:0.2s;
  }
  button:hover { opacity:0.9; }
  .row { display:flex; gap:8px; }
  .row > * { flex:1; }
  .expense-list { margin-top:10px; }
  .item {
    display:flex; justify-content:space-between;
    background:#FFE3E7;
    border-radius:12px;
    padding:8px 10px;
    margin:5px 0;
    font-size:15px;
  }
  .summary {
    background:#FFE3E7;
    border-radius:12px;
    padding:10px;
    margin-top:10px;
    text-align:center;
    font-size:15px;
  }
  .footer-buttons {
    display:flex; flex-wrap:wrap; gap:10px; justify-content:center;
    margin-top:12px;
  }
  .footer-buttons button { flex:1 1 48%; font-size:14px; padding:8px; }
  .modal {
    position:fixed; inset:0;
    background: rgba(0,0,0,0.5);
    display:flex; justify-content:center; align-items:center;
    visibility:hidden; opacity:0;
    transition:0.2s;
  }
  .modal.active { visibility:visible; opacity:1; }
  .modal-content {
    background:white; border-radius:12px; padding:15px;
    width:90%; max-width:350px;
  }
  .modal-content textarea { height:120px; }
</style>
</head>
<body>
<h1>ค่าใช้จ่ายต้น&ป๋อมแป๋ม 💕</h1>
<div class="container">
  <div class="row">
    <input id="youName" placeholder="ชื่อคุณ (ต้น)">
    <input id="partnerName" placeholder="ชื่อคู่รัก (ป๋อมแป๋ม)">
    <button id="swapNameBtn">↔️</button>
  </div>
  <div class="row">
    <input id="title" placeholder="รายการ เช่น อาหาร">
    <input id="amount" type="number" placeholder="จำนวนเงิน">
  </div>
  <div class="row">
    <select id="payer">
      <option value="you">คุณจ่าย</option>
      <option value="partner">คู่รักจ่าย</option>
    </select>
    <input id="date" type="date">
  </div>
  <div class="row">
    <button id="addBtn">➕ เพิ่ม</button>
    <button id="clearBtn" style="background:#ccc;color:#333;">ล้าง</button>
  </div>

  <div class="summary" id="summaryBox">ยังไม่มีรายการ</div>
  <div class="expense-list" id="list"></div>

  <div class="footer-buttons">
    <button id="resetAll" style="background:#999;">รีเซ็ตทั้งหมด</button>
    <button id="exportBtn" style="background:#ff9f43;">📤 ส่งออก</button>
    <button id="importBtn" style="background:#54a0ff;">📥 นำเข้า</button>
    <button id="viewBillBtn" style="background:#2ecc71;">🧾 ดูบิล</button>
  </div>
</div>

<div class="modal" id="modal">
  <div class="modal-content">
    <h3>นำเข้าข้อมูล JSON</h3>
    <textarea id="importArea" placeholder="วางข้อมูล JSON ที่นี่"></textarea>
    <div class="row">
      <button id="applyImport">ตกลง</button>
      <button id="closeModal" style="background:#ccc;color:#333;">ปิด</button>
    </div>
  </div>
</div>

<script>
(() => {
  const STORAGE_KEY = "coupleSplitData";
  const youInput = document.getElementById("youName");
  const partnerInput = document.getElementById("partnerName");
  const swapNameBtn = document.getElementById("swapNameBtn");
  const title = document.getElementById("title");
  const amount = document.getElementById("amount");
  const payer = document.getElementById("payer");
  const date = document.getElementById("date");
  const addBtn = document.getElementById("addBtn");
  const clearBtn = document.getElementById("clearBtn");
  const list = document.getElementById("list");
  const summaryBox = document.getElementById("summaryBox");
  const resetAll = document.getElementById("resetAll");
  const exportBtn = document.getElementById("exportBtn");
  const importBtn = document.getElementById("importBtn");
  const viewBillBtn = document.getElementById("viewBillBtn");
  const modal = document.getElementById("modal");
  const closeModal = document.getElementById("closeModal");
  const importArea = document.getElementById("importArea");
  const applyImport = document.getElementById("applyImport");

  let expenses = [];

  function save(){ localStorage.setItem(STORAGE_KEY, JSON.stringify(expenses)); }
  function load(){ expenses = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]"); render(); }
  function saveNames(){ localStorage.setItem("coupleNames", JSON.stringify({ you: youInput.value, partner: partnerInput.value })); }
  function loadNames(){ const n = JSON.parse(localStorage.getItem("coupleNames") || "{}"); if(n.you) youInput.value=n.you; if(n.partner) partnerInput.value=n.partner; }

  function render(){
    list.innerHTML="";
    if(expenses.length===0){ summaryBox.textContent="ยังไม่มีรายการ"; return; }
    let you=0,partner=0;
    expenses.forEach(e=>{
      if(e.payer==="you") you+=e.amount; else partner+=e.amount;
      const div=document.createElement("div");
      div.className="item";
      div.innerHTML=`<span>${e.title} (${e.date||"-"})</span><span>${e.payer==="you"?youInput.value:partnerInput.value} จ่าย: ${e.amount}฿</span>`;
      list.appendChild(div);
    });
    const diff=you-partner;
    if(diff>0) summaryBox.textContent=`${partnerInput.value} ต้องโอนให้ ${youInput.value} ${(Math.abs(diff/2)).toFixed(2)} บาท`;
    else if(diff<0) summaryBox.textContent=`${youInput.value} ต้องโอนให้ ${partnerInput.value} ${(Math.abs(diff/2)).toFixed(2)} บาท`;
    else summaryBox.textContent="ตอนนี้ทั้งคู่จ่ายเท่ากัน ❤️";
  }

  function openBillSummary(){
    let totalYou=0,totalPartner=0;
    expenses.forEach(e=>{ if(e.payer==="you") totalYou+=e.amount; else totalPartner+=e.amount; });
    const diff=totalYou-totalPartner;
    let summaryMessage="";
    if(diff>0) summaryMessage=`${partnerInput.value} ต้องโอนให้ ${youInput.value} ${(Math.abs(diff/2)).toFixed(2)} บาท`;
    else if(diff<0) summaryMessage=`${youInput.value} ต้องโอนให้ ${partnerInput.value} ${(Math.abs(diff/2)).toFixed(2)} บาท`;
    else summaryMessage="ตอนนี้ทั้งคู่จ่ายเท่ากัน ❤️";
    const detailsHtml = expenses.map(e=>`<div class="bill-item"><span>${e.title}</span><span>${e.amount}฿ (${e.payer==="you"?youInput.value:partnerInput.value})</span></div>`).join("");
    const billWindow=window.open("","_blank");
    const billContent=`<!DOCTYPE html><html lang="th"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width, initial-scale=1"><title>บิลสรุปค่าใช้จ่าย</title><style>
      body{font-family:'Prompt',sans-serif;background:#fff9f9;padding:20px;}
      .bill-container{background:white;padding:20px;border-radius:16px;max-width:500px;margin:auto;box-shadow:0 2px 6px rgba(0,0,0,0.1);}
      .bill-header{text-align:center;color:#FF6B81;margin-bottom:20px;}
      .bill-header h2{margin:0;font-size:26px;}
      .bill-summary{text-align:center;background:#FFE3E7;padding:10px;border-radius:10px;margin-bottom:15px;}
      .bill-item{display:flex;justify-content:space-between;border-bottom:1px dashed #ddd;padding:6px 0;}
      .bill-footer{text-align:center;margin-top:25px;}
      .bill-footer button{background:#FF6B81;border:none;color:white;padding:10px 20px;border-radius:8px;cursor:pointer;margin:0 5px;}
      .bill-footer button:nth-child(2){background:#ccc;color:#333;}
    </style></head><body>
    <div class="bill-container">
      <div class="bill-header"><h2>บิลสรุปค่าใช้จ่าย</h2><p>${youInput.value} ❤️ ${partnerInput.value}</p></div>
      <div class="bill-summary"><p>${summaryMessage}</p></div>
      ${detailsHtml||'<p style="text-align:center;color:#999;">ไม่มีรายการ</p>'}
      <div class="bill-footer">
        <button onclick="window.print()">🧾 พิมพ์</button>
        <button onclick="window.close()">ปิด</button>
      </div>
    </div>
    </body></html>`;
    billWindow.document.open();
    billWindow.document.write(billContent);
    billWindow.document.close();
  }

  swapNameBtn.onclick=()=>{ const tmp=youInput.value; youInput.value=partnerInput.value; partnerInput.value=tmp; saveNames(); render(); };
  youInput.oninput=partnerInput.oninput=saveNames;

  addBtn.onclick=()=>{
    const t=title.value.trim(),a=parseFloat(amount.value);
    if(!t||isNaN(a)) return alert("กรุณากรอกชื่อรายการและจำนวนให้ครบ");
    const d=date.value||new Date().toISOString().split("T")[0];
    expenses.push({id:Date.now(),title:t,amount:a,payer:payer.value,date:d});
    save(); render(); title.value=""; amount.value=""; 
  };
  clearBtn.onclick=()=>{ title.value=""; amount.value=""; date.value=""; payer.value="you"; };
  resetAll.onclick=()=>{ if(confirm("ต้องการรีเซ็ตข้อมูลทั้งหมดหรือไม่?")){ localStorage.removeItem(STORAGE_KEY); expenses=[]; render(); } };
  exportBtn.onclick=()=>{ const blob=new Blob([JSON.stringify(expenses,null,2)],{type:"application/json"}); const a=document.createElement("a"); a.href=URL.createObjectURL(blob); a.download="couplesplit-data.json"; a.click(); };
  importBtn.onclick=()=>modal.classList.add("active");
  closeModal.onclick=()=>modal.classList.remove("active");
  applyImport.onclick=()=>{ try{ const data=JSON.parse(importArea.value); if(Array.isArray(data)){ expenses=data; save(); render(); modal.classList.remove("active"); }else alert("ข้อมูลไม่ถูกต้อง"); }catch{ alert("รูปแบบ JSON ไม่ถูกต้อง"); } };
  viewBillBtn.onclick=openBillSummary;

  loadNames(); load();
})();
</script>
</body>
</html>
