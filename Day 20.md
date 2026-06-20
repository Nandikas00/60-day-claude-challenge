# Built an AI Face Puzzle Game using claude :

## Key Learnings :

- Learned how to use Claude for prompt-driven game development, converting a high-level idea into a working web application.
- Implemented camera access using the browser MediaDevices API to capture user photos directly within the game.
- Gained experience handling camera permissions, access denial states, and retry mechanisms for better user experience.
- Developed a face image scrambling algorithm by dividing captured images into puzzle pieces and shuffling them dynamically.
- Learned to manage game state, including move tracking, puzzle completion detection, and timer functionality.
- Implemented local storage to save and display best scores without requiring a backend.
- Improved understanding of HTML, CSS, and JavaScript integration for creating interactive browser-based games.
- Learned how to design a responsive and engaging UI with clear game instructions and feedback messages.
- Explored client-side image processing, ensuring user photos remain on the device and are never uploaded to external servers.
- Practiced iterative prompt engineering, refining prompts to generate cleaner code, improve features, and fix issues efficiently.

### HTML OF THE APPLICATION :
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Face Puzzle — Photobooth Slider</title>
<style>
  @font-face {
    font-family: 'FigDisplay';
    src: local('Arial Black');
    font-weight: 900;
  }

  :root{
    --bg: #15151a;
    --bg-soft: #1e1e26;
    --paper: #f5f0e6;
    --paper-dim: #e7e0d0;
    --ink: #1a1a1f;
    --accent: #ff5d3a;
    --accent-dim: #c8472a;
    --violet: #7c6fff;
    --green: #3ddc84;
    --line: rgba(245,240,230,0.14);
    --sprocket: rgba(245,240,230,0.35);
  }

  *{ box-sizing: border-box; }

  html, body{
    margin:0; padding:0;
    background: var(--bg);
    color: var(--paper);
    font-family: 'Courier New', ui-monospace, SFMono-Regular, Menlo, monospace;
    min-height: 100vh;
    overflow-x: hidden;
  }

  body{
    background-image:
      radial-gradient(circle at 15% 10%, rgba(124,111,255,0.10), transparent 40%),
      radial-gradient(circle at 85% 90%, rgba(255,93,58,0.10), transparent 45%);
    display:flex;
    flex-direction:column;
    align-items:center;
    padding: 24px 14px 60px;
  }

  .display{
    font-family: 'Arial Black', Impact, 'Helvetica Neue', sans-serif;
    font-weight: 900;
    letter-spacing: -0.02em;
    text-transform: uppercase;
  }

  /* ===== Header / film strip motif ===== */
  .filmstrip{
    width:100%;
    max-width: 720px;
    display:flex;
    align-items:center;
    gap:8px;
    margin-bottom: 6px;
  }
  .sprockets{
    display:flex;
    gap:6px;
    flex:1;
    overflow:hidden;
  }
  .sprockets span{
    width:9px; height:9px;
    border-radius:2px;
    background: var(--sprocket);
    flex: none;
  }

  header{
    width:100%;
    max-width: 720px;
    text-align:center;
    margin: 4px 0 22px;
  }
  header h1{
    font-size: clamp(2rem, 7vw, 3.4rem);
    margin: 6px 0 4px;
    line-height: 0.92;
  }
  header h1 span{ color: var(--accent); }
  header p{
    margin:0;
    font-size: 0.8rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--paper-dim);
    opacity:0.7;
  }

  .stage{
    width:100%;
    max-width: 720px;
    background: var(--bg-soft);
    border: 1px solid var(--line);
    border-radius: 18px;
    padding: 20px;
    position: relative;
    box-shadow: 0 30px 60px -30px rgba(0,0,0,0.6);
  }

  .stage::before{
    content:"";
    position:absolute;
    inset:0;
    border-radius: 18px;
    padding:1px;
    pointer-events:none;
  }

  /* ===== Screens ===== */
  .screen{ display:none; width:100%; }
  .screen.active{ display:flex; flex-direction:column; align-items:center; gap:16px; }

  /* ===== Camera screen ===== */
  .video-wrap{
    position:relative;
    width:100%;
    max-width: 480px;
    aspect-ratio: 4/3;
    background:#000;
    border-radius: 14px;
    overflow:hidden;
    border: 2px solid var(--line);
  }
  #video{
    width:100%; height:100%;
    object-fit: cover;
    transform: scaleX(-1);
    display:block;
  }
  .video-wrap .corner-tag{
    position:absolute; top:10px; left:10px;
    background: rgba(255,93,58,0.9);
    color:#fff;
    font-size:0.65rem;
    padding:3px 8px;
    border-radius:4px;
    letter-spacing:0.08em;
    text-transform:uppercase;
    display:flex; align-items:center; gap:5px;
  }
  .corner-tag .dot{
    width:6px;height:6px;border-radius:50%;
    background:#fff;
    animation: blink 1.4s infinite;
  }
  @keyframes blink{ 50%{ opacity:0.25; } }

  #canvasSnap{ display:none; }

  .cam-error{
    width:100%;
    max-width: 480px;
    background: rgba(255,93,58,0.08);
    border: 1px dashed var(--accent);
    border-radius: 14px;
    padding: 22px;
    text-align:center;
    font-size: 0.85rem;
    line-height:1.6;
    color: var(--paper);
    display:none;
  }
  .cam-error.show{ display:block; }
  .cam-error b{ color: var(--accent); display:block; margin-bottom:6px; font-size:1rem; }

  /* ===== Buttons ===== */
  .btn-row{
    display:flex;
    gap:10px;
    flex-wrap:wrap;
    justify-content:center;
    width:100%;
  }
  button{
    font-family: inherit;
    cursor:pointer;
    border:none;
    border-radius: 10px;
    padding: 12px 22px;
    font-size: 0.85rem;
    font-weight:700;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    transition: transform 0.12s ease, filter 0.12s ease, box-shadow 0.12s ease;
  }
  button:active{ transform: translateY(1px) scale(0.98); }
  button:focus-visible{
    outline: 2px solid var(--violet);
    outline-offset: 2px;
  }

  .btn-primary{
    background: var(--accent);
    color: #fff;
    box-shadow: 0 8px 20px -8px rgba(255,93,58,0.7);
  }
  .btn-primary:hover{ filter:brightness(1.08); }

  .btn-secondary{
    background: transparent;
    color: var(--paper);
    border: 1px solid var(--line);
  }
  .btn-secondary:hover{ background: rgba(245,240,230,0.06); }

  .btn-ghost{
    background: rgba(124,111,255,0.12);
    color: var(--violet);
    border: 1px solid rgba(124,111,255,0.4);
  }
  .btn-ghost:hover{ background: rgba(124,111,255,0.22); }

  button:disabled{
    opacity:0.4;
    cursor:not-allowed;
    filter:none !important;
    transform:none !important;
  }

  /* ===== Difficulty screen ===== */
  .preview-thumb{
    width:160px; height:160px;
    border-radius:12px;
    overflow:hidden;
    border: 2px solid var(--line);
    box-shadow: 0 10px 24px -10px rgba(0,0,0,0.6);
  }
  .preview-thumb img{ width:100%; height:100%; object-fit:cover; display:block; }

  .diff-grid{
    display:flex;
    gap:12px;
    flex-wrap:wrap;
    justify-content:center;
  }
  .diff-card{
    background: var(--bg);
    border: 1px solid var(--line);
    border-radius: 12px;
    padding: 16px 20px;
    text-align:center;
    cursor:pointer;
    width: 120px;
    transition: border-color 0.15s ease, transform 0.15s ease;
  }
  .diff-card:hover{ border-color: var(--accent); transform: translateY(-2px); }
  .diff-card.selected{ border-color: var(--green); box-shadow: 0 0 0 1px var(--green); }
  .diff-card .num{
    font-family: 'Arial Black', sans-serif;
    font-weight:900;
    font-size: 1.8rem;
    color: var(--accent);
    line-height:1;
  }
  .diff-card .lbl{
    font-size: 0.65rem;
    text-transform:uppercase;
    letter-spacing:0.08em;
    color: var(--paper-dim);
    margin-top:4px;
  }

  /* ===== Game HUD ===== */
  .hud{
    width:100%;
    display:flex;
    justify-content:space-between;
    align-items:center;
    flex-wrap:wrap;
    gap:10px;
    background: var(--bg);
    border: 1px solid var(--line);
    border-radius: 12px;
    padding: 10px 16px;
  }
  .hud-item{
    text-align:center;
    flex:1;
    min-width: 80px;
  }
  .hud-item .val{
    font-family: 'Arial Black', sans-serif;
    font-weight:900;
    font-size: 1.25rem;
    color: var(--paper);
    letter-spacing: 0.02em;
  }
  .hud-item .val.accent{ color: var(--accent); }
  .hud-item .val.green{ color: var(--green); }
  .hud-item .lbl{
    font-size: 0.6rem;
    text-transform:uppercase;
    letter-spacing:0.1em;
    color: var(--paper-dim);
    opacity:0.7;
  }
  .hud-divider{
    width:1px; height:30px;
    background: var(--line);
  }

  /* ===== Puzzle board ===== */
  .board-wrap{
    position:relative;
    width:100%;
    max-width: 480px;
    aspect-ratio: 1/1;
  }
  .board{
    position:relative;
    width:100%;
    height:100%;
    background: #000;
    border-radius: 10px;
    overflow:hidden;
    border: 2px solid var(--line);
    touch-action: none;
    user-select:none;
  }
  .piece{
    position:absolute;
    background-repeat:no-repeat;
    box-sizing:border-box;
    border: 1px solid rgba(0,0,0,0.35);
    cursor:grab;
    transition: top 0.18s cubic-bezier(.2,.8,.3,1), left 0.18s cubic-bezier(.2,.8,.3,1), box-shadow 0.15s ease, border-color 0.15s ease;
    will-change: top, left;
  }
  .piece.dragging{
    cursor:grabbing;
    z-index: 50;
    border: 3px solid var(--violet);
    box-shadow: 0 14px 30px -10px rgba(124,111,255,0.7);
    transition: box-shadow 0.15s ease, border-color 0.15s ease;
  }
  .piece.correct{
    border: 3px solid var(--green);
    box-shadow: 0 0 0 2px rgba(61,220,132,0.25) inset;
  }
  .piece .num-badge{
    position:absolute;
    top:2px; left:2px;
    background: rgba(0,0,0,0.55);
    color: #fff;
    font-size: 9px;
    line-height:1;
    padding: 2px 4px;
    border-radius: 3px;
    pointer-events:none;
    opacity: 0.0;
    transition: opacity 0.15s ease;
  }
  .board.show-numbers .piece .num-badge{ opacity: 1; }

  .board-actions{
    width:100%;
    display:flex;
    justify-content:center;
    margin-top: 4px;
  }
  .toggle-numbers{
    font-size: 0.7rem;
    color: var(--paper-dim);
    display:flex;
    align-items:center;
    gap:6px;
    cursor:pointer;
    user-select:none;
  }
  .toggle-numbers input{ accent-color: var(--violet); }

  /* ===== Win overlay ===== */
  .win-overlay{
    position:fixed;
    inset:0;
    background: rgba(10,10,12,0.86);
    backdrop-filter: blur(6px);
    display:none;
    align-items:center;
    justify-content:center;
    z-index: 200;
    padding: 16px;
  }
  .win-overlay.show{ display:flex; }
  .win-card{
    background: var(--bg-soft);
    border: 1px solid var(--line);
    border-radius: 18px;
    padding: 28px 26px 22px;
    width: 100%;
    max-width: 420px;
    text-align:center;
    box-shadow: 0 40px 80px -20px rgba(0,0,0,0.7);
    animation: pop 0.35s cubic-bezier(.2,.9,.3,1.2);
  }
  @keyframes pop{
    from{ transform: scale(0.85); opacity:0; }
    to{ transform: scale(1); opacity:1; }
  }
  .win-card .tag{
    font-size:0.7rem;
    letter-spacing:0.16em;
    text-transform:uppercase;
    color: var(--accent);
    margin-bottom: 4px;
  }
  .win-card h2{
    font-family: 'Arial Black', sans-serif;
    font-weight:900;
    font-size: 2.1rem;
    margin: 0 0 14px;
  }
  .win-thumb{
    width:120px; height:120px;
    margin: 0 auto 14px;
    border-radius:10px;
    overflow:hidden;
    border: 2px solid var(--green);
  }
  .win-thumb img{ width:100%; height:100%; object-fit:cover; }

  .win-stats{
    display:flex;
    justify-content:space-around;
    margin: 10px 0 18px;
    gap:8px;
  }
  .win-stats div{ flex:1; }
  .win-stats .v{
    font-family:'Arial Black', sans-serif;
    font-weight:900;
    font-size: 1.3rem;
    color: var(--paper);
  }
  .win-stats .l{
    font-size:0.6rem;
    text-transform:uppercase;
    letter-spacing:0.08em;
    color: var(--paper-dim);
    opacity:0.7;
  }

  .new-best{
    display:none;
    background: rgba(61,220,132,0.12);
    color: var(--green);
    border: 1px solid rgba(61,220,132,0.4);
    border-radius: 8px;
    padding: 6px 10px;
    font-size: 0.72rem;
    letter-spacing:0.06em;
    text-transform:uppercase;
    margin-bottom: 14px;
  }
  .new-best.show{ display:inline-block; }

  /* ===== Leaderboard ===== */
  .leaderboard{
    width:100%;
    max-width: 720px;
    margin-top: 26px;
  }
  .leaderboard h3{
    font-family:'Arial Black', sans-serif;
    font-weight:900;
    text-transform:uppercase;
    font-size: 1rem;
    letter-spacing: 0.04em;
    color: var(--paper-dim);
    margin: 0 0 10px;
    display:flex;
    align-items:center;
    gap:8px;
  }
  .leaderboard h3::before{
    content:"";
    width:8px;height:8px;
    background:var(--accent);
    border-radius:50%;
    display:inline-block;
  }
  table.lb{
    width:100%;
    border-collapse: collapse;
    font-size: 0.78rem;
    background: var(--bg-soft);
    border: 1px solid var(--line);
    border-radius: 12px;
    overflow:hidden;
  }
  table.lb th, table.lb td{
    padding: 9px 10px;
    text-align:left;
    border-bottom: 1px solid var(--line);
  }
  table.lb th{
    color: var(--paper-dim);
    text-transform:uppercase;
    font-size: 0.62rem;
    letter-spacing:0.08em;
    font-weight:700;
  }
  table.lb tr:last-child td{ border-bottom:none; }
  table.lb td.rank{ color: var(--accent); font-weight:700; width: 26px; }
  table.lb td.empty{
    text-align:center;
    color: var(--paper-dim);
    opacity:0.6;
    padding: 18px;
  }

  .footer-note{
    margin-top: 30px;
    font-size: 0.65rem;
    color: var(--paper-dim);
    opacity:0.45;
    text-align:center;
    letter-spacing:0.04em;
  }

  @media (max-width: 480px){
    .stage{ padding: 14px; border-radius: 14px; }
    .hud-item{ min-width: 70px; }
  }
