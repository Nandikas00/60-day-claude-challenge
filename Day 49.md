# Today I built a Personal AI Playbook using claude :

## Key Learnings :
- Learned how to design a structured AI-assisted debugging workflow that guides developers from problem identification to long-term prevention.
- Gained practical experience in creating reusable AI prompt templates for different debugging stages, reducing repetitive prompt writing.
- Explored prompt engineering techniques to generate context-aware prompts using predefined building blocks like roles, context, and expected output.
- Understood the importance of providing complete project context to AI for generating more accurate and relevant debugging assistance.
- Learned how self-review and iterative feedback loops improve the quality and reliability of AI-generated code fixes.
- Practiced building reusable debugging workflows covering error analysis, reproduction, solution verification, and post-mortem documentation.
- Improved frontend development skills by creating an intuitive dashboard with workflow management, search, prompt organization, and local storage support.
- Strengthened understanding of knowledge management by converting resolved bugs into reusable playbooks that accelerate future debugging sessions.

### Output Screenshots :
<img width="1838" height="870" alt="Screenshot (681)" src="https://github.com/user-attachments/assets/408d11da-18b0-4a07-802f-933258422ed9" />
<img width="1838" height="870" alt="Screenshot (680)" src="https://github.com/user-attachments/assets/d473a4e4-6789-49b5-8da2-174687a5512c" />

