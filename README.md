

<!doctype html>
<html lang="hi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0" />
  <title>91 Club — मोबाइल बजट टूल</title>
  <meta name="description" content="91 Club के यूज़र्स के लिए मोबाइल-फ्रेंडली बजट/अलोकेशन टूल (Hindi)." />
  <style>
    :root{
      --bg:#0f172a; --card:#ffffff; --muted:#94a3b8; --accent:#06b6d4; --glass:rgba(6,182,212,0.12);
      --success:#16a34a; --danger:#ef4444; --maxw:760px;
      font-family: "Segoe UI", Roboto, "Noto Sans", Arial, sans-serif;
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;background:linear-gradient(180deg,#07122a 0%, #042033 100%); color:var(--card);}
    .wrap{max-width:var(--maxw);margin:12px auto;padding:14px;}
    header{display:flex;align-items:center;gap:12px;margin-bottom:12px}
    h1{font-size:18px;margin:0}
    .subtitle{font-size:13px;color:rgba(255,255,255,0.78)}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.05), rgba(255,255,255,0.02)); border-radius:14px;padding:14px;box-shadow:0 6px 24px rgba(2,6,23,0.6);}
    label{display:block;font-size:13px;color:var(--muted);margin-bottom:6px}
    input[type="number"], input[type="text"], select {
      width:100%;padding:10px;border-radius:10px;border:0;background:rgba(255,255,255,0.04); color:var(--card);font-size:15px;
    }
    .top-row{display:flex;gap:8px;align-items:center;margin-bottom:12px}
    .top-row > *{flex:1}
    .add-btn{background:transparent;border:1px dashed rgba(255,255,255,0.08); padding:10px;border-radius:10px;color:var(--accent);cursor:pointer}
    .list{margin-top:10px;display:grid;gap:8px}
    .item{display:grid;grid-template-columns: 1fr auto auto;gap:8px;align-items:center;padding:10px;border-radius:10px;background:linear-gradient(90deg, rgba(255,255,255,0.02), transparent);}
    .iname{font-weight:600;font-size:15px;color:var(--card);margin-bottom:6px}
    .small{font-size:13px;color:var(--muted)}
    .pill{background:var(--glass);padding:6px 8px;border-radius:999px;font-size:13px;color:var(--card);min-width:80px;text-align:center}
    .controls{display:flex;gap:8px;align-items:center}
    .btn{background:var(--accent);color:#042033;border:0;padding:10px 12px;border-radius:10px;font-weight:600;cursor:pointer}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--card)}
    .summary{display:flex;gap:12px;align-items:center;margin-top:12px;flex-wrap:wrap}
    .tile{flex:1;min-width:140px;padding:10px;border-radius:10px;background:rgba(255,255,255,0.02)}
    .big{font-size:16px;font-weight:700}
    .right{text-align:right}
    footer{margin-top:14px;display:flex;gap:8px;align-items:center;justify-content:space-between;flex-wrap:wrap}
    .open-club{width:100%;padding:12px;border-radius:12px;border:0;font-weight:700;font-size:16px;background:linear-gradient(90deg,var(--accent),#0ea5a4);color:#042033;cursor:pointer}
    .muted{font-size:13px;color:var(--muted)}
    .danger{color:var(--danger);font-weight:700}
    .success{color:var(--success);font-weight:700}
    @media (max-width:520px){
      .item{grid-template-columns: 1fr 120px 100px}
    }
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div>
        <h1>91 Club — Budget Tool</h1>
        <div class="subtitle">कहाँ कितना पैसा लग रहा है — मोबाइल फ्रेंडली</div>
      </div>
      <div style="text-align:right">
        <div class="small muted">Offline-friendly</div>
      </div>
    </header>

    <main class="card" role="main" aria-live="polite">
      <div class="top-row">
        <div>
          <label for="total">कुल बजट (₹)</label>
          <input id="total" type="number" min="0" step="0.01" value="10000" />
        </div>
        <div style="width:120px">
          <label for="mode">मोड</label>
          <select id="mode">
            <option value="mixed">मिक्स्ड</option>
            <option value="amount">Amount only</option>
            <option value="percent">Percent only</option>
          </select>
        </div>
      </div>

      <div style="display:flex;gap:8px;align-items:center;margin-bottom:8px">
        <button id="add" class="add-btn">+ नई कैटेगरी</button>
        <button id="importSample" class="btn ghost">Sample भरो</button>
        <div style="flex:1"></div>
        <button id="exportCsv" class="btn ghost">CSV डाउनलोड</button>
        <button id="shareBtn" class="btn">शेयर</button>
      </div>

      <div class="list" id="list">
        <!-- categories -->
      </div>

      <div class="summary" aria-hidden="false">
        <div class="tile">
          <div class="small">कुल आवंटित</div>
          <div class="big" id="sumAmount">₹0.00</div>
        </div>
        <div class="tile">
          <div class="small">कुल प्रतिशत</div>
          <div class="big" id="sumPercent">0.00%</div>
        </div>
        <div class="tile right">
          <div class="small">बैलेंस</div>
          <div class="big" id="balance">—</div>
        </div>
      </div>

      <div style="margin-top:12px" class="muted small">
        नोट: Amount या Percent में से किसी एक को भरें; दूसरा फील्ड ऑटो-पॉप्युलेट होगा। मोबाइल पर शेयर बटन से लोग लिंक/CSV भेज सकेंगे।
      </div>
    </main>

    <footer>
      <div style="flex:1">
        <div class="muted small">91 Club खोलने के लिए नीचे बटन का प्रयोग करें</div>
      </div>
      <div style="flex-basis:320px">
        <button id="openClub" class="open-club">91 Club खोलें</button>
      </div>
    </footer>
  </div>

  <script>
    // --- CONFIG: अपना 91 Club URL/APP-Scheme यहाँ बदलें ---
    const clubUrl = 'https://91club.com/';           // वेब fallback link
    const clubAppScheme = '91club://home';           // अगर ऐप का custom URL scheme होता है (उदाहरण)
    // -----------------------------------------------------

    // Default sample categories
    const sample = [
      {name: 'खाना', amount: 3000, percent: null},
      {name: 'रेंट / EMI', amount: 2500, percent: null},
      {name: 'बिजली/इंटरनेट', amount: 800, percent: null},
      {name: 'बचत', amount: 1500, percent: null},
      {name: 'मनोरंजन', amount: 1200, percent: null}
    ];

    const totalEl = document.getElementById('total');
    const listEl = document.getElementById('list');
    const addBtn = document.getElementById('add');
    const importSampleBtn = document.getElementById('importSample');
    const modeEl = document.getElementById('mode');
    const sumAmountEl = document.getElementById('sumAmount');
    const sumPercentEl = document.getElementById('sumPercent');
    const balanceEl = document.getElementById('balance');
    const exportCsvBtn = document.getElementById('exportCsv');
    const shareBtn = document.getElementById('shareBtn');
    const openClubBtn = document.getElementById('openClub');

    let cats = [];

    function fmtMoney(v){ return '₹' + Number(v||0).toLocaleString('en-IN',{minimumFractionDigits:2,maximumFractionDigits:2}); }
    function fmtPct(v){ return Number(v||0).toFixed(2) + '%'; }

    function render(){
      listEl.innerHTML = '';
      cats.forEach((c, idx) => {
        const item = document.createElement('div');
        item.className = 'item';
        item.innerHTML = `
          <div>
            <div class="iname" contenteditable="true" data-idx="${idx}" data-field="name">${escapeHtml(c.name)}</div>
            <div class="small muted">Tap name to edit</div>
          </div>
          <div>
            <label class="small muted">Amount (₹)</label>
            <input type="number" data-idx="${idx}" data-field="amount" min="0" step="0.01" value="${c.amount!=null?Number(c.amount).toFixed(2):''}" />
          </div>
          <div>
            <label class="small muted">Percent (%)</label>
            <input type="number" data-idx="${idx}" data-field="percent" min="0" max="100" step="0.01" value="${c.percent!=null?Number(c.percent).toFixed(2):''}" />
          </div>
        `;
        // context menu: long press to delete? simple double-click delete name
        listEl.appendChild(item);
      });

      attachListeners();
      recalcAll();
    }

    function attachListeners(){
      // name edits
      document.querySelectorAll('[data-field="name"]').forEach(el=>{
        el.addEventListener('input', (e)=>{
          const idx = Number(el.getAttribute('data-idx'));
          cats[idx].name = el.textContent.trim();
        });
        el.addEventListener('dblclick', (e)=>{
          // double click to delete category
          if(confirm('क्या आप इस कैटेगरी को हटाना चाहते हैं?')) {
            const idx = Number(el.getAttribute('data-idx'));
            cats.splice(idx,1);
            render();
          }
        });
      });

      // number inputs
      document.querySelectorAll('input[data-field]').forEach(el=>{
        el.addEventListener('input', (e)=>{
          const idx = Number(el.getAttribute('data-idx'));
          const field = el.getAttribute('data-field');
          const val = el.value === '' ? null : Number(el.value);
          cats[idx][field] = val;
          // auto-calc other if possible
          if(field === 'amount'){
            if(modeEl.value === 'amount'){ cats[idx].percent = null; }
            else if (modeEl.value === 'percent'){ cats[idx].percent = totalEl.value ? (Number(val)/Number(totalEl.value))*100 : null; }
            else {
              cats[idx].percent = totalEl.value ? (Number(val||0)/Number(totalEl.value))*100 : null;
            }
          } else if(field === 'percent'){
            if(modeEl.value === 'percent'){ cats[idx].amount = null; }
            else if (modeEl.value === 'amount'){ cats[idx].amount = totalEl.value ? (Number(val)/100)*Number(totalEl.value) : null; }
            else {
              cats[idx].amount = totalEl.value ? (Number(val||0)/100)*Number(totalEl.value) : null;
            }
          }
          render(); // re-render to update values cleanly
        });
      });
    }

    function recalcAll(){
      const total = Number(totalEl.value) || 0;
      if(modeEl.value === 'percent'){
        cats.forEach(c=>{
          c.amount = c.percent!=null ? (Number(c.percent)/100)*total : null;
        });
      } else if(modeEl.value === 'amount'){
        cats.forEach(c=>{
          c.percent = c.amount!=null && total>0 ? (Number(c.amount)/total)*100 : null;
        });
      } else {
        cats.forEach(c=>{
          if((c.amount==null || c.amount==='') && (c.percent!=null && c.percent!=='')) {
            c.amount = total * (Number(c.percent)/100);
          } else if ((c.percent==null || c.percent==='') && (c.amount!=null && c.amount!=='')) {
            c.percent = total>0 ? (Number(c.amount)/total)*100 : null;
          }
        });
      }

      const sumAmount = cats.reduce((s,c)=> s + (Number(c.amount)||0), 0);
      const sumPercent = cats.reduce((s,c)=> s + (Number(c.percent)||0), 0);

      sumAmountEl.textContent = fmtMoney(sumAmount);
      sumPercentEl.textContent = fmtPct(sumPercent);

      const diff = Number(total) - sumAmount;
      if(Math.abs(diff) < 0.005){
        balanceEl.innerHTML = `<span class="success">सही मेल — आवंटन पूरा ✔</span>`;
      } else if (diff > 0){
        balanceEl.innerHTML = `<span>Remaining: ${fmtMoney(diff)}</span>`;
      } else {
        balanceEl.innerHTML = `<span class="danger">Over by: ${fmtMoney(Math.abs(diff))}</span>`;
      }
    }

    // helper
    function escapeHtml(s){ return String(s||'').replace(/[&<>"]/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c])); }

    // events
    addBtn.addEventListener('click', ()=>{
      cats.push({name:'नई कैटेगरी', amount:null, percent:null});
      render();
      // focus last name (allow slight delay)
      setTimeout(()=> {
        const names = document.querySelectorAll('[data-field="name"]');
        if(names.length) names[names.length-1].focus();
      }, 50);
    });

    importSampleBtn.addEventListener('click', ()=>{
      if(confirm('Sample कैटेगरी जोड़ें? (अभी की सूची मिट जाएगी)')) {
        cats = JSON.parse(JSON.stringify(sample));
        render();
      }
    });

    totalEl.addEventListener('input', ()=> render());
    modeEl.addEventListener('change', ()=> {
      // clear conflicting fields depending on mode
      if(modeEl.value === 'amount') { cats.forEach(c=> c.percent = null); }
      if(modeEl.value === 'percent') { cats.forEach(c=> c.amount = null); }
      render();
    });

    exportCsvBtn.addEventListener('click', ()=>{
      const header = ['Category','Amount (INR)','Percent (%)'];
      let csv = header.join(',') + '\\n';
      cats.forEach(c=>{
        csv += `"${(c.name||'')}",${(Number(c.amount||0).toFixed(2))},${(Number(c.percent||0).toFixed(2))}\\n`;
      });
      const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'allocation_91club.csv';
      document.body.appendChild(a);
      a.click();
      a.remove();
      URL.revokeObjectURL(url);
    });

    shareBtn.addEventListener('click', async ()=>{
      const total = Number(totalEl.value) || 0;
      let text = `91 Club Budget — कुल: ${fmtMoney(total)}\\n`;
      cats.forEach(c=>{
        text += `${c.name || '-'}: ${fmtMoney(Number(c.amount||0))} (${fmtPct(Number(c.percent||0))})\\n`;
      });
      text += '\\nOpen: ' + clubUrl;
      if(navigator.share){
        try{
          await navigator.share({title:'91 Club Budget', text});
        }catch(e){
          alert('Share रद्द हुआ।');
        }
      } else {
        // fallback: copy to clipboard
        try{
          await navigator.clipboard.writeText(text);
          alert('टेक्स्ट क्लिपबोर्ड में कॉपी हुआ — अब आप उसे 91 Club पर पेस्ट कर सकते हैं।');
        }catch(e){
          prompt('Copy this text manually:', text);
        }
      }
    });

    // Open 91 Club — try app scheme, then fallback to web
    openClubBtn.addEventListener('click', ()=>{
      // first attempt with custom scheme
      const now = Date.now();
      const timeout = 1200;
      let opened = false;

      // If custom scheme blank, just go to web
      if(!clubAppScheme || clubAppScheme === ''){
        window.location.href = clubUrl;
        return;
      }

      // create iframe trick for iOS/older
      const iframe = document.createElement('iframe');
      iframe.style.display = 'none';
      iframe.src = clubAppScheme;
      document.body.appendChild(iframe);

      // fallback timer
      setTimeout(()=> {
        document.body.removeChild(iframe);
        // if user still on page, open web fallback
        window.location.href = clubUrl;
      }, timeout);
    });

    // Initialize with sample
    cats = JSON.parse(JSON.stringify(sample));
    render();

    // Recalc interval to keep numbers updated (in case of external edits)
    setInterval(recalcAll, 600);

  </script>
</body>
</html>
