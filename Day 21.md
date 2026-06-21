# Today I Built a Digital Privacy Intelligence Dashboard using claude :

🔍 Privacy Findings :

- Analyzed digital exposure across 15 commonly used services and estimated a privacy score.
- Identified how data from multiple platforms can be combined to create a cross-platform identity graph.
- Highlighted high-value data assets that advertisers and data brokers may infer, including:
    (i)   Purchase intent signals
    (ii)  Entertainment preferences
    (iii) Social network patterns
    (iv)  Payment behavior indicators
    (v)   Gaming engagement trends
- Demonstrated how data concentration within a few companies can increase privacy risks.
- Simulated privacy-improving actions and estimated their impact on overall privacy score.

📚 Key Learnings:

- Digital footprints are created not by a single app, but by the combination of services we use daily.
- Cross-platform data aggregation can reveal surprisingly detailed behavioral patterns.
- Privacy risks often arise from data correlation rather than direct data sharing.
- Small actions such as enabling 2FA, limiting ad identifiers, and restricting permissions can improve privacy posture.
- Interactive dashboards make complex privacy concepts easier to understand and communicate.
- Claude can be effectively used to generate complete analytical dashboards from well-structured prompts.
- Data visualization helps transform abstract privacy concerns into actionable insights.

## HTML FILE:

<style>
  :root{
    --bg-0:#0B0F14;
    --bg-1:#0F151C;
    --bg-2:#141C25;
    --bg-3:#1A2430;
    --line:#26323F;
    --line-soft:#1D2731;
    --ink-0:#EAF0F5;
    --ink-1:#AEC0CE;
    --ink-2:#728495;
    --ink-3:#4D5C6B;
    --accent:#5EEAD4;
    --accent-dim:#2A6E63;
    --accent-soft:rgba(94,234,212,0.10);
    --amber:#F2B85C;
    --amber-soft:rgba(242,184,92,0.12);
    --orange:#F2924A;
    --orange-soft:rgba(242,146,74,0.12);
    --red:#F0654F;
    --red-soft:rgba(240,101,79,0.12);
    --blue:#6FA8FF;
    --green:#6FE3A0;
    --mono: 'IBM Plex Mono', 'SF Mono', ui-monospace, monospace;
    --sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    --r-sm:8px;
    --r-md:12px;
    --r-lg:18px;
  }

  *{box-sizing:border-box; margin:0; padding:0;}

  body{
    background:
      radial-gradient(ellipse 1200px 700px at 15% -10%, rgba(94,234,212,0.06), transparent 60%),
      radial-gradient(ellipse 900px 600px at 100% 0%, rgba(111,168,255,0.05), transparent 55%),
      var(--bg-0);
    color:var(--ink-0);
    font-family:var(--sans);
    -webkit-font-smoothing:antialiased;
    line-height:1.5;
    min-height:100vh;
    padding-bottom:80px;
  }

  ::selection{ background:var(--accent-soft); color:var(--ink-0); }

  .wrap{ max-width:1180px; margin:0 auto; padding:0 28px; }

  /* ---------- TOPBAR ---------- */
  .topbar{
    border-bottom:1px solid var(--line-soft);
    background:rgba(11,15,20,0.85);
    backdrop-filter:blur(10px);
    position:sticky; top:0; z-index:50;
  }
  .topbar-inner{
    max-width:1180px; margin:0 auto; padding:16px 28px;
    display:flex; align-items:center; justify-content:space-between;
  }
  .brand{ display:flex; align-items:center; gap:10px; }
  .brand-mark{
    width:30px; height:30px; border-radius:8px;
    background:linear-gradient(135deg, var(--accent), #3B9E8E);
    display:flex; align-items:center; justify-content:center;
    font-family:var(--mono); font-weight:700; font-size:14px; color:#06120F;
  }
  .brand-text{ font-family:var(--mono); font-size:13px; letter-spacing:0.04em; color:var(--ink-1); }
  .brand-text b{ color:var(--ink-0); font-weight:600; }
  .topbar-tag{
    font-family:var(--mono); font-size:11px; color:var(--ink-3);
    border:1px solid var(--line); border-radius:20px; padding:5px 12px;
    letter-spacing:0.03em;
  }
  .topbar-tag b{ color:var(--accent); font-weight:600; }

  /* ---------- HERO ---------- */
  .hero{ padding:48px 0 28px; }
  .eyebrow{
    font-family:var(--mono); font-size:11.5px; letter-spacing:0.12em; text-transform:uppercase;
    color:var(--accent); display:flex; align-items:center; gap:8px; margin-bottom:14px;
  }
  .eyebrow::before{ content:''; width:6px; height:6px; border-radius:50%; background:var(--accent); box-shadow:0 0 8px var(--accent); }
  h1{
    font-size:34px; font-weight:650; letter-spacing:-0.02em; color:var(--ink-0);
    max-width:680px; line-height:1.2;
  }
  .hero-sub{ color:var(--ink-2); font-size:14.5px; max-width:620px; margin-top:12px; }

  /* ---------- DISCLAIMER STRIP ---------- */
  .strip{
    margin-top:24px; border:1px solid var(--line); border-radius:var(--r-md);
    background:var(--bg-1); padding:14px 18px; display:flex; gap:12px; align-items:flex-start;
  }
  .strip-icon{ font-family:var(--mono); color:var(--amber); font-size:14px; flex-shrink:0; margin-top:1px; }
  .strip p{ font-size:12.5px; color:var(--ink-2); line-height:1.6; }
  .strip b{ color:var(--ink-1); }

  /* ---------- SCORE ROW ---------- */
  .score-row{ display:grid; grid-template-columns:1fr 1fr; gap:18px; margin-top:28px; }
  @media (max-width:760px){ .score-row{ grid-template-columns:1fr; } }

  .score-card{
    border:1px solid var(--line); border-radius:var(--r-lg);
    background:linear-gradient(180deg, var(--bg-2), var(--bg-1));
    padding:26px; position:relative; overflow:hidden;
  }
  .score-card::before{
    content:''; position:absolute; top:-40%; right:-20%; width:280px; height:280px;
    border-radius:50%; filter:blur(60px); opacity:0.18; pointer-events:none;
  }
  .score-card.footprint::before{ background:var(--orange); }
  .score-card.privacy::before{ background:var(--accent); }

  .score-top{ display:flex; justify-content:space-between; align-items:flex-start; }
  .score-label{ font-family:var(--mono); font-size:11.5px; text-transform:uppercase; letter-spacing:0.08em; color:var(--ink-2); }
  .score-badge{
    font-family:var(--mono); font-size:11px; padding:4px 10px; border-radius:20px; font-weight:600;
    display:flex; align-items:center; gap:6px;
  }
  .score-num-row{ display:flex; align-items:baseline; gap:10px; margin-top:18px; }
  .score-num{ font-family:var(--mono); font-size:56px; font-weight:700; letter-spacing:-0.03em; }
  .score-max{ font-family:var(--mono); font-size:16px; color:var(--ink-3); }

  .score-bar-track{
    margin-top:18px; height:8px; border-radius:6px; background:var(--bg-3); overflow:hidden;
    border:1px solid var(--line-soft);
  }
  .score-bar-fill{ height:100%; border-radius:6px; }

  .score-zones{ display:flex; justify-content:space-between; margin-top:8px; }
  .score-zones span{ font-family:var(--mono); font-size:9.5px; color:var(--ink-3); }

  .score-foot{ margin-top:16px; font-size:12.5px; color:var(--ink-2); line-height:1.6; }

  /* ---------- STAT STRIP ---------- */
  .stat-grid{
    display:grid; grid-template-columns:repeat(4,1fr); gap:14px; margin-top:18px;
  }
  @media (max-width:760px){ .stat-grid{ grid-template-columns:1fr 1fr; } }
  .stat-card{
    border:1px solid var(--line); border-radius:var(--r-md); background:var(--bg-1);
    padding:16px 18px;
  }
  .stat-num{ font-family:var(--mono); font-size:24px; font-weight:700; color:var(--ink-0); }
  .stat-label{ font-size:11.5px; color:var(--ink-2); margin-top:4px; }
  .stat-tag{ display:inline-block; margin-top:8px; font-family:var(--mono); font-size:9.5px; padding:2px 7px; border-radius:4px; }
  .tag-fact{ background:rgba(111,168,255,0.12); color:var(--blue); }
  .tag-est{ background:var(--amber-soft); color:var(--amber); }

  /* ---------- SECTION SCAFFOLD ---------- */
  section.block{ margin-top:56px; }
  .block-head{ display:flex; align-items:flex-end; justify-content:space-between; gap:20px; margin-bottom:18px; flex-wrap:wrap; }
  .block-num{ font-family:var(--mono); font-size:11px; color:var(--ink-3); letter-spacing:0.06em; }
  .block-title{ font-size:21px; font-weight:650; letter-spacing:-0.01em; margin-top:4px; }
  .block-desc{ font-size:13px; color:var(--ink-2); max-width:520px; margin-top:6px; line-height:1.55; }
  .panel{
    border:1px solid var(--line); border-radius:var(--r-lg); background:var(--bg-1); padding:24px;
  }

  /* ---------- HEATMAP ---------- */
  .heatmap-grid{
    display:grid; grid-template-columns:repeat(5,1fr); gap:10px;
  }
  @media (max-width:640px){ .heatmap-grid{ grid-template-columns:repeat(3,1fr); } }
  .heat-cell{
    border-radius:var(--r-md); padding:14px 12px; border:1px solid var(--line-soft);
    display:flex; flex-direction:column; gap:10px; min-height:96px; position:relative;
    transition:transform .15s ease;
  }
  .heat-cell:hover{ transform:translateY(-2px); }
  .heat-app{ font-size:13px; font-weight:600; color:var(--ink-0); }
  .heat-meta{ font-family:var(--mono); font-size:9.5px; color:var(--ink-2); }
  .heat-score{
    position:absolute; top:10px; right:12px; font-family:var(--mono); font-size:10px; font-weight:700;
  }
  .heat-bar{ height:4px; border-radius:3px; background:rgba(255,255,255,0.08); overflow:hidden; margin-top:auto; }
  .heat-bar i{ display:block; height:100%; border-radius:3px; }

  .legend-row{ display:flex; gap:18px; margin-top:18px; flex-wrap:wrap; }
  .legend-item{ display:flex; align-items:center; gap:7px; font-family:var(--mono); font-size:10.5px; color:var(--ink-2); }
  .legend-dot{ width:9px; height:9px; border-radius:3px; }

  /* ---------- COMPANY RANKING ---------- */
  .rank-list{ display:flex; flex-direction:column; gap:10px; }
  .rank-row{
    display:grid; grid-template-columns:28px 150px 1fr 90px; align-items:center; gap:16px;
    padding:13px 4px; border-bottom:1px solid var(--line-soft);
  }
  .rank-row:last-child{ border-bottom:none; }
  @media (max-width:640px){ .rank-row{ grid-template-columns:24px 1fr; row-gap:8px; } .rank-bar-wrap, .rank-pct{ grid-column:2/3; } }
  .rank-pos{ font-family:var(--mono); font-size:12px; color:var(--ink-3); }
  .rank-name{ font-size:13.5px; font-weight:600; color:var(--ink-0); }
  .rank-services{ font-family:var(--mono); font-size:10px; color:var(--ink-2); margin-top:2px; }
  .rank-bar-wrap{ height:9px; border-radius:6px; background:var(--bg-3); overflow:hidden; border:1px solid var(--line-soft); }
  .rank-bar{ height:100%; border-radius:6px; background:linear-gradient(90deg, var(--accent-dim), var(--accent)); }
  .rank-pct{ font-family:var(--mono); font-size:12px; color:var(--ink-1); text-align:right; }

  /* ---------- MATRIX TABLE ---------- */
  .matrix-scroll{ overflow-x:auto; }
  table.matrix{ width:100%; border-collapse:collapse; min-width:760px; }
  table.matrix th{
    text-align:left; font-family:var(--mono); font-size:10px; text-transform:uppercase; letter-spacing:0.05em;
    color:var(--ink-3); padding:0 10px 12px; font-weight:600; border-bottom:1px solid var(--line);
  }
  table.matrix td{ padding:11px 10px; border-bottom:1px solid var(--line-soft); font-size:12.5px; vertical-align:middle; }
  table.matrix tr:last-child td{ border-bottom:none; }
  .app-cell{ display:flex; align-items:center; gap:10px; font-weight:600; color:var(--ink-0); }
  .app-dot{ width:8px; height:8px; border-radius:50%; flex-shrink:0; }
  .dot-yes{ color:var(--accent); }
  .dot-no{ color:var(--ink-3); }
  .dot-partial{ color:var(--amber); }
  .lvl{ font-family:var(--mono); font-size:9.5px; padding:3px 8px; border-radius:5px; display:inline-block; font-weight:600; }
  .lvl-high{ background:var(--red-soft); color:var(--red); }
  .lvl-med{ background:var(--amber-soft); color:var(--amber); }
  .lvl-low{ background:rgba(111,168,255,0.12); color:var(--blue); }

  /* ---------- RISK RADAR ---------- */
  .radar-wrap{ display:grid; grid-template-columns:1fr 320px; gap:30px; align-items:center; }
  @media (max-width:760px){ .radar-wrap{ grid-template-columns:1fr; } }
  .radar-legend{ display:flex; flex-direction:column; gap:14px; }
  .radar-item{ display:flex; justify-content:space-between; align-items:center; padding:10px 0; border-bottom:1px solid var(--line-soft); }
  .radar-item:last-child{ border:none; }
  .radar-axis-name{ font-size:12.5px; color:var(--ink-1); font-weight:500; }
  .radar-axis-val{ font-family:var(--mono); font-size:12px; color:var(--accent); font-weight:700; }

  /* ---------- DIGITAL TWIN ---------- */
  .twin-grid{ display:grid; grid-template-columns:1fr 1fr; gap:16px; }
  @media (max-width:640px){ .twin-grid{ grid-template-columns:1fr; } }
  .twin-card{
    border:1px solid var(--line-soft); border-radius:var(--r-md); padding:16px 18px; background:var(--bg-2);
  }
  .twin-head{ display:flex; align-items:center; gap:8px; margin-bottom:8px; }
  .twin-icon{ font-size:15px; }
  .twin-title{ font-family:var(--mono); font-size:11px; text-transform:uppercase; letter-spacing:0.05em; color:var(--ink-2); }
  .twin-body{ font-size:13px; color:var(--ink-0); line-height:1.6; }
  .twin-body b{ color:var(--accent); font-weight:600; }
  .est-pill{ float:right; font-family:var(--mono); font-size:8.5px; background:var(--amber-soft); color:var(--amber); padding:2px 7px; border-radius:4px; }

  /* ---------- DATA ASSETS ---------- */
  .asset-list{ display:flex; flex-direction:column; gap:0; }
  .asset-row{
    display:grid; grid-template-columns:32px 1fr 130px; gap:16px; align-items:center;
    padding:16px 4px; border-bottom:1px solid var(--line-soft);
  }
  .asset-row:last-child{ border:none; }
  @media (max-width:640px){ .asset-row{ grid-template-columns:28px 1fr; } .asset-value{ grid-column:2/3; justify-self:start; margin-top:4px;} }
  .asset-rank{ font-family:var(--mono); font-size:13px; color:var(--ink-3); }
  .asset-name{ font-size:13.5px; font-weight:600; color:var(--ink-0); }
  .asset-desc{ font-size:11.5px; color:var(--ink-2); margin-top:3px; }
  .asset-value{ font-family:var(--mono); font-size:10.5px; padding:5px 10px; border-radius:6px; text-align:center; font-weight:700; justify-self:end; }

  /* ---------- SIMULATOR ---------- */
  .sim-panel{ display:grid; grid-template-columns:1.1fr 1fr; gap:30px; }
  @media (max-width:760px){ .sim-panel{ grid-template-columns:1fr; } }
  .sim-controls{ display:flex; flex-direction:column; gap:14px; }
  .sim-toggle{
    display:flex; align-items:center; justify-content:space-between; gap:14px;
    border:1px solid var(--line-soft); border-radius:var(--r-md); padding:12px 16px; background:var(--bg-2);
    cursor:pointer; user-select:none;
  }
  .sim-toggle-label{ font-size:12.5px; color:var(--ink-1); }
  .sim-toggle-label small{ display:block; color:var(--ink-3); font-size:10.5px; margin-top:2px; font-family:var(--mono); }
  .switch{ width:38px; height:21px; border-radius:20px; background:var(--bg-3); border:1px solid var(--line); position:relative; flex-shrink:0; transition:background .2s; }
  .switch i{ position:absolute; top:2px; left:2px; width:15px; height:15px; border-radius:50%; background:var(--ink-2); transition:all .2s; }
  .switch.on{ background:var(--accent-soft); border-color:var(--accent-dim); }
  .switch.on i{ left:19px; background:var(--accent); }

  .sim-result{
    border:1px solid var(--line-soft); border-radius:var(--r-md); padding:22px; background:var(--bg-2);
    display:flex; flex-direction:column; align-items:center; justify-content:center; text-align:center;
  }
  .sim-result-label{ font-family:var(--mono); font-size:10.5px; color:var(--ink-2); text-transform:uppercase; letter-spacing:0.06em; }
  .sim-result-num{ font-family:var(--mono); font-size:48px; font-weight:700; color:var(--accent); margin-top:10px; }
  .sim-result-delta{ font-family:var(--mono); font-size:12.5px; color:var(--green); margin-top:6px; }
  .sim-bar-track{ width:100%; height:8px; border-radius:6px; background:var(--bg-3); margin-top:18px; overflow:hidden; border:1px solid var(--line-soft); }
  .sim-bar-fill{ height:100%; border-radius:6px; background:linear-gradient(90deg, var(--accent-dim), var(--accent)); transition:width .35s ease; }

  /* ---------- VERDICT ---------- */
  .verdict-panel{
    border:1px solid var(--line); border-radius:var(--r-lg);
    background:linear-gradient(135deg, var(--bg-2) 0%, var(--bg-1) 100%);
    padding:32px; position:relative; overflow:hidden;
  }
  .verdict-panel::after{
    content:''; position:absolute; bottom:-30%; left:-10%; width:320px; height:320px; border-radius:50%;
    background:var(--accent); filter:blur(90px); opacity:0.08; pointer-events:none;
  }
  .verdict-tag{ font-family:var(--mono); font-size:10.5px; color:var(--accent); text-transform:uppercase; letter-spacing:0.1em; }
  .verdict-title{ font-size:22px; font-weight:650; margin-top:10px; max-width:600px; }
  .verdict-body{ font-size:13.5px; color:var(--ink-1); line-height:1.7; margin-top:14px; max-width:680px; }
  .verdict-body b{ color:var(--ink-0); }

  /* ---------- FOOTER ---------- */
  .footnote{
    margin-top:50px; border-top:1px solid var(--line-soft); padding-top:22px;
    font-size:11.5px; color:var(--ink-3); line-height:1.7;
  }
  .footnote b{ color:var(--ink-2); }
</style>

<div class="topbar">
  <div class="topbar-inner">
    <div class="brand">
      <div class="brand-mark">DF</div>
      <div class="brand-text"><b>Footprint</b>Scope &nbsp;/&nbsp; exposure report</div>
    </div>
    <div class="topbar-tag">15 SERVICES SCANNED · <b>SIMULATED</b></div>
  </div>
</div>

<div class="wrap">

  <!-- HERO -->
  <div class="hero">
    <div class="eyebrow">Digital Footprint Report</div>
    <h1>What 15 apps on one phone add up to.</h1>
    <p class="hero-sub">A structural read of the reported app list below — who owns what, where exposure concentrates, and what could reasonably (not certainly) be inferred from it.</p>

    <div class="strip">
      <div class="strip-icon">&#9888;</div>
      <p><b>This is not a real scan.</b> Nothing here was pulled from any account, device, or private database. Every score is a heuristic estimate computed from the 15 service names provided, treated as the only Facts. Anything about behavior, spending, lifestyle, or habits below is a labeled <b>Estimate</b> — a plausible inference, never a certainty.</p>
    </div>
  </div>

  <!-- SCORES -->
  <div class="score-row">
    <div class="score-card footprint">
      <div class="score-top">
        <div class="score-label">Digital Footprint Score</div>
        <div class="score-badge" style="background:var(--orange-soft); color:var(--orange);">🟠 SIGNIFICANT</div>
      </div>
      <div class="score-num-row">
        <div class="score-num" style="color:var(--orange);">68</div>
        <div class="score-max">/ 100</div>
      </div>
      <div class="score-bar-track"><div class="score-bar-fill" style="width:68%; background:linear-gradient(90deg,#7A4E20,var(--orange));"></div></div>
      <div class="score-zones"><span>🟢 0–30</span><span>🟡 31–60</span><span>🟠 61–80</span><span>🔴 81–100</span></div>
      <div class="score-foot">Driven by breadth (15 services, 11 companies), daily-use categories (social, messaging, payments), and overlap across social + entertainment + commerce + finance.</div>
    </div>

    <div class="score-card privacy">
      <div class="score-top">
        <div class="score-label">Privacy Score</div>
        <div class="score-badge" style="background:var(--amber-soft); color:var(--amber);">🟡 FAIR</div>
      </div>
      <div class="score-num-row">
        <div class="score-num" style="color:var(--accent);">47</div>
        <div class="score-max">/ 100</div>
      </div>
      <div class="score-bar-track"><div class="score-bar-fill" style="width:47%; background:linear-gradient(90deg,var(--accent-dim),var(--accent));"></div></div>
      <div class="score-zones"><span>🔴 0–30</span><span>🟠 31–60</span><span>🟡 61–80</span><span>🟢 81–100</span></div>
      <div class="score-foot">Pulled down by heavy concentration in a small number of ad-funded ecosystems (Google, Meta) and at least one financial-data surface (Google Pay).</div>
    </div>
  </div>

  <div class="stat-grid">
    <div class="stat-card">
      <div class="stat-num">15</div>
      <div class="stat-label">Total Services Used</div>
      <span class="stat-tag tag-fact">FACT</span>
    </div>
    <div class="stat-card">
      <div class="stat-num">11</div>
      <div class="stat-label">Parent Companies</div>
      <span class="stat-tag tag-fact">INFERRED FACT</span>
    </div>
    <div class="stat-card">
      <div class="stat-num">27%</div>
      <div class="stat-label">Ecosystem Concentration (Google)</div>
      <span class="stat-tag tag-est">ESTIMATE</span>
    </div>
    <div class="stat-card">
      <div class="stat-num">High</div>
      <div class="stat-label">Estimated Tracking Surface</div>
      <span class="stat-tag tag-est">ESTIMATE</span>
    </div>
  </div>

  <!-- 1. EXPOSURE HEATMAP -->
  <section class="block">
    <div class="block-head">
      <div>
        <div class="block-num">01 — EXPOSURE HEATMAP</div>
        <div class="block-title">Exposure Heatmap</div>
        <div class="block-desc">Relative estimated data-exposure intensity per app, based on category norms (social/messaging apps and ad-funded platforms typically collect more than utilities).</div>
      </div>
    </div>
    <div class="panel">
      <div class="heatmap-grid" id="heatGrid"></div>
      <div class="legend-row">
        <div class="legend-item"><span class="legend-dot" style="background:var(--red);"></span>High exposure (est.)</div>
        <div class="legend-item"><span class="legend-dot" style="background:var(--orange);"></span>Elevated (est.)</div>
        <div class="legend-item"><span class="legend-dot" style="background:var(--amber);"></span>Moderate (est.)</div>
        <div class="legend-item"><span class="legend-dot" style="background:var(--accent);"></span>Lower (est.)</div>
      </div>
    </div>
  </section>

  <!-- 2. COMPANY EXPOSURE RANKING -->
  <section class="block">
    <div class="block-head">
      <div>
        <div class="block-num">02 — COMPANY EXPOSURE RANKING</div>
        <div class="block-title">Company Exposure Ranking</div>
        <div class="block-desc">Share of the 15-service footprint each parent company controls. Higher share = more of this profile sits inside one company's ecosystem.</div>
      </div>
    </div>
    <div class="panel">
      <div class="rank-list" id="rankList"></div>
    </div>
  </section>

  <!-- 3. DATA COLLECTION MATRIX -->
  <section class="block">
    <div class="block-head">
      <div>
        <div class="block-num">03 — DATA COLLECTION MATRIX</div>
        <div class="block-title">Data Collection Matrix</div>
        <div class="block-desc">Estimated likelihood that each category of data is collected by each app, based on each platform's publicly known business model and category norms — not confirmed permissions.</div>
      </div>
    </div>
    <div class="panel">
      <div class="matrix-scroll">
        <table class="matrix" id="matrixTable"></table>
      </div>
    </div>
  </section>

  <!-- 4. RISK RADAR -->
  <section class="block">
    <div class="block-head">
      <div>
        <div class="block-num">04 — RISK RADAR</div>
        <div class="block-title">Risk Radar</div>
        <div class="block-desc">Six estimated risk dimensions, scored 0–100, based purely on which service categories are present in the Facts list.</div>
      </div>
    </div>
    <div class="panel radar-wrap">
      <div id="radarSvgHolder"></div>
      <div class="radar-legend" id="radarLegend"></div>
    </div>
  </section>

  <!-- 5. DIGITAL TWIN PROFILE -->
  <section class="block">
    <div class="block-head">
      <div>
        <div class="block-num">05 — DIGITAL TWIN PROFILE</div>
        <div class="block-title">Digital Twin Profile</div>
        <div class="block-desc">A composite sketch of the kind of user this app list resembles. Entirely pattern-based, entirely speculative — every line below is an Estimate.</div>
      </div>
    </div>
    <div class="panel">
      <div class="twin-grid" id="twinGrid"></div>
    </div>
  </section>

  <!-- 6. MOST VALUABLE DATA ASSETS -->
  <section class="block">
    <div class="block-head">
      <div>
        <div class="block-num">06 — MOST VALUABLE DATA ASSETS</div>
        <div class="block-title">Most Valuable Data Assets</div>
        <div class="block-desc">The pieces of inferred data that would be most commercially useful to advertisers or data brokers, ranked by estimated value.</div>
      </div>
    </div>
    <div class="panel">
      <div class="asset-list" id="assetList"></div>
    </div>
  </section>

  <!-- 7. PRIVACY IMPROVEMENT SIMULATOR -->
  <section class="block">
    <div class="block-head">
      <div>
        <div class="block-num">07 — PRIVACY IMPROVEMENT SIMULATOR</div>
        <div class="block-title">Privacy Improvement Simulator</div>
        <div class="block-desc">Toggle common privacy actions to see an estimated effect on the Privacy Score. Illustrative only — actual impact depends on real settings inside each app.</div>
      </div>
    </div>
    <div class="panel">
      <div class="sim-panel">
        <div class="sim-controls" id="simControls"></div>
        <div class="sim-result">
          <div class="sim-result-label">Projected Privacy Score</div>
          <div class="sim-result-num" id="simScore">47</div>
          <div class="sim-result-delta" id="simDelta">+0 from current</div>
          <div class="sim-bar-track"><div class="sim-bar-fill" id="simBar" style="width:47%;"></div></div>
        </div>
      </div>
    </div>
  </section>

  <!-- FINAL VERDICT -->
  <section class="block">
    <div class="block-head">
      <div>
        <div class="block-num">08 — FINAL VERDICT</div>
        <div class="block-title">Final Verdict</div>
      </div>
    </div>
    <div class="verdict-panel">
      <div class="verdict-tag">Summary read</div>
      <div class="verdict-title">A broad, ordinary, ad-ecosystem-heavy footprint — not an extreme one.</div>
      <div class="verdict-body">
        The 15 services span <b>11 companies</b>, with <b>Google alone accounting for 4 of them</b> (Search, YouTube, Pay, Photos) — the single largest concentration in this profile. That combination of search, video, payments, and photo storage under one company is the most structurally significant fact here, because it lets one company connect identity, interest, and financial signals without needing any other app. Add Meta's two services (Instagram, WhatsApp) and over a third of this footprint sits inside two companies.
        <br><br>
        Everything else in this report — the Digital Twin traits, the spending estimates, the lifestyle read — is a <b>labeled Estimate</b> built from category norms, not from any observed activity. <b>Treat it as a starting hypothesis for a conversation about privacy settings, not a profile of a real person.</b>
      </div>
    </div>
  </section>

  <div class="footnote">
    <b>Methodology note:</b> All 15 services listed are treated as user-reported Facts. Parent companies are inferred from public ownership records and labeled as inferred facts. All scores, rankings, heatmap intensities, matrix likelihoods, radar values, digital twin traits, and data-asset valuations are computed heuristically from category norms and are labeled Estimates — none reflect access to any private account, app permission data, or data-broker record. No certainty is claimed about any inferred trait. Where information could not reasonably be inferred from the Facts, this report would state "Not enough information provided."
  </div>

</div>

<script>
(function(){

  // ---- DATA MODEL ----
  const apps = [
    {name:"Instagram", company:"Meta", cat:"Social", exposure:88},
    {name:"WhatsApp", company:"Meta", cat:"Messaging", exposure:62},
    {name:"Snapchat", company:"Snap Inc.", cat:"Social", exposure:84},
    {name:"TikTok", company:"ByteDance", cat:"Social", exposure:92},
    {name:"YouTube", company:"Google", cat:"Entertainment", exposure:78},
    {name:"Google Search", company:"Google", cat:"Search", exposure:90},
    {name:"Google Pay", company:"Google", cat:"Finance", exposure:80},
    {name:"Google Photos", company:"Google", cat:"Storage", exposure:58},
    {name:"Discord", company:"Discord Inc.", cat:"Messaging", exposure:55},
    {name:"iMessage", company:"Apple", cat:"Messaging", exposure:30},
    {name:"Spotify", company:"Spotify AB", cat:"Entertainment", exposure:50},
    {name:"Roblox", company:"Roblox Corp.", cat:"Gaming", exposure:65},
    {name:"PUBG Mobile", company:"Krafton", cat:"Gaming", exposure:60},
    {name:"Amazon", company:"Amazon", cat:"Shopping", exposure:75},
    {name:"Meesho", company:"Meesho", cat:"Shopping", exposure:68},
  ];

  function heatColor(v){
    if(v>=80) return "var(--red)";
    if(v>=65) return "var(--orange)";
    if(v>=50) return "var(--amber)";
    return "var(--accent)";
  }
  function heatBg(v){
    if(v>=80) return "var(--red-soft)";
    if(v>=65) return "var(--orange-soft)";
    if(v>=50) return "var(--amber-soft)";
    return "var(--accent-soft)";
  }

  // ---- 1. HEATMAP ----
  const heatGrid = document.getElementById('heatGrid');
  apps.slice().sort((a,b)=>b.exposure-a.exposure).forEach(a=>{
    const c = heatColor(a.exposure);
    const bg = heatBg(a.exposure);
    const cell = document.createElement('div');
    cell.className = 'heat-cell';
    cell.style.background = bg;
    cell.style.borderColor = c;
    cell.innerHTML = `
      <div class="heat-score" style="color:${c}">${a.exposure}</div>
      <div class="heat-app">${a.name}</div>
      <div class="heat-meta">${a.company} · ${a.cat}</div>
      <div class="heat-bar"><i style="width:${a.exposure}%; background:${c};"></i></div>
    `;
    heatGrid.appendChild(cell);
  });

  // ---- 2. COMPANY RANKING ----
  const companyMap = {};
  apps.forEach(a=>{
    if(!companyMap[a.company]) companyMap[a.company] = [];
    companyMap[a.company].push(a.name);
  });
  const totalServices = apps.length;
  const ranked = Object.entries(companyMap)
    .map(([name, list])=>({name, list, pct: Math.round((list.length/totalServices)*1000)/10}))
    .sort((a,b)=> b.list.length - a.list.length || a.name.localeCompare(b.name));

  const rankList = document.getElementById('rankList');
  ranked.forEach((c, i)=>{
    const row = document.createElement('div');
    row.className = 'rank-row';
    row.innerHTML = `
      <div class="rank-pos">${String(i+1).padStart(2,'0')}</div>
      <div>
        <div class="rank-name">${c.name}</div>
        <div class="rank-services">${c.list.join(', ')}</div>
      </div>
      <div class="rank-bar-wrap"><div class="rank-bar" style="width:${Math.max(c.pct*2.4,4)}%;"></div></div>
      <div class="rank-pct">${c.list.length} svc · ${c.pct}%</div>
    `;
    rankList.appendChild(row);
  });

  // ---- 3. DATA COLLECTION MATRIX ----
  const dims = ["Location","Contacts","Browsing","Purchases","Biometric/Camera","Voice/Audio","Financial"];
  const matrixData = {
    "Instagram":      [1,1,1,0.5,1,0.5,0],
    "Snapchat":       [1,1,0.5,0,1,1,0],
    "TikTok":         [1,0.5,1,0.5,1,1,0],
    "YouTube":        [0.5,0,1,0,0,0.5,0],
    "Discord":        [0.5,0.5,0.5,0,0.5,1,0],
    "WhatsApp":       [0.5,1,0,0,0.5,0.5,0],
    "iMessage":       [0,0.5,0,0,0,0,0],
    "Spotify":        [0.5,0,1,0.5,0,0,0.5],
    "Roblox":         [0,0,0.5,1,0,0.5,0.5],
    "PUBG Mobile":    [1,0,0.5,1,0,0.5,0.5],
    "Amazon":         [0.5,0,1,1,0,0,1],
    "Meesho":         [0.5,0,1,1,0,0,1],
    "Google Search":  [1,0,1,0.5,0,0.5,0],
    "Google Pay":     [0.5,0.5,0.5,1,0,0,1],
    "Google Photos":  [0.5,0,0,0,1,0,0],
  };

  function lvlBadge(v){
    if(v===1) return '<span class="lvl lvl-high">LIKELY</span>';
    if(v===0.5) return '<span class="lvl lvl-med">POSSIBLE</span>';
    return '<span class="lvl lvl-low">UNLIKELY</span>';
  }

  const table = document.getElementById('matrixTable');
  let thead = '<tr><th>App</th>' + dims.map(d=>`<th>${d}</th>`).join('') + '</tr>';
  let tbody = '';
  apps.forEach(a=>{
    const vals = matrixData[a.name];
    tbody += `<tr><td class="app-cell"><span class="app-dot" style="background:${heatColor(a.exposure)}"></span>${a.name}</td>` +
      vals.map(v=>`<td>${lvlBadge(v)}</td>`).join('') + `</tr>`;
  });
  table.innerHTML = thead + tbody;

  // ---- 4. RISK RADAR ----
  const radarDims = [
    {label:"Social Exposure", val:82},
    {label:"Financial Surface", val:55},
    {label:"Behavioral Tracking", val:74},
    {label:"Communication Privacy", val:48},
    {label:"Location Inference", val:60},
    {label:"Identity Consolidation", val:70},
  ];

  function buildRadarSVG(dims){
    const cx=170, cy=170, R=130;
    const n = dims.length;
    const angle = i => (Math.PI*2*i/n) - Math.PI/2;
    const ptAt = (i, r) => {
      const a = angle(i);
      return [cx + r*Math.cos(a), cy + r*Math.sin(a)];
    };
    let rings = '';
    [0.25,0.5,0.75,1].forEach(f=>{
      let pts = dims.map((_,i)=>ptAt(i, R*f).join(',')).join(' ');
      rings += `<polygon points="${pts}" fill="none" stroke="#26323F" stroke-width="1"/>`;
    });
    let spokes = dims.map((_,i)=>{
      const [x,y] = ptAt(i, R);
      return `<line x1="${cx}" y1="${cy}" x2="${x}" y2="${y}" stroke="#1D2731" stroke-width="1"/>`;
    }).join('');
    let dataPts = dims.map((d,i)=> ptAt(i, R*d.val/100).join(',')).join(' ');
    let labels = dims.map((d,i)=>{
      const [x,y] = ptAt(i, R+26);
      return `<text x="${x}" y="${y}" fill="#728495" font-family="IBM Plex Mono, monospace" font-size="9.5" text-anchor="middle" dominant-baseline="middle">${d.label}</text>`;
    }).join('');
    return `<svg viewBox="0 0 340 340" width="100%" height="340">
      ${rings}${spokes}
      <polygon points="${dataPts}" fill="rgba(94,234,212,0.16)" stroke="#5EEAD4" stroke-width="2"/>
      ${dims.map((d,i)=>{const [x,y]=ptAt(i,R*d.val/100); return `<circle cx="${x}" cy="${y}" r="3.5" fill="#5EEAD4"/>`;}).join('')}
      ${labels}
    </svg>`;
  }
  document.getElementById('radarSvgHolder').innerHTML = buildRadarSVG(radarDims);

  const radarLegend = document.getElementById('radarLegend');
  radarDims.forEach(d=>{
    const row = document.createElement('div');
    row.className = 'radar-item';
    row.innerHTML = `<span class="radar-axis-name">${d.label}</span><span class="radar-axis-val">${d.val}</span>`;
    radarLegend.appendChild(row);
  });

  // ---- 5. DIGITAL TWIN ----
  const twinData = [
    {icon:"🎮", title:"Entertainment & Gaming", body:"Presence of TikTok, YouTube, Spotify, Roblox, and PUBG Mobile suggests <b>frequent short-form video and gaming engagement</b> — common among younger or youth-skewing users."},
    {icon:"🛍️", title:"Shopping Behavior", body:"Amazon and Meesho together suggest <b>price-sensitive, multi-platform online shopping</b>, possibly comparing listings across a premium marketplace and a value-focused one."},
    {icon:"💬", title:"Communication Style", body:"A spread across WhatsApp, iMessage, and Discord suggests <b>fragmented messaging habits</b> — likely different platforms for family, close friends, and online communities respectively."},
    {icon:"📍", title:"Mobility & Location", body:"Google Pay plus Google Search together imply <b>routine location-tagged activity</b> (payments, local search), though no GPS or travel data is present in the Facts."},
    {icon:"🧑‍🤝‍🧑", title:"Likely Age Bracket", body:"The Roblox + PUBG Mobile + Snapchat + TikTok combination is most common among <b>teen-to-young-adult users</b> in current adoption patterns — not a confirmed age."},
    {icon:"💳", title:"Financial Footprint", body:"Google Pay is the only financial app in this Facts list, suggesting <b>light-to-moderate digital payment activity</b> rather than heavy fintech or investment app use."},
  ];
  const twinGrid = document.getElementById('twinGrid');
  twinData.forEach(t=>{
    const card = document.createElement('div');
    card.className = 'twin-card';
    card.innerHTML = `<span class="est-pill">ESTIMATE</span>
      <div class="twin-head"><span class="twin-icon">${t.icon}</span><span class="twin-title">${t.title}</span></div>
      <div class="twin-body">${t.body}</div>`;
    twinGrid.appendChild(card);
  });

  // ---- 6. MOST VALUABLE DATA ASSETS ----
  const assets = [
    {name:"Cross-platform identity graph", desc:"Same person reasoned across Google, Meta, and shopping apps — the single most valuable asset to advertisers.", value:"VERY HIGH", color:"var(--red)"},
    {name:"Purchase intent signals", desc:"Amazon + Meesho usage reveals shopping comparison behavior and price sensitivity.", value:"HIGH", color:"var(--orange)"},
    {name:"Entertainment preference profile", desc:"YouTube + Spotify + TikTok combine into a detailed taste and attention-span profile.", value:"HIGH", color:"var(--orange)"},
    {name:"Social graph (estimated)", desc:"Instagram, Snapchat, WhatsApp, Discord together imply a dense, estimable social network.", value:"MEDIUM", color:"var(--amber)"},
    {name:"Payment & spend category data", desc:"Google Pay alone offers limited but real transaction-category signals.", value:"MEDIUM", color:"var(--amber)"},
    {name:"Gaming engagement pattern", desc:"Roblox + PUBG Mobile suggest session-length and in-app purchase propensity.", value:"LOW–MED", color:"var(--accent)"},
  ];
  const assetList = document.getElementById('assetList');
  assets.forEach((a,i)=>{
    const row = document.createElement('div');
    row.className = 'asset-row';
    row.innerHTML = `
      <div class="asset-rank">${String(i+1).padStart(2,'0')}</div>
      <div>
        <div class="asset-name">${a.name}</div>
        <div class="asset-desc">${a.desc}</div>
      </div>
      <div class="asset-value" style="background:${a.color}22; color:${a.color};">${a.value}</div>
    `;
    assetList.appendChild(row);
  });

  // ---- 7. SIMULATOR ----
  const baseScore = 47;
  const actions = [
    {id:'ad-id', label:'Reset / limit ad identifiers', sub:'Instagram · TikTok · Snapchat', impact:6},
    {id:'loc-perm', label:'Restrict background location access', sub:'Google Search · Google Pay', impact:5},
    {id:'pay-2fa', label:'Enable 2FA on Google Pay', sub:'Google Pay', impact:4},
    {id:'discord-dm', label:'Disable open DMs from strangers', sub:'Discord · Roblox', impact:4},
    {id:'photo-backup', label:'Turn off automatic cloud photo backup', sub:'Google Photos', impact:3},
    {id:'shopping-track', label:'Opt out of personalized shopping ads', sub:'Amazon · Meesho', impact:3},
  ];
  const simControls = document.getElementById('simControls');
  const state = {};
  actions.forEach(a=>{
    state[a.id] = false;
    const row = document.createElement('div');
    row.className = 'sim-toggle';
    row.innerHTML = `
      <div class="sim-toggle-label">${a.label}<small>${a.sub} · est. +${a.impact} pts</small></div>
      <div class="switch" id="sw-${a.id}"><i></i></div>
    `;
    row.addEventListener('click', ()=>{
      state[a.id] = !state[a.id];
      document.getElementById('sw-'+a.id).classList.toggle('on', state[a.id]);
      updateSim();
    });
    simControls.appendChild(row);
  });

  function updateSim(){
    let total = baseScore;
    actions.forEach(a=>{ if(state[a.id]) total += a.impact; });
    total = Math.min(total, 100);
    document.getElementById('simScore').textContent = total;
    document.getElementById('simDelta').textContent = `+${total-baseScore} from current`;
    document.getElementById('simBar').style.width = total + '%';
  }

})();
</script>