#### HTML File :

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Debug Loop — Your Personal AI Playbook</title>
<style>
  :root{
    --ink:#12141a; --ink2:#191c24; --ink3:#20242e; --line:#2a2f3b;
    --text:#e7e9ee; --text-dim:#9aa1b0; --text-faint:#666d7e;
    --amber:#f0a868; --amber-dim:#8a6339; --teal:#5eead4; --teal-dim:#2f6e64;
    --red:#f27979; --green:#8fd19e;
    --radius:10px; --mono:'SF Mono','JetBrains Mono',Consolas,'Roboto Mono',monospace;
    --sans:-apple-system,BlinkMacSystemFont,'Inter','Segoe UI',Roboto,sans-serif;
    --shadow: 0 8px 30px rgba(0,0,0,.35);
  }
  [data-theme="light"]{
    --ink:#f7f6f2; --ink2:#ffffff; --ink3:#eeece5; --line:#dcd9cf;
    --text:#1c1b18; --text-dim:#5b584f; --text-faint:#8a8778;
    --amber:#b5702a; --amber-dim:#e4c9a4; --teal:#0e7c6c; --teal-dim:#bfe6de;
    --shadow: 0 8px 24px rgba(0,0,0,.08);
  }
  *{box-sizing:border-box; margin:0; padding:0;}
  body{background:var(--ink); color:var(--text); font-family:var(--sans); line-height:1.5; transition:background .25s,color .25s;}
  ::selection{background:var(--amber); color:#12141a;}
  code, .mono{font-family:var(--mono);}
  button{font-family:inherit; cursor:pointer;}
  a{color:inherit;}
  ::-webkit-scrollbar{width:10px;height:10px;}
  ::-webkit-scrollbar-thumb{background:var(--line); border-radius:6px;}

  /* ===== Layout shell ===== */
  .app{display:flex; min-height:100vh;}
  .sidebar{
    width:230px; flex-shrink:0; border-right:1px solid var(--line); background:var(--ink2);
    display:flex; flex-direction:column; padding:20px 14px; position:sticky; top:0; height:100vh;
  }
  .brand{display:flex; align-items:center; gap:10px; padding:0 6px 18px; border-bottom:1px solid var(--line); margin-bottom:14px;}
  .brand-mark{width:30px;height:30px;border-radius:8px;background:linear-gradient(135deg,var(--amber),var(--teal)); flex-shrink:0; position:relative;}
  .brand-mark::after{content:"";position:absolute; inset:8px; border:2px solid var(--ink2); border-radius:3px;}
  .brand-text{font-size:14.5px; font-weight:700; letter-spacing:.2px;}
  .brand-sub{font-size:10.5px; color:var(--text-faint); font-family:var(--mono);}

  .navlist{display:flex; flex-direction:column; gap:2px; margin-top:4px;}
  .navitem{
    display:flex; align-items:center; gap:10px; padding:9px 10px; border-radius:8px; border:none;
    background:transparent; color:var(--text-dim); font-size:13.5px; text-align:left; width:100%; font-weight:500;
    transition:background .15s, color .15s;
  }
  .navitem:hover{background:var(--ink3); color:var(--text);}
  .navitem.active{background:var(--ink3); color:var(--amber);}
  .navitem .ic{width:16px; text-align:center; opacity:.9; font-size:14px;}

  .sidebar-foot{margin-top:auto; display:flex; flex-direction:column; gap:8px; padding-top:14px; border-top:1px solid var(--line);}
  .kbd-hint{font-size:11px; color:var(--text-faint); font-family:var(--mono); display:flex; justify-content:space-between;}
  .kbd{background:var(--ink3); border:1px solid var(--line); border-radius:4px; padding:1px 5px; font-size:10.5px;}

  .main{flex:1; min-width:0;}
  .topbar{
    position:sticky; top:0; z-index:20; display:flex; align-items:center; gap:12px;
    padding:14px 28px; border-bottom:1px solid var(--line); background:color-mix(in srgb, var(--ink) 88%, transparent);
    backdrop-filter:blur(10px);
  }
  .searchwrap{flex:1; max-width:420px; position:relative;}
  .searchwrap input{
    width:100%; background:var(--ink2); border:1px solid var(--line); color:var(--text); border-radius:8px;
    padding:8px 12px 8px 32px; font-size:13px; outline:none;
  }
  .searchwrap input:focus{border-color:var(--amber);}
  .searchwrap .sic{position:absolute; left:11px; top:50%; transform:translateY(-50%); color:var(--text-faint); font-size:13px;}
  .topbar-actions{display:flex; align-items:center; gap:8px; margin-left:auto;}
  .iconbtn{
    width:34px; height:34px; border-radius:8px; border:1px solid var(--line); background:var(--ink2); color:var(--text-dim);
    display:flex; align-items:center; justify-content:center; font-size:14px; transition:.15s;
  }
  .iconbtn:hover{color:var(--text); border-color:var(--amber);}
  .btn{
    border-radius:8px; border:1px solid var(--line); background:var(--ink2); color:var(--text);
    padding:8px 14px; font-size:13px; font-weight:600; display:inline-flex; align-items:center; gap:6px; transition:.15s;
  }
  .btn:hover{border-color:var(--amber); color:var(--amber);}
  .btn.primary{background:linear-gradient(135deg,var(--amber),#e08a4a); color:#1a1206; border:none;}
  .btn.primary:hover{filter:brightness(1.08); color:#1a1206;}
  .btn.ghost{background:transparent;}
  .btn.small{padding:5px 10px; font-size:12px;}

  .view{padding:26px 28px 60px; max-width:1180px;}
  .view.hidden{display:none;}

  /* ===== Explainer banner ===== */
  .explainer{
    background:linear-gradient(135deg, var(--ink3), var(--ink2)); border:1px solid var(--line); border-left:3px solid var(--amber);
    border-radius:var(--radius); padding:16px 18px; margin-bottom:22px; display:flex; gap:14px; align-items:flex-start;
  }
  .explainer .exic{font-size:20px; margin-top:1px;}
  .explainer-body{flex:1;}
  .explainer-title{font-weight:700; font-size:14px; margin-bottom:4px;}
  .explainer-text{font-size:13px; color:var(--text-dim); line-height:1.55;}
  .explainer-text b{color:var(--text);}
  .explainer-close{background:none; border:none; color:var(--text-faint); font-size:16px; padding:2px 6px;}
  .explainer-close:hover{color:var(--text);}

  h1.pagetitle{font-size:23px; font-weight:800; letter-spacing:-.2px; margin-bottom:4px;}
  .pagesubtitle{font-size:13.5px; color:var(--text-dim); margin-bottom:20px;}

  /* ===== Context Profile card ===== */
  .ctx-card{
    background:var(--ink2); border:1px solid var(--line); border-radius:var(--radius); padding:18px 20px; margin-bottom:24px;
  }
  .ctx-head{display:flex; align-items:center; justify-content:space-between; margin-bottom:4px;}
  .ctx-head h3{font-size:14.5px;}
  .ctx-desc{font-size:12.5px; color:var(--text-dim); margin-bottom:14px;}
  .ctx-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(200px,1fr)); gap:10px;}
  .field label{display:block; font-size:11px; color:var(--text-faint); margin-bottom:4px; font-weight:600; text-transform:uppercase; letter-spacing:.3px;}
  .field input, .field select, .field textarea{
    width:100%; background:var(--ink); border:1px solid var(--line); color:var(--text); border-radius:7px;
    padding:8px 10px; font-size:13px; outline:none; font-family:inherit;
  }
  .field textarea{resize:vertical; min-height:56px;}
  .field input:focus, .field select:focus, .field textarea:focus{border-color:var(--teal);}
  .ctx-status{font-size:11.5px; color:var(--teal); margin-top:12px; display:flex; align-items:center; gap:6px; font-family:var(--mono);}

  /* ===== Stat row ===== */
  .stats{display:grid; grid-template-columns:repeat(auto-fit,minmax(150px,1fr)); gap:12px; margin-bottom:24px;}
  .statcard{background:var(--ink2); border:1px solid var(--line); border-radius:var(--radius); padding:14px 16px;}
  .statnum{font-size:22px; font-weight:800; font-family:var(--mono);}
  .statlabel{font-size:11.5px; color:var(--text-faint); margin-top:2px;}

  /* ===== Category sections ===== */
  .cat-section{margin-bottom:30px;}
  .cat-header{display:flex; align-items:baseline; gap:10px; margin-bottom:12px;}
  .cat-header h2{font-size:15.5px; font-weight:700;}
  .cat-header .count{font-size:11.5px; color:var(--text-faint); font-family:var(--mono);}
  .cat-header .catdesc{font-size:12px; color:var(--text-dim); margin-left:auto;}

  .wf-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(300px,1fr)); gap:12px;}
  .wf-card{
    background:var(--ink2); border:1px solid var(--line); border-radius:var(--radius); padding:16px; cursor:pointer;
    transition:.15s; display:flex; flex-direction:column; gap:8px; position:relative;
  }
  .wf-card:hover{border-color:var(--amber); transform:translateY(-1px);}
  .wf-top{display:flex; align-items:flex-start; justify-content:space-between; gap:8px;}
  .wf-title{font-size:14px; font-weight:700; line-height:1.3;}
  .wf-star{background:none; border:none; color:var(--text-faint); font-size:15px; flex-shrink:0;}
  .wf-star.active{color:var(--amber);}
  .wf-desc{font-size:12.5px; color:var(--text-dim); line-height:1.5; flex:1;}
  .wf-tags{display:flex; gap:6px; flex-wrap:wrap;}
  .tag{font-size:10.5px; background:var(--ink3); border:1px solid var(--line); color:var(--text-faint); padding:2px 7px; border-radius:20px; font-family:var(--mono);}
  .wf-foot{display:flex; gap:6px; margin-top:2px;}

  .empty{
    text-align:center; padding:50px 20px; color:var(--text-faint); font-size:13.5px;
    border:1px dashed var(--line); border-radius:var(--radius);
  }

  /* ===== Modal ===== */
  .overlay{
    position:fixed; inset:0; background:rgba(5,6,10,.6); backdrop-filter:blur(3px); z-index:100;
    display:flex; align-items:flex-start; justify-content:center; padding:40px 20px; overflow-y:auto;
  }
  .overlay.hidden{display:none;}
  .modal{
    background:var(--ink2); border:1px solid var(--line); border-radius:14px; max-width:720px; width:100%;
    box-shadow:var(--shadow); animation:pop .18s ease;
  }
  @keyframes pop{from{opacity:0; transform:translateY(8px) scale(.98);} to{opacity:1; transform:none;}}
  .modal-head{display:flex; align-items:flex-start; justify-content:space-between; padding:20px 22px; border-bottom:1px solid var(--line); gap:12px;}
  .modal-head h2{font-size:17px;}
  .modal-head .mh-desc{font-size:12.5px; color:var(--text-dim); margin-top:4px;}
  .modal-close{background:var(--ink3); border:1px solid var(--line); border-radius:8px; width:30px; height:30px; color:var(--text-dim); flex-shrink:0;}
  .modal-body{padding:20px 22px; max-height:70vh; overflow-y:auto;}
  .modal-foot{padding:16px 22px; border-top:1px solid var(--line); display:flex; gap:8px; justify-content:flex-end;}

  .section-label{font-size:11px; text-transform:uppercase; letter-spacing:.4px; color:var(--text-faint); font-weight:700; margin:18px 0 8px;}
  .section-label:first-child{margin-top:0;}
  .varfields{display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-bottom:6px;}
  .promptbox{
    background:var(--ink); border:1px solid var(--line); border-radius:8px; padding:14px; font-family:var(--mono);
    font-size:12.5px; line-height:1.7; white-space:pre-wrap; word-break:break-word; color:var(--text-dim); max-height:260px; overflow-y:auto;
  }
  .promptbox .fill{color:var(--teal); font-weight:600;}
  .promptbox .empty-var{color:var(--red);}
  ul.bp{padding-left:18px; font-size:12.5px; color:var(--text-dim); display:flex; flex-direction:column; gap:5px;}
  .example-box{background:var(--ink); border:1px solid var(--line); border-radius:8px; padding:12px 14px; font-size:12.5px; color:var(--text-dim); font-style:italic;}

  /* ===== Prompt/Loop builder ===== */
  .builder-wrap{display:grid; grid-template-columns:1.1fr 1fr; gap:20px; align-items:start;}
  @media (max-width:900px){.builder-wrap{grid-template-columns:1fr;}}
  .blockpicker{display:flex; flex-direction:column; gap:10px;}
  .block-choice{
    background:var(--ink2); border:1px solid var(--line); border-radius:10px; padding:12px 14px; cursor:pointer; transition:.15s;
  }
  .block-choice:hover{border-color:var(--teal);}
  .block-choice .bc-top{display:flex; justify-content:space-between; align-items:center;}
  .block-choice .bc-title{font-size:13.5px; font-weight:700; display:flex; align-items:center; gap:8px;}
  .block-choice .bc-badge{width:20px; height:20px; border-radius:5px; display:flex; align-items:center; justify-content:center; font-size:11px; background:var(--ink3); color:var(--amber);}
  .block-choice .bc-desc{font-size:11.5px; color:var(--text-faint); margin-top:4px; line-height:1.5;}
  .block-choice .bc-add{font-size:11px; color:var(--teal); font-weight:700;}
  .block-choice.added{opacity:.4; pointer-events:none;}

  .assembled{display:flex; flex-direction:column; gap:10px; min-height:120px;}
  .ablock{background:var(--ink2); border:1px solid var(--line); border-radius:10px; padding:12px 14px;}
  .ablock-top{display:flex; align-items:center; gap:8px; margin-bottom:6px;}
  .ablock-top .bc-badge{width:20px;height:20px;border-radius:5px;display:flex;align-items:center;justify-content:center;font-size:11px;background:var(--ink3);color:var(--teal); flex-shrink:0;}
  .ablock-title{font-size:13px; font-weight:700; flex:1;}
  .ablock-remove{background:none; border:none; color:var(--text-faint); font-size:13px;}
  .ablock-remove:hover{color:var(--red);}
  .ablock-hint{font-size:11px; color:var(--text-faint); margin-bottom:8px; line-height:1.5;}
  .ablock select, .ablock textarea, .ablock input{
    width:100%; background:var(--ink); border:1px solid var(--line); color:var(--text); border-radius:6px; padding:7px 9px; font-size:12.5px; margin-bottom:6px; font-family:inherit;
  }
  .ablock textarea{min-height:44px; resize:vertical;}

  .preview-col{position:sticky; top:80px;}
  .preview-card{background:var(--ink2); border:1px solid var(--line); border-radius:12px; padding:16px;}
  .preview-head{display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;}
  .preview-head h3{font-size:13.5px;}
  .preview-out{
    background:var(--ink); border:1px solid var(--line); border-radius:8px; padding:14px; font-family:var(--mono);
    font-size:12px; line-height:1.7; white-space:pre-wrap; word-break:break-word; color:var(--text-dim); min-height:160px; max-height:420px; overflow-y:auto;
  }

  .toast{
    position:fixed; bottom:22px; left:50%; transform:translateX(-50%) translateY(20px); background:var(--ink3); border:1px solid var(--teal);
    color:var(--text); padding:10px 18px; border-radius:8px; font-size:13px; opacity:0; transition:.25s; z-index:200; font-weight:600;
    display:flex; align-items:center; gap:8px; box-shadow:var(--shadow);
  }
  .toast.show{opacity:1; transform:translateX(-50%) translateY(0);}

  .filterbar{display:flex; gap:8px; margin-bottom:18px; flex-wrap:wrap;}
  .chip{
    background:var(--ink2); border:1px solid var(--line); color:var(--text-dim); padding:6px 12px; border-radius:20px; font-size:12px; font-weight:600;
  }
  .chip.active{border-color:var(--amber); color:var(--amber); background:var(--ink3);}

  .help-body h4{font-size:13.5px; margin:16px 0 6px;}
  .help-body h4:first-child{margin-top:0;}
  .help-body p, .help-body li{font-size:13px; color:var(--text-dim); line-height:1.6;}
  .help-body ul{padding-left:18px; margin-top:4px;}

  @media (max-width:760px){
    .sidebar{position:fixed; left:-240px; z-index:50; transition:left .2s; box-shadow:var(--shadow);}
    .sidebar.open{left:0;}
    .topbar{padding:12px 14px;}
    .view{padding:18px 14px 60px;}
    .mobile-menu-btn{display:flex !important;}
    .varfields{grid-template-columns:1fr;}
  }
  .mobile-menu-btn{display:none;}

  .kbd-modal-list{display:flex; flex-direction:column; gap:8px;}
  .kbd-row{display:flex; justify-content:space-between; font-size:13px; padding:6px 0; border-bottom:1px solid var(--line);}

  @media (prefers-reduced-motion: reduce){
    *{animation:none !important; transition:none !important;}
  }