</style>
</head>
<body>

<div class="filmstrip">
  <div class="sprockets" id="sprocketsTop"></div>
</div>

<header>
  <h1>FACE<span>SHUFFLE</span></h1>
  <p>snap a photo &middot; scramble it &middot; piece yourself back together</p>
</header>

<div class="stage">

  <!-- ===================== SCREEN 1: CAMERA ===================== -->
  <div class="screen active" id="screen-camera">
    <div class="video-wrap" id="videoWrap">
      <video id="video" autoplay playsinline muted></video>
      <div class="corner-tag"><span class="dot"></span> LIVE</div>
    </div>
    <div class="cam-error" id="camError">
      <b>Camera unavailable</b>
      <span id="camErrorMsg">We couldn't access your webcam. Please allow camera permission and reload, or check that no other app is using the camera.</span>
    </div>
    <canvas id="canvasSnap"></canvas>
    <div class="btn-row">
      <button class="btn-primary" id="btnSnap" disabled>📸 Take Photo</button>
      <button class="btn-secondary" id="btnRetryCam" style="display:none;">Retry Camera</button>
    </div>
  </div>

  <!-- ===================== SCREEN 2: DIFFICULTY ===================== -->
  <div class="screen" id="screen-difficulty">
    <div class="preview-thumb"><img id="snapPreview" alt="Your snapshot"></div>
    <div class="diff-grid">
      <div class="diff-card" data-size="3">
        <div class="num">3×3</div>
        <div class="lbl">Easy</div>
      </div>
      <div class="diff-card selected" data-size="4">
        <div class="num">4×4</div>
        <div class="lbl">Medium</div>
      </div>
      <div class="diff-card" data-size="5">
        <div class="num">5×5</div>
        <div class="lbl">Hard</div>
      </div>
    </div>
    <div class="btn-row">
      <button class="btn-secondary" id="btnRetake1">Retake Photo</button>
      <button class="btn-primary" id="btnStartPuzzle">Start Puzzle ▶</button>
    </div>
  </div>

  <!-- ===================== SCREEN 3: GAME ===================== -->
  <div class="screen" id="screen-game">
    <div class="hud">
      <div class="hud-item">
        <div class="val accent" id="hudTime">00:00.0</div>
        <div class="lbl">Time</div>
      </div>
      <div class="hud-divider"></div>
      <div class="hud-item">
        <div class="val" id="hudMoves">0</div>
        <div class="lbl">Moves</div>
      </div>
      <div class="hud-divider"></div>
      <div class="hud-item">
        <div class="val green" id="hudCorrect">0 / 0</div>
        <div class="lbl">Placed</div>
      </div>
      <div class="hud-divider"></div>
      <div class="hud-item">
        <div class="val" id="hudDiff">4×4</div>
        <div class="lbl">Grid</div>
      </div>
    </div>

    <div class="board-wrap">
      <div class="board" id="board"></div>
    </div>

    <div class="board-actions">
      <label class="toggle-numbers"><input type="checkbox" id="toggleNumbers"> show piece numbers</label>
    </div>

    <div class="btn-row">
      <button class="btn-secondary" id="btnRetake2">Retake Photo</button>
      <button class="btn-ghost" id="btnNewPhotoGame">New Photo</button>
      <button class="btn-secondary" id="btnShuffleAgain">Reshuffle</button>
    </div>
  </div>

