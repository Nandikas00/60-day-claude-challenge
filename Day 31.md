# Today, I Built an AI Supply Chain Control Tower using claude :
📚 Key Learnings :

- Learned how AI can provide real-time visibility across an entire supply chain instead of monitoring individual operations.

- Understood the importance of integrating inventory, logistics, supplier, and demand data into a single control dashboard.

- Explored how predictive analytics can identify potential disruptions before they impact business operations.

- Gained experience designing AI-assisted decision support for inventory optimization and replenishment planning.

- Learned how supply chain KPIs such as inventory turnover, order fulfillment, lead time, and service level influence operational decisions.

- Understood how automation can reduce manual monitoring by generating intelligent alerts and recommendations.

- Improved skills in prompt engineering by breaking down complex business requirements into structured AI prompts.

- Learned how interactive dashboards help decision-makers prioritize critical issues and respond faster during supply chain disruptions.

- Explored the role of scenario analysis and "what-if" simulations in evaluating operational strategies.

- Gained practical experience building an AI-powered business application using Claude while combining domain knowledge with software development.

## OUTPUT SCREENSHOT :

<img width="1570" height="898" alt="Screenshot (473)" src="https://github.com/user-attachments/assets/89a3fbeb-0289-4644-8099-40e8f76c240a" />