</style>
</head>
<body data-theme="dark">
<div class="app">

  <!-- ============ SIDEBAR ============ -->
  <nav class="sidebar" id="sidebar">
    <div class="brand">
      <div class="brand-mark"></div>
      <div>
        <div class="brand-text">Debug Loop</div>
        <div class="brand-sub">Your Personal AI Playbook</div>
      </div>
    </div>
    <div class="navlist">
      <button class="navitem active" data-view="dashboard"><span class="ic">▤</span> Dashboard</button>
      <button class="navitem" data-view="workflows"><span class="ic">⌥</span> Debugging Workflows</button>
      <button class="navitem" data-view="promptbuilder"><span class="ic">✎</span> Prompt Builder</button>
      <button class="navitem" data-view="loopbuilder"><span class="ic">↻</span> Loop Builder</button>
      <button class="navitem" data-view="saved"><span class="ic">★</span> My Saved Workflows</button>
    </div>
    <div class="sidebar-foot">
      <div class="kbd-hint"><span>Search</span><span class="kbd">/</span></div>
      <div class="kbd-hint"><span>New workflow</span><span class="kbd">N</span></div>
      <div class="kbd-hint"><span>Toggle theme</span><span class="kbd">T</span></div>
      <button class="btn ghost small" id="exportBtn" style="width:100%; justify-content:center;">⤓ Export data</button>
      <button class="btn ghost small" id="importBtn" style="width:100%; justify-content:center;">⤒ Import data</button>
      <input type="file" id="importFile" accept="application/json" style="display:none;">
    </div>
  </nav>

  <!-- ============ MAIN ============ -->
  <div class="main">
    <div class="topbar">
      <button class="iconbtn mobile-menu-btn" id="menuBtn">☰</button>
      <div class="searchwrap">
        <span class="sic">⌕</span>
        <input type="text" id="searchInput" placeholder="Search workflows, tags, templates… ( / )">
      </div>
      <div class="topbar-actions">
        <button class="iconbtn" id="helpBtn" title="What is this?">?</button>
        <button class="iconbtn" id="themeBtn" title="Toggle dark/light">◐</button>
        <button class="btn primary small" id="newWorkflowBtn">+ New workflow</button>
      </div>
    </div>

    <!-- ===== DASHBOARD ===== -->
    <section class="view" id="view-dashboard">
      <div class="explainer" id="explainerBanner">
        <div class="exic">💡</div>
        <div class="explainer-body">
          <div class="explainer-title">What Debug Loop is</div>
          <div class="explainer-text">
            This is a personal toolkit of <b>reusable AI prompt templates</b>, built specifically around how <b>frontend engineers debug code with AI</b>. It's organized into three parts: <b>Debugging Workflows</b> (ready-made, fill-in-the-blank templates for each stage of a debugging session), the <b>Prompt Builder</b> (assemble a custom prompt from labeled building blocks like Role, Context, and Output Format), and the <b>Loop Builder</b> (turn any prompt into a self-checking, repeat-until-done instruction set for an AI agent). Everything you save lives only in this browser's local storage — nothing is sent anywhere.
          </div>
        </div>
        <button class="explainer-close" id="closeExplainer" title="Dismiss">✕</button>
      </div>

      <h1 class="pagetitle">Dashboard</h1>
      <p class="pagesubtitle">Your saved AI debugging workflows, at a glance.</p>

      <div class="ctx-card">
        <div class="ctx-head"><h3>🧩 Context Profile</h3></div>
        <p class="ctx-desc">Fill this out <b>once</b>. Every workflow template below can pull these details in automatically with one click, so you stop re-typing the same project context into every AI chat.</p>
        <div class="ctx-grid" id="ctxGrid"></div>
        <div class="ctx-status" id="ctxStatus"></div>
      </div>

      <div class="stats" id="statsRow"></div>

      <div id="dashboardCats"></div>
    </section>

    <!-- ===== WORKFLOWS (all, filterable) ===== -->
    <section class="view hidden" id="view-workflows">
      <h1 class="pagetitle">Debugging Workflows</h1>
      <p class="pagesubtitle">Step-by-step, fill-in-the-blank templates for every stage of a debugging session — from capturing context to verifying the fix.</p>
      <div class="filterbar" id="filterBar"></div>
      <div id="workflowsAll"></div>
    </section>

    <!-- ===== PROMPT BUILDER ===== -->
    <section class="view hidden" id="view-promptbuilder">
      <h1 class="pagetitle">Prompt Builder</h1>
      <p class="pagesubtitle">Assemble a one-off prompt from labeled building blocks. Add the blocks you need, fill them in, and watch the final prompt take shape on the right.</p>
      <div class="builder-wrap">
        <div>
          <div class="section-label">Available blocks — click to add</div>
          <div class="blockpicker" id="pbPicker"></div>
        </div>
        <div class="preview-col">
          <div class="section-label">Your prompt, assembled live</div>
          <div class="assembled" id="pbAssembled"></div>
          <div class="preview-card" style="margin-top:14px;">
            <div class="preview-head">
              <h3>Live preview</h3>
              <button class="btn small" id="pbCopy">⧉ Copy prompt</button>
            </div>
            <div class="preview-out" id="pbOutput">Add a block on the left to begin building your prompt.</div>
            <button class="btn small ghost" id="pbSave" style="margin-top:10px; width:100%; justify-content:center;">★ Save as a reusable workflow</button>
          </div>
        </div>
      </div>
    </section>

    <!-- ===== LOOP BUILDER ===== -->
    <section class="view hidden" id="view-loopbuilder">
      <h1 class="pagetitle">Loop Builder</h1>
      <p class="pagesubtitle">
        Turn any normal prompt into an <b>autonomous looping prompt</b> — instructions that tell the AI to keep retrying and self-checking its own work until a goal is met, instead of stopping after one pass. Useful for things like "keep iterating on this fix until all tests pass."
      </p>
      <div class="builder-wrap">
        <div>
          <div class="section-label">1. Paste the base prompt to loop</div>
          <div class="field" style="margin-bottom:16px;">
            <textarea id="loopBase" rows="4" placeholder="e.g. Fix the failing test in checkout.test.js and explain the root cause."></textarea>
          </div>
          <div class="section-label">2. Define the loop — click a block to add it</div>
          <div class="blockpicker" id="lbPicker"></div>
        </div>
        <div class="preview-col">
          <div class="section-label">Assembled loop instructions</div>
          <div class="assembled" id="lbAssembled"></div>
          <div class="preview-card" style="margin-top:14px;">
            <div class="preview-head">
              <h3>Live preview</h3>
              <button class="btn small" id="lbCopy">⧉ Copy loop prompt</button>
            </div>
            <div class="preview-out" id="lbOutput">Paste a base prompt and add loop blocks to begin.</div>
            <button class="btn small ghost" id="lbSave" style="margin-top:10px; width:100%; justify-content:center;">★ Save as a reusable workflow</button>
          </div>
        </div>
      </div>
    </section>

    <!-- ===== SAVED ===== -->
    <section class="view hidden" id="view-saved">
      <h1 class="pagetitle">My Saved Workflows</h1>
      <p class="pagesubtitle">Workflows you've created, duplicated, or saved from the Prompt and Loop Builders.</p>
      <div id="savedList"></div>
    </section>
  </div>
</div>

<!-- ===== Workflow detail modal ===== -->
<div class="overlay hidden" id="wfOverlay">
  <div class="modal">
    <div class="modal-head">
      <div>
        <h2 id="wfModalTitle">Workflow title</h2>
        <div class="mh-desc" id="wfModalDesc">Description</div>
      </div>
      <button class="modal-close" id="wfModalClose">✕</button>
    </div>
    <div class="modal-body" id="wfModalBody"></div>
    <div class="modal-foot">
      <button class="btn ghost small" id="wfDuplicateBtn">⧉ Duplicate</button>
      <button class="btn ghost small" id="wfEditBtn">✎ Edit</button>
      <button class="btn primary small" id="wfCopyBtn">⧉ Copy filled prompt</button>
    </div>
  </div>
</div>

<!-- ===== New/Edit workflow modal ===== -->
<div class="overlay hidden" id="editOverlay">
  <div class="modal">
    <div class="modal-head">
      <div>
        <h2 id="editModalTitle">New workflow</h2>
        <div class="mh-desc">Create a reusable template with your own {{variables}}.</div>
      </div>
      <button class="modal-close" id="editModalClose">✕</button>
    </div>
    <div class="modal-body">
      <div class="section-label">Title</div>
      <input class="field-input" id="editTitle" style="width:100%; background:var(--ink); border:1px solid var(--line); color:var(--text); border-radius:7px; padding:8px 10px; font-size:13px;">
      <div class="section-label">Category</div>
      <select id="editCategory" style="width:100%; background:var(--ink); border:1px solid var(--line); color:var(--text); border-radius:7px; padding:8px 10px; font-size:13px;"></select>
      <div class="section-label">Short description</div>
      <input id="editDesc" style="width:100%; background:var(--ink); border:1px solid var(--line); color:var(--text); border-radius:7px; padding:8px 10px; font-size:13px;">
      <div class="section-label">Template — use <code>{{variable_name}}</code> for fill-in spots</div>
      <textarea id="editTemplate" rows="8" style="width:100%; background:var(--ink); border:1px solid var(--line); color:var(--text); border-radius:7px; padding:10px; font-size:12.5px; font-family:var(--mono);"></textarea>
      <div class="section-label">Best practices (one per line, optional)</div>
      <textarea id="editBP" rows="3" style="width:100%; background:var(--ink); border:1px solid var(--line); color:var(--text); border-radius:7px; padding:10px; font-size:12.5px;"></textarea>
    </div>
    <div class="modal-foot">
      <button class="btn ghost small" id="editCancel">Cancel</button>
      <button class="btn primary small" id="editSave">Save workflow</button>
    </div>
  </div>
</div>

