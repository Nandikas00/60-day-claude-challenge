# Today I built a Verdict Engine using claude:

## Key Learnings :
- Learned how AI can evaluate complex scenarios by analyzing evidence, arguments, and multiple perspectives before generating a reasoned verdict.
- Gained practical experience in designing structured decision-making workflows that prioritize logic, transparency, and explainability over simple AI-generated responses.
- Explored prompt engineering techniques to guide AI in comparing evidence, identifying inconsistencies, and producing balanced conclusions.
- Understood the importance of confidence scoring, reasoning paths, and evidence-based justification in building trustworthy AI systems.
- Learned how AI can assist in risk assessment, conflict resolution, and objective analysis by reducing bias and organizing information effectively.
- Improved frontend development skills by creating an interactive dashboard with verdict summaries, evidence visualization, confidence indicators, and detailed reasoning reports.
- Practiced designing user-centric interfaces that present complex AI analysis in a clear, understandable, and actionable format.
- Strengthened understanding of how explainable AI improves user trust by making every recommendation transparent and supported by evidence.

### Output Screenshots :
<img width="1144" height="873" alt="Screenshot (678)" src="https://github.com/user-attachments/assets/01807dba-fe57-4164-85be-817ada61238c" />
<img width="1248" height="869" alt="Screenshot (677)" src="https://github.com/user-attachments/assets/ef4177af-866d-41e8-8e6b-849a31fc2a9c" />

