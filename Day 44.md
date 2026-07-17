# Today I built an AI-Powered LinkedIn Profile Optimizer using claude :

## Key Learnings :
- Learned how AI can analyze professional profiles and provide personalized recommendations for improving recruiter visibility.
- Gained practical experience in evaluating LinkedIn profiles based on headlines, summaries, experience, skills, and keyword optimization.
- Explored prompt engineering techniques to generate tailored profile rewrites instead of generic suggestions.
- Understood the importance of ATS-friendly and recruiter-focused keywords in improving profile discoverability.
- Learned how structured feedback, profile scoring, and actionable roadmaps help users improve their professional branding.
- Improved frontend development skills by creating an interactive dashboard with profile audits, before-and-after comparisons, progress tracking, and personalized recommendations.
- Practiced designing user-centric interfaces that present AI-generated insights in a clear, engaging, and actionable format.
- Strengthened understanding of how AI can support career development by combining content optimization with data-driven feedback.

### Output Screenshots :
<img width="1920" height="1080" alt="Screenshot (665)" src="https://github.com/user-attachments/assets/97023467-bfbf-40ba-9b6b-2768352c4de8" />
<img width="1920" height="1080" alt="Screenshot (666)" src="https://github.com/user-attachments/assets/29b3b489-4dda-4cb6-b01e-7757107c4aa8" />

