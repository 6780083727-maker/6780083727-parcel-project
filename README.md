<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>ระบบบริหารจัดการพัสดุ — โรงเรียนวัดสังเวช</title>
  <style>
    /* โทนสี: น้ำเงินกรมท่า + ขาว + เทาอ่อน */
    :root{
      --navy:#0b3d91;
      --white:#ffffff;
      --light:#f4f6f8;
      --muted:#6b7280;
      --success:#0f9d58;
      --danger:#d9534f;
      --card-shadow: 0 2px 6px rgba(11,61,145,0.08);
      --radius:8px;
      --max-width:1100px;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: "Noto Sans Thai", "Segoe UI", Roboto, Arial, sans-serif;
      background:var(--light);
      color:#222;
      -webkit-font-smoothing:antialiased;
    }
    header.topbar{
      background:var(--navy);
      color:var(--white);
      padding:12px 16px;
      display:flex;
      align-items:center;
      justify-content:space-between;
    }
    header .brand{
      display:flex;
      align-items:center;
      gap:12px;
      font-weight:700;
      font-size:18px;
    }
    header .brand .logo{
      width:36px;height:36px;border-radius:6px;background:linear-gradient(180deg,#153a8a,#0b3d91);
      display:flex;align-items:center;justify-content:center;color:#fff;
      box-shadow:0 1px 3px rgba(0,0,0,0.12);
    }
    .container{
      max-width:var(--max-width);
      margin:20px auto;
      display:grid;
      grid-template-columns: 240px 1fr;
      gap:20px;
      padding:0 12px;
    }
    /* Sidebar */
    nav.sidebar{
      background:var(--white);
      border-radius:var(--radius);
      padding:14px;
      box-shadow:var(--card-shadow);
      height:calc(100vh - 110px);
      position:sticky;
      top:86px;
      overflow:auto;
    }
    nav.sidebar a.menu{
      display:flex;
      align-items:center;
      gap:12px;
      padding:10px 8px;
      border-radius:6px;
      color:#111;
      text-decoration:none;
      margin-bottom:6px;
      font-weight:600;
    }
    nav.sidebar a.menu:hover{background:#f1f5fb}
    nav.sidebar .section-title{font-size:12px;color:var(--muted);margin:10px 6px}
    /* Main */
    main.card{
      background:var(--white);
      padding:16px;
      border-radius:var(--radius);
      box-shadow:var(--card-shadow);
      min-height:60vh;
    }
    .row{display:flex;gap:12px;flex-wrap:wrap}
    .card-small{
      background:linear-gradient(180deg,#fff,#f8fbff);
      padding:12px;border-radius:10px;flex:1;min-width:160px;
      box-shadow:0 1px 4px rgba(11,61,145,0.04);
    }
    .card-small h3{margin:0;font-size:20px;color:var(--navy)}
    .card-small p{margin:6px 0 0;color:var(--muted);font-size:13px}
    /* Table / list */
    .toolbar{display:flex;gap:10px;align-items:center;margin-bottom:12px;flex-wrap:wrap}
    .search{flex:1;display:flex}
    .search input{flex:1;padding:10px;border-radius:8px;border:1px solid #e6e9ef}
    .btn{display:inline-flex;align-items:center;gap:8px;padding:9px 12px;border-radius:8px;border:0;background:var(--navy);color:#fff;font-weight:600;cursor:pointer}
    .btn.ghost{background:transparent;color:var(--navy);border:1px solid rgba(11,61,145,0.08)}
    table{width:100%;border-collapse:collapse}
    table thead th{background:#fbfdff;color:var(--muted);text-align:left;padding:10px;border-bottom:1px solid #eef2f6;font-size:13px}
    table tbody td{padding:10px;border-bottom:1px solid #f3f5f8;font-size:14px}
    .badge{display:inline-block;padding:6px 8px;border-radius:999px;background:#eef6ff;color:var(--navy);font-weight:700;font-size:13px}
    .low{background:#fff3f2;color:var(--danger);border:1px solid rgba(217,83,79,0.08)}
    .status{padding:6px 8px;border-radius:6px;font-weight:700}
    .status.pending{background:#fffbee;color:#a07f00}
    .status.approved{background:#ecfbf3;color:var(--success)}
    /* form */
    label{display:block;font-size:13px;color:var(--muted);margin-bottom:6px}
    input[type="text"], input[type="number"], select, textarea{
      width:100%;padding:10px;border-radius:8px;border:1px solid #e6e9ef;background:#fff;
    }
    .form-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    .note{font-size:13px;color:var(--muted);margin-top:6px}
    /* responsive */
    @media (max-width:900px){
      .container{grid-template-columns:1fr; padding:0 12px}
      nav.sidebar{position:static;height:auto;display:flex;overflow:auto;flex-direction:row;gap:8px;padding:8px}
      nav.sidebar a.menu{padding:8px 10px;border-radius:8px;white-space:nowrap}
      header .brand{font-size:16px}
    }
  </style>
</head>
<body>
  <header class="topbar">
    <div class="brand">
      <div class="logo">สว</div>
      <div>
        ระบบบริหารจัดการพัสดุ<br/><small style="opacity:.9;font-weight:500">โรงเรียนวัดสังเวช</small>
      </div>
    </div>
    <div style="display:flex;gap:12px;align-items:center">
      <div id="userBox" style="color:#fff;font-weight:700">เจ้าหน้าที่พัสดุ</div>
      <button class="btn" onclick="logout()" style="background:#ff6b6b">ออกจากระบบ</button>
    </div>
  </header>

  <div class="container">
    <nav class="sidebar" aria-label="เมนูหลัก">
      <div class="section-title">การนำทาง</div>
      <a class="menu" href="#" onclick="nav('dashboard')">🏠 Dashboard</a>
      <a class="menu" href="#" onclick="nav('items')">📦 พัสดุ (รายการ)</a>
      <a class="menu" href="#" onclick="nav('requisition-new')">📝 ขอเบิกพัสดุ</a>
      <a class="menu" href="#" onclick="nav('my-requests')">🔎 คำขอของฉัน</a>
      <a class="menu" href="#" onclick="nav('approvals')">✅ จัดการการอนุมัติ</a>
      <a class="menu" href="#" onclick="nav('reports')">🧾 รายงาน</a>
      <div class="section-title">การจัดการ</div>
      <a class="menu" href="#" onclick="nav('personnel')">👥 บุคลากร</a>
      <a class="menu" href="#" onclick="nav('settings')">⚙️ ตั้งค่า</a>
    </nav>

    <main class="card" id="mainContent">
      <!-- dynamic content -->
      <div id="page-dashboard">
        <h2>สรุปภาพรวม</h2>
        <div class="row" style="margin-top:12px">
          <div class="card-small">
            <h3 id="totalItems">0</h3>
            <p>จำนวนพัสดุทั้งหมด</p>
          </div>
          <div class="card-small">
            <h3 id="pendingReq">0</h3>
            <p>คำขอรออนุมัติ</p>
          </div>
          <div class="card-small">
            <h3 id="lowStockCount">0</h3>
            <p>พัสดุใกล้หมด</p>
          </div>
        </div>

        <section style="margin-top:18px">
          <h3>Top 10 พัสดุที่ถูกเบิกบ่อย</h3>
          <div id="topItems" style="margin-top:8px"></div>
        </section>
      </div>

      <div id="page-items" style="display:none">
        <h2>พัสดุที่มีอยู่</h2>
        <div class="toolbar">
          <div class="search">
            <input id="searchInput" placeholder="ค้นหา (รหัส, ชื่อพัสดุ) ..." />
            <button class="btn ghost" style="margin-left:8px" onclick="resetFilters()">ล้าง</button>
          </div>
          <select id="categoryFilter" style="padding:10px;border-radius:8px;border:1px solid #e6e9ef">
            <option value="">ทุกหมวด</option>
          </select>
          <button class="btn" onclick="showNewItem()">+ เพิ่มพัสดุ</button>
        </div>

        <table>
          <thead>
            <tr><th>รหัส</th><th>ชื่อพัสดุ</th><th>หน่วย</th><th>คงเหลือ</th><th>ที่เก็บ</th><th>สถานะ</th><th></th></tr>
          </thead>
          <tbody id="itemsTable"></tbody>
        </table>
      </div>

      <div id="page-requisition-new" style="display:none">
        <h2>แบบฟอร์มขอเบิกพัสดุ</h2>
        <form id="requisitionForm" onsubmit="submitRequisition(event)">
          <div class="form-grid" style="margin-top:12px">
            <div>
              <label>ชื่อ-สกุลผู้ขอเบิก</label>
              <input type="text" id="reqName" value="น.ส. สมใจ ใจดี" readonly />
            </div>
            <div>
              <label>หน่วยงาน/สายชั้น/กลุ่มสาระ</label>
              <input type="text" id="reqDept" value="ครู/กลุ่มสาระคณิตศาสตร์" />
            </div>
          </div>

          <div style="margin-top:12px">
            <label>รายการพัสดุที่ต้องการเบิก</label>
            <div id="requisitionItems"></div>
            <button type="button" class="btn ghost" onclick="addReqItem()">+ เพิ่มรายการ</button>
          </div>

          <div style="margin-top:12px">
            <label>เหตุผลการขอเบิก</label>
            <textarea id="reqReason" rows="3" placeholder="เช่น ใช้สำหรับกิจกรรม/แผนการสอน ..."></textarea>
          </div>

          <div style="margin-top:12px;display:flex;gap:10px;align-items:center">
            <input type="file" id="reqAttachment" />
            <div class="note">สามารถแนบไฟล์ประกอบ (เช่น แผนการสอน)</div>
          </div>

          <div style="margin-top:12px">
            <button class="btn" type="submit">ส่งคำขอ</button>
            <button class="btn ghost" type="button" onclick="nav('my-requests')">ยกเลิก</button>
          </div>
        </form>
      </div>

      <div id="page-my-requests" style="display:none">
        <h2>คำขอของฉัน</h2>
        <table>
          <thead><tr><th>เลขที่คำขอ</th><th>วันที่</th><th>รายการ</th><th>สถานะ</th><th></th></tr></thead>
          <tbody id="myReqTable"></tbody>
        </table>
      </div>

      <div id="page-approvals" style="display:none">
        <h2>จัดการการอนุมัติ (สำหรับ Admin)</h2>
        <div class="note">รายการคำขอที่รออนุมัติ</div>
        <table style="margin-top:12px">
          <thead><tr><th>เลขที่</th><th>ผู้ขอ</th><th>รายการ</th><th>สถานะ</th><th>การกระทำ</th></tr></thead>
          <tbody id="pendingReqTable"></tbody>
        </table>
      </div>

      <div id="page-reports" style="display:none">
        <h2>รายงาน</h2>
        <div class="toolbar" style="margin-top:12px">
          <input type="date" id="fromDate" />
          <input type="date" id="toDate" />
          <select id="reportCategory"><option value="">ทุกหมวด</option></select>
          <button class="btn" onclick="generateReport()">Export Excel</button>
        </div>
        <div class="note" style="margin-top:8px">ตัวอย่าง: รายงานการเบิกแยกตามบุคลากร / หมวดหมู่ / วันที่</div>
      </div>

      <div id="page-personnel" style="display:none">
        <h2>บุคลากร</h2>
        <div class="toolbar" style="margin-top:12px">
          <input id="personSearch" placeholder="ค้นหาชื่อ/หน่วยงาน" />
          <button class="btn" onclick="showAddPerson()">+ เพิ่มบุคลากร</button>
        </div>
        <table style="margin-top:12px">
          <thead><tr><th>ชื่อ-สกุล</th><th>ตำแหน่ง</th><th>หน่วยงาน</th><th>สิทธิ์</th></tr></thead>
          <tbody id="personTable"></tbody>
        </table>
      </div>

    </main>
  </div>

  <!-- Simple modal area for Add Item -->
  <div id="modalArea" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,0.45);align-items:center;justify-content:center;padding:20px">
    <div style="background:#fff;border-radius:10px;max-width:640px;width:100%;padding:18px;box-shadow:0 12px 40px rgba(0,0,0,0.25)">
      <h3 id="modalTitle">เพิ่มพัสดุ</h3>
      <form id="itemForm" onsubmit="saveItem(event)">
        <div class="form-grid">
          <div>
            <label>รหัสพัสดุ</label>
            <input type="text" id="itemCode" />
          </div>
          <div>
            <label>ชื่อพัสดุ</label>
            <input type="text" id="itemName" />
          </div>
        </div>
        <div class="form-grid" style="margin-top:10px">
          <div>
            <label>หมวดหมู่</label>
            <select id="itemCategory"></select>
          </div>
          <div>
            <label>หน่วยนับ</label>
            <input type="text" id="itemUnit" value="ชิ้น" />
          </div>
        </div>
        <div class="form-grid" style="margin-top:10px">
          <div>
            <label>จำนวนเริ่มต้น</label>
            <input type="number" id="itemQty" value="0" />
          </div>
          <div>
            <label>จำนวนขั้นต่ำที่ควรมี</label>
            <input type="number" id="itemMin" value="5" />
          </div>
        </div>
        <div style="margin-top:10px">
          <label>สถานที่จัดเก็บ</label>
          <input type="text" id="itemLocation" />
        </div>
        <div style="margin-top:12px;display:flex;gap:8px;justify-content:flex-end">
          <button class="btn" type="submit">บันทึก</button>
          <button class="btn ghost" type="button" onclick="closeModal()">ยกเลิก</button>
        </div>
      </form>
    </div>
  </div>

  <script>
    /* Demo data (local, frontend-only) */
    const categories = [
      {id:1,name:"สื่อการสอน"},
      {id:2,name:"อุปกรณ์สำนักงาน"},
      {id:3,name:"เครื่องคอมพิวเตอร์"},
      {id:4,name:"วัสดุทำความสะอาด"}
    ];
    let items = [
      {id:1,code:"MAT-001",name:"กระดาษ A4",category_id:2,unit:"แพ็ค",quantity:50,min_quantity:10,location:"คลังกลาง"},
      {id:2,code:"TEA-101",name:"โปรเจคเตอร์ (ยืม)",category_id:3,unit:"เครื่อง",quantity:2,min_quantity:1,location:"ห้องมัลติมีเดีย"},
      {id:3,code:"MAT-010",name:"ปากกาเคมีสีดำ",category_id:2,unit:"กล่อง",quantity:8,min_quantity:10,location:"คลังกลาง"},
      {id:4,code:"CLEAN-01",name:"น้ำยาล้างพื้น",category_id:4,unit:"ลิตร",quantity:25,min_quantity:5,location:"คลังทำความสะอาด"},
      {id:5,code:"EDU-02",name:"หนังสือแบบฝึกหัด",category_id:1,unit:"เล่ม",quantity:120,min_quantity:20,location:"คลังหนังสือ"}
    ];
    let requisitions = [
      {id:1,requisition_no:"REQ-2025-0001",requester:"น.ส. สมใจ ใจดี",department:"กลุ่มสาระคณิตศาสตร์",items:[{name:"กระดาษ A4",qty:2}],status:"approved",created_at:"2025-11-10"},
      {id:2,requisition_no:"REQ-2025-0002",requester:"นาย ทดสอบ",department:"ฝ่ายบริหาร",items:[{name:"ปากกาเคมีสีดำ",qty:1}],status:"pending",created_at:"2025-11-22"}
    ];
    let users = [
      {id:1,username:"admin",full_name:"เจ้าหน้าที่พัสดุ",role:"admin"},
      {id:2,username:"teacher1",full_name:"น.ส. สมใจ ใจดี",role:"staff"}
    ];

    /* Initialize UI */
    function init(){
      populateCategoryFilters();
      renderDashboard();
      renderItems();
      renderMyRequests();
      renderPendingApprovals();
      populatePersonnel();
      document.getElementById('searchInput').addEventListener('input', renderItems);
    }
    function nav(page){
      const pages = ['dashboard','items','requisition-new','my-requests','approvals','reports','personnel','settings'];
      pages.forEach(p=>{
        const el = document.getElementById('page-'+p.replace('-','-'));
        if(el) el.style.display = 'none';
      });
      const active = document.getElementById('page-'+page);
      if(active) active.style.display = 'block';
      // special cases
      if(page==='items'){renderItems();}
      if(page==='dashboard'){renderDashboard();}
    }
    function populateCategoryFilters(){
      const cf = document.getElementById('categoryFilter');
      const rc = document.getElementById('reportCategory');
      categories.forEach(c=>{
        const o=document.createElement('option');o.value=c.id;o.textContent=c.name;cf.appendChild(o);
        const o2=document.createElement('option');o2.value=c.id;o2.textContent=c.name;rc.appendChild(o2);
      });
      const ic = document.getElementById('itemCategory');
      categories.forEach(c=>{const o=document.createElement('option');o.value=c.id;o.textContent=c.name;ic.appendChild(o)})
    }

    function renderDashboard(){
      document.getElementById('totalItems').textContent = items.length;
      const pending = requisitions.filter(r=>r.status==="pending").length;
      document.getElementById('pendingReq').textContent = pending;
      const low = items.filter(i=>i.quantity <= i.min_quantity).length;
      document.getElementById('lowStockCount').textContent = low;
      // top items (most issued) — demo: sort by id
      const topDiv = document.getElementById('topItems'); topDiv.innerHTML='';
      items.slice(0,5).forEach(it=>{
        const d=document.createElement('div');d.style.padding='8px 10px';d.style.borderBottom='1px solid #f3f5f8';
        d.innerHTML = `<strong>${it.name}</strong> <div class="note">คงเหลือ ${it.quantity} ${it.unit}</div>`;
        topDiv.appendChild(d);
      })
    }

    function renderItems(){
      const q = document.getElementById('searchInput').value.trim().toLowerCase();
      const cat = document.getElementById('categoryFilter').value;
      const tbody = document.getElementById('itemsTable'); tbody.innerHTML='';
      items.filter(it=>{
        if(q && !(it.name.toLowerCase().includes(q) || it.code.toLowerCase().includes(q))) return false;
        if(cat && String(it.category_id)!==String(cat)) return false;
        return true;
      }).forEach(it=>{
        const tr = document.createElement('tr');
        const catName = categories.find(c=>c.id===it.category_id)?.name || '-';
        tr.innerHTML = `<td>${it.code}</td><td>${it.name}<div class="note">${catName}</div></td><td>${it.unit}</td><td>${it.quantity}</td><td>${it.location}</td><td>${it.quantity<=it.min_quantity?'<span class="badge low">ใกล้หมด</span>':'<span class="badge">ปกติ</span>'}</td><td><button class="btn ghost" onclick="editItem(${it.id})">แก้ไข</button></td>`;
        tbody.appendChild(tr);
      })
    }

    function showNewItem(){
      document.getElementById('modalTitle').textContent='เพิ่มพัสดุ';
      document.getElementById('itemForm').dataset.editId = '';
      document.getElementById('itemCode').value='';
      document.getElementById('itemName').value='';
      document.getElementById('itemQty').value=0;
      document.getElementById('itemMin').value=5;
      document.getElementById('itemUnit').value='ชิ้น';
      document.getElementById('itemLocation').value='';
      showModal();
    }
    function editItem(id){
      const it = items.find(i=>i.id===id); if(!it) return alert('ไม่พบรายการ');
      document.getElementById('modalTitle').textContent='แก้ไขพัสดุ';
      document.getElementById('itemForm').dataset.editId = id;
      document.getElementById('itemCode').value=it.code;
      document.getElementById('itemName').value=it.name;
      document.getElementById('itemQty').value=it.quantity;
      document.getElementById('itemMin').value=it.min_quantity;
      document.getElementById('itemUnit').value=it.unit;
      document.getElementById('itemLocation').value=it.location;
      document.getElementById('itemCategory').value=it.category_id;
      showModal();
    }
    function saveItem(e){
      e.preventDefault();
      const editId = e.target.dataset.editId;
      const data = {
        code: document.getElementById('itemCode').value.trim(),
        name: document.getElementById('itemName').value.trim(),
        quantity: Number(document.getElementById('itemQty').value||0),
        min_quantity: Number(document.getElementById('itemMin').value||0),
        unit: document.getElementById('itemUnit').value.trim(),
        location: document.getElementById('itemLocation').value.trim(),
        category_id: Number(document.getElementById('itemCategory').value||1)
      };
      if(!data.name || !data.code) return alert('กรุณากรอก รหัส และชื่อพัสดุ');
      if(editId){
        const it = items.find(i=>i.id==editId);
        Object.assign(it,data);
      } else {
        data.id = items.length ? Math.max(...items.map(i=>i.id))+1 : 1;
        items.push(data);
      }
      closeModal(); renderItems(); renderDashboard();
    }
    function showModal(){document.getElementById('modalArea').style.display='flex'}
    function closeModal(){document.getElementById('modalArea').style.display='none'}

    function addReqItem(){
      const container = document.getElementById('requisitionItems');
      const idx = container.children.length;
      const div = document.createElement('div'); div.style.display='flex'; div.style.gap='8px'; div.style.marginTop='8px';
      const sel = document.createElement('select'); sel.style.flex='1'; sel.innerHTML = '<option value="">-- เลือกพัสดุ --</option>';
      items.forEach(it=>{const o=document.createElement('option');o.value=it.id;o.textContent=`${it.name} (คง ${it.quantity} ${it.unit})`;sel.appendChild(o)});
      const qty = document.createElement('input'); qty.type='number'; qty.style.width='120px'; qty.placeholder='จำนวน';
      const btn = document.createElement('button'); btn.className='btn ghost'; btn.type='button'; btn.textContent='ลบ'; btn.onclick=()=>div.remove();
      div.appendChild(sel); div.appendChild(qty); div.appendChild(btn); container.appendChild(div);
    }

    function submitRequisition(e){
      e.preventDefault();
      const nodes = Array.from(document.getElementById('requisitionItems').children);
      if(nodes.length===0) return alert('กรุณาเพิ่มรายการที่ต้องการเบิกอย่างน้อย 1 รายการ');
      const reqItems=[];
      for(const n of nodes){
        const sel = n.querySelector('select'); const qty = n.querySelector('input[type="number"]');
        if(!sel.value || !qty.value) return alert('กรุณาเลือกพัสดุและระบุจำนวนทุกแถว');
        const it = items.find(x=>x.id==sel.value);
        reqItems.push({item_id: it.id, name: it.name, qty: Number(qty.value)});
      }
      // generate auto req no
      const newNo = 'REQ-2025-'+String(requisitions.length+1).padStart(4,'0');
      requisitions.push({
        id:requisitions.length+1,
        requisition_no:newNo,
        requester:document.getElementById('reqName').value,
        department:document.getElementById('reqDept').value,
        items:reqItems,
        status:'pending',
        created_at:new Date().toISOString().slice(0,10)
      });
      alert('ส่งคำขอเรียบร้อย รหัสคำขอ: '+newNo);
      // reset form
      document.getElementById('requisitionItems').innerHTML='';
      document.getElementById('reqReason').value='';
      renderMyRequests(); renderPendingApprovals(); nav('my-requests');
    }

    function renderMyRequests(){
      const tbody = document.getElementById('myReqTable'); tbody.innerHTML='';
      const my = requisitions.filter(r=>r.requester.includes('สมใจ') || true); // demo: show all for now
      my.forEach(r=>{
        const tr=document.createElement('tr');
        tr.innerHTML = `<td>${r.requisition_no}</td><td>${r.created_at}</td><td>${r.items.map(i=>i.name+' x'+i.qty).join(', ')}</td><td><span class="status ${r.status==='pending'?'pending':'approved'}">${r.status}</span></td><td><button class="btn ghost" onclick="viewReq('${r.requisition_no}')">รายละเอียด</button></td>`;
        tbody.appendChild(tr);
      })
    }
    function viewReq(no){ const r = requisitions.find(x=>x.requisition_no===no); if(!r) return;
      alert('เลขที่: '+r.requisition_no+'\nผู้ขอ: '+r.requester+'\nสถานะ: '+r.status+'\nรายการ: '+r.items.map(i=>i.name+' x'+i.qty).join('\\n'));
    }

    function renderPendingApprovals(){
      const tbody = document.getElementById('pendingReqTable'); tbody.innerHTML='';
      const pending = requisitions.filter(r=>r.status==='pending');
      pending.forEach(r=>{
        const tr=document.createElement('tr');
        tr.innerHTML = `<td>${r.requisition_no}</td><td>${r.requester}</td><td>${r.items.map(i=>i.name+' x'+i.qty).join(', ')}</td><td><span class="status pending">รออนุมัติ</span></td><td><button class="btn" onclick="approveReq(${r.id}, true)">อนุมัติ</button><button class="btn ghost" style="margin-left:8px" onclick="approveReq(${r.id}, false)">ไม่อนุมัติ</button></td>`;
        tbody.appendChild(tr);
      })
    }
    function approveReq(id, approved){
      const r = requisitions.find(x=>x.id===id); if(!r) return;
      if(!approved){
        const reason = prompt('ระบุเหตุผลที่ไม่อนุมัติ');
        if(!reason) return;
        r.status='rejected';
      } else {
        // decrease stock demo
        r.items.forEach(itm=>{
          const item = items.find(x=>x.id===itm.item_id);
          if(item) item.quantity = Math.max(0, item.quantity - itm.qty);
        });
        r.status='approved';
      }
      renderPendingApprovals(); renderItems(); renderDashboard(); renderMyRequests();
      alert('อัพเดตสถานะเรียบร้อย');
    }

    function resetFilters(){
      document.getElementById('searchInput').value='';
      document.getElementById('categoryFilter').value='';
      renderItems();
    }

    function populatePersonnel(){
      const tbody = document.getElementById('personTable'); tbody.innerHTML='';
      users.forEach(u=>{
        const tr=document.createElement('tr');
        tr.innerHTML=`<td>${u.full_name}</td><td>${u.role==='admin'?'เจ้าหน้าที่พัสดุ':u.role==='staff'?'บุคลากร':'ผู้บริหาร'}</td><td>-</td><td>${u.role}</td>`;
        tbody.appendChild(tr);
      })
    }

    function showAddPerson(){ alert('หน้าจอเพิ่มบุคลากร (ตัวอย่าง)') }
    function generateReport(){ alert('สร้างรายงาน Excel (ตัวอย่าง)') }
    function logout(){ alert('ออกจากระบบ'); /* redirect to login page */ }

    window.addEventListener('load', init);
  </script>
</body>
</html>
