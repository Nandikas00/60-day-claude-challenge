# Today I built AI Workflow Architect using claude:
## Key Learnings :
- Learned how to design an end-to-end AI-assisted workflow for database design and optimization, covering every stage from requirements gathering to long-term maintenance.
- Gained practical experience in breaking complex database architecture into structured, easy-to-follow workflow stages.
- Improved understanding of database normalization, schema design, relationships, constraints, and indexing strategies for scalable applications.
- Explored how AI tools like Claude can assist with schema reviews, query optimization, migration planning, and architectural decision-making.
- Learned to create reusable AI prompts that improve consistency and reduce manual effort during database design and performance tuning.
- Strengthened knowledge of query optimization techniques using execution plans, indexing strategies, and performance analysis.
- Understood the importance of performance testing, monitoring, and continuous database optimization for production-ready systems.
- Practiced designing interactive learning experiences with progress tracking, decision trees, bookmarking, note-taking, and workflow visualization.
- Learned to compare multiple AI-powered tools and select the right solution based on specific workflow requirements.
- Improved frontend development skills by building a responsive, interactive application using HTML, CSS, and JavaScript with local storage support.

# Output Screenshots :

<img width="1920" height="897" alt="Screenshot (663)" src="https://github.com/user-attachments/assets/56dbbbc4-ef38-4cb9-bae0-c939cd7dae65" />
<img width="1920" height="885" alt="Screenshot (662)" src="https://github.com/user-attachments/assets/b63ae39e-713c-46bf-8919-4377341f4b58" />

## HTML File :
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Workflow Architect — Database Design &amp; Optimization</title>
<style>
:root{
  --bg:#0B1220;
  --surface:#101A2E;
  --surface-2:#16223B;
  --border:#243047;
  --text:#E7ECF5;
  --muted:#8C99B4;
  --teal:#4FD1C5;
  --teal-dim:#2E7D74;
  --amber:#F2B84B;
  --amber-dim:#8A6621;
  --danger:#E8637A;
  --radius:10px;
  --mono: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, monospace;
  --sans: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}