</div>

<div class="leaderboard">
  <h3>Best Times</h3>
  <table class="lb">
    <thead>
      <tr><th>#</th><th>Time</th><th>Moves</th><th>Grid</th><th>Date</th></tr>
    </thead>
    <tbody id="lbBody">
      <tr><td class="empty" colspan="5">No times saved yet — finish a puzzle to set a record!</td></tr>
    </tbody>
  </table>
</div>

<div class="footer-note">All processing happens locally in your browser. No photos or video ever leave your device.</div>

<!-- ===================== WIN OVERLAY ===================== -->
<div class="win-overlay" id="winOverlay">
  <div class="win-card">
    <div class="tag">Puzzle Complete</div>
    <h2>NICE WORK!</h2>
    <div class="win-thumb"><img id="winThumb" alt="Completed face"></div>
    <div class="new-best" id="newBestBadge">★ New Top-5 Time!</div>
    <div class="win-stats">
      <div><div class="v" id="winTime">00:00.0</div><div class="l">Time</div></div>
      <div><div class="v" id="winMoves">0</div><div class="l">Moves</div></div>
      <div><div class="v" id="winDiff">4×4</div><div class="l">Grid</div></div>
    </div>
    <div class="btn-row">
      <button class="btn-primary" id="btnPlayAgain">🔁 Play Again</button>
      <button class="btn-secondary" id="btnNewPhotoWin">📷 New Photo</button>
    </div>
  </div>
