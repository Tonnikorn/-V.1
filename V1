<!doctype html>
<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>CoupleSplit — ต้น & แป๋ม</title>
  <meta name="description" content="เว็บสำหรับคู่รักช่วยบันทึกรายรับ-รายจ่ายและคำนวนการหารครึ่งอย่างเรียบง่าย" />
  <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai:wght@400;600;700&family=Charm:wght@400;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#fbfcfd;
      --card:#ffffff;
      --muted:#8892a0;
      --accent:#ff70a6;
      --accent-2:#ff97a7;
      --danger:#ef4444;
      --success:#22c55e;
      --radius:16px;
      --glass: rgba(255,255,255,0.7);
      font-family: 'IBM Plex Sans Thai', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
      color:#334155;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      background:linear-gradient(180deg,var(--bg),#f0f8ff);
      display:flex; align-items:center; justify-content:center;
      padding:20px;
      font-size:16px;
    }
    .wrap{
      width:100%; max-width:980px;
      background:var(--card);
      border-radius:24px;
      box-shadow:0 12px 30px rgba(15,23,42,0.08), 0 4px 12px rgba(15,23,42,0.04);
      overflow:hidden;
      border:1px solid rgba(15,23,42,0.03);
    }
    header{
      display:flex; align-items:center; justify-content:space-between;
      padding:20px 24px;
      gap:16px;
      background:linear-gradient(90deg, var(--accent-2), var(--accent));
      color:white;
      flex-wrap: wrap;
    }
    .brand{display:flex; gap:12px; align-items:center}
    .logo{
      width:50px; height:50px;
      border-radius:12px;
      background:rgba(255,255,255,0.2);
      display:flex; align-items:center; justify-content:center;
      color:white; font-weight:700; font-size:18px;
      font-family: 'Charm', cursive;
    }
    h1{margin:0;font-size:22px; font-weight:700;}
    p.lead{margin:0;color:rgba(255,255,255,0.8);font-size:14px; font-weight:400;}

    .names{display:flex; gap:10px; align-items:center; flex-wrap: wrap;}
    .name-field{display:flex; flex-direction:column; align-items:flex-start}
    .name-field input{
      width:120px;
      padding:8px 12px; border-radius:10px;
      border:1px solid rgba(255,255,255,0.3);
      font-size:15px; color:white;
      background:rgba(255,255,255,0.1);
      transition: all 0.2s ease;
    }
    .name-field input::placeholder { color: rgba(255,255,255,0.7); }
    .name-field input:focus { background: rgba(255,255,255,0.2); border-color: rgba(255,255,255,0.6); outline: none; }
    .names label.muted{color:rgba(255,255,255,0.8); font-size:12px;}
    .swap{
      background:rgba(255,255,255,0.2); padding:8px; border-radius:10px;
      display:flex; align-items:center; justify-content:center;
      border:1px solid rgba(255,255,255,0.3); color:white; cursor:pointer;
      font-size:18px; font-weight:600;
      transition: all 0.2s ease;
    }
    .swap:hover{background:rgba(255,255,255,0.3); border-color:rgba(255,255,255,0.5);}

    main{
      display:grid; grid-template-columns:1fr 360px;
      gap:20px;
      padding:20px 24px 24px;
    }

    /* left column */
    .panel{
      background:var(--glass);
      backdrop-filter: blur(8px);
      border-radius:18px;
      padding:18px;
      border:1px solid rgba(255,255,255,0.5);
      box-shadow:0 4px 15px rgba(0,0,0,0.05);
      transition: all 0.2s ease;
    }
    .summary{display:flex; align-items:center; justify-content:space-between; gap:16px; flex-wrap: wrap;}
    .big{font-size:24px; font-weight:700; color:#334155; line-height:1.2;}
    .big.positive{color:var(--success);}
    .big.negative{color:var(--danger);}
    .small{color:var(--muted); font-size:14px; font-weight:600;}

    .filters{display:flex; gap:10px; align-items:center; margin-top:16px; flex-wrap: wrap;}
    select, input[type='date'], input[type='text'], input[type='number']{
      padding:10px 14px; border-radius:12px;
      border:1px solid #cbd5e1;
      background:white; font-size:15px;
      appearance: none;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 20 20' fill='none' stroke='%236b7280' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpath d='M6 9l6 6 6-6'/%3E%3C/svg%3E");
      background-repeat: no-repeat;
      background-position: right 10px center;
      background-size: 16px;
      flex:1; min-width:120px;
    }
    .filters select{flex:none; width:auto;}


    .list{margin-top:16px; display:flex; flex-direction:column; gap:12px}
    .item{
      display:flex; justify-content:space-between; gap:12px;
      padding:12px 16px; border-radius:14px;
      border:1px solid rgba(255,255,255,0.6);
      background:rgba(255,255,255,0.9);
      box-shadow:0 2px 8px rgba(0,0,0,0.03);
      transition: all 0.2s ease;
      position:relative;
      flex-wrap: wrap;
    }
    .item:hover{transform: translateY(-2px); box-shadow:0 4px 12px rgba(0,0,0,0.05);}
    .item .left-content {flex-grow:1;}
    .item .right-content {display:flex; flex-direction:column; align-items:flex-end; gap:4px;}

    .meta{color:var(--muted); font-size:13px}
    .amount{font-weight:700; font-size:18px; color:#334155;}
    .amount.paid-by-you {color: var(--accent); }
    .amount.paid-by-partner {color: #3b82f6; }

    .actions{display:flex; gap:8px; margin-top:8px; justify-content:flex-end;}
    .btn{
      padding:8px 14px; border-radius:10px;
      border:1px solid #e2e8f0; background:white;
      font-size:14px; cursor:pointer;
      font-weight:600;
      transition: all 0.2s ease;
      color:#475569;
    }
    .btn:hover{background:#f0f4f8; border-color:#cbd5e1;}
    .btn.secondary{background:transparent; border-color:transparent;}
    .btn.danger{color:var(--danger); border-color:rgba(239,68,68,0.2); background:rgba(239,68,68,0.05);}
    .btn.danger:hover{background:rgba(239,68,68,0.1); border-color:rgba(239,68,68,0.3);}
    .btn.primary{
      background:linear-gradient(90deg,var(--accent),var(--accent-2));
      color:white; border:none;
      box-shadow:0 4px 10px rgba(255,112,166,0.2);
    }
    .btn.primary:hover{
      background:linear-gradient(90deg,var(--accent-2),var(--accent));
      box-shadow:0 6px 15px rgba(255,112,166,0.3);
      transform: translateY(-1px);
    }


    /* right column */
    .right-col{display:flex; flex-direction:column; gap:16px}
    .add-card{display:flex; flex-direction:column; gap:12px}
    .grid2{display:grid; grid-template-columns:1fr 1fr; gap:10px}
    label.muted{color:var(--muted); font-size:13px; font-weight:600;}

    footer{
      padding:16px 24px;
      display:flex; justify-content:space-between; align-items:center;
      color:var(--muted); font-size:12px;
      border-top:1px solid rgba(15,23,42,0.03);
      flex-wrap: wrap;
      gap:10px;
    }
    footer div:last-child {
      display: flex;
      justify-content: flex-end;
      flex-grow: 1;
    }

    /* modal */
    .modal-backdrop{position:fixed; inset:0; background:rgba(2,6,23,0.55); display:flex; align-items:center; justify-content:center; z-index:100; opacity:0; visibility:hidden; transition:opacity 0.3s ease, visibility 0.3s ease;}
    .modal-backdrop.active{opacity:1; visibility:visible;}
    .modal{
      width:100%; max-width:520px;
      background:white; border-radius:18px; padding:20px;
      box-shadow:0 10px 30px rgba(0,0,0,0.15);
      transform: translateY(20px); transition:transform 0.3s ease;
    }
    .modal-backdrop.active .modal{transform: translateY(0);}

    textarea{
      width:100%; height:160px;
      padding:12px; border-radius:10px;
      border:1px solid #cbd5e1; font-size:14px;
      resize:vertical;
    }
    h3{color:#334155;}

    /* Bill Popup Styles (These are critical for the new window) */
    .bill-popup-body {
        font-family: 'IBM Plex Sans Thai', sans-serif;
        padding: 30px;
        background-color: #f7f7f7;
    }
    .bill-container {
        max-width: 600px;
        margin: 0 auto;
        padding: 30px;
        background-color: white;
        border-radius: 10px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    }
    .bill-header {
        text-align: center;
        border-bottom: 2px solid var(--accent);
        padding-bottom: 10px;
        margin-bottom: 20px;
    }
    .bill-header h2 {
        color: var(--accent);
        margin: 0;
        font-size: 28px;
    }
    .bill-summary p {
        font-size: 18px;
        line-height: 1.6;
        color: #333;
        margin-bottom: 10px;
    }
    .bill-summary strong {
        color: var(--danger);
        font-size: 20px;
    }
    .bill-details h3 {
        margin-top: 25px;
        color: var(--muted);
        border-bottom: 1px solid #eee;
        padding-bottom: 5px;
    }
    .bill-item {
        display: flex;
        justify-content: space-between;
        padding: 8px 0;
        border-bottom: 1px dashed #eee;
        font-size: 15px;
    }
    .bill-item:last-child {
        border-bottom: none;
    }
    .bill-footer {
        text-align: center;
        margin-top: 30px;
        padding-top: 15px;
        border-top: 2px solid var(--accent);
    }
    .bill-footer button {
        background-color: var(--accent);
        color: white;
        border: none;
        padding: 10px 20px;
        border-radius: 8px;
        cursor: pointer;
        font-size: 16px;
    }

        @media (max-width:880px){ 
        body{padding:10px;} 
        .wrap{border-radius:16px;} 
        header{
            padding:16px; 
            flex-direction:column; 
            align-items:flex-start;
        } 
        .brand{
            width:100%; 
            justify-content:center;
        }
        /* Center names below the logo, give them some space */
        .names{
            width: 100%;
            justify-content: center;
            margin-top: 10px; 
            gap: 10px;
        }
        .name-field input{
            width:120px;
        }
        
        /* Adjust Layout to 1 column and move 'Add Card' to top */
        main{
            grid-template-columns: 1fr;
            padding: 16px 10px;
            gap: 16px;
        }
        .right-col{
            order: -1; 
        }
        
        /* Make form elements full width and stack them */
        .summary{
            flex-direction: column;
            align-items: flex-start;
            gap: 8px;
        }
        .filters, .grid2{
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .grid2{
            grid-template-columns: 1fr; /* Stack columns in Add Card */
        }
        
        select, input[type='date'], input[type='text'], input[type='number']{
            width: 100%;
            min-width: unset;
        }
        
        /* List Item adjustments for better readability */
        .item {
            flex-direction: column;
            align-items: flex-start;
        }
        .item .right-content {
            width: 100%;
            flex-direction: row; /* Put amount and actions on same line */
            justify-content: space-between;
            align-items: center;
            margin-top: 8px;
        }
        .actions {
            margin-top: 0;
        }

        /* Adjust Footer to stack vertically */
        footer{
            flex-direction: column;
            align-items: center;
            padding: 12px;
        }
        footer div:last-child {
          justify-content: center;
          width: 100%;
        }
    }
    
    /* Small mobile tweaks - Keep the grid2 fix for 480px */
    @media (max-width:480px) {
        .grid2 { grid-template-columns: 1fr; }
        .name-field input { width: 100px; }
        .names {gap: 8px;}
    }

  </style>
</head>
<body>
  <div class="wrap" role="application">
    <header>
      <div class="brand">
        <div class="logo">CS</div>
        <div>
          <h1>CoupleSplit</h1>
          <p class="lead">แอพเว็บแบ่งจ่ายสำหรับคู่รัก — คำนวนครึ่งอย่างเรียบง่าย</p>
        </div>
      </div>

      <div class="names" aria-hidden="false">
        <div class="name-field">
          <label class="muted">คุณ</label>
          <input id="youName" value="ต้น" />
          </div>
        <div class="swap" title="สลับผู้จ่าย">⇄</div>
        <div class="name-field">
          <label class="muted">แฟน</label>
          <input id="partnerName" value="แป๋ม" />
        </div>
      </div>
    </header>

    <main>
      <section class="panel">
        <div class="summary">
          <div>
            <div class="small">ยอดสุทธิ (จากรายการที่เลือก)</div>
            <div id="netText" class="big">เสมอกัน</div>
            <div class="muted" id="detailText">(ไม่มีรายการ)</div>
          </div>
          <div style="text-align:right">
            <div class="small">ยอดที่ <span id="partnerNameSummary">แป๋ม</span> ติด <span id="youNameSummary">ต้น</span></div>
            <div id="partnerOwes" class="big positive">0.00 ฿</div>
            <div style="height:10px"></div>
            <div class="small">ยอดที่ <span id="youNameSummary2">ต้น</span> ติด <span id="partnerNameSummary2">แป๋ม</span></div>
            <div id="youOwes" class="big negative">0.00 ฿</div>
          </div>
        </div>

        <div class="filters">
          <label class="muted">เดือน</label>
          <select id="monthFilter">
            <option value="all">ทั้งหมด</option>
          </select>
          <div style="flex:1"></div>
          <div class="muted">รายการทั้งหมด: <span id="totalCount">0</span></div>
        </div>

        <div class="list" id="list"></div>
      </section>

      <aside class="right-col">
        <div class="panel add-card">
          <div>
            <div class="muted">เพิ่มรายการใหม่</div>
            <div class="muted" style="font-size:12px">กรอกชื่อรายการ จำนวน และเลือกผู้จ่าย</div>
          </div>

          <div class="grid2">
            <input id="title" placeholder="ชื่อรายการ เช่น ข้าวเที่ยง" type="text" />
            <input id="amount" placeholder="จำนวน (฿)" inputmode="decimal" type="number" step="0.01" />
            <div>
              <label class="muted" style="font-size:13px">ผู้จ่าย</label>
              <select id="payer" style="width:100%; margin-top:6px;">
                <option value="you">คุณ</option>
                <option value="partner">แฟน</option>
              </select>
            </div>
            <div>
              <label class="muted" style="font-size:13px">วันที่</label>
              <input id="date" type="date" style="width:100%; margin-top:6px;" />
            </div>
          </div>

          <div style="display:flex; gap:8px; justify-content:flex-end; margin-top:8px">
            <button class="btn" id="clearBtn">ล้าง</button>
            <button class="btn primary" id="addBtn">+ เพิ่มรายการ</button>
          </div>
        </div>

        <div class="panel">
          <div class="muted">ทางลัด</div>
          <div style="display:flex; gap:8px; margin-top:8px; flex-wrap:wrap;">
            <button class="btn primary" id="viewBillBtn">ดูบิลสรุป</button> <button class="btn" id="exportBtn">ส่งออก JSON</button>
            <button class="btn" id="importBtn">นำเข้า JSON</button>
          </div>
          <div style="margin-top:10px" class="muted">เมนูเพิ่มเติม: ส่งบิล / เชื่อมบัญชี (ยังไม่เปิดใช้งาน)</div>
        </div>
      </aside>
    </main>

    <footer>
      <div>ออกแบบให้สวย เรียบ และสมมาตร — เน้นใช้ง่าย</div>
      <div><button class="btn danger" id="resetAll">รีเซ็ตทั้งหมด</button></div>
    </footer>
  </div>

  <div id="modal" class="modal-backdrop" role="dialog" aria-modal="true">
    <div class="modal">
      <h3 style="margin:0 0 12px 0; color:#334155;">นำเข้า JSON</h3>
      <textarea id="importArea" placeholder="วางข้อมูล JSON ที่นี่..."></textarea>
      <div style="display:flex; justify-content:flex-end; gap:8px; margin-top:12px">
        <button class="btn" id="closeModal">ยกเลิก</button>
        <button class="btn primary" id="applyImport">นำเข้า</button>
      </div>
    </div>
  </div>

  <script>
    // CoupleSplit — plain HTML/JS single-file
    (function(){
      const $ = id => document.getElementById(id);
      const youInput = $('youName');
      const partnerInput = $('partnerName');
      const swapNameBtn = document.querySelector('.swap');

      // Summary name elements
      const partnerNameSummary = $('partnerNameSummary');
      const youNameSummary = $('youNameSummary');
      const partnerNameSummary2 = $('partnerNameSummary2');
      const youNameSummary2 = $('youNameSummary2');


      const listEl = $('list');
      const monthFilter = $('monthFilter');
      const netText = $('netText');
      const detailText = $('detailText');
      const partnerOwesEl = $('partnerOwes');
      const youOwesEl = $('youOwes');
      const totalCount = $('totalCount');

      const title = $('title'); const amount = $('amount'); const payer = $('payer'); const date = $('date');
      const addBtn = $('addBtn'); const clearBtn = $('clearBtn'); const resetAll = $('resetAll');
      const exportBtn = $('exportBtn'); const importBtn = $('importBtn');
      const viewBillBtn = $('viewBillBtn'); // Get the new button
      const modal = $('modal'); const importArea = $('importArea'); const closeModal = $('closeModal'); const applyImport = $('applyImport');

      const STORAGE_KEY = 'couplesplit:expenses';
      const NAMES_KEY = 'couplesplit:names';

      let expenses = [];

      // --- helpers ---
      function save(){ localStorage.setItem(STORAGE_KEY, JSON.stringify(expenses)); }
      function saveNames(){ localStorage.setItem(NAMES_KEY, JSON.stringify({you: youInput.value, partner: partnerInput.value})); }
      function load(){ const s = localStorage.getItem(STORAGE_KEY); expenses = s? JSON.parse(s): []; render(); }
      function loadNames(){
        const s = localStorage.getItem(NAMES_KEY);
        if(s){
          const n=JSON.parse(s);
          youInput.value = n.you || 'ต้น';
          partnerInput.value = n.partner || 'แป๋ม';
        } else {
            youInput.value = 'ต้น';
            partnerInput.value = 'แป๋ม';
        }
      }

      function fmt(n){ return Number(n).toFixed(2); } // Simplified format without '฿' for calculation logic
      function fmtB(n){ return fmt(n) + ' ฿'; } // Format with '฿' for display
      function monthKey(d){
          const dt = new Date(d);
          if(isNaN(dt.getTime()) || !d) return '';
          const y = dt.getFullYear();
          const m = String(dt.getMonth()+1).padStart(2,'0');
          return y+'-'+m;
      }

      function computeBalances(list){
          let you=0, partner=0;
          list.forEach(ex=>{
              const half = Number(ex.amount)/2;
              if(ex.payer === 'you') partner += half; // Partner owes you
              else you += half; // You owe partner
          });
          return { youOwes: Math.round(you*100)/100, partnerOwes: Math.round(partner*100)/100 };
      }

      function escapeHtml(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

      // --- rendering ---
      function render(){
        const youName = escapeHtml(youInput.value);
        const partnerName = escapeHtml(partnerInput.value);

        // Update summary name elements
        partnerNameSummary.textContent = partnerName;
        youNameSummary.textContent = youName;
        partnerNameSummary2.textContent = partnerName;
        youNameSummary2.textContent = youName;

        // 1. Month Filter Population
        const months = Array.from(new Set(expenses.map(e => monthKey(e.date)).filter(x=>x))).sort((a,b)=>b.localeCompare(a));
        const currentFilterValue = monthFilter.value;
        monthFilter.innerHTML = '<option value="all">ทั้งหมด</option>' + months.map(m=>`<option value="${m}">${m}</option>`).join('');
        if(months.includes(currentFilterValue) || currentFilterValue === 'all'){
            monthFilter.value = currentFilterValue;
        } else {
             monthFilter.value = 'all';
        }

        const filter = monthFilter.value || 'all';
        const filtered = expenses.filter(e=> filter==='all' ? true : monthKey(e.date) === filter);

        // 2. List Rendering
        listEl.innerHTML = '';
        if(filtered.length===0){ listEl.innerHTML = '<div style="text-align:center; padding:28px; color:var(--muted)">ยังไม่มีรายการ</div>'; }
        filtered.forEach(ex=>{
          const item = document.createElement('div');
          item.className='item';

          const leftContent = document.createElement('div');
          leftContent.className = 'left-content';
          leftContent.innerHTML = `<div style="font-weight:600">${escapeHtml(ex.title)}</div><div class="meta">${ex.date || 'ไม่ระบุวันที่'} • จ่ายโดย ${ex.payer==='you'? youName : partnerName}</div>`;

          const rightContent = document.createElement('div');
          rightContent.className = 'right-content';
          const halfAmount = Number(ex.amount)/2;
          const amountClass = ex.payer === 'you' ? 'paid-by-you' : 'paid-by-partner';
          rightContent.innerHTML = `<div class="amount ${amountClass}">${fmtB(Number(ex.amount))}</div><div class="meta">แบ่ง: ${fmtB(halfAmount).replace(' ฿','')} ฿</div>`;

          const actions = document.createElement('div'); actions.className='actions';
          const swap = document.createElement('button'); swap.className='btn'; swap.textContent='สลับผู้จ่าย';
          swap.onclick = ()=>{
            const originalEx = expenses.find(x=>x.id === ex.id);
            if(originalEx){
              originalEx.payer = originalEx.payer==='you' ? 'partner' : 'you';
              save();
              render();
            }
          };

          const del = document.createElement('button'); del.className='btn danger'; del.textContent='ลบ';
          del.onclick = ()=>{
            if(confirm(`ต้องการลบรายการ "${escapeHtml(ex.title)}" หรือไม่?`)){
              expenses = expenses.filter(x=>x.id!==ex.id);
              save();
              render();
            }
          };
          actions.appendChild(swap); actions.appendChild(del);
          rightContent.appendChild(actions);

          item.appendChild(leftContent);
          item.appendChild(rightContent);
          listEl.appendChild(item);
        });

        // 3. Summary Update
        const balances = computeBalances(filtered);
        partnerOwesEl.textContent = fmtB(balances.partnerOwes);
        youOwesEl.textContent = fmtB(balances.youOwes);

        if (balances.partnerOwes > 0) { partnerOwesEl.classList.add('positive'); } else { partnerOwesEl.classList.remove('positive'); }
        if (balances.youOwes > 0) { youOwesEl.classList.add('negative'); } else { youOwesEl.classList.remove('negative'); }

        const net = Math.round((balances.partnerOwes - balances.youOwes)*100)/100;

        netText.classList.remove('positive', 'negative');
        if(net === 0){ netText.textContent = 'เสมอกัน'; }
        else if(net > 0){
          netText.textContent = `${partnerName} ติด ${youName} ${net.toFixed(2)} ฿`;
          netText.classList.add('positive');
        } else {
          netText.textContent = `${youName} ติด ${partnerName} ${Math.abs(net).toFixed(2)} ฿`;
          netText.classList.add('negative');
        }

        detailText.textContent = `คำนวนจาก ${filter==='all' ? 'ทั้งหมด' : filter} (${filtered.length} รายการ)`;
        totalCount.textContent = filtered.length;
      }

      // --- NEW: Bill Summary Logic ---
      function openBillSummary() {
          const youName = escapeHtml(youInput.value);
          const partnerName = escapeHtml(partnerInput.value);
          const filter = monthFilter.value || 'all';
          const filtered = expenses.filter(e=> filter==='all' ? true : monthKey(e.date) === filter);
          const balances = computeBalances(filtered);
          const net = Math.round((balances.partnerOwes - balances.youOwes)*100)/100;

          let summaryMessage = '';
          let billClass = '';

          if (net === 0) {
              summaryMessage = 'ยอดรวมสุทธิ: เสมอกัน! 🥳';
              billClass = 'equal';
          } else if (net > 0) {
              summaryMessage = `สรุป: ${partnerName} ต้องจ่ายคืน ${youName} เป็นจำนวนเงิน <strong>${net.toFixed(2)} ฿</strong>`;
              billClass = 'positive';
          } else {
              summaryMessage = `สรุป: ${youName} ต้องจ่ายคืน ${partnerName} เป็นจำนวนเงิน <strong>${Math.abs(net).toFixed(2)} ฿</strong>`;
              billClass = 'negative';
          }

          let detailsHtml = filtered.map(ex => {
              const payerName = ex.payer === 'you' ? youName : partnerName;
              const receiverName = ex.payer === 'you' ? partnerName : youName;
              const halfAmount = Number(ex.amount) / 2;
              const owesDirection = ex.payer === 'you' ? `${receiverName} ติด ${payerName}` : `${payerName} ติด ${receiverName}`;

              return `<div class="bill-item">
                          <span>${ex.date} - ${escapeHtml(ex.title)} (จ่ายโดย ${payerName})</span>
                          <span>${fmtB(halfAmount)}</span>
                      </div>`;
          }).join('');

          const billWindow = window.open('', 'CoupleSplitBillSummary', 'width=650,height=700,scrollbars=yes,resizable=yes');

          const billContent = `
            <html>
            <head>
                <title>สรุปบิล: ${youName} & ${partnerName}</title>
                <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai:wght@400;600;700&display=swap" rel="stylesheet">
                <style>
                    body { ${document.querySelector('body').style.cssText} } /* Inherit main styles */
                    ${document.querySelector('style').textContent} /* Copy main styles for context */

                    .bill-popup-body {
                        font-family: 'IBM Plex Sans Thai', sans-serif;
                        padding: 30px;
                        background-color: #f7f7f7;
                        color: #333;
                    }
                    .bill-container {
                        max-width: 600px;
                        margin: 0 auto;
                        padding: 30px;
                        background-color: white;
                        border-radius: 10px;
                        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
                    }
                    .bill-header {
                        text-align: center;
                        border-bottom: 2px solid var(--accent);
                        padding-bottom: 10px;
                        margin-bottom: 20px;
                    }
                    .bill-header h2 {
                        color: var(--accent);
                        margin: 0;
                        font-size: 28px;
                    }
                    .bill-summary {
                        text-align: center;
                        padding: 15px;
                        background-color: #fff0f5; /* Light pink background */
                        border-radius: 8px;
                        margin-bottom: 25px;
                        border: 1px solid var(--accent-2);
                    }
                    .bill-summary p {
                        font-size: 18px;
                        line-height: 1.6;
                        color: #333;
                        margin: 0;
                    }
                    .bill-summary strong {
                        color: var(--danger);
                        font-size: 24px;
                        font-weight: 700;
                    }
                    .bill-details h3 {
                        margin-top: 20px;
                        color: #475569;
                        border-bottom: 1px solid #eee;
                        padding-bottom: 5px;
                        font-size: 18px;
                    }
                    .bill-item {
                        display: flex;
                        justify-content: space-between;
                        padding: 8px 0;
                        border-bottom: 1px dashed #eee;
                        font-size: 15px;
                    }
                    .bill-item span:last-child {
                        font-weight: 600;
                    }
                    .bill-item:last-child {
                        border-bottom: none;
                    }
                    .bill-footer {
                        text-align: center;
                        margin-top: 30px;
                        padding-top: 15px;
                        border-top: 2px solid #eee;
                    }
                    .bill-footer button {
                        background-color: var(--accent);
                        color: white;
                        border: none;
                        padding: 10px 20px;
                        border-radius: 8px;
                        cursor: pointer;
                        font-size: 16px;
                        margin-right: 10px;
                    }
                    @media print {
                        .bill-footer { display: none; }
                        .bill-popup-body { background: white; padding: 0; }
                    }
                </style>
            </head>
            <body class="bill-popup-body">
                <div class="bill-container">
                    <div class="bill-header">
                        <h2>บิลสรุป CoupleSplit</h2>
                        <p>สำหรับรายการ ${filter === 'all' ? 'ทั้งหมด' : `เดือน ${filter}`}</p>
                        <p style="font-size: 14px; color: ${net > 0 ? 'var(--success)' : net < 0 ? 'var(--danger)' : '#475569'};">
                            ยอดที่ ${partnerName} ติด ${youName}: ${fmtB(balances.partnerOwes)} | ยอดที่ ${youName} ติด ${partnerName}: ${fmtB(balances.youOwes)}
                        </p>
                    </div>

                    <div class="bill-summary">
                        <p>${summaryMessage}</p>
                    </div>

                    <div class="bill-details">
                        <h3>รายการที่นำมาคำนวณ (${filtered.length} รายการ)</h3>
                        ${detailsHtml || '<p style="text-align:center; color:var(--muted);">ไม่มีรายการในบิลนี้</p>'}
                    </div>

                    <div class="bill-footer">
                        <button onclick="window.print()">พิมพ์บิลนี้</button>
                        <button onclick="window.close()">ปิด</button>
                    </div>
                </div>
            </body>
            </html>
          `;

          billWindow.document.write(billContent);
          billWindow.document.close();
      }

      // --- event listeners ---
      addBtn.addEventListener('click', ()=>{
        const t = title.value.trim();
        const a = parseFloat(amount.value);
        const p = payer.value;
        const d = date.value || new Date().toISOString().slice(0,10);

        if(!t || !a || isNaN(a) || a<=0){
          alert('กรุณากรอกชื่อและจำนวนที่ถูกต้อง');
          return;
        }

        const newId = Date.now() + Math.floor(Math.random() * 1000);
        const ex = { id: newId, title: t, amount: Math.round(a*100)/100, payer: p, date: d };
        expenses.unshift(ex);
        save();
        title.value=''; amount.value='';
        render();
      });

      clearBtn.addEventListener('click', ()=>{ title.value=''; amount.value=''; payer.value='you'; });
      monthFilter.addEventListener('change', ()=> render());
      youInput.addEventListener('change', ()=>{ saveNames(); render(); });
      partnerInput.addEventListener('change', ()=>{ saveNames(); render(); });
      viewBillBtn.addEventListener('click', openBillSummary); // Attach new function

      swapNameBtn.addEventListener('click', () => {
        [youInput.value, partnerInput.value] = [partnerInput.value, youInput.value];
        saveNames();
        if (payer.value === 'you') {
            payer.value = 'partner';
        } else if (payer.value === 'partner') {
            payer.value = 'you';
        }
        render();
      });

      exportBtn.addEventListener('click', ()=>{
        const data = { names: { you: youInput.value, partner: partnerInput.value }, expenses };
        const blob = new Blob([JSON.stringify(data, null, 2)], {type:'application/json'});
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href=url;
        a.download=`couplesplit-export-${new Date().toISOString().slice(0, 10)}.json`;
        document.body.appendChild(a);
        a.click();
        a.remove();
        URL.revokeObjectURL(url);
      });

      importBtn.addEventListener('click', ()=>{ modal.classList.add('active'); importArea.value=''; 
          
          closeModal.onclick = ()=> modal.classList.remove('active');
          applyImport.onclick = ()=>{
            try{
              const obj = JSON.parse(importArea.value);
              let importedExpenses = [];
              let importedNames = null;

              if(Array.isArray(obj)){ importedExpenses = obj; }
              else if(obj && Array.isArray(obj.expenses)){ importedExpenses = obj.expenses; importedNames = obj.names; }
              else { alert('ไฟล์ JSON ไม่ถูกต้อง'); return; }

              expenses = importedExpenses;
              if(importedNames){
                youInput.value = importedNames.you || 'ต้น';
                partnerInput.value = importedNames.partner || 'แป๋ม';
                saveNames();
              }

              save();
              modal.classList.remove('active');
              render();
            }catch(e){ alert('อ่าน JSON ไม่สำเร็จ: ' + e.message); }
          };
      });

      resetAll.addEventListener('click', ()=>{
        if(confirm('คุณแน่ใจหรือไม่? ข้อมูลทั้งหมดจะถูกลบและไม่สามารถกู้คืนได้')){
          expenses=[]; save();
          localStorage.removeItem(NAMES_KEY);
          youInput.value='ต้น'; partnerInput.value='แป๋ม';
          render();
        }
      });

      // initial load
      loadNames();
      load();

      // Allow pressing Enter on amount to add
      amount.addEventListener('keydown', (e)=>{ if(e.key === 'Enter'){ addBtn.click(); } });
      title.addEventListener('keydown', (e)=>{ if(e.key === 'Enter'){ amount.focus(); } });


      // Set default date to today's date if not already set by loaded data
      if (!date.value) {
          date.value = new Date().toISOString().slice(0,10);
      }
    })();
  </script>
</body>
</html>
