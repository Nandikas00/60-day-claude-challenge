# Today I created an AI-Powered Adaptive Interview Defense Simulator using claude :

📚 Key Learnings :
- Learned how AI can extract key claims from resumes and project descriptions for interview preparation.
- Understood the importance of validating every technical claim with supporting knowledge and real examples.
- Explored prompt engineering techniques to generate adaptive follow-up interview questions.
- Gained experience designing AI workflows that simulate realistic interviewer behavior instead of simple Q&A.
- Learned how structured prompts can assess confidence, technical depth, architecture decisions, and problem-solving ability.
- Improved understanding of converting static resume content into interactive interview simulations.
- Practiced building user-focused interfaces for uploading resumes and generating personalized interview defense scenarios.
- Discovered how AI can identify weak or unsupported claims, helping users prepare stronger and more credible interview responses.
- Learned the value of adaptive questioning to uncover knowledge gaps and encourage deeper technical explanations.
- Enhanced skills in creating practical AI applications that combine document analysis, reasoning, and personalized coaching.

## Output Screenshots :
<img width="871" height="873" alt="Screenshot (687)" src="https://github.com/user-attachments/assets/e969c87c-f61f-46a7-98f5-e58850a7ccb5" />
<img width="1052" height="870" alt="Screenshot (686)" src="https://github.com/user-attachments/assets/859d28bc-a350-4997-8a00-82ad7c7d5eff" />