</div>

<script>
(function(){
  "use strict";

  /* ---------------------------------------------------------------
     Decorative sprocket holes for the film-strip header
  --------------------------------------------------------------- */
  var sprocketsTop = document.getElementById('sprocketsTop');
  for (var s = 0; s < 60; s++){
    var sp = document.createElement('span');
    sprocketsTop.appendChild(sp);
  }

  /* ---------------------------------------------------------------
     Element refs
  --------------------------------------------------------------- */
  var video = document.getElementById('video');
  var btnSnap = document.getElementById('btnSnap');
  var btnRetryCam = document.getElementById('btnRetryCam');
  var camError = document.getElementById('camError');
  var camErrorMsg = document.getElementById('camErrorMsg');
  var videoWrap = document.getElementById('videoWrap');
  var canvasSnap = document.getElementById('canvasSnap');

  var screenCamera = document.getElementById('screen-camera');
  var screenDifficulty = document.getElementById('screen-difficulty');
  var screenGame = document.getElementById('screen-game');

  var snapPreview = document.getElementById('snapPreview');
  var diffCards = document.querySelectorAll('.diff-card');
  var btnRetake1 = document.getElementById('btnRetake1');
  var btnStartPuzzle = document.getElementById('btnStartPuzzle');

  var board = document.getElementById('board');
  var hudTime = document.getElementById('hudTime');
  var hudMoves = document.getElementById('hudMoves');
  var hudCorrect = document.getElementById('hudCorrect');
  var hudDiff = document.getElementById('hudDiff');
  var toggleNumbers = document.getElementById('toggleNumbers');

  var btnRetake2 = document.getElementById('btnRetake2');
  var btnNewPhotoGame = document.getElementById('btnNewPhotoGame');
  var btnShuffleAgain = document.getElementById('btnShuffleAgain');

  var winOverlay = document.getElementById('winOverlay');
  var winThumb = document.getElementById('winThumb');
  var winTime = document.getElementById('winTime');
  var winMoves = document.getElementById('winMoves');
  var winDiff = document.getElementById('winDiff');
  var newBestBadge = document.getElementById('newBestBadge');
  var btnPlayAgain = document.getElementById('btnPlayAgain');
  var btnNewPhotoWin = document.getElementById('btnNewPhotoWin');

  var lbBody = document.getElementById('lbBody');

  /* ---------------------------------------------------------------
     State
  --------------------------------------------------------------- */
  var stream = null;
  var capturedDataUrl = null;
  var gridSize = 4;
  var pieces = [];          // array of piece objects, index = current array order (not used for logic)
  var cellPx = 0;
  var boardPx = 0;
  var totalPieces = 0;
  var moveCount = 0;
  var correctCount = 0;
  var timerStart = null;
  var timerInterval = null;
  var elapsedFrozen = 0;
  var puzzleActive = false;
  var dragState = null;

  var LB_KEY = 'facePuzzleLeaderboard_v1';

  /* ---------------------------------------------------------------
     Screen switching
  --------------------------------------------------------------- */
  function showScreen(el){
    [screenCamera, screenDifficulty, screenGame].forEach(function(s){
      s.classList.remove('active');
    });
    el.classList.add('active');
  }

  /* ---------------------------------------------------------------
     CAMERA
  --------------------------------------------------------------- */
  function startCamera(){
    camError.classList.remove('show');
    btnRetryCam.style.display = 'none';
    btnSnap.disabled = true;

    if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia){
      handleCameraError({ name: 'NotSupportedError', message: 'getUserMedia is not supported in this browser.' });
      return;
    }

    var constraints = {
      video: { facingMode: 'user', width: { ideal: 1280 }, height: { ideal: 960 } },
      audio: false
    };

    navigator.mediaDevices.getUserMedia(constraints)
      .then(function(s){
        stream = s;
        video.srcObject = stream;
        videoWrap.style.display = '';
        camError.classList.remove('show');
        btnSnap.disabled = false;
      })
      .catch(function(err){
        handleCameraError(err);
      });
  }

  function handleCameraError(err){
    var msg = "We couldn't access your webcam. Please allow camera permission and reload, or check that no other app is using the camera.";
    if (err && err.name){
      if (err.name === 'NotAllowedError' || err.name === 'PermissionDeniedError'){
        msg = "Camera permission was denied. Please allow camera access in your browser's site settings, then click Retry Camera.";
      } else if (err.name === 'NotFoundError' || err.name === 'DevicesNotFoundError'){
        msg = "No camera was found on this device. Please connect a webcam and try again.";
      } else if (err.name === 'NotReadableError' || err.name === 'TrackStartError'){
        msg = "Your camera is already in use by another application. Close it and click Retry Camera.";
      } else if (err.name === 'NotSupportedError'){
        msg = "This browser doesn't support camera access, or the page isn't served over HTTPS/localhost.";
      } else if (err.name === 'SecurityError'){
        msg = "Camera access requires a secure (HTTPS) connection or localhost.";
      }
    }
    camErrorMsg.textContent = msg;
    camError.classList.add('show');
    videoWrap.style.display = 'none';
    btnSnap.disabled = true;
    btnRetryCam.style.display = '';
  }

  function stopCamera(){
    if (stream){
      stream.getTracks().forEach(function(t){ t.stop(); });
      stream = null;
    }
  }

  btnRetryCam.addEventListener('click', startCamera);

  btnSnap.addEventListener('click', function(){
    if (!stream) return;
    var vw = video.videoWidth || 640;
    var vh = video.videoHeight || 480;
    var side = Math.min(vw, vh);
    var sx = (vw - side) / 2;
    var sy = (vh - side) / 2;

    canvasSnap.width = 720;
    canvasSnap.height = 720;
    var ctx = canvasSnap.getContext('2d');
    ctx.save();
    // Mirror to match the preview (front camera feels natural mirrored)
    ctx.translate(canvasSnap.width, 0);
    ctx.scale(-1, 1);
    ctx.drawImage(video, sx, sy, side, side, 0, 0, canvasSnap.width, canvasSnap.height);
    ctx.restore();

    capturedDataUrl = canvasSnap.toDataURL('image/png');
    snapPreview.src = capturedDataUrl;

    stopCamera();
    showScreen(screenDifficulty);
  });

  /* ---------------------------------------------------------------
     DIFFICULTY SELECTION
  --------------------------------------------------------------- */
  diffCards.forEach(function(card){
    card.addEventListener('click', function(){
      diffCards.forEach(function(c){ c.classList.remove('selected'); });
      card.classList.add('selected');
      gridSize = parseInt(card.getAttribute('data-size'), 10);
    });
  });

  btnRetake1.addEventListener('click', function(){
    showScreen(screenCamera);
    startCamera();
  });

  btnStartPuzzle.addEventListener('click', function(){
    hudDiff.textContent = gridSize + '×' + gridSize;
    showScreen(screenGame);
    buildPuzzle();
  });

  /* ---------------------------------------------------------------
     PUZZLE BUILD
  --------------------------------------------------------------- */
  function measureBoard(){
    var rect = board.getBoundingClientRect();
    boardPx = rect.width;
    cellPx = boardPx / gridSize;
  }

  function buildPuzzle(){
    board.innerHTML = '';
    pieces = [];
    moveCount = 0;
    correctCount = 0;
    totalPieces = gridSize * gridSize;
    hudMoves.textContent = '0';
    updateCorrectHud();
    measureBoard();

    // Build ordered list of correct (row,col) positions
    var correctPositions = [];
    for (var r = 0; r < gridSize; r++){
      for (var c = 0; c < gridSize; c++){
        correctPositions.push({ row: r, col: c });
      }
    }

    // Create a solvable scramble: start solved, perform many random adjacent-ish swaps
    // (simple random permutation is fine since this is a free-swap puzzle, not a sliding 15-puzzle —
    // any permutation is solvable because pieces can swap with any other piece freely.)
    var order = correctPositions.map(function(_, i){ return i; });
    shuffleArray(order);

    // Guard against an already-solved shuffle (especially likely on 3x3)
    var isIdentity = order.every(function(v, i){ return v === i; });
    if (isIdentity){
      // swap first two
      var tmp = order[0]; order[0] = order[1]; order[1] = tmp;
    }

    for (var i = 0; i < totalPieces; i++){
      var correctIdx = i;
      var correctPos = correctPositions[correctIdx];
      var currentPos = correctPositions[order[i]];

      var piece = document.createElement('div');
      piece.className = 'piece';
      piece.style.width = cellPx + 'px';
      piece.style.height = cellPx + 'px';
      piece.style.backgroundImage = 'url(' + capturedDataUrl + ')';
      piece.style.backgroundSize = (cellPx * gridSize) + 'px ' + (cellPx * gridSize) + 'px';
      piece.style.backgroundPosition = (-correctPos.col * cellPx) + 'px ' + (-correctPos.row * cellPx) + 'px';
      piece.style.left = (currentPos.col * cellPx) + 'px';
      piece.style.top = (currentPos.row * cellPx) + 'px';

      var badge = document.createElement('div');
      badge.className = 'num-badge';
      badge.textContent = (correctIdx + 1);
      piece.appendChild(badge);

      piece.dataset.correctRow = correctPos.row;
      piece.dataset.correctCol = correctPos.col;
      piece.dataset.curRow = currentPos.row;
      piece.dataset.curCol = currentPos.col;

      attachDragHandlers(piece);
      board.appendChild(piece);
      pieces.push(piece);
    }

    refreshCorrectness();
    startTimer();
    puzzleActive = true;
  }

  function shuffleArray(arr){
    for (var i = arr.length - 1; i > 0; i--){
      var j = Math.floor(Math.random() * (i + 1));
      var t = arr[i]; arr[i] = arr[j]; arr[j] = t;
    }
  }

  window.addEventListener('resize', function(){
    if (!screenGame.classList.contains('active')) return;
    measureBoard();
    pieces.forEach(function(p){
      p.style.width = cellPx + 'px';
      p.style.height = cellPx + 'px';
      p.style.backgroundSize = (cellPx * gridSize) + 'px ' + (cellPx * gridSize) + 'px';
      var cc = parseInt(p.dataset.correctCol, 10);
      var cr = parseInt(p.dataset.correctRow, 10);
      p.style.backgroundPosition = (-cc * cellPx) + 'px ' + (-cr * cellPx) + 'px';
      var curR = parseInt(p.dataset.curRow, 10);
      var curC = parseInt(p.dataset.curCol, 10);
      p.style.left = (curC * cellPx) + 'px';
      p.style.top = (curR * cellPx) + 'px';
    });
  });

  /* ---------------------------------------------------------------
     DRAG & TOUCH HANDLING
  --------------------------------------------------------------- */
  function attachDragHandlers(piece){
    piece.addEventListener('mousedown', function(e){
      e.preventDefault();
      beginDrag(piece, e.clientX, e.clientY);
    });
    piece.addEventListener('touchstart', function(e){
      var t = e.touches[0];
      beginDrag(piece, t.clientX, t.clientY);
    }, { passive: true });
  }

  function beginDrag(piece, clientX, clientY){
    if (!puzzleActive) return;
    var boardRect = board.getBoundingClientRect();
    var pieceRect = piece.getBoundingClientRect();

    dragState = {
      piece: piece,
      offsetX: clientX - pieceRect.left,
      offsetY: clientY - pieceRect.top,
      boardRect: boardRect,
      startLeft: parseFloat(piece.style.left),
      startTop: parseFloat(piece.style.top)
    };

    piece.classList.add('dragging');
    piece.style.transition = 'box-shadow 0.15s ease, border-color 0.15s ease';

    document.addEventListener('mousemove', onDragMove);
    document.addEventListener('mouseup', onDragEnd);
    document.addEventListener('touchmove', onDragMove, { passive: false });
    document.addEventListener('touchend', onDragEnd);
  }

  function getPointFromEvent(e){
    if (e.touches && e.touches.length){
      return { x: e.touches[0].clientX, y: e.touches[0].clientY };
    }
    return { x: e.clientX, y: e.clientY };
  }

  function onDragMove(e){
    if (!dragState) return;
    if (e.type === 'touchmove') e.preventDefault();
    var pt = getPointFromEvent(e);
    var rect = dragState.boardRect;
    var newLeft = pt.x - rect.left - dragState.offsetX;
    var newTop = pt.y - rect.top - dragState.offsetY;

    // Clamp within board bounds (allow slight overhang for feel)
    var maxLeft = boardPx - cellPx;
    var maxTop = boardPx - cellPx;
    newLeft = Math.max(-cellPx * 0.3, Math.min(maxLeft + cellPx * 0.3, newLeft));
    newTop = Math.max(-cellPx * 0.3, Math.min(maxTop + cellPx * 0.3, newTop));

    dragState.piece.style.left = newLeft + 'px';
    dragState.piece.style.top = newTop + 'px';
  }

  function onDragEnd(e){
    if (!dragState) return;
    document.removeEventListener('mousemove', onDragMove);
    document.removeEventListener('mouseup', onDragEnd);
    document.removeEventListener('touchmove', onDragMove);
    document.removeEventListener('touchend', onDragEnd);

    var piece = dragState.piece;
    var curLeft = parseFloat(piece.style.left);
    var curTop = parseFloat(piece.style.top);

    // Determine nearest cell
    var col = Math.round(curLeft / cellPx);
    var row = Math.round(curTop / cellPx);
    col = Math.max(0, Math.min(gridSize - 1, col));
    row = Math.max(0, Math.min(gridSize - 1, row));

    // Find if another piece occupies that target cell
    var targetPiece = null;
    for (var i = 0; i < pieces.length; i++){
      var p = pieces[i];
      if (p === piece) continue;
      var pr = parseInt(p.dataset.curRow, 10);
      var pc = parseInt(p.dataset.curCol, 10);
      if (pr === row && pc === col){
        targetPiece = p;
        break;
      }
    }

    var startRow = parseInt(piece.dataset.curRow, 10);
    var startCol = parseInt(piece.dataset.curCol, 10);
    var moved = (row !== startRow || col !== startCol);

    piece.style.transition = 'top 0.18s cubic-bezier(.2,.8,.3,1), left 0.18s cubic-bezier(.2,.8,.3,1), box-shadow 0.15s ease, border-color 0.15s ease';

    if (targetPiece){
      // swap positions
      targetPiece.style.left = (startCol * cellPx) + 'px';
      targetPiece.style.top = (startRow * cellPx) + 'px';
      targetPiece.dataset.curRow = startRow;
      targetPiece.dataset.curCol = startCol;

      piece.style.left = (col * cellPx) + 'px';
      piece.style.top = (row * cellPx) + 'px';
      piece.dataset.curRow = row;
      piece.dataset.curCol = col;

      moveCount++;
      hudMoves.textContent = moveCount;
    } else if (moved){
      // empty-ish cell (shouldn't really happen since board is fully packed,
      // but guard anyway) — snap back since every cell is always occupied
      piece.style.left = (startCol * cellPx) + 'px';
      piece.style.top = (startRow * cellPx) + 'px';
    } else {
      // snap back to same place (no real move)
      piece.style.left = (startCol * cellPx) + 'px';
      piece.style.top = (startRow * cellPx) + 'px';
    }

    piece.classList.remove('dragging');
    dragState = null;

    refreshCorrectness();
    checkWin();
  }

  /* ---------------------------------------------------------------
     CORRECTNESS / WIN CHECK
  --------------------------------------------------------------- */
  function refreshCorrectness(){
    var count = 0;
    pieces.forEach(function(p){
      var cr = parseInt(p.dataset.correctRow, 10);
      var cc = parseInt(p.dataset.correctCol, 10);
      var curR = parseInt(p.dataset.curRow, 10);
      var curC = parseInt(p.dataset.curCol, 10);
      if (cr === curR && cc === curC){
        p.classList.add('correct');
        count++;
      } else {
        p.classList.remove('correct');
      }
    });
    correctCount = count;
    updateCorrectHud();
  }

  function updateCorrectHud(){
    hudCorrect.textContent = correctCount + ' / ' + totalPieces;
  }

  function checkWin(){
    if (correctCount === totalPieces && totalPieces > 0){
      puzzleActive = false;
      stopTimer();
      showWin();
    }
  }

  /* ---------------------------------------------------------------
     TIMER
  --------------------------------------------------------------- */
  function startTimer(){
    timerStart = Date.now();
    elapsedFrozen = 0;
    clearInterval(timerInterval);
    timerInterval = setInterval(updateTimerDisplay, 100);
    updateTimerDisplay();
  }

  function stopTimer(){
    elapsedFrozen = Date.now() - timerStart;
    clearInterval(timerInterval);
    timerInterval = null;
  }

  function updateTimerDisplay(){
    var elapsed = timerStart ? (Date.now() - timerStart) : 0;
    hudTime.textContent = formatTime(elapsed);
  }

  function formatTime(ms){
    var totalSec = ms / 1000;
    var mm = Math.floor(totalSec / 60);
    var ss = Math.floor(totalSec % 60);
    var t = Math.floor((totalSec * 10) % 10);
    return pad2(mm) + ':' + pad2(ss) + '.' + t;
  }

  function pad2(n){ return (n < 10 ? '0' : '') + n; }

  /* ---------------------------------------------------------------
     SHOW NUMBERS TOGGLE
  --------------------------------------------------------------- */
  toggleNumbers.addEventListener('change', function(){
    board.classList.toggle('show-numbers', toggleNumbers.checked);
  });

  /* ---------------------------------------------------------------
     WIN OVERLAY + LEADERBOARD
  --------------------------------------------------------------- */
  function showWin(){
    winThumb.src = capturedDataUrl;
    var finalMs = elapsedFrozen;
    winTime.textContent = formatTime(finalMs);
    winMoves.textContent = moveCount;
    winDiff.textContent = gridSize + '×' + gridSize;

    var isBest = saveScore(finalMs, moveCount, gridSize);
    newBestBadge.classList.toggle('show', isBest);

    renderLeaderboard();
    winOverlay.classList.add('show');
  }

  function loadScores(){
    try{
      var raw = localStorage.getItem(LB_KEY);
      if (!raw) return [];
      var arr = JSON.parse(raw);
      if (!Array.isArray(arr)) return [];
      return arr;
    } catch(e){
      return [];
    }
  }

  function saveScore(ms, moves, size){
    var scores = loadScores();
    var entry = {
      ms: ms,
      moves: moves,
      grid: size + '×' + size,
      date: new Date().toLocaleDateString(undefined, { year:'numeric', month:'short', day:'numeric' })
    };
    scores.push(entry);
    scores.sort(function(a, b){ return a.ms - b.ms; });
    var wasTop5 = scores.indexOf(entry) < 5;
    scores = scores.slice(0, 5);
    try{
      localStorage.setItem(LB_KEY, JSON.stringify(scores));
    } catch(e){ /* storage unavailable — ignore silently */ }
    return wasTop5 && scores.indexOf(entry) !== -1;
  }

  function renderLeaderboard(){
    var scores = loadScores();
    if (!scores.length){
      lbBody.innerHTML = '<tr><td class="empty" colspan="5">No times saved yet — finish a puzzle to set a record!</td></tr>';
      return;
    }
    var html = '';
    scores.forEach(function(entry, idx){
      html += '<tr>' +
        '<td class="rank">' + (idx + 1) + '</td>' +
        '<td>' + formatTime(entry.ms) + '</td>' +
        '<td>' + entry.moves + '</td>' +
        '<td>' + entry.grid + '</td>' +
        '<td>' + entry.date + '</td>' +
        '</tr>';
    });
    lbBody.innerHTML = html;
  }

  /* ---------------------------------------------------------------
     BUTTON WIRING — Retake / New Photo / Play Again / Reshuffle
  --------------------------------------------------------------- */
  function goToCameraFresh(){
    puzzleActive = false;
    clearInterval(timerInterval);
    winOverlay.classList.remove('show');
    showScreen(screenCamera);
    startCamera();
  }

  btnRetake2.addEventListener('click', goToCameraFresh);
  btnNewPhotoGame.addEventListener('click', goToCameraFresh);
  btnNewPhotoWin.addEventListener('click', goToCameraFresh);

  btnShuffleAgain.addEventListener('click', function(){
    clearInterval(timerInterval);
    buildPuzzle();
  });

  btnPlayAgain.addEventListener('click', function(){
    winOverlay.classList.remove('show');
    clearInterval(timerInterval);
    buildPuzzle();
  });

  /* ---------------------------------------------------------------
     INIT
  --------------------------------------------------------------- */
  renderLeaderboard();
  startCamera();

})();
</script>
</body>
</html>


#### Output Screenshots :
<img width="1920" height="915" alt="Screenshot (317)" src="https://github.com/user-attachments/assets/04fbe2fd-a991-4ddf-b97e-faee9d898f1b" />
<img width="1920" height="912" alt="Screenshot (316)" src="https://github.com/user-attachments/assets/6efd8bad-a100-4295-af14-bb038d2a48cf" />
<img width="1920" height="914" alt="Screenshot (315)" src="https://github.com/user-attachments/assets/e6a5ca8f-70c9-42d3-a132-f47a3bba4e58" />