<!-- ===== Help modal ===== -->
<div class="overlay hidden" id="helpOverlay">
  <div class="modal">
    <div class="modal-head">
      <div><h2>What is this?</h2></div>
      <button class="modal-close" id="helpModalClose">✕</button>
    </div>
    <div class="modal-body help-body">
      <h4>The short version</h4>
      <p>Debug Loop is a personal library of AI prompt <b>systems</b> — not one-off prompts, but reusable templates and building blocks you fill in each time you debug something with an AI model.</p>
      <h4>Dashboard</h4>
      <p>Your home base: a Context Profile you fill out once, quick stats, and your workflows grouped by debugging stage.</p>
      <h4>Debugging Workflows</h4>
      <p>Ready-made templates for each stage of a debugging session (capturing context, root-causing, reading stack traces, reproducing, proposing a fix, verifying it, and writing a post-mortem). Each one has editable variables, a filled-in example, and best practices.</p>
      <h4>Prompt Builder</h4>
      <p>Build a custom one-off prompt from labeled blocks — Role, Objective, Context, Constraints, Reasoning Strategy, Output Format, Tone, Examples, Quality Checks — with a live preview of the assembled result.</p>
      <h4>Loop Builder</h4>
      <p>Take any prompt and wrap it in instructions that make an AI agent retry and self-check its own work automatically: Goal, Evaluation Criteria, Improvement Strategy, Stop Conditions, Safety Rules.</p>
      <h4>My Saved Workflows</h4>
      <p>Anything you create, duplicate, edit, or save from the builders lands here, alongside the built-in library. Everything is stored only in this browser (localStorage) — use Export/Import in the sidebar to back it up or move it to another device.</p>
      <h4>Keyboard shortcuts</h4>
      <div class="kbd-modal-list">
        <div class="kbd-row"><span>Focus search</span><span class="kbd">/</span></div>
        <div class="kbd-row"><span>New workflow</span><span class="kbd">N</span></div>
        <div class="kbd-row"><span>Toggle dark/light</span><span class="kbd">T</span></div>
        <div class="kbd-row"><span>Close any dialog</span><span class="kbd">Esc</span></div>
      </div>
    </div>
  </div>
</div>

<!-- ===== Onboarding modal (first run) ===== -->
<div class="overlay hidden" id="onboardOverlay">
  <div class="modal" style="max-width:520px;">
    <div class="modal-head">
      <div><h2>Welcome to Debug Loop 👋</h2><div class="mh-desc">A playbook built around how you actually debug frontend code with AI.</div></div>
      <button class="modal-close" id="onboardClose">✕</button>
    </div>
    <div class="modal-body">
      <p style="font-size:13.5px; color:var(--text-dim); line-height:1.7; margin-bottom:12px;">Based on a short setup interview, this playbook is tuned for:</p>
      <ul class="bp" style="margin-bottom:16px;">
        <li><b>Role:</b> Software / Frontend engineering</li>
        <li><b>Focus:</b> Debugging &amp; error analysis</li>
        <li><b>Biggest pain point:</b> re-explaining project context every time</li>
        <li><b>Tools:</b> Claude, ChatGPT, Gemini, GitHub Copilot</li>
      </ul>
      <p style="font-size:13.5px; color:var(--text-dim); line-height:1.7;">Start by filling out your <b>Context Profile</b> on the Dashboard — every workflow can pull it in automatically, so you never retype it again.</p>
    </div>
    <div class="modal-foot">
      <button class="btn primary small" id="onboardStart">Get started →</button>
    </div>
  </div>
</div>

<div class="toast" id="toast">✓ Copied to clipboard</div>