### HTML File :

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Defend Your Experience — The Dossier</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,450;0,9..144,600;1,9..144,450&family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,500;1,6..72,400&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --paper:#F6F2E9;
    --paper-raised:#FBF8F1;
    --ink:#241F19;
    --ink-soft:#5A5245;
    --hairline:#D9D0BC;
    --burgundy:#7C2F2B;
    --burgundy-soft:#A9524B;
    --sage:#4F5C46;
    --gold:#B08A4E;
    --danger:#8C3A2F;
    --shadow: 0 1px 2px rgba(36,31,25,0.06), 0 8px 24px rgba(36,31,25,0.06);
    --radius: 3px;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:
      radial-gradient(ellipse at top left, rgba(176,138,78,0.06), transparent 45%),
      var(--paper);
    color:var(--ink);
    font-family:'Newsreader', Georgia, serif;
    font-size:17px;
    line-height:1.55;
    min-height:100vh;
  }
  ::selection{ background: rgba(124,47,43,0.18); }
  h1,h2,h3,.display{
    font-family:'Fraunces', Georgia, serif;
    font-weight:450;
    letter-spacing:-0.01em;
    color:var(--ink);
    margin:0;
  }
  .mono{ font-family:'IBM Plex Mono', monospace; letter-spacing:0.02em; }
  .eyebrow{
    font-family:'IBM Plex Mono', monospace;
    font-size:11px;
    letter-spacing:0.14em;
    text-transform:uppercase;
    color:var(--ink-soft);
  }
  a{color:inherit;}
  button{font-family:inherit;}
  :focus-visible{ outline:2px solid var(--burgundy); outline-offset:2px; }

  /* ---------- layout shell ---------- */
  #app{ max-width:920px; margin:0 auto; padding:0 24px 120px; }
  header.masthead{
    padding:38px 0 22px;
    border-bottom:2px solid var(--ink);
    margin-bottom:36px;
    display:flex; justify-content:space-between; align-items:flex-end; gap:16px; flex-wrap:wrap;
  }
  header.masthead .title-block h1{ font-size:32px; }
  header.masthead .title-block .eyebrow{ margin-bottom:6px; }
  header.masthead .status{ text-align:right; }
  header.masthead .status .mono{ font-size:12px; color:var(--ink-soft); }

  .screen{ animation: fadein .5s ease both; }
  @keyframes fadein{ from{opacity:0; transform:translateY(6px);} to{opacity:1; transform:none;} }
  @media (prefers-reduced-motion: reduce){ .screen{animation:none;} }

  .hidden{ display:none !important; }

  /* ---------- buttons ---------- */
  .btn{
    display:inline-flex; align-items:center; gap:8px;
    padding:12px 22px;
    border:1px solid var(--ink);
    background:var(--ink);
    color:var(--paper);
    border-radius:var(--radius);
    font-family:'IBM Plex Mono', monospace;
    font-size:13px;
    letter-spacing:0.03em;
    cursor:pointer;
    transition:transform .15s ease, background .15s ease;
  }
  .btn:hover{ background:var(--burgundy); border-color:var(--burgundy); }
  .btn:active{ transform:translateY(1px); }
  .btn.secondary{
    background:transparent; color:var(--ink); border-color:var(--hairline);
  }
  .btn.secondary:hover{ border-color:var(--ink); background:transparent; color:var(--ink); }
  .btn.danger{ background:transparent; color:var(--danger); border-color:var(--danger); }
  .btn.danger:hover{ background:var(--danger); color:var(--paper); }
  .btn[disabled]{ opacity:0.45; cursor:not-allowed; }
  .btn-row{ display:flex; gap:12px; flex-wrap:wrap; margin-top:22px; }

  /* ---------- intro / upload screen ---------- */
  .lede{ font-size:19px; color:var(--ink-soft); max-width:64ch; margin-bottom:8px; }
  .lede strong{ color:var(--ink); font-weight:500; }

  .dropzone{
    margin-top:28px;
    border:1.5px dashed var(--hairline);
    border-radius:var(--radius);
    background:var(--paper-raised);
    padding:40px 28px;
    text-align:center;
    transition: border-color .2s ease, background .2s ease;
  }
  .dropzone.dragover{ border-color:var(--burgundy); background:#FBF3EC; }
  .dropzone .icon{ font-size:28px; margin-bottom:10px; opacity:0.7; }
  .dropzone input[type=file]{ display:none; }
  .dropzone .file-label{
    text-decoration:underline;
    text-underline-offset:3px;
    cursor:pointer;
    color:var(--burgundy);
  }
  .dropzone .filename{ margin-top:14px; font-family:'IBM Plex Mono',monospace; font-size:12.5px; color:var(--sage); }

  textarea.pastebox{
    width:100%; margin-top:16px;
    min-height:160px;
    background:var(--paper-raised);
    border:1px solid var(--hairline);
    border-radius:var(--radius);
    padding:16px;
    font-family:'Newsreader', serif;
    font-size:15px;
    color:var(--ink);
    resize:vertical;
  }
  .or-divider{ display:flex; align-items:center; gap:12px; margin:22px 0 4px; color:var(--ink-soft); }
  .or-divider::before,.or-divider::after{ content:''; flex:1; height:1px; background:var(--hairline); }
  .or-divider span{ font-family:'IBM Plex Mono',monospace; font-size:11px; letter-spacing:0.1em; text-transform:uppercase; }

  /* MCQ */
  .mcq-group{ margin:26px 0; }
  .mcq-q{ font-family:'Fraunces',serif; font-size:20px; margin-bottom:14px; }
  .mcq-options{ display:grid; gap:10px; }
  .mcq-opt{
    display:flex; gap:12px; align-items:flex-start;
    border:1px solid var(--hairline);
    border-radius:var(--radius);
    padding:14px 16px;
    background:var(--paper-raised);
    cursor:pointer;
    transition:border-color .15s ease, background .15s ease;
  }
  .mcq-opt:hover{ border-color:var(--gold); }
  .mcq-opt.selected{ border-color:var(--burgundy); background:#FBF3EC; }
  .mcq-opt .letter{
    font-family:'IBM Plex Mono',monospace; font-size:12px;
    width:22px; height:22px; flex:none;
    border:1px solid var(--ink-soft); border-radius:50%;
    display:flex; align-items:center; justify-content:center;
    color:var(--ink-soft);
  }
  .mcq-opt.selected .letter{ background:var(--burgundy); border-color:var(--burgundy); color:var(--paper); }
  .mcq-opt .opt-text{ font-size:15.5px; }
  .mcq-opt .opt-sub{ display:block; font-size:12.5px; color:var(--ink-soft); margin-top:2px; }

  /* ---------- claims extraction screen ---------- */
  .claim-card{
    border:1px solid var(--hairline);
    background:var(--paper-raised);
    border-radius:var(--radius);
    padding:18px 20px;
    margin-bottom:12px;
    display:flex; gap:16px; align-items:flex-start;
  }
  .claim-card .tag{
    font-family:'IBM Plex Mono',monospace; font-size:10.5px; letter-spacing:0.08em; text-transform:uppercase;
    color:var(--gold); border:1px solid var(--gold); border-radius:2px; padding:2px 7px; flex:none; margin-top:3px;
  }
  .claim-card .txt{ font-size:15.5px; }
  .claim-card .src{ font-size:12px; color:var(--ink-soft); margin-top:4px; font-family:'IBM Plex Mono',monospace; }

  .loading-block{ text-align:center; padding:60px 10px; }
  .loading-block .spinner{
    width:34px; height:34px; margin:0 auto 18px;
    border:2px solid var(--hairline); border-top-color:var(--burgundy);
    border-radius:50%; animation:spin 0.9s linear infinite;
  }
  @keyframes spin{ to{ transform:rotate(360deg); } }
  .loading-block .msg{ font-family:'IBM Plex Mono',monospace; font-size:12.5px; color:var(--ink-soft); }

  /* ---------- interview screen ---------- */
  .interview-grid{ display:grid; grid-template-columns: 1fr 260px; gap:32px; align-items:start; }
  @media (max-width:800px){ .interview-grid{ grid-template-columns:1fr; } .sidebar{ order:-1; } }

  .progress-bar-wrap{ margin-bottom:26px; }
  .progress-bar{ height:4px; background:var(--hairline); border-radius:2px; overflow:hidden; }
  .progress-bar-fill{ height:100%; background:var(--burgundy); transition:width .4s ease; }
  .progress-label{ display:flex; justify-content:space-between; margin-top:8px; font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--ink-soft); }

  .claim-under-review{
    border-left:3px solid var(--burgundy);
    padding:4px 0 4px 16px;
    margin-bottom:22px;
  }
  .claim-under-review .eyebrow{ margin-bottom:4px; }
  .claim-under-review .claim-text{ font-family:'Fraunces',serif; font-size:21px; line-height:1.35; }

  .transcript{ display:flex; flex-direction:column; gap:16px; margin-bottom:22px; }
  .bubble{ max-width:100%; padding:14px 18px; border-radius:var(--radius); font-size:15.5px; }
  .bubble.interviewer{
    background:var(--paper-raised); border:1px solid var(--hairline); border-left:3px solid var(--ink);
  }
  .bubble.interviewer .who{ font-family:'IBM Plex Mono',monospace; font-size:10.5px; text-transform:uppercase; letter-spacing:0.08em; color:var(--ink-soft); display:block; margin-bottom:6px; }
  .bubble.user{
    background:#fff; border:1px solid var(--hairline); border-left:3px solid var(--sage); margin-left:auto; max-width:92%;
  }
  .bubble.user .who{ font-family:'IBM Plex Mono',monospace; font-size:10.5px; text-transform:uppercase; letter-spacing:0.08em; color:var(--sage); display:block; margin-bottom:6px; }
  .bubble.system-note{
    font-family:'IBM Plex Mono',monospace; font-size:12px; color:var(--ink-soft); text-align:center; padding:6px;
  }

  .answer-box{ margin-top:10px; }
  textarea.answer-input{
    width:100%; min-height:110px;
    border:1px solid var(--hairline); border-radius:var(--radius);
    background:var(--paper-raised);
    padding:14px 16px;
    font-family:'Newsreader',serif; font-size:15.5px;
    resize:vertical;
  }
  textarea.answer-input:focus{ border-color:var(--burgundy); }
  .answer-controls{ display:flex; justify-content:space-between; align-items:center; margin-top:10px; }
  .char-count{ font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--ink-soft); }

  .sidebar .panel{
    border:1px solid var(--hairline); background:var(--paper-raised); border-radius:var(--radius); padding:18px; margin-bottom:16px;
  }
  .sidebar .panel h3{ font-size:14px; font-family:'IBM Plex Mono',monospace; text-transform:uppercase; letter-spacing:0.08em; margin-bottom:12px; color:var(--ink-soft); }
  .confidence-row{ display:flex; align-items:center; gap:10px; margin-bottom:9px; font-size:13px; }
  .confidence-row .dot{ width:8px; height:8px; border-radius:50%; flex:none; }
  .confidence-row .label{ flex:1; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; }
  .confidence-row .pct{ font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--ink-soft); }
  .dot.defended{ background:var(--sage); }
  .dot.shaky{ background:var(--gold); }
  .dot.unverified{ background:var(--danger); }
  .dot.pending{ background:var(--hairline); border:1px solid var(--ink-soft); }

  .verdict-flash{
    display:inline-block; margin-top:10px; padding:6px 12px; border-radius:2px;
    font-family:'IBM Plex Mono',monospace; font-size:11px; letter-spacing:0.06em; text-transform:uppercase;
  }
  .verdict-flash.defended{ background:rgba(79,92,70,0.14); color:var(--sage); }
  .verdict-flash.shaky{ background:rgba(176,138,78,0.16); color:var(--gold); }
  .verdict-flash.unverified{ background:rgba(140,58,47,0.14); color:var(--danger); }

  .stamp{
    display:inline-block; border:2px solid currentColor; border-radius:4px; padding:2px 10px;
    font-family:'IBM Plex Mono',monospace; font-size:11px; letter-spacing:0.08em; text-transform:uppercase;
    transform:rotate(-3deg);
  }

  /* ---------- report screen ---------- */
  .report-hero{ text-align:center; padding:30px 0 10px; }
  .report-hero .score{ font-family:'Fraunces',serif; font-size:74px; line-height:1; }
  .report-hero .score-label{ font-family:'IBM Plex Mono',monospace; font-size:12px; letter-spacing:0.1em; text-transform:uppercase; color:var(--ink-soft); margin-top:8px; }

  .report-section{ margin:36px 0; }
  .report-section h2{ font-size:22px; border-bottom:1px solid var(--hairline); padding-bottom:10px; margin-bottom:16px; }

  .bar-row{ display:grid; grid-template-columns: 200px 1fr 44px; align-items:center; gap:12px; margin-bottom:12px; font-size:13.5px; }
  .bar-row .name{ overflow:hidden; text-overflow:ellipsis; white-space:nowrap; }
  .bar-track{ height:10px; background:var(--hairline); border-radius:5px; overflow:hidden; }
  .bar-fill{ height:100%; border-radius:5px; }
  .bar-row .pct{ font-family:'IBM Plex Mono',monospace; font-size:11.5px; text-align:right; color:var(--ink-soft); }

  .report-card{
    border:1px solid var(--hairline); background:var(--paper-raised); border-radius:var(--radius);
    padding:20px 22px; margin-bottom:14px;
  }
  .report-card .head{ display:flex; justify-content:space-between; align-items:flex-start; gap:12px; margin-bottom:10px; }
  .report-card .claim-txt{ font-family:'Fraunces',serif; font-size:17.5px; line-height:1.4; }
  .report-card .feedback{ font-size:15px; color:var(--ink); }
  .report-card .rec{ margin-top:10px; padding-top:10px; border-top:1px dashed var(--hairline); font-size:14px; color:var(--sage); }
  .report-card .rec strong{ font-family:'IBM Plex Mono',monospace; font-size:10.5px; text-transform:uppercase; letter-spacing:0.06em; display:block; margin-bottom:4px; color:var(--ink-soft); }

  .empty-state{ text-align:center; padding:70px 20px; color:var(--ink-soft); }
  .empty-state .glyph{ font-size:34px; margin-bottom:14px; }

  footer.byline{ text-align:center; margin-top:60px; padding-top:20px; border-top:1px solid var(--hairline); font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--ink-soft); }

  .toast{
    position:fixed; bottom:24px; left:50%; transform:translateX(-50%);
    background:var(--ink); color:var(--paper); padding:12px 20px; border-radius:var(--radius);
    font-family:'IBM Plex Mono',monospace; font-size:13px; box-shadow:var(--shadow); z-index:999;
    opacity:0; pointer-events:none; transition:opacity .3s ease, transform .3s ease;
  }
  .toast.show{ opacity:1; transform:translateX(-50%) translateY(-6px); }

  .inline-note{
    font-size:13px; color:var(--ink-soft); background:rgba(176,138,78,0.1); border:1px solid var(--gold);
    border-radius:var(--radius); padding:10px 14px; margin-top:14px;
  }