#### HTML File :
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Flagship Value Finder — iPhone 16 vs Galaxy S25 vs Pixel 9 vs OnePlus 13</title>
<style>
  :root{
    --ink:#1c2521;
    --paper:#f6f3ec;
    --panel:#ffffff;
    --line:#dcd5c4;
    --moss:#3c5c48;
    --moss-dark:#26382d;
    --clay:#af5a3a;
    --gold:#c99a3a;
    --muted:#6b6558;
    --good:#3c5c48;
    --warn:#af5a3a;
    --mono: 'IBM Plex Mono', 'Courier New', monospace;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:var(--paper);
    color:var(--ink);
    font-family: Georgia, 'Iowan Old Style', serif;
    line-height:1.5;
    -webkit-font-smoothing:antialiased;
  }
  .wrap{max-width:1180px;margin:0 auto;padding:32px 24px 80px;}

  /* header */
  header{
    display:flex;
    justify-content:space-between;
    align-items:flex-end;
    gap:24px;
    border-bottom:3px solid var(--ink);
    padding-bottom:18px;
    margin-bottom:28px;
    flex-wrap:wrap;
  }
  .eyebrow{
    font-family:var(--mono);
    text-transform:uppercase;
    letter-spacing:.14em;
    font-size:11px;
    color:var(--clay);
    margin-bottom:6px;
  }
  h1{
    font-size:clamp(28px,4vw,42px);
    margin:0;
    font-weight:700;
    letter-spacing:-0.01em;
  }
  .subtitle{
    max-width:420px;
    font-size:14px;
    color:var(--muted);
    font-family:var(--mono);
    line-height:1.6;
  }

  /* layout */
  .grid{
    display:grid;
    grid-template-columns: 300px 1fr;
    gap:28px;
  }
  @media (max-width:900px){
    .grid{grid-template-columns:1fr;}
  }

  /* weight panel */
  .panel{
    background:var(--panel);
    border:1px solid var(--line);
    border-radius:2px;
  }
  .weights{
    padding:22px;
    position:sticky;
    top:20px;
    align-self:start;
  }
  .weights h2{
    font-size:13px;
    text-transform:uppercase;
    letter-spacing:.1em;
    font-family:var(--mono);
    margin:0 0 4px;
  }
  .weights p.hint{
    font-size:12px;
    color:var(--muted);
    margin:0 0 18px;
    font-family:var(--mono);
  }
  .criterion{margin-bottom:16px;}
  .criterion label{
    display:flex;
    justify-content:space-between;
    font-size:13px;
    font-weight:700;
    margin-bottom:6px;
  }
  .criterion .val{
    font-family:var(--mono);
    color:var(--moss);
    font-weight:700;
  }
  input[type=range]{
    -webkit-appearance:none;
    width:100%;
    height:4px;
    background:var(--line);
    border-radius:2px;
    outline:none;
  }
  input[type=range]::-webkit-slider-thumb{
    -webkit-appearance:none;
    width:16px;height:16px;
    border-radius:50%;
    background:var(--moss);
    cursor:pointer;
    border:2px solid var(--panel);
    box-shadow:0 0 0 1px var(--moss);
  }
  input[type=range]::-moz-range-thumb{
    width:14px;height:14px;
    border-radius:50%;
    background:var(--moss);
    cursor:pointer;
    border:2px solid var(--panel);
  }
  .weight-total{
    margin-top:14px;
    padding-top:14px;
    border-top:1px dashed var(--line);
    font-family:var(--mono);
    font-size:12px;
    color:var(--muted);
    display:flex;
    justify-content:space-between;
  }
  .reset-btn{
    margin-top:14px;
    width:100%;
    background:var(--ink);
    color:var(--paper);
    border:none;
    padding:9px;
    font-family:var(--mono);
    font-size:11px;
    text-transform:uppercase;
    letter-spacing:.08em;
    cursor:pointer;
    border-radius:2px;
  }
  .reset-btn:hover{background:var(--moss-dark);}
  .preset-row{display:flex;gap:6px;margin-top:10px;flex-wrap:wrap;}
  .preset-btn{
    flex:1;
    min-width:80px;
    background:var(--paper);
    border:1px solid var(--line);
    padding:6px 4px;
    font-family:var(--mono);
    font-size:10px;
    cursor:pointer;
    border-radius:2px;
    color:var(--ink);
  }
  .preset-btn:hover{border-color:var(--moss);color:var(--moss);}

  /* results */
  .results{padding:22px;}
  .results h2{
    font-size:13px;
    text-transform:uppercase;
    letter-spacing:.1em;
    font-family:var(--mono);
    margin:0 0 18px;
  }
  .rank-row{
    display:grid;
    grid-template-columns: 34px 1fr 90px;
    align-items:center;
    gap:14px;
    padding:14px 0;
    border-bottom:1px solid var(--line);
  }
  .rank-row:last-child{border-bottom:none;}
  .rank-num{
    font-family:var(--mono);
    font-size:20px;
    font-weight:700;
    color:var(--muted);
  }
  .rank-row.first .rank-num{color:var(--gold);}
  .phone-name{font-size:17px;font-weight:700;}
  .phone-sub{font-size:12px;color:var(--muted);font-family:var(--mono);margin-top:2px;}
  .bar-track{
    height:8px;
    background:var(--line);
    border-radius:4px;
    overflow:hidden;
    margin-top:8px;
  }
  .bar-fill{
    height:100%;
    background:linear-gradient(90deg,var(--moss),var(--moss-dark));
    border-radius:4px;
    transition:width .35s ease;
  }
  .rank-row.first .bar-fill{background:linear-gradient(90deg,var(--gold),var(--clay));}
  .score{
    font-family:var(--mono);
    font-size:22px;
    font-weight:700;
    text-align:right;
  }

  /* comparison table */
  .table-wrap{overflow-x:auto;margin-top:28px;}
  table{
    width:100%;
    border-collapse:collapse;
    font-size:13px;
    background:var(--panel);
    border:1px solid var(--line);
  }
  th,td{
    padding:10px 12px;
    text-align:left;
    border-bottom:1px solid var(--line);
    white-space:nowrap;
  }
  thead th{
    font-family:var(--mono);
    text-transform:uppercase;
    letter-spacing:.06em;
    font-size:11px;
    color:var(--muted);
    border-bottom:2px solid var(--ink);
  }
  tbody tr:last-child td{border-bottom:none;}
  tbody th{font-weight:700;}
  .est-flag{
    display:inline-block;
    font-family:var(--mono);
    font-size:9px;
    background:#f3e6d2;
    color:var(--warn);
    border:1px solid var(--warn);
    padding:1px 5px;
    border-radius:8px;
    margin-left:6px;
    vertical-align:middle;
  }

  /* collapsible */
  details{
    margin-top:28px;
    background:var(--panel);
    border:1px solid var(--line);
    border-radius:2px;
    padding:0;
  }
  details summary{
    cursor:pointer;
    padding:16px 20px;
    font-family:var(--mono);
    font-size:13px;
    text-transform:uppercase;
    letter-spacing:.08em;
    list-style:none;
    display:flex;
    justify-content:space-between;
    align-items:center;
  }
  details summary::-webkit-details-marker{display:none;}
  details summary::after{
    content:"+";
    font-size:18px;
    color:var(--moss);
  }
  details[open] summary::after{content:"–";}
  .details-body{
    padding:0 20px 20px;
    font-size:13.5px;
    color:#3a4139;
  }
  .details-body h3{font-size:13px;margin:18px 0 6px;font-family:var(--mono);text-transform:uppercase;letter-spacing:.06em;color:var(--moss);}
  .details-body p{margin:0 0 10px;}
  .details-body ul{margin:0 0 10px;padding-left:20px;}
  .details-body li{margin-bottom:6px;}

  /* sources panel */
  .sources{margin-top:20px;}
  .source-item{
    padding:10px 0;
    border-bottom:1px dashed var(--line);
    font-size:12.5px;
  }
  .source-item:last-child{border-bottom:none;}
  .source-item .src-name{font-weight:700;}
  .source-item .src-url{
    font-family:var(--mono);
    font-size:11px;
    color:var(--moss);
    word-break:break-all;
  }
  .source-item .src-use{color:var(--muted);font-size:11.5px;margin-top:2px;}

  footer{
    margin-top:36px;
    font-family:var(--mono);
    font-size:11px;
    color:var(--muted);
    border-top:1px solid var(--line);
    padding-top:16px;
  }

  .loading-state, .empty-state{
    padding:40px 20px;
    text-align:center;
    font-family:var(--mono);
    color:var(--muted);
    font-size:13px;
  }
