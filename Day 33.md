# Today, I built a Media Integrity Analyzer using claude :

## 📚 Key Learnings :
- Learned how misleading headlines can shape opinions even before people read the full article.
- Explored techniques for identifying clickbait by comparing headlines with the actual information presented.
- Gained a better understanding of how emotional language is used to influence user behavior and encourage engagement.
- Learned to recognize common manipulation techniques such as urgency, fear, exaggeration, and absolute claims.
- Understood the importance of evaluating source reliability before accepting information as factual.
- Improved my ability to think critically by analyzing the relationship between evidence and the claims being made.
- Designed an interactive learning experience that helps users practice media literacy instead of simply presenting results.
- Enhanced my prompt engineering skills by using Claude to structure educational content, explanations, and feedback.
- Learned how AI can simplify complex concepts and present them in an engaging, user-friendly format.
- Reinforced the importance of verifying information through multiple trusted sources before sharing or acting on online content.

### OUTPUT Screenshot :

<img width="836" height="911" alt="Screenshot (526)" src="https://github.com/user-attachments/assets/ce99b56a-1d7e-460b-98b9-814e8d816e1b" />

#### HTML File :

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Media Integrity Analyzer</title>
<style>
  :root{
    --bg-0:#050a14;
    --bg-1:#0a1428;
    --bg-2:#0f1c38;
    --bg-3:#152447;
    --accent:#4f8cff;
    --accent-2:#7db3ff;
    --accent-soft:rgba(79,140,255,0.14);
    --good:#4ade80;
    --warn:#fbbf24;
    --bad:#f87171;
    --text-0:#eaf0fb;
    --text-1:#b7c3dd;
    --text-2:#7f8db0;
    --border:rgba(125,179,255,0.14);
    --shadow:0 20px 60px rgba(0,0,0,0.5);
    --radius:18px;
    --font-serif:'Georgia', 'Iowan Old Style', serif;
    --font-sans:-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  }

  *{box-sizing:border-box;margin:0;padding:0;}

  html,body{
    background:
      radial-gradient(ellipse 800px 500px at 15% -10%, rgba(79,140,255,0.16), transparent 60%),
      radial-gradient(ellipse 900px 600px at 100% 20%, rgba(79,140,255,0.10), transparent 55%),
      var(--bg-0);
    color:var(--text-0);
    font-family:var(--font-sans);
    min-height:100vh;
    line-height:1.55;
    -webkit-font-smoothing:antialiased;
  }

  .wrap{
    max-width:920px;
    margin:0 auto;
    padding:48px 24px 120px;
  }

  /* ===== Top Bar / Header ===== */
  header.top{
    display:flex;
    justify-content:space-between;
    align-items:flex-start;
    margin-bottom:36px;
    gap:20px;
    flex-wrap:wrap;
  }

  .brand{
    display:flex;
    flex-direction:column;
    gap:6px;
  }

  .brand h1{
    font-family:var(--font-serif);
    font-size:2rem;
    font-weight:700;
    letter-spacing:-0.02em;
    background:linear-gradient(120deg, var(--text-0), var(--accent-2));
    -webkit-background-clip:text;
    background-clip:text;
    -webkit-text-fill-color:transparent;
  }

  .brand p{
    color:var(--text-2);
    font-size:0.92rem;
    max-width:440px;
  }

  .badge{
    font-size:0.72rem;
    text-transform:uppercase;
    letter-spacing:0.12em;
    color:var(--accent-2);
    background:var(--accent-soft);
    border:1px solid var(--border);
    padding:5px 10px;
    border-radius:999px;
    display:inline-block;
    width:fit-content;
  }

  /* ===== Metrics Dashboard (Live) ===== */
  .metrics{
    display:grid;
    grid-template-columns:repeat(4, 1fr);
    gap:12px;
    margin-bottom:40px;
  }

  .metric-card{
    background:linear-gradient(160deg, var(--bg-2), var(--bg-1));
    border:1px solid var(--border);
    border-radius:14px;
    padding:14px 16px;
    position:relative;
    overflow:hidden;
    transition:transform 0.3s ease, box-shadow 0.3s ease;
  }

  .metric-card:hover{
    transform:translateY(-3px);
    box-shadow:0 10px 30px rgba(0,0,0,0.4);
  }

  .metric-label{
    font-size:0.68rem;
    text-transform:uppercase;
    letter-spacing:0.08em;
    color:var(--text-2);
    margin-bottom:6px;
  }

  .metric-value{
    font-size:1.5rem;
    font-weight:700;
    font-family:var(--font-serif);
    color:var(--text-0);
  }

  .metric-bar{
    margin-top:8px;
    height:5px;
    background:rgba(255,255,255,0.06);
    border-radius:99px;
    overflow:hidden;
  }

  .metric-bar-fill{
    height:100%;
    border-radius:99px;
    background:linear-gradient(90deg, var(--accent), var(--accent-2));
    width:0%;
    transition:width 1s cubic-bezier(.22,1,.36,1);
  }

  /* ===== Progress Steps ===== */
  .progress-track{
    display:flex;
    align-items:center;
    gap:8px;
    margin-bottom:40px;
  }

  .progress-step{
    flex:1;
    height:4px;
    background:rgba(255,255,255,0.08);
    border-radius:99px;
    overflow:hidden;
    position:relative;
  }

  .progress-step::after{
    content:'';
    position:absolute;
    inset:0;
    background:linear-gradient(90deg, var(--accent), var(--accent-2));
    width:0%;
    transition:width 0.6s ease;
  }

  .progress-step.done::after{width:100%;}
  .progress-step.active::after{width:50%;}

  /* ===== Section / Card ===== */
  .card{
    background:linear-gradient(160deg, var(--bg-2), var(--bg-1));
    border:1px solid var(--border);
    border-radius:var(--radius);
    padding:32px;
    margin-bottom:28px;
    box-shadow:var(--shadow);
    animation:fadeUp 0.6s cubic-bezier(.22,1,.36,1);
  }

  @keyframes fadeUp{
    from{opacity:0; transform:translateY(18px);}
    to{opacity:1; transform:translateY(0);}
  }

  .card.hidden{display:none;}

  .lesson-tag{
    display:inline-flex;
    align-items:center;
    gap:8px;
    font-size:0.72rem;
    text-transform:uppercase;
    letter-spacing:0.1em;
    color:var(--accent-2);
    margin-bottom:14px;
  }

  .lesson-tag::before{
    content:'';
    width:7px;
    height:7px;
    border-radius:50%;
    background:var(--accent-2);
    box-shadow:0 0 10px var(--accent-2);
  }

  .card h2{
    font-family:var(--font-serif);
    font-size:1.6rem;
    margin-bottom:12px;
    letter-spacing:-0.01em;
  }

  .card h3{
    font-family:var(--font-serif);
    font-size:1.15rem;
    margin-bottom:10px;
    color:var(--text-0);
  }

  .card p{
    color:var(--text-1);
    margin-bottom:14px;
    font-size:0.98rem;
  }

  .why-box{
    background:rgba(79,140,255,0.07);
    border-left:3px solid var(--accent);
    padding:14px 18px;
    border-radius:8px;
    margin-bottom:22px;
    font-size:0.92rem;
    color:var(--text-1);
  }

  .why-box strong{color:var(--accent-2);}

  /* ===== Article / Post Preview ===== */
  .article-preview{
    background:var(--bg-3);
    border:1px solid var(--border);
    border-radius:14px;
    padding:24px;
    margin-bottom:24px;
    position:relative;
  }

  .article-preview .source-line{
    font-size:0.75rem;
    color:var(--text-2);
    text-transform:uppercase;
    letter-spacing:0.06em;
    margin-bottom:10px;
    display:flex;
    justify-content:space-between;
  }

  .article-preview h4{
    font-family:var(--font-serif);
    font-size:1.35rem;
    line-height:1.35;
    color:var(--text-0);
    margin-bottom:14px;
  }

  .article-preview .body-text{
    font-size:0.94rem;
    color:var(--text-1);
    line-height:1.7;
  }

  .post-preview{
    background:var(--bg-3);
    border:1px solid var(--border);
    border-radius:14px;
    padding:22px;
    margin-bottom:24px;
  }

  .post-preview .handle{
    font-size:0.85rem;
    color:var(--accent-2);
    font-weight:600;
    margin-bottom:10px;
  }

  .post-preview .caption{
    font-size:1.02rem;
    color:var(--text-0);
    line-height:1.6;
  }

  /* ===== Highlight marks ===== */
  mark.flag{
    background:rgba(248,113,113,0.22);
    color:#ffb3b3;
    padding:1px 4px;
    border-radius:4px;
    font-weight:600;
    box-shadow:inset 0 0 0 1px rgba(248,113,113,0.3);
  }

  mark.emo{
    background:rgba(251,191,36,0.2);
    color:#ffd980;
    padding:1px 4px;
    border-radius:4px;
    font-weight:600;
    box-shadow:inset 0 0 0 1px rgba(251,191,36,0.3);
  }

  /* ===== Buttons / Choices ===== */
  .choice-row{
    display:flex;
    gap:12px;
    flex-wrap:wrap;
    margin-bottom:22px;
  }

  .choice-btn{
    flex:1;
    min-width:110px;
    padding:14px 18px;
    background:var(--bg-3);
    border:1px solid var(--border);
    color:var(--text-0);
    border-radius:12px;
    font-size:0.95rem;
    font-weight:600;
    cursor:pointer;
    transition:all 0.25s ease;
    font-family:var(--font-sans);
  }

  .choice-btn:hover{
    border-color:var(--accent);
    background:var(--accent-soft);
    transform:translateY(-2px);
  }

  .choice-btn.selected{
    background:linear-gradient(120deg, var(--accent), #3a6fd6);
    border-color:var(--accent);
    color:#fff;
    box-shadow:0 8px 20px rgba(79,140,255,0.35);
  }

  textarea.answer-box{
    width:100%;
    min-height:90px;
    background:var(--bg-3);
    border:1px solid var(--border);
    border-radius:12px;
    color:var(--text-0);
    padding:14px 16px;
    font-family:var(--font-sans);
    font-size:0.94rem;
    resize:vertical;
    margin-bottom:18px;
    transition:border-color 0.25s ease;
  }

  textarea.answer-box:focus{
    outline:none;
    border-color:var(--accent);
    box-shadow:0 0 0 3px var(--accent-soft);
  }

  .btn-primary{
    background:linear-gradient(120deg, var(--accent), #3a6fd6);
    color:#fff;
    border:none;
    padding:14px 28px;
    border-radius:12px;
    font-size:0.98rem;
    font-weight:700;
    cursor:pointer;
    transition:transform 0.25s ease, box-shadow 0.25s ease;
    box-shadow:0 10px 25px rgba(79,140,255,0.3);
    font-family:var(--font-sans);
  }

  .btn-primary:hover{
    transform:translateY(-2px);
    box-shadow:0 14px 32px rgba(79,140,255,0.42);
  }

  .btn-primary:disabled{
    opacity:0.4;
    cursor:not-allowed;
    transform:none;
    box-shadow:none;
  }

  .btn-secondary{
    background:transparent;
    color:var(--accent-2);
    border:1px solid var(--border);
    padding:13px 26px;
    border-radius:12px;
    font-size:0.95rem;
    font-weight:600;
    cursor:pointer;
    transition:all 0.25s ease;
    font-family:var(--font-sans);
  }

  .btn-secondary:hover{
    background:var(--accent-soft);
    border-color:var(--accent);
  }

  /* ===== Reveal Panel ===== */
  .reveal{
    margin-top:22px;
    padding-top:22px;
    border-top:1px dashed var(--border);
    animation:fadeUp 0.5s ease;
  }

  .score-display{
    display:flex;
    align-items:center;
    gap:20px;
    margin-bottom:20px;
    flex-wrap:wrap;
  }

  .score-ring{
    width:88px;
    height:88px;
    border-radius:50%;
    display:flex;
    align-items:center;
    justify-content:center;
    font-family:var(--font-serif);
    font-size:1.5rem;
    font-weight:700;
    background:conic-gradient(var(--accent) calc(var(--pct,50) * 1%), rgba(255,255,255,0.08) 0);
    position:relative;
    flex-shrink:0;
  }

  .score-ring::before{
    content:'';
    position:absolute;
    inset:6px;
    background:var(--bg-2);
    border-radius:50%;
  }

  .score-ring span{position:relative; z-index:1;}

  .score-meta h3{margin-bottom:4px;}
  .score-meta p{margin-bottom:0; color:var(--text-2); font-size:0.88rem;}

  .info-grid{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:16px;
    margin-bottom:18px;
  }

  .info-block{
    background:rgba(255,255,255,0.03);
    border:1px solid var(--border);
    border-radius:12px;
    padding:16px 18px;
  }

  .info-block .label{
    font-size:0.7rem;
    text-transform:uppercase;
    letter-spacing:0.08em;
    color:var(--accent-2);
    margin-bottom:6px;
  }

  .info-block .value{
    font-size:0.93rem;
    color:var(--text-1);
  }

  .rewrite-box{
    background:rgba(74,222,128,0.08);
    border-left:3px solid var(--good);
    border-radius:8px;
    padding:14px 18px;
    margin-bottom:16px;
    font-family:var(--font-serif);
    font-size:1.02rem;
    color:#d5ffe4;
  }

  .takeaway-box{
    background:rgba(79,140,255,0.09);
    border:1px solid var(--border);
    border-radius:12px;
    padding:16px 18px;
    display:flex;
    gap:12px;
    align-items:flex-start;
  }

  .takeaway-box .icon{
    font-size:1.3rem;
    flex-shrink:0;
  }

  .takeaway-box p{margin:0; color:var(--text-0); font-size:0.94rem;}

  /* ===== Dashboard (Final) ===== */
  .dash-hero{
    text-align:center;
    padding:44px 20px;
  }

  .dash-score{
    width:180px;
    height:180px;
    border-radius:50%;
    margin:0 auto 20px;
    display:flex;
    align-items:center;
    justify-content:center;
    background:conic-gradient(var(--accent) calc(var(--pct,50) * 1%), rgba(255,255,255,0.07) 0);
    position:relative;
    animation:pop 0.8s cubic-bezier(.22,1,.36,1);
  }

  @keyframes pop{
    0%{transform:scale(0.7); opacity:0;}
    100%{transform:scale(1); opacity:1;}
  }

  .dash-score::before{
    content:'';
    position:absolute;
    inset:12px;
    background:var(--bg-1);
    border-radius:50%;
  }

  .dash-score .num{
    position:relative;
    z-index:1;
    font-family:var(--font-serif);
    font-size:3rem;
    font-weight:700;
  }

  .dash-score .num small{
    font-size:1.1rem;
    color:var(--text-2);
    display:block;
    margin-top:-6px;
  }

  .dash-hero h2{
    font-family:var(--font-serif);
    font-size:1.8rem;
    margin-bottom:8px;
  }

  .dash-hero p{color:var(--text-2); max-width:480px; margin:0 auto;}

  .dash-grid{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:16px;
    margin-top:10px;
  }

  .habit-list{
    list-style:none;
    display:flex;
    flex-direction:column;
    gap:10px;
  }

  .habit-list li{
    display:flex;
    gap:12px;
    align-items:flex-start;
    background:rgba(255,255,255,0.03);
    border:1px solid var(--border);
    border-radius:10px;
    padding:12px 14px;
    font-size:0.9rem;
    color:var(--text-1);
  }

  .habit-list li .num-badge{
    width:22px;
    height:22px;
    border-radius:50%;
    background:var(--accent-soft);
    color:var(--accent-2);
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:0.75rem;
    font-weight:700;
    flex-shrink:0;
  }

  .redflag-box{
    background:rgba(248,113,113,0.08);
    border:1px solid rgba(248,113,113,0.25);
    border-radius:12px;
    padding:16px 18px;
    color:#ffb3b3;
    font-size:0.92rem;
  }

  .cta-row{
    display:flex;
    justify-content:center;
    gap:14px;
    margin-top:28px;
    flex-wrap:wrap;
  }

  footer{
    text-align:center;
    color:var(--text-2);
    font-size:0.8rem;
    margin-top:40px;
  }

  @media (max-width:640px){
    .metrics{grid-template-columns:repeat(2,1fr);}
    .info-grid{grid-template-columns:1fr;}
    .dash-grid{grid-template-columns:1fr;}
    .card{padding:22px;}
    .brand h1{font-size:1.6rem;}
  }
</style>
</head>
<body>
<div class="wrap">

  <header class="top">
    <div class="brand">
      <span class="badge">Media Literacy Lab</span>
      <h1>Media Integrity Analyzer</h1>
      <p>A guided, interactive lesson in spotting misleading headlines and emotional manipulation — learn by observing, thinking, then revealing.</p>
    </div>
  </header>

  <div class="metrics">
    <div class="metric-card">
      <div class="metric-label">Headline Accuracy</div>
      <div class="metric-value" id="m-headline">—</div>
      <div class="metric-bar"><div class="metric-bar-fill" id="m-headline-bar"></div></div>
    </div>
    <div class="metric-card">
      <div class="metric-label">Source Reliability</div>
      <div class="metric-value" id="m-source">—</div>
      <div class="metric-bar"><div class="metric-bar-fill" id="m-source-bar"></div></div>
    </div>
    <div class="metric-card">
      <div class="metric-label">Emotional Manipulation</div>
      <div class="metric-value" id="m-emotion">—</div>
      <div class="metric-bar"><div class="metric-bar-fill" id="m-emotion-bar"></div></div>
    </div>
    <div class="metric-card">
      <div class="metric-label">Audience Targeting</div>
      <div class="metric-value" id="m-audience">—</div>
      <div class="metric-bar"><div class="metric-bar-fill" id="m-audience-bar"></div></div>
    </div>
  </div>

  <div class="progress-track">
    <div class="progress-step active" id="pstep-1"></div>
    <div class="progress-step" id="pstep-2"></div>
    <div class="progress-step" id="pstep-3"></div>
  </div>

  <!-- ================= CHALLENGE 1: HEADLINE DETECTIVE ================= -->
  <section class="card" id="challenge1">
    <div class="lesson-tag">Lesson 01 · Headline Detective</div>
    <h2>Can you spot a misleading headline?</h2>
    <p>Publishers often stretch the truth in headlines to earn clicks — a practice called "clickbait." Exaggeration, vague sourcing, and emotionally loaded words can make a small story sound huge.</p>
    <div class="why-box"><strong>Why it matters:</strong> Misleading headlines shape opinions before you even read the article — and most people only read the headline. Learning to spot the gap between headline and substance is the first defense against misinformation.</div>

    <div class="article-preview">
      <div class="source-line"><span id="c1-source">The Daily Pulse</span><span id="c1-time">2 hours ago</span></div>
      <h4 id="c1-headline"></h4>
      <div class="body-text" id="c1-body"></div>
    </div>

    <h3>Would you click this?</h3>
    <div class="choice-row" id="c1-click-choices">
      <button class="choice-btn" data-val="Yes">Yes</button>
      <button class="choice-btn" data-val="Maybe">Maybe</button>
      <button class="choice-btn" data-val="No">No</button>
    </div>

    <h3>What parts feel exaggerated or misleading? (optional — jot your thoughts)</h3>
    <textarea class="answer-box" id="c1-thoughts" placeholder="e.g. the word 'SHOCKING', the vague claim about scientists..."></textarea>

    <button class="btn-primary" id="c1-reveal-btn" disabled>Reveal the Analysis</button>

    <div class="reveal hidden" id="c1-reveal">
      <div class="score-display">
        <div class="score-ring" id="c1-score-ring" style="--pct:38"><span id="c1-score-num">38%</span></div>
        <div class="score-meta">
          <h3>Headline Accuracy Score</h3>
          <p>How well the headline reflects the actual article content.</p>
        </div>
      </div>

      <h3>Highlighted Mismatches</h3>
      <div class="article-preview" style="margin-bottom:18px;">
        <h4 id="c1-headline-marked"></h4>
        <div class="body-text" id="c1-body-marked"></div>
      </div>

      <div class="info-grid">
        <div class="info-block">
          <div class="label">Why It's Misleading</div>
          <div class="value">The headline implies a definitive, dramatic conclusion ("proven," "banned," "everyone") while the article only describes a small, preliminary, or partial finding. This gap between claim and evidence is the core clickbait tactic.</div>
        </div>
        <div class="info-block">
          <div class="label">Fair, Rewritten Headline</div>
          <div class="value" id="c1-rewrite" style="color:#d5ffe4;"></div>
        </div>
      </div>

      <div class="takeaway-box">
        <div class="icon">💡</div>
        <p id="c1-takeaway">Key takeaway: Headlines are marketing copy for the article, not a summary of its findings. Always ask "does the body actually support this claim?"</p>
      </div>
    </div>
  </section>

  <!-- ================= CHALLENGE 2: EMOTION DETECTOR ================= -->
  <section class="card hidden" id="challenge2">
    <div class="lesson-tag">Lesson 02 · Emotion Detector</div>
    <h2>What is this post making you feel — and why?</h2>
    <p>Social media content is often engineered to trigger a fast emotional reaction — outrage, fear, envy, or urgency — because strong feelings drive shares, comments, and watch-time.</p>
    <div class="why-box"><strong>Why it matters:</strong> When we react emotionally, we think less critically. Recognizing the specific words and techniques used to trigger emotion helps you pause before reacting, sharing, or buying.</div>

    <div class="post-preview">
      <div class="handle" id="c2-handle">@viral.now</div>
      <div class="caption" id="c2-caption"></div>
    </div>

    <h3>How did this post make you feel?</h3>
    <div class="choice-row" id="c2-feel-choices">
      <button class="choice-btn" data-val="Anxious / Fearful">Anxious / Fearful</button>
      <button class="choice-btn" data-val="Angry / Outraged">Angry / Outraged</button>
      <button class="choice-btn" data-val="Excited / FOMO">Excited / FOMO</button>
      <button class="choice-btn" data-val="Neutral">Neutral</button>
    </div>

    <h3>Which words influenced that feeling? (optional)</h3>
    <textarea class="answer-box" id="c2-thoughts" placeholder="e.g. 'before it's too late', 'everyone is switching'..."></textarea>

    <button class="btn-primary" id="c2-reveal-btn" disabled>Reveal the Analysis</button>

    <div class="reveal hidden" id="c2-reveal">
      <div class="score-display">
        <div class="score-ring" id="c2-score-ring" style="--pct:72"><span id="c2-score-num">72%</span></div>
        <div class="score-meta">
          <h3>Emotional Manipulation Score</h3>
          <p>How strongly this post is engineered to provoke a reaction over reflection.</p>
        </div>
      </div>

      <h3>Highlighted Emotional Phrases</h3>
      <div class="post-preview" style="margin-bottom:18px;">
        <div class="caption" id="c2-caption-marked"></div>
      </div>

      <div class="info-grid">
        <div class="info-block">
          <div class="label">Target Audience</div>
          <div class="value" id="c2-audience"></div>
        </div>
        <div class="info-block">
          <div class="label">Intended Emotional Response</div>
          <div class="value" id="c2-intended"></div>
        </div>
        <div class="info-block">
          <div class="label">Manipulation Technique</div>
          <div class="value" id="c2-technique"></div>
        </div>
        <div class="info-block">
          <div class="label">Neutral Rewrite</div>
          <div class="value" id="c2-rewrite" style="color:#d5ffe4;"></div>
        </div>
      </div>

      <div class="takeaway-box">
        <div class="icon">💡</div>
        <p id="c2-takeaway">Key takeaway: Strong emotional language is a design choice, not an accident. Pause before reacting to content that feels urgent or outrageous.</p>
      </div>

      <div style="margin-top:22px; text-align:right;">
        <button class="btn-primary" id="goto-dashboard-btn">See My Media Integrity Dashboard →</button>
      </div>
    </div>
  </section>

  <!-- ================= FINAL DASHBOARD ================= -->
  <section class="card hidden" id="dashboard">
    <div class="lesson-tag">Summary · Media Integrity Dashboard</div>

    <div class="dash-hero">
      <div class="dash-score" id="dash-score-ring" style="--pct:55">
        <div class="num" id="dash-score-num">55<small>OVERALL SCORE</small></div>
      </div>
      <h2>Your Media Integrity Snapshot</h2>
      <p id="dash-summary">You're building the instincts to separate signal from spin. Keep practicing — literacy is a habit, not a one-time test.</p>
    </div>

    <div class="dash-grid">
      <div class="info-block">
        <div class="label">What You Learned</div>
        <div class="value" id="dash-learned">You practiced spotting the gap between a dramatic headline and its actual evidence, and identified emotionally loaded language designed to provoke a fast reaction.</div>
      </div>
      <div class="info-block">
        <div class="label">Biggest Red Flag</div>
        <div class="value redflag-box" id="dash-redflag" style="border:none; background:transparent; padding:0;">Loaded, absolute language ("proven," "everyone," "before it's too late") standing in for actual evidence.</div>
      </div>
    </div>

    <h3 style="margin-top:26px;">Three Practical Media Literacy Habits</h3>
    <ul class="habit-list">
      <li><span class="num-badge">1</span><span>Read past the headline — check whether the article's body actually supports the claim being made.</span></li>
      <li><span class="num-badge">2</span><span>Notice your emotional reaction. If content makes you feel rushed, outraged, or fearful, pause before sharing or acting.</span></li>
      <li><span class="num-badge">3</span><span>Check the source and look for a second, independent source before treating a claim as fact.</span></li>
    </ul>

    <div class="cta-row">
      <button class="btn-primary" id="replay-btn">🔄 Replay with New Scenarios</button>
    </div>
  </section>

  <footer>Media Integrity Analyzer · A self-contained media literacy lesson · No data leaves your browser</footer>
</div>

<script>
(function(){

  // ---------- Content Banks ----------
  var headlineBank = [
    {
      source:"The Daily Pulse", time:"2 hours ago",
      headline:"SHOCKING: Scientists PROVE Coffee Instantly Reverses Aging, Doctors Stunned",
      body:"A small university study followed 24 adults who drank two cups of coffee daily for six weeks. Researchers observed a slight, temporary improvement in one blood marker linked to inflammation. The lead author cautioned that the sample size was too small to draw broad conclusions and called for larger, long-term trials before any health claims could be made.",
      flagWords:["SHOCKING","PROVE","Instantly Reverses Aging","Doctors Stunned"],
      bodyFlagPhrases:["small university study","24 adults","slight, temporary improvement","too small to draw broad conclusions"],
      rewrite:"Small Study Finds Modest, Short-Term Link Between Coffee and One Inflammation Marker",
      score:32
    },
    {
      source:"UrbanWire News", time:"5 hours ago",
      headline:"City Officials BAN All Cars Downtown, Residents Furious",
      body:"The city council approved a pilot program restricting private vehicle traffic on a four-block stretch of Main Street on weekend evenings only, for a three-month trial. Local business owners were split, with several supporting the change as good for foot traffic. A public feedback session is scheduled before any permanent decision is made.",
      flagWords:["BAN All Cars","Furious"],
      bodyFlagPhrases:["pilot program","four-block stretch","weekend evenings only","three-month trial"],
      rewrite:"City Council Approves 3-Month Weekend Car-Free Trial on Four Blocks of Main Street",
      score:28
    },
    {
      source:"TechToday Wire", time:"just now",
      headline:"This One App Setting Is SECRETLY Stealing Your Data — Turn It Off NOW",
      body:"A security researcher found that a popular app's optional analytics setting, which is disclosed in the app's privacy policy and disabled by default, sends anonymized usage statistics to improve performance. Users can review and adjust this setting at any time in the app's privacy menu.",
      flagWords:["SECRETLY Stealing","Turn It Off NOW"],
      bodyFlagPhrases:["optional analytics setting","disclosed in the app's privacy policy","disabled by default","anonymized usage statistics"],
      rewrite:"Security Researcher Highlights Optional, Disclosed Analytics Setting in Popular App",
      score:24
    }
  ];

  var postBank = [
    {
      handle:"@wellness.now",
      caption:"Doctors HATE this simple trick 😱 Everyone is switching before it's too late — don't be the last one to find out the truth they don't want you to know! Link in bio before it's REMOVED 🔥",
      flagPhrases:["Doctors HATE this","😱","Everyone is switching","before it's too late","the truth they don't want you to know","before it's REMOVED","🔥"],
      audience:"Health-anxious adults, ages 25–55, active on wellness and self-improvement content, likely to respond to urgency and insider-secret framing.",
      intended:"Fear of missing out (FOMO) combined with mild anxiety and distrust of institutions, driving an impulsive click before 'critical thinking' kicks in.",
      technique:"Urgency + Manufactured Scarcity + Us-vs-Them framing ('they don't want you to know')",
      rewrite:"A wellness product is available, and some people report liking it. Consider researching independent reviews before purchasing."
    },
    {
      handle:"@moneymindset.daily",
      caption:"I can't believe how many people are STILL broke doing it the old way 💸 Rich people know this ONE secret and they are laughing at you for not using it. Comment 'YES' now or regret it forever.",
      flagPhrases:["STILL broke","💸","ONE secret","laughing at you","Comment 'YES' now","regret it forever"],
      audience:"Young adults interested in personal finance and side-income content, especially those feeling behind financially.",
      intended:"Shame and social comparison, paired with urgency, to drive comments (which boost the post's reach) and impulsive engagement.",
      technique:"Shame-based comparison + Engagement bait + False urgency",
      rewrite:"This account is promoting a financial strategy. Engagement-driving language doesn't mean the advice is proven — verify with an independent financial source."
    },
    {
      handle:"@newsflash.viral",
      caption:"BREAKING 🚨 You won't BELIEVE what just happened — this changes EVERYTHING and the mainstream media is staying SILENT. Share before this gets taken down!!",
      flagPhrases:["BREAKING 🚨","won't BELIEVE","changes EVERYTHING","staying SILENT","Share before this gets taken down"],
      audience:"News consumers primed for distrust of traditional outlets, likely to share rapidly without verifying.",
      intended:"Outrage and urgency, encouraging immediate sharing before any fact-checking can occur.",
      technique:"False urgency + Vague sourcing + Suppression narrative ('media is silent')",
      rewrite:"A claim is circulating online. No specific event or source is named — treat with skepticism until a credible outlet confirms it."
    }
  ];

  var state = {
    c1: null, c1ClickChoice:null, c1Revealed:false,
    c2: null, c2FeelChoice:null, c2Revealed:false,
    metrics:{headline:null, source:null, emotion:null, audience:null}
  };

  function pick(arr){ return arr[Math.floor(Math.random()*arr.length)]; }

  function escapeHtml(str){
    return str.replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;");
  }

  function highlight(text, phrases, cls){
    var safe = escapeHtml(text);
    phrases.forEach(function(p){
      var safeP = escapeHtml(p);
      // escape regex special chars
      var re = new RegExp(safeP.replace(/[.*+?^${}()|[\]\\]/g,'\\$&'), 'gi');
      safe = safe.replace(re, function(match){ return '<mark class="'+cls+'">'+match+'</mark>'; });
    });
    return safe;
  }

  function setMetric(id, value){
    var valEl = document.getElementById('m-'+id);
    var barEl = document.getElementById('m-'+id+'-bar');
    valEl.textContent = value + '%';
    requestAnimationFrame(function(){ barEl.style.width = value + '%'; });
  }

  // ---------- Challenge 1 Setup ----------
  function setupChallenge1(){
    state.c1 = pick(headlineBank);
    state.c1ClickChoice = null;
    state.c1Revealed = false;

    document.getElementById('c1-source').textContent = state.c1.source;
    document.getElementById('c1-time').textContent = state.c1.time;
    document.getElementById('c1-headline').textContent = state.c1.headline;
    document.getElementById('c1-body').textContent = state.c1.body;
    document.getElementById('c1-thoughts').value = '';

    document.querySelectorAll('#c1-click-choices .choice-btn').forEach(function(btn){
      btn.classList.remove('selected');
    });
    document.getElementById('c1-reveal-btn').disabled = true;
    document.getElementById('c1-reveal').classList.add('hidden');
  }

  document.querySelectorAll('#c1-click-choices .choice-btn').forEach(function(btn){
    btn.addEventListener('click', function(){
      document.querySelectorAll('#c1-click-choices .choice-btn').forEach(function(b){ b.classList.remove('selected'); });
      btn.classList.add('selected');
      state.c1ClickChoice = btn.getAttribute('data-val');
      document.getElementById('c1-reveal-btn').disabled = false;
    });
  });

  document.getElementById('c1-reveal-btn').addEventListener('click', function(){
    if(state.c1Revealed) return;
    state.c1Revealed = true;
    var d = state.c1;

    document.getElementById('c1-score-num').textContent = d.score + '%';
    document.getElementById('c1-score-ring').style.setProperty('--pct', d.score);

    document.getElementById('c1-headline-marked').innerHTML = highlight(d.headline, d.flagWords, 'flag');
    document.getElementById('c1-body-marked').innerHTML = highlight(d.body, d.bodyFlagPhrases, 'flag');

    document.getElementById('c1-rewrite').textContent = d.rewrite;

    document.getElementById('c1-reveal').classList.remove('hidden');
    document.getElementById('c1-reveal-btn').disabled = true;

    // update metrics
    state.metrics.headline = d.score;
    state.metrics.source = Math.min(95, d.score + 22 + Math.round(Math.random()*10));
    setMetric('headline', state.metrics.headline);
    setMetric('source', state.metrics.source);

    document.getElementById('pstep-1').classList.add('done');
    document.getElementById('pstep-2').classList.add('active');

    setTimeout(function(){
      document.getElementById('challenge2').classList.remove('hidden');
      document.getElementById('challenge2').scrollIntoView({behavior:'smooth', block:'start'});
    }, 500);
  });

  // ---------- Challenge 2 Setup ----------
  function setupChallenge2(){
    state.c2 = pick(postBank);
    state.c2FeelChoice = null;
    state.c2Revealed = false;

    document.getElementById('c2-handle').textContent = state.c2.handle;
    document.getElementById('c2-caption').textContent = state.c2.caption;
    document.getElementById('c2-thoughts').value = '';

    document.querySelectorAll('#c2-feel-choices .choice-btn').forEach(function(btn){
      btn.classList.remove('selected');
    });
    document.getElementById('c2-reveal-btn').disabled = true;
    document.getElementById('c2-reveal').classList.add('hidden');
  }

  document.querySelectorAll('#c2-feel-choices .choice-btn').forEach(function(btn){
    btn.addEventListener('click', function(){
      document.querySelectorAll('#c2-feel-choices .choice-btn').forEach(function(b){ b.classList.remove('selected'); });
      btn.classList.add('selected');
      state.c2FeelChoice = btn.getAttribute('data-val');
      document.getElementById('c2-reveal-btn').disabled = false;
    });
  });

  document.getElementById('c2-reveal-btn').addEventListener('click', function(){
    if(state.c2Revealed) return;
    state.c2Revealed = true;
    var d = state.c2;

    var manipScore = 60 + Math.round(Math.random()*25);

    document.getElementById('c2-score-num').textContent = manipScore + '%';
    document.getElementById('c2-score-ring').style.setProperty('--pct', manipScore);

    document.getElementById('c2-caption-marked').innerHTML = highlight(d.caption, d.flagPhrases, 'emo');
    document.getElementById('c2-audience').textContent = d.audience;
    document.getElementById('c2-intended').textContent = d.intended;
    document.getElementById('c2-technique').textContent = d.technique;
    document.getElementById('c2-rewrite').textContent = d.rewrite;

    document.getElementById('c2-reveal').classList.remove('hidden');
    document.getElementById('c2-reveal-btn').disabled = true;

    state.metrics.emotion = manipScore;
    state.metrics.audience = 55 + Math.round(Math.random()*30);
    setMetric('emotion', state.metrics.emotion);
    setMetric('audience', state.metrics.audience);

    document.getElementById('pstep-2').classList.add('done');
    document.getElementById('pstep-3').classList.add('active');
  });

  document.getElementById('goto-dashboard-btn').addEventListener('click', function(){
    showDashboard();
  });

  function showDashboard(){
    var m = state.metrics;
    var overall = Math.round(
      (m.headline + m.source + (100 - m.emotion) + (100 - Math.min(m.audience,90))) / 4
    );
    overall = Math.max(10, Math.min(95, overall));

    document.getElementById('dash-score-num').innerHTML = overall + '<small>OVERALL SCORE</small>';
    document.getElementById('dash-score-ring').style.setProperty('--pct', overall);

    var summaryText;
    if(overall >= 70){
      summaryText = "Strong instincts! You caught the gap between headline drama and real evidence, and noticed the emotional levers being pulled.";
    } else if(overall >= 45){
      summaryText = "Good start — you're noticing manipulation patterns. Keep practicing spotting the mismatch between claims and evidence.";
    } else {
      summaryText = "This content was engineered to bypass careful reading. That's normal — awareness is the first step, and you just built some.";
    }
    document.getElementById('dash-summary').textContent = summaryText;

    document.getElementById('dash-learned').textContent =
      "You practiced comparing a headline (\"" + state.c1.headline.slice(0,40) + "...\") to its actual article content, and identified emotionally charged phrases in a social post designed to trigger " +
      state.c2.intended.split(',')[0].toLowerCase() + ".";

    document.getElementById('dash-redflag').textContent =
      "Absolute, urgent language standing in for evidence — phrases like \"" + state.c1.flagWords[0] + "\" and \"" + state.c2.flagPhrases[0] + "\" — designed to short-circuit careful reading.";

    document.getElementById('challenge1').classList.add('hidden');
    document.getElementById('challenge2').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('pstep-3').classList.add('done');
    document.getElementById('dashboard').scrollIntoView({behavior:'smooth', block:'start'});
  }

  document.getElementById('replay-btn').addEventListener('click', function(){
    // reset progress steps
    document.getElementById('pstep-1').classList.remove('done');
    document.getElementById('pstep-1').classList.add('active');
    document.getElementById('pstep-2').classList.remove('done','active');
    document.getElementById('pstep-3').classList.remove('done','active');

    state.metrics = {headline:null, source:null, emotion:null, audience:null};
    ['headline','source','emotion','audience'].forEach(function(k){
      document.getElementById('m-'+k).textContent = '—';
      document.getElementById('m-'+k+'-bar').style.width = '0%';
    });

    setupChallenge1();
    setupChallenge2();

    document.getElementById('dashboard').classList.add('hidden');
    document.getElementById('challenge2').classList.add('hidden');
    document.getElementById('challenge1').classList.remove('hidden');
    document.getElementById('challenge1').scrollIntoView({behavior:'smooth', block:'start'});
  });

  // ---------- Init ----------
  setupChallenge1();
  setupChallenge2();

})();
</script>
</body>
</html>