</style>
</head>
<body>
<div id="app">

  <header class="masthead">
    <div class="title-block">
      <div class="eyebrow">The Dossier — Defense Preparation File</div>
      <h1>Defend Your Experience</h1>
    </div>
    <div class="status">
      <div class="mono" id="statusLine">no case file open</div>
      <div class="mono" id="statusSub" style="margin-top:4px;"></div>
    </div>
  </header>

  <!-- ===================== SCREEN: INTRO / UPLOAD ===================== -->
  <section id="screen-intro" class="screen">
    <p class="lede">This isn't a resume reviewer. It's a skeptical interviewer who reads every claim you've made about yourself — <strong>every "led," "built," "improved," and "architected"</strong> — and won't let any of it go unquestioned. Your job is to defend it, out loud, until it holds.</p>
    <p class="lede" style="font-size:15.5px;">Upload or paste the document describing your experience. It can be a resume, LinkedIn export, project write-up, or performance review. Everything that follows is generated from your own words — nothing here is templated.</p>

    <div class="dropzone" id="dropzone">
      <div class="icon">✒</div>
      <div>Drop a file here, or <label class="file-label" for="fileInput">choose a file</label></div>
      <div style="font-size:12.5px;color:var(--ink-soft);margin-top:6px;">.txt or .pdf-as-text — plain text works best</div>
      <input type="file" id="fileInput" accept=".txt,.md,text/plain">
      <div class="filename" id="filename"></div>
    </div>

    <div class="or-divider"><span>or paste it directly</span></div>
    <textarea class="pastebox" id="pasteBox" placeholder="Paste your resume, bio, or project description here..."></textarea>

    <div id="introMcqHost"></div>

    <div class="btn-row">
      <button class="btn" id="btnExtract">Open the case file →</button>
      <button class="btn secondary hidden" id="btnResume">Resume last session</button>
    </div>
    <div class="inline-note hidden" id="introNote"></div>
  </section>

  <!-- ===================== SCREEN: EXTRACTING ===================== -->
  <section id="screen-extracting" class="screen hidden">
    <div class="loading-block">
      <div class="spinner"></div>
      <div class="msg" id="extractMsg">Reading the file...</div>
    </div>
  </section>

  <!-- ===================== SCREEN: CLAIMS REVIEW ===================== -->
  <section id="screen-claims" class="screen hidden">
    <div class="eyebrow" style="margin-bottom:6px;">Exhibits identified</div>
    <h2 style="font-size:26px;margin-bottom:10px;">Every claim you'll need to defend</h2>
    <p class="lede" style="font-size:15.5px;">These were pulled directly from your document. Nothing generic — each one is something you specifically asserted about yourself.</p>
    <div id="claimsList" style="margin-top:22px;"></div>
    <div class="btn-row">
      <button class="btn" id="btnBeginInterview">Begin the interview →</button>
      <button class="btn secondary" id="btnBackToIntro">Start over</button>
    </div>
  </section>

  <!-- ===================== SCREEN: INTERVIEW ===================== -->
  <section id="screen-interview" class="screen hidden">
    <div class="progress-bar-wrap">
      <div class="progress-bar"><div class="progress-bar-fill" id="progressFill" style="width:0%;"></div></div>
      <div class="progress-label">
        <span id="progressText">Claim 1 of N</span>
        <span id="progressPct">0%</span>
      </div>
    </div>

    <div class="interview-grid">
      <div class="main-col">
        <div class="claim-under-review">
          <div class="eyebrow" id="claimTag">Under examination</div>
          <div class="claim-text" id="claimText">—</div>
        </div>

        <div class="transcript" id="transcript"></div>

        <div class="loading-block hidden" id="interviewerThinking" style="padding:24px 0;">
          <div class="spinner" style="width:22px;height:22px;margin-bottom:0;display:inline-block;vertical-align:middle;"></div>
          <span class="msg" style="margin-left:10px;" id="thinkingMsg">The interviewer is considering your answer...</span>
        </div>

        <div class="answer-box" id="answerBox">
          <textarea class="answer-input" id="answerInput" placeholder="Answer as you would in the room. Be specific — the vaguer the answer, the harder the follow-up."></textarea>
          <div class="answer-controls">
            <span class="char-count" id="charCount">0 characters</span>
            <button class="btn" id="btnSubmitAnswer">Submit answer →</button>
          </div>
        </div>
      </div>

      <div class="sidebar">
        <div class="panel">
          <h3>Confidence map</h3>
          <div id="confidenceMap"></div>
        </div>
        <div class="panel">
          <h3>This claim</h3>
          <div id="claimVerdictPanel" class="mono" style="font-size:12.5px;color:var(--ink-soft);">not yet assessed</div>
        </div>
        <div class="panel">
          <button class="btn secondary" id="btnSkipClaim" style="width:100%;justify-content:center;">Move to next claim</button>
        </div>
      </div>
    </div>
  </section>

  <!-- ===================== SCREEN: REPORT ===================== -->
  <section id="screen-report" class="screen hidden">
    <div class="report-hero">
      <div class="eyebrow">Final Defense Report</div>
      <div class="score" id="overallScore">—</div>
      <div class="score-label">Overall defense strength</div>
    </div>

    <div class="report-section">
      <h2>How each claim held up</h2>
      <div id="reportBars"></div>
    </div>

    <div class="report-section">
      <h2>Well defended</h2>
      <div id="reportStrong"></div>
    </div>

    <div class="report-section">
      <h2>Needs work before the real interview</h2>
      <div id="reportWeak"></div>
    </div>

    <div class="report-section">
      <h2>Interviewer's closing notes</h2>
      <p id="reportClosing" style="font-size:16px;"></p>
    </div>

    <div class="btn-row">
      <button class="btn" id="btnExportReport">Export report (.txt) →</button>
      <button class="btn secondary" id="btnPrintReport">Print / Save as PDF</button>
      <button class="btn danger" id="btnNewSession">Start a new case file</button>
    </div>
  </section>

  <footer class="byline">Defend Your Experience — every question generated from your own words, not a template.</footer>