### HTML File :

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Supply Chain Control Tower</title>
<style>
  :root{
    --bg-0:#060a14;
    --bg-1:#0a1120;
    --bg-2:#0f1a2e;
    --panel:#111c33;
    --panel-border:#1f3358;
    --cyan:#3fd6ff;
    --blue:#4d8bff;
    --green:#3ee0a0;
    --orange:#ffb24d;
    --red:#ff5470;
    --text-0:#eaf2ff;
    --text-1:#9db2d6;
    --text-2:#5f7196;
    --mono: 'JetBrains Mono', 'Courier New', monospace;
    --sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  }
  *{box-sizing:border-box; margin:0; padding:0;}
  html,body{height:100%;}
  body{
    background:
      radial-gradient(1200px 600px at 15% -10%, rgba(63,214,255,0.08), transparent 60%),
      radial-gradient(1000px 500px at 100% 0%, rgba(77,139,255,0.10), transparent 55%),
      var(--bg-0);
    color:var(--text-0);
    font-family:var(--sans);
    overflow-x:hidden;
    min-height:100%;
  }
  ::selection{background:var(--cyan); color:#00131a;}
  ::-webkit-scrollbar{width:8px; height:8px;}
  ::-webkit-scrollbar-track{background:var(--bg-1);}
  ::-webkit-scrollbar-thumb{background:var(--panel-border); border-radius:4px;}

  /* ============ layout shells ============ */
  .app{max-width:1400px; margin:0 auto; padding:18px 22px 40px;}
  .hidden{display:none !important;}

  /* ============ top bar ============ */
  .topbar{
    display:flex; align-items:center; justify-content:space-between;
    padding:14px 18px; margin-bottom:16px;
    background:linear-gradient(180deg, rgba(17,28,51,0.9), rgba(10,17,32,0.9));
    border:1px solid var(--panel-border);
    border-radius:14px;
    backdrop-filter: blur(6px);
  }
  .brand{display:flex; align-items:center; gap:12px;}
  .brand-mark{
    width:38px; height:38px; border-radius:10px;
    background:conic-gradient(from 220deg, var(--cyan), var(--blue), var(--cyan));
    display:flex; align-items:center; justify-content:center;
    font-weight:800; color:#00131a; font-size:16px;
    box-shadow:0 0 22px rgba(63,214,255,0.45);
  }
  .brand-text h1{font-size:16px; letter-spacing:0.04em; font-weight:700;}
  .brand-text span{font-size:11px; color:var(--text-2); letter-spacing:0.14em; text-transform:uppercase;}
  .top-actions{display:flex; gap:8px; align-items:center;}
  .icon-btn{
    display:flex; align-items:center; gap:6px;
    background:var(--bg-2); border:1px solid var(--panel-border);
    color:var(--text-1); padding:8px 12px; border-radius:9px;
    font-size:12px; cursor:pointer; transition:all .15s ease;
    font-family:var(--sans); font-weight:600;
  }
  .icon-btn:hover{border-color:var(--cyan); color:var(--cyan); box-shadow:0 0 12px rgba(63,214,255,0.2);}
  .icon-btn.active{color:var(--cyan); border-color:var(--cyan);}

  .clock{
    font-family:var(--mono); font-size:22px; font-weight:700;
    color:var(--cyan); letter-spacing:0.05em;
    padding:6px 14px; border-radius:8px;
    background:rgba(63,214,255,0.08); border:1px solid rgba(63,214,255,0.3);
    min-width:92px; text-align:center;
  }
  .clock.warn{color:var(--orange); border-color:rgba(255,178,77,0.4); background:rgba(255,178,77,0.08);}
  .clock.crit{color:var(--red); border-color:rgba(255,84,112,0.5); background:rgba(255,84,112,0.1); animation:pulseSoft 1s infinite;}

  /* ============ KPI strip ============ */
  .kpi-grid{
    display:grid; grid-template-columns:repeat(8, 1fr); gap:10px; margin-bottom:16px;
  }
  .kpi-card{
    background:linear-gradient(180deg, rgba(17,28,51,0.85), rgba(10,17,32,0.85));
    border:1px solid var(--panel-border); border-radius:12px;
    padding:12px 12px 10px;
    position:relative; overflow:hidden;
    transition:transform .2s ease, box-shadow .2s ease;
  }
  .kpi-card::after{
    content:''; position:absolute; inset:0;
    background:radial-gradient(120px 60px at 20% 0%, rgba(63,214,255,0.10), transparent 70%);
    pointer-events:none;
  }
  .kpi-card:hover{transform:translateY(-2px); box-shadow:0 8px 24px rgba(0,0,0,0.4);}
  .kpi-label{font-size:10px; letter-spacing:0.08em; text-transform:uppercase; color:var(--text-2); font-weight:700; margin-bottom:6px;}
  .kpi-value{font-family:var(--mono); font-size:20px; font-weight:700; color:var(--text-0); display:flex; align-items:baseline; gap:3px;}
  .kpi-value .unit{font-size:11px; color:var(--text-2); font-weight:500;}
  .kpi-delta{font-size:11px; margin-top:4px; font-weight:600; height:14px;}
  .kpi-delta.up{color:var(--green);}
  .kpi-delta.down{color:var(--red);}
  .kpi-bar{height:4px; border-radius:2px; background:var(--bg-1); margin-top:8px; overflow:hidden;}
  .kpi-bar-fill{height:100%; border-radius:2px; transition:width .4s ease, background .4s ease;}
  .kpi-score .kpi-value{color:var(--cyan);}
  .kpi-flash{animation:flashCard .5s ease;}
  @keyframes flashCard{
    0%{box-shadow:0 0 0 0 rgba(63,214,255,0.6);}
    100%{box-shadow:0 0 0 14px rgba(63,214,255,0);}
  }

  /* ============ main grid ============ */
  .main-grid{
    display:grid; grid-template-columns:1.55fr 1fr; gap:16px; align-items:start;
  }

  .panel{
    background:linear-gradient(180deg, rgba(17,28,51,0.75), rgba(10,17,32,0.75));
    border:1px solid var(--panel-border); border-radius:14px;
    padding:16px 16px 18px;
  }
  .panel-head{
    display:flex; align-items:center; justify-content:space-between;
    margin-bottom:12px; padding-bottom:10px;
    border-bottom:1px solid var(--panel-border);
  }
  .panel-head h2{font-size:13px; letter-spacing:0.08em; text-transform:uppercase; color:var(--text-1); font-weight:700;}
  .panel-head .count-pill{
    font-family:var(--mono); font-size:11px; color:var(--cyan);
    background:rgba(63,214,255,0.1); border:1px solid rgba(63,214,255,0.25);
    padding:2px 9px; border-radius:20px;
  }

  /* ============ alert feed ============ */
  .alert-feed{display:flex; flex-direction:column; gap:12px; min-height:120px;}
  .empty-state{
    text-align:center; color:var(--text-2); font-size:13px; padding:40px 10px;
    border:1px dashed var(--panel-border); border-radius:10px;
  }

  .alert-card{
    background:var(--bg-2); border:1px solid var(--panel-border); border-left:4px solid var(--blue);
    border-radius:10px; padding:14px 14px 12px;
    animation:slideIn .35s ease;
    position:relative;
  }
  @keyframes slideIn{
    from{opacity:0; transform:translateX(-16px);}
    to{opacity:1; transform:translateX(0);}
  }
  .alert-card.priority-critical{border-left-color:var(--red);}
  .alert-card.priority-high{border-left-color:var(--orange);}
  .alert-card.priority-medium{border-left-color:var(--blue);}
  .alert-card.pulse-crit{animation:slideIn .35s ease, pulseCard 1.4s infinite;}
  @keyframes pulseCard{
    0%,100%{box-shadow:0 0 0 0 rgba(255,84,112,0.0);}
    50%{box-shadow:0 0 0 3px rgba(255,84,112,0.18);}
  }
  .alert-card.resolving{animation:dissolveOut .4s ease forwards;}
  @keyframes dissolveOut{
    to{opacity:0; transform:scale(0.97) translateX(10px); max-height:0; padding:0; margin:0; border:0;}
  }

  .alert-top{display:flex; justify-content:space-between; align-items:flex-start; gap:10px; margin-bottom:6px;}
  .alert-title-wrap{display:flex; align-items:center; gap:8px;}
  .alert-icon{font-size:18px;}
  .alert-title{font-size:14px; font-weight:700; color:var(--text-0);}
  .badge{
    font-size:9.5px; font-weight:800; letter-spacing:0.06em; text-transform:uppercase;
    padding:3px 8px; border-radius:5px; white-space:nowrap;
  }
  .badge.priority-critical{background:rgba(255,84,112,0.15); color:var(--red); border:1px solid rgba(255,84,112,0.4);}
  .badge.priority-high{background:rgba(255,178,77,0.15); color:var(--orange); border:1px solid rgba(255,178,77,0.4);}
  .badge.priority-medium{background:rgba(77,139,255,0.15); color:var(--blue); border:1px solid rgba(77,139,255,0.4);}

  .alert-desc{font-size:12.5px; color:var(--text-1); line-height:1.5; margin-bottom:8px;}
  .alert-meta{display:flex; gap:14px; font-size:11px; color:var(--text-2); margin-bottom:10px; font-family:var(--mono);}
  .alert-meta b{color:var(--text-1); font-weight:700;}
  .alert-timer{color:var(--orange);}
  .alert-timer.crit{color:var(--red);}

  .alert-actions{display:flex; flex-wrap:wrap; gap:7px;}
  .action-btn{
    background:var(--bg-1); border:1px solid var(--panel-border); color:var(--text-1);
    font-size:11.5px; font-weight:600; padding:7px 11px; border-radius:7px; cursor:pointer;
    transition:all .15s ease; font-family:var(--sans);
  }
  .action-btn:hover{border-color:var(--cyan); color:var(--cyan); background:rgba(63,214,255,0.08); transform:translateY(-1px);}
  .action-btn.ignore{color:var(--text-2);}
  .action-btn.ignore:hover{border-color:var(--red); color:var(--red); background:rgba(255,84,112,0.08);}
  .action-btn.delay{color:var(--text-2);}
  .action-btn.delay:hover{border-color:var(--orange); color:var(--orange); background:rgba(255,178,77,0.08);}

  .alert-timerbar{height:3px; border-radius:2px; background:var(--bg-1); margin-top:10px; overflow:hidden;}
  .alert-timerbar-fill{height:100%; background:linear-gradient(90deg, var(--cyan), var(--orange)); transition:width .3s linear;}

  /* ============ event log ============ */
  .log-list{display:flex; flex-direction:column-reverse; gap:8px; max-height:560px; overflow-y:auto; padding-right:4px;}
  .log-item{
    font-size:12px; padding:9px 10px; border-radius:8px; background:var(--bg-2);
    border-left:3px solid var(--panel-border); line-height:1.4;
    animation:logIn .3s ease;
  }
  @keyframes logIn{from{opacity:0; transform:translateY(-6px);} to{opacity:1; transform:translateY(0);}}
  .log-item .log-time{color:var(--text-2); font-family:var(--mono); font-size:10px; margin-right:6px;}
  .log-item.good{border-left-color:var(--green); color:#c8f5e2;}
  .log-item.bad{border-left-color:var(--red); color:#ffd0d9;}
  .log-item.neutral{border-left-color:var(--text-2); color:var(--text-1);}
  .log-item.spawn{border-left-color:var(--blue); color:var(--text-1);}

  /* ============ overlays / modals ============ */
  .overlay{
    position:fixed; inset:0; background:rgba(3,6,14,0.82);
    display:flex; align-items:center; justify-content:center; z-index:100;
    backdrop-filter: blur(4px);
    padding:20px;
  }
  .modal{
    background:linear-gradient(180deg, rgba(17,28,51,0.98), rgba(9,15,28,0.98));
    border:1px solid var(--panel-border); border-radius:16px;
    padding:30px 32px; max-width:520px; width:100%;
    box-shadow:0 20px 60px rgba(0,0,0,0.6);
    max-height:88vh; overflow-y:auto;
  }
  .modal h2{font-size:20px; margin-bottom:14px; color:var(--cyan);}
  .modal p, .modal li{font-size:13.5px; color:var(--text-1); line-height:1.65;}
  .modal ul{margin:10px 0 10px 18px;}
  .modal h3{font-size:13px; color:var(--text-0); margin:14px 0 6px; text-transform:uppercase; letter-spacing:0.05em;}
  .modal-close-row{margin-top:22px; display:flex; justify-content:flex-end; gap:10px;}
  .btn-primary{
    background:linear-gradient(135deg, var(--cyan), var(--blue)); color:#00131a; border:none;
    padding:10px 20px; border-radius:9px; font-weight:800; font-size:13px; cursor:pointer;
    transition:transform .15s ease, box-shadow .15s ease;
  }
  .btn-primary:hover{transform:translateY(-1px); box-shadow:0 6px 20px rgba(63,214,255,0.35);}
  .btn-secondary{
    background:transparent; color:var(--text-1); border:1px solid var(--panel-border);
    padding:10px 20px; border-radius:9px; font-weight:700; font-size:13px; cursor:pointer;
  }
  .btn-secondary:hover{border-color:var(--cyan); color:var(--cyan);}

  /* start screen */
  .start-screen{
    min-height:88vh; display:flex; flex-direction:column; align-items:center; justify-content:center;
    text-align:center; gap:18px; padding:20px;
  }
  .start-screen .brand-mark{width:64px; height:64px; font-size:26px; border-radius:16px;}
  .start-title{font-size:34px; font-weight:800; letter-spacing:-0.01em;}
  .start-title span{color:var(--cyan);}
  .start-sub{font-size:14px; color:var(--text-1); max-width:480px; line-height:1.6;}
  .start-stats{display:flex; gap:22px; margin-top:6px; flex-wrap:wrap; justify-content:center;}
  .start-stat{
    background:var(--bg-2); border:1px solid var(--panel-border); border-radius:10px;
    padding:12px 18px; min-width:120px;
  }
  .start-stat .n{font-family:var(--mono); font-size:20px; color:var(--cyan); font-weight:700;}
  .start-stat .l{font-size:10.5px; color:var(--text-2); text-transform:uppercase; letter-spacing:0.06em; margin-top:2px;}
  .start-actions{display:flex; gap:12px; margin-top:10px;}

  /* end screen */
  .grade-circle{
    width:120px; height:120px; border-radius:50%; margin:0 auto 16px;
    display:flex; align-items:center; justify-content:center;
    font-size:48px; font-weight:800; font-family:var(--mono);
    border:4px solid var(--cyan); box-shadow:0 0 40px rgba(63,214,255,0.4);
    background:radial-gradient(circle, rgba(63,214,255,0.12), transparent 70%);
  }
  .end-summary-grid{
    display:grid; grid-template-columns:1fr 1fr; gap:8px 16px; margin:16px 0;
    font-size:12.5px;
  }
  .end-row{display:flex; justify-content:space-between; border-bottom:1px dashed var(--panel-border); padding:6px 0;}
  .end-row b{color:var(--text-0); font-family:var(--mono);}
  .end-narrative{
    background:var(--bg-2); border:1px solid var(--panel-border); border-radius:10px;
    padding:14px; font-size:13px; line-height:1.6; color:var(--text-1); margin-top:6px;
  }

  /* pause overlay */
  .pause-badge{
    font-size:13px; color:var(--text-1); text-align:center; margin-top:6px;
  }

  @keyframes pulseSoft{
    0%,100%{opacity:1;} 50%{opacity:0.6;}
  }

  /* responsive */
  @media (max-width: 1100px){
    .kpi-grid{grid-template-columns:repeat(4,1fr);}
    .main-grid{grid-template-columns:1fr;}
  }
  @media (max-width: 620px){
    .kpi-grid{grid-template-columns:repeat(2,1fr);}
    .topbar{flex-wrap:wrap; gap:10px;}
    .app{padding:12px;}
    .alert-actions{gap:6px;}
  }
</style>
</head>
<body>

<div class="app" id="app">

  <!-- ===================== START SCREEN ===================== -->
  <div class="start-screen" id="startScreen">
    <div class="brand-mark">CT</div>
    <div class="start-title">AI Supply Chain <span>Control Tower</span></div>
    <div class="start-sub">
      You're the new Head of Operations. For the next 3 minutes, alerts will hit your network in
      real time — port congestion, supplier delays, stockouts, breakdowns. Every call you make
      moves the numbers. Keep the network alive.
    </div>
    <div class="start-stats">
      <div class="start-stat"><div class="n">3:00</div><div class="l">Shift Length</div></div>
      <div class="start-stat"><div class="n">10</div><div class="l">Alert Types</div></div>
      <div class="start-stat"><div class="n">8</div><div class="l">Live KPIs</div></div>
    </div>
    <div class="start-actions">
      <button class="btn-primary" id="startBtn">Start Shift</button>
      <button class="btn-secondary" id="helpBtnStart">How to Play</button>
    </div>
  </div>

  <!-- ===================== GAME SCREEN ===================== -->
  <div id="gameScreen" class="hidden">

    <div class="topbar">
      <div class="brand">
        <div class="brand-mark">CT</div>
        <div class="brand-text">
          <h1>Control Tower</h1>
          <span>Live Operations Feed</span>
        </div>
      </div>
      <div class="top-actions">
        <button class="icon-btn active" id="soundBtn">🔊 Sound</button>
        <button class="icon-btn" id="pauseBtn">⏸ Pause</button>
        <button class="icon-btn" id="helpBtn">❔ Help</button>
        <div class="clock" id="clock">3:00</div>
      </div>
    </div>

    <div class="kpi-grid" id="kpiGrid"><!-- KPI cards injected by JS --></div>

    <div class="main-grid">
      <div class="panel">
        <div class="panel-head">
          <h2>Active Alerts</h2>
          <div class="count-pill" id="alertCount">0 open</div>
        </div>
        <div class="alert-feed" id="alertFeed">
          <div class="empty-state" id="emptyState">Network nominal. Standing by for the first alert…</div>
        </div>
      </div>

      <div class="panel">
        <div class="panel-head">
          <h2>Event Log</h2>
          <div class="count-pill" id="logCount">0 events</div>
        </div>
        <div class="log-list" id="logList"></div>
      </div>
    </div>
  </div>

  <!-- ===================== END SCREEN ===================== -->
  <div id="endOverlay" class="overlay hidden">
    <div class="modal" style="max-width:560px;">
      <div style="text-align:center;">
        <div style="font-size:11px; letter-spacing:0.12em; text-transform:uppercase; color:var(--text-2); margin-bottom:6px;">Shift Complete</div>
        <div class="grade-circle" id="gradeCircle">A</div>
        <div style="font-family:var(--mono); font-size:26px; color:var(--cyan); font-weight:800;" id="finalScore">0</div>
        <div style="font-size:11px; color:var(--text-2); text-transform:uppercase; letter-spacing:0.08em;">Final Score</div>
      </div>

      <div class="end-summary-grid" id="endSummaryGrid"></div>

      <div class="end-narrative" id="endNarrative"></div>

      <div class="modal-close-row">
        <button class="btn-secondary" id="helpBtnEnd">How to Play</button>
        <button class="btn-primary" id="playAgainBtn">Play Again</button>
      </div>
    </div>
  </div>

  <!-- ===================== PAUSE OVERLAY ===================== -->
  <div id="pauseOverlay" class="overlay hidden">
    <div class="modal" style="text-align:center; max-width:360px;">
      <h2>Shift Paused</h2>
      <p>Operations are frozen. Take a breath — the alerts will wait.</p>
      <div class="modal-close-row" style="justify-content:center;">
        <button class="btn-primary" id="resumeBtn">Resume Shift</button>
      </div>
    </div>
  </div>

  <!-- ===================== HELP MODAL ===================== -->
  <div id="helpOverlay" class="overlay hidden">
    <div class="modal">
      <h2>How to Run the Tower</h2>
      <p>Alerts will appear on the left as issues hit your supply chain. Each one shows its priority, business impact, and a countdown — if it expires unresolved, it auto-resolves badly.</p>
      <h3>Your Job</h3>
      <ul>
        <li>Read the alert and pick the action that best fits the situation.</li>
        <li>Fast, well-matched responses protect KPIs and raise your score.</li>
        <li>Mismatched or lazy responses (like Ignore) cost you.</li>
        <li>Some decisions have consequences that land a few seconds later — watch the log.</li>
      </ul>
      <h3>Priority Colors</h3>
      <ul>
        <li><b style="color:var(--red)">Critical</b> — resolve immediately, revenue at risk.</li>
        <li><b style="color:var(--orange)">High</b> — resolve soon.</li>
        <li><b style="color:var(--blue)">Medium</b> — manage when you can.</li>
      </ul>
      <h3>Your 8 KPIs</h3>
      <p>Service Level, Customer Satisfaction, Inventory Health, Transportation Efficiency, Operating Cost, Revenue Protected, Score, and the shift Timer. Keep the network humming for 3 minutes.</p>
      <div class="modal-close-row">
        <button class="btn-primary" id="closeHelpBtn">Got it</button>
      </div>
    </div>
  </div>

</div>

<script>
(function(){
  'use strict';

  /* ============================================================
     STATE
  ============================================================ */
  const SHIFT_SECONDS = 180;

  const state = {
    running:false,
    paused:false,
    soundOn:true,
    timeLeft:SHIFT_SECONDS,
    score:0,
    kpi:{
      service:92,
      satisfaction:88,
      inventory:85,
      transport:90,
      cost:40,        // lower is better (operating cost index)
      revenue:100      // % revenue protected
    },
    alerts:[],           // active alert objects
    resolved:0,
    correct:0,
    wrong:0,
    nextAlertId:1,
    spawnTimer:null,
    tickTimer:null,
    difficultyStage:0,
    logSeq:0
  };

  /* ============================================================
     CONTENT LIBRARY
  ============================================================ */
  const ALERT_TYPES = [
    {
      key:'port', icon:'🚢', title:'Port Congestion',
      desc:'Container backlog at the origin port is delaying 3 vessels carrying key inbound stock.',
      impact:'Inbound stock at risk, transportation efficiency dropping.',
      actions:[
        {label:'Reroute Trucks', quality:'ok', effects:{transport:+4, cost:+6, service:+2}},
        {label:'Approve Air Freight', quality:'good', effects:{transport:+8, cost:+14, service:+6, revenue:+3}},
        {label:'Use Backup Supplier', quality:'ok', effects:{inventory:+5, cost:+8}},
        {label:'Ignore', quality:'bad', effects:{transport:-10, service:-8, revenue:-6}},
        {label:'Delay Decision', quality:'delay', effects:{transport:-4}}
      ]
    },
    {
      key:'supplier', icon:'📦', title:'Supplier Delay',
      desc:'A tier-1 supplier confirms a 5-day slip on a critical component shipment.',
      impact:'Production risk if not resolved before buffer stock runs out.',
      actions:[
        {label:'Use Backup Supplier', quality:'good', effects:{inventory:+8, cost:+7, service:+5}},
        {label:'Expedite Shipment', quality:'ok', effects:{inventory:+4, cost:+9}},
        {label:'Transfer Inventory', quality:'ok', effects:{inventory:+5, transport:-2}},
        {label:'Ignore', quality:'bad', effects:{inventory:-10, service:-7}},
        {label:'Delay Decision', quality:'delay', effects:{inventory:-3}}
      ]
    },
    {
      key:'truck', icon:'🚛', title:'Truck Breakdown',
      desc:'A delivery truck broke down mid-route with a full load for 4 regional stores.',
      impact:'Last-mile delivery delayed, customer satisfaction exposed.',
      actions:[
        {label:'Reroute Trucks', quality:'good', effects:{transport:+7, satisfaction:+5, cost:+4}},
        {label:'Expedite Shipment', quality:'ok', effects:{transport:+4, cost:+6}},
        {label:'Approve Air Freight', quality:'ok', effects:{satisfaction:+6, cost:+12}},
        {label:'Ignore', quality:'bad', effects:{satisfaction:-9, transport:-6}},
        {label:'Delay Decision', quality:'delay', effects:{satisfaction:-3}}
      ]
    },
    {
      key:'stock', icon:'🏬', title:'Warehouse Running Out of Stock',
      desc:'Regional warehouse inventory has dropped below the safety threshold for top SKUs.',
      impact:'Stockouts likely within hours, service level exposed.',
      actions:[
        {label:'Transfer Inventory', quality:'good', effects:{inventory:+9, service:+6}},
        {label:'Increase Production', quality:'ok', effects:{inventory:+6, cost:+8}},
        {label:'Expedite Shipment', quality:'ok', effects:{inventory:+5, cost:+6}},
        {label:'Ignore', quality:'bad', effects:{service:-10, satisfaction:-6, revenue:-5}},
        {label:'Delay Decision', quality:'delay', effects:{inventory:-4}}
      ]
    },
    {
      key:'customs', icon:'🛃', title:'Customs Inspection',
      desc:'Random customs inspection is holding a high-value container at the border.',
      impact:'Clearance delay could ripple into downstream delivery commitments.',
      actions:[
        {label:'Expedite Shipment', quality:'good', effects:{transport:+6, cost:+5, service:+3}},
        {label:'Reroute Trucks', quality:'ok', effects:{transport:+3}},
        {label:'Approve Air Freight', quality:'ok', effects:{transport:+7, cost:+13}},
        {label:'Ignore', quality:'bad', effects:{transport:-8, revenue:-4}},
        {label:'Delay Decision', quality:'delay', effects:{transport:-3}}
      ]
    },
    {
      key:'demand', icon:'📈', title:'Demand Spike',
      desc:'A viral social post triggered a 3x demand spike for one SKU in the last hour.',
      impact:'Upside opportunity — but only if supply can keep up.',
      actions:[
        {label:'Increase Production', quality:'good', effects:{revenue:+10, inventory:-3, cost:+9}},
        {label:'Transfer Inventory', quality:'ok', effects:{revenue:+5, inventory:-2}},
        {label:'Approve Air Freight', quality:'ok', effects:{revenue:+6, cost:+11}},
        {label:'Ignore', quality:'bad', effects:{revenue:-9, satisfaction:-5}},
        {label:'Delay Decision', quality:'delay', effects:{revenue:-3}}
      ]
    },
    {
      key:'factory', icon:'🏭', title:'Factory Machine Failure',
      desc:'A key production line went down at your primary manufacturing facility.',
      impact:'Output drops, order fulfillment for the week is at risk.',
      actions:[
        {label:'Increase Production', quality:'ok', effects:{service:+3, cost:+10}},
        {label:'Use Backup Supplier', quality:'good', effects:{inventory:+7, service:+5, cost:+6}},
        {label:'Transfer Inventory', quality:'ok', effects:{inventory:+4}},
        {label:'Ignore', quality:'bad', effects:{service:-10, revenue:-7}},
        {label:'Delay Decision', quality:'delay', effects:{service:-4}}
      ]
    },
    {
      key:'weather', icon:'🌪️', title:'Weather Disruption',
      desc:'A storm system is shutting down a key transit corridor for the next 12 hours.',
      impact:'Multiple routes affected; on-time delivery at risk network-wide.',
      actions:[
        {label:'Reroute Trucks', quality:'good', effects:{transport:+8, cost:+5, satisfaction:+3}},
        {label:'Approve Air Freight', quality:'ok', effects:{transport:+6, cost:+13}},
        {label:'Delay Decision', quality:'delay', effects:{transport:-4}},
        {label:'Ignore', quality:'bad', effects:{transport:-11, satisfaction:-7}}
      ]
    },
    {
      key:'count', icon:'🔢', title:'Wrong Inventory Count',
      desc:'A cycle count audit found a major discrepancy in system vs physical stock.',
      impact:'Planning accuracy compromised until reconciled.',
      actions:[
        {label:'Transfer Inventory', quality:'ok', effects:{inventory:+3, cost:+3}},
        {label:'Use Backup Supplier', quality:'ok', effects:{inventory:+4, cost:+5}},
        {label:'Expedite Shipment', quality:'good', effects:{inventory:+7, service:+4}},
        {label:'Ignore', quality:'bad', effects:{inventory:-8, service:-5}},
        {label:'Delay Decision', quality:'delay', effects:{inventory:-3}}
      ]
    },
    {
      key:'damage', icon:'💥', title:'Damaged Shipment',
      desc:'Inbound quality check flagged water damage on a full pallet load.',
      impact:'Replacement needed to avoid downstream stockout and refunds.',
      actions:[
        {label:'Use Backup Supplier', quality:'good', effects:{inventory:+6, revenue:+4, cost:+6}},
        {label:'Expedite Shipment', quality:'ok', effects:{inventory:+4, cost:+7}},
        {label:'Approve Air Freight', quality:'ok', effects:{inventory:+5, cost:+12}},
        {label:'Ignore', quality:'bad', effects:{revenue:-8, satisfaction:-6}},
        {label:'Delay Decision', quality:'delay', effects:{revenue:-3}}
      ]
    }
  ];

  const PRIORITIES = ['critical','high','medium'];

  /* ============================================================
     DOM refs
  ============================================================ */
  const $ = id => document.getElementById(id);
  const startScreen = $('startScreen');
  const gameScreen = $('gameScreen');
  const kpiGrid = $('kpiGrid');
  const alertFeed = $('alertFeed');
  const emptyState = $('emptyState');
  const logList = $('logList');
  const clockEl = $('clock');
  const alertCountEl = $('alertCount');
  const logCountEl = $('logCount');
  const endOverlay = $('endOverlay');
  const pauseOverlay = $('pauseOverlay');
  const helpOverlay = $('helpOverlay');

  /* ============================================================
     KPI DEFINITIONS FOR RENDERING
  ============================================================ */
  const KPI_DEFS = [
    {key:'service', label:'Service Level', unit:'%', good:'high'},
    {key:'satisfaction', label:'Cust. Satisfaction', unit:'%', good:'high'},
    {key:'inventory', label:'Inventory Health', unit:'%', good:'high'},
    {key:'transport', label:'Transport Efficiency', unit:'%', good:'high'},
    {key:'cost', label:'Operating Cost', unit:'idx', good:'low'},
    {key:'revenue', label:'Revenue Protected', unit:'%', good:'high'},
    {key:'score', label:'Score', unit:'pts', good:'high', isScore:true},
    {key:'time', label:'Time Remaining', unit:'', good:'high', isTime:true}
  ];

  function buildKpiGrid(){
    kpiGrid.innerHTML = '';
    KPI_DEFS.forEach(def=>{
      const card = document.createElement('div');
      card.className = 'kpi-card' + (def.isScore ? ' kpi-score' : '');
      card.id = 'kpiCard-' + def.key;
      card.innerHTML = `
        <div class="kpi-label">${def.label}</div>
        <div class="kpi-value" id="kpiVal-${def.key}">--<span class="unit">${def.unit}</span></div>
        <div class="kpi-delta" id="kpiDelta-${def.key}"></div>
        ${def.isTime ? '' : `<div class="kpi-bar"><div class="kpi-bar-fill" id="kpiBar-${def.key}"></div></div>`}
      `;
      kpiGrid.appendChild(card);
    });
  }

  function barColor(key, value){
    if(key==='cost'){
      if(value<=35) return 'var(--green)';
      if(value<=65) return 'var(--orange)';
      return 'var(--red)';
    }
    if(value>=75) return 'var(--green)';
    if(value>=45) return 'var(--orange)';
    return 'var(--red)';
  }

  function renderKpis(deltas){
    deltas = deltas || {};
    KPI_DEFS.forEach(def=>{
      const valEl = $('kpiVal-'+def.key);
      const deltaEl = $('kpiDelta-'+def.key);
      const barEl = $('kpiBar-'+def.key);
      if(!valEl) return;

      let display;
      if(def.isTime){
        display = formatTime(state.timeLeft);
      } else if(def.isScore){
        display = Math.max(0, Math.round(state.score));
      } else {
        const v = Math.max(0, Math.min(150, state.kpi[def.key]));
        display = Math.round(v);
      }
      valEl.innerHTML = display + `<span class="unit">${def.unit}</span>`;

      if(barEl && !def.isTime){
        const v = def.isScore ? Math.min(100, Math.max(0,(state.score/2000)*100)) : Math.max(0, Math.min(100, state.kpi[def.key]));
        barEl.style.width = v + '%';
        barEl.style.background = def.isScore ? 'linear-gradient(90deg, var(--cyan), var(--blue))' : barColor(def.key, state.kpi[def.key]);
      }

      const d = deltas[def.key];
      if(d){
        deltaEl.textContent = (d>0?'+':'') + Math.round(d) + (def.isScore? ' pts':' ');
        deltaEl.className = 'kpi-delta ' + (def.key==='cost' ? (d>0?'down':'up') : (d>0?'up':'down'));
        const card = $('kpiCard-'+def.key);
        card.classList.remove('kpi-flash'); void card.offsetWidth; card.classList.add('kpi-flash');
        setTimeout(()=>{ if(deltaEl) deltaEl.textContent=''; }, 2200);
      }
    });
  }

  function formatTime(sec){
    const m = Math.floor(sec/60);
    const s = sec % 60;
    return m + ':' + String(s).padStart(2,'0');
  }

  /* ============================================================
     LOGGING
  ============================================================ */
  function log(msg, type){
    type = type || 'neutral';
    state.logSeq++;
    const item = document.createElement('div');
    item.className = 'log-item ' + type;
    const t = formatTime(state.timeLeft);
    item.innerHTML = `<span class="log-time">[${t}]</span>${msg}`;
    logList.appendChild(item);
    logCountEl.textContent = state.logSeq + ' events';
    // cap log size
    while(logList.children.length > 80){ logList.removeChild(logList.firstChild); }
  }

  /* ============================================================
     ALERT SPAWNING
  ============================================================ */
  function randPick(arr){ return arr[Math.floor(Math.random()*arr.length)]; }

  function currentAlertDuration(){
    // shrink duration as difficulty increases
    const base = 26;
    const reduction = state.difficultyStage * 2.5;
    return Math.max(14, base - reduction);
  }

  function spawnAlert(){
    if(!state.running || state.paused) return;
    if(state.alerts.length >= 6) return; // cap simultaneous alerts

    const type = randPick(ALERT_TYPES);
    const priority = randPick(PRIORITIES);
    const duration = currentAlertDuration() + (priority==='critical' ? -4 : priority==='medium' ? 4 : 0);
    const id = state.nextAlertId++;

    const alert = {
      id, type, priority,
      timeLeft: Math.max(10, duration),
      totalTime: Math.max(10, duration),
      resolving:false
    };
    state.alerts.push(alert);
    renderAlerts();
    log(`${type.icon} New alert: <b>${type.title}</b> (${priority} priority)`, 'spawn');
  }

  function scheduleNextSpawn(){
    if(!state.running) return;
    // spawn interval shrinks as time passes -> more alerts later
    const elapsed = SHIFT_SECONDS - state.timeLeft;
    const stage = Math.min(4, Math.floor(elapsed/35));
    state.difficultyStage = stage;
    const baseInterval = 6000 - stage*900; // ms
    const jitter = Math.random()*1500;
    const interval = Math.max(1500, baseInterval + jitter);
    state.spawnTimer = setTimeout(()=>{
      spawnAlert();
      scheduleNextSpawn();
    }, interval);
  }

  /* ============================================================
     RENDER ALERTS
  ============================================================ */
  function renderAlerts(){
    alertCountEl.textContent = state.alerts.length + ' open';
    emptyState.classList.toggle('hidden', state.alerts.length>0);

    // remove DOM nodes for alerts no longer present, then rebuild present ones
    const existingIds = new Set(state.alerts.map(a=>a.id));
    Array.from(alertFeed.children).forEach(node=>{
      if(node.id && node.id.startsWith('alert-')){
        const id = parseInt(node.id.replace('alert-',''));
        if(!existingIds.has(id) && !node.classList.contains('resolving')) node.remove();
      }
    });

    state.alerts.forEach(a=>{
      let node = $('alert-'+a.id);
      if(!node){
        node = document.createElement('div');
        node.id = 'alert-'+a.id;
        node.className = 'alert-card priority-'+a.priority + (a.priority==='critical' ? ' pulse-crit':'');
        alertFeed.appendChild(node);
      }
      const pct = Math.max(0, (a.timeLeft/a.totalTime)*100);
      const critTime = a.timeLeft <= 5;
      node.innerHTML = `
        <div class="alert-top">
          <div class="alert-title-wrap">
            <span class="alert-icon">${a.type.icon}</span>
            <span class="alert-title">${a.type.title}</span>
          </div>
          <span class="badge priority-${a.priority}">${a.priority}</span>
        </div>
        <div class="alert-desc">${a.type.desc}</div>
        <div class="alert-meta">
          <span>⏱ <span class="alert-timer ${critTime?'crit':''}">${a.timeLeft}s</span></span>
          <span>⚠ <b>Impact:</b> ${a.type.impact}</span>
        </div>
        <div class="alert-actions" id="actions-${a.id}"></div>
        <div class="alert-timerbar"><div class="alert-timerbar-fill" style="width:${pct}%"></div></div>
      `;
      const actionsWrap = $('actions-'+a.id);
      a.type.actions.forEach((act, idx)=>{
        const btn = document.createElement('button');
        btn.className = 'action-btn' + (act.label==='Ignore'?' ignore':'') + (act.label==='Delay Decision'?' delay':'');
        btn.textContent = act.label;
        btn.onclick = ()=> resolveAlert(a.id, idx);
        actionsWrap.appendChild(btn);
      });
    });
  }

  /* ============================================================
     RESOLVE / TICK ALERTS
  ============================================================ */
  function applyEffects(effects, scoreDelta){
    const deltas = {};
    Object.keys(effects).forEach(k=>{
      state.kpi[k] = clampKpi(k, state.kpi[k] + effects[k]);
      deltas[k] = effects[k];
    });
    if(scoreDelta){
      state.score = Math.max(0, state.score + scoreDelta);
      deltas.score = scoreDelta;
    }
    renderKpis(deltas);
  }

  function clampKpi(key, v){
    if(key==='cost') return Math.max(0, Math.min(150, v));
    return Math.max(0, Math.min(100, v));
  }

  function resolveAlert(id, actionIdx){
    const alert = state.alerts.find(a=>a.id===id);
    if(!alert || alert.resolving) return;
    const action = alert.type.actions[actionIdx];
    alert.resolving = true;

    const node = $('alert-'+id);
    if(node) node.classList.add('resolving');

    let scoreDelta = 0;
    let logType = 'neutral';
    let verb = '';

    if(action.quality==='good'){
      scoreDelta = 80 + Math.round(alert.timeLeft*1.2);
      state.correct++;
      logType='good'; verb='Resolved well';
    } else if(action.quality==='ok'){
      scoreDelta = 35 + Math.round(alert.timeLeft*0.5);
      state.correct++;
      logType='good'; verb='Resolved';
    } else if(action.quality==='bad'){
      scoreDelta = -40;
      state.wrong++;
      logType='bad'; verb='Ignored';
    } else if(action.quality==='delay'){
      scoreDelta = -10;
      logType='neutral'; verb='Delayed';
      // schedule a delayed extra consequence
      setTimeout(()=>{
        if(!state.running) return;
        const followUp = {};
        Object.keys(action.effects).forEach(k=> followUp[k] = Math.round(action.effects[k]*1.5));
        applyEffects(followUp, -15);
        log(`⏳ Delayed fallout from <b>${alert.type.title}</b> hits the network.`, 'bad');
      }, 4000);
    }

    applyEffects(action.effects, scoreDelta);
    log(`${alert.type.icon} <b>${alert.type.title}</b> — ${verb} via "${action.label}" (${scoreDelta>=0?'+':''}${scoreDelta} pts)`, logType);

    state.resolved++;

    setTimeout(()=>{
      state.alerts = state.alerts.filter(a=>a.id!==id);
      if(node) node.remove();
      renderAlerts();
    }, 420);
  }

  function autoExpireAlert(alert){
    alert.resolving = true;
    const node = $('alert-'+alert.id);
    if(node) node.classList.add('resolving');

    const penalty = alert.priority==='critical' ? -55 : alert.priority==='high' ? -35 : -18;
    const effects = alert.priority==='critical'
      ? {service:-9, satisfaction:-7, revenue:-6}
      : alert.priority==='high'
      ? {service:-5, satisfaction:-4}
      : {service:-2};

    applyEffects(effects, penalty);
    state.wrong++;
    log(`${alert.type.icon} <b>${alert.type.title}</b> expired unresolved — network took the hit (${penalty} pts)`, 'bad');

    setTimeout(()=>{
      state.alerts = state.alerts.filter(a=>a.id!==alert.id);
      if(node) node.remove();
      renderAlerts();
    }, 420);
  }

  /* ============================================================
     MAIN TICK (1s)
  ============================================================ */
  function tick(){
    if(!state.running || state.paused) return;

    state.timeLeft--;
    clockEl.textContent = formatTime(state.timeLeft);
    clockEl.classList.toggle('warn', state.timeLeft<=60 && state.timeLeft>20);
    clockEl.classList.toggle('crit', state.timeLeft<=20);

    // countdown alerts
    state.alerts.forEach(a=>{
      if(a.resolving) return;
      a.timeLeft--;
    });
    const expired = state.alerts.filter(a=>!a.resolving && a.timeLeft<=0);
    expired.forEach(autoExpireAlert);

    renderAlerts();
    renderKpis();

    if(state.timeLeft<=0){
      endShift();
      return;
    }
    state.tickTimer = setTimeout(tick, 1000);
  }

  /* ============================================================
     START / END / RESET
  ============================================================ */
  function startGame(){
    // reset state
    state.running = true;
    state.paused = false;
    state.timeLeft = SHIFT_SECONDS;
    state.score = 0;
    state.kpi = {service:92, satisfaction:88, inventory:85, transport:90, cost:40, revenue:100};
    state.alerts = [];
    state.resolved = 0;
    state.correct = 0;
    state.wrong = 0;
    state.nextAlertId = 1;
    state.difficultyStage = 0;
    state.logSeq = 0;

    logList.innerHTML = '';
    alertFeed.innerHTML = '';
    alertFeed.appendChild(emptyState);
    buildKpiGrid();
    renderKpis();
    clockEl.textContent = formatTime(state.timeLeft);
    clockEl.classList.remove('warn','crit');

    startScreen.classList.add('hidden');
    gameScreen.classList.remove('hidden');
    endOverlay.classList.add('hidden');

    log('🟢 Shift started. Network monitoring is live.', 'good');

    clearTimeout(state.spawnTimer);
    clearTimeout(state.tickTimer);
    // first alert appears quickly to hook the player
    state.spawnTimer = setTimeout(()=>{ spawnAlert(); scheduleNextSpawn(); }, 1800);
    state.tickTimer = setTimeout(tick, 1000);
  }

  function computeGrade(){
    const s = state.score;
    if(s>=1600) return 'A+';
    if(s>=1200) return 'A';
    if(s>=800) return 'B';
    if(s>=450) return 'C';
    return 'D';
  }

  const NARRATIVES = {
    'A+':"Flawless shift. The network barely felt the disruptions — every call was fast, sharp, and cost-aware. This is what a world-class control tower looks like.",
    'A':"Strong command of the floor. Most fires were caught early and handled well, with only minor drag on cost and satisfaction.",
    'B':"Solid, steady operations. You kept things mostly under control, but a few slow calls let avoidable damage through.",
    'C':"A rough shift. Too many alerts were delayed or ignored, and the network absorbed damage that better triage would have prevented.",
    'D':"The tower lost the thread. Alerts piled up faster than they were cleared, and KPIs paid the price across the board."
  };

  function endShift(){
    state.running = false;
    clearTimeout(state.spawnTimer);
    clearTimeout(state.tickTimer);

    const grade = computeGrade();
    $('gradeCircle').textContent = grade;
    $('finalScore').textContent = Math.round(state.score) + ' pts';

    const gradeColor = {'A+':'var(--green)','A':'var(--green)','B':'var(--blue)','C':'var(--orange)','D':'var(--red)'}[grade];
    $('gradeCircle').style.borderColor = gradeColor;
    $('gradeCircle').style.color = gradeColor;
    $('gradeCircle').style.boxShadow = `0 0 40px ${gradeColor}66`;

    const rows = [
      ['Service Level', Math.round(state.kpi.service)+'%'],
      ['Cust. Satisfaction', Math.round(state.kpi.satisfaction)+'%'],
      ['Inventory Health', Math.round(state.kpi.inventory)+'%'],
      ['Transport Efficiency', Math.round(state.kpi.transport)+'%'],
      ['Operating Cost Index', Math.round(state.kpi.cost)],
      ['Revenue Protected', Math.round(state.kpi.revenue)+'%'],
      ['Alerts Resolved', state.resolved],
      ['Correct Decisions', state.correct],
      ['Wrong Decisions', state.wrong],
      ['Final Grade', grade]
    ];
    $('endSummaryGrid').innerHTML = rows.map(r=>`<div class="end-row"><span>${r[0]}</span><b>${r[1]}</b></div>`).join('');
    $('endNarrative').textContent = NARRATIVES[grade];

    log('🔴 Shift ended. Final report generated.', 'neutral');
    endOverlay.classList.remove('hidden');
  }

  /* ============================================================
     PAUSE / RESUME / SOUND / HELP
  ============================================================ */
  function togglePause(){
    if(!state.running) return;
    state.paused = !state.paused;
    $('pauseBtn').textContent = state.paused ? '▶ Resume' : '⏸ Pause';
    pauseOverlay.classList.toggle('hidden', !state.paused);
    if(!state.paused){
      state.tickTimer = setTimeout(tick, 1000);
    }
  }

  function toggleSound(){
    state.soundOn = !state.soundOn;
    const btn = $('soundBtn');
    btn.textContent = state.soundOn ? '🔊 Sound' : '🔇 Muted';
    btn.classList.toggle('active', state.soundOn);
  }

  function openHelp(){ helpOverlay.classList.remove('hidden'); }
  function closeHelp(){ helpOverlay.classList.add('hidden'); }

  /* ============================================================
     EVENT WIRING
  ============================================================ */
  $('startBtn').addEventListener('click', startGame);
  $('helpBtnStart').addEventListener('click', openHelp);
  $('helpBtn').addEventListener('click', openHelp);
  $('helpBtnEnd').addEventListener('click', openHelp);
  $('closeHelpBtn').addEventListener('click', closeHelp);
  $('pauseBtn').addEventListener('click', togglePause);
  $('resumeBtn').addEventListener('click', togglePause);
  $('soundBtn').addEventListener('click', toggleSound);
  $('playAgainBtn').addEventListener('click', startGame);

  // init KPI grid shell before start (for consistent layout, though hidden)
  buildKpiGrid();

})();
</script>
</body>
</html>