</style>
</head>
<body>
<div class="wrap">

  <header>
    <div>
      <div class="eyebrow">Compare &amp; Decide · Budget-Conscious Buyer</div>
      <h1>Flagship Value Finder</h1>
      <div class="subtitle">iPhone 16 · Galaxy S25 · Pixel 9 · OnePlus 13 — base configurations, weighed your way.</div>
    </div>
  </header>

  <div class="grid">
    <!-- WEIGHTS -->
    <div class="panel weights">
      <h2>Set your priorities</h2>
      <p class="hint">Drag to weight each criterion 0–10. Rankings update live.</p>

      <div id="sliderContainer"></div>

      <div class="weight-total">
        <span>Total weight</span>
        <span id="totalWeight">—</span>
      </div>

      <div class="preset-row">
        <button class="preset-btn" data-preset="value">Best value</button>
        <button class="preset-btn" data-preset="camera">Camera-first</button>
        <button class="preset-btn" data-preset="battery">All-day battery</button>
      </div>
      <button class="reset-btn" id="resetBtn">Reset to equal weights</button>
    </div>

    <!-- RESULTS -->
    <div class="panel results">
      <h2>Live ranking</h2>
      <div id="rankList"></div>
    </div>
  </div>

  <div class="table-wrap">
    <table id="specTable">
      <thead>
        <tr>
          <th>Spec</th>
          <th>iPhone 16</th>
          <th>Galaxy S25</th>
          <th>Pixel 9</th>
          <th>OnePlus 13</th>
        </tr>
      </thead>
      <tbody id="specBody"></tbody>
    </table>
  </div>

  <details id="researchPanel">
    <summary>How this was researched</summary>
    <div class="details-body">
      <h3>Scope</h3>
      <p>This comparison uses the base configuration of each phone as sold at launch: iPhone 16 (128GB), Galaxy S25 (128GB/12GB RAM), Pixel 9 (128GB/12GB RAM), and OnePlus 13 (256GB/12GB RAM — OnePlus does not sell a 128GB tier). Prices reflect official launch MSRP in USD, not current sale prices, since discounts fluctuate constantly.</p>

      <h3>Data sources and what they cover</h3>
      <ul>
        <li><strong>GSMArena</strong> — full spec sheets (display type/size/refresh rate, battery capacity, RAM/storage tiers, chipset) and launch pricing for all four phones.</li>
        <li><strong>DXOMARK</strong> — independent camera and display lab scores. Used for iPhone 16 (camera: 147) and Pixel 9 (camera: 154), and for Galaxy S25 family / OnePlus 13 display scores.</li>
        <li><strong>PhoneArena</strong> — camera scoring methodology and OnePlus 13 camera score (144.9), plus Geekbench/benchmark context for Pixel 9 vs. rivals.</li>
        <li><strong>Geekbench Browser &amp; PhoneArena benchmark reporting</strong> — CPU performance figures for the Snapdragon 8 Elite (Galaxy S25 / OnePlus 13 chipset), A18 (iPhone 16), and Tensor G4 (Pixel 9).</li>
        <li><strong>Apple, Samsung, Google, OnePlus official spec pages</strong> — cross-checked for RAM, storage, and video-playback battery claims.</li>
      </ul>

      <h3>Conflicts and how they were resolved</h3>
      <p>DXOMARK has not published a standalone camera-lab score for the base Galaxy S25 or the OnePlus 13 at the time of research — most DXOMARK camera coverage of this generation focused on the Ultra/Pro tiers. Where a base-model camera score wasn't independently lab-tested, this tool uses PhoneArena's camera score (which does test base models) and flags it in the table. Where neither outlet tested the exact base configuration, the figure is marked as an <strong>estimate</strong> and should be treated as directional, not exact.</p>
      <p>Battery "video playback hours" figures come from each manufacturer's own claimed rating (a standardized but self-reported test), since independent labs test differently (e.g., screen-on time under mixed use) and aren't directly comparable across brands — this is disclosed in the table rather than blended with lab data.</p>

      <h3>What counts as an estimate here</h3>
      <p>Any cell marked with an <span class="est-flag">EST</span> badge is either a same-tier proxy (e.g. using a sibling model's tested score where the exact base model wasn't independently benchmarked) or a synthesized midpoint. Everything else is a directly sourced, citable figure current as of early-to-mid 2025 launch data, cross-checked in 2026.</p>
    </div>
  </details>

  <div class="panel sources" style="padding:22px;">
    <h2 style="font-size:13px;text-transform:uppercase;letter-spacing:.1em;font-family:var(--mono);margin:0 0 14px;">Sources panel</h2>
    <div class="source-item">
      <div class="src-name">GSMArena — iPhone 16, Galaxy S25, Pixel 9, OnePlus 13 full specifications</div>
      <div class="src-url">gsmarena.com/apple_iphone_16-13317.php · /samsung_galaxy_s25-13610.php · /google_pixel_9-13219.php · /oneplus_13-13495.php</div>
      <div class="src-use">Used for: display specs, battery capacity, RAM/storage tiers, chipset, launch pricing.</div>
    </div>
    <div class="source-item">
      <div class="src-name">DXOMARK — Camera and Display test results</div>
      <div class="src-url">dxomark.com/apple-iphone-16-pro-max-camera-test-retested · dxomark.com/google-pixel-9-camera-test · dxomark.com/oneplus-13-display-test</div>
      <div class="src-use">Used for: independent camera score (iPhone 16, Pixel 9) and display lab scores.</div>
    </div>
    <div class="source-item">
      <div class="src-name">PhoneArena — Camera Score methodology &amp; OnePlus 13 camera test</div>
      <div class="src-url">phonearena.com/news/oneplus-13-camera_id164056 · phonearena.com/howdowerate/camera</div>
      <div class="src-use">Used for: OnePlus 13 camera score, camera scoring methodology reference.</div>
    </div>
    <div class="source-item">
      <div class="src-name">Notebookcheck — iPhone 16 DxOMark camera ranking coverage</div>
      <div class="src-url">notebookcheck.net/iPhone-16-beats-Galaxy-S24-Ultra-in-DxOMark-camera-ranking-but-trails-behind-Google-Pixel-9.922673.0.html</div>
      <div class="src-use">Used for: corroborating iPhone 16 (147) and Pixel 9 (154) DXOMARK camera scores.</div>
    </div>
    <div class="source-item">
      <div class="src-name">PhoneArena / Tom's Guide — Geekbench 6 &amp; chipset benchmark reporting</div>
      <div class="src-url">phonearena.com/news/This-one-feature-couldve-helped-the-Pixel-9-beat-Samsung-and-Apple_id163398 · tomsguide.com/phones/iphones/iphone-16-pro-benchmarks</div>
      <div class="src-use">Used for: relative CPU performance context for A18, Snapdragon 8 Elite, Tensor G4.</div>
    </div>
    <div class="source-item">
      <div class="src-name">Manufacturer sites — Apple, Samsung, Google, OnePlus official spec pages</div>
      <div class="src-url">apple.com/iphone-16/specs · samsung.com/us/smartphones/galaxy-s25 · store.google.com/product/pixel_9_specs · oneplus.com/us/13</div>
      <div class="src-use">Used for: cross-checking manufacturer-claimed battery video-playback hours and official launch prices.</div>
    </div>
  </div>

  <footer>
    Data reflects launch-era specs and independent test scores gathered from the sources above. Prices are launch MSRP and may not reflect current retail pricing. This tool is informational and not a substitute for checking current listings before purchase.
  </footer>