[data-theme="light"]{
  --bg:#F3F5FA;
  --surface:#FFFFFF;
  --surface-2:#EEF1F8;
  --border:#D8DEEA;
  --text:#131A29;
  --muted:#5B6478;
  --teal:#0F8F82;
  --teal-dim:#CFEFEC;
  --amber:#B9791A;
  --amber-dim:#F6E3BE;
  --danger:#C23A54;
}
*{box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{
  margin:0;
  background:var(--bg);
  color:var(--text);
  font-family:var(--sans);
  transition:background .3s ease, color .3s ease;
  line-height:1.55;
}
@media (prefers-reduced-motion: reduce){
  html{scroll-behavior:auto;}
  *{animation-duration:0.001ms !important; transition-duration:0.001ms !important;}
}
a{color:var(--teal);}
::selection{background:var(--teal-dim); color:var(--text);}
button, input, textarea{font-family:inherit; color:inherit;}
.wrap{max-width:1180px; margin:0 auto; padding:0 24px;}

/* ---------- Top bar ---------- */
.topbar{
  position:sticky; top:0; z-index:50;
  background:color-mix(in srgb, var(--bg) 88%, transparent);
  backdrop-filter:blur(10px);
  border-bottom:1px solid var(--border);
}
.topbar-inner{display:flex; align-items:center; justify-content:space-between; padding:14px 24px; max-width:1180px; margin:0 auto;}
.brand{display:flex; align-items:center; gap:10px; font-weight:700; letter-spacing:.2px;}
.brand-mark{width:26px; height:26px; border-radius:6px; background:linear-gradient(135deg, var(--teal), var(--amber)); display:flex; align-items:center; justify-content:center; font-family:var(--mono); font-size:12px; color:#08131f; font-weight:700;}
.brand small{display:block; font-weight:400; color:var(--muted); font-size:11px; margin-top:1px;}
.topbar-actions{display:flex; gap:8px; align-items:center;}
.icon-btn{
  background:var(--surface); border:1px solid var(--border); color:var(--text);
  border-radius:8px; padding:8px 12px; font-size:13px; cursor:pointer;
  display:flex; align-items:center; gap:6px; transition:.2s;
}
.icon-btn:hover{border-color:var(--teal); color:var(--teal);}
.icon-btn:focus-visible, button:focus-visible, a:focus-visible, input:focus-visible, textarea:focus-visible{outline:2px solid var(--teal); outline-offset:2px;}

/* ---------- Hero ---------- */
.hero{padding:64px 24px 40px; border-bottom:1px solid var(--border); position:relative; overflow:hidden;}
.hero-inner{max-width:1180px; margin:0 auto; display:grid; grid-template-columns:1.1fr .9fr; gap:48px; align-items:center;}
@media (max-width:900px){.hero-inner{grid-template-columns:1fr;}}
.eyebrow{font-family:var(--mono); font-size:12px; color:var(--amber); letter-spacing:1.5px; text-transform:uppercase; margin-bottom:14px;}
.hero h1{font-size:44px; line-height:1.08; margin:0 0 16px; letter-spacing:-.5px;}
.hero h1 span{color:var(--teal);}
.hero p{color:var(--muted); font-size:16px; max-width:52ch; margin:0 0 26px;}
.hero-cta{display:flex; gap:12px; flex-wrap:wrap;}
.btn{
  border-radius:8px; padding:12px 20px; font-size:14px; font-weight:600; cursor:pointer; border:1px solid transparent;
  transition:transform .15s ease, box-shadow .15s ease;
}
.btn:hover{transform:translateY(-1px);}
.btn-primary{background:var(--teal); color:#06181a;}
.btn-primary:hover{box-shadow:0 6px 20px -6px var(--teal);}
.btn-ghost{background:transparent; border-color:var(--border); color:var(--text);}
.btn-ghost:hover{border-color:var(--teal); color:var(--teal);}

/* ER diagram signature element */
.er-diagram{background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:20px; position:relative; min-height:280px;}
.er-table{position:absolute; width:150px; background:var(--surface-2); border:1px solid var(--border); border-radius:8px; overflow:hidden; box-shadow:0 10px 30px -12px rgba(0,0,0,.5); animation:float 6s ease-in-out infinite;}
.er-table .th{background:var(--teal-dim); color:var(--text); font-family:var(--mono); font-size:11px; padding:6px 10px; border-bottom:1px solid var(--border); font-weight:700;}
[data-theme="light"] .er-table .th{color:#08131f;}
.er-table .row{font-family:var(--mono); font-size:10.5px; padding:5px 10px; color:var(--muted); border-bottom:1px solid var(--border);}
.er-table .row.key{color:var(--amber);}
.er-table:nth-child(1){top:10px; left:10px; animation-delay:0s;}
.er-table:nth-child(2){top:40px; right:10px; animation-delay:1.2s;}
.er-table:nth-child(3){bottom:10px; left:60px; animation-delay:2.4s;}
@keyframes float{0%,100%{transform:translateY(0);}50%{transform:translateY(-6px);}}
.er-diagram svg.lines{position:absolute; inset:0; width:100%; height:100%; pointer-events:none;}
.er-diagram svg.lines line{stroke:var(--border); stroke-width:1.5; stroke-dasharray:4 4;}

/* ---------- Section shells ---------- */
section{padding:56px 24px;}
.section-head{margin-bottom:28px;}
.section-head .tag{font-family:var(--mono); font-size:11px; color:var(--teal); text-transform:uppercase; letter-spacing:1.2px; margin-bottom:8px;}
.section-head h2{font-size:28px; margin:0 0 8px; letter-spacing:-.3px;}
.section-head p{color:var(--muted); margin:0; max-width:65ch;}

/* ---------- Progress ---------- */
.progress-wrap{background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:18px 20px; display:flex; align-items:center; gap:16px; margin-bottom:32px;}
.progress-bar{flex:1; height:8px; background:var(--surface-2); border-radius:99px; overflow:hidden;}
.progress-fill{height:100%; background:linear-gradient(90deg, var(--teal), var(--amber)); width:0%; transition:width .4s ease;}
.progress-label{font-family:var(--mono); font-size:12px; color:var(--muted); white-space:nowrap;}

/* ---------- Stage nav (tabs) ---------- */
.stage-nav{display:flex; gap:6px; overflow-x:auto; padding-bottom:6px; margin-bottom:8px; scrollbar-width:thin;}
.stage-nav button{
  flex:0 0 auto; background:var(--surface); border:1px solid var(--border); border-radius:99px;
  padding:9px 16px; font-size:12.5px; cursor:pointer; color:var(--muted); white-space:nowrap; transition:.2s;
  font-family:var(--mono);
}
.stage-nav button.active{background:var(--teal); color:#06181a; border-color:var(--teal); font-weight:700;}
.stage-nav button:hover:not(.active){border-color:var(--teal); color:var(--teal);}

/* ---------- Stage card ---------- */
.stage-panel{display:none; background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:32px; animation:fadein .35s ease;}
.stage-panel.active{display:block;}
@keyframes fadein{from{opacity:0; transform:translateY(6px);} to{opacity:1; transform:translateY(0);}}
.stage-top{display:flex; justify-content:space-between; align-items:flex-start; gap:20px; margin-bottom:8px; flex-wrap:wrap;}
.stage-title{display:flex; align-items:center; gap:12px;}
.stage-num{font-family:var(--mono); font-size:13px; color:var(--bg); background:var(--amber); width:30px; height:30px; border-radius:8px; display:flex; align-items:center; justify-content:center; font-weight:700; flex:0 0 auto;}
.stage-title h3{margin:0; font-size:22px;}
.stage-time{font-family:var(--mono); font-size:12px; color:var(--muted); border:1px solid var(--border); border-radius:99px; padding:5px 12px; white-space:nowrap;}
.stage-actions{display:flex; gap:8px;}
.chip-btn{background:var(--surface-2); border:1px solid var(--border); border-radius:8px; padding:6px 10px; font-size:12px; cursor:pointer; color:var(--muted); display:flex; align-items:center; gap:5px;}
.chip-btn:hover{color:var(--text); border-color:var(--teal);}
.chip-btn.done{background:var(--teal-dim); color:var(--text); border-color:var(--teal);}
.chip-btn.bookmarked{color:var(--amber); border-color:var(--amber);}

.grid2{display:grid; grid-template-columns:1fr 1fr; gap:28px; margin-top:22px;}
@media (max-width:800px){.grid2{grid-template-columns:1fr;}}
.block h4{font-size:13px; text-transform:uppercase; letter-spacing:.8px; color:var(--amber); font-family:var(--mono); margin:0 0 10px;}
.block ul{margin:0; padding-left:18px; color:var(--text);}
.block ul li{margin-bottom:6px;}
.block ul.muted-list li{color:var(--muted);}

.tool-table{width:100%; border-collapse:collapse; margin-top:10px; font-size:13.5px;}
.tool-table th, .tool-table td{text-align:left; padding:10px 12px; border-bottom:1px solid var(--border); vertical-align:top;}
.tool-table th{color:var(--muted); font-family:var(--mono); font-size:11px; text-transform:uppercase; letter-spacing:.6px;}
.tool-table td.tool-name{font-weight:700; color:var(--teal);}

.prompt-box{background:var(--surface-2); border:1px solid var(--border); border-left:3px solid var(--teal); border-radius:8px; padding:14px 16px; font-family:var(--mono); font-size:12.5px; color:var(--text); position:relative; margin-bottom:10px; white-space:pre-wrap;}
.copy-btn{position:absolute; top:8px; right:8px; background:var(--surface); border:1px solid var(--border); border-radius:6px; font-size:11px; padding:4px 8px; cursor:pointer; color:var(--muted);}
.copy-btn:hover{color:var(--teal); border-color:var(--teal);}

.mistake-row{display:flex; gap:10px; align-items:flex-start; margin-bottom:8px; font-size:13.5px;}
.mistake-x{color:var(--danger); font-family:var(--mono); flex:0 0 auto;}
.output-row{display:flex; gap:10px; align-items:flex-start; margin-bottom:8px; font-size:13.5px;}
.output-check{color:var(--teal); font-family:var(--mono); flex:0 0 auto;}

.notes-area{width:100%; min-height:80px; background:var(--surface-2); border:1px solid var(--border); border-radius:8px; padding:12px; font-size:13px; margin-top:8px; resize:vertical;}

/* ---------- Diagram / decision tree ---------- */
.diagram-shell{background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:24px; overflow-x:auto;}
.flow-row{display:flex; align-items:center; gap:0; min-width:800px;}
.flow-node{flex:1; background:var(--surface-2); border:1px solid var(--border); border-radius:8px; padding:14px 12px; text-align:center; font-size:12.5px; cursor:pointer; transition:.2s;}
.flow-node:hover{border-color:var(--teal); transform:translateY(-2px);}
.flow-node .n{font-family:var(--mono); color:var(--amber); font-size:11px; display:block; margin-bottom:4px;}
.flow-arrow{flex:0 0 auto; width:34px; text-align:center; color:var(--muted); font-size:18px;}

.decision-tree{background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:24px;}
.dt-q{font-family:var(--mono); font-size:13px; color:var(--teal); margin-bottom:10px;}
.dt-options{display:flex; gap:10px; flex-wrap:wrap;}
.dt-options button{background:var(--surface-2); border:1px solid var(--border); border-radius:8px; padding:10px 14px; font-size:13px; cursor:pointer;}
.dt-options button:hover{border-color:var(--teal);}
.dt-result{margin-top:16px; padding:14px; background:var(--teal-dim); border-radius:8px; font-size:13.5px; display:none; color:var(--text);}

.compare-table{width:100%; border-collapse:collapse; margin-top:12px; font-size:13px;}
.compare-table th, .compare-table td{border:1px solid var(--border); padding:10px 12px;}
.compare-table th{background:var(--surface-2); font-family:var(--mono); font-size:11px; text-transform:uppercase; color:var(--muted);}
.compare-table td.hl{color:var(--teal); font-weight:700;}

/* ---------- Summary / footer sections ---------- */
.stack-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:16px; margin-top:18px;}
.stack-card{background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:18px;}
.stack-card .role{font-family:var(--mono); font-size:11px; color:var(--muted); text-transform:uppercase; margin-bottom:6px;}
.stack-card .name{font-size:16px; font-weight:700; color:var(--teal); margin-bottom:6px;}
.stack-card .why{font-size:12.5px; color:var(--muted);}

.pill-list{display:flex; flex-wrap:wrap; gap:8px; margin-top:12px;}
.pill{background:var(--surface-2); border:1px solid var(--border); border-radius:99px; padding:6px 14px; font-size:12.5px; font-family:var(--mono);}

.res-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(240px,1fr)); gap:14px; margin-top:16px;}
.res-card{background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:16px;}
.res-card a{font-weight:700; text-decoration:none;}
.res-card p{color:var(--muted); font-size:12.5px; margin:6px 0 0;}

footer{border-top:1px solid var(--border); padding:32px 24px; text-align:center; color:var(--muted); font-size:12.5px;}

@media print{
  .topbar, .stage-nav, .stage-actions, .hero-cta, .icon-btn, .dt-options, .copy-btn{display:none !important;}
  body{background:#fff; color:#000;}
  .stage-panel{display:block !important; border:1px solid #ccc; page-break-inside:avoid; margin-bottom:24px;}
  section{padding:12px 0;}
}
</style>
</head>
<body data-theme="dark">

<div class="topbar">
  <div class="topbar-inner">
    <div class="brand">
      <div class="brand-mark">DB</div>
      <div>AI Workflow Architect
        <small>Database Design &amp; Optimization</small>
      </div>
    </div>
    <div class="topbar-actions">
      <button class="icon-btn" id="themeToggle">☾ Theme</button>
      <button class="icon-btn" id="printBtn">⎙ Print Guide</button>
    </div>
  </div>
</div>

<section class="hero">
  <div class="hero-inner">
    <div>
      <div class="eyebrow">Backend Development → Database Design &amp; Optimization</div>
      <h1>Ship a schema that <span>scales</span>, not one that survives launch day.</h1>
      <p>A complete, end-to-end AI-augmented workflow — from requirements gathering through indexing, query tuning, and long-term maintenance — with the tools, prompts, and checkpoints for each stage.</p>
      <div class="hero-cta">
        <button class="btn btn-primary" onclick="document.getElementById('stages').scrollIntoView()">Start the workflow</button>
        <button class="btn btn-ghost" onclick="document.getElementById('diagram').scrollIntoView()">View the full map</button>
      </div>
    </div>
    <div class="er-diagram">
      <svg class="lines"><line x1="90" y1="60" x2="230" y2="90"/><line x1="150" y1="130" x2="230" y2="90"/></svg>
      <div class="er-table">
        <div class="th">users</div>
        <div class="row key">id ⚿ PK</div>
        <div class="row">email</div>
        <div class="row">created_at</div>
      </div>
      <div class="er-table">
        <div class="th">orders</div>
        <div class="row key">id ⚿ PK</div>
        <div class="row">user_id ⚷ FK</div>
        <div class="row">idx_status</div>
      </div>
      <div class="er-table">
        <div class="th">order_items</div>
        <div class="row key">id ⚿ PK</div>
        <div class="row">order_id ⚷ FK</div>
        <div class="row">sku</div>
      </div>
    </div>
  </div>
</section>

<section id="stages">
  <div class="wrap">
    <div class="section-head">
      <div class="tag">The workflow</div>
      <h2>Six stages, planning to production</h2>
      <p>Track progress, bookmark stages you'll revisit, and jot notes as you go — everything saves locally in your browser.</p>
    </div>

    <div class="progress-wrap">
      <div class="progress-label" id="progressLabel">0 / 6 stages complete</div>
      <div class="progress-bar"><div class="progress-fill" id="progressFill"></div></div>
      <button class="icon-btn" id="resetBtn">↺ Reset</button>
    </div>

    <div class="stage-nav" id="stageNav"></div>
    <div id="stagePanels"></div>
  </div>
</section>

<section id="diagram">
  <div class="wrap">
    <div class="section-head">
      <div class="tag">Visual map</div>
      <h2>End-to-end flow</h2>
      <p>Click a node to jump to that stage.</p>
    </div>
    <div class="diagram-shell">
      <div class="flow-row" id="flowRow"></div>
    </div>
  </div>
</section>

<section>
  <div class="wrap">
    <div class="section-head">
      <div class="tag">Decision support</div>
      <h2>Which database model fits?</h2>
    </div>
    <div class="decision-tree">
      <div class="dt-q">Q1. Does your data have complex relationships that need multi-table joins and strict consistency?</div>
      <div class="dt-options">
        <button onclick="showResult('rel-yes')">Yes — relational integrity matters</button>
        <button onclick="showResult('rel-no')">No — flexible, document-like records</button>
      </div>
      <div class="dt-result" id="res-rel-yes"><strong>Go relational (PostgreSQL / MySQL).</strong> Model with normalized tables (3NF as a baseline), enforce foreign keys, and plan indexes around your read patterns before writing a line of app code.</div>
      <div class="dt-result" id="res-rel-no"><strong>Consider a document or wide-column store (MongoDB / DynamoDB).</strong> Design around access patterns first — decide your queries, then shape the documents to match them.</div>
    </div>
  </div>
</section>

<section>
  <div class="wrap">
    <div class="section-head">
      <div class="tag">Tool landscape</div>
      <h2>How the AI tools compare</h2>
    </div>
    <table class="compare-table">
      <tr><th>Tool</th><th>Best for</th><th>Strength</th><th>Watch out for</th></tr>
      <tr><td class="hl">Claude (Sonnet/Opus)</td><td>Schema reasoning, migration review, long context</td><td>Explains tradeoffs, catches normalization issues</td><td>Verify generated DDL against your actual dialect</td></tr>
      <tr><td class="hl">dbdiagram.io + AI</td><td>Visual ER modeling</td><td>Fast diagram-to-DDL export</td><td>Not ideal for deep query tuning</td></tr>
      <tr><td class="hl">EverSQL / SQLAI</td><td>Query optimization</td><td>Auto index suggestions from real query logs</td><td>Needs production-like data to be accurate</td></tr>
      <tr><td class="hl">pgAdmin/EXPLAIN + AI copilot</td><td>Reading query plans</td><td>Ties AI reasoning to real EXPLAIN output</td><td>Still requires you to understand plan basics</td></tr>
      <tr><td class="hl">Datadog/New Relic AI insights</td><td>Ongoing monitoring</td><td>Flags slow queries and drift over time</td><td>Cost scales with data volume</td></tr>
    </table>
  </div>
</section>

<section>
  <div class="wrap">
    <div class="section-head">
      <div class="tag">Wrap-up</div>
      <h2>Workflow summary</h2>
      <p>Requirements → conceptual model → normalized schema → indexing strategy → query optimization → monitored, scaling system. Each handoff should leave you with a reviewable artifact (ERD, DDL, EXPLAIN plan, or dashboard) before moving forward.</p>
    </div>

    <div class="section-head" style="margin-top:36px;">
      <div class="tag">Recommended stack</div>
      <h2>Your default toolkit</h2>
    </div>
    <div class="stack-grid">
      <div class="stack-card"><div class="role">Modeling</div><div class="name">Claude + dbdiagram.io</div><div class="why">Reason through entities in chat, export the finalized ERD to DDL.</div></div>
      <div class="stack-card"><div class="role">Schema review</div><div class="name">Claude (long context)</div><div class="why">Paste full schema for normalization and constraint checks.</div></div>
      <div class="stack-card"><div class="role">Query tuning</div><div class="name">EverSQL / native EXPLAIN</div><div class="why">Pairs automated suggestions with plan-level ground truth.</div></div>
      <div class="stack-card"><div class="role">Monitoring</div><div class="name">Datadog APM</div><div class="why">Surfaces slow queries and index drift after ship.</div></div>
    </div>

    <div class="section-head" style="margin-top:36px;">
      <div class="tag">Keep learning</div>
      <h2>Resources &amp; communities</h2>
    </div>
    <div class="res-grid">
      <div class="res-card"><a href="https://use-the-index-luke.com" target="_blank" rel="noopener">Use The Index, Luke!</a><p>Free, deep guide to SQL indexing.</p></div>
      <div class="res-card"><a href="https://www.postgresql.org/docs/current/performance-tips.html" target="_blank" rel="noopener">PostgreSQL Performance Tips</a><p>Official tuning documentation.</p></div>
      <div class="res-card"><a href="https://www.reddit.com/r/Database/" target="_blank" rel="noopener">r/Database</a><p>Community troubleshooting and design review.</p></div>
      <div class="res-card"><a href="https://www.reddit.com/r/PostgreSQL/" target="_blank" rel="noopener">r/PostgreSQL</a><p>Engine-specific tuning discussions.</p></div>
    </div>

    <div class="section-head" style="margin-top:36px;">
      <div class="tag">Search this</div>
      <h2>Keywords worth researching</h2>
    </div>
    <div class="pill-list">
      <span class="pill">database normalization 3NF</span>
      <span class="pill">composite index strategy</span>
      <span class="pill">query execution plan reading</span>
      <span class="pill">N+1 query problem</span>
      <span class="pill">database sharding vs partitioning</span>
      <span class="pill">connection pooling</span>
      <span class="pill">read replica lag</span>
    </div>

    <div class="section-head" style="margin-top:36px;">
      <div class="tag">More prompts</div>
      <h2>Additional AI prompts to reuse</h2>
    </div>
    <div class="prompt-box">Review this schema for redundant data and suggest which tables violate 3rd normal form.<button class="copy-btn" onclick="copyPrompt(this)">Copy</button></div>
    <div class="prompt-box">Here is a slow query and its EXPLAIN output — identify the bottleneck and suggest an index.<button class="copy-btn" onclick="copyPrompt(this)">Copy</button></div>
    <div class="prompt-box">Given these access patterns, should I denormalize this relationship for read performance?<button class="copy-btn" onclick="copyPrompt(this)">Copy</button></div>

    <div class="section-head" style="margin-top:36px;">
      <div class="tag">Looking ahead</div>
      <h2>Future automation opportunities</h2>
    </div>
    <ul class="block-ul">
      <li>Auto-generate migration scripts from schema diffs using an AI reviewer as a gate before merge.</li>
      <li>Feed slow-query logs into an AI agent weekly to propose index additions automatically.</li>
      <li>Use AI to draft synthetic load-test datasets that mirror production data shape without exposing real records.</li>
    </ul>
  </div>
</section>

<footer>Built with the AI Workflow Architect · Your progress, notes, and bookmarks are stored locally in this browser only.</footer>

<script>
const STAGES = [
  {
    id:'requirements', title:'Requirements & Data Modeling', time:'2–4 hrs',
    objectives:['Capture what the system needs to store and how it will be queried','Identify entities, relationships, and cardinalities','Set scale expectations (rows, growth rate, read/write ratio)'],
    tasks:['Interview stakeholders or review product spec for data needs','List every entity and its attributes','Draft a conceptual ER diagram','Define read vs write access patterns'],
    tools:[
      {name:'Claude', why:'Turns loose requirements into a structured entity list and asks clarifying questions you missed', alt:'ChatGPT'},
      {name:'dbdiagram.io', why:'Fast visual ERD sketching with DBML syntax', alt:'Lucidchart, drawSQL'},
      {name:'Miro AI', why:'Collaborative whiteboarding for stakeholder workshops', alt:'FigJam'}
    ],
    prompts:['I\'m building [product]. Here\'s the feature list: [paste]. List the core entities, their key attributes, and relationships I\'ll need to model.'],
    best:['Model access patterns before tables, not after','Involve whoever owns the business logic, not just engineering','Write down growth assumptions — they drive every later decision'],
    mistakes:['Jumping straight to tables without listing relationships first','Ignoring how data will be queried, only how it will be stored','Skipping edge cases like soft deletes or multi-tenancy up front'],
    outputs:['A conceptual ER diagram','A written list of access patterns','Rough scale estimates (rows/year, peak QPS)'],
    tips:['Keep a running glossary of entity names — naming drift causes schema pain later.']
  },
  {
    id:'schema', title:'Schema Design & Normalization', time:'3–6 hrs',
    objectives:['Convert the conceptual model into a normalized relational schema','Choose appropriate data types and constraints','Decide where to intentionally denormalize'],
    tasks:['Draft table definitions with primary/foreign keys','Normalize to 3NF, then evaluate selective denormalization','Define constraints (NOT NULL, UNIQUE, CHECK)','Write the initial migration'],
    tools:[
      {name:'Claude', why:'Reviews full DDL for normalization violations and suggests fixes in context', alt:'GitHub Copilot Chat'},
      {name:'dbdiagram.io', why:'Exports ERD directly to SQL DDL', alt:'DataGrip schema designer'},
      {name:'Prisma / Drizzle AI assist', why:'Type-safe schema-as-code with inline suggestions', alt:'TypeORM'}
    ],
    prompts:['Here is my draft schema: [paste DDL]. Check for normalization issues, missing constraints, and suggest appropriate data types.'],
    best:['Default to 3NF; denormalize only with a measured reason','Use surrogate keys unless a natural key is truly stable','Name columns consistently (snake_case, singular table names or plural — pick one)'],
    mistakes:['Using VARCHAR for everything instead of proper types (dates, enums, numerics)','Skipping foreign key constraints "for speed"','Over-normalizing to the point of requiring 6+ joins for common reads'],
    outputs:['Finalized DDL / schema-as-code file','ER diagram matching the schema exactly','A short doc explaining any denormalization decisions'],
    tips:['Run the schema through a linter or AI review before the first migration ships to prod.']
  },
  {
    id:'indexing', title:'Indexing Strategy', time:'2–5 hrs',
    objectives:['Identify which columns need indexes based on real query patterns','Balance read speed against write overhead','Plan composite indexes for multi-column filters'],
    tasks:['List your top 10 most frequent queries','Map each query to existing or needed indexes','Add composite indexes matching filter + sort order','Remove unused or duplicate indexes'],
    tools:[
      {name:'EverSQL', why:'Analyzes queries and recommends specific indexes automatically', alt:'SQLAI.ai'},
      {name:'Claude', why:'Explains index tradeoffs and reasons about composite column order', alt:'ChatGPT'},
      {name:'pganalyze', why:'Finds unused indexes and index bloat in Postgres', alt:'pg_stat_statements manually'}
    ],
    prompts:['Here are my most common queries: [paste]. What indexes (including composite) would you recommend, and in what column order?'],
    best:['Order composite index columns by equality filters first, then range filters, then sort columns','Index foreign keys used in joins','Periodically review and drop unused indexes'],
    mistakes:['Indexing every column "just in case"','Ignoring write-heavy tables where extra indexes slow inserts','Wrong column order in composite indexes, making them unused'],
    outputs:['An indexing plan mapped to real queries','Migration adding the finalized indexes','A short list of indexes intentionally not added, with rationale'],
    tips:['Re-run this stage after 30 days of production traffic — real usage differs from assumptions.']
  },
  {
    id:'query-opt', title:'Query Optimization', time:'3–6 hrs',
    objectives:['Find and fix slow or inefficient queries','Understand and read query execution plans','Eliminate N+1 query patterns in application code'],
    tasks:['Run EXPLAIN/EXPLAIN ANALYZE on slow queries','Rewrite queries flagged for sequential scans','Batch or eager-load queries causing N+1 issues','Benchmark before/after each change'],
    tools:[
      {name:'Claude', why:'Reads EXPLAIN output and translates it into plain-language bottlenecks', alt:'ChatGPT'},
      {name:'EverSQL', why:'Auto-rewrites inefficient SQL and shows the diff', alt:'pgHero'},
      {name:'pgAdmin / DataGrip', why:'Visual EXPLAIN plan viewer for the actual engine', alt:'native psql \\d+'}
    ],
    prompts:['Here is a slow query and its EXPLAIN ANALYZE output: [paste]. What is the bottleneck, and how would you rewrite it?'],
    best:['Always benchmark with production-like data volume, not a near-empty dev DB','Fix one query at a time and re-measure','Watch for sequential scans on large tables as the first red flag'],
    mistakes:['Optimizing queries against a mostly-empty local database','Adding indexes without checking if the planner actually uses them','Ignoring ORM-generated queries — they\'re a common N+1 source'],
    outputs:['A list of optimized queries with before/after timing','Updated ORM code avoiding N+1 patterns','Documented query plan baselines for key endpoints'],
    tips:['Log slow queries above a threshold (e.g. 100ms) in production to keep finding new candidates.']
  },
  {
    id:'testing', title:'Performance Testing & Monitoring', time:'4–8 hrs',
    objectives:['Validate the schema and indexes under realistic load','Set up ongoing visibility into database health','Establish performance baselines and alert thresholds'],
    tasks:['Generate realistic test data at production scale','Run load tests against key endpoints','Set up dashboards for query latency and connection pool usage','Configure alerts for slow queries and lock contention'],
    tools:[
      {name:'k6 / Locust (AI-assisted scripting)', why:'AI helps draft load test scripts matching real traffic shapes', alt:'JMeter'},
      {name:'Datadog / New Relic', why:'AI-driven anomaly detection on query latency over time', alt:'Grafana + Prometheus'},
      {name:'Claude', why:'Helps design realistic synthetic datasets and interpret dashboard anomalies', alt:'ChatGPT'}
    ],
    prompts:['Help me design a synthetic dataset generator for a [entity] table that mirrors realistic production distribution (not uniform random).'],
    best:['Test with data skew, not perfectly even distributions','Set alert thresholds based on measured baselines, not guesses','Include connection pool exhaustion in your test scenarios'],
    mistakes:['Load testing with unrealistic, uniformly distributed test data','No alerting until after a production incident','Ignoring connection pool limits until they\'re hit live'],
    outputs:['A load test report with latency percentiles (p50/p95/p99)','Live monitoring dashboard','Alert rules for slow queries and pool saturation'],
    tips:['Re-baseline your alert thresholds every quarter as traffic grows.']
  },
  {
    id:'scaling', title:'Scaling & Maintenance', time:'Ongoing',
    objectives:['Plan for growth beyond current capacity','Keep the schema healthy as the product evolves','Establish a review cadence for schema changes'],
    tasks:['Evaluate read replicas, partitioning, or sharding as needed','Set up a migration review process for future changes','Schedule periodic index and query audits','Document the schema for the whole team'],
    tools:[
      {name:'Claude', why:'Reviews proposed migrations for backward compatibility and risk', alt:'GitHub Copilot Chat'},
      {name:'pganalyze', why:'Ongoing automated health and index audits', alt:'Percona Monitoring'},
      {name:'dbdocs.io', why:'Keeps schema documentation in sync automatically', alt:'SchemaSpy'}
    ],
    prompts:['Here is a proposed migration: [paste]. Will this be backward-compatible with existing running application code during rollout?'],
    best:['Require migration review before merge, even for "small" changes','Prefer additive migrations; avoid breaking changes in a single deploy','Keep schema docs versioned alongside the codebase'],
    mistakes:['Running destructive migrations without a rollback plan','Letting schema documentation go stale after the first few months','Scaling vertically indefinitely instead of planning for partitioning early'],
    outputs:['A living schema documentation site','A migration review checklist','A quarterly database health report'],
    tips:['Automate a monthly "unused index and dead table" report so cleanup never gets skipped.']
  }
];

const stageNav = document.getElementById('stageNav');
const stagePanels = document.getElementById('stagePanels');
const flowRow = document.getElementById('flowRow');

let state = JSON.parse(localStorage.getItem('dbWorkflowState') || '{}');
state.done = state.done || {};
state.bookmarks = state.bookmarks || {};
state.notes = state.notes || {};
let activeStage = state.activeStage || STAGES[0].id;

function saveState(){ localStorage.setItem('dbWorkflowState', JSON.stringify(state)); }

function renderNav(){
  stageNav.innerHTML = STAGES.map((s,i)=>`<button data-id="${s.id}" class="${s.id===activeStage?'active':''}">${state.done[s.id]?'✓ ':''}${i+1}. ${s.title}</button>`).join('');
  stageNav.querySelectorAll('button').forEach(b=>b.addEventListener('click', ()=>{ activeStage=b.dataset.id; state.activeStage=activeStage; saveState(); render(); }));
}

function renderFlow(){
  flowRow.innerHTML = STAGES.map((s,i)=>`<div class="flow-node" data-id="${s.id}"><span class="n">0${i+1}</span>${s.title}</div>${i<STAGES.length-1?'<div class="flow-arrow">→</div>':''}`).join('');
  flowRow.querySelectorAll('.flow-node').forEach(n=>n.addEventListener('click', ()=>{
    activeStage=n.dataset.id; state.activeStage=activeStage; saveState(); render();
    document.getElementById('stages').scrollIntoView();
  }));
}

function renderPanels(){
  stagePanels.innerHTML = STAGES.map((s,i)=>`
    <div class="stage-panel ${s.id===activeStage?'active':''}" id="panel-${s.id}">
      <div class="stage-top">
        <div class="stage-title">
          <div class="stage-num">${i+1}</div>
          <h3>${s.title}</h3>
        </div>
        <div class="stage-time">⏱ ${s.time}</div>
      </div>
      <div class="stage-actions" style="margin:14px 0 6px;">
        <button class="chip-btn ${state.done[s.id]?'done':''}" onclick="toggleDone('${s.id}')">${state.done[s.id]?'✓ Complete':'Mark complete'}</button>
        <button class="chip-btn ${state.bookmarks[s.id]?'bookmarked':''}" onclick="toggleBookmark('${s.id}')">${state.bookmarks[s.id]?'★ Bookmarked':'☆ Bookmark'}</button>
      </div>

      <div class="grid2">
        <div class="block"><h4>Objectives</h4><ul>${s.objectives.map(o=>`<li>${o}</li>`).join('')}</ul></div>
        <div class="block"><h4>Tasks</h4><ul>${s.tasks.map(t=>`<li>${t}</li>`).join('')}</ul></div>
      </div>

      <div class="block" style="margin-top:22px;">
        <h4>Best AI tools for this stage</h4>
        <table class="tool-table">
          <tr><th>Tool</th><th>Why it's recommended</th><th>Alternative</th></tr>
          ${s.tools.map(t=>`<tr><td class="tool-name">${t.name}</td><td>${t.why}</td><td>${t.alt}</td></tr>`).join('')}
        </table>
      </div>

      <div class="block" style="margin-top:22px;">
        <h4>Prompt example</h4>
        ${s.prompts.map(p=>`<div class="prompt-box">${p}<button class="copy-btn" onclick="copyPrompt(this)">Copy</button></div>`).join('')}
      </div>

      <div class="grid2" style="margin-top:22px;">
        <div class="block"><h4>Best practices</h4><ul>${s.best.map(b=>`<li>${b}</li>`).join('')}</ul></div>
        <div class="block"><h4>Common mistakes</h4>${s.mistakes.map(m=>`<div class="mistake-row"><span class="mistake-x">✕</span><span>${m}</span></div>`).join('')}</div>
      </div>

      <div class="grid2" style="margin-top:22px;">
        <div class="block"><h4>Expected outputs</h4>${s.outputs.map(o=>`<div class="output-row"><span class="output-check">✓</span><span>${o}</span></div>`).join('')}</div>
        <div class="block"><h4>Efficiency tips</h4><ul class="muted-list">${s.tips.map(t=>`<li>${t}</li>`).join('')}</ul></div>
      </div>

      <div class="block" style="margin-top:22px;">
        <h4>Your notes</h4>
        <textarea class="notes-area" placeholder="Jot notes for this stage..." oninput="saveNote('${s.id}', this.value)">${state.notes[s.id]||''}</textarea>
      </div>
    </div>
  `).join('');
}

function toggleDone(id){ state.done[id] = !state.done[id]; saveState(); render(); }
function toggleBookmark(id){ state.bookmarks[id] = !state.bookmarks[id]; saveState(); render(); }
function saveNote(id, val){ state.notes[id] = val; saveState(); }

function renderProgress(){
  const total = STAGES.length;
  const done = STAGES.filter(s=>state.done[s.id]).length;
  document.getElementById('progressLabel').textContent = `${done} / ${total} stages complete`;
  document.getElementById('progressFill').style.width = (done/total*100)+'%';
}

function render(){
  renderNav();
  renderPanels();
  renderProgress();
}

function copyPrompt(btn){
  const text = btn.parentElement.textContent.replace('Copy','').trim();
  navigator.clipboard.writeText(text).then(()=>{ btn.textContent='Copied!'; setTimeout(()=>btn.textContent='Copy',1500); });
}

function showResult(which){
  document.querySelectorAll('.dt-result').forEach(r=>r.style.display='none');
  document.getElementById('res-'+which).style.display='block';
}

document.getElementById('resetBtn').addEventListener('click', ()=>{
  if(confirm('Reset all progress, bookmarks, and notes?')){
    state = {done:{}, bookmarks:{}, notes:{}, activeStage: STAGES[0].id};
    activeStage = STAGES[0].id;
    saveState();
    render();
  }
});

document.getElementById('printBtn').addEventListener('click', ()=>window.print());

const themeToggle = document.getElementById('themeToggle');
function applyTheme(t){
  document.body.setAttribute('data-theme', t);
  themeToggle.textContent = t==='dark' ? '☾ Theme' : '☀ Theme';
  localStorage.setItem('dbWorkflowTheme', t);
}
applyTheme(localStorage.getItem('dbWorkflowTheme') || 'dark');
themeToggle.addEventListener('click', ()=>{
  applyTheme(document.body.getAttribute('data-theme')==='dark' ? 'light' : 'dark');
});

renderFlow();
render();
</script>
</body>
</html>