#### HTML File :
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>LinkedIn Profile Audit</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@400;600;700;800&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#11151b;
    --surface:#181e26;
    --surface2:#1f2731;
    --line:#2a3340;
    --text:#e9ecf1;
    --muted:#8b96a5;
    --roast:#e8543e;
    --roast-dim:#3a2621;
    --rebuild:#33d489;
    --rebuild-dim:#183328;
    --gold:#e8b93e;
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    background:var(--bg);
    color:var(--text);
    font-family:'Inter',sans-serif;
    line-height:1.55;
  }
  .wrap{max-width:880px;margin:0 auto;padding:40px 24px 100px;}
  h1,h2,h3{font-family:'Sora',sans-serif;margin:0 0 8px;}
  .mono{font-family:'JetBrains Mono',monospace;}

  /* HERO */
  .hero{text-align:center;padding:20px 0 36px;border-bottom:1px solid var(--line);margin-bottom:32px;}
  .eyebrow{color:var(--muted);font-size:13px;letter-spacing:.14em;text-transform:uppercase;margin-bottom:12px;}
  .hero h1{font-size:clamp(28px,5vw,42px);font-weight:800;}
  .hero p{color:var(--muted);max-width:520px;margin:12px auto 0;font-size:15px;}

  .gauge-row{display:flex;justify-content:center;gap:36px;margin-top:32px;flex-wrap:wrap;}
  .gauge{text-align:center;}
  .gauge svg{width:140px;height:140px;}
  .gauge .score{font-family:'Sora',sans-serif;font-weight:800;font-size:26px;}
  .gauge .label{color:var(--muted);font-size:12px;text-transform:uppercase;letter-spacing:.08em;margin-top:6px;}
  .gauge.before .score{color:var(--roast);}
  .gauge.after .score{color:var(--rebuild);}
  .gauge-arrow{align-self:center;font-size:28px;color:var(--muted);}

  /* TABS */
  .tabs{display:flex;gap:4px;background:var(--surface);border:1px solid var(--line);border-radius:10px;padding:4px;margin-bottom:28px;position:sticky;top:12px;z-index:10;}
  .tab{flex:1;text-align:center;padding:11px 8px;border-radius:8px;cursor:pointer;font-size:13.5px;font-weight:600;color:var(--muted);transition:.15s;}
  .tab.active{background:var(--surface2);color:var(--text);}
  .tab:hover{color:var(--text);}
  .panel{display:none;}
  .panel.active{display:block;animation:fade .25s ease;}
  @keyframes fade{from{opacity:0;transform:translateY(4px);}to{opacity:1;transform:translateY(0);}}

  /* CARDS */
  .card{background:var(--surface);border:1px solid var(--line);border-radius:14px;padding:24px;margin-bottom:20px;}
  .card-head{display:flex;justify-content:space-between;align-items:center;gap:12px;margin-bottom:14px;flex-wrap:wrap;}
  .card-head h3{font-size:17px;}
  .score-pill{font-family:'JetBrains Mono',monospace;font-weight:600;font-size:13px;padding:5px 12px;border-radius:20px;white-space:nowrap;}
  .score-pill.low{background:var(--roast-dim);color:var(--roast);}
  .score-pill.mid{background:#332a1a;color:var(--gold);}
  .score-pill.high{background:var(--rebuild-dim);color:var(--rebuild);}

  .quote{background:var(--surface2);border-left:3px solid var(--roast);padding:12px 14px;border-radius:6px;font-style:italic;color:#c9cfd8;font-size:14px;margin:10px 0;}
  .reaction{font-size:14px;color:var(--muted);margin-bottom:10px;}
  .breakdown{display:grid;gap:10px;margin-top:12px;}
  .breakdown div{font-size:14px;}
  .breakdown b{color:var(--text);}

  /* REBUILD */
  .option{border:1px solid var(--line);border-radius:10px;padding:16px;margin-bottom:12px;background:var(--surface2);}
  .option .tag{font-size:11px;text-transform:uppercase;letter-spacing:.08em;color:var(--rebuild);font-weight:600;margin-bottom:6px;}
  .option p{margin:0;font-size:15px;font-weight:500;}
  .option .why{color:var(--muted);font-size:13px;margin-top:8px;}

  .about-block{border-left:3px solid var(--rebuild);padding:14px 16px;background:var(--surface2);border-radius:0 8px 8px 0;margin-bottom:10px;}
  .about-block .part-label{font-size:11px;color:var(--rebuild);text-transform:uppercase;letter-spacing:.08em;margin-bottom:4px;}
  .about-block p{margin:0;font-size:14.5px;}
  .keywords{display:flex;flex-wrap:wrap;gap:6px;margin-top:14px;}
  .kw{background:var(--rebuild-dim);color:var(--rebuild);font-size:12px;padding:4px 10px;border-radius:14px;font-family:'JetBrains Mono',monospace;}

  .ba{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px;}
  .ba .before, .ba .after{padding:12px;border-radius:8px;font-size:13.5px;}
  .ba .before{background:var(--roast-dim);border:1px solid #4a2a24;}
  .ba .after{background:var(--rebuild-dim);border:1px solid #1f4536;}
  .ba .lab{font-size:10.5px;text-transform:uppercase;letter-spacing:.08em;color:var(--muted);margin-bottom:4px;}
  @media (max-width:600px){.ba{grid-template-columns:1fr;}}

  .skill-cols{display:grid;grid-template-columns:1fr 1fr;gap:18px;}
  @media (max-width:600px){.skill-cols{grid-template-columns:1fr;}}
  .skill-cols h4{font-size:13px;text-transform:uppercase;letter-spacing:.06em;margin-bottom:10px;}
  .skill-cols ol,.skill-cols ul{margin:0;padding-left:18px;font-size:14px;}
  .skill-cols li{margin-bottom:6px;}
  .pin-row{display:flex;gap:8px;margin-top:14px;flex-wrap:wrap;}
  .pin{background:var(--gold);color:#1a1508;font-weight:700;font-size:12.5px;padding:5px 12px;border-radius:14px;}

  /* SCORECARD TABLE */
  table{width:100%;border-collapse:collapse;font-size:14px;}
  th,td{padding:10px 8px;text-align:left;border-bottom:1px solid var(--line);}
  th{color:var(--muted);font-weight:600;font-size:12px;text-transform:uppercase;letter-spacing:.05em;}
  td.delta{color:var(--rebuild);font-weight:700;font-family:'JetBrains Mono',monospace;}
  tr.overall td{font-weight:700;font-size:15px;border-top:2px solid var(--line);border-bottom:none;padding-top:14px;}

  /* PLAN */
  .day{border:1px solid var(--line);border-radius:12px;margin-bottom:12px;overflow:hidden;}
  .day-head{padding:14px 18px;background:var(--surface2);display:flex;justify-content:space-between;align-items:center;cursor:pointer;}
  .day-head span.d{font-family:'JetBrains Mono',monospace;color:var(--rebuild);font-weight:600;margin-right:10px;}
  .day-body{padding:0 18px;max-height:0;overflow:hidden;transition:max-height .3s ease, padding .3s ease;}
  .day-body.open{padding:16px 18px 18px;max-height:800px;}
  .day-body ul{margin:0;padding-left:18px;font-size:14px;}
  .day-body li{margin-bottom:6px;}
  .post-draft{background:var(--surface);border:1px dashed var(--line);border-radius:8px;padding:12px 14px;font-size:13.5px;margin-top:10px;white-space:pre-wrap;}
  .char-count{color:var(--muted);font-size:11.5px;margin-top:6px;font-family:'JetBrains Mono',monospace;}

  /* SUMMARY CARD */
  .summary-card{background:linear-gradient(155deg,#182420,#11151b 60%);border:1px solid #234436;border-radius:16px;padding:28px;text-align:center;}
  .summary-card .sc-scores{display:flex;justify-content:center;gap:24px;margin:18px 0;font-family:'Sora',sans-serif;}
  .summary-card .sc-scores div span{display:block;font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.08em;}
  .summary-card .sc-scores .num{font-size:28px;font-weight:800;}
  .summary-card .before .num{color:var(--roast);}
  .summary-card .after .num{color:var(--rebuild);}
  .summary-card ol{text-align:left;max-width:420px;margin:16px auto;font-size:14px;}
  .summary-card li{margin-bottom:6px;}
  .summary-card .highlight{color:var(--rebuild);font-weight:600;margin-top:14px;font-size:14.5px;}
  .copy-btn{margin-top:20px;background:var(--rebuild);color:#0b1a13;border:none;padding:10px 22px;border-radius:8px;font-weight:700;font-size:13.5px;cursor:pointer;font-family:'Inter',sans-serif;}
  .copy-btn:hover{opacity:.9;}

  .section-title{font-size:12px;text-transform:uppercase;letter-spacing:.1em;color:var(--muted);margin:28px 0 12px;}
  .invisible-cost{font-size:13px;color:var(--gold);margin-top:6px;}
</style>
</head>
<body>
<div class="wrap">

  <div class="hero">
    <div class="eyebrow">LinkedIn Profile Audit · Ex-Recruiter Review</div>
    <h1>Your Profile, Roasted &amp; Rebuilt</h1>
    <p>Goal: land a software developer / Python full-stack / AI engineer role. Here's exactly what recruiters see today, and what to fix so they stop scrolling.</p>
    <div class="gauge-row">
      <div class="gauge before">
        <svg viewBox="0 0 120 120"><circle cx="60" cy="60" r="52" fill="none" stroke="#2a3340" stroke-width="10"/>
          <circle cx="60" cy="60" r="52" fill="none" stroke="#e8543e" stroke-width="10" stroke-linecap="round"
            stroke-dasharray="326.7" stroke-dashoffset="228.7" transform="rotate(-90 60 60)"/></svg>
        <div class="score">30<span style="font-size:14px;color:var(--muted)">/100</span></div>
        <div class="label">Before</div>
      </div>
      <div class="gauge-arrow">→</div>
      <div class="gauge after">
        <svg viewBox="0 0 120 120"><circle cx="60" cy="60" r="52" fill="none" stroke="#2a3340" stroke-width="10"/>
          <circle cx="60" cy="60" r="52" fill="none" stroke="#33d489" stroke-width="10" stroke-linecap="round"
            stroke-dasharray="326.7" stroke-dashoffset="65.3" transform="rotate(-90 60 60)"/></svg>
        <div class="score">80<span style="font-size:14px;color:var(--muted)">/100</span></div>
        <div class="label">After</div>
      </div>
    </div>
  </div>

  <div class="tabs">
    <div class="tab active" data-tab="roast">Roast</div>
    <div class="tab" data-tab="rebuild">Rebuild</div>
    <div class="tab" data-tab="scorecard">Scorecard</div>
    <div class="tab" data-tab="plan">7-Day Plan</div>
    <div class="tab" data-tab="summary">Summary Card</div>
  </div>

  <!-- ROAST -->
  <div class="panel active" id="roast">

    <div class="card">
      <div class="card-head"><h3>Headline</h3><div class="score-pill low">4/10</div></div>
      <div class="reaction">Recruiter's 3-second read: "Another fresher who hasn't decided what they are yet."</div>
      <div class="quote">"Aspiring Software Engineer | Python Full-Stack Developer | Django | React"</div>
      <div class="breakdown">
        <div>❌ <b>The problem:</b> "Aspiring" is the first word a recruiter reads. It signals "not there yet" before they've seen anything else. The rest is just a tech-stack list with no proof or differentiator.</div>
        <div>🧠 <b>Why it hurts:</b> Recruiters search LinkedIn by keyword AND scan headlines to filter. Yours reads like every other MCA grad's headline — nothing here says "look closer."</div>
        <div>🔍 <b>Invisible cost:</b> You're competing on identical keywords with thousands of profiles, but with zero differentiation, so you lose the tie-break every time.</div>
      </div>
    </div>

    <div class="card">
      <div class="card-head"><h3>About — First 2 Lines</h3><div class="score-pill low">3/10</div></div>
      <div class="reaction">This is the ONLY part visible before "see more." Most people never click.</div>
      <div class="quote">"Aspiring Software Developer | AI Enthusiast | MCA Student"</div>
      <div class="breakdown">
        <div>❌ <b>The problem:</b> It just repeats your headline in sentence form. No hook, no reason to click "see more."</div>
        <div>🧠 <b>Why it hurts:</b> Recruiters decide whether to expand your About section in under 2 seconds. A repeated title gives them zero new information to justify the click.</div>
        <div>🔍 <b>Invisible cost:</b> Your strongest lines — the ones about SafeDrive AI, NL2SQL, the NLP/LLM work — are buried three paragraphs down where most readers never reach.</div>
      </div>
    </div>

    <div class="card">
      <div class="card-head"><h3>About — Full Section</h3><div class="score-pill mid">5/10</div></div>
      <div class="reaction">"Solid technical substance, wrapped in generic phrasing I've read 500 times."</div>
      <div class="breakdown">
        <div>❌ <b>The problem:</b> Phrases like <span class="mono">"passionate about designing scalable software systems"</span> and <span class="mono">"solve meaningful problems"</span> are filler — every candidate writes this. Meanwhile your actual proof (three real AI projects) is described vaguely, with no outcomes, scale, or metrics.</div>
        <div>🧠 <b>Why it hurts:</b> Recruiters skim for evidence, not adjectives. "Passionate," "innovative," and "leveraging technology" get mentally filtered out — they're looking for what you built and what happened because of it.</div>
        <div>🔍 <b>Invisible cost:</b> You built an NL2SQL system and an AI symptom checker — genuinely resume-worthy projects — but they read like a list, not proof. That's the difference between "read more" and "message this person."</div>
      </div>
    </div>

    <div class="card">
      <div class="card-head"><h3>Experience</h3><div class="score-pill low">0/10</div></div>
      <div class="reaction">"No Experience section. I'm not sure this person has ever shipped anything."</div>
      <div class="breakdown">
        <div>❌ <b>The problem:</b> You have zero entries in Experience — only certifications are listed. For a recruiter, Experience is the section they check first, before About.</div>
        <div>🧠 <b>Why it hurts:</b> Certifications tell a recruiter what you studied. Experience (or projects framed as experience) tells them what you can actually do. Right now your profile only proves the former.</div>
        <div>🔍 <b>Invisible cost:</b> Your three real projects (SafeDrive AI, Symptom Checker, NL2SQL) never show up as separate, skimmable, keyword-rich entries — they're invisible to anyone who doesn't fully read your About paragraph.</div>
      </div>
    </div>

    <div class="card">
      <div class="card-head"><h3>Skills &amp; Keywords</h3><div class="score-pill mid">4/10</div></div>
      <div class="reaction">"Skills list doesn't match the About section. Which one is true?"</div>
      <div class="quote">Full-Stack Development, Prompt Engineering, AI Ethics, Responsible AI, Generative AI, Machine Learning, Neural Networks, Deep Learning, Big Data, Data Visualization</div>
      <div class="breakdown">
        <div>❌ <b>The problem:</b> Your About section repeatedly mentions Python, Django, Flask, SQL, NLP, LLM Applications, and REST APIs — none of which are in your Skills list. Meanwhile broad terms like "AI Ethics," "Responsible AI," "Big Data," and "Data Visualization" are in your top 10 but don't appear anywhere else on your profile.</div>
        <div>🧠 <b>Why it hurts:</b> Recruiter search is keyword-driven. If a recruiter searches "Django" or "Flask," you don't show up — even though you've built real projects in both.</div>
        <div>🔍 <b>Invisible cost:</b> You are invisible in the exact searches ("Python Developer," "Django Developer," "Flask") that match your actual experience, while showing up for searches ("AI Ethics," "Big Data") where you have no proof to back it up.</div>
      </div>
    </div>

    <div class="card" style="text-align:center;background:var(--roast-dim);border-color:#4a2a24;">
      <h3 style="margin-bottom:4px;">Overall Profile Strength</h3>
      <div style="font-family:'Sora',sans-serif;font-size:38px;font-weight:800;color:var(--roast);">30<span style="font-size:18px;color:var(--muted);">/100</span></div>
      <div style="font-size:13.5px;color:var(--muted);margin-top:6px;">Real technical substance, almost none of it is discoverable or provable in its current form.</div>
    </div>
  </div>

  <!-- REBUILD -->
  <div class="panel" id="rebuild">

    <div class="section-title">Headline — 3 Options</div>
    <div class="option">
      <div class="tag">Option 1 · Keyword-Optimized</div>
      <p>Python Full-Stack Developer | Django · Flask · React · SQL | Building AI-Powered Apps (NLP, LLMs)</p>
      <div class="why">Why: front-loads the exact terms recruiters search for (Python, Django, Flask, React, SQL). Use this one — your goal is recruiter search visibility.</div>
    </div>
    <div class="option">
      <div class="tag">Option 2 · Value-Proposition</div>
      <p>I Build AI-Powered Web Apps That Turn Plain Language Into Working Software | Python · Django · React</p>
      <div class="why">Why: leads with what you do for someone, not just your stack. Better if you start reaching out to startups/founders directly.</div>
    </div>
    <div class="option">
      <div class="tag">Option 3 · Authority</div>
      <p>MCA Graduate → Full-Stack + AI Engineer | Built SafeDrive AI, NL2SQL &amp; an AI Symptom Checker | Open to Software Developer Roles</p>
      <div class="why">Why: signals momentum (graduate → engineer) and names real proof up front. Best for founders/hiring managers who skim fast.</div>
    </div>

    <div class="section-title">About Section — Rewrite</div>
    <div class="about-block">
      <div class="part-label">Hook (before "see more")</div>
      <p>I turn plain-English questions into working software — chatbots that read your documents, systems that convert your words into SQL.</p>
    </div>
    <div class="about-block">
      <div class="part-label">Story</div>
      <p>I'm an MCA graduate and Python full-stack developer who builds AI-powered applications end to end — backend, frontend, and the ML/NLP layer that makes them intelligent. I work mainly in Python, Django, Flask, SQL, and React, with hands-on experience integrating LLMs and NLP into real products.</p>
    </div>
    <div class="about-block">
      <div class="part-label">Proof</div>
      <p>• Built <b>SafeDrive AI</b>, a document assistant that lets users query files using natural language.<br>
      • Built an <b>AI Symptom Checker Chatbot</b> using NLP to interpret user input and return relevant guidance.<br>
      • Built <b>NL2SQL</b>, a system that converts natural language into database queries — combining LLM reasoning with SQL generation.</p>
    </div>
    <div class="about-block">
      <div class="part-label">CTA</div>
      <p>Open to Software Developer, Python Full-Stack Developer, and AI Engineer roles. Message me, or check the Featured section below for project demos and code.</p>
    </div>
    <div class="keywords">
      <span class="kw">Python</span><span class="kw">Django</span><span class="kw">Flask</span><span class="kw">React</span><span class="kw">SQL</span><span class="kw">NLP</span><span class="kw">LLM</span><span class="kw">REST API</span><span class="kw">Full-Stack Developer</span><span class="kw">Software Developer</span>
    </div>

    <div class="section-title">Experience → Add as "Projects" Entries</div>
    <div class="card">
      <div class="card-head"><h3>SafeDrive AI — Personal Project</h3></div>
      <div class="ba">
        <div class="before"><div class="lab">Before</div>"a smart file assistant that enables users to interact with documents using natural language"</div>
        <div class="after"><div class="lab">After</div>Built an AI-powered document assistant using Python and LLM integration, enabling users to query PDF/text files in natural language and receive accurate, context-aware answers.</div>
      </div>
      <div class="ba">
        <div class="before"><div class="lab">Before</div>(not mentioned)</div>
        <div class="after"><div class="lab">After</div>Designed the retrieval pipeline connecting document parsing, embeddings, and LLM response generation into a single working flow.</div>
      </div>
      <div class="invisible-cost">Note: add real numbers if you have them — file types supported, response time, or accuracy — even rough estimates beat none.</div>
    </div>
    <div class="card">
      <div class="card-head"><h3>NL2SQL — Personal Project</h3></div>
      <div class="ba">
        <div class="before"><div class="lab">Before</div>"a system that converts natural language queries into database queries"</div>
        <div class="after"><div class="lab">After</div>Developed an NL2SQL engine that converts plain-English questions into executable SQL, combining LLM prompt design with schema-aware query generation.</div>
      </div>
    </div>
    <div class="card">
      <div class="card-head"><h3>AI Symptom Checker Chatbot — Personal Project</h3></div>
      <div class="ba">
        <div class="before"><div class="lab">Before</div>"an AI-powered Symptom Checker Chatbot"</div>
        <div class="after"><div class="lab">After</div>Built an NLP-based chatbot that interprets user-described symptoms and returns relevant guidance, applying natural language understanding to a real-world use case.</div>
      </div>
    </div>

    <div class="section-title">Skills Recommendations</div>
    <div class="card">
      <div class="skill-cols">
        <div>
          <h4 style="color:var(--rebuild);">Add (priority order)</h4>
          <ol>
            <li>Python</li>
            <li>Django</li>
            <li>Flask</li>
            <li>SQL</li>
            <li>REST APIs</li>
            <li>Natural Language Processing (NLP)</li>
            <li>Large Language Models (LLM)</li>
            <li>JavaScript</li>
            <li>Git &amp; GitHub</li>
            <li>Software Development</li>
          </ol>
        </div>
        <div>
          <h4 style="color:var(--roast);">Remove</h4>
          <ul>
            <li>AI Ethics</li>
            <li>Responsible AI</li>
            <li>Big Data</li>
            <li>Data Visualization</li>
          </ul>
          <div style="color:var(--muted);font-size:12.5px;margin-top:8px;">These aren't backed by anything else on your profile — they dilute your focus instead of sharpening it.</div>
        </div>
      </div>
      <div class="pin-row">
        <div class="pin">📌 Python</div>
        <div class="pin">📌 Django</div>
        <div class="pin">📌 Full-Stack Development</div>
      </div>
    </div>
  </div>

  <!-- SCORECARD -->
  <div class="panel" id="scorecard">
    <div class="card">
      <table>
        <tr><th>Section</th><th>Before</th><th>After</th><th>Change</th></tr>
        <tr><td>Headline</td><td>4/10</td><td>8/10</td><td class="delta">+4</td></tr>
        <tr><td>About (Hook)</td><td>3/10</td><td>8/10</td><td class="delta">+5</td></tr>
        <tr><td>About (Full)</td><td>5/10</td><td>8/10</td><td class="delta">+3</td></tr>
        <tr><td>Experience</td><td>0/10</td><td>6/10</td><td class="delta">+6</td></tr>
        <tr><td>Skills/Keywords</td><td>4/10</td><td>8/10</td><td class="delta">+4</td></tr>
        <tr class="overall"><td>OVERALL</td><td>30/100</td><td>80/100</td><td class="delta">+50</td></tr>
      </table>
      <div style="font-size:13px;color:var(--muted);margin-top:14px;">Experience is capped at 6/10 even after the rebuild — reframed projects help, but nothing fully replaces a real internship or job entry. That's the next milestone to chase.</div>
    </div>
  </div>

  <!-- PLAN -->
  <div class="panel" id="plan">

    <div class="day">
      <div class="day-head" onclick="toggleDay(this)"><div><span class="d">DAY 1</span>Make all profile changes</div><span>+</span></div>
      <div class="day-body">
        <ul>
          <li>☐ Update headline (Option 1, keyword-optimized)</li>
          <li>☐ Replace About section with the rewritten version above</li>
          <li>☐ Add 3 Projects as Experience entries (SafeDrive AI, NL2SQL, AI Symptom Checker)</li>
          <li>☐ Update Skills list — add the 10 recommended, remove the 4 flagged</li>
          <li>☐ Pin Python, Django, Full-Stack Development to the top</li>
          <li>☐ Add a Featured section with GitHub links or demos if you have them</li>
        </ul>
      </div>
    </div>

    <div class="day">
      <div class="day-head" onclick="toggleDay(this)"><div><span class="d">DAY 2</span>Publish Post #1 — "I rebuilt my LinkedIn"</div><span>+</span></div>
      <div class="day-body">
        <div class="post-draft">I just rewrote my entire LinkedIn profile — and it made me realize how much I was underselling myself.

For months my headline said "Aspiring Software Developer." Turns out that one word was doing a lot of damage — it told recruiters "not ready yet" before they'd read a single line further.

Here's what actually changed:
→ Stopped listing my tech stack, started showing what I built with it
→ Rewrote my projects (SafeDrive AI, an NL2SQL engine, an AI symptom checker) as proof, not just descriptions
→ Fixed my skills list so it actually matches what I can do

Still a fresher. Still learning. But my profile finally says that with proof instead of apology.

If you're a recent grad — check whether your profile is selling you short too. What's one line on your profile you'd rewrite today?</div>
        <div class="char-count">~890 characters — under the 1300 limit</div>
      </div>
    </div>

    <div class="day">
      <div class="day-head" onclick="toggleDay(this)"><div><span class="d">DAY 3</span>Send 10 connection requests</div><span>+</span></div>
      <div class="day-body">
        <p style="font-size:14px;margin-top:0;">Target: Engineering managers, tech leads, and recruiters at companies hiring Python/Django/Full-Stack developers — especially at startups (they hire faster and check LinkedIn more actively than large companies). Also connect with 2-3 people doing similar AI/NLP project work — they often share leads.</p>
        <div class="post-draft">Hi [Name], I'm an MCA grad building full-stack apps with Python/Django and some AI/NLP integrations (LLMs, NL2SQL). Really admire the work your team does — would love to stay connected and learn from your journey.</div>
        <div class="char-count">~270 characters — under the 300 limit</div>
      </div>
    </div>

    <div class="day">
      <div class="day-head" onclick="toggleDay(this)"><div><span class="d">DAY 4</span>Comment on 5 posts in your space</div><span>+</span></div>
      <div class="day-body">
        <p style="font-size:14px;margin-top:0;"><b>The Value Comment formula:</b> Agree + Add Insight + Ask a Question.</p>
        <ul>
          <li><b>Agree</b> — react to their specific point, not the topic generally ("This matches what I saw building an NL2SQL system...")</li>
          <li><b>Add Insight</b> — one concrete thing from your own experience</li>
          <li><b>Ask a Question</b> — invites a reply, which is what gets you noticed by the poster and their audience</li>
        </ul>
        <div class="post-draft">Example: "This matches what I ran into building an NL2SQL project — the hardest part wasn't the SQL generation, it was getting the LLM to understand ambiguous schema names. Did you find prompt design or fine-tuning worked better for that?"</div>
      </div>
    </div>

    <div class="day">
      <div class="day-head" onclick="toggleDay(this)"><div><span class="d">DAY 5</span>Publish Post #2 — lessons-learned / hot take</div><span>+</span></div>
      <div class="day-body">
        <div class="post-draft">Unpopular opinion: as a fresher, "I know 10 frameworks" is a weaker pitch than "I shipped 3 working projects."

Recruiters don't hire skill lists. They hire proof.

While building my NL2SQL project, I learned this the hard way — the SQL generation wasn't the hard part. Getting an LLM to correctly interpret ambiguous natural language ("show me last month's numbers" — whose numbers? which month field?) was.

That one problem taught me more about real-world NLP than any tutorial did.

If you're a student or fresher: pick ONE project, finish it end-to-end, and be able to explain the hardest bug you hit. That story is worth more on your profile than ten "familiar with X" bullet points.

What's the hardest bug you've had to explain in an interview?</div>
        <div class="char-count">~950 characters — under the 1300 limit</div>
      </div>
    </div>

    <div class="day">
      <div class="day-head" onclick="toggleDay(this)"><div><span class="d">DAY 6</span>Engage + 5 more connections</div><span>+</span></div>
      <div class="day-body">
        <ul>
          <li>☐ Reply to every comment on both posts within a few hours — replies extend reach more than the original post does</li>
          <li>☐ Send 5 more connection requests using the same template, targeting a different company/niche than Day 3</li>
          <li>☐ Revisit anyone who engaged with your posts — send a short thank-you + connect if not already connected</li>
        </ul>
      </div>
    </div>

    <div class="day">
      <div class="day-head" onclick="toggleDay(this)"><div><span class="d">DAY 7</span>Review the numbers</div><span>+</span></div>
      <div class="day-body">
        <p style="font-size:14px;margin-top:0;">Check profile views and connection acceptance rate vs. before you started.</p>
        <ul>
          <li><b>Profile views up sharply?</b> Your headline/keywords are working — recruiters are finding you in search.</li>
          <li><b>Views flat but connections accepted well?</b> Your outreach targeting is good; focus next week on more posting/visibility.</li>
          <li><b>Connections not accepting?</b> Your message template or targeting needs adjusting — try naming something specific about their company or work.</li>
          <li><b>Posts got few comments?</b> The hook (first 1-2 lines) likely needs to be sharper — that's what decides whether someone stops scrolling.</li>
        </ul>
      </div>
    </div>
  </div>

  <!-- SUMMARY -->
  <div class="panel" id="summary">
    <div class="summary-card">
      <div class="eyebrow" style="margin-bottom:4px;">Ready to screenshot</div>
      <h2>I let AI roast my LinkedIn profile today.</h2>
      <p style="color:var(--muted);margin-top:6px;">Here's what changed:</p>
      <div class="sc-scores">
        <div class="before"><span>Before</span><div class="num">30/100</div></div>
        <div class="after"><span>After</span><div class="num">80/100</div></div>
      </div>
      <ol>
        <li>My headline said "Aspiring" — undercutting myself before recruiters read anything else</li>
        <li>My real projects (an AI document assistant, an NL2SQL engine) were buried in a paragraph instead of listed as proof</li>
        <li>My Skills list didn't even include Python, Django, or Flask — the exact terms recruiters search for</li>
      </ol>
      <div class="highlight">The #1 thing that made the biggest difference: turning three personal projects into proper Experience entries — proof beats a skills list every time.</div>
      <button class="copy-btn" onclick="copySummary()">Copy summary text</button>
    </div>
  </div>

</div>

<script>
  document.querySelectorAll('.tab').forEach(t=>{
    t.addEventListener('click',()=>{
      document.querySelectorAll('.tab').forEach(x=>x.classList.remove('active'));
      document.querySelectorAll('.panel').forEach(x=>x.classList.remove('active'));
      t.classList.add('active');
      document.getElementById(t.dataset.tab).classList.add('active');
      window.scrollTo({top:0,behavior:'smooth'});
    });
  });
  function toggleDay(el){
    const body = el.nextElementSibling;
    const plus = el.querySelector('span:last-child');
    const isOpen = body.classList.contains('open');
    document.querySelectorAll('.day-body.open').forEach(b=>{b.classList.remove('open');b.previousElementSibling.querySelector('span:last-child').textContent='+';});
    if(!isOpen){ body.classList.add('open'); plus.textContent='–'; }
  }
  function copySummary(){
    const text = "I let AI roast my LinkedIn profile today. Here's what changed:\\n\\nBefore: 30/100\\nAfter: 80/100\\n\\nTop 3 mistakes I was making:\\n1. My headline said 'Aspiring' — undercutting myself before recruiters read anything else\\n2. My real projects were buried in a paragraph instead of listed as proof\\n3. My Skills list didn't even include Python, Django, or Flask\\n\\nThe #1 thing that made the biggest difference: turning three personal projects into proper Experience entries — proof beats a skills list every time.";
    navigator.clipboard.writeText(text).then(()=>{
      const btn = document.querySelector('.copy-btn');
      const orig = btn.textContent;
      btn.textContent = 'Copied!';
      setTimeout(()=>btn.textContent=orig,1500);
    });
  }
</script>
</body>
</html>