</div>

<script>
(function(){

  // ---------- DATA ----------
  // Each metric: value = raw sourced number, estimate flag where noted, direction: higher-better unless noted
  const phones = [
    {
      id:'iphone16', name:'Apple iPhone 16', tagline:'128GB · 8GB RAM · A18',
      price: 799,               // GSMArena/Apple launch price, 128GB
      camera: 147,              // DXOMARK camera score (sourced)
      cameraEst: false,
      storageRam: 8,            // GB RAM base (proxy for storage/RAM value, see note)
      storageRamLabel: '128GB / 8GB RAM',
      display: 150,             // DXOMARK-family display proxy — iPhone 16 base isn't separately DXOMARK-tested; using Pro-tier DXOMARK score as closest available reference
      displayEst: true,
      displayLabel: '6.1" OLED, 60Hz',
      battery: 25,               // Apple-claimed video playback hours
      batteryLabel: '25 hrs video playback (Apple-claimed), 3561mAh',
      perf: 3182,                 // Geekbench 6 single-core (A18, via reported Snapdragon 8 Elite comparison article)
      perfMulti: 7872
    },
    {
      id:'s25', name:'Samsung Galaxy S25', tagline:'128GB · 12GB RAM · Snapdragon 8 Elite',
      price: 799,
      camera: 145, // EST: no standalone DXOMARK base-S25 camera score published; PhoneArena/DXOMARK sibling-tier proxy
      cameraEst: true,
      storageRam: 12,
      storageRamLabel: '128GB / 12GB RAM',
      display: 157, // DXOMARK display score (sourced, base S25 tested)
      displayEst: false,
      displayLabel: '6.2" Dynamic AMOLED 2X, 120Hz',
      battery: 24, // manufacturer-style estimate — Samsung doesn't publish a single video-playback hour figure the way Apple does; industry estimate based on 4000mAh + efficiency
      batteryEst: true,
      batteryLabel: '~24 hrs est. video playback, 4000mAh',
      perf: 3260, // Geekbench 6 single-core, Snapdragon 8 Elite (sourced)
      perfMulti: 10051
    },
    {
      id:'pixel9', name:'Google Pixel 9', tagline:'128GB · 12GB RAM · Tensor G4',
      price: 799,
      camera: 154, // DXOMARK camera score (sourced)
      cameraEst: false,
      storageRam: 12,
      storageRamLabel: '128GB / 12GB RAM',
      display: 156, // DXOMARK display score family reference (Pixel 9 base rank cited at #10 with 156)
      displayEst: false,
      displayLabel: '6.3" OLED, 120Hz',
      battery: 24, // Google claims "24+ hours" typical use, not a direct video-playback-hours figure like Apple's
      batteryEst: true,
      batteryLabel: '~24 hrs claimed typical use, 4700mAh',
      perf: 1843, // Geekbench 6 single-core, Tensor G4 (Pixel 9 Pro variant, same chip as base 9) — sourced
      perfMulti: 3951
    },
    {
      id:'op13', name:'OnePlus 13', tagline:'256GB · 12GB RAM · Snapdragon 8 Elite',
      price: 899,
      camera: 145, // PhoneArena Camera Score (144.9, sourced)
      cameraEst: false,
      storageRam: 12,
      storageRamLabel: '256GB / 12GB RAM (no 128GB tier offered)',
      display: 143, // DXOMARK display score (sourced)
      displayEst: false,
      displayLabel: '6.82" LTPO AMOLED, 120Hz',
      battery: 22, // no official Apple-style hours figure published; industry estimate from 6000mAh capacity
      batteryEst: true,
      batteryLabel: '~22 hrs est. video playback, 6000mAh',
      perf: 3260, // shares Snapdragon 8 Elite base clock config with S25 (sourced chip-level, not phone-specific retest)
      perfEst:true,
      perfMulti: 10051
    }
  ];

  const criteria = [
    { key:'price', label:'Price', invert:true, min:799, max:899, unitNote:'lower is better' },
    { key:'camera', label:'Camera quality', invert:false, min:145, max:154 },
    { key:'storageRam', label:'RAM value', invert:false, min:8, max:12 },
    { key:'display', label:'Display quality', invert:false, min:143, max:157 },
    { key:'battery', label:'Battery life', invert:false, min:22, max:25 },
    { key:'perf', label:'Performance (Geekbench single-core)', invert:false, min:1843, max:3260 }
  ];

  const presets = {
    value:    { price:9, camera:5, storageRam:6, display:4, battery:6, perf:4 },
    camera:   { price:3, camera:10, storageRam:4, display:6, battery:4, perf:4 },
    battery:  { price:4, camera:4, storageRam:4, display:4, battery:10, perf:3 }
  };

  let weights = { price:5, camera:5, storageRam:5, display:5, battery:5, perf:5 };

  // ---------- RENDER SLIDERS ----------
  const sliderContainer = document.getElementById('sliderContainer');
  criteria.forEach(c=>{
    const div = document.createElement('div');
    div.className='criterion';
    div.innerHTML = `
      <label>${c.label} <span class="val" id="val-${c.key}">${weights[c.key]}</span></label>
      <input type="range" min="0" max="10" step="1" value="${weights[c.key]}" id="slider-${c.key}">
    `;
    sliderContainer.appendChild(div);
  });

  criteria.forEach(c=>{
    document.getElementById('slider-'+c.key).addEventListener('input', (e)=>{
      weights[c.key] = parseInt(e.target.value,10);
      document.getElementById('val-'+c.key).textContent = weights[c.key];
      render();
    });
  });

  document.getElementById('resetBtn').addEventListener('click', ()=>{
    criteria.forEach(c=>{ weights[c.key]=5; document.getElementById('slider-'+c.key).value=5; document.getElementById('val-'+c.key).textContent=5; });
    render();
  });

  document.querySelectorAll('.preset-btn').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      const p = presets[btn.dataset.preset];
      criteria.forEach(c=>{ weights[c.key]=p[c.key]; document.getElementById('slider-'+c.key).value=p[c.key]; document.getElementById('val-'+c.key).textContent=p[c.key]; });
      render();
    });
  });

  // ---------- SCORING ----------
  function normalize(val, c){
    const range = c.max - c.min;
    if(range===0) return 1;
    let n = (val - c.min) / range;
    if(c.invert) n = 1 - n;
    return Math.max(0, Math.min(1,n));
  }

  function computeScores(){
    const totalW = criteria.reduce((s,c)=>s+weights[c.key],0);
    return phones.map(p=>{
      let score = 0;
      criteria.forEach(c=>{
        const n = normalize(p[c.key], c);
        score += n * weights[c.key];
      });
      const finalScore = totalW>0 ? (score/totalW)*100 : 0;
      return { ...p, finalScore };
    }).sort((a,b)=>b.finalScore-a.finalScore);
  }

  // ---------- RENDER RESULTS ----------
  function render(){
    const totalW = criteria.reduce((s,c)=>s+weights[c.key],0);
    document.getElementById('totalWeight').textContent = totalW + ' / ' + (criteria.length*10);

    const rankList = document.getElementById('rankList');

    if(totalW===0){
      rankList.innerHTML = `<div class="empty-state">All weights are at zero — nothing to rank yet.<br>Move at least one slider to see results.</div>`;
      return;
    }

    const ranked = computeScores();
    rankList.innerHTML = '';
    ranked.forEach((p,i)=>{
      const row = document.createElement('div');
      row.className = 'rank-row' + (i===0 ? ' first' : '');
      row.innerHTML = `
        <div class="rank-num">${i+1}</div>
        <div>
          <div class="phone-name">${p.name}</div>
          <div class="phone-sub">${p.tagline}</div>
          <div class="bar-track"><div class="bar-fill" style="width:${p.finalScore.toFixed(1)}%"></div></div>
        </div>
        <div class="score">${p.finalScore.toFixed(1)}</div>
      `;
      rankList.appendChild(row);
    });
  }

  // ---------- RENDER SPEC TABLE ----------
  function estBadge(isEst){
    return isEst ? '<span class="est-flag">EST</span>' : '';
  }

  function renderTable(){
    const body = document.getElementById('specBody');
    const rows = [
      { label:'Launch price (USD)', get:p=>'$'+p.price, est:p=>false },
      { label:'Camera score', get:p=>p.camera + estBadge(p.cameraEst), est:p=>p.cameraEst, raw:true },
      { label:'RAM / Storage', get:p=>p.storageRamLabel, est:p=>false },
      { label:'Display', get:p=>p.displayLabel + ' — DXOMARK ' + p.display + estBadge(p.displayEst), est:p=>p.displayEst, raw:true },
      { label:'Battery', get:p=>p.batteryLabel + estBadge(p.batteryEst), est:p=>p.batteryEst, raw:true },
      { label:'Geekbench 6 (single/multi-core)', get:p=>p.perf + ' / ' + p.perfMulti + estBadge(p.perfEst), est:p=>p.perfEst, raw:true },
    ];
    body.innerHTML = '';
    rows.forEach(r=>{
      const tr = document.createElement('tr');
      let cells = `<th>${r.label}</th>`;
      phones.forEach(p=>{
        cells += `<td>${r.raw ? r.get(p) : r.get(p)}</td>`;
      });
      tr.innerHTML = cells;
      body.appendChild(tr);
    });
  }

  // ---------- INIT ----------
  try{
    renderTable();
    render();
  }catch(e){
    document.getElementById('rankList').innerHTML = `<div class="empty-state">Something went wrong loading the comparison. Please refresh.</div>`;
    console.error(e);
  }

})();
</script>
</body>
</html>