</div>

<div class="toast" id="toast"></div>

<script>
(function(){
  "use strict";

  /* ======================= STATE ======================= */
  const STORAGE_KEY = "defend-experience-session-v1";
  const state = {
    resumeText: "",
    difficulty: "toughest", // fixed per interview design
    style: "editorial",
    claims: [],            // {id, text, category, source, status, confidence, transcript:[], depth}
    currentClaimIndex: 0,
    screen: "intro",
    report: null
  };

  function saveState(){
    try{ localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); }catch(e){}
  }
  function loadState(){
    try{
      const raw = localStorage.getItem(STORAGE_KEY);
      if(!raw) return null;
      return JSON.parse(raw);
    }catch(e){ return null; }
  }
  function clearState(){
    try{ localStorage.removeItem(STORAGE_KEY); }catch(e){}
  }

  /* ======================= UTIL ======================= */
  function $(id){ return document.getElementById(id); }
  function showScreen(name){
    ["intro","extracting","claims","interview","report"].forEach(s=>{
      $("screen-"+s).classList.toggle("hidden", s!==name);
    });
    state.screen = name;
    updateStatusLine();
    saveState();
  }
  function toast(msg){
    const t = $("toast");
    t.textContent = msg;
    t.classList.add("show");
    setTimeout(()=>t.classList.remove("show"), 2600);
  }
  function updateStatusLine(){
    const total = state.claims.length;
    if(state.screen==="intro"){ $("statusLine").textContent = "no case file open"; $("statusSub").textContent=""; return; }
    if(total===0){ $("statusLine").textContent = "case file loading"; $("statusSub").textContent=""; return; }
    const defended = state.claims.filter(c=>c.status==="defended").length;
    $("statusLine").textContent = total + " claims on file";
    $("statusSub").textContent = defended + " defended so far";
  }

  /* ======================= ANTHROPIC API ======================= */
  async function callClaude(system, userMessage, {retries=2}={}){
    const body = {
      model: "claude-sonnet-4-6",
      max_tokens: 1000,
      system: system,
      messages: [{ role:"user", content: userMessage }]
    };
    for(let attempt=0; attempt<=retries; attempt++){
      try{
        const res = await fetch("https://api.anthropic.com/v1/messages", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(body)
        });
        if(res.status===429 || res.status===529){
          if(attempt<retries){ await new Promise(r=>setTimeout(r, 1200*(attempt+1))); continue; }
          throw new Error("RATE_LIMIT");
        }
        if(!res.ok){ throw new Error("HTTP_"+res.status); }
        const data = await res.json();
        const text = (data.content||[]).map(b=>b.text||"").join("\n").trim();
        return text;
      }catch(err){
        if(attempt>=retries) throw err;
        await new Promise(r=>setTimeout(r, 900*(attempt+1)));
      }
    }
    throw new Error("FAILED");
  }

  function extractJson(text){
    let t = text.trim();
    t = t.replace(/^```json\s*/i,"").replace(/^```\s*/,"").replace(/```\s*$/,"");
    const start = t.indexOf("{"); const startArr = t.indexOf("[");
    let s = -1;
    if(start!==-1 && (startArr===-1 || start<startArr)) s = start; else s = startArr;
    if(s>0) t = t.slice(s);
    const lastBrace = Math.max(t.lastIndexOf("}"), t.lastIndexOf("]"));
    if(lastBrace!==-1) t = t.slice(0, lastBrace+1);
    return JSON.parse(t);
  }

  async function withFallback(fn, fallbackMsg){
    try{
      return await fn();
    }catch(err){
      console.error(err);
      toast(fallbackMsg || "The interviewer's line went quiet for a moment — please try again.");
      throw err;
    }
  }

  /* ======================= INTRO SCREEN ======================= */
  let uploadedText = "";

  const dropzone = $("dropzone");
  const fileInput = $("fileInput");
  ["dragenter","dragover"].forEach(ev=>{
    dropzone.addEventListener(ev, e=>{ e.preventDefault(); dropzone.classList.add("dragover"); });
  });
  ["dragleave","drop"].forEach(ev=>{
    dropzone.addEventListener(ev, e=>{ e.preventDefault(); dropzone.classList.remove("dragover"); });
  });
  dropzone.addEventListener("drop", e=>{
    const f = e.dataTransfer.files[0];
    if(f) handleFile(f);
  });
  fileInput.addEventListener("change", e=>{
    const f = e.target.files[0];
    if(f) handleFile(f);
  });
  function handleFile(f){
    $("filename").textContent = f.name;
    const reader = new FileReader();
    reader.onload = e=>{
      uploadedText = e.target.result;
      $("pasteBox").value = uploadedText;
    };
    reader.readAsText(f);
  }

  // MCQ for difficulty/context is pre-decided via conversation already (toughest, behavioral).
  // Style already chosen (editorial) — reflected purely in CSS, no extra prompt needed.

  $("btnExtract").addEventListener("click", async ()=>{
    const text = ($("pasteBox").value || uploadedText || "").trim();
    if(text.length < 40){
      toast("Add a bit more detail first — paste your resume or project text above.");
      return;
    }
    state.resumeText = text;
    showScreen("extracting");
    await runExtraction(text);
  });

  // Resume last session if present
  (function initResume(){
    const saved = loadState();
    if(saved && saved.resumeText && saved.claims && saved.claims.length){
      $("btnResume").classList.remove("hidden");
      $("btnResume").addEventListener("click", ()=>{
        Object.assign(state, saved);
        renderClaimsList();
        renderConfidenceMap();
        if(state.screen==="interview"){ showScreen("interview"); renderInterviewScreen(); }
        else if(state.screen==="report"){ showScreen("report"); renderReport(state.report); }
        else { showScreen("claims"); }
      });
    }
  })();

  /* ======================= EXTRACTION ======================= */
  const extractMessages = [
    "Reading the file...",
    "Underlining every bold claim...",
    "Cross-referencing verbs like 'led' and 'built'...",
    "Separating fact from framing...",
    "Assembling the case file..."
  ];
  async function runExtraction(text){
    let i=0;
    const interval = setInterval(()=>{
      i = (i+1)%extractMessages.length;
      $("extractMsg").textContent = extractMessages[i];
    }, 900);

    const system = `You are a meticulous, skeptical interview preparation analyst. You read a person's resume, bio, or project document and extract every meaningful, checkable claim they made about themselves. A claim is anything that asserts an action, an outcome, a skill, a metric, an ownership statement, or a scope of responsibility (e.g. "architected a full-stack app", "reduced overfitting", "led a team", "improved performance"). Ignore pure facts with nothing to defend (like dates, degree names, GPA alone) UNLESS they imply an achievement (e.g. "1st in class" is a claim; "MCA, IMS Noida" is not).
Respond ONLY with strict JSON, no prose, no markdown fences. Format:
{"claims":[{"text":"the claim in the person's own words, cleaned up to one sentence","category":"one short label like Ownership, Technical Depth, Impact/Metric, Scope, Architecture Decision, Quality/Testing","source":"which project or section it came from"}]}
Extract between 8 and 14 claims. Prioritize the claims most likely to be probed hard by a skeptical interviewer: vague verbs (architected, led, improved), unverified metrics, security/authentication claims, and any claim implying full ownership of a project.`;

    try{
      const raw = await callClaude(system, "Here is the document:\n\n" + text);
      const parsed = extractJson(raw);
      const claims = (parsed.claims||[]).map((c,idx)=>({
        id: "c"+idx+"_"+Date.now(),
        text: c.text,
        category: c.category || "Claim",
        source: c.source || "",
        status: "pending",      // pending | defended | shaky | unverified
        confidence: 0,
        transcript: [],
        depth: 0,
        feedback: "",
        recommendation: ""
      }));
      if(!claims.length) throw new Error("NO_CLAIMS");
      state.claims = claims;
      state.currentClaimIndex = 0;
      clearInterval(interval);
      renderClaimsList();
      showScreen("claims");
    }catch(err){
      clearInterval(interval);
      console.error(err);
      $("extractMsg").textContent = "Couldn't read the file clearly — please try again in a moment.";
      setTimeout(()=>showScreen("intro"), 1800);
      toast("The interviewer couldn't parse that document. Try pasting plain text instead.");
    }
  }

  function renderClaimsList(){
    const host = $("claimsList");
    host.innerHTML = "";
    state.claims.forEach(c=>{
      const div = document.createElement("div");
      div.className = "claim-card";
      div.innerHTML = `<span class="tag">${escapeHtml(c.category)}</span>
        <div>
          <div class="txt">${escapeHtml(c.text)}</div>
          ${c.source ? `<div class="src">from: ${escapeHtml(c.source)}</div>` : ""}
        </div>`;
      host.appendChild(div);
    });
    updateStatusLine();
  }

  function escapeHtml(s){
    return (s||"").replace(/[&<>"']/g, m=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[m]));
  }

  $("btnBackToIntro").addEventListener("click", ()=>{
    state.claims = [];
    showScreen("intro");
  });

  $("btnBeginInterview").addEventListener("click", ()=>{
    state.currentClaimIndex = 0;
    showScreen("interview");
    renderInterviewScreen(true);
  });

  /* ======================= INTERVIEW SCREEN ======================= */
  function currentClaim(){ return state.claims[state.currentClaimIndex]; }

  function renderProgress(){
    const total = state.claims.length;
    const done = state.claims.filter(c=>c.status!=="pending").length;
    const idx = state.currentClaimIndex;
    $("progressText").textContent = `Claim ${Math.min(idx+1,total)} of ${total}`;
    const pct = Math.round((done/total)*100);
    $("progressFill").style.width = pct+"%";
    $("progressPct").textContent = pct+"% defended";
  }

  function renderConfidenceMap(){
    const host = $("confidenceMap");
    host.innerHTML = "";
    state.claims.forEach((c,idx)=>{
      const row = document.createElement("div");
      row.className = "confidence-row";
      const statusClass = c.status;
      row.innerHTML = `<span class="dot ${statusClass}"></span>
        <span class="label">${escapeHtml(c.text.slice(0,34))}${c.text.length>34?"…":""}</span>
        <span class="pct">${c.status==="pending" ? "—" : c.confidence+"%"}</span>`;
      host.appendChild(row);
    });
  }

  async function renderInterviewScreen(fresh){
    if(state.currentClaimIndex >= state.claims.length){
      await finishAndBuildReport();
      return;
    }
    renderProgress();
    renderConfidenceMap();
    const c = currentClaim();
    $("claimTag").textContent = "Under examination — " + c.category;
    $("claimText").textContent = c.text;
    $("transcript").innerHTML = "";
    $("claimVerdictPanel").textContent = "not yet assessed";
    $("claimVerdictPanel").className = "mono";
    $("answerInput").value = "";
    $("charCount").textContent = "0 characters";
    $("answerBox").classList.remove("hidden");

    c.transcript.forEach(turn=>appendBubble(turn.role, turn.text));

    if(c.transcript.length===0){
      await askOpeningQuestion(c);
    }
    saveState();
  }

  function appendBubble(role, text){
    const div = document.createElement("div");
    if(role==="interviewer"){
      div.className = "bubble interviewer";
      div.innerHTML = `<span class="who">Interviewer</span>${escapeHtml(text)}`;
    } else {
      div.className = "bubble user";
      div.innerHTML = `<span class="who">You</span>${escapeHtml(text)}`;
    }
    $("transcript").appendChild(div);
    div.scrollIntoView({behavior:"smooth", block:"end"});
  }

  function setThinking(on, msg){
    $("interviewerThinking").classList.toggle("hidden", !on);
    if(msg) $("thinkingMsg").textContent = msg;
    $("answerBox").classList.toggle("hidden", on);
  }

  async function askOpeningQuestion(c){
    setThinking(true, "The interviewer is reading this claim closely...");
    const system = `You are a sharp, skeptical, but fair behavioral interviewer preparing an early-career candidate (0-3 years experience) to defend their resume. You do NOT know who is behind the toughest version of your persona yet — assume the toughest realistic interviewer, since the candidate wants maximum preparation. Your job right now is to ask ONE opening question that challenges this specific claim. Focus especially on ownership ("did you personally do this or was it the team/a library/a tutorial?"), specificity (vague claims get probed for concrete detail), and plausibility for someone at this experience level. Do not be cruel or sarcastic — be direct, professional, and a little probing, like a good hiring manager who has seen a thousand resumes. Keep the question to 1-3 sentences. Respond with plain text only — the question itself, nothing else, no preamble.`;
    const user = `Full document for context:\n${state.resumeText}\n\nThe specific claim to open on: "${c.text}" (category: ${c.category})\n\nAsk your opening question.`;
    try{
      const q = await callClaude(system, user);
      c.transcript.push({role:"interviewer", text:q});
      appendBubble("interviewer", q);
    }catch(err){
      const fallback = `Walk me through exactly what you did for: "${c.text}". What was your specific contribution versus the team's?`;
      c.transcript.push({role:"interviewer", text:fallback});
      appendBubble("interviewer", fallback);
      toast("Connection hiccup — using a standard follow-up for now.");
    }finally{
      setThinking(false);
    }
  }

  $("answerInput").addEventListener("input", e=>{
    $("charCount").textContent = e.target.value.length + " characters";
  });

  $("btnSubmitAnswer").addEventListener("click", submitAnswer);
  $("answerInput").addEventListener("keydown", e=>{
    if(e.key==="Enter" && (e.metaKey||e.ctrlKey)){ submitAnswer(); }
  });

  async function submitAnswer(){
    const val = $("answerInput").value.trim();
    if(!val){ toast("Enter an answer before submitting."); return; }
    const c = currentClaim();
    c.transcript.push({role:"user", text:val});
    appendBubble("user", val);
    $("answerInput").value = "";
    $("charCount").textContent = "0 characters";
    c.depth += 1;
    setThinking(true, "The interviewer is weighing your answer...");

    const system = `You are a sharp, skeptical, fair behavioral interviewer defending-your-experience session, examining an early-career candidate. You are currently probing ONE specific resume claim across a short back-and-forth (usually 2-4 exchanges). Given the full conversation so far about this claim, decide:
1) Whether to ask a deeper, more specific follow-up (escalate: ask about edge cases, metrics, what would happen if challenged, alternative approaches, or trade-offs) OR conclude this claim.
2) A running verdict: "defended" (specific, credible, owns the work, holds up under pressure), "shaky" (partially convincing but vague, inconsistent, or over-claims), or "unverified" (cannot substantiate, admits it was minimal/team-driven/tutorial-following, or contradicts itself).
3) A confidence score 0-100 reflecting how well defended the claim is right now.
4) Brief feedback (1-2 sentences, direct, specific to what they actually said).
5) If concluding (moveOn:true), a one-sentence recommendation for how they could tell this story more strongly in a real interview.
Rules: Conclude (moveOn:true) after at most 3 user answers on this claim, or earlier if the claim is clearly well-defended with concrete specifics, or clearly falling apart. Escalate specificity each round rather than repeating similar questions. Respond ONLY with strict JSON, no markdown fences:
{"moveOn": boolean, "nextQuestion": "string or empty if moveOn is true", "verdict": "defended|shaky|unverified", "confidence": number, "feedback": "string", "recommendation": "string, only meaningful if moveOn is true, else empty string"}`;

    const convo = c.transcript.map(t=> (t.role==="interviewer"?"INTERVIEWER: ":"CANDIDATE: ") + t.text).join("\n");
    const user = `Claim being examined: "${c.text}" (category: ${c.category})\nExchange count so far: ${c.depth}\n\nFull conversation on this claim:\n${convo}\n\nDecide the next step.`;

    try{
      const raw = await callClaude(system, user);
      const parsed = extractJson(raw);
      c.status = parsed.verdict || "shaky";
      c.confidence = typeof parsed.confidence === "number" ? Math.max(0,Math.min(100,parsed.confidence)) : 50;
      c.feedback = parsed.feedback || "";
      if(parsed.moveOn){
        c.recommendation = parsed.recommendation || "";
        showVerdictFlash(c);
        renderConfidenceMap();
        saveState();
        setTimeout(()=>{
          state.currentClaimIndex += 1;
          renderInterviewScreen();
        }, 1400);
      }else{
        const q = parsed.nextQuestion || "Can you be more specific about your exact role in that?";
        c.transcript.push({role:"interviewer", text:q});
        appendBubble("interviewer", q);
        renderConfidenceMap();
        updateClaimPanel(c);
        saveState();
      }
    }catch(err){
      toast("The interviewer's line dropped for a moment — try submitting again.");
      c.depth -= 1; // allow retry
    }finally{
      setThinking(false);
    }
  }

  function updateClaimPanel(c){
    $("claimVerdictPanel").innerHTML = `<div class="stamp ${c.status}" style="color:${c.status==='defended'?'var(--sage)':c.status==='shaky'?'var(--gold)':'var(--danger)'}">${c.status}</div><div style="margin-top:8px;">${escapeHtml(c.feedback)}</div>`;
  }

  function showVerdictFlash(c){
    updateClaimPanel(c);
    const flash = document.createElement("div");
    flash.className = "verdict-flash "+c.status;
    flash.textContent = c.status + " — " + c.confidence + "% confidence. Moving to next claim...";
    $("transcript").appendChild(flash);
    flash.scrollIntoView({behavior:"smooth"});
  }

  $("btnSkipClaim").addEventListener("click", ()=>{
    const c = currentClaim();
    if(c.status==="pending"){ c.status="unverified"; c.confidence=20; c.feedback="Skipped without a defense."; }
    state.currentClaimIndex += 1;
    renderInterviewScreen();
  });

  /* ======================= REPORT ======================= */
  async function finishAndBuildReport(){
    showScreen("report");
    $("reportBars").innerHTML = "";
    $("reportStrong").innerHTML = "";
    $("reportWeak").innerHTML = "";
    $("reportClosing").innerHTML = "";
    $("overallScore").innerHTML = `<div class="spinner" style="width:26px;height:26px;margin:0 auto;"></div>`;

    const avg = Math.round(state.claims.reduce((s,c)=>s+(c.confidence||0),0)/state.claims.length);

    const system = `You are a skeptical but constructive behavioral interviewer writing a closing note after a full mock defense session with an early-career candidate. You've just finished probing every claim on their resume. Write 3-5 sentences of direct, honest, encouraging-but-not-soft closing feedback about their overall defense performance, referencing real patterns from the session (e.g. tendency to over-claim ownership, strong technical specificity, vague metrics). Respond with plain text only, no headers, no markdown.`;
    const summary = state.claims.map(c=>`- "${c.text}" — verdict: ${c.status}, confidence: ${c.confidence}%, feedback: ${c.feedback}`).join("\n");
    let closing = "";
    try{
      closing = await callClaude(system, "Session summary:\n"+summary);
    }catch(err){
      closing = "Overall, some claims held up well under pressure while others need firmer, more specific evidence. Focus on naming your exact individual contribution for every project, and always have one concrete number or outcome ready, even an approximate one, rather than a general statement of success.";
    }

    state.report = { avg, closing, claims: state.claims };
    renderReport(state.report);
    saveState();
  }

  function renderReport(report){
    $("overallScore").textContent = report.avg + "%";
    const scoreColor = report.avg>=70 ? "var(--sage)" : report.avg>=45 ? "var(--gold)" : "var(--danger)";
    $("overallScore").style.color = scoreColor;

    const barsHost = $("reportBars");
    barsHost.innerHTML = "";
    report.claims.forEach(c=>{
      const color = c.status==="defended" ? "var(--sage)" : c.status==="shaky" ? "var(--gold)" : "var(--danger)";
      const row = document.createElement("div");
      row.className = "bar-row";
      row.innerHTML = `<div class="name" title="${escapeHtml(c.text)}">${escapeHtml(c.text.slice(0,28))}${c.text.length>28?"…":""}</div>
        <div class="bar-track"><div class="bar-fill" style="width:${c.confidence}%;background:${color};"></div></div>
        <div class="pct">${c.confidence}%</div>`;
      barsHost.appendChild(row);
    });

    const strong = report.claims.filter(c=>c.status==="defended");
    const weak = report.claims.filter(c=>c.status!=="defended");

    $("reportStrong").innerHTML = strong.length ? "" : `<div class="empty-state" style="padding:24px;"><div class="glyph">—</div>No claims fully held up yet. That's exactly what the practice below is for.</div>`;
    strong.forEach(c=>{
      const card = document.createElement("div");
      card.className = "report-card";
      card.innerHTML = `<div class="head"><div class="claim-txt">${escapeHtml(c.text)}</div><div class="stamp" style="color:var(--sage);">defended</div></div>
        <div class="feedback">${escapeHtml(c.feedback)}</div>`;
      $("reportStrong").appendChild(card);
    });

    $("reportWeak").innerHTML = weak.length ? "" : `<div class="empty-state" style="padding:24px;"><div class="glyph">✓</div>Every claim held up under pressure. Strong session.</div>`;
    weak.forEach(c=>{
      const card = document.createElement("div");
      card.className = "report-card";
      const color = c.status==="shaky" ? "var(--gold)" : "var(--danger)";
      card.innerHTML = `<div class="head"><div class="claim-txt">${escapeHtml(c.text)}</div><div class="stamp" style="color:${color};">${c.status}</div></div>
        <div class="feedback">${escapeHtml(c.feedback)}</div>
        ${c.recommendation ? `<div class="rec"><strong>To strengthen this story</strong>${escapeHtml(c.recommendation)}</div>` : ""}`;
      $("reportWeak").appendChild(card);
    });

    $("reportClosing").textContent = report.closing;
  }

  $("btnExportReport").addEventListener("click", ()=>{
    if(!state.report) return;
    const lines = [];
    lines.push("DEFEND YOUR EXPERIENCE — DEFENSE REPORT");
    lines.push("Overall defense strength: " + state.report.avg + "%");
    lines.push("");
    state.claims.forEach(c=>{
      lines.push("CLAIM: " + c.text);
      lines.push("Verdict: " + c.status + " (" + c.confidence + "% confidence)");
      lines.push("Feedback: " + c.feedback);
      if(c.recommendation) lines.push("Recommendation: " + c.recommendation);
      lines.push("");
    });
    lines.push("CLOSING NOTES:");
    lines.push(state.report.closing);
    const blob = new Blob([lines.join("\n")], {type:"text/plain"});
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url; a.download = "defense-report.txt";
    a.click();
    URL.revokeObjectURL(url);
  });

  $("btnPrintReport").addEventListener("click", ()=> window.print());

  $("btnNewSession").addEventListener("click", ()=>{
    clearState();
    Object.assign(state, {
      resumeText:"", claims:[], currentClaimIndex:0, screen:"intro", report:null
    });
    $("pasteBox").value = "";
    $("filename").textContent = "";
    uploadedText = "";
    showScreen("intro");
  });

  /* ======================= INIT ======================= */
  updateStatusLine();
  showScreen("intro");

})();
</script>
</body>
</html>
