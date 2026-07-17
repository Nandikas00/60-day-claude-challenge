# Today I Built Content Intelligence Studio using claude :

## Key Learnings :
- Learned how AI can analyze content quality and provide actionable recommendations to improve clarity, engagement, and overall effectiveness.
- Gained practical experience in evaluating content using metrics such as readability, tone, SEO optimization, audience alignment, and keyword usage.
- Explored prompt engineering techniques to generate personalized content insights and optimization strategies.
- Understood the importance of balancing search engine optimization with user-focused, high-quality content.
- Learned how AI-driven analytics can identify content gaps, highlight improvement opportunities, and support data-driven content decisions.
- Built an interactive dashboard that visualizes content scores, performance metrics, and AI-generated recommendations in an easy-to-understand format.
- Improved frontend development skills by creating responsive interfaces with dynamic reports, charts, and real-time feedback.
- Strengthened understanding of how AI can streamline content strategy, improve productivity, and enhance digital communication.

### Output Screenshots :
<img width="1600" height="1299" alt="WhatsApp Image 2026-07-17 at 10 44 03 PM" src="https://github.com/user-attachments/assets/1105d21a-7cc4-42a5-99e1-bf7f23eec3ec" />


#### HTML File :

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Content Intelligence Studio</title>
<style>
:root{
  --ink:#0A0E17;
  --panel:#111726;
  --panel-2:#161D30;
  --line:#232C42;
  --paper:#ECEEF5;
  --slate:#8790A6;
  --slate-dim:#5C6580;
  --amber:#F5A623;
  --amber-dim:#8A6420;
  --teal:#3ECF8E;
  --coral:#FF6B6B;
  --violet:#8B7CF6;
  --display: Georgia, 'Iowan Old Style', 'Palatino Linotype', serif;
  --body: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
  --mono: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, monospace;
  --r: 14px;
}
*{box-sizing:border-box; margin:0; padding:0;}
html{color-scheme:dark;}
body{
  background:
    radial-gradient(ellipse 900px 500px at 15% -10%, rgba(139,124,246,.10), transparent 60%),
    radial-gradient(ellipse 700px 500px at 100% 0%, rgba(62,207,142,.08), transparent 55%),
    var(--ink);
  color:var(--paper);
  font-family:var(--body);
  line-height:1.5;
  min-height:100vh;
  -webkit-font-smoothing:antialiased;
}
@media (prefers-reduced-motion: reduce){ *{animation-duration:.001ms !important; transition-duration:.001ms !important;} }