<script>
(function(){
"use strict";

/* ============================================================
   DATA MODEL
   ============================================================ */
const CATEGORIES = [
  {id:"context", name:"Context Capture", desc:"Package your project once so you never re-explain it."},
  {id:"triage",  name:"Root Cause Triage", desc:"Narrow down what's actually broken before touching code."},
  {id:"trace",   name:"Error & Stack Trace Analysis", desc:"Turn a raw error/stack trace into a clear diagnosis."},
  {id:"repro",   name:"Reproduction & Isolation", desc:"Build the smallest reliable repro of the bug."},
  {id:"fix",     name:"Fix Proposal & Verification", desc:"Get a reviewed fix, not just a guess."},
  {id:"post",    name:"Post-Mortem & Prevention", desc:"Capture what happened so it doesn't happen again."},
];

const CTX_FIELDS = [
  {key:"framework", label:"Framework / stack", type:"text", placeholder:"e.g. React 18 + TypeScript + Vite"},
  {key:"repo_type", label:"Project type", type:"select", options:["SPA","SSR / Next.js","Component library","Browser extension","Static site","Mobile web / PWA","Other"]},
  {key:"state_mgmt", label:"State management", type:"text", placeholder:"e.g. Redux Toolkit, Zustand, Context API"},
  {key:"styling", label:"Styling approach", type:"text", placeholder:"e.g. Tailwind, CSS Modules, styled-components"},
  {key:"testing", label:"Testing setup", type:"text", placeholder:"e.g. Vitest + React Testing Library"},
  {key:"conventions", label:"Conventions / constraints AI should respect", type:"textarea", placeholder:"e.g. functional components only, no default exports, strict TS"},
];

// {{project_context}} is a special variable auto-filled from the Context Profile.
const DEFAULT_WORKFLOWS = [
{
  id:"wf_context_snapshot", category:"context", builtin:true,
  title:"Context Snapshot (paste once per session)",
  desc:"The first message of any debugging chat. Front-loads everything the AI needs so you're never re-explaining your stack mid-conversation.",
  tags:["context","onboarding-ai"],
  template:
`You're helping me debug a frontend issue. Here is my project context — refer back to it instead of asking me to repeat it:

Stack: {{project_context}}

Additional notes for this session: {{session_notes}}

Acknowledge you've got this context, then wait for me to describe the bug.`,
  variables:[
    {name:"session_notes", label:"Anything else specific to this session", type:"textarea", placeholder:"e.g. working on a legacy module that predates our lint rules"},
  ],
  example:"Stack: React 18 + TypeScript + Vite, SPA, Redux Toolkit, Tailwind, Vitest + RTL, functional components only, strict TS. Session notes: working on the checkout flow, which still has some class components.",
  bestPractices:[
    "Send this as your very first message in a new AI chat or thread.",
    "Keep your Context Profile up to date — this template pulls it in automatically.",
    "If the AI's suggestions ignore your conventions, paste this again mid-chat as a reminder."
  ]
},
{
  id:"wf_root_cause_triage", category:"triage", builtin:true,
  title:"Root Cause Triage",
  desc:"Structures a vague 'something's broken' into a clear diagnostic question before you write any prompt asking for a fix.",
  tags:["triage","diagnosis"],
  template:
`Act as a senior frontend engineer helping me triage a bug. Don't propose a fix yet — first help me narrow down the cause.

Stack: {{project_context}}

Expected behavior: {{expected}}
Actual behavior: {{actual}}
When it started: {{when_started}}
Recent changes around that time: {{recent_changes}}

Give me:
1. The 3 most likely root causes, ranked by probability
2. One specific thing to check for each, that would confirm or rule it out
3. Any question you need answered before you could narrow it further`,
  variables:[
    {name:"expected", label:"Expected behavior", type:"textarea", placeholder:"What should happen"},
    {name:"actual", label:"Actual behavior", type:"textarea", placeholder:"What actually happens"},
    {name:"when_started", label:"When it started", type:"text", placeholder:"e.g. after last deploy, always, only on Safari"},
    {name:"recent_changes", label:"Recent changes", type:"textarea", placeholder:"Recent commits, dependency bumps, config changes"},
  ],
  example:"Expected: clicking 'Add to cart' updates the badge count. Actual: badge count updates on the 2nd click, not the 1st. Started: after upgrading Redux Toolkit last week.",
  bestPractices:[
    "Deliberately withhold the fix request — asking for causes first prevents premature, generic fixes.",
    "List recent changes even if you think they're unrelated; AI is good at spotting non-obvious correlations.",
    "If the AI gives you a probing question, answer it before moving to the trace/repro stage."
  ]
},
{
  id:"wf_stack_trace", category:"trace", builtin:true,
  title:"Stack Trace / Console Error Decoder",
  desc:"Turns a wall of red console text into a plain-language diagnosis anchored to your actual code.",
  tags:["stack-trace","errors"],
  template:
`Here is an error from my frontend app. Explain it in plain language, then map it to what's likely happening in my code.

Stack: {{project_context}}

Error / stack trace:
{{error_text}}

Relevant code (if any):
{{code_snippet}}

Give me:
1. A one-sentence plain-English translation of the error
2. The most likely line(s) or pattern in my code causing it
3. Whether this is likely a symptom of a deeper issue vs. an isolated bug`,
  variables:[
    {name:"error_text", label:"Error / stack trace", type:"textarea", placeholder:"Paste the full error and stack trace"},
    {name:"code_snippet", label:"Relevant code snippet", type:"textarea", placeholder:"Paste the function/component the error points to"},
  ],
  example:"Error: TypeError: Cannot read properties of undefined (reading 'map') at ProductList.tsx:42. Code: the products array is read from a Redux selector before the fetch resolves.",
  bestPractices:[
    "Always paste the full stack trace, not just the top line — the call chain often matters more than the message.",
    "Include the actual code the trace points to, not a paraphrase.",
    "Ask explicitly whether it's a symptom of something deeper — this catches root-cause vs. band-aid fixes."
  ]
},
{
  id:"wf_repro", category:"repro", builtin:true,
  title:"Minimal Reproduction Builder",
  desc:"Gets AI's help stripping a bug down to the smallest possible repro — the fastest way to actually understand it.",
  tags:["repro","isolation"],
  template:
`Help me build the smallest possible reproduction of this bug so I can isolate it from the rest of the app.

Stack: {{project_context}}

Bug summary: {{bug_summary}}
Current repro steps (may be too broad): {{repro_steps}}
Suspected component/module: {{suspected_area}}

Give me:
1. A minimal set of repro steps, stripped of anything unrelated
2. A tiny standalone code snippet (or sandbox-ready component) that reproduces it in isolation
3. What to remove next if this minimal version still doesn't isolate it cleanly`,
  variables:[
    {name:"bug_summary", label:"Bug summary", type:"textarea", placeholder:"One or two sentences"},
    {name:"repro_steps", label:"Current repro steps", type:"textarea", placeholder:"Whatever steps currently trigger it, even if broad"},
    {name:"suspected_area", label:"Suspected component / module", type:"text", placeholder:"e.g. CartContext, useCheckout hook"},
  ],
  example:"Bug: cart total is wrong after applying a discount code twice. Repro steps: full checkout flow, apply code, apply again. Suspected area: useDiscount hook.",
  bestPractices:[
    "Isolation is the goal — a fix built on a messy repro often fixes the wrong thing.",
    "Ask for a sandbox-ready snippet so you can actually verify the repro works before moving to the fix stage.",
    "If AI's minimal repro doesn't trigger the bug, that mismatch is itself useful diagnostic information."
  ]
},
{
  id:"wf_fix_verify", category:"fix", builtin:true,
  title:"Fix Proposal + Self-Review",
  desc:"Asks for a fix and a critique of that fix in the same pass, so you're not the only reviewer.",
  tags:["fix","review"],
  template:
`Propose a fix for this bug, then critique your own proposed fix before I apply it.

Stack: {{project_context}}

Confirmed root cause: {{root_cause}}
Constraints: {{constraints}}

Structure your answer as:
1. The proposed fix (code + explanation)
2. Edge cases this fix might not cover
3. Any risk of regression elsewhere in the codebase
4. How I should verify the fix actually works (specific test or manual steps)`,
  variables:[
    {name:"root_cause", label:"Confirmed root cause", type:"textarea", placeholder:"What triage/trace analysis confirmed"},
    {name:"constraints", label:"Constraints", type:"textarea", placeholder:"e.g. can't change the public API, must ship without a migration"},
  ],
  example:"Root cause: discount hook doesn't debounce rapid clicks, so the reducer applies the action twice. Constraints: can't touch the reducer's public shape, other components depend on it.",
  bestPractices:[
    "Never skip the self-critique step — it's what catches fixes that pass the happy path but break edge cases.",
    "Always ask for a concrete verification step, not just 'test it' — a specific test or manual sequence.",
    "State real constraints; a fix that technically works but breaks a constraint isn't usable."
  ]
},
{
  id:"wf_postmortem", category:"post", builtin:true,
  title:"Post-Mortem & Prevention Note",
  desc:"Closes the loop: turns a resolved bug into a short, reusable note so the same class of bug doesn't resurface.",
  tags:["post-mortem","prevention"],
  template:
`Write a short post-mortem for this bug, aimed at preventing similar bugs in the future — not a formal incident report, just a useful note for the team/repo.

Stack: {{project_context}}

Bug: {{bug_summary}}
Root cause: {{root_cause}}
Fix applied: {{fix_applied}}

Include:
1. A 2-3 sentence summary in plain language
2. The underlying pattern that caused it (so we recognize it next time)
3. One concrete guardrail we could add (lint rule, test, type, code review checklist item)`,
  variables:[
    {name:"bug_summary", label:"Bug summary", type:"textarea"},
    {name:"root_cause", label:"Root cause", type:"textarea"},
    {name:"fix_applied", label:"Fix applied", type:"textarea"},
  ],
  example:"Bug: discount applied twice on rapid double-click. Root cause: no debounce on the async action creator. Fix: added a pending-state guard. Guardrail: add an ESLint rule flagging async action creators without a pending guard.",
  bestPractices:[
    "Keep it short — a post-mortem nobody reads doesn't prevent anything.",
    "Always end with one concrete, actionable guardrail, not just a description of what happened.",
    "Save these in your saved workflows list so patterns become visible over time."
  ]
},
];

/* Prompt Builder block library */
const PB_BLOCKS = [
  {id:"role", title:"Role", icon:"◆", desc:"Tells the AI what persona/expertise to adopt. Sets the lens it reasons from — a 'senior frontend engineer' answers differently than a 'general assistant'.",
   field:{type:"select", options:["Senior frontend engineer","Staff engineer doing a design review","QA engineer hunting edge cases","Patient mentor explaining to a junior dev","Security-focused code reviewer","Custom…"]}},
  {id:"objective", title:"Objective", icon:"⊙", desc:"The single concrete outcome you want. Keeps the AI focused on one job instead of drifting into tangents.",
   field:{type:"textarea", placeholder:"e.g. Find why the cart total is off by one cent after applying a coupon"}},
  {id:"context", title:"Context", icon:"▤", desc:"Background the AI needs but shouldn't have to ask for — your stack, the file, prior attempts. Reduces back-and-forth.",
   field:{type:"textarea", placeholder:"e.g. React 18 + Redux Toolkit; bug appeared after upgrading to RTK 2.0"}},
  {id:"constraints", title:"Constraints", icon:"⊘", desc:"Hard limits the answer must respect — what NOT to change, performance budgets, style rules. Prevents technically-correct-but-unusable answers.",
   field:{type:"textarea", placeholder:"e.g. cannot change the public hook API; no new dependencies"}},
  {id:"reasoning", title:"Reasoning Strategy", icon:"∴", desc:"How the AI should think before answering — e.g. step-by-step, or list hypotheses before concluding. Improves accuracy on non-trivial problems.",
   field:{type:"select", options:["Think step-by-step before answering","List 3 hypotheses, rank by likelihood, then investigate the top one","Work backward from the expected output","Compare 2 possible approaches, then pick one and justify it","Custom…"]}},
  {id:"outputformat", title:"Output Format", icon:"▦", desc:"The exact shape you want the answer in. Removes ambiguity so you get something you can act on immediately, not a wall of prose.",
   field:{type:"select", options:["Numbered steps","Code diff only, no prose","Table: Cause | Evidence | Confidence","Short summary + collapsible detail","Bullet list, max 5 points","Custom…"]}},
  {id:"tone", title:"Tone", icon:"✦", desc:"The register of the response. Mostly matters for anything you'll paste into docs, PR comments, or send to teammates as-is.",
   field:{type:"select", options:["Direct and terse","Explain like I'm reviewing this for the first time","Formal, suitable for a PR comment","Casual, like a pairing session"]}},
  {id:"examples", title:"Examples", icon:"❝", desc:"A sample input/output pair. Anchors the AI's answer to a concrete pattern instead of a generic default.",
   field:{type:"textarea", placeholder:"e.g. Input: 'off by one' bugs in the past were usually inclusive/exclusive range errors"}},
  {id:"qualitycheck", title:"Quality Checks", icon:"✓", desc:"A checklist the AI should verify its own answer against before returning it. Catches obvious mistakes before you see them.",
   field:{type:"textarea", placeholder:"e.g. Does the fix handle the empty-cart case? Does it add a test?"}},
];

/* Loop Builder block library */
const LB_BLOCKS = [
  {id:"goal", title:"Goal", icon:"◎", desc:"What 'done' looks like for the whole loop, in one sentence. Everything else in the loop is measured against this.",
   field:{type:"textarea", placeholder:"e.g. All unit tests in checkout.test.js pass and no new lint errors are introduced"}},
  {id:"evalcriteria", title:"Evaluation Criteria", icon:"⚖", desc:"How the AI should judge each attempt — the specific, checkable signals that separate a good attempt from a bad one.",
   field:{type:"textarea", placeholder:"e.g. Run the test suite; check for TypeScript errors; confirm no unrelated files changed"}},
  {id:"improvestrategy", title:"Improvement Strategy", icon:"↗", desc:"What the AI should do differently on each retry if the previous attempt failed — prevents it from repeating the same failed approach.",
   field:{type:"select", options:["Change one variable at a time and re-test","Read the failure output and address only that specific failure","Try a fundamentally different approach after 2 failed attempts","Narrow scope further each retry until the failure is isolated","Custom…"]}},
  {id:"stopcond", title:"Stop Conditions", icon:"■", desc:"Exactly when the loop should stop — on success, after N attempts, or if it detects it's stuck. Prevents runaway or endless loops.",
   field:{type:"textarea", placeholder:"e.g. Stop after 5 attempts, or immediately once all tests pass, or if the same error repeats twice in a row"}},
  {id:"safety", title:"Safety Rules", icon:"⚠", desc:"Boundaries the AI must never cross while iterating — files it can't touch, actions that need your approval first. Keeps an autonomous loop from doing something risky.",
   field:{type:"textarea", placeholder:"e.g. Never modify files outside /src/checkout; never run destructive git commands; ask before installing new dependencies"}},
];

/* ============================================================
   STATE
   ============================================================ */
const LS = {
  ctx:"dl_context_profile", wf:"dl_user_workflows", fav:"dl_favorites",
  theme:"dl_theme", explainer:"dl_explainer_dismissed", onboarded:"dl_onboarded"
};
let state = {
  ctxProfile: JSON.parse(localStorage.getItem(LS.ctx) || "{}"),
  userWorkflows: JSON.parse(localStorage.getItem(LS.wf) || "[]"),
  favorites: JSON.parse(localStorage.getItem(LS.fav) || "[]"),
  search: "",
  activeFilter: "all",
  pbBlocks: [],
  lbBlocks: [],
  editingId: null,
};

function saveLS(){
  localStorage.setItem(LS.ctx, JSON.stringify(state.ctxProfile));
  localStorage.setItem(LS.wf, JSON.stringify(state.userWorkflows));
  localStorage.setItem(LS.fav, JSON.stringify(state.favorites));
}

function allWorkflows(){ return DEFAULT_WORKFLOWS.concat(state.userWorkflows); }

function escapeHtml(s){
  return (s||"").replace(/[&<>"']/g, c => ({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]));
}

function toast(msg){
  const t = document.getElementById("toast");
  t.textContent = "✓ " + msg;
  t.classList.add("show");
  clearTimeout(toast._h);
  toast._h = setTimeout(()=>t.classList.remove("show"), 1800);
}

function copyText(text){
  navigator.clipboard.writeText(text).then(()=>toast("Copied to clipboard")).catch(()=>{
    const ta=document.createElement("textarea"); ta.value=text; document.body.appendChild(ta);
    ta.select(); document.execCommand("copy"); document.body.removeChild(ta);
    toast("Copied to clipboard");
  });
}

/* ============================================================
   NAVIGATION
   ============================================================ */
const views = ["dashboard","workflows","promptbuilder","loopbuilder","saved"];
function showView(name){
  views.forEach(v=>{
    document.getElementById("view-"+v).classList.toggle("hidden", v!==name);
  });
  document.querySelectorAll(".navitem").forEach(b=>b.classList.toggle("active", b.dataset.view===name));
  document.getElementById("sidebar").classList.remove("open");
  if(name==="dashboard") renderDashboard();
  if(name==="workflows") renderWorkflowsView();
  if(name==="saved") renderSaved();
  if(name==="promptbuilder") renderPB();
  if(name==="loopbuilder") renderLB();
}
document.querySelectorAll(".navitem").forEach(b=>b.addEventListener("click", ()=>showView(b.dataset.view)));
document.getElementById("menuBtn").addEventListener("click", ()=>document.getElementById("sidebar").classList.toggle("open"));

/* ============================================================
   CONTEXT PROFILE
   ============================================================ */
function renderCtxGrid(){
  const grid = document.getElementById("ctxGrid");
  grid.innerHTML = CTX_FIELDS.map(f=>{
    const val = state.ctxProfile[f.key] || "";
    if(f.type==="select"){
      return `<div class="field"><label>${f.label}</label>
        <select data-ctxkey="${f.key}">
          <option value="">—</option>
          ${f.options.map(o=>`<option value="${escapeHtml(o)}" ${val===o?"selected":""}>${o}</option>`).join("")}
        </select></div>`;
    }
    if(f.type==="textarea"){
      return `<div class="field" style="grid-column:1/-1;"><label>${f.label}</label>
        <textarea data-ctxkey="${f.key}" placeholder="${escapeHtml(f.placeholder||"")}">${escapeHtml(val)}</textarea></div>`;
    }
    return `<div class="field"><label>${f.label}</label>
      <input data-ctxkey="${f.key}" value="${escapeHtml(val)}" placeholder="${escapeHtml(f.placeholder||"")}"></div>`;
  }).join("");
  grid.querySelectorAll("[data-ctxkey]").forEach(el=>{
    el.addEventListener("input", ()=>{
      state.ctxProfile[el.dataset.ctxkey] = el.value;
      saveLS();
      updateCtxStatus();
    });
  });
  updateCtxStatus();
}
function ctxSummary(){
  const parts = CTX_FIELDS.map(f=>state.ctxProfile[f.key]).filter(Boolean);
  return parts.length ? parts.join(" · ") : "";
}
function updateCtxStatus(){
  const el = document.getElementById("ctxStatus");
  const filled = CTX_FIELDS.filter(f=>state.ctxProfile[f.key]).length;
  if(filled===0){ el.textContent = "○ Not filled in yet — fill this out to auto-inject context into every template."; el.style.color="var(--text-faint)"; }
  else { el.textContent = `● Saved — ${filled}/${CTX_FIELDS.length} fields set. Auto-injected wherever a template uses {{project_context}}.`; el.style.color="var(--teal)"; }
}

/* ============================================================
   DASHBOARD
   ============================================================ */
function renderDashboard(){
  renderCtxGrid();
  const wfs = allWorkflows();
  const stats = document.getElementById("statsRow");
  stats.innerHTML = `
    <div class="statcard"><div class="statnum">${wfs.length}</div><div class="statlabel">Total workflows</div></div>
    <div class="statcard"><div class="statnum">${state.favorites.length}</div><div class="statlabel">Favorited</div></div>
    <div class="statcard"><div class="statnum">${state.userWorkflows.length}</div><div class="statlabel">Custom-built by you</div></div>
    <div class="statcard"><div class="statnum">${CATEGORIES.length}</div><div class="statlabel">Debugging stages covered</div></div>
  `;
  const cont = document.getElementById("dashboardCats");
  cont.innerHTML = "";
  CATEGORIES.forEach(cat=>{
    const items = wfs.filter(w=>w.category===cat.id);
    if(!items.length) return;
    const sec = document.createElement("div");
    sec.className = "cat-section";
    sec.innerHTML = `<div class="cat-header"><h2>${cat.name}</h2><span class="count">${items.length}</span><span class="catdesc">${cat.desc}</span></div>
      <div class="wf-grid">${items.map(wfCardHtml).join("")}</div>`;
    cont.appendChild(sec);
  });
  bindWfCards(cont);
}

/* ============================================================
   WORKFLOWS VIEW (filter + search)
   ============================================================ */
function renderFilterBar(){
  const bar = document.getElementById("filterBar");
  const chips = [{id:"all", name:"All"}, ...CATEGORIES];
  bar.innerHTML = chips.map(c=>`<button class="chip ${state.activeFilter===c.id?"active":""}" data-filter="${c.id}">${c.name}</button>`).join("");
  bar.querySelectorAll(".chip").forEach(b=>b.addEventListener("click", ()=>{
    state.activeFilter = b.dataset.filter;
    renderWorkflowsView();
  }));
}
function matchesSearch(w){
  if(!state.search) return true;
  const s = state.search.toLowerCase();
  return w.title.toLowerCase().includes(s) || w.desc.toLowerCase().includes(s) || (w.tags||[]).some(t=>t.toLowerCase().includes(s));
}
function renderWorkflowsView(){
  renderFilterBar();
  const cont = document.getElementById("workflowsAll");
  let wfs = allWorkflows().filter(matchesSearch);
  if(state.activeFilter!=="all") wfs = wfs.filter(w=>w.category===state.activeFilter);
  if(!wfs.length){
    cont.innerHTML = `<div class="empty">No workflows match your search or filter yet. Try a different term, or create a new workflow from the Prompt Builder.</div>`;
    return;
  }
  const grouped = {};
  wfs.forEach(w=>{ (grouped[w.category] = grouped[w.category]||[]).push(w); });
  cont.innerHTML = CATEGORIES.filter(c=>grouped[c.id]).map(cat=>`
    <div class="cat-section">
      <div class="cat-header"><h2>${cat.name}</h2><span class="count">${grouped[cat.id].length}</span><span class="catdesc">${cat.desc}</span></div>
      <div class="wf-grid">${grouped[cat.id].map(wfCardHtml).join("")}</div>
    </div>`).join("");
  bindWfCards(cont);
}

function wfCardHtml(w){
  const fav = state.favorites.includes(w.id);
  return `<div class="wf-card" data-id="${w.id}">
    <div class="wf-top">
      <div class="wf-title">${escapeHtml(w.title)}</div>
      <button class="wf-star ${fav?"active":""}" data-favid="${w.id}" title="Favorite">★</button>
    </div>
    <div class="wf-desc">${escapeHtml(w.desc)}</div>
    <div class="wf-tags">${(w.tags||[]).map(t=>`<span class="tag">${escapeHtml(t)}</span>`).join("")}${w.builtin?"":'<span class="tag">custom</span>'}</div>
  </div>`;
}
function bindWfCards(root){
  root.querySelectorAll(".wf-star").forEach(b=>{
    b.addEventListener("click", (e)=>{
      e.stopPropagation();
      const id = b.dataset.favid;
      const idx = state.favorites.indexOf(id);
      if(idx>-1) state.favorites.splice(idx,1); else state.favorites.push(id);
      saveLS();
      b.classList.toggle("active");
    });
  });
  root.querySelectorAll(".wf-card").forEach(c=>{
    c.addEventListener("click", ()=>openWfModal(c.dataset.id));
  });
}

/* ============================================================
   SAVED VIEW
   ============================================================ */
function renderSaved(){
  const cont = document.getElementById("savedList");
  const items = allWorkflows().filter(w=>state.favorites.includes(w.id) || !w.builtin);
  if(!items.length){
    cont.innerHTML = `<div class="empty">Nothing saved yet. Star a workflow, or build one in the Prompt/Loop Builder and click "Save as a reusable workflow".</div>`;
    return;
  }
  cont.innerHTML = `<div class="wf-grid">${items.map(wfCardHtml).join("")}</div>`;
  bindWfCards(cont);
}

/* ============================================================
   WORKFLOW DETAIL MODAL (fill variables, live template, copy)
   ============================================================ */
let currentWfFill = {};
function openWfModal(id){
  const w = allWorkflows().find(x=>x.id===id);
  if(!w) return;
  currentWfFill = {};
  document.getElementById("wfModalTitle").textContent = w.title;
  document.getElementById("wfModalDesc").textContent = w.desc;
  const body = document.getElementById("wfModalBody");
  let html = "";
  const vars = w.variables || [];
  if(vars.length){
    html += `<div class="section-label">Fill in the variables</div><div class="varfields">`;
    vars.forEach(v=>{
      html += `<div class="field" style="${v.type==='textarea'?'grid-column:1/-1;':''}">
        <label>${escapeHtml(v.label)}</label>
        ${v.type==='textarea'
          ? `<textarea data-var="${v.name}" placeholder="${escapeHtml(v.placeholder||"")}"></textarea>`
          : `<input data-var="${v.name}" placeholder="${escapeHtml(v.placeholder||"")}">`}
      </div>`;
    });
    html += `</div>`;
  }
  html += `<div class="section-label">Live template preview</div><div class="promptbox" id="wfLivePreview"></div>`;
  if(w.example){
    html += `<div class="section-label">Filled example</div><div class="example-box">${escapeHtml(w.example)}</div>`;
  }
  if(w.bestPractices && w.bestPractices.length){
    html += `<div class="section-label">Best practices</div><ul class="bp">${w.bestPractices.map(b=>`<li>${escapeHtml(b)}</li>`).join("")}</ul>`;
  }
  body.innerHTML = html;
  body.querySelectorAll("[data-var]").forEach(el=>{
    el.addEventListener("input", ()=>{ currentWfFill[el.dataset.var]=el.value; updateWfPreview(w); });
  });
  updateWfPreview(w);
  document.getElementById("wfOverlay").dataset.wfid = id;
  document.getElementById("wfOverlay").classList.remove("hidden");
}
function fillTemplate(template, fillMap){
  return template.replace(/\{\{(\w+)\}\}/g, (m, key)=>{
    if(key==="project_context") return ctxSummary() || "[fill in your Context Profile on the Dashboard]";
    return fillMap[key] || `[${key}]`;
  });
}
function updateWfPreview(w){
  const filled = fillTemplate(w.template, currentWfFill);
  document.getElementById("wfLivePreview").textContent = filled;
}
document.getElementById("wfModalClose").addEventListener("click", ()=>document.getElementById("wfOverlay").classList.add("hidden"));
document.getElementById("wfOverlay").addEventListener("click", (e)=>{ if(e.target.id==="wfOverlay") e.currentTarget.classList.add("hidden"); });
document.getElementById("wfCopyBtn").addEventListener("click", ()=>{
  const id = document.getElementById("wfOverlay").dataset.wfid;
  const w = allWorkflows().find(x=>x.id===id);
  copyText(fillTemplate(w.template, currentWfFill));
});
document.getElementById("wfDuplicateBtn").addEventListener("click", ()=>{
  const id = document.getElementById("wfOverlay").dataset.wfid;
  const w = allWorkflows().find(x=>x.id===id);
  const copy = JSON.parse(JSON.stringify(w));
  copy.id = "wf_custom_"+Date.now();
  copy.title = w.title + " (copy)";
  copy.builtin = false;
  state.userWorkflows.push(copy);
  saveLS();
  toast("Duplicated to My Saved Workflows");
  document.getElementById("wfOverlay").classList.add("hidden");
  showView("saved");
});
document.getElementById("wfEditBtn").addEventListener("click", ()=>{
  const id = document.getElementById("wfOverlay").dataset.wfid;
  document.getElementById("wfOverlay").classList.add("hidden");
  openEditModal(id);
});

/* ============================================================
   NEW / EDIT WORKFLOW MODAL
   ============================================================ */
function populateCategorySelect(){
  const sel = document.getElementById("editCategory");
  sel.innerHTML = CATEGORIES.map(c=>`<option value="${c.id}">${c.name}</option>`).join("");
}
function openEditModal(id){
  populateCategorySelect();
  state.editingId = id || null;
  const isNew = !id;
  document.getElementById("editModalTitle").textContent = isNew ? "New workflow" : "Edit workflow";
  if(isNew){
    document.getElementById("editTitle").value = "";
    document.getElementById("editCategory").value = "context";
    document.getElementById("editDesc").value = "";
    document.getElementById("editTemplate").value = "";
    document.getElementById("editBP").value = "";
  } else {
    const w = allWorkflows().find(x=>x.id===id);
    document.getElementById("editTitle").value = w.title;
    document.getElementById("editCategory").value = w.category;
    document.getElementById("editDesc").value = w.desc;
    document.getElementById("editTemplate").value = w.template;
    document.getElementById("editBP").value = (w.bestPractices||[]).join("\n");
  }
  document.getElementById("editOverlay").classList.remove("hidden");
}
document.getElementById("newWorkflowBtn").addEventListener("click", ()=>openEditModal(null));
document.getElementById("editModalClose").addEventListener("click", ()=>document.getElementById("editOverlay").classList.add("hidden"));
document.getElementById("editCancel").addEventListener("click", ()=>document.getElementById("editOverlay").classList.add("hidden"));
document.getElementById("editOverlay").addEventListener("click", (e)=>{ if(e.target.id==="editOverlay") e.currentTarget.classList.add("hidden"); });
document.getElementById("editSave").addEventListener("click", ()=>{
  const title = document.getElementById("editTitle").value.trim() || "Untitled workflow";
  const category = document.getElementById("editCategory").value;
  const desc = document.getElementById("editDesc").value.trim() || "Custom workflow.";
  const template = document.getElementById("editTemplate").value;
  const bp = document.getElementById("editBP").value.split("\n").map(s=>s.trim()).filter(Boolean);
  const varNames = Array.from(new Set((template.match(/\{\{(\w+)\}\}/g)||[]).map(m=>m.replace(/[{}]/g,"")))).filter(v=>v!=="project_context");
  const variables = varNames.map(n=>({name:n, label:n.replace(/_/g," ").replace(/\b\w/g,c=>c.toUpperCase()), type:"textarea", placeholder:""}));

  if(state.editingId){
    const idx = state.userWorkflows.findIndex(w=>w.id===state.editingId);
    if(idx>-1){
      state.userWorkflows[idx] = {...state.userWorkflows[idx], title, category, desc, template, bestPractices:bp, variables};
    } else {
      // editing a builtin -> fork it into user workflows
      state.userWorkflows.push({id:"wf_custom_"+Date.now(), builtin:false, title, category, desc, template, bestPractices:bp, variables, tags:["custom"]});
    }
  } else {
    state.userWorkflows.push({id:"wf_custom_"+Date.now(), builtin:false, title, category, desc, template, bestPractices:bp, variables, tags:["custom"]});
  }
  saveLS();
  document.getElementById("editOverlay").classList.add("hidden");
  toast("Workflow saved");
  showView("saved");
});

/* ============================================================
   PROMPT BUILDER
   ============================================================ */
function renderPB(){
  const picker = document.getElementById("pbPicker");
  picker.innerHTML = PB_BLOCKS.map(b=>{
    const added = state.pbBlocks.some(x=>x.blockId===b.id);
    return `<div class="block-choice ${added?"added":""}" data-block="${b.id}">
      <div class="bc-top"><div class="bc-title"><span class="bc-badge">${b.icon}</span>${b.title}</div><span class="bc-add">${added?"Added":"+ Add"}</span></div>
      <div class="bc-desc">${b.desc}</div>
    </div>`;
  }).join("");
  picker.querySelectorAll(".block-choice").forEach(el=>{
    el.addEventListener("click", ()=>{
      const id = el.dataset.block;
      if(state.pbBlocks.some(x=>x.blockId===id)) return;
      state.pbBlocks.push({blockId:id, value:"", customLabel:""});
      renderPB();
    });
  });
  renderPBAssembled();
  renderPBOutput();
}
function renderPBAssembled(){
  const cont = document.getElementById("pbAssembled");
  if(!state.pbBlocks.length){
    cont.innerHTML = `<div class="empty">No blocks added yet. Pick blocks from the left to start assembling your prompt.</div>`;
    return;
  }
  cont.innerHTML = state.pbBlocks.map((b,i)=>{
    const def = PB_BLOCKS.find(x=>x.id===b.blockId);
    let inputHtml = "";
    if(def.field.type==="select"){
      inputHtml = `<select data-i="${i}" data-role="select">
        <option value="">— choose —</option>
        ${def.field.options.map(o=>`<option value="${escapeHtml(o)}" ${b.value===o?"selected":""}>${o}</option>`).join("")}
      </select>`;
      if(b.value==="Custom…"){
        inputHtml += `<textarea data-i="${i}" data-role="custom" placeholder="Write your own...">${escapeHtml(b.customLabel||"")}</textarea>`;
      }
    } else {
      inputHtml = `<textarea data-i="${i}" data-role="text" placeholder="${escapeHtml(def.field.placeholder||"")}">${escapeHtml(b.value||"")}</textarea>`;
    }
    return `<div class="ablock">
      <div class="ablock-top"><span class="bc-badge">${def.icon}</span><span class="ablock-title">${def.title}</span><button class="ablock-remove" data-remove="${i}">✕ remove</button></div>
      <div class="ablock-hint">${def.desc}</div>
      ${inputHtml}
    </div>`;
  }).join("");
  cont.querySelectorAll("[data-role='select']").forEach(el=>{
    el.addEventListener("change", ()=>{ state.pbBlocks[+el.dataset.i].value = el.value; renderPBAssembled(); renderPBOutput(); });
  });
  cont.querySelectorAll("[data-role='custom']").forEach(el=>{
    el.addEventListener("input", ()=>{ state.pbBlocks[+el.dataset.i].customLabel = el.value; renderPBOutput(); });
  });
  cont.querySelectorAll("[data-role='text']").forEach(el=>{
    el.addEventListener("input", ()=>{ state.pbBlocks[+el.dataset.i].value = el.value; renderPBOutput(); });
  });
  cont.querySelectorAll("[data-remove]").forEach(el=>{
    el.addEventListener("click", ()=>{ state.pbBlocks.splice(+el.dataset.remove,1); renderPB(); });
  });
}
function pbBlockText(b){
  const def = PB_BLOCKS.find(x=>x.id===b.blockId);
  let val = b.value;
  if(val==="Custom…") val = b.customLabel;
  if(!val) return null;
  return `${def.title}: ${val}`;
}
function renderPBOutput(){
  const out = document.getElementById("pbOutput");
  const lines = state.pbBlocks.map(pbBlockText).filter(Boolean);
  out.textContent = lines.length ? lines.join("\n\n") : "Fill in the blocks on the left to see your assembled prompt here.";
}
document.getElementById("pbCopy").addEventListener("click", ()=>{
  const lines = state.pbBlocks.map(pbBlockText).filter(Boolean);
  if(!lines.length){ toast("Nothing to copy yet"); return; }
  copyText(lines.join("\n\n"));
});
document.getElementById("pbSave").addEventListener("click", ()=>{
  const lines = state.pbBlocks.map(pbBlockText).filter(Boolean);
  if(!lines.length){ toast("Add some blocks first"); return; }
  const template = lines.join("\n\n");
  state.userWorkflows.push({
    id:"wf_custom_"+Date.now(), builtin:false, category:"fix",
    title:"Custom prompt — "+new Date().toLocaleDateString(),
    desc:"Saved from the Prompt Builder.", template, variables:[], tags:["custom","prompt-builder"],
    bestPractices:[]
  });
  saveLS();
  toast("Saved to My Saved Workflows");
  showView("saved");
});

/* ============================================================
   LOOP BUILDER
   ============================================================ */
function renderLB(){
  const picker = document.getElementById("lbPicker");
  picker.innerHTML = LB_BLOCKS.map(b=>{
    const added = state.lbBlocks.some(x=>x.blockId===b.id);
    return `<div class="block-choice ${added?"added":""}" data-block="${b.id}">
      <div class="bc-top"><div class="bc-title"><span class="bc-badge">${b.icon}</span>${b.title}</div><span class="bc-add">${added?"Added":"+ Add"}</span></div>
      <div class="bc-desc">${b.desc}</div>
    </div>`;
  }).join("");
  picker.querySelectorAll(".block-choice").forEach(el=>{
    el.addEventListener("click", ()=>{
      const id = el.dataset.block;
      if(state.lbBlocks.some(x=>x.blockId===id)) return;
      state.lbBlocks.push({blockId:id, value:"", customLabel:""});
      renderLB();
    });
  });
  renderLBAssembled();
  renderLBOutput();
  document.getElementById("loopBase").oninput = renderLBOutput;
}
function renderLBAssembled(){
  const cont = document.getElementById("lbAssembled");
  if(!state.lbBlocks.length){
    cont.innerHTML = `<div class="empty">No loop rules added yet. Add Goal + Stop Conditions at minimum before saving a loop.</div>`;
    return;
  }
  cont.innerHTML = state.lbBlocks.map((b,i)=>{
    const def = LB_BLOCKS.find(x=>x.id===b.blockId);
    let inputHtml = "";
    if(def.field.type==="select"){
      inputHtml = `<select data-i="${i}" data-role="select">
        <option value="">— choose —</option>
        ${def.field.options.map(o=>`<option value="${escapeHtml(o)}" ${b.value===o?"selected":""}>${o}</option>`).join("")}
      </select>`;
      if(b.value==="Custom…"){
        inputHtml += `<textarea data-i="${i}" data-role="custom" placeholder="Write your own...">${escapeHtml(b.customLabel||"")}</textarea>`;
      }
    } else {
      inputHtml = `<textarea data-i="${i}" data-role="text" placeholder="${escapeHtml(def.field.placeholder||"")}">${escapeHtml(b.value||"")}</textarea>`;
    }
    return `<div class="ablock">
      <div class="ablock-top"><span class="bc-badge">${def.icon}</span><span class="ablock-title">${def.title}</span><button class="ablock-remove" data-remove="${i}">✕ remove</button></div>
      <div class="ablock-hint">${def.desc}</div>
      ${inputHtml}
    </div>`;
  }).join("");
  cont.querySelectorAll("[data-role='select']").forEach(el=>{
    el.addEventListener("change", ()=>{ state.lbBlocks[+el.dataset.i].value = el.value; renderLBAssembled(); renderLBOutput(); });
  });
  cont.querySelectorAll("[data-role='custom']").forEach(el=>{
    el.addEventListener("input", ()=>{ state.lbBlocks[+el.dataset.i].customLabel = el.value; renderLBOutput(); });
  });
  cont.querySelectorAll("[data-role='text']").forEach(el=>{
    el.addEventListener("input", ()=>{ state.lbBlocks[+el.dataset.i].value = el.value; renderLBOutput(); });
  });
  cont.querySelectorAll("[data-remove]").forEach(el=>{
    el.addEventListener("click", ()=>{ state.lbBlocks.splice(+el.dataset.remove,1); renderLB(); });
  });
}
function lbBlockText(b){
  const def = LB_BLOCKS.find(x=>x.id===b.blockId);
  let val = b.value;
  if(val==="Custom…") val = b.customLabel;
  if(!val) return null;
  return `${def.title}: ${val}`;
}
function assembledLoopText(){
  const base = document.getElementById("loopBase").value.trim();
  const lines = state.lbBlocks.map(lbBlockText).filter(Boolean);
  if(!base && !lines.length) return "";
  let out = "";
  if(base) out += `Task: ${base}\n\n`;
  out += `Work on this in a loop: attempt a solution, evaluate it against the criteria below, and retry until the stop conditions are met.\n\n`;
  out += lines.join("\n\n");
  return out;
}
function renderLBOutput(){
  const out = document.getElementById("lbOutput");
  const text = assembledLoopText();
  out.textContent = text || "Paste a base prompt and add loop blocks to begin.";
}
document.getElementById("lbCopy").addEventListener("click", ()=>{
  const text = assembledLoopText();
  if(!text){ toast("Nothing to copy yet"); return; }
  copyText(text);
});
document.getElementById("lbSave").addEventListener("click", ()=>{
  const text = assembledLoopText();
  if(!text){ toast("Add a base prompt and some blocks first"); return; }
  state.userWorkflows.push({
    id:"wf_custom_"+Date.now(), builtin:false, category:"fix",
    title:"Custom loop — "+new Date().toLocaleDateString(),
    desc:"Saved from the Loop Builder.", template:text, variables:[], tags:["custom","loop-builder"],
    bestPractices:["Review each iteration's diff before letting the loop continue.","Keep Safety Rules explicit — don't rely on the AI to infer boundaries."]
  });
  saveLS();
  toast("Saved to My Saved Workflows");
  showView("saved");
});

/* ============================================================
   SEARCH, EXPLAINER, HELP, THEME, ONBOARDING
   ============================================================ */
const searchInput = document.getElementById("searchInput");
searchInput.addEventListener("input", ()=>{
  state.search = searchInput.value;
  const activeView = document.querySelector(".navitem.active").dataset.view;
  if(activeView!=="workflows") showView("workflows"); else renderWorkflowsView();
});

if(localStorage.getItem(LS.explainer)==="1"){
  document.getElementById("explainerBanner").style.display = "none";
}
document.getElementById("closeExplainer").addEventListener("click", ()=>{
  document.getElementById("explainerBanner").style.display = "none";
  localStorage.setItem(LS.explainer, "1");
});

document.getElementById("helpBtn").addEventListener("click", ()=>document.getElementById("helpOverlay").classList.remove("hidden"));
document.getElementById("helpModalClose").addEventListener("click", ()=>document.getElementById("helpOverlay").classList.add("hidden"));
document.getElementById("helpOverlay").addEventListener("click", (e)=>{ if(e.target.id==="helpOverlay") e.currentTarget.classList.add("hidden"); });

function applyTheme(t){
  document.body.setAttribute("data-theme", t);
  localStorage.setItem(LS.theme, t);
}
applyTheme(localStorage.getItem(LS.theme) || "dark");
document.getElementById("themeBtn").addEventListener("click", ()=>{
  applyTheme(document.body.getAttribute("data-theme")==="dark" ? "light" : "dark");
});

if(!localStorage.getItem(LS.onboarded)){
  document.getElementById("onboardOverlay").classList.remove("hidden");
}
function closeOnboard(){
  document.getElementById("onboardOverlay").classList.add("hidden");
  localStorage.setItem(LS.onboarded, "1");
}
document.getElementById("onboardClose").addEventListener("click", closeOnboard);
document.getElementById("onboardStart").addEventListener("click", closeOnboard);

/* Import / Export */
document.getElementById("exportBtn").addEventListener("click", ()=>{
  const data = {ctxProfile:state.ctxProfile, userWorkflows:state.userWorkflows, favorites:state.favorites};
  const blob = new Blob([JSON.stringify(data,null,2)], {type:"application/json"});
  const a = document.createElement("a");
  a.href = URL.createObjectURL(blob);
  a.download = "debug-loop-backup.json";
  a.click();
  toast("Exported");
});
document.getElementById("importBtn").addEventListener("click", ()=>document.getElementById("importFile").click());
document.getElementById("importFile").addEventListener("change", (e)=>{
  const file = e.target.files[0];
  if(!file) return;
  const reader = new FileReader();
  reader.onload = ()=>{
    try{
      const data = JSON.parse(reader.result);
      if(data.ctxProfile) state.ctxProfile = data.ctxProfile;
      if(data.userWorkflows) state.userWorkflows = data.userWorkflows;
      if(data.favorites) state.favorites = data.favorites;
      saveLS();
      toast("Imported successfully");
      showView("dashboard");
    }catch(err){ toast("Import failed — invalid file"); }
  };
  reader.readAsText(file);
});

/* Keyboard shortcuts */
document.addEventListener("keydown", (e)=>{
  const tag = (e.target.tagName||"").toLowerCase();
  const typing = tag==="input"||tag==="textarea"||tag==="select";
  if(e.key==="Escape"){
    document.querySelectorAll(".overlay").forEach(o=>o.classList.add("hidden"));
    return;
  }
  if(typing) return;
  if(e.key==="/"){ e.preventDefault(); searchInput.focus(); }
  if(e.key.toLowerCase()==="n"){ openEditModal(null); }
  if(e.key.toLowerCase()==="t"){ applyTheme(document.body.getAttribute("data-theme")==="dark" ? "light" : "dark"); }
});

/* ============================================================
   INIT
   ============================================================ */
showView("dashboard");
})();
</script>
</body>
</html>
