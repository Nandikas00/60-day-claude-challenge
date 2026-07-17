# Today I built Autonomous Agent Studio using claude:

## Key Learnings :
- Learned how autonomous AI agents can plan, reason, and execute tasks independently with minimal human intervention.
- Gained practical experience in designing multi-agent workflows where specialized AI agents collaborate to solve complex problems.
- Explored prompt engineering techniques to define agent roles, objectives, constraints, and decision-making behavior.
- Understood the importance of memory management, tool integration, and context retention in building intelligent autonomous systems.
- Learned how task planning, workflow orchestration, and agent collaboration improve efficiency and scalability.
- Practiced creating AI-powered interfaces for configuring, monitoring, and managing autonomous agents through an interactive dashboard.
- Improved frontend development skills by building responsive visualizations for agent status, workflow execution, and performance tracking.
- Strengthened understanding of how AI agents can automate repetitive processes while maintaining transparency and user control.

### Output Screenshots :

<img width="1319" height="904" alt="Screenshot (673)" src="https://github.com/user-attachments/assets/6c9b7bfd-2749-462b-8587-ae3055b628b2" />
<img width="1920" height="884" alt="Screenshot (672)" src="https://github.com/user-attachments/assets/4187aab0-e1e9-4bc0-883a-13a96092586e" />