a{color:inherit;}
::selection{background:var(--amber); color:#1a1400;}
::-webkit-scrollbar{width:10px; height:10px;}
::-webkit-scrollbar-thumb{background:var(--line); border-radius:8px;}
::-webkit-scrollbar-track{background:transparent;}

button{font-family:inherit; cursor:pointer;}
:focus-visible{outline:2px solid var(--amber); outline-offset:2px;}

/* ---------- Shell ---------- */
.shell{max-width:1400px; margin:0 auto; padding:28px 28px 80px;}

.topbar{
  display:flex; align-items:center; justify-content:space-between; gap:16px;
  padding-bottom:24px; margin-bottom:28px; border-bottom:1px solid var(--line);
}
.brand{display:flex; align-items:baseline; gap:10px;}
.brand .mark{
  width:34px; height:34px; border-radius:9px;
  background:linear-gradient(140deg, var(--amber), var(--violet));
  display:inline-flex; align-items:center; justify-content:center;
  font-family:var(--display); font-weight:700; font-size:17px; color:#140f00;
  flex:0 0 auto;
}
.brand h1{font-family:var(--display); font-weight:600; font-size:21px; letter-spacing:.2px;}
.brand .tag{font-size:12px; color:var(--slate); letter-spacing:.4px; text-transform:uppercase; margin-left:2px;}
.mode-pill{
  font-size:11.5px; color:var(--slate); border:1px solid var(--line); padding:6px 12px; border-radius:999px;
  display:flex; align-items:center; gap:8px; background:var(--panel);
}
.mode-pill b{color:var(--paper); font-weight:600;}
.dot{width:6px; height:6px; border-radius:50%; background:var(--teal); box-shadow:0 0 8px var(--teal);}

/* ---------- Layout ---------- */
.layout{display:grid; grid-template-columns:340px 1fr; gap:24px; align-items:start;}
@media (max-width:980px){ .layout{grid-template-columns:1fr;} }

.card{
  background:linear-gradient(180deg, var(--panel), var(--panel-2));
  border:1px solid var(--line); border-radius:var(--r);
  padding:20px;
}
.card + .card{margin-top:20px;}
.card h2{font-family:var(--display); font-size:15.5px; font-weight:600; margin-bottom:4px;}
.card .sub{font-size:12.3px; color:var(--slate); margin-bottom:16px;}

/* ---------- Config controls ---------- */
.field{margin-bottom:14px;}
.field label{display:block; font-size:11.5px; text-transform:uppercase; letter-spacing:.5px; color:var(--slate); margin-bottom:7px;}
.seg{display:flex; flex-wrap:wrap; gap:6px;}
.seg button{
  flex:1 1 auto; min-width:max-content; padding:8px 12px; font-size:12.5px; border-radius:8px;
  border:1px solid var(--line); background:rgba(255,255,255,.02); color:var(--slate);
  transition:all .15s ease;
}
.seg button:hover{border-color:var(--slate-dim); color:var(--paper);}
.seg button.active{background:rgba(245,166,35,.12); border-color:var(--amber); color:var(--amber); font-weight:600;}

.upload-zone{
  border:1.5px dashed var(--line); border-radius:10px; padding:20px 14px; text-align:center;
  cursor:pointer; transition:all .15s ease; background:rgba(255,255,255,.015);
}
.upload-zone:hover, .upload-zone.drag{border-color:var(--amber); background:rgba(245,166,35,.05);}
.upload-zone svg{width:26px; height:26px; opacity:.5; margin-bottom:8px;}
.upload-zone p{font-size:12.5px; color:var(--slate);}
.upload-zone .hint{font-size:11px; color:var(--slate-dim); margin-top:3px;}
input[type=file]{display:none;}

.preview-wrap{position:relative; margin-top:12px; border-radius:10px; overflow:hidden; border:1px solid var(--line);}
.preview-wrap img{width:100%; display:block; max-height:280px; object-fit:cover;}
.preview-remove{
  position:absolute; top:8px; right:8px; background:rgba(10,14,23,.85); border:1px solid var(--line);
  color:var(--paper); width:26px; height:26px; border-radius:7px; font-size:14px; line-height:1;
}

textarea{
  width:100%; resize:vertical; min-height:90px; background:rgba(255,255,255,.02);
  border:1px solid var(--line); border-radius:9px; color:var(--paper); font-family:var(--body);
  font-size:13px; padding:12px; line-height:1.55;
}
textarea:focus-visible{outline:2px solid var(--amber);}
textarea::placeholder{color:var(--slate-dim);}

.run-btn{
  width:100%; padding:13px; border-radius:10px; border:none; margin-top:6px;
  background:linear-gradient(120deg, var(--amber), #e08a1c); color:#1a1200; font-weight:700; font-size:13.5px;
  letter-spacing:.2px; display:flex; align-items:center; justify-content:center; gap:8px;
  transition:transform .15s ease, box-shadow .15s ease;
  box-shadow:0 8px 24px -8px rgba(245,166,35,.5);
}
.run-btn:hover:not(:disabled){transform:translateY(-1px); box-shadow:0 10px 28px -6px rgba(245,166,35,.6);}
.run-btn:disabled{opacity:.45; cursor:not-allowed; box-shadow:none;}
.run-btn.secondary{
  background:rgba(255,255,255,.03); color:var(--paper); border:1px solid var(--line); box-shadow:none;
}
.run-btn.secondary:hover:not(:disabled){border-color:var(--slate-dim);}

.err-box{
  margin-top:12px; padding:11px 13px; border-radius:9px; background:rgba(255,107,107,.08);
  border:1px solid rgba(255,107,107,.35); color:#ffb3b3; font-size:12.3px; display:none;
}
.err-box.show{display:block;}
.err-box button{margin-top:8px; background:rgba(255,107,107,.15); border:1px solid rgba(255,107,107,.4); color:#ffd7d7; padding:6px 12px; border-radius:6px; font-size:11.5px;}

/* ---------- Pipeline (signature element) ---------- */
.pipeline{display:flex; flex-direction:column; gap:0;}
.pnode{
  display:flex; align-items:flex-start; gap:14px; padding:12px 4px; position:relative;
}
.pnode::before{
  content:''; position:absolute; left:17px; top:38px; bottom:-6px; width:1.5px; background:var(--line);
}
.pnode:last-child::before{display:none;}
.pnode .pdot{
  width:35px; height:35px; border-radius:9px; border:1.5px solid var(--line); flex:0 0 auto;
  display:flex; align-items:center; justify-content:center; font-size:14px; background:var(--panel-2);
  color:var(--slate-dim); transition:all .25s ease; z-index:1;
}
.pnode.active .pdot{border-color:var(--amber); color:var(--amber); background:rgba(245,166,35,.1); animation:pulse 1.4s ease-in-out infinite;}
.pnode.done .pdot{border-color:var(--teal); color:var(--teal); background:rgba(62,207,142,.1);}
.pnode.error .pdot{border-color:var(--coral); color:var(--coral); background:rgba(255,107,107,.1);}
@keyframes pulse{0%,100%{box-shadow:0 0 0 0 rgba(245,166,35,.35);} 50%{box-shadow:0 0 0 6px rgba(245,166,35,0);}}
.pinfo{padding-top:4px;}
.pinfo .pname{font-size:13px; font-weight:600;}
.pinfo .pfocus{font-size:11.8px; color:var(--slate); margin-top:2px; line-height:1.45;}
.pinfo .pstatus{font-size:10.5px; text-transform:uppercase; letter-spacing:.5px; color:var(--slate-dim); margin-top:5px;}
.pnode.active .pstatus{color:var(--amber);}
.pnode.done .pstatus{color:var(--teal);}
.pnode.error .pstatus{color:var(--coral);}

/* ---------- Activity log ---------- */
.log{
  background:#070A11; border:1px solid var(--line); border-radius:10px; padding:12px 14px;
  font-family:var(--mono); font-size:11.3px; color:var(--slate); max-height:220px; overflow-y:auto;
}
.log .line{padding:2px 0; display:flex; gap:8px;}
.log .line .t{color:var(--slate-dim); flex:0 0 auto;}
.log .line.ok{color:var(--teal);}
.log .line.warn{color:var(--amber);}
.log .line.err{color:var(--coral);}

/* ---------- Main / Results ---------- */
.empty-state{
  min-height:520px; display:flex; flex-direction:column; align-items:center; justify-content:center;
  text-align:center; border:1px solid var(--line); border-radius:var(--r);
  background:linear-gradient(180deg, var(--panel), var(--panel-2)); padding:40px;
}
.empty-state .glyph{font-family:var(--display); font-size:52px; color:var(--line); margin-bottom:14px;}
.empty-state h3{font-family:var(--display); font-size:19px; margin-bottom:8px;}
.empty-state p{font-size:13px; color:var(--slate); max-width:380px;}

.tabs{display:flex; gap:6px; border-bottom:1px solid var(--line); margin-bottom:22px; overflow-x:auto;}
.tabs button{
  padding:11px 16px; font-size:13px; color:var(--slate); background:none; border:none;
  border-bottom:2px solid transparent; white-space:nowrap; font-weight:500;
}
.tabs button.active{color:var(--paper); border-color:var(--amber); font-weight:700;}
.tab-panel{display:none; animation:fadein .35s ease;}
.tab-panel.active{display:block;}
@keyframes fadein{from{opacity:0; transform:translateY(6px);} to{opacity:1; transform:translateY(0);}}

/* Score hero */
.score-hero{display:grid; grid-template-columns:220px 1fr; gap:32px; align-items:center; margin-bottom:24px;}
@media (max-width:700px){.score-hero{grid-template-columns:1fr; justify-items:center; text-align:center;}}
.gauge-wrap{position:relative; width:200px; height:200px;}
.gauge-num{
  position:absolute; inset:0; display:flex; flex-direction:column; align-items:center; justify-content:center;
}
.gauge-num .n{font-family:var(--display); font-size:46px; font-weight:700;}
.gauge-num .l{font-size:10.5px; text-transform:uppercase; letter-spacing:1px; color:var(--slate); margin-top:2px;}
.score-meta h3{font-family:var(--display); font-size:22px; margin-bottom:8px;}
.score-meta p{font-size:13.5px; color:var(--slate); line-height:1.65;}

.chips{display:flex; gap:8px; flex-wrap:wrap; margin-top:14px;}
.chip{font-size:11px; padding:5px 11px; border-radius:999px; border:1px solid var(--line); color:var(--slate);}
.chip.pos{border-color:rgba(62,207,142,.4); color:var(--teal); background:rgba(62,207,142,.06);}
.chip.risk{border-color:rgba(255,107,107,.4); color:var(--coral); background:rgba(255,107,107,.06);}

/* category breakdown bars */
.cat-grid{display:grid; gap:14px;}
.cat-row{display:grid; grid-template-columns:150px 1fr 42px; align-items:center; gap:14px;}
.cat-row .cname{font-size:12.8px; font-weight:600;}
.cat-row .cname span{display:block; font-size:11px; font-weight:400; color:var(--slate-dim); margin-top:1px;}
.bar-track{height:8px; border-radius:6px; background:var(--line); overflow:hidden;}
.bar-fill{height:100%; border-radius:6px; background:linear-gradient(90deg, var(--violet), var(--amber)); width:0%; transition:width 1s cubic-bezier(.2,.8,.2,1);}
.cat-row .cscore{font-size:13px; font-weight:700; text-align:right; font-family:var(--mono);}

/* reviewer cards */
.reviewer-card{border:1px solid var(--line); border-radius:12px; padding:18px 20px; margin-bottom:16px; background:rgba(255,255,255,.015);}
.reviewer-head{display:flex; align-items:center; justify-content:space-between; gap:12px; margin-bottom:10px; flex-wrap:wrap;}
.reviewer-head h4{font-family:var(--display); font-size:15.5px;}
.reviewer-head .rfocus{font-size:11.8px; color:var(--slate); font-weight:400; display:block; margin-top:2px;}
.rscore{font-family:var(--mono); font-weight:700; font-size:16px; padding:4px 12px; border-radius:8px; border:1px solid var(--line);}
.rbody{font-size:13.3px; color:#C7CCDA; line-height:1.65;}
.rbody p{margin-bottom:8px;}
.subsec{margin-top:12px;}
.subsec h5{font-size:11px; text-transform:uppercase; letter-spacing:.5px; color:var(--slate); margin-bottom:6px;}
.subsec ul{padding-left:18px;}
.subsec li{font-size:12.8px; color:#C7CCDA; margin-bottom:5px; line-height:1.5;}
.subsec.strengths h5{color:var(--teal);}
.subsec.weaknesses h5{color:var(--coral);}
.subsec.opportunities h5{color:var(--amber);}

/* rewrite lab */
.compare{display:grid; grid-template-columns:1fr 1fr; gap:18px;}
@media (max-width:800px){.compare{grid-template-columns:1fr;}}
.compare-col{border:1px solid var(--line); border-radius:12px; padding:16px 18px;}
.compare-col.before{background:rgba(255,107,107,.04); border-color:rgba(255,107,107,.25);}
.compare-col.after{background:rgba(62,207,142,.04); border-color:rgba(62,207,142,.25);}
.compare-col h5{font-size:11px; text-transform:uppercase; letter-spacing:.6px; margin-bottom:10px;}
.compare-col.before h5{color:var(--coral);}
.compare-col.after h5{color:var(--teal);}
.compare-col .txt{font-size:13.3px; white-space:pre-wrap; line-height:1.65; color:#D7DAE4;}

.hook-list{display:grid; gap:10px; margin-top:10px;}
.hook-item{
  border:1px solid var(--line); border-radius:9px; padding:12px 14px; font-size:13px; display:flex; gap:12px;
  align-items:flex-start; background:rgba(255,255,255,.015);
}
.hook-item .hn{font-family:var(--mono); color:var(--amber); font-weight:700; flex:0 0 auto;}

.checklist{display:grid; gap:8px; margin-top:6px;}
.check-item{display:flex; gap:10px; align-items:flex-start; font-size:13px; padding:10px 12px; border:1px solid var(--line); border-radius:9px;}
.check-item .cb{width:17px; height:17px; border-radius:5px; border:1.5px solid var(--slate-dim); flex:0 0 auto; margin-top:2px; display:flex; align-items:center; justify-content:center; font-size:11px; color:var(--teal);}

/* report */
.report-grid{display:grid; grid-template-columns:1fr 1fr; gap:18px; margin-top:18px;}
@media (max-width:800px){.report-grid{grid-template-columns:1fr;}}
.report-block{border:1px solid var(--line); border-radius:12px; padding:16px 18px; background:rgba(255,255,255,.015);}
.report-block h5{font-size:12px; text-transform:uppercase; letter-spacing:.5px; color:var(--slate); margin-bottom:10px;}
.report-block.wide{grid-column:1 / -1;}
.predict-row{display:flex; align-items:center; justify-content:space-between; padding:9px 0; border-bottom:1px dashed var(--line); font-size:13px;}
.predict-row:last-child{border-bottom:none;}
.predict-tag{font-family:var(--mono); font-weight:700; color:var(--amber);}
.exec-summary{font-size:14px; line-height:1.75; color:#D7DAE4;}

.deep-prompts{display:grid; gap:8px; margin-top:8px;}
.dp-item{
  border:1px solid var(--line); border-radius:8px; padding:10px 12px; font-size:12.6px; font-family:var(--mono);
  color:var(--slate); cursor:pointer; transition:all .15s ease;
}
.dp-item:hover{border-color:var(--amber); color:var(--paper); background:rgba(245,166,35,.05);}

.badge-critical{
  display:inline-block; font-size:10.5px; text-transform:uppercase; letter-spacing:.5px;
  padding:3px 9px; border-radius:999px; margin-left:8px; vertical-align:middle;
}
.badge-critical.gentle{background:rgba(62,207,142,.12); color:var(--teal);}
.badge-critical.balanced{background:rgba(245,166,35,.12); color:var(--amber);}
.badge-critical.brutal{background:rgba(255,107,107,.12); color:var(--coral);}

.skeleton{background:linear-gradient(90deg, var(--line) 25%, #2a3350 37%, var(--line) 63%); background-size:400% 100%; animation:shimmer 1.4s ease infinite; border-radius:6px;}
@keyframes shimmer{0%{background-position:100% 0;} 100%{background-position:0 0;}}

footer.note{margin-top:40px; text-align:center; font-size:11.5px; color:var(--slate-dim);}
</style>
</head>
<body>
<div class="shell">

  <div class="topbar">
    <div class="brand">
      <span class="mark">Ci</span>
      <h1>Content Intelligence Studio</h1>
      <span class="tag">AI Consultant</span>
    </div>
    <div class="mode-pill"><span class="dot"></span> Live via <b>Claude</b> · no data stored</div>
  </div>

  <div class="layout">
    <!-- ============ SIDEBAR ============ -->
    <div class="sidebar">
      <div class="card">
        <h2>1 · Brief</h2>
        <div class="sub">Confirm the context — this shapes which reviewers get assembled.</div>

        <div class="field">
          <label>Content type</label>
          <div class="seg" id="seg-type">
            <button data-v="Social media post/caption" class="active">Post / Caption</button>
            <button data-v="Video (thumbnail + title + transcript)">Video</button>
            <button data-v="Blog/article">Article</button>
          </div>
        </div>

        <div class="field">
          <label>Platform</label>
          <div class="seg" id="seg-platform">
            <button data-v="LinkedIn" class="active">LinkedIn</button>
            <button data-v="YouTube">YouTube</button>
            <button data-v="Instagram">Instagram</button>
          </div>
        </div>

        <div class="field">
          <label>Primary goal</label>
          <div class="seg" id="seg-goal">
            <button data-v="Maximize engagement/virality" class="active">Virality</button>
            <button data-v="Drive conversions/sales">Conversions</button>
            <button data-v="Build authority/thought leadership">Authority</button>
          </div>
        </div>

        <div class="field">
          <label>Review intensity</label>
          <div class="seg" id="seg-crit">
            <button data-v="gentle">Gentle</button>
            <button data-v="balanced" class="active">Balanced</button>
            <button data-v="brutal">Brutal</button>
          </div>
        </div>
      </div>

      <div class="card">
        <h2>2 · Upload</h2>
        <div class="sub">Screenshot of the live post is preferred. Text is optional context.</div>

        <div class="upload-zone" id="dropzone">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M12 16V4M12 4l-4 4M12 4l4 4"/><path d="M4 16v3a1 1 0 001 1h14a1 1 0 001-1v-3"/></svg>
          <p>Drop a screenshot, or click to browse</p>
          <div class="hint">PNG / JPG · post, thumbnail, or analytics capture</div>
        </div>
        <input type="file" id="fileInput" accept="image/*">
        <div id="previewWrap"></div>

        <div class="field" style="margin-top:16px;">
          <label>Post text / caption (optional context)</label>
          <textarea id="textInput" placeholder="Paste the caption text here if you have it — helps Claude read small text in screenshots accurately."></textarea>
        </div>
      </div>

      <div class="card">
        <h2>3 · Run</h2>
        <div class="sub">Claude will design the reviewer pipeline automatically, then run it live.</div>
        <button class="run-btn" id="runBtn">▶ &nbsp;Run Full Analysis</button>
        <button class="run-btn secondary" id="resetBtn" style="display:none;">↺ &nbsp;Start New Analysis</button>
        <div class="err-box" id="errBox">
          <div id="errMsg"></div>
          <button id="retryBtn">Retry</button>
        </div>
      </div>

      <div class="card" id="pipelineCard" style="display:none;">
        <h2>Reviewer Pipeline</h2>
        <div class="sub">Each stage calls Claude live and streams its verdict below.</div>
        <div class="pipeline" id="pipeline"></div>
      </div>

      <div class="card" id="logCard" style="display:none;">
        <h2>Activity Log</h2>
        <div class="log" id="logBox"></div>
      </div>
    </div>

    <!-- ============ MAIN ============ -->
    <div class="main">
      <div class="empty-state" id="emptyState">
        <div class="glyph">Ci</div>
        <h3>No analysis yet</h3>
        <p>Confirm your brief, upload a screenshot of the LinkedIn post (or paste the text), and run the analysis. Claude will assemble a custom panel of reviewers and produce a full diagnostic report — nothing here is scripted.</p>
      </div>

      <div id="results" style="display:none;">
        <div class="tabs" id="tabs">
          <button data-tab="overview" class="active">Overview</button>
          <button data-tab="reviewers">Reviewer Panel</button>
          <button data-tab="rewrite">Rewrite Lab</button>
          <button data-tab="checklist">Publishing Checklist</button>
          <button data-tab="report">Final Report</button>
        </div>

        <div class="tab-panel active" id="tab-overview"></div>
        <div class="tab-panel" id="tab-reviewers"></div>
        <div class="tab-panel" id="tab-rewrite"></div>
        <div class="tab-panel" id="tab-checklist"></div>
        <div class="tab-panel" id="tab-report"></div>
      </div>
    </div>
  </div>

  <footer class="note">Content Intelligence Studio · all scoring, reasoning and rewrites are generated live by Claude and are estimates, not guarantees of performance.</footer>
</div>

<script>
(function(){
  "use strict";

  /* ---------------- state ---------------- */
  const state = {
    contentType: "Social media post/caption",
    platform: "LinkedIn",
    goal: "Maximize engagement/virality",
    criticality: "balanced",
    imageBase64: null,
    imageMediaType: null,
    text: "",
    reviewers: [],      // {name, focus, system}
    reviewerResults: [], // parsed results
    finalReport: null
  };

  /* ---------------- segmented controls ---------------- */
  function wireSeg(id, key){
    const el = document.getElementById(id);
    el.addEventListener("click", e=>{
      const btn = e.target.closest("button");
      if(!btn) return;
      [...el.children].forEach(b=>b.classList.remove("active"));
      btn.classList.add("active");
      state[key] = btn.dataset.v;
    });
  }
  wireSeg("seg-type","contentType");
  wireSeg("seg-platform","platform");
  wireSeg("seg-goal","goal");
  wireSeg("seg-crit","criticality");

  /* ---------------- upload ---------------- */
  const dropzone = document.getElementById("dropzone");
  const fileInput = document.getElementById("fileInput");
  const previewWrap = document.getElementById("previewWrap");

  dropzone.addEventListener("click", ()=>fileInput.click());
  dropzone.addEventListener("dragover", e=>{e.preventDefault(); dropzone.classList.add("drag");});
  dropzone.addEventListener("dragleave", ()=>dropzone.classList.remove("drag"));
  dropzone.addEventListener("drop", e=>{
    e.preventDefault(); dropzone.classList.remove("drag");
    if(e.dataTransfer.files[0]) handleFile(e.dataTransfer.files[0]);
  });
  fileInput.addEventListener("change", e=>{
    if(e.target.files[0]) handleFile(e.target.files[0]);
  });

  function handleFile(file){
    if(!file.type.startsWith("image/")){ alert("Please upload an image file."); return; }
    const reader = new FileReader();
    reader.onload = ()=>{
      const result = reader.result; // data:image/png;base64,....
      const parts = result.split(",");
      state.imageMediaType = parts[0].match(/data:(.*);base64/)[1];
      state.imageBase64 = parts[1];
      previewWrap.innerHTML = `<div class="preview-wrap"><img src="${result}" alt="Uploaded preview"><button class="preview-remove" id="removeImg" title="Remove image">✕</button></div>`;
      document.getElementById("removeImg").addEventListener("click", (ev)=>{
        ev.stopPropagation();
        state.imageBase64 = null; state.imageMediaType = null;
        previewWrap.innerHTML = ""; fileInput.value = "";
      });
    };
    reader.readAsDataURL(file);
  }

  /* ---------------- logging ---------------- */
  const logCard = document.getElementById("logCard");
  const logBox = document.getElementById("logBox");
  function log(msg, cls){
    logCard.style.display = "block";
    const time = new Date().toLocaleTimeString([], {hour12:false});
    const div = document.createElement("div");
    div.className = "line " + (cls||"");
    div.innerHTML = `<span class="t">${time}</span><span>${msg}</span>`;
    logBox.appendChild(div);
    logBox.scrollTop = logBox.scrollHeight;
  }

  /* ---------------- error box ---------------- */
  const errBox = document.getElementById("errBox");
  const errMsg = document.getElementById("errMsg");
  const retryBtn = document.getElementById("retryBtn");
  let lastFailedStep = null;
  function showError(message, retryFn){
    errBox.classList.add("show");
    errMsg.textContent = message;
    lastFailedStep = retryFn;
  }
  function hideError(){ errBox.classList.remove("show"); }
  retryBtn.addEventListener("click", ()=>{
    hideError();
    if(lastFailedStep) lastFailedStep();
  });

  /* ---------------- Claude API wrapper ---------------- */
  async function callClaude(systemPrompt, userContent, opts){
    opts = opts || {};
    const maxRetries = opts.maxRetries === undefined ? 2 : opts.maxRetries;
    let attempt = 0, lastErr = null;
    while(attempt <= maxRetries){
      try{
        const res = await fetch("https://api.anthropic.com/v1/messages", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            model: "claude-sonnet-4-6",
            max_tokens: opts.maxTokens || 1800,
            system: systemPrompt,
            messages: [{ role: "user", content: userContent }]
          })
        });
        if(!res.ok){
          const t = await res.text().catch(()=> "");
          throw new Error(`API error ${res.status}: ${t.slice(0,200)}`);
        }
        const data = await res.json();
        const textBlocks = (data.content||[]).filter(b=>b.type==="text").map(b=>b.text);
        const text = textBlocks.join("\n").trim();
        if(!text) throw new Error("Empty response from model.");
        return text;
      }catch(err){
        lastErr = err;
        attempt++;
        if(attempt <= maxRetries){
          log(`Retrying after error: ${err.message}`, "warn");
          await new Promise(r=>setTimeout(r, 700*attempt));
        }
      }
    }
    throw lastErr;
  }

  function buildUserContent(promptText){
    const content = [];
    if(state.imageBase64){
      content.push({ type:"image", source:{ type:"base64", media_type: state.imageMediaType, data: state.imageBase64 } });
    }
    content.push({ type:"text", text: promptText });
    return content;
  }

  /* ---------------- plain-text parsing helpers ----------------
     Every prompt asks Claude to answer using UPPERCASE_LABEL: markers,
     one per line, with "- " bullet items for list sections. No JSON anywhere. */

  function parseSections(raw){
    const lines = raw.split("\n");
    const sections = {};
    let current = null;
    for(let line of lines){
      const m = line.match(/^\s{0,3}([A-Z][A-Z0-9_ ]{1,40}):\s*(.*)$/);
      if(m && m[1].trim().split(" ").length <= 4){
        current = m[1].trim().replace(/\s+/g,"_");
        sections[current] = sections[current] || [];
        if(m[2].trim()) sections[current].push(m[2].trim());
      } else if(current){
        if(line.trim() !== "") sections[current].push(line.trim());
      }
    }
    const out = {};
    for(const k in sections){
      out[k] = sections[k].join("\n").trim();
    }
    return out;
  }

  function bulletList(str){
    if(!str) return [];
    return str.split("\n").map(l=>l.replace(/^[-•*]\s*/,"").trim()).filter(Boolean);
  }

  function extractScore(str){
    if(!str) return null;
    const m = str.match(/(\d{1,3})/);
    if(!m) return null;
    let n = parseInt(m[1],10);
    return Math.max(0, Math.min(100, n));
  }

  /* ---------------- pipeline UI ---------------- */
  const pipelineCard = document.getElementById("pipelineCard");
  const pipelineEl = document.getElementById("pipeline");

  function renderPipeline(reviewers){
    pipelineCard.style.display = "block";
    pipelineEl.innerHTML = "";
    reviewers.forEach((r, i)=>{
      const div = document.createElement("div");
      div.className = "pnode";
      div.id = "pnode-"+i;
      div.innerHTML = `
        <div class="pdot">${i+1}</div>
        <div class="pinfo">
          <div class="pname">${escapeHtml(r.name)}</div>
          <div class="pfocus">${escapeHtml(r.focus)}</div>
          <div class="pstatus">Queued</div>
        </div>`;
      pipelineEl.appendChild(div);
    });
  }
  function setNodeState(i, cls, statusText){
    const node = document.getElementById("pnode-"+i);
    if(!node) return;
    node.classList.remove("active","done","error");
    node.classList.add(cls);
    node.querySelector(".pstatus").textContent = statusText;
    node.querySelector(".pdot").textContent = cls==="done" ? "✓" : cls==="error" ? "!" : (i+1);
  }

  function escapeHtml(s){
    return String(s||"").replace(/[&<>"']/g, c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]));
  }

  /* ---------------- Run button ---------------- */
  const runBtn = document.getElementById("runBtn");
  const resetBtn = document.getElementById("resetBtn");
  const emptyState = document.getElementById("emptyState");
  const results = document.getElementById("results");

  runBtn.addEventListener("click", runAnalysis);
  resetBtn.addEventListener("click", ()=>{
    location.reload();
  });

  async function runAnalysis(){
    if(!state.imageBase64 && !document.getElementById("textInput").value.trim()){
      showError("Upload a screenshot or paste the post text before running the analysis.", runAnalysis);
      return;
    }
    hideError();
    state.text = document.getElementById("textInput").value.trim();
    runBtn.disabled = true;
    runBtn.textContent = "Running…";
    logBox.innerHTML = "";
    log("Analysis started for " + state.platform + " · " + state.contentType, "ok");

    try{
      await planPipeline();
      await runReviewers();
      await synthesizeReport();
      renderResults();
      results.style.display = "block";
      emptyState.style.display = "none";
      resetBtn.style.display = "block";
      log("Analysis complete.", "ok");
    }catch(err){
      log("Fatal error: " + err.message, "err");
      showError("Something went wrong: " + err.message, runAnalysis);
    }finally{
      runBtn.disabled = false;
      runBtn.textContent = "▶  Run Full Analysis";
    }
  }

  /* ---------------- Stage 1: Planner ---------------- */
  async function planPipeline(){
    log("Designing reviewer pipeline…");
    const plannerSystem = `You are the Chief Strategist at a top-tier content consultancy. Given a brief about a piece of content (type, platform, goal), design a custom panel of 4 specialist AI reviewers best suited to critique this exact content. Choose reviewer roles and focus areas specifically appropriate to the platform and goal described — do not default to generic roles if better ones fit.

Respond in PLAIN TEXT ONLY using exactly this repeating format, one reviewer per block, nothing else before or after:

REVIEWER: <short role name, 2-4 words>
FOCUS: <one sentence on what this reviewer evaluates>
SYSTEM: <a full production-quality system prompt, 3-5 sentences, instructing this specialist how to evaluate the content, what lens to use, and how strict to be given a "${state.criticality}" review intensity>

Repeat this block exactly 4 times for 4 distinct reviewers. Do not use JSON, markdown headers, numbering, or code fences.`;

    const briefText = `Content type: ${state.contentType}
Platform: ${state.platform}
Primary goal: ${state.goal}
Review intensity requested: ${state.criticality}
${state.text ? "Post text provided: " + state.text : "Post text not provided — an image/screenshot will be supplied to reviewers."}

Design the 4-reviewer panel now.`;

    const raw = await callClaude(plannerSystem, [{type:"text", text: briefText}], {maxTokens:1200});
    const blocks = raw.split(/\n(?=REVIEWER:)/).map(b=>b.trim()).filter(Boolean);
    const reviewers = [];
    for(const b of blocks){
      const name = (b.match(/REVIEWER:\s*(.*)/)||[])[1];
      const focus = (b.match(/FOCUS:\s*(.*)/)||[])[1];
      const sysMatch = b.match(/SYSTEM:\s*([\s\S]*)/);
      const system = sysMatch ? sysMatch[1].trim() : "";
      if(name && system){
        reviewers.push({ name: name.trim(), focus: (focus||"").trim(), system });
      }
    }
    if(reviewers.length === 0){
      throw new Error("Could not parse a reviewer pipeline from the planning stage.");
    }
    state.reviewers = reviewers.slice(0,5);
    renderPipeline(state.reviewers);
    log(`Pipeline assembled: ${state.reviewers.map(r=>r.name).join(", ")}`, "ok");
  }

  /* ---------------- Stage 2: Reviewers ---------------- */
  async function runReviewers(){
    state.reviewerResults = [];
    for(let i=0;i<state.reviewers.length;i++){
      const r = state.reviewers[i];
      setNodeState(i, "active", "Reviewing…");
      log(`Running reviewer: ${r.name}…`);

      const critLine = {
        gentle: "Be encouraging and constructive; lead with what works, and frame issues gently.",
        balanced: "Be honest and even-handed; give credit where due but do not soften real weaknesses.",
        brutal: "Be rigorous and unsparing, as if this must survive scrutiny from a top agency's creative director. Do not pad praise."
      }[state.criticality];

      const system = `${r.system}\n\n${critLine}\n\nYou MUST respond in PLAIN TEXT using exactly these markers, each on its own line, no JSON, no markdown headers, no code fences:

SCORE: <a single integer 0-100 for this dimension>
REASONING: <2-4 sentences of your expert reasoning, referencing specifics from the actual content you were shown>
STRENGTHS:
- <specific strength>
- <specific strength>
WEAKNESSES:
- <specific weakness>
- <specific weakness>
OPPORTUNITIES:
- <a missed opportunity specific to ${state.platform}>
- <a missed opportunity specific to ${state.platform}>
RECOMMENDATION:
- <one concrete, actionable recommendation>
- <one concrete, actionable recommendation>`;

      const userPrompt = `Here is the content to review (platform: ${state.platform}, goal: ${state.goal}).${state.text ? "\n\nCaption/text:\n" + state.text : ""}${state.imageBase64 ? "\n\nA screenshot/image of the content is attached — analyze the actual visual content directly, including any text visible in the image, layout, and visual design." : ""}

Evaluate strictly from your specialist lens now.`;

      try{
        const raw = await callClaude(system, buildUserContent(userPrompt), {maxTokens:900});
        const sec = parseSections(raw);
        const result = {
          name: r.name,
          focus: r.focus,
          score: extractScore(sec.SCORE) ?? 70,
          reasoning: sec.REASONING || "",
          strengths: bulletList(sec.STRENGTHS),
          weaknesses: bulletList(sec.WEAKNESSES),
          opportunities: bulletList(sec.OPPORTUNITIES),
          recommendations: bulletList(sec.RECOMMENDATION)
        };
        state.reviewerResults.push(result);
        setNodeState(i, "done", `Scored ${result.score}/100`);
        log(`${r.name} complete — score ${result.score}/100`, "ok");
      }catch(err){
        setNodeState(i, "error", "Failed");
        log(`${r.name} failed: ${err.message}`, "err");
        state.reviewerResults.push({
          name: r.name, focus: r.focus, score: null,
          reasoning: "This reviewer could not complete its analysis due to an API error: " + err.message,
          strengths: [], weaknesses: [], opportunities: [], recommendations: []
        });
      }
    }
  }

  /* ---------------- Stage 3: Synthesis / final report ---------------- */
  async function synthesizeReport(){
    log("Synthesizing final report…");
    const synthSystem = `You are the Editor-in-Chief of a premium content consultancy, producing the final client-facing report by synthesizing several specialist reviews into one cohesive diagnostic. Be specific to the actual content shown — never generic. Match a "${state.criticality}" tone as instructed to the specialists.

Respond in PLAIN TEXT ONLY using exactly these markers, each starting a new line, no JSON, no markdown headers, no code fences:

OVERALL_SCORE: <single integer 0-100, a holistic synthesis of the panel's scores>
EXEC_SUMMARY: <4-6 sentences, executive summary of overall content health and verdict>
HEALTH_REPORT: <3-4 sentences describing the content's current state like a diagnostic report>
TOP_IMPROVEMENTS:
- <highest impact improvement, most important first>
- <second highest impact improvement>
- <third highest impact improvement>
PREDICTED_REACH: <one short phrase estimate, e.g. "Below average for account size">
PREDICTED_ENGAGEMENT: <one short phrase estimate, e.g. "Moderate — hook underperforms">
PREDICTED_SHAREABILITY: <one short phrase estimate>
BEFORE_TEXT: <the original post text as given or transcribed from the image, verbatim as best as can be read>
AFTER_TEXT: <a fully rewritten, publish-ready version of the post optimized for ${state.platform} and the stated goal>
HOOK_1: <alternative opening hook/first line>
HOOK_2: <alternative opening hook/first line>
HOOK_3: <alternative opening hook/first line>
CHECKLIST:
- <a publishing readiness checklist item>
- <a publishing readiness checklist item>
- <a publishing readiness checklist item>
- <a publishing readiness checklist item>
DEEPER_PROMPT_1: <a follow-up prompt the user could ask an AI to go deeper on one specific weakness>
DEEPER_PROMPT_2: <a follow-up prompt the user could ask an AI to go deeper on another angle>
DEEPER_PROMPT_3: <a follow-up prompt the user could ask an AI to go deeper on another angle>`;

    const panelSummary = state.reviewerResults.map(r=>
      `Reviewer: ${r.name} (${r.focus})\nScore: ${r.score}\nReasoning: ${r.reasoning}\nStrengths: ${r.strengths.join("; ")}\nWeaknesses: ${r.weaknesses.join("; ")}\nOpportunities: ${r.opportunities.join("; ")}\nRecommendations: ${r.recommendations.join("; ")}`
    ).join("\n\n");

    const userPrompt = `Platform: ${state.platform}\nContent type: ${state.contentType}\nGoal: ${state.goal}\n${state.text ? "Caption/text:\n"+state.text : ""}\n\nHere is the full specialist panel's findings:\n\n${panelSummary}\n\n${state.imageBase64 ? "The original screenshot is attached again for your reference — use it to transcribe accurate BEFORE_TEXT and to inform the rewrite." : ""}\n\nProduce the final synthesized report now.`;

    const raw = await callClaude(synthSystem, buildUserContent(userPrompt), {maxTokens:2200});
    const sec = parseSections(raw);
    state.finalReport = {
      overallScore: extractScore(sec.OVERALL_SCORE) ?? Math.round(state.reviewerResults.reduce((a,r)=>a+(r.score||0),0)/Math.max(1,state.reviewerResults.length)),
      execSummary: sec.EXEC_SUMMARY || "",
      healthReport: sec.HEALTH_REPORT || "",
      topImprovements: bulletList(sec.TOP_IMPROVEMENTS),
      predictedReach: sec.PREDICTED_REACH || "—",
      predictedEngagement: sec.PREDICTED_ENGAGEMENT || "—",
      predictedShareability: sec.PREDICTED_SHAREABILITY || "—",
      beforeText: sec.BEFORE_TEXT || state.text || "(no text captured)",
      afterText: sec.AFTER_TEXT || "",
      hooks: [sec.HOOK_1, sec.HOOK_2, sec.HOOK_3].filter(Boolean),
      checklist: bulletList(sec.CHECKLIST),
      deeperPrompts: [sec.DEEPER_PROMPT_1, sec.DEEPER_PROMPT_2, sec.DEEPER_PROMPT_3].filter(Boolean)
    };
    log("Final report synthesized.", "ok");
  }

  /* ---------------- Rendering ---------------- */
  function renderResults(){
    renderOverview();
    renderReviewers();
    renderRewrite();
    renderChecklist();
    renderReport();
  }

  function gaugeSvg(score){
    const r = 80, c = 2*Math.PI*r;
    const pct = Math.max(0,Math.min(100,score))/100;
    const offset = c*(1-pct);
    const color = score>=75 ? "var(--teal)" : score>=50 ? "var(--amber)" : "var(--coral)";
    return `<svg viewBox="0 0 200 200" width="200" height="200">
      <circle cx="100" cy="100" r="${r}" fill="none" stroke="var(--line)" stroke-width="14"/>
      <circle cx="100" cy="100" r="${r}" fill="none" stroke="${color}" stroke-width="14" stroke-linecap="round"
        stroke-dasharray="${c}" stroke-dashoffset="${offset}" transform="rotate(-90 100 100)"
        style="transition: stroke-dashoffset 1.2s cubic-bezier(.2,.8,.2,1);"/>
    </svg>`;
  }

  function renderOverview(){
    const fr = state.finalReport;
    const critBadge = {gentle:"gentle", balanced:"balanced", brutal:"brutal"}[state.criticality];
    const critLabel = {gentle:"Gentle Review", balanced:"Balanced Review", brutal:"Brutal Review"}[state.criticality];

    let html = `
      <div class="score-hero">
        <div class="gauge-wrap">
          ${gaugeSvg(fr.overallScore)}
          <div class="gauge-num"><div class="n">${fr.overallScore}</div><div class="l">/ 100</div></div>
        </div>
        <div class="score-meta">
          <h3>Content Health <span class="badge-critical ${critBadge}">${critLabel}</span></h3>
          <p>${escapeHtml(fr.healthReport)}</p>
          <div class="chips">
            <span class="chip">${escapeHtml(state.platform)}</span>
            <span class="chip">${escapeHtml(state.goal)}</span>
            ${fr.overallScore>=70 ? '<span class="chip pos">Ready with polish</span>' : '<span class="chip risk">Needs revision</span>'}
          </div>
        </div>
      </div>

      <div class="card">
        <h2>Executive Summary</h2>
        <div class="exec-summary">${escapeHtml(fr.execSummary)}</div>
      </div>

      <div class="card">
        <h2>Category Breakdown</h2>
        <div class="sub">Score from each specialist reviewer in the panel.</div>
        <div class="cat-grid">
          ${state.reviewerResults.map(r=>`
            <div class="cat-row">
              <div class="cname">${escapeHtml(r.name)}<span>${escapeHtml(r.focus)}</span></div>
              <div class="bar-track"><div class="bar-fill" data-w="${r.score||0}"></div></div>
              <div class="cscore">${r.score!==null? r.score : "—"}</div>
            </div>`).join("")}
        </div>
      </div>

      <div class="card">
        <h2>Highest-Impact Improvements</h2>
        <div class="subsec"><ul>${fr.topImprovements.map(t=>`<li>${escapeHtml(t)}</li>`).join("")}</ul></div>
      </div>
    `;
    document.getElementById("tab-overview").innerHTML = html;
    requestAnimationFrame(()=>{
      document.querySelectorAll("#tab-overview .bar-fill").forEach(el=>{
        el.style.width = el.dataset.w + "%";
      });
    });
  }

  function renderReviewers(){
    let html = state.reviewerResults.map(r=>`
      <div class="reviewer-card">
        <div class="reviewer-head">
          <h4>${escapeHtml(r.name)}<span class="rfocus">${escapeHtml(r.focus)}</span></h4>
          <div class="rscore" style="color:${scoreColor(r.score)}; border-color:${scoreColor(r.score)}44;">${r.score!==null? r.score+"/100" : "N/A"}</div>
        </div>
        <div class="rbody"><p>${escapeHtml(r.reasoning)}</p></div>
        <div class="subsec strengths"><h5>Strengths</h5><ul>${r.strengths.map(s=>`<li>${escapeHtml(s)}</li>`).join("") || "<li>—</li>"}</ul></div>
        <div class="subsec weaknesses"><h5>Weaknesses</h5><ul>${r.weaknesses.map(s=>`<li>${escapeHtml(s)}</li>`).join("") || "<li>—</li>"}</ul></div>
        <div class="subsec opportunities"><h5>Missed Opportunities</h5><ul>${r.opportunities.map(s=>`<li>${escapeHtml(s)}</li>`).join("") || "<li>—</li>"}</ul></div>
        <div class="subsec"><h5>Recommendations</h5><ul>${r.recommendations.map(s=>`<li>${escapeHtml(s)}</li>`).join("") || "<li>—</li>"}</ul></div>
      </div>
    `).join("");
    document.getElementById("tab-reviewers").innerHTML = html;
  }

  function scoreColor(s){
    if(s===null) return "var(--slate)";
    if(s>=75) return "var(--teal)";
    if(s>=50) return "var(--amber)";
    return "var(--coral)";
  }

  function renderRewrite(){
    const fr = state.finalReport;
    let html = `
      <div class="card">
        <h2>Before vs. After</h2>
        <div class="sub">Original vs. Claude's rewritten, publish-ready version.</div>
        <div class="compare">
          <div class="compare-col before"><h5>Before</h5><div class="txt">${escapeHtml(fr.beforeText)}</div></div>
          <div class="compare-col after"><h5>After</h5><div class="txt">${escapeHtml(fr.afterText)}</div></div>
        </div>
      </div>
      <div class="card">
        <h2>Alternative Hooks</h2>
        <div class="sub">Swap-in openers to test against the current one.</div>
        <div class="hook-list">
          ${fr.hooks.map((h,i)=>`<div class="hook-item"><span class="hn">H${i+1}</span><span>${escapeHtml(h)}</span></div>`).join("")}
        </div>
      </div>
    `;
    document.getElementById("tab-rewrite").innerHTML = html;
  }

  function renderChecklist(){
    const fr = state.finalReport;
    let html = `
      <div class="card">
        <h2>Publishing Checklist</h2>
        <div class="sub">Confirm each item before this goes live on ${escapeHtml(state.platform)}.</div>
        <div class="checklist">
          ${fr.checklist.map(c=>`<div class="check-item"><span class="cb">✓</span><span>${escapeHtml(c)}</span></div>`).join("")}
        </div>
      </div>
    `;
    document.getElementById("tab-checklist").innerHTML = html;
  }

  function renderReport(){
    const fr = state.finalReport;
    let html = `
      <div class="card">
        <h2>Final Report</h2>
        <div class="sub">Full diagnostic summary, ready to share.</div>
        <div class="report-grid">
          <div class="report-block wide">
            <h5>Executive Summary</h5>
            <div class="exec-summary">${escapeHtml(fr.execSummary)}</div>
          </div>
          <div class="report-block">
            <h5>Predicted Performance <span style="font-weight:400; color:var(--slate-dim); text-transform:none; letter-spacing:0;">(AI estimate)</span></h5>
            <div class="predict-row"><span>Reach</span><span class="predict-tag">${escapeHtml(fr.predictedReach)}</span></div>
            <div class="predict-row"><span>Engagement</span><span class="predict-tag">${escapeHtml(fr.predictedEngagement)}</span></div>
            <div class="predict-row"><span>Shareability</span><span class="predict-tag">${escapeHtml(fr.predictedShareability)}</span></div>
          </div>
          <div class="report-block">
            <h5>Top Improvements</h5>
            <ul style="padding-left:16px;">${fr.topImprovements.map(t=>`<li style="margin-bottom:6px; font-size:13px;">${escapeHtml(t)}</li>`).join("")}</ul>
          </div>
          <div class="report-block wide">
            <h5>Go Deeper</h5>
            <div class="sub" style="margin-bottom:8px;">Copy one of these into a new chat with Claude for a focused follow-up.</div>
            <div class="deep-prompts">
              ${fr.deeperPrompts.map(p=>`<div class="dp-item" title="Click to copy">${escapeHtml(p)}</div>`).join("")}
            </div>
          </div>
        </div>
      </div>
    `;
    document.getElementById("tab-report").innerHTML = html;
    document.querySelectorAll(".dp-item").forEach(el=>{
      el.addEventListener("click", ()=>{
        navigator.clipboard.writeText(el.textContent).then(()=>{
          const orig = el.textContent;
          el.textContent = "Copied ✓";
          setTimeout(()=>{ el.textContent = orig; }, 1200);
        }).catch(()=>{});
      });
    });
  }

  /* ---------------- Tabs ---------------- */
  document.getElementById("tabs").addEventListener("click", e=>{
    const btn = e.target.closest("button");
    if(!btn) return;
    document.querySelectorAll("#tabs button").forEach(b=>b.classList.remove("active"));
    btn.classList.add("active");
    document.querySelectorAll(".tab-panel").forEach(p=>p.classList.remove("active"));
    document.getElementById("tab-"+btn.dataset.tab).classList.add("active");
  });

})();
</script>
</body>
</html>