#### HTML File :
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Autonomous Agent Studio — Bug-Fix Pipeline</title>
<style>
:root{
  --bg:#0B1220;
  --bg-panel:#101A2E;
  --bg-panel-2:#0D1626;
  --line:#1E2C48;
  --line-soft:#182238;
  --ink:#DCE6F5;
  --ink-dim:#8496B8;
  --ink-faint:#546382;
  --amber:#E8A23D;
  --amber-dim:#8A6428;
  --teal:#3DDC97;
  --teal-dim:#215E43;
  --red:#E8543D;
  --red-dim:#7A2E22;
  --mono: ui-monospace, "SFMono-Regular", "IBM Plex Mono", Menlo, Consolas, monospace;
  --sans: -apple-system, "Segoe UI", "Inter", system-ui, sans-serif;
}
*{box-sizing:border-box; margin:0; padding:0;}
html,body{background:var(--bg); color:var(--ink); font-family:var(--sans); min-height:100vh;}
body{
  background-image:
    radial-gradient(circle at 15% 0%, rgba(232,162,61,0.06), transparent 40%),
    radial-gradient(circle at 85% 100%, rgba(61,220,151,0.05), transparent 40%);
}
::selection{background:var(--amber-dim); color:#fff;}
::-webkit-scrollbar{width:10px; height:10px;}
::-webkit-scrollbar-track{background:var(--bg-panel-2);}
::-webkit-scrollbar-thumb{background:var(--line); border-radius:4px;}

.wrap{max-width:1400px; margin:0 auto; padding:28px 24px 80px;}

/* ---------- Header ---------- */
.hdr{display:flex; justify-content:space-between; align-items:flex-end; gap:24px; flex-wrap:wrap; margin-bottom:28px; border-bottom:1px solid var(--line); padding-bottom:22px;}
.hdr .eyebrow{font-family:var(--mono); font-size:11px; letter-spacing:.18em; text-transform:uppercase; color:var(--amber); margin-bottom:8px;}
.hdr h1{font-size:30px; font-weight:700; letter-spacing:-0.02em; color:#fff;}
.hdr p{color:var(--ink-dim); font-size:14px; margin-top:6px; max-width:560px; line-height:1.5;}
.hdr-right{display:flex; gap:10px; align-items:center;}
.pill{font-family:var(--mono); font-size:11px; padding:6px 10px; border:1px solid var(--line); border-radius:20px; color:var(--ink-dim); display:flex; align-items:center; gap:6px;}
.dot{width:6px; height:6px; border-radius:50%; background:var(--ink-faint);}
.dot.live{background:var(--teal); box-shadow:0 0 6px var(--teal);}
.dot.err{background:var(--red); box-shadow:0 0 6px var(--red);}

/* ---------- Setup card ---------- */
.card{background:var(--bg-panel); border:1px solid var(--line); border-radius:10px; padding:22px;}
.section-title{font-family:var(--mono); font-size:11px; letter-spacing:.14em; text-transform:uppercase; color:var(--ink-faint); margin-bottom:14px; display:flex; align-items:center; gap:8px;}
.section-title::before{content:''; width:14px; height:1px; background:var(--amber-dim);}

label{display:block; font-size:12px; color:var(--ink-dim); margin-bottom:6px; font-family:var(--mono);}
textarea, input[type=text]{
  width:100%; background:var(--bg-panel-2); border:1px solid var(--line); color:var(--ink);
  border-radius:7px; padding:12px; font-family:var(--mono); font-size:13px; line-height:1.55;
  resize:vertical; transition:border-color .15s;
}
textarea:focus, input:focus{outline:none; border-color:var(--amber-dim);}
.grid2{display:grid; grid-template-columns:1fr 1fr; gap:16px;}
@media(max-width:820px){.grid2{grid-template-columns:1fr;}}
.field{margin-bottom:16px;}
.row-inline{display:flex; gap:14px; flex-wrap:wrap; align-items:flex-end;}
.small-field{min-width:170px;}
select{background:var(--bg-panel-2); border:1px solid var(--line); color:var(--ink); padding:10px 12px; border-radius:7px; font-family:var(--mono); font-size:13px; width:100%;}

.btn{
  font-family:var(--mono); font-size:13px; font-weight:600; letter-spacing:.02em;
  padding:12px 22px; border-radius:7px; border:1px solid transparent; cursor:pointer;
  transition:transform .1s, box-shadow .15s, opacity .15s;
}
.btn:active{transform:scale(0.98);}
.btn-primary{background:var(--amber); color:#1a1200; box-shadow:0 0 0 rgba(232,162,61,0);}
.btn-primary:hover{box-shadow:0 4px 18px rgba(232,162,61,0.25);}
.btn-primary:disabled{opacity:.4; cursor:not-allowed; box-shadow:none;}
.btn-ghost{background:transparent; border:1px solid var(--line); color:var(--ink-dim);}
.btn-ghost:hover{border-color:var(--ink-faint); color:var(--ink);}

/* ---------- Layout after run starts ---------- */
.studio{display:none; margin-top:28px; gap:20px; grid-template-columns:340px 1fr; align-items:start;}
.studio.active{display:grid;}
@media(max-width:1050px){.studio.active{grid-template-columns:1fr;}}

/* -- Loop diagram -- */
.loop-card{position:sticky; top:20px;}
.loop-svg-wrap{width:100%; aspect-ratio:1/1; position:relative;}
svg text{font-family:var(--mono);}
.node-label{fill:var(--ink); font-size:10.5px; font-weight:600;}
.node-sub{fill:var(--ink-faint); font-size:8px;}
.node-circle{fill:var(--bg-panel-2); stroke:var(--line); stroke-width:1.5; transition:stroke .25s, fill .25s;}
.node-circle.active{stroke:var(--amber); fill:#1B1408; filter:drop-shadow(0 0 8px rgba(232,162,61,.5));}
.node-circle.done{stroke:var(--teal-dim);}
.loop-path{fill:none; stroke:var(--line); stroke-width:1.5;}
.pulse{fill:var(--amber); filter:drop-shadow(0 0 5px var(--amber));}
.branch-path{fill:none; stroke:var(--line-soft); stroke-width:1.5; stroke-dasharray:3 4;}

.agent-legend{margin-top:16px; display:flex; flex-direction:column; gap:8px;}
.agent-item{display:flex; gap:10px; align-items:flex-start; padding:8px; border-radius:6px; transition:background .15s;}
.agent-item.active{background:rgba(232,162,61,.08);}
.agent-swatch{width:8px; height:8px; border-radius:50%; margin-top:5px; flex-shrink:0;}
.agent-item h4{font-size:12px; color:var(--ink); margin-bottom:2px;}
.agent-item p{font-size:11px; color:var(--ink-faint); line-height:1.4;}

/* -- Right column -- */
.main-col{display:flex; flex-direction:column; gap:20px;}

.status-bar{display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:12px;}
.status-left{display:flex; align-items:center; gap:12px;}
.spinner{width:14px; height:14px; border-radius:50%; border:2px solid var(--line); border-top-color:var(--amber); animation:spin 0.8s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.round-badge{font-family:var(--mono); font-size:13px; color:#fff; font-weight:600;}
.status-msg{font-family:var(--mono); font-size:12px; color:var(--ink-dim);}
.stat-chip{font-family:var(--mono); font-size:11px; color:var(--ink-dim); border:1px solid var(--line); padding:5px 10px; border-radius:6px;}
.stat-chip b{color:var(--teal);}

.tabs{display:flex; gap:4px; border-bottom:1px solid var(--line); margin-bottom:0;}
.tab{font-family:var(--mono); font-size:12px; padding:10px 14px; color:var(--ink-faint); cursor:pointer; border-bottom:2px solid transparent; transition:color .15s;}
.tab.active{color:var(--amber); border-color:var(--amber);}
.tab:hover{color:var(--ink);}
.tab-panel{display:none; padding-top:16px;}
.tab-panel.active{display:block;}

.log-line{font-family:var(--mono); font-size:12px; padding:6px 0; border-bottom:1px solid var(--line-soft); display:flex; gap:10px; color:var(--ink-dim); animation:fadeIn .3s ease;}
@keyframes fadeIn{from{opacity:0; transform:translateY(-3px);} to{opacity:1; transform:translateY(0);}}
.log-line .tag{color:var(--amber); flex-shrink:0; width:90px;}
.log-line.err .tag{color:var(--red);}
.log-line.ok .tag{color:var(--teal);}
.log-box{max-height:340px; overflow-y:auto; background:var(--bg-panel-2); border:1px solid var(--line); border-radius:8px; padding:12px;}

pre.codeblock{background:var(--bg-panel-2); border:1px solid var(--line); border-radius:8px; padding:14px; font-family:var(--mono); font-size:12.3px; line-height:1.6; overflow-x:auto; white-space:pre-wrap; word-break:break-word; color:var(--ink);}
.round-card{border:1px solid var(--line); border-radius:8px; padding:16px; margin-bottom:14px; background:var(--bg-panel-2);}
.round-hdr{display:flex; justify-content:space-between; align-items:center; margin-bottom:10px; flex-wrap:wrap; gap:8px;}
.round-hdr h3{font-size:13px; font-family:var(--mono); color:#fff;}
.score-tag{font-family:var(--mono); font-size:13px; font-weight:700; padding:3px 10px; border-radius:20px;}
.score-tag.good{color:var(--teal); background:rgba(61,220,151,.1); border:1px solid var(--teal-dim);}
.score-tag.mid{color:var(--amber); background:rgba(232,162,61,.1); border:1px solid var(--amber-dim);}
.score-tag.low{color:var(--red); background:rgba(232,84,61,.1); border:1px solid var(--red-dim);}
.delta{font-family:var(--mono); font-size:11px; color:var(--ink-faint);}
.delta.pos{color:var(--teal);}
.crit-block{font-size:12.5px; color:var(--ink-dim); line-height:1.6; white-space:pre-wrap; margin-top:6px;}
.subhead{font-family:var(--mono); font-size:10.5px; text-transform:uppercase; letter-spacing:.1em; color:var(--ink-faint); margin:12px 0 4px;}

.mem-item{font-family:var(--mono); font-size:11.5px; color:var(--ink-dim); padding:8px 10px; border-left:2px solid var(--amber-dim); background:var(--bg-panel-2); margin-bottom:6px; border-radius:0 6px 6px 0;}

.final-banner{border:1px solid var(--teal-dim); background:rgba(61,220,151,.06); border-radius:10px; padding:20px; display:none;}
.final-banner.show{display:block;}
.final-banner h3{color:var(--teal); font-family:var(--mono); font-size:14px; margin-bottom:8px;}
.final-banner p{color:var(--ink-dim); font-size:13px; line-height:1.6;}

.chart-wrap{background:var(--bg-panel-2); border:1px solid var(--line); border-radius:8px; padding:16px;}

.hidden{display:none !important;}

/* bottom sections */
.bottom-sections{margin-top:60px; display:flex; flex-direction:column; gap:36px;}
.bottom-sections h2{font-size:20px; color:#fff; margin-bottom:14px; display:flex; align-items:center; gap:10px;}
.bottom-sections h2::before{content:''; width:20px; height:2px; background:var(--amber);}
.arch-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(230px,1fr)); gap:14px;}
.arch-item{border:1px solid var(--line); background:var(--bg-panel); border-radius:8px; padding:16px;}
.arch-item h4{font-family:var(--mono); font-size:12px; color:var(--amber); margin-bottom:6px;}
.arch-item p{font-size:12.5px; color:var(--ink-dim); line-height:1.6;}
.ext-list{display:grid; grid-template-columns:repeat(auto-fit,minmax(260px,1fr)); gap:12px;}
.ext-item{border:1px dashed var(--line); border-radius:8px; padding:14px; font-size:12.5px; color:var(--ink-dim); line-height:1.55;}
.ext-item b{color:var(--ink); display:block; margin-bottom:4px; font-size:13px;}
.prompt-list{display:flex; flex-direction:column; gap:10px;}
.prompt-item{font-family:var(--mono); font-size:12.5px; color:var(--ink-dim); background:var(--bg-panel-2); border:1px solid var(--line); border-radius:8px; padding:12px 14px;}
footer{text-align:center; color:var(--ink-faint); font-size:11px; font-family:var(--mono); margin-top:60px; padding-top:20px; border-top:1px solid var(--line);}
</style>
</head>
<body>
<div class="wrap">

  <div class="hdr">
    <div>
      <div class="eyebrow">Autonomous Agent Studio</div>
      <h1>Bug-Fix Pipeline</h1>
      <p>A live multi-agent loop — Planner, Executor, Evaluator, Critic, Improver, Safety Monitor, Memory Manager and Final Reviewer — collaborating in real rounds against the Claude API until your fix is provably done.</p>
    </div>
    <div class="hdr-right">
      <div class="pill"><span class="dot" id="conn-dot"></span><span id="conn-text">idle</span></div>
    </div>
  </div>

  <!-- SETUP -->
  <div class="card" id="setup-card">
    <div class="section-title">01 — Define the bug</div>
    <div class="field">
      <label for="code-input">Buggy code</label>
      <textarea id="code-input" rows="10" placeholder="Paste the buggy function / file here...">function calculateDiscount(price, discountPercent) {
  // Bug: discount sometimes results in negative or NaN prices,
  // and percentages > 100 aren't handled.
  let discount = price * discountPercent / 100;
  let final = price - discount;
  return final;
}

// Also: calculateDiscount("49.99", 20) should work but currently returns NaN
// because price arrives as a string from the form input.</textarea>
    </div>
    <div class="field">
      <label for="desc-input">Bug description / expected behavior</label>
      <textarea id="desc-input" rows="4" placeholder="Describe what's wrong and what should happen instead...">calculateDiscount should: accept numeric strings and coerce them safely, clamp discountPercent to [0,100], never return a negative price, round to 2 decimals, and throw a clear error for invalid (non-numeric) price input instead of returning NaN silently.</textarea>
    </div>
    <div class="section-title" style="margin-top:22px;">02 — Run parameters</div>
    <div class="row-inline">
      <div class="small-field">
        <label>Score threshold to stop</label>
        <select id="threshold-select">
          <option value="95" selected>≥ 95 / 100</option>
        </select>
      </div>
      <div class="small-field">
        <label>Plateau delta (2 rounds)</label>
        <select id="plateau-select">
          <option value="2" selected>&lt; 2 pts improvement</option>
          <option value="1">&lt; 1 pt improvement</option>
          <option value="3">&lt; 3 pts improvement</option>
        </select>
      </div>
      <div class="small-field">
        <label>Hard iteration cap (safety only)</label>
        <select id="cap-select">
          <option value="8" selected>8 rounds</option>
          <option value="6">6 rounds</option>
          <option value="10">10 rounds</option>
        </select>
      </div>
      <div style="flex:1"></div>
      <button class="btn btn-primary" id="run-btn">▶ Run pipeline</button>
    </div>
  </div>

  <!-- STUDIO -->
  <div class="studio" id="studio">
    <!-- LEFT: loop diagram -->
    <div class="card loop-card">
      <div class="section-title">Live orchestration loop</div>
      <div class="loop-svg-wrap">
        <svg viewBox="0 0 320 320" id="loop-svg">
          <!-- cycle path between evaluator(0) critic(1) improver(2) back to evaluator -->
          <path id="path-ev-cr" class="loop-path" d="M 160 60 A 110 110 0 0 1 254 220" />
          <path id="path-cr-im" class="loop-path" d="M 254 220 A 110 110 0 0 1 66 220" />
          <path id="path-im-ev" class="loop-path" d="M 66 220 A 110 110 0 0 1 160 60" marker-end="url(#arrowhead)" />
          <!-- branch to final reviewer -->
          <path id="path-branch" class="branch-path" d="M 160 60 L 160 12" marker-end="url(#arrowhead2)" />
          <defs>
            <marker id="arrowhead" markerWidth="8" markerHeight="8" refX="6" refY="4" orient="auto">
              <path d="M0,0 L8,4 L0,8 Z" fill="var(--line)" />
            </marker>
            <marker id="arrowhead2" markerWidth="8" markerHeight="8" refX="6" refY="4" orient="auto">
              <path d="M0,0 L8,4 L0,8 Z" fill="var(--line-soft)" />
            </marker>
          </defs>

          <circle id="pulse-dot" class="pulse" r="4" cx="160" cy="60" opacity="0"/>

          <!-- Planner / Executor (pre-loop) -->
          <circle class="node-circle" id="node-plan" cx="160" cy="160" r="34"/>
          <text x="160" y="156" text-anchor="middle" class="node-label">PLANNER</text>
          <text x="160" y="168" text-anchor="middle" class="node-sub">→ executor</text>

          <!-- Evaluator top -->
          <circle class="node-circle" id="node-eval" cx="160" cy="60" r="30"/>
          <text x="160" y="57" text-anchor="middle" class="node-label">EVALUATOR</text>
          <text x="160" y="69" text-anchor="middle" class="node-sub">scores draft</text>

          <!-- Critic right -->
          <circle class="node-circle" id="node-crit" cx="254" cy="220" r="30"/>
          <text x="254" y="217" text-anchor="middle" class="node-label">CRITIC</text>
          <text x="254" y="229" text-anchor="middle" class="node-sub">finds issues</text>

          <!-- Improver left -->
          <circle class="node-circle" id="node-imp" cx="66" cy="220" r="30"/>
          <text x="66" y="217" text-anchor="middle" class="node-label">IMPROVER</text>
          <text x="66" y="229" text-anchor="middle" class="node-sub">rewrites</text>

          <!-- Final reviewer top -->
          <circle class="node-circle" id="node-final" cx="160" cy="0" r="0" opacity="0"/>
        </svg>
      </div>
      <div class="agent-legend" id="agent-legend">
        <div class="agent-item" data-agent="plan"><span class="agent-swatch" style="background:var(--amber)"></span><div><h4>Planner</h4><p>Reads the bug + code once, produces a structured fix plan and edge cases to cover.</p></div></div>
        <div class="agent-item" data-agent="exec"><span class="agent-swatch" style="background:var(--amber)"></span><div><h4>Executor</h4><p>Writes the first working draft of the fixed code from the plan.</p></div></div>
        <div class="agent-item" data-agent="eval"><span class="agent-swatch" style="background:#7fb3ff"></span><div><h4>Evaluator</h4><p>Scores the current draft 0–100 on correctness + code quality, every round.</p></div></div>
        <div class="agent-item" data-agent="crit"><span class="agent-swatch" style="background:var(--red)"></span><div><h4>Critic</h4><p>Finds concrete, actionable flaws in the draft the evaluator flagged.</p></div></div>
        <div class="agent-item" data-agent="imp"><span class="agent-swatch" style="background:var(--teal)"></span><div><h4>Improver</h4><p>Rewrites the draft using the evaluation + critique. Feeds next round's Evaluator.</p></div></div>
        <div class="agent-item" data-agent="safety"><span class="agent-swatch" style="background:#b98cf2"></span><div><h4>Safety Monitor</h4><p>Flags risky patterns (injection, unsafe eval, unhandled input) each round.</p></div></div>
        <div class="agent-item" data-agent="mem"><span class="agent-swatch" style="background:#5c7a9c"></span><div><h4>Memory Manager</h4><p>Distills durable lessons across rounds so Improver doesn't repeat mistakes.</p></div></div>
        <div class="agent-item" data-agent="final"><span class="agent-swatch" style="background:#fff"></span><div><h4>Final Reviewer</h4><p>Signs off once a stop condition fires; writes the human-readable summary.</p></div></div>
      </div>
    </div>

    <!-- RIGHT: main column -->
    <div class="main-col">

      <div class="card status-bar">
        <div class="status-left">
          <div class="spinner" id="spinner"></div>
          <span class="round-badge" id="round-badge">Initializing…</span>
          <span class="status-msg" id="status-msg">—</span>
        </div>
        <div style="display:flex; gap:8px; flex-wrap:wrap;">
          <span class="stat-chip">Retries: <b id="stat-retries">0</b></span>
          <span class="stat-chip">API calls: <b id="stat-calls">0</b></span>
          <span class="stat-chip">Best score: <b id="stat-best">—</b></span>
        </div>
      </div>

      <div class="final-banner" id="final-banner">
        <h3 id="final-title">✓ Pipeline complete</h3>
        <p id="final-text"></p>
      </div>

      <div class="card">
        <div class="tabs">
          <div class="tab active" data-tab="rounds">Round history</div>
          <div class="tab" data-tab="draft">Current draft</div>
          <div class="tab" data-tab="chart">Score trend</div>
          <div class="tab" data-tab="memory">Memory</div>
          <div class="tab" data-tab="log">Activity log</div>
        </div>

        <div class="tab-panel active" id="panel-rounds"><div id="rounds-container"><p style="color:var(--ink-faint); font-family:var(--mono); font-size:12px;">Rounds will appear here once the loop starts…</p></div></div>

        <div class="tab-panel" id="panel-draft">
          <div class="subhead">Latest fixed code</div>
          <pre class="codeblock" id="draft-view">Waiting for executor…</pre>
        </div>

        <div class="tab-panel" id="panel-chart">
          <div class="chart-wrap"><svg id="chart-svg" viewBox="0 0 600 220" width="100%"></svg></div>
        </div>

        <div class="tab-panel" id="panel-memory">
          <div class="subhead">Cross-round memory entries</div>
          <div id="memory-container"><p style="color:var(--ink-faint); font-family:var(--mono); font-size:12px;">No memory entries yet.</p></div>
        </div>

        <div class="tab-panel" id="panel-log">
          <div class="log-box" id="log-box"></div>
        </div>
      </div>

    </div>
  </div>

  <!-- BOTTOM SECTIONS -->
  <div class="bottom-sections" id="bottom-sections" style="display:none;">

    <div>
      <h2>Final output & agent performance</h2>
      <div class="arch-grid" id="perf-grid"></div>
    </div>

    <div>
      <h2>How the stop-check governs the loop</h2>
      <div class="arch-grid">
        <div class="arch-item"><h4>01 · Plateau check</h4><p>After each Evaluator call, compare the last two score deltas. If both improvements fall below the plateau delta, the loop concludes the Improver has converged and hands off to Final Reviewer — even below threshold.</p></div>
        <div class="arch-item"><h4>02 · Threshold check</h4><p>If the current score meets or exceeds the target (95), the loop stops immediately — this is the "intended" successful ending most rounds are aiming for.</p></div>
        <div class="arch-item"><h4>03 · Hard cap (fallback)</h4><p>A fixed maximum round count exists purely as a safety net against runaway loops or a stubborn draft — it is never the goal, only a circuit breaker.</p></div>
        <div class="arch-item"><h4>State threading</h4><p>Each round's Evaluator sees the live draft + rubric. Critic sees the draft + that evaluation. Improver sees draft + evaluation + critique + accumulated memory. The next round's Evaluator only ever sees the Improver's fresh output — never stale drafts.</p></div>
      </div>
    </div>

    <div>
      <h2>Architecture overview</h2>
      <div class="arch-grid">
        <div class="arch-item"><h4>Pre-loop</h4><p>Planner reads the bug once and writes a structured plan. Executor turns that plan into the first draft — this seeds round 1's Evaluator.</p></div>
        <div class="arch-item"><h4>Per-round loop</h4><p>A JS <code>while(true)</code> loop calls Evaluator → Safety Monitor → Critic → (stop check) → Improver → Memory Manager, each a live <code>fetch</code> to the Messages API, appending to a running <code>history[]</code> array.</p></div>
        <div class="arch-item"><h4>No hardcoded rounds</h4><p>The number of iterations is unknown until runtime — it's whatever the stop-check decides, bounded only by the hard cap safety net.</p></div>
        <div class="arch-item"><h4>Resilience</h4><p>Each API call is wrapped in retry-with-backoff (up to 3 attempts) and a JSON-repair pass, so a malformed model response doesn't kill the run.</p></div>
      </div>
    </div>

    <div>
      <h2>Extension ideas</h2>
      <div class="ext-list">
        <div class="ext-item"><b>Test-execution loop</b>Give Executor a real sandboxed runner so Evaluator scores against actual test results, not just static reasoning.</div>
        <div class="ext-item"><b>Multi-file context</b>Extend Planner/Executor to operate across a small repo graph instead of a single snippet.</div>
        <div class="ext-item"><b>Human-in-the-loop gate</b>Pause before Final Reviewer and let a person approve or redirect the Improver's next pass.</div>
        <div class="ext-item"><b>Specialized Critics</b>Split Critic into Security Critic + Style Critic + Performance Critic running in parallel each round.</div>
        <div class="ext-item"><b>Persistent memory store</b>Move Memory Manager's entries into a vector store so lessons persist across entirely separate pipeline runs.</div>
        <div class="ext-item"><b>Adaptive thresholds</b>Let Planner set the score threshold dynamically based on how critical the bug is.</div>
      </div>
    </div>

    <div>
      <h2>Prompts for building more advanced autonomous systems</h2>
      <div class="prompt-list">
        <div class="prompt-item">"Add a parallel Security Critic and Performance Critic to this pipeline, have Improver reconcile conflicting feedback between them each round."</div>
        <div class="prompt-item">"Wire the Executor to a real code-execution sandbox so the Evaluator can score against actual passing/failing tests instead of static analysis."</div>
        <div class="prompt-item">"Turn Memory Manager into a persistent store shared across multiple bug-fix runs so the pipeline gets better over time."</div>
        <div class="prompt-item">"Add a human-approval gate between Critic and Improver for high-risk changes flagged by Safety Monitor."</div>
      </div>
    </div>

  </div>

  <footer>Autonomous Agent Studio — orchestration runs live against api.anthropic.com/v1/messages. No API key required in this environment.</footer>
</div>

<script>
(function(){
  const MODEL = "claude-sonnet-4-6";
  const API_URL = "https://api.anthropic.com/v1/messages";

  const el = id => document.getElementById(id);
  const runBtn = el('run-btn');
  const codeInput = el('code-input');
  const descInput = el('desc-input');
  const threshold = () => parseInt(el('threshold-select').value,10);
  const plateauDelta = () => parseInt(el('plateau-select').value,10);
  const hardCap = () => parseInt(el('cap-select').value,10);

  let stats = { retries:0, calls:0, best:null };
  let history = []; // {round, score, critique, draft, delta, safety}
  let memory = [];
  let currentDraft = "";

  function setConn(state){
    const dot = el('conn-dot'), txt = el('conn-text');
    dot.className = 'dot' + (state==='live' ? ' live' : state==='err' ? ' err' : '');
    txt.textContent = state==='live' ? 'connected' : state==='err' ? 'error' : 'idle';
  }

  function log(tag, msg, kind){
    const box = el('log-box');
    const line = document.createElement('div');
    line.className = 'log-line' + (kind ? ' '+kind : '');
    const time = new Date().toLocaleTimeString();
    line.innerHTML = `<span class="tag">[${tag}]</span><span>${escapeHtml(msg)} <span style="color:var(--ink-faint)">· ${time}</span></span>`;
    box.appendChild(line);
    box.scrollTop = box.scrollHeight;
  }

  function escapeHtml(s){
    return String(s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
  }

  function setStatus(round, msg){
    el('round-badge').textContent = round;
    el('status-msg').textContent = msg;
  }

  function setSpinner(on){
    el('spinner').style.display = on ? 'block' : 'none';
  }

  function setActiveAgent(agentKey){
    document.querySelectorAll('.agent-item').forEach(i => i.classList.toggle('active', i.dataset.agent===agentKey));
    document.querySelectorAll('.node-circle').forEach(n => n.classList.remove('active'));
    const map = {plan:'node-plan', exec:'node-plan', eval:'node-eval', crit:'node-crit', imp:'node-imp', safety:'node-eval', mem:'node-imp', final:'node-final'};
    const nodeId = map[agentKey];
    if(nodeId){ const n = el(nodeId); if(n) n.classList.add('active'); }
    movePulse(agentKey);
  }

  function movePulse(agentKey){
    const pulse = el('pulse-dot');
    const pos = {
      eval:{x:160,y:60}, crit:{x:254,y:220}, imp:{x:66,y:220}, safety:{x:160,y:60}, mem:{x:66,y:220}
    };
    if(pos[agentKey]){
      pulse.setAttribute('opacity','1');
      pulse.setAttribute('cx', pos[agentKey].x);
      pulse.setAttribute('cy', pos[agentKey].y);
    } else {
      pulse.setAttribute('opacity','0');
    }
  }

  function updateStatChips(){
    el('stat-retries').textContent = stats.retries;
    el('stat-calls').textContent = stats.calls;
    el('stat-best').textContent = stats.best===null ? '—' : stats.best+'/100';
  }

  // -------- API CALL WITH RETRY --------
  async function callAgent(systemPrompt, userPrompt, {json=false, maxTokens=1800} = {}){
    let attempt = 0;
    const maxAttempts = 3;
    while(attempt < maxAttempts){
      attempt++;
      try{
        stats.calls++; updateStatChips();
        const res = await fetch(API_URL, {
          method:"POST",
          headers:{"Content-Type":"application/json"},
          body: JSON.stringify({
            model: MODEL,
            max_tokens: maxTokens,
            system: systemPrompt,
            messages: [{role:"user", content:userPrompt}]
          })
        });
        if(!res.ok){
          throw new Error("HTTP "+res.status);
        }
        const data = await res.json();
        setConn('live');
        const textBlocks = (data.content||[]).filter(b=>b.type==="text").map(b=>b.text);
        const text = textBlocks.join("\n").trim();
        if(!text) throw new Error("Empty response");
        if(json){
          return extractJson(text);
        }
        return text;
      }catch(err){
        setConn('err');
        stats.retries++; updateStatChips();
        log('RETRY', `Attempt ${attempt} failed (${err.message}). ${attempt<maxAttempts ? 'Retrying…' : 'Giving up.'}`, 'err');
        if(attempt >= maxAttempts) throw err;
        await new Promise(r=>setTimeout(r, 500*attempt));
      }
    }
  }

  function extractJson(text){
    let cleaned = text.replace(/```json/gi,'').replace(/```/g,'').trim();
    // try to find first { ... last }
    const start = cleaned.indexOf('{');
    const end = cleaned.lastIndexOf('}');
    if(start!==-1 && end!==-1){
      cleaned = cleaned.slice(start, end+1);
    }
    try{
      return JSON.parse(cleaned);
    }catch(e){
      // best-effort repair: strip trailing commas
      try{
        const repaired = cleaned.replace(/,(\s*[}\]])/g,'$1');
        return JSON.parse(repaired);
      }catch(e2){
        throw new Error("Could not parse JSON from model response");
      }
    }
  }

  function extractCode(text){
    const match = text.match(/```(?:[a-zA-Z]*)\n([\s\S]*?)```/);
    return match ? match[1].trim() : text.trim();
  }

  // -------- SYSTEM PROMPTS --------
  const SYS = {
    planner: `You are the Planner agent in an autonomous bug-fix pipeline. You receive buggy code and a bug description. Produce a concise, structured fix plan: root cause analysis, the concrete behavioral requirements the fix must satisfy, and a list of edge cases to cover. Do not write code. Be specific and technical. Keep it under 200 words.`,

    executor: `You are the Executor agent in an autonomous bug-fix pipeline. You receive the original buggy code, the bug description, and a fix plan from the Planner. Write a complete, corrected version of the code that satisfies every requirement in the plan. Output ONLY a single fenced code block with the full corrected code — no prose before or after.`,

    evaluator: `You are the Evaluator agent in an autonomous bug-fix pipeline. You score a candidate code fix against a rubric of correctness and code quality. Be rigorous and consistent — do not inflate scores. A 95+ score should mean the fix is essentially production-ready with no remaining meaningful issues.
Score sub-dimensions internally (correctness/bug resolution, edge-case handling, code quality/idiom, regression risk) but report a single overall integer score 0-100.
Respond ONLY with strict JSON, no markdown fences, no prose outside the JSON, in exactly this shape:
{"score": <integer 0-100>, "reasoning": "<3-5 sentence justification citing specific lines/behaviors>", "remaining_issues": ["<short issue>", "..."]}`,

    safety: `You are the Safety Monitor agent in an autonomous bug-fix pipeline. Inspect the candidate code fix for risky patterns: unsafe eval/exec, injection vectors, unhandled untrusted input, unsafe type coercion, resource leaks, or logic that could silently corrupt data. This is advisory, not blocking. Respond ONLY with strict JSON, no prose outside it:
{"risk_level": "none"|"low"|"medium"|"high", "flags": ["<short flag>", "..."]}`,

    critic: `You are the Critic agent in an autonomous bug-fix pipeline. You receive the candidate code, the Evaluator's score and reasoning, and its list of remaining issues. Your job is to turn that into concrete, actionable critique for the Improver: name exact problems and, where useful, the specific line or pattern at fault. Do not rewrite the code yourself. Do not repeat generic advice — be specific to this draft. Keep it under 180 words, plain text (no JSON, no code fences).`,

    improver: `You are the Improver agent in an autonomous bug-fix pipeline. You receive the current code draft, the Evaluator's score/reasoning, the Critic's specific feedback, and accumulated memory notes from prior rounds. Rewrite the code to resolve every issue raised, without introducing regressions or removing correct behavior. Output ONLY a single fenced code block with the full improved code — no prose before or after.`,

    memory: `You are the Memory Manager agent in an autonomous bug-fix pipeline. Given this round's evaluation and critique, distill ONE short durable lesson (max 20 words) that should NOT be forgotten in later rounds — a recurring mistake to avoid or a constraint to keep satisfying. Respond with plain text only, just the single lesson sentence, nothing else.`,

    finalReviewer: `You are the Final Reviewer agent in an autonomous bug-fix pipeline. You receive the full round history (scores, critiques) and the final code draft. Write a concise, human-facing sign-off: confirm what was fixed, note the final score and why the loop stopped, and flag anything a human should still double check before shipping. Keep it under 150 words, plain text.`
  };

  // -------- UI RENDER HELPERS --------
  function scoreClass(score){
    if(score>=90) return 'good';
    if(score>=75) return 'mid';
    return 'low';
  }

  function renderRoundCard(entry){
    const container = el('rounds-container');
    if(container.querySelector('p')) container.innerHTML = '';
    const div = document.createElement('div');
    div.className = 'round-card';
    const deltaTxt = entry.delta===null ? '' : `<span class="delta ${entry.delta>0?'pos':''}">Δ ${entry.delta>0?'+':''}${entry.delta}</span>`;
    div.innerHTML = `
      <div class="round-hdr">
        <h3>Round ${entry.round} — Evaluator + Critic + Improver</h3>
        <div style="display:flex; align-items:center; gap:10px;">
          ${deltaTxt}
          <span class="score-tag ${scoreClass(entry.score)}">${entry.score}/100</span>
        </div>
      </div>
      <div class="subhead">Evaluator reasoning</div>
      <div class="crit-block">${escapeHtml(entry.reasoning||'')}</div>
      <div class="subhead">Critic feedback</div>
      <div class="crit-block">${escapeHtml(entry.critique||'')}</div>
      ${entry.safetyFlags && entry.safetyFlags.length ? `<div class="subhead">Safety monitor (${entry.safetyRisk})</div><div class="crit-block">${escapeHtml(entry.safetyFlags.join(' · '))}</div>` : ''}
    `;
    container.appendChild(div);
  }

  function renderMemory(){
    const container = el('memory-container');
    if(memory.length===0) return;
    container.innerHTML = '';
    memory.forEach((m,i)=>{
      const d = document.createElement('div');
      d.className = 'mem-item';
      d.textContent = `#${i+1} · ${m}`;
      container.appendChild(d);
    });
  }

  function renderDraft(){
    el('draft-view').textContent = currentDraft || '—';
  }

  function renderChart(){
    const svg = el('chart-svg');
    const w=600,h=220,pad=36;
    const pts = history.map(h=>h.score);
    if(pts.length===0){ svg.innerHTML=''; return; }
    const maxY=100, minY=0;
    const stepX = pts.length>1 ? (w-2*pad)/(pts.length-1) : 0;
    const toY = v => h-pad - (v-minY)/(maxY-minY)*(h-2*pad);
    let path = pts.map((v,i)=>`${i===0?'M':'L'} ${pad+i*stepX} ${toY(v)}`).join(' ');
    let gridLines = '';
    [0,25,50,75,95,100].forEach(v=>{
      const y=toY(v);
      gridLines += `<line x1="${pad}" y1="${y}" x2="${w-pad}" y2="${y}" stroke="${v===95?'var(--amber-dim)':'var(--line-soft)'}" stroke-width="1" stroke-dasharray="${v===95?'0':'2 4'}"/>`;
      gridLines += `<text x="4" y="${y+3}" font-size="9" fill="var(--ink-faint)" font-family="var(--mono)">${v}</text>`;
    });
    let dots = pts.map((v,i)=>`<circle cx="${pad+i*stepX}" cy="${toY(v)}" r="3.5" fill="${v>=95?'var(--teal)':'var(--amber)'}"/>`).join('');
    let labels = pts.map((v,i)=>`<text x="${pad+i*stepX}" y="${h-8}" font-size="9" text-anchor="middle" fill="var(--ink-faint)" font-family="var(--mono)">R${i+1}</text>`).join('');
    svg.innerHTML = gridLines + `<path d="${path}" fill="none" stroke="var(--amber)" stroke-width="2"/>` + dots + labels;
  }

  function switchTab(tabName){
    document.querySelectorAll('.tab').forEach(t=>t.classList.toggle('active', t.dataset.tab===tabName));
    document.querySelectorAll('.tab-panel').forEach(p=>p.classList.toggle('active', p.id==='panel-'+tabName));
  }
  document.querySelectorAll('.tab').forEach(t=>t.addEventListener('click', ()=>switchTab(t.dataset.tab)));

  // -------- MAIN PIPELINE --------
  async function runPipeline(){
    runBtn.disabled = true;
    el('studio').classList.add('active');
    el('bottom-sections').style.display = 'none';
    el('final-banner').classList.remove('show');
    history = []; memory = []; stats = {retries:0, calls:0, best:null};
    updateStatChips();
    el('rounds-container').innerHTML = '<p style="color:var(--ink-faint); font-family:var(--mono); font-size:12px;">Rounds will appear here once the loop starts…</p>';
    el('memory-container').innerHTML = '<p style="color:var(--ink-faint); font-family:var(--mono); font-size:12px;">No memory entries yet.</p>';
    el('log-box').innerHTML = '';
    setSpinner(true);

    const bugCode = codeInput.value.trim();
    const bugDesc = descInput.value.trim();
    const targetScore = threshold();
    const pDelta = plateauDelta();
    const cap = hardCap();

    try{
      // ---- PLANNER ----
      setStatus('Planning', 'Planner analyzing bug and drafting fix plan…');
      setActiveAgent('plan');
      log('PLANNER','Sending bug + code for analysis…');
      const plan = await callAgent(SYS.planner, `Buggy code:\n${bugCode}\n\nBug description / expected behavior:\n${bugDesc}`);
      log('PLANNER','Plan received.', 'ok');

      // ---- EXECUTOR ----
      setStatus('Executing', 'Executor writing first draft fix…');
      setActiveAgent('exec');
      log('EXECUTOR','Generating first draft from plan…');
      const execRaw = await callAgent(SYS.executor, `Original buggy code:\n${bugCode}\n\nBug description:\n${bugDesc}\n\nFix plan:\n${plan}`);
      currentDraft = extractCode(execRaw);
      renderDraft();
      log('EXECUTOR','First draft ready.', 'ok');

      // ---- LOOP ----
      let round = 0;
      let stopReason = null;
      let prevScore = null;
      let deltas = [];

      while(true){
        round++;
        setStatus(`Round ${round}`, 'Evaluator scoring current draft…');
        setActiveAgent('eval');
        log('EVALUATOR', `Round ${round}: scoring draft…`);
        const evalResult = await callAgent(SYS.evaluator,
          `Candidate code:\n${currentDraft}\n\nOriginal bug description / requirements:\n${bugDesc}\n\nMemory notes from prior rounds:\n${memory.join('\n') || '(none yet)'}`,
          {json:true});
        const score = Math.max(0, Math.min(100, Math.round(evalResult.score)));
        log('EVALUATOR', `Round ${round} score: ${score}/100`, 'ok');

        // ---- SAFETY MONITOR ----
        setStatus(`Round ${round}`, 'Safety Monitor scanning for risk patterns…');
        setActiveAgent('safety');
        log('SAFETY', `Round ${round}: scanning draft for risk patterns…`);
        let safety = {risk_level:'none', flags:[]};
        try{
          safety = await callAgent(SYS.safety, `Candidate code:\n${currentDraft}`, {json:true, maxTokens:600});
        }catch(e){
          log('SAFETY', 'Safety scan failed, continuing without it.', 'err');
        }
        log('SAFETY', `Round ${round}: risk=${safety.risk_level||'none'}${safety.flags && safety.flags.length ? ' — '+safety.flags.join('; ') : ''}`, safety.risk_level==='high'?'err':'ok');

        // ---- CRITIC ----
        setStatus(`Round ${round}`, 'Critic identifying concrete issues…');
        setActiveAgent('crit');
        log('CRITIC', `Round ${round}: generating specific critique…`);
        const critique = await callAgent(SYS.critic,
          `Candidate code:\n${currentDraft}\n\nEvaluator score: ${score}/100\nEvaluator reasoning: ${evalResult.reasoning}\nRemaining issues flagged: ${(evalResult.remaining_issues||[]).join('; ')}`);
        log('CRITIC', `Round ${round}: critique received.`, 'ok');

        const delta = prevScore===null ? null : (score - prevScore);
        if(delta!==null) deltas.push(delta);
        stats.best = stats.best===null ? score : Math.max(stats.best, score);
        updateStatChips();

        history.push({round, score, reasoning: evalResult.reasoning, critique, delta, draft: currentDraft, safetyFlags: safety.flags, safetyRisk: safety.risk_level});
        renderRoundCard(history[history.length-1]);
        renderChart();

        // ---- STOP CHECKS (in order) ----
        setStatus(`Round ${round}`, 'Checking stop condition…');
        log('STOP-CHECK', `Round ${round}: evaluating plateau → threshold → hard cap…`);

        // 1. Plateau: last two deltas both < pDelta (need at least 2 rounds of delta history)
        if(deltas.length>=2 && deltas[deltas.length-1] < pDelta && deltas[deltas.length-2] < pDelta){
          stopReason = {type:'plateau', detail:`Score improvement fell below ${pDelta} pts for two consecutive rounds (Δ${deltas[deltas.length-2]}, Δ${deltas[deltas.length-1]}). Improver has converged.`};
        }
        // 2. Threshold
        else if(score >= targetScore){
          stopReason = {type:'threshold', detail:`Score ${score} met or exceeded the target threshold of ${targetScore}.`};
        }
        // 3. Hard cap
        else if(round >= cap){
          stopReason = {type:'hardcap', detail:`Reached the hard iteration cap of ${cap} rounds without meeting threshold or plateauing — safety fallback triggered.`};
        }

        if(stopReason){
          log('STOP-CHECK', `Stop condition fired: ${stopReason.type.toUpperCase()} — ${stopReason.detail}`, 'ok');
          break;
        }

        // ---- IMPROVER ----
        setStatus(`Round ${round}`, 'Improver rewriting draft…');
        setActiveAgent('imp');
        log('IMPROVER', `Round ${round}: rewriting draft using evaluation + critique…`);
        const impRaw = await callAgent(SYS.improver,
          `Current draft:\n${currentDraft}\n\nEvaluator score: ${score}/100\nEvaluator reasoning: ${evalResult.reasoning}\n\nCritic feedback:\n${critique}\n\nMemory notes:\n${memory.join('\n') || '(none yet)'}\n\nOriginal requirements:\n${bugDesc}`);
        currentDraft = extractCode(impRaw);
        renderDraft();
        log('IMPROVER', `Round ${round}: improved draft ready.`, 'ok');

        // ---- MEMORY MANAGER ----
        setStatus(`Round ${round}`, 'Memory Manager distilling lesson…');
        setActiveAgent('mem');
        try{
          const lesson = await callAgent(SYS.memory,
            `Evaluator reasoning: ${evalResult.reasoning}\nCritic feedback: ${critique}`, {maxTokens:200});
          memory.push(lesson);
          renderMemory();
          log('MEMORY', `Round ${round}: "${lesson}"`, 'ok');
        }catch(e){
          log('MEMORY', 'Memory distillation failed, continuing without it.', 'err');
        }

        prevScore = score;
      }

      // ---- FINAL REVIEWER ----
      setStatus('Final review', 'Final Reviewer signing off…');
      setActiveAgent('final');
      document.getElementById('node-final').setAttribute('r','30');
      document.getElementById('node-final').setAttribute('opacity','1');
      document.getElementById('node-final').setAttribute('cx','160');
      document.getElementById('node-final').setAttribute('cy','12');
      log('FINAL', 'Compiling final sign-off…');
      const historySummary = history.map(h=>`Round ${h.round}: score ${h.score}, delta ${h.delta===null?'n/a':h.delta}`).join('\n');
      const finalText = await callAgent(SYS.finalReviewer,
        `Round history:\n${historySummary}\n\nStop reason: ${stopReason.type} — ${stopReason.detail}\n\nFinal code draft:\n${currentDraft}`);
      log('FINAL', 'Sign-off complete.', 'ok');

      setSpinner(false);
      setStatus(`Complete — ${history.length} round${history.length===1?'':'s'} run`, `Stopped on: ${stopReason.type.toUpperCase()}`);
      el('final-banner').classList.add('show');
      el('final-title').textContent = `✓ Pipeline complete — stopped on ${stopReason.type.toUpperCase()}`;
      el('final-text').textContent = finalText;

      renderBottomSections(stopReason, finalText);
      switchTab('draft');

    }catch(err){
      setSpinner(false);
      setConn('err');
      setStatus('Failed', err.message || 'Unexpected error');
      log('FATAL', err.message || String(err), 'err');
    }finally{
      runBtn.disabled = false;
    }
  }

  function renderBottomSections(stopReason, finalText){
    el('bottom-sections').style.display = 'flex';
    const grid = el('perf-grid');
    grid.innerHTML = '';
    const first = history[0], last = history[history.length-1];
    const items = [
      {h:'Final code', p: null, code:true},
      {h:'Rounds run', p:`${history.length} evaluator/critic/improver rounds, ${stats.calls} total live API calls, ${stats.retries} retries recovered.`},
      {h:'Score trajectory', p:`Started at ${first.score}/100, ended at ${last.score}/100 (best: ${stats.best}/100). Stopped via ${stopReason.type.toUpperCase()}.`},
      {h:'Final Reviewer sign-off', p: finalText},
      {h:'Safety posture', p: history.map(h=>`R${h.round}: ${h.safetyRisk||'none'}`).join(' · ')},
      {h:'Memory lessons captured', p: memory.length ? memory.join(' · ') : 'None needed — converged quickly.'}
    ];
    items.forEach(it=>{
      const div = document.createElement('div');
      div.className = 'arch-item';
      if(it.code){
        div.innerHTML = `<h4>${it.h}</h4><pre class="codeblock" style="max-height:220px; overflow:auto; margin-top:8px;">${escapeHtml(currentDraft)}</pre>`;
      } else {
        div.innerHTML = `<h4>${it.h}</h4><p>${escapeHtml(it.p)}</p>`;
      }
      grid.appendChild(div);
    });
  }

  runBtn.addEventListener('click', runPipeline);
})();
</script>
</body>
</html>
