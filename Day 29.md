# Today I Built Operation Lifeline: Supply Chain Crisis La using claude:

## Key Learnings :

- Learned that supply chain resilience depends on coordinating multiple stakeholders rather than optimizing a single process.
- Understood how disruptions propagate across procurement, manufacturing, warehousing, transportation, and customer fulfillment.
- Explored how inventory levels, supplier reliability, transportation delays, and production capacity collectively impact business continuity.
- Simulated real-world decision-making by prioritizing operational actions based on changing crisis conditions.
- Gained insight into balancing cost, speed, and service quality during supply chain disruptions.
- Learned the importance of risk monitoring through operational KPIs instead of relying on reactive responses.
- Designed a workflow that visualizes crisis progression, helping users understand dependencies between different supply chain stages.
- Structured complex logistics concepts into an interactive simulator that makes enterprise operations easier to understand.
- Used Claude to rapidly generate a functional UI, business workflow, and operational logic from a single detailed prompt.
- Reinforced how AI can accelerate the creation of educational business simulators while keeping domain-specific workflows realistic.

### Output Screenshots :
<img width="1920" height="1080" alt="Screenshot (462)" src="https://github.com/user-attachments/assets/9bdf453b-69a0-4ee9-bda4-ef6b85f80435" />
<img width="1920" height="1080" alt="Screenshot (461)" src="https://github.com/user-attachments/assets/251fe97e-89d0-45e5-9828-d000d6f8da2c" />

#### HTML File :

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Operation Lifeline: Supply Chain Crisis Lab</title>
<script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Space+Grotesk:wght@400;500;600;700&display=swap');

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #080c14;
    --surface: #0e1420;
    --surface2: #141c2e;
    --surface3: #1a2440;
    --border: rgba(99,130,210,0.13);
    --border2: rgba(99,130,210,0.22);
    --accent: #3d72ff;
    --accent2: #7c4fff;
    --accent3: #00d4aa;
    --accent4: #ff6b35;
    --accent5: #ffd700;
    --danger: #ff4757;
    --warn: #ffa502;
    --success: #2ed573;
    --text: #e8edf8;
    --text2: #8899c4;
    --text3: #5a6d9a;
    --glow: rgba(61,114,255,0.18);
    --glow2: rgba(124,79,255,0.15);
    --font-display: 'Space Grotesk', sans-serif;
    --font-body: 'Inter', sans-serif;
    --r: 14px;
    --r2: 20px;
    --transition: all 0.22s cubic-bezier(.4,0,.2,1);
  }

  html, body { height: 100%; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-body);
    font-size: 15px;
    line-height: 1.6;
    min-height: 100vh;
    overflow-x: hidden;
  }

  #root { min-height: 100vh; display: flex; flex-direction: column; }

  /* ── SCROLLBAR ── */
  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: var(--surface); }
  ::-webkit-scrollbar-thumb { background: var(--surface3); border-radius: 3px; }

  /* ── LAYOUT ── */
  .screen { min-height: 100vh; display: flex; flex-direction: column; align-items: center; justify-content: flex-start; padding: 40px 20px 60px; }
  .container { width: 100%; max-width: 860px; }
  .wide-container { width: 100%; max-width: 1060px; }

  /* ── WELCOME ── */
  .welcome-hero {
    min-height: 100vh;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    text-align: center; padding: 40px 20px;
    background: radial-gradient(ellipse 80% 60% at 50% 0%, rgba(61,114,255,0.12) 0%, transparent 70%),
                radial-gradient(ellipse 50% 40% at 80% 80%, rgba(124,79,255,0.08) 0%, transparent 60%);
  }
  .welcome-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(61,114,255,0.12); border: 1px solid rgba(61,114,255,0.3);
    border-radius: 100px; padding: 6px 16px; margin-bottom: 28px;
    font-size: 12px; font-weight: 600; letter-spacing: .08em; text-transform: uppercase; color: var(--accent);
  }
  .welcome-badge .dot { width: 6px; height: 6px; background: var(--accent3); border-radius: 50%; animation: pulse 2s infinite; }
  @keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:.5;transform:scale(1.4)} }

  .welcome-title {
    font-family: var(--font-display); font-size: clamp(36px,6vw,68px); font-weight: 700;
    line-height: 1.1; letter-spacing: -.02em; margin-bottom: 16px;
    background: linear-gradient(135deg, #fff 0%, #a8c0ff 50%, #7c4fff 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  }
  .welcome-subtitle { font-size: clamp(15px,2.5vw,19px); color: var(--text2); max-width: 540px; margin: 0 auto 40px; line-height: 1.7; }

  .welcome-meta { display: flex; gap: 24px; justify-content: center; flex-wrap: wrap; margin-bottom: 48px; }
  .welcome-meta-item { display: flex; align-items: center; gap: 8px; font-size: 13px; color: var(--text3); }
  .welcome-meta-item .icon { font-size: 16px; }

  /* ── BUTTONS ── */
  .btn {
    display: inline-flex; align-items: center; justify-content: center; gap: 8px;
    padding: 14px 28px; border-radius: var(--r); border: none; cursor: pointer;
    font-family: var(--font-body); font-size: 15px; font-weight: 600;
    transition: var(--transition); text-decoration: none; white-space: nowrap;
  }
  .btn-primary {
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    color: #fff; box-shadow: 0 0 32px rgba(61,114,255,0.35), 0 4px 16px rgba(0,0,0,0.4);
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 0 48px rgba(61,114,255,0.5), 0 8px 24px rgba(0,0,0,0.4); }
  .btn-primary:active { transform: translateY(0); }

  .btn-secondary {
    background: var(--surface2); color: var(--text); border: 1px solid var(--border2);
  }
  .btn-secondary:hover { background: var(--surface3); border-color: rgba(99,130,210,0.4); }

  .btn-outline {
    background: transparent; color: var(--accent); border: 1px solid rgba(61,114,255,0.4);
  }
  .btn-outline:hover { background: rgba(61,114,255,0.1); border-color: var(--accent); }

  .btn-danger {
    background: rgba(255,71,87,0.15); color: var(--danger); border: 1px solid rgba(255,71,87,0.3);
  }
  .btn-danger:hover { background: rgba(255,71,87,0.25); }

  .btn-lg { padding: 18px 40px; font-size: 17px; border-radius: var(--r2); }
  .btn-sm { padding: 8px 16px; font-size: 13px; border-radius: 8px; }
  .btn:disabled { opacity: 0.4; cursor: not-allowed; transform: none !important; }

  /* ── CARDS ── */
  .card {
    background: var(--surface2); border: 1px solid var(--border);
    border-radius: var(--r2); padding: 24px; transition: var(--transition);
  }
  .card:hover { border-color: var(--border2); background: var(--surface3); }
  .card-glow { box-shadow: 0 0 40px var(--glow); }
  .card-accent { border-color: rgba(61,114,255,0.35); background: linear-gradient(135deg, var(--surface2), rgba(61,114,255,0.04)); }

  .card-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 16px; }
  .card-grid-2 { display: grid; grid-template-columns: repeat(auto-fill, minmax(340px, 1fr)); gap: 16px; }

  /* ── SECTION HEADER ── */
  .section-header { margin-bottom: 32px; }
  .section-eyebrow {
    font-size: 11px; font-weight: 700; letter-spacing: .12em; text-transform: uppercase;
    color: var(--accent); margin-bottom: 10px; display: flex; align-items: center; gap: 8px;
  }
  .section-eyebrow::before { content: ''; display: block; width: 24px; height: 2px; background: var(--accent); border-radius: 2px; }
  .section-title { font-family: var(--font-display); font-size: clamp(22px,4vw,32px); font-weight: 700; color: var(--text); line-height: 1.2; margin-bottom: 10px; }
  .section-desc { color: var(--text2); font-size: 15px; line-height: 1.7; max-width: 600px; }

  /* ── STAT PILL ── */
  .stat-row { display: flex; gap: 12px; flex-wrap: wrap; margin-bottom: 24px; }
  .stat-pill {
    display: flex; align-items: center; gap: 8px;
    background: var(--surface3); border: 1px solid var(--border); border-radius: 100px;
    padding: 6px 14px; font-size: 13px; color: var(--text2); font-weight: 500;
  }
  .stat-pill .label { color: var(--text3); font-size: 11px; text-transform: uppercase; letter-spacing:.06em; }
  .stat-pill .value { color: var(--text); font-weight: 600; }

  /* ── COMPANY CARD ── */
  .company-header {
    background: linear-gradient(135deg, var(--surface2), rgba(61,114,255,0.06));
    border: 1px solid rgba(61,114,255,0.25); border-radius: var(--r2);
    padding: 28px 32px; margin-bottom: 24px;
    display: flex; align-items: flex-start; justify-content: space-between; gap: 20px; flex-wrap: wrap;
  }
  .company-logo {
    width: 52px; height: 52px; border-radius: 12px; display: flex; align-items: center; justify-content: center;
    font-size: 22px; font-weight: 800; font-family: var(--font-display);
    background: linear-gradient(135deg, var(--accent), var(--accent2)); color: #fff; flex-shrink: 0;
  }
  .company-name { font-family: var(--font-display); font-size: 22px; font-weight: 700; color: var(--text); }
  .company-industry { font-size: 13px; color: var(--accent3); font-weight: 600; text-transform: uppercase; letter-spacing:.06em; margin-top: 2px; }
  .company-revenue { font-family: var(--font-display); font-size: 28px; font-weight: 700; color: var(--text); }
  .company-revenue-label { font-size: 12px; color: var(--text3); text-transform: uppercase; letter-spacing:.06em; }

  .metric-card { background: var(--surface); border: 1px solid var(--border); border-radius: var(--r); padding: 18px 20px; }
  .metric-value { font-family: var(--font-display); font-size: 26px; font-weight: 700; color: var(--text); line-height: 1; margin-bottom: 4px; }
  .metric-label { font-size: 12px; color: var(--text3); text-transform: uppercase; letter-spacing:.06em; }
  .metric-sub { font-size: 12px; color: var(--text2); margin-top: 2px; }

  /* ── CRISIS ── */
  .crisis-card {
    background: linear-gradient(135deg, rgba(255,71,87,0.08), rgba(255,107,53,0.06));
    border: 1px solid rgba(255,71,87,0.3); border-radius: var(--r2); padding: 28px 32px; margin-bottom: 24px;
    position: relative; overflow: hidden;
  }
  .crisis-card::before {
    content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px;
    background: linear-gradient(90deg, var(--danger), var(--accent4));
  }
  .crisis-icon { font-size: 48px; margin-bottom: 16px; }
  .crisis-name { font-family: var(--font-display); font-size: 26px; font-weight: 700; color: #fff; margin-bottom: 8px; }
  .crisis-desc { font-size: 15px; color: rgba(232,237,248,0.8); line-height: 1.7; margin-bottom: 20px; }
  .crisis-badge {
    display: inline-flex; align-items: center; gap: 6px; padding: 6px 14px; border-radius: 100px;
    font-size: 12px; font-weight: 700; text-transform: uppercase; letter-spacing:.08em;
  }
  .urgency-critical { background: rgba(255,71,87,0.2); color: var(--danger); border: 1px solid rgba(255,71,87,0.4); }
  .urgency-high { background: rgba(255,165,2,0.2); color: var(--warn); border: 1px solid rgba(255,165,2,0.4); }
  .urgency-medium { background: rgba(255,214,0,0.15); color: var(--accent5); border: 1px solid rgba(255,214,0,0.3); }

  .impact-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(140px, 1fr)); gap: 10px; margin-top: 20px; }
  .impact-item {
    background: rgba(0,0,0,0.25); border: 1px solid rgba(255,71,87,0.15);
    border-radius: 10px; padding: 12px 14px;
  }
  .impact-label { font-size: 11px; color: rgba(232,237,248,0.5); text-transform: uppercase; letter-spacing:.06em; margin-bottom: 4px; }
  .impact-value { font-size: 16px; font-weight: 700; color: var(--danger); }

  /* ── ACTIONS ── */
  .action-card {
    background: var(--surface2); border: 1px solid var(--border); border-radius: var(--r2); padding: 22px;
    cursor: pointer; transition: var(--transition); position: relative; overflow: hidden;
    display: flex; flex-direction: column; gap: 10px;
  }
  .action-card:hover { border-color: rgba(61,114,255,0.4); background: var(--surface3); transform: translateY(-2px); }
  .action-card.selected {
    border-color: var(--accent); background: linear-gradient(135deg, rgba(61,114,255,0.12), rgba(124,79,255,0.08));
    box-shadow: 0 0 24px rgba(61,114,255,0.2);
  }
  .action-card.selected::before {
    content: '✓'; position: absolute; top: 14px; right: 14px;
    width: 24px; height: 24px; background: var(--accent); border-radius: 50%;
    display: flex; align-items: center; justify-content: center; font-size: 12px; font-weight: 700; color: #fff;
    display: grid; place-items: center;
  }
  .action-icon { font-size: 28px; }
  .action-name { font-family: var(--font-display); font-size: 16px; font-weight: 700; color: var(--text); }
  .action-desc { font-size: 13px; color: var(--text2); line-height: 1.6; }
  .action-why { font-size: 12px; color: var(--accent3); line-height: 1.5; padding: 8px 12px; background: rgba(0,212,170,0.07); border-radius: 8px; border-left: 2px solid var(--accent3); }
  .action-effects { display: flex; gap: 6px; flex-wrap: wrap; }
  .effect-tag {
    font-size: 11px; padding: 3px 9px; border-radius: 6px; font-weight: 600;
    background: rgba(61,114,255,0.12); color: var(--accent); border: 1px solid rgba(61,114,255,0.2);
  }
  .effect-tag.neg { background: rgba(255,71,87,0.1); color: var(--danger); border-color: rgba(255,71,87,0.2); }
  .effect-tag.pos { background: rgba(46,213,115,0.1); color: var(--success); border-color: rgba(46,213,115,0.2); }

  /* ── PROGRESS BARS ── */
  .metric-bar-wrap { margin-bottom: 18px; }
  .metric-bar-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px; }
  .metric-bar-label { font-size: 13px; font-weight: 600; color: var(--text2); display: flex; align-items: center; gap: 6px; }
  .metric-bar-value { font-size: 14px; font-weight: 700; color: var(--text); font-family: var(--font-display); }
  .metric-bar-track { height: 8px; background: rgba(255,255,255,0.07); border-radius: 100px; overflow: hidden; }
  .metric-bar-fill { height: 100%; border-radius: 100px; transition: width 1.2s cubic-bezier(.4,0,.2,1); }
  .bar-blue { background: linear-gradient(90deg, var(--accent), var(--accent2)); }
  .bar-green { background: linear-gradient(90deg, var(--accent3), #00b894); }
  .bar-red { background: linear-gradient(90deg, var(--danger), #ff6b8a); }
  .bar-orange { background: linear-gradient(90deg, var(--accent4), var(--warn)); }
  .bar-gold { background: linear-gradient(90deg, var(--accent5), #ffb347); }

  .delta { font-size: 12px; font-weight: 600; padding: 2px 7px; border-radius: 6px; margin-left: 6px; }
  .delta-pos { background: rgba(46,213,115,0.15); color: var(--success); }
  .delta-neg { background: rgba(255,71,87,0.15); color: var(--danger); }
  .delta-neu { background: rgba(255,255,255,0.07); color: var(--text3); }

  /* ── NEGOTIATION ── */
  .negotiation-header {
    background: linear-gradient(135deg, rgba(124,79,255,0.1), rgba(61,114,255,0.05));
    border: 1px solid rgba(124,79,255,0.25); border-radius: var(--r2); padding: 24px; margin-bottom: 24px;
  }
  .trust-meter { display: flex; align-items: center; gap: 16px; }
  .trust-bar { flex: 1; height: 10px; background: rgba(255,255,255,0.07); border-radius: 100px; overflow: hidden; }
  .trust-fill { height: 100%; background: linear-gradient(90deg, var(--accent2), var(--accent3)); border-radius: 100px; transition: width 0.8s cubic-bezier(.4,0,.2,1); }

  .round-card { background: var(--surface); border: 1px solid var(--border); border-radius: var(--r2); padding: 24px; margin-bottom: 20px; }
  .round-label { font-size: 11px; font-weight: 700; letter-spacing:.1em; text-transform: uppercase; color: var(--accent2); margin-bottom: 12px; display: flex; align-items: center; gap: 8px; }
  .round-question { font-size: 17px; font-weight: 600; color: var(--text); margin-bottom: 8px; line-height: 1.5; }
  .round-context { font-size: 13px; color: var(--text2); margin-bottom: 20px; line-height: 1.6; padding: 12px; background: rgba(255,255,255,0.03); border-radius: 10px; border-left: 2px solid rgba(124,79,255,0.4); }

  .choice-btn {
    width: 100%; text-align: left; background: var(--surface2); border: 1px solid var(--border);
    border-radius: var(--r); padding: 16px 18px; cursor: pointer; transition: var(--transition);
    margin-bottom: 10px; color: var(--text); font-family: var(--font-body); font-size: 14px; line-height: 1.5;
    display: flex; align-items: flex-start; gap: 12px;
  }
  .choice-btn:hover { background: var(--surface3); border-color: var(--border2); transform: translateX(4px); }
  .choice-btn.chosen { background: rgba(124,79,255,0.12); border-color: var(--accent2); }
  .choice-btn .choice-key { 
    min-width: 28px; height: 28px; border-radius: 8px; display: grid; place-items: center;
    background: rgba(255,255,255,0.07); font-size: 13px; font-weight: 700; color: var(--text3); flex-shrink: 0; margin-top: 1px;
  }
  .choice-btn.chosen .choice-key { background: var(--accent2); color: #fff; }

  /* ── CEO QUESTIONS ── */
  .question-card { background: var(--surface); border: 1px solid var(--border); border-radius: var(--r2); padding: 28px; margin-bottom: 20px; }
  .q-number { font-size: 11px; font-weight: 700; color: var(--accent); text-transform: uppercase; letter-spacing:.1em; margin-bottom: 12px; }
  .q-text { font-size: 18px; font-weight: 600; color: var(--text); margin-bottom: 8px; line-height: 1.5; }
  .q-context { font-size: 14px; color: var(--text2); margin-bottom: 20px; line-height: 1.6; background: rgba(255,255,255,0.03); padding: 12px; border-radius: 10px; }
  .q-options { display: grid; gap: 10px; }
  .q-opt {
    background: var(--surface2); border: 1px solid var(--border); border-radius: var(--r);
    padding: 14px 18px; cursor: pointer; transition: var(--transition); text-align: left;
    font-family: var(--font-body); font-size: 14px; color: var(--text); line-height: 1.5;
    display: flex; align-items: center; gap: 10px;
  }
  .q-opt:hover:not(:disabled) { background: var(--surface3); border-color: var(--border2); }
  .q-opt.correct { background: rgba(46,213,115,0.1); border-color: rgba(46,213,115,0.4); color: var(--success); }
  .q-opt.wrong { background: rgba(255,71,87,0.1); border-color: rgba(255,71,87,0.4); color: var(--danger); }
  .q-opt:disabled { cursor: default; }
  .q-feedback { margin-top: 14px; padding: 12px 16px; border-radius: 10px; font-size: 13px; line-height: 1.6; }
  .q-feedback.good { background: rgba(46,213,115,0.08); border: 1px solid rgba(46,213,115,0.2); color: var(--success); }
  .q-feedback.bad { background: rgba(255,71,87,0.08); border: 1px solid rgba(255,71,87,0.2); color: #ff8090; }

  /* ── AI INVESTMENTS ── */
  .ai-card {
    background: var(--surface2); border: 1px solid var(--border); border-radius: var(--r2); padding: 22px;
    cursor: pointer; transition: var(--transition); position: relative;
  }
  .ai-card:hover { border-color: rgba(0,212,170,0.4); background: var(--surface3); transform: translateY(-2px); }
  .ai-card.selected {
    border-color: var(--accent3); background: linear-gradient(135deg, rgba(0,212,170,0.08), transparent);
    box-shadow: 0 0 24px rgba(0,212,170,0.15);
  }
  .ai-card.selected::before {
    content: '✓'; position: absolute; top: 14px; right: 14px;
    width: 22px; height: 22px; background: var(--accent3); border-radius: 50%;
    display: grid; place-items: center; font-size: 12px; font-weight: 700; color: #000;
  }
  .ai-icon { font-size: 32px; margin-bottom: 12px; }
  .ai-name { font-family: var(--font-display); font-size: 16px; font-weight: 700; color: var(--text); margin-bottom: 6px; }
  .ai-desc { font-size: 13px; color: var(--text2); line-height: 1.6; margin-bottom: 12px; }
  .ai-roi { display: flex; gap: 8px; flex-wrap: wrap; }
  .roi-tag { font-size: 11px; padding: 4px 10px; border-radius: 6px; font-weight: 600; background: rgba(0,212,170,0.1); color: var(--accent3); border: 1px solid rgba(0,212,170,0.2); }

  /* ── FINAL DASHBOARD ── */
  .score-circle {
    width: 140px; height: 140px; border-radius: 50%; position: relative;
    display: flex; align-items: center; justify-content: center; flex-direction: column;
    background: conic-gradient(var(--accent) 0deg, var(--accent2) var(--angle), rgba(255,255,255,0.05) var(--angle));
    flex-shrink: 0;
  }
  .score-circle-inner {
    width: 110px; height: 110px; border-radius: 50%; background: var(--bg);
    display: flex; align-items: center; justify-content: center; flex-direction: column;
    position: absolute;
  }
  .score-number { font-family: var(--font-display); font-size: 36px; font-weight: 800; color: var(--text); line-height: 1; }
  .score-label { font-size: 11px; color: var(--text3); text-transform: uppercase; letter-spacing:.06em; margin-top: 3px; }

  .grade-badge {
    font-family: var(--font-display); font-size: 48px; font-weight: 800; line-height: 1;
    padding: 8px 20px; border-radius: 12px;
  }

  .feedback-card { background: var(--surface); border: 1px solid var(--border); border-radius: var(--r2); padding: 24px; margin-bottom: 16px; }
  .feedback-title { font-size: 13px; font-weight: 700; text-transform: uppercase; letter-spacing:.08em; margin-bottom: 12px; display: flex; align-items: center; gap: 8px; }
  .feedback-text { font-size: 15px; color: var(--text2); line-height: 1.7; }

  .lesson-item {
    display: flex; align-items: flex-start; gap: 12px; padding: 14px 0;
    border-bottom: 1px solid var(--border);
  }
  .lesson-item:last-child { border-bottom: none; }
  .lesson-num { min-width: 28px; height: 28px; border-radius: 8px; background: rgba(61,114,255,0.15); color: var(--accent); display: grid; place-items: center; font-size: 13px; font-weight: 700; flex-shrink: 0; margin-top: 1px; }
  .lesson-text { font-size: 14px; color: var(--text2); line-height: 1.6; }

  /* ── PROGRESS STEPPER ── */
  .stepper { display: flex; gap: 0; align-items: center; justify-content: center; margin-bottom: 48px; flex-wrap: wrap; gap: 4px; }
  .step {
    display: flex; align-items: center; gap: 8px; padding: 8px 14px; border-radius: 100px;
    font-size: 12px; font-weight: 600; color: var(--text3); transition: var(--transition);
  }
  .step.active { background: rgba(61,114,255,0.15); color: var(--accent); }
  .step.done { color: var(--accent3); }
  .step-num { width: 22px; height: 22px; border-radius: 50%; display: grid; place-items: center; font-size: 11px; font-weight: 700; background: rgba(255,255,255,0.07); color: var(--text3); flex-shrink: 0; }
  .step.active .step-num { background: var(--accent); color: #fff; }
  .step.done .step-num { background: var(--accent3); color: #000; font-size: 13px; }
  .step-connector { width: 20px; height: 1px; background: var(--border); flex-shrink: 0; }

  /* ── DIVIDER ── */
  .divider { height: 1px; background: var(--border); margin: 28px 0; }

  /* ── TAG ── */
  .tag { display: inline-flex; align-items: center; gap: 4px; padding: 3px 9px; border-radius: 6px; font-size: 12px; font-weight: 600; }
  .tag-blue { background: rgba(61,114,255,0.15); color: var(--accent); }
  .tag-green { background: rgba(0,212,170,0.12); color: var(--accent3); }
  .tag-red { background: rgba(255,71,87,0.12); color: var(--danger); }
  .tag-orange { background: rgba(255,107,53,0.15); color: var(--accent4); }
  .tag-purple { background: rgba(124,79,255,0.15); color: var(--accent2); }

  /* ── ANIMATIONS ── */
  @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
  .animate-in { animation: fadeInUp 0.4s ease both; }
  .animate-fade { animation: fadeIn 0.4s ease both; }
  .delay-1 { animation-delay: 0.1s; }
  .delay-2 { animation-delay: 0.2s; }
  .delay-3 { animation-delay: 0.3s; }
  .delay-4 { animation-delay: 0.4s; }
  .delay-5 { animation-delay: 0.5s; }

  /* ── NOTIFICATION ── */
  .notify {
    position: fixed; bottom: 28px; left: 50%; transform: translateX(-50%);
    background: var(--surface3); border: 1px solid var(--border2);
    border-radius: var(--r); padding: 14px 24px; font-size: 14px; font-weight: 500; color: var(--text);
    box-shadow: 0 8px 32px rgba(0,0,0,0.5); z-index: 1000; animation: fadeInUp .3s ease;
    display: flex; align-items: center; gap: 10px; max-width: 420px; text-align: center;
  }

  /* ── RESPONSIVE ── */
  @media(max-width: 600px) {
    .card-grid-2 { grid-template-columns: 1fr; }
    .company-header { flex-direction: column; }
    .stepper { display: none; }
    .card { padding: 18px; }
  }

  /* ── TOOLTIP ── */
  .tooltip-wrap { position: relative; display: inline-flex; }
  .tooltip-icon { width: 18px; height: 18px; border-radius: 50%; background: rgba(255,255,255,0.08); display: grid; place-items: center; font-size: 11px; font-weight: 700; color: var(--text3); cursor: help; }
  .tooltip-box {
    position: absolute; bottom: calc(100% + 8px); left: 50%; transform: translateX(-50%);
    background: var(--surface3); border: 1px solid var(--border2); border-radius: 10px; padding: 10px 14px;
    font-size: 13px; color: var(--text2); line-height: 1.5; white-space: nowrap; max-width: 240px; white-space: normal;
    z-index: 100; box-shadow: 0 8px 24px rgba(0,0,0,0.5); pointer-events: none;
    display: none;
  }
  .tooltip-wrap:hover .tooltip-box { display: block; }

  /* ── BACK BUTTON ── */
  .back-row { display: flex; align-items: center; gap: 12px; margin-bottom: 32px; }

  /* INFO PANEL */
  .info-box { background: rgba(61,114,255,0.06); border: 1px solid rgba(61,114,255,0.2); border-radius: var(--r); padding: 14px 18px; margin-bottom: 20px; font-size: 13px; color: var(--text2); line-height: 1.6; }
  .info-box strong { color: var(--accent); }

  .selection-counter { 
    position: sticky; bottom: 20px; background: var(--surface3); border: 1px solid var(--border2);
    border-radius: var(--r); padding: 14px 20px; display: flex; align-items: center; justify-content: space-between;
    box-shadow: 0 8px 32px rgba(0,0,0,0.5); z-index: 50; margin-top: 24px;
  }
</style>
</head>
<body>
<div id="root"></div>
<script type="text/babel">
const { useState, useEffect, useRef } = React;

// ──────────────────────────────────────────────────────────────
// DATA
// ──────────────────────────────────────────────────────────────

const INDUSTRIES = [
  { name: 'Consumer Electronics', icon: '💻' }, { name: 'Pharmaceutical', icon: '💊' },
  { name: 'Automotive', icon: '🚗' }, { name: 'Food & Beverage', icon: '🥤' },
  { name: 'Aerospace', icon: '✈️' }, { name: 'Textile & Apparel', icon: '👗' },
  { name: 'Industrial Equipment', icon: '⚙️' }, { name: 'Medical Devices', icon: '🏥' }
];

const COMPANY_PREFIXES = ['Apex','Nexus','Vega','Orion','Helix','Nova','Titan','Atlas','Zenith','Crest'];
const COMPANY_SUFFIXES = ['Systems','Global','Dynamics','Industries','Corp','Solutions','Ventures','Holdings'];

const COUNTRIES = ['USA','Germany','China','India','Brazil','Vietnam','Mexico','South Korea','Taiwan','Japan','Malaysia','Thailand'];

const CRISES = [
  {
    id: 'fire', icon: '🔥', name: 'Factory Fire',
    desc: "A fire has broken out at one of your key production facilities. Firefighters have contained the blaze, but the facility will be offline for weeks. Insurance adjusters are on-site. Production is at a halt.",
    urgency: 'critical',
    context: "Factory fires can happen due to electrical faults, equipment failure, or human error. They not only destroy inventory and equipment but also halt production, disrupt supplier payments, and damage customer confidence.",
    impacts: { revenueRisk: '$42M', productionLoss: '60%', timeToRecover: '6 weeks', stockImpact: '-18%' }
  },
  {
    id: 'bankruptcy', icon: '💸', name: 'Supplier Bankruptcy',
    desc: "Your second-largest raw material supplier has filed for Chapter 11 bankruptcy. They supply 40% of a critical component. Their production line is frozen and your safety stock covers only 9 days.",
    urgency: 'critical',
    context: "Supplier bankruptcies are a hidden risk in most supply chains. Companies that rely heavily on a single supplier for key inputs are extremely vulnerable. This is a lesson in supplier diversification.",
    impacts: { revenueRisk: '$28M', productionLoss: '40%', timeToRecover: '8 weeks', stockImpact: '-12%' }
  },
  {
    id: 'strike', icon: '⚓', name: 'Port Strike',
    desc: "Dockworkers at the Port of Rotterdam — your primary European hub — have gone on strike indefinitely. 18 containers of finished goods worth $12M are stuck at sea. Retailers are threatening to cancel orders.",
    urgency: 'high',
    context: "Port strikes are surprisingly common and can ripple through global supply chains for months. Air freight alternatives exist but cost 5-7x more. Companies without multi-port strategies get hit hardest.",
    impacts: { revenueRisk: '$12M', productionLoss: '25%', timeToRecover: '3 weeks', stockImpact: '-8%' }
  },
  {
    id: 'cyber', icon: '🔐', name: 'Cyberattack',
    desc: "A ransomware attack has encrypted your warehouse management system and ERP. Attackers are demanding $3.2M. Your team cannot track inventory, process orders, or communicate with logistics partners.",
    urgency: 'critical',
    context: "Cyberattacks on supply chain software are the fastest-growing threat in the industry. A compromised WMS or ERP can bring operations to a standstill within hours, affecting every downstream customer.",
    impacts: { revenueRisk: '$35M', productionLoss: '70%', timeToRecover: '4 weeks', stockImpact: '-22%' }
  },
  {
    id: 'flood', icon: '🌊', name: 'Regional Flood',
    desc: "Severe flooding across Southeast Asia has submerged two of your three regional warehouses and blocked primary logistics roads. Inventory worth $18M is at risk. Rescue operations are underway.",
    urgency: 'high',
    context: "Climate-related disruptions are increasing in frequency. Companies with warehouses in flood-prone regions face repeated shocks. Geographic diversification of storage is now a strategic necessity.",
    impacts: { revenueRisk: '$18M', productionLoss: '35%', timeToRecover: '5 weeks', stockImpact: '-10%' }
  },
  {
    id: 'shortage', icon: '🪨', name: 'Raw Material Shortage',
    desc: "A global shortage of lithium carbonate (a key component in your products) has pushed prices up 340% in three months. Three competitors are fighting for the same limited supply. Your Q3 production targets are at risk.",
    urgency: 'high',
    context: "Commodity shortages occur when demand outstrips mining or extraction capacity. Being at the mercy of spot market prices destroys margins. Long-term contracts and material substitution are key strategies.",
    impacts: { revenueRisk: '$22M', productionLoss: '45%', timeToRecover: '10 weeks', stockImpact: '-14%' }
  },
  {
    id: 'political', icon: '⚡', name: 'Political Conflict',
    desc: "Escalating geopolitical tensions between two key trade partners have resulted in new export restrictions. Your primary supplier in the affected region cannot ship goods. Tariffs on imports have tripled overnight.",
    urgency: 'critical',
    context: "Geopolitical risks are one of the hardest to predict but most damaging to supply chains. Companies that concentrate sourcing in politically unstable regions are repeatedly caught off guard.",
    impacts: { revenueRisk: '$31M', productionLoss: '50%', timeToRecover: '12 weeks', stockImpact: '-19%' }
  },
  {
    id: 'shipping', icon: '🚢', name: 'Shipping Network Collapse',
    desc: "A major logistics carrier has gone bankrupt. Ocean freight rates have spiked 800% as capacity evaporates. Your shipments worth $24M are in limbo, with no ETA. Contracts with retailers include penalty clauses.",
    urgency: 'high',
    context: "Carrier failures expose companies that over-concentrate their shipping relationships. Freight rate volatility can turn profitable products into loss-makers overnight. Carrier diversification is critical.",
    impacts: { revenueRisk: '$24M', productionLoss: '30%', timeToRecover: '7 weeks', stockImpact: '-11%' }
  }
];

const ACTIONS = [
  {
    id: 'alt_supplier', icon: '🔍', name: 'Activate Backup Supplier',
    desc: 'Immediately qualify and onboard your secondary supplier list. Pay a 20% premium to get them producing your components within 72 hours.',
    why: 'Backup suppliers are expensive but they keep your production line alive. Without them, you stop shipping entirely.',
    effects: { cost: -12, inventory: +8, profit: -8, deliverySpeed: +10, satisfaction: +12 },
    tags: ['+Inventory', '+Delivery', '-Cost']
  },
  {
    id: 'air_freight', icon: '✈️', name: 'Emergency Air Freight',
    desc: 'Divert all critical shipments to air freight. Cost is 6x ocean freight, but delivery times drop from 30 days to 3 days.',
    why: 'When you promise customers a delivery date, missing it destroys trust. Air freight is expensive insurance.',
    effects: { cost: -18, inventory: +5, profit: -14, deliverySpeed: +20, satisfaction: +10 },
    tags: ['+Delivery', '+Satisfaction', '-Cost', '-Profit']
  },
  {
    id: 'reduce_skus', icon: '📦', name: 'Reduce SKU Count',
    desc: 'Temporarily cut your product range by 40%. Concentrate all production capacity and inventory on your top 20 revenue-generating products.',
    why: 'Fewer products means better service levels for each one. Customers prefer reliable supply of key products over unreliable supply of all products.',
    effects: { cost: +8, inventory: +15, profit: -5, deliverySpeed: +8, satisfaction: +6 },
    tags: ['+Inventory', '+Cost Savings', '+Delivery']
  },
  {
    id: 'customer_comms', icon: '📣', name: 'Proactive Customer Communication',
    desc: 'Send dedicated account managers to every major customer. Be transparent about delays, offer partial shipments, and renegotiate deadlines before they escalate.',
    why: 'Customers forgive supply disruptions if you communicate early and honestly. They do not forgive being surprised.',
    effects: { cost: -4, inventory: 0, profit: +2, deliverySpeed: 0, satisfaction: +20 },
    tags: ['+Satisfaction', '+Trust', 'Low Cost']
  },
  {
    id: 'inventory_share', icon: '🤝', name: 'Cross-Dock Inventory Pooling',
    desc: 'Partner with two non-competing companies in your industry to share excess warehouse inventory and logistics capacity.',
    why: 'Industry collaboration in a crisis is underused. You may have excess of what they need, and vice versa — mutual benefit without cash outlay.',
    effects: { cost: +5, inventory: +12, profit: +4, deliverySpeed: +6, satisfaction: +8 },
    tags: ['+Inventory', '+Collaboration', 'Low Risk']
  },
  {
    id: 'demand_pause', icon: '⏸️', name: 'Demand Smoothing Protocol',
    desc: 'Implement a temporary allocation system. Cap orders from each customer based on historical demand. Prevent hoarding behavior that would deplete your stock.',
    why: 'In crises, customers panic-order twice what they need, which empties your warehouses and starves others. Allocation systems keep the system fair and stable.',
    effects: { cost: +3, inventory: +18, profit: -3, deliverySpeed: -5, satisfaction: -5 },
    tags: ['+Inventory', 'Fairness', '-Satisfaction']
  }
];

const NEG_ROUNDS = [
  {
    id: 1, label: 'Round 1 — Opening Position',
    question: 'Your supplier\'s team enters with a hardened face. They open: "Given market conditions, we need a 35% price increase and can only guarantee 60% of your usual volume." How do you respond?',
    context: 'This is a classic opening gambit — anchor high on price, low on volume. Your goal in Round 1 is to establish your own position without burning bridges. Showing data signals competence; emotional appeals backfire at this stage.',
    choices: [
      { text: 'Present data showing industry average price increases are only 12%. Propose a 14% increase with full volume.', trust: +5, price: +3, lead: +2, label: 'A' },
      { text: 'Accept their terms immediately to preserve the relationship.', trust: +8, price: -12, lead: +0, label: 'B' },
      { text: 'Walk out, saying you will find another supplier.', trust: -15, price: +8, lead: -5, label: 'C' },
      { text: 'Ask for 6-week negotiation delay to "study the numbers."', trust: -3, price: +0, lead: -8, label: 'D' }
    ]
  },
  {
    id: 2, label: 'Round 2 — Counter Proposal',
    question: 'The supplier softens slightly: "We can do 18% increase, but only if you sign a 3-year exclusivity agreement." This would lock you in. How do you negotiate?',
    context: 'Exclusivity agreements feel reassuring but they eliminate your negotiating power for the next 3 years and expose you to supplier failure risk. Counter-proposing a performance clause converts a constraint into a partnership.',
    choices: [
      { text: 'Propose a 2-year preferred-supplier agreement (not exclusivity) with a volume commitment tied to their performance KPIs.', trust: +8, price: +5, lead: +3, label: 'A' },
      { text: 'Sign the 3-year exclusivity. The certainty is worth it.', trust: +5, price: -5, lead: +0, label: 'B' },
      { text: 'Reject entirely and propose month-to-month contracts only.', trust: -10, price: +2, lead: -4, label: 'C' },
      { text: 'Ask for an independent arbitration clause as a condition of any deal.', trust: +2, price: +1, lead: +1, label: 'D' }
    ]
  },
  {
    id: 3, label: 'Round 3 — Value Exchange',
    question: 'You\'re making progress, but the supplier is asking for faster payment terms — from 60 days to 15 days — to improve their cash flow. What do you offer?',
    context: 'Payment terms are a hidden lever most negotiators ignore. Paying faster improves their cash flow (which they value enormously) in exchange for a price concession or improved lead time — a win-win structure.',
    choices: [
      { text: 'Offer 30-day terms (middle ground) in exchange for a 5% price reduction and priority production slot.', trust: +10, price: +8, lead: +6, label: 'A' },
      { text: 'Accept 15-day terms with no conditions — you want the goodwill.', trust: +6, price: -3, lead: +1, label: 'B' },
      { text: 'Refuse any change to payment terms — 60 days is standard.', trust: -8, price: +0, lead: -3, label: 'C' },
      { text: 'Offer supply chain financing (bank pays supplier immediately, you pay bank in 60 days).', trust: +12, price: +4, lead: +5, label: 'D' }
    ]
  },
  {
    id: 4, label: 'Round 4 — Closing Terms',
    question: 'Final round. Both sides are close. The supplier asks for one last concession: a joint business review (JBR) meeting every quarter. How do you close?',
    context: 'Quarterly JBRs seem like overhead but they transform a transactional supplier relationship into a strategic partnership. When the next crisis hits, partners get priority treatment. This is about building resilience, not just closing this deal.',
    choices: [
      { text: 'Agree to quarterly JBRs and propose adding shared KPI dashboards so both teams track performance together.', trust: +15, price: +4, lead: +8, label: 'A' },
      { text: 'Agree to quarterly JBRs with no additional requirements.', trust: +8, price: +2, lead: +2, label: 'B' },
      { text: 'Counter-propose annual reviews only — quarterly is too much overhead.', trust: -5, price: +1, lead: -2, label: 'C' },
      { text: 'Agree to JBRs but insist they are optional with a 48-hour cancellation policy.', trust: -8, price: +0, lead: +0, label: 'D' }
    ]
  }
];

const CEO_QUESTIONS = [
  {
    q: 'Your CFO recommends cutting inventory by 30% to reduce working capital costs. Your Chief Supply Chain Officer warns this leaves you exposed. What do you decide?',
    context: 'This is a classic tension between finance (minimizing working capital) and operations (maintaining resilience). "Lean" is efficient but fragile. Post-pandemic, most companies learned this the hard way.',
    options: [
      { text: 'Cut inventory by 15% — a balanced compromise that satisfies both sides.', correct: false, feedback: 'Compromise sounds smart, but 15% may still leave you exposed without a clear risk analysis. Better to define the right level by product category.' },
      { text: 'Conduct an SKU-level risk analysis. Reduce inventory on low-risk items, maintain safety stock on critical components.', correct: true, feedback: 'Excellent. This is data-driven differentiation. Not all inventory is equal — some SKUs are replaceable in days, others take months. Treat them differently.' },
      { text: 'Follow the CFO\'s advice. Finance drives strategic direction.', correct: false, feedback: 'Deferring entirely to finance without cross-functional input is how supply chain crises happen. The supply chain team\'s expertise must be in the room.' },
      { text: 'Reject any inventory reduction — resilience must come first.', correct: false, feedback: 'Blanket rejection without analysis is also wrong. Over-stocking ties up cash and creates its own risks (obsolescence, storage costs). Analysis first.' }
    ]
  },
  {
    q: 'Your biggest customer (30% of revenue) is demanding you absorb a supplier price increase rather than pass it through. They threaten to switch suppliers. How do you respond?',
    context: 'Customer concentration risk is a structural vulnerability. When one customer accounts for 30%+ of revenue, they have disproportionate negotiating leverage. How you respond signals your pricing strategy for years.',
    options: [
      { text: 'Absorb the full increase to protect the relationship and revenue.', correct: false, feedback: 'This sets a dangerous precedent. You train customers to expect you to absorb all increases, which erodes your margins permanently.' },
      { text: 'Pass through 100% of the increase — the customer must understand supplier economics.', correct: false, feedback: 'A hard stance risks losing 30% of revenue overnight. Even if you\'re right on principle, the timing is wrong during a crisis.' },
      { text: 'Propose a transparent cost-sharing model: you absorb 50%, they absorb 50%, with a sunset clause for 12 months.', correct: true, feedback: 'Smart. Transparency builds trust. A time-bound split is fair, defensible, and preserves the relationship while protecting your margin.' },
      { text: 'Delay the conversation until after the crisis resolves.', correct: false, feedback: 'Delay creates uncertainty on both sides. Customers need answers during a crisis, not silence. Delaying often leads to them finding alternatives.' }
    ]
  },
  {
    q: 'Your team wants to implement a new supply chain AI system immediately to help manage the crisis. The vendor says it will take 90 days to fully implement. What do you approve?',
    context: 'Technology adoption during a crisis is high-risk. A 90-day implementation timeline means you won\'t see benefits until after the crisis peaks. But rushing also leads to failed deployments that make things worse.',
    options: [
      { text: 'Approve the full implementation — you need the full system to tackle the crisis.', correct: false, feedback: 'Implementing a full system mid-crisis is like changing an engine while the car is moving. You risk destabilizing existing operations.' },
      { text: 'Reject the new system — no technology changes during a crisis.', correct: false, feedback: 'Too rigid. Some tools can be deployed quickly and add real value even during a crisis. The answer is selective deployment.' },
      { text: 'Approve a rapid MVP deployment of the two most critical modules (inventory visibility and supplier risk) within 2 weeks.', correct: true, feedback: 'Correct approach. Rapid capability deployment for immediate pain points, without the full 90-day risk. Phased rollouts in crisis situations are best practice.' },
      { text: 'Tell the vendor to start, but stop if things get worse.', correct: false, feedback: 'Vague approval criteria creates confusion and poor vendor management. Be specific about scope, timeline, and success metrics from the start.' }
    ]
  },
  {
    q: 'The media has gotten wind of your supply chain crisis and a journalist is calling for a statement. Your PR team says: "Say nothing." Your COO says: "Be transparent." What do you do?',
    context: 'Crisis communication is one of the most consequential decisions an executive makes. The 2010 BP oil spill and 2021 Facebook outage are textbook examples of communication failures. Transparency, when genuine, builds long-term trust.',
    options: [
      { text: 'Issue a brief, honest statement: what happened, what you\'re doing, and when you\'ll update stakeholders again.', correct: true, feedback: 'This is the right call. Proactive, honest communication prevents rumor escalation, demonstrates control, and builds investor/customer confidence.' },
      { text: 'Say nothing until the crisis is resolved. "No comment" is safest.', correct: false, feedback: 'Silence creates a vacuum that gets filled by speculation. "No comment" in 2024 is read as: "we have something to hide."' },
      { text: 'Issue an optimistic statement downplaying the severity to prevent panic.', correct: false, feedback: 'If the reality is later revealed to be worse than your statement suggested, trust collapses permanently. Dishonesty in a crisis is worse than the crisis itself.' },
      { text: 'Let your PR team handle it — this is not a CEO-level concern.', correct: false, feedback: 'Supply chain crises that affect revenue, customers, and investors absolutely require C-suite visibility. Delegating entirely signals leadership absence.' }
    ]
  },
  {
    q: 'Post-crisis, your board wants a "never again" plan. You have budget for exactly one strategic investment. Which do you choose?',
    context: 'Strategic resilience investments require trade-offs. There is no unlimited budget. This question tests your understanding of root cause vs. symptom. The best investment addresses the systemic vulnerability exposed by the crisis, not just the symptom.',
    options: [
      { text: 'Build a second backup production facility in a different country.', correct: false, feedback: 'Expensive and slow to build. A second facility addresses single-point failure risk but takes 2-3 years and significant capital. Not always the best first move.' },
      { text: 'Create a supply chain risk intelligence platform that monitors all supplier financial health, geopolitical risk, and logistics disruptions in real time.', correct: true, feedback: 'Excellent choice. Early warning systems are the force multiplier — they let you prevent future crises rather than just respond to them. Higher ROI than physical redundancy.' },
      { text: 'Hire 20 additional procurement managers.', correct: false, feedback: 'Headcount without technology and process change has diminishing returns. The problem was information gaps and structural fragility, not headcount.' },
      { text: 'Increase safety stock for all products by 60%.', correct: false, feedback: 'Blanket inventory increases are blunt and expensive. The issue was systemic fragility — better risk monitoring addresses the root cause across all scenarios.' }
    ]
  }
];

const AI_INVESTMENTS = [
  {
    id: 'forecasting', icon: '📈', name: 'Demand Forecasting AI',
    desc: 'Uses historical sales, market signals, social data, and weather patterns to predict demand 90 days ahead with 94% accuracy. Replaces spreadsheet-based guesswork.',
    impact: ['Reduces excess inventory by 28%', 'Cuts stockouts by 42%', 'Saves $3-8M annually in holding costs'],
    roi: ['28% less excess inventory', '42% fewer stockouts', '94% forecast accuracy']
  },
  {
    id: 'inventory', icon: '📦', name: 'Inventory Optimization Engine',
    desc: 'Dynamically calculates optimal safety stock levels for each SKU based on demand variability, supplier lead times, and service level targets.',
    impact: ['Reduces working capital by 22%', 'Improves service levels by 15%', 'Frees up warehouse space'],
    roi: ['22% working capital freed', '+15% service levels', 'Real-time reorder alerts']
  },
  {
    id: 'supplier_risk', icon: '🛡️', name: 'Supplier Risk Monitor',
    desc: 'Continuously monitors 500+ risk signals per supplier — financial filings, news sentiment, geopolitical events, weather — and alerts you 30 days before a crisis hits.',
    impact: ['Detects supplier failures 30 days early', 'Prevents 70% of supply disruptions', 'Ranks all suppliers by risk score'],
    roi: ['30-day early warning', '70% disruption prevention', 'Risk-ranked supplier list']
  },
  {
    id: 'vision', icon: '👁️', name: 'Warehouse Vision AI',
    desc: 'Computer vision cameras + AI track every item in your warehouse in real time — no barcode scanning needed. Detects misplacements, damage, and theft automatically.',
    impact: ['Eliminates manual inventory counting', 'Reduces pick errors by 91%', 'Cuts shrinkage by 35%'],
    roi: ['91% fewer pick errors', '35% less shrinkage', 'Zero manual counting']
  },
  {
    id: 'procurement', icon: '🤖', name: 'Procurement Copilot',
    desc: 'AI assistant that negotiates with suppliers, generates RFQs, analyzes contracts for risk clauses, and recommends the optimal supplier mix based on cost, quality, and risk.',
    impact: ['Reduces procurement cycle from 45 to 7 days', 'Identifies 12% cost savings on average', 'Flags 93% of risky contract terms'],
    roi: ['7-day procurement cycles', '12% average cost savings', '93% contract risk coverage']
  }
];

// ──────────────────────────────────────────────────────────────
// UTILITIES
// ──────────────────────────────────────────────────────────────

function rand(arr) { return arr[Math.floor(Math.random() * arr.length)]; }
function randInt(min, max) { return Math.floor(Math.random() * (max - min + 1)) + min; }
function clamp(val, min, max) { return Math.max(min, Math.min(max, val)); }

function generateCompany() {
  const industry = rand(INDUSTRIES);
  const name = rand(COMPANY_PREFIXES) + ' ' + rand(COMPANY_SUFFIXES);
  const ticker = name.split(' ').map(w => w[0]).join('').substring(0, 4).toUpperCase();
  const revenue = randInt(120, 980);
  const factories = randInt(2, 8);
  const warehouses = randInt(4, 16);
  const suppliers = randInt(80, 450);
  const inventoryDays = randInt(18, 65);
  const leadTime = randInt(14, 58);
  const countries = randInt(6, 28);
  const employees = randInt(800, 12000);
  const margin = randInt(8, 24);
  const supplyChainCountries = COUNTRIES.slice().sort(() => Math.random() - 0.5).slice(0, 4);
  return { name, ticker, industry, revenue, factories, warehouses, suppliers, inventoryDays, leadTime, countries, employees, margin, supplyChainCountries };
}

function generateCrisis() {
  return rand(CRISES);
}

function generateMetrics() {
  return {
    cost: randInt(55, 80),
    inventory: randInt(45, 75),
    profit: randInt(50, 75),
    deliverySpeed: randInt(50, 80),
    satisfaction: randInt(55, 80)
  };
}

// ──────────────────────────────────────────────────────────────
// PROGRESS BAR
// ──────────────────────────────────────────────────────────────

function ProgressBar({ label, value, prev, color, tooltip }) {
  const delta = value - (prev || value);
  const w = clamp(value, 0, 100);
  return (
    <div className="metric-bar-wrap">
      <div className="metric-bar-header">
        <div className="metric-bar-label">
          {label}
          {tooltip && (
            <div className="tooltip-wrap">
              <div className="tooltip-icon">?</div>
              <div className="tooltip-box">{tooltip}</div>
            </div>
          )}
        </div>
        <div className="metric-bar-value" style={{ display: 'flex', alignItems: 'center', gap: 6 }}>
          {value}%
          {prev !== undefined && delta !== 0 && (
            <span className={`delta ${delta > 0 ? 'delta-pos' : 'delta-neg'}`}>
              {delta > 0 ? '+' : ''}{delta}
            </span>
          )}
        </div>
      </div>
      <div className="metric-bar-track">
        <div className={`metric-bar-fill ${color}`} style={{ width: `${w}%` }} />
      </div>
    </div>
  );
}

// ──────────────────────────────────────────────────────────────
// STEPPER
// ──────────────────────────────────────────────────────────────

const STEPS = ['Company', 'Crisis', 'War Room', 'Negotiation', 'CEO', 'AI Strategy', 'Results'];

function Stepper({ current }) {
  return (
    <div className="stepper">
      {STEPS.map((s, i) => {
        const idx = i + 1;
        const active = idx === current;
        const done = idx < current;
        return (
          <React.Fragment key={s}>
            <div className={`step ${active ? 'active' : ''} ${done ? 'done' : ''}`}>
              <div className="step-num">{done ? '✓' : idx}</div>
              {s}
            </div>
            {i < STEPS.length - 1 && <div className="step-connector" />}
          </React.Fragment>
        );
      })}
    </div>
  );
}

// ──────────────────────────────────────────────────────────────
// SCREENS
// ──────────────────────────────────────────────────────────────

function Welcome({ onStart }) {
  return (
    <div className="welcome-hero">
      <div className="welcome-badge">
        <div className="dot" /> Supply Chain Simulation
      </div>
      <h1 className="welcome-title">Operation Lifeline</h1>
      <p style={{ fontFamily: 'var(--font-display)', fontSize: 'clamp(16px,3vw,22px)', color: 'var(--text2)', marginBottom: 12, fontWeight: 500 }}>
        Supply Chain Crisis Lab
      </p>
      <p className="welcome-subtitle">
        Step into the role of Chief Supply Chain Officer. Navigate a real business crisis, negotiate with suppliers, make leadership decisions, and invest in AI — then see how your choices score.
      </p>
      <div className="welcome-meta">
        {[['⏱', '25–35 min'], ['🎓', 'Beginner Friendly'], ['🎲', 'Randomized Every Play'], ['📊', 'Real Frameworks']].map(([icon, text]) => (
          <div key={text} className="welcome-meta-item">
            <span className="icon">{icon}</span> {text}
          </div>
        ))}
      </div>
      <button className="btn btn-primary btn-lg animate-in" onClick={onStart}>
        Start Simulation →
      </button>
      <p style={{ color: 'var(--text3)', fontSize: 13, marginTop: 20 }}>No login required. Runs entirely in your browser.</p>
    </div>
  );
}

// ──────────────────────────────────────────────────────────────
function CompanyScreen({ company, crisis, onNext }) {
  return (
    <div className="screen">
      <div className="container animate-in">
        <Stepper current={1} />
        <div className="section-header">
          <div className="section-eyebrow">Step 1 of 7</div>
          <h2 className="section-title">Your Company Profile</h2>
          <p className="section-desc">
            You've just been appointed CSCO (Chief Supply Chain Officer) of this company. Study your operation before the crisis hits — understanding your scale determines your options.
          </p>
        </div>

        <div className="company-header">
          <div style={{ display: 'flex', alignItems: 'flex-start', gap: 16 }}>
            <div className="company-logo">{company.ticker}</div>
            <div>
              <div className="company-name">{company.name}</div>
              <div className="company-industry">{company.industry.icon} {company.industry.name}</div>
              <div className="stat-row" style={{ marginTop: 10, marginBottom: 0 }}>
                {company.supplyChainCountries.map(c => <span key={c} className="tag tag-blue">{c}</span>)}
              </div>
            </div>
          </div>
          <div style={{ textAlign: 'right' }}>
            <div className="company-revenue-label">Annual Revenue</div>
            <div className="company-revenue">${company.revenue}M</div>
            <div style={{ fontSize: 13, color: 'var(--text3)', marginTop: 4 }}>Net Margin: {company.margin}%</div>
          </div>
        </div>

        <div className="card-grid animate-in delay-1">
          {[
            { label: 'Production Factories', value: company.factories, sub: 'Across ' + company.countries + ' countries', icon: '🏭' },
            { label: 'Warehouses', value: company.warehouses, sub: 'Regional & local DCs', icon: '🏬' },
            { label: 'Active Suppliers', value: company.suppliers, sub: 'Tier 1, 2 & 3', icon: '🔗' },
            { label: 'Inventory Days', value: company.inventoryDays + 'd', sub: 'Days of stock on hand', icon: '📦' },
            { label: 'Avg Lead Time', value: company.leadTime + 'd', sub: 'From PO to delivery', icon: '⏱' },
            { label: 'Employees', value: company.employees.toLocaleString(), sub: 'Supply chain team', icon: '👥' }
          ].map(m => (
            <div key={m.label} className="metric-card animate-fade">
              <div style={{ fontSize: 24, marginBottom: 8 }}>{m.icon}</div>
              <div className="metric-value">{m.value}</div>
              <div className="metric-label">{m.label}</div>
              <div className="metric-sub">{m.sub}</div>
            </div>
          ))}
        </div>

        <div className="info-box animate-in delay-3" style={{ marginTop: 20 }}>
          <strong>📋 What this means for you:</strong> With {company.inventoryDays} days of inventory and a {company.leadTime}-day lead time, you have{' '}
          {company.inventoryDays > company.leadTime ? 'a comfortable buffer' : 'very limited buffer'} before a supply disruption becomes a production shutdown.
          Your {company.suppliers} suppliers create {company.suppliers > 200 ? 'good diversity but high management complexity' : 'some concentration risk worth addressing'}.
        </div>

        <div style={{ display: 'flex', justifyContent: 'flex-end', marginTop: 28 }}>
          <button className="btn btn-primary" onClick={onNext}>View Crisis Alert →</button>
        </div>
      </div>
    </div>
  );
}

// ──────────────────────────────────────────────────────────────
function CrisisScreen({ company, crisis, onNext }) {
  const urgencyClass = crisis.urgency === 'critical' ? 'urgency-critical' : crisis.urgency === 'high' ? 'urgency-high' : 'urgency-medium';
  return (
    <div className="screen">
      <div className="container animate-in">
        <Stepper current={2} />
        <div className="section-header">
          <div className="section-eyebrow">Step 2 of 7</div>
          <h2 className="section-title">🚨 Crisis Alert</h2>
          <p className="section-desc">A major disruption has hit your supply chain. Read carefully — the details matter for the decisions ahead.</p>
        </div>

        <div className="crisis-card animate-in">
          <div style={{ display: 'flex', alignItems: 'flex-start', justifyContent: 'space-between', flexWrap: 'wrap', gap: 12, marginBottom: 12 }}>
            <div className="crisis-icon">{crisis.icon}</div>
            <span className={`crisis-badge ${urgencyClass}`}>
              🔴 {crisis.urgency.toUpperCase()} URGENCY
            </span>
          </div>
          <div className="crisis-name">{crisis.name}</div>
          <div className="crisis-desc">{crisis.desc}</div>
          <div className="impact-grid">
            {Object.entries(crisis.impacts).map(([k, v]) => (
              <div key={k} className="impact-item">
                <div className="impact-label">{k.replace(/([A-Z])/g, ' $1').trim()}</div>
                <div className="impact-value">{v}</div>
              </div>
            ))}
          </div>
        </div>

        <div className="card animate-in delay-1" style={{ marginBottom: 20 }}>
          <div className="feedback-title" style={{ color: 'var(--accent3)' }}>💡 Why This Matters</div>
          <p className="feedback-text">{crisis.context}</p>
        </div>

        <div className="info-box animate-in delay-2">
          <strong>🎯 Your mission:</strong> As CSCO of {company.name}, you have 72 hours to respond. Every decision you make in the next six stages will be scored on cost efficiency, resilience, leadership quality, and customer impact.
        </div>

        <div style={{ display: 'flex', justifyContent: 'flex-end', marginTop: 28 }}>
          <button className="btn btn-primary" onClick={onNext}>Enter War Room →</button>
        </div>
      </div>
    </div>
  );
}

// ──────────────────────────────────────────────────────────────
function WarRoom({ metrics: baseMetrics, onNext }) {
  const [selected, setSelected] = useState([]);
  const [applied, setApplied] = useState(false);
  const [currentMetrics, setCurrentMetrics] = useState(baseMetrics);
  const [notify, setNotify] = useState('');

  const toggleAction = (id) => {
    if (applied) return;
    setSelected(prev => {
      if (prev.includes(id)) return prev.filter(x => x !== id);
      if (prev.length >= 3) {
        setNotify('You can only select 3 actions. Deselect one first.');
        setTimeout(() => setNotify(''), 3000);
        return prev;
      }
      return [...prev, id];
    });
  };

  const applyActions = () => {
    if (selected.length < 3) {
      setNotify('Please select exactly 3 response actions.');
      setTimeout(() => setNotify(''), 3000);
      return;
    }
    const selectedActions = ACTIONS.filter(a => selected.includes(a.id));
    const newMetrics = { ...baseMetrics };
    selectedActions.forEach(a => {
      Object.entries(a.effects).forEach(([k, v]) => {
        newMetrics[k] = clamp((newMetrics[k] || 50) + v, 0, 100);
      });
    });
    setCurrentMetrics(newMetrics);
    setApplied(true);
  };

  const metricConfig = [
    { key: 'cost', label: 'Cost Control', color: 'bar-orange', tooltip: 'Lower cost means higher this score. Actions that spend money reduce this.' },
    { key: 'inventory', label: 'Inventory Level', color: 'bar-blue', tooltip: 'Your ability to keep products in stock and ready to ship.' },
    { key: 'profit', label: 'Profit Margin', color: 'bar-green', tooltip: 'Your margin after crisis expenses. Some actions cost short-term for long-term gain.' },
    { key: 'deliverySpeed', label: 'Delivery Speed', color: 'bar-gold', tooltip: 'How quickly you can get products to customers during the crisis.' },
    { key: 'satisfaction', label: 'Customer Satisfaction', color: 'bar-blue', tooltip: 'How happy your customers are with how you\'re handling the situation.' }
  ];

  return (
    <div className="screen">
      <div className="wide-container animate-in">
        <Stepper current={3} />
        <div className="section-header">
          <div className="section-eyebrow">Step 3 of 7</div>
          <h2 className="section-title">⚔️ War Room: Crisis Response</h2>
          <p className="section-desc">
            Choose exactly <strong style={{ color: 'var(--text)' }}>3 response actions</strong> from the six options below. Each action has trade-offs — there is no perfect combination. Think about which metrics matter most given the crisis.
          </p>
        </div>

        <div style={{ display: 'grid', gridTemplateColumns: '1fr 300px', gap: 24, alignItems: 'start' }}>
          <div>
            <div className="info-box">
              <strong>💡 How to think about this:</strong> Each action has positive and negative effects. Consider which metrics are most at risk given your crisis, and prioritize actions that protect those — even at cost to others.
            </div>
            <div className="card-grid-2">
              {ACTIONS.map(a => (
                <div
                  key={a.id}
                  className={`action-card ${selected.includes(a.id) ? 'selected' : ''}`}
                  onClick={() => toggleAction(a.id)}
                >
                  <div className="action-icon">{a.icon}</div>
                  <div className="action-name">{a.name}</div>
                  <div className="action-desc">{a.desc}</div>
                  <div className="action-why">{a.why}</div>
                  <div className="action-effects">
                    {a.tags.map(t => (
                      <span key={t} className={`effect-tag ${t.startsWith('+') ? 'pos' : t.startsWith('-') ? 'neg' : ''}`}>{t}</span>
                    ))}
                  </div>
                </div>
              ))}
            </div>
          </div>

          <div style={{ position: 'sticky', top: 20 }}>
            <div className="card card-glow" style={{ marginBottom: 16 }}>
              <div style={{ fontSize: 13, fontWeight: 700, color: 'var(--text3)', textTransform: 'uppercase', letterSpacing: '.06em', marginBottom: 16 }}>
                Business Metrics
              </div>
              {metricConfig.map(m => (
                <ProgressBar
                  key={m.key}
                  label={m.label}
                  value={currentMetrics[m.key]}
                  prev={applied ? baseMetrics[m.key] : undefined}
                  color={m.color}
                  tooltip={m.tooltip}
                />
              ))}
            </div>
            <div className="selection-counter" style={{ position: 'static', marginTop: 0 }}>
              <div>
                <div style={{ fontSize: 13, color: 'var(--text2)' }}>Actions Selected</div>
                <div style={{ fontFamily: 'var(--font-display)', fontSize: 22, fontWeight: 700, color: selected.length === 3 ? 'var(--success)' : 'var(--text)' }}>
                  {selected.length} / 3
                </div>
              </div>
              {!applied ? (
                <button
                  className="btn btn-primary btn-sm"
                  onClick={applyActions}
                  disabled={selected.length < 3}
                >
                  Apply →
                </button>
              ) : (
                <button className="btn btn-primary btn-sm" onClick={() => onNext(selected, currentMetrics)}>
                  Continue →
                </button>
              )}
            </div>
          </div>
        </div>
      </div>
      {notify && <div className="notify">⚠️ {notify}</div>}
    </div>
  );
}

// ──────────────────────────────────────────────────────────────
function Negotiation({ onNext }) {
  const [round, setRound] = useState(0);
  const [trust, setTrust] = useState(50);
  const [price, setPrice] = useState(50);
  const [leadScore, setLeadScore] = useState(50);
  const [choices, setChoices] = useState([]);
  const [chosen, setChosen] = useState(null);
  const [showFeedback, setShowFeedback] = useState(false);

  const currentRound = NEG_ROUNDS[round];

  const handleChoice = (c, idx) => {
    if (chosen !== null) return;
    setChosen(idx);
    setTrust(t => clamp(t + c.trust, 0, 100));
    setPrice(p => clamp(p + c.price, 0, 100));
    setLeadScore(l => clamp(l + c.lead, 0, 100));
    setChoices(prev => [...prev, { round: round + 1, choice: c }]);
    setShowFeedback(true);
  };

  const nextRound = () => {
    if (round < NEG_ROUNDS.length - 1) {
      setRound(r => r + 1);
      setChosen(null);
      setShowFeedback(false);
    } else {
      const score = Math.round((trust * 0.4 + price * 0.35 + leadScore * 0.25));
      onNext(score, trust, price, leadScore);
    }
  };

  const feedbackMessages = {
    0: ['📊 Sharp move — data wins arguments, especially in Round 1.', '🤝 Accepting immediately leaves value on the table.', '❌ Walking out early destroys trust permanently.', '⏳ Delay signals indecision and frustrates suppliers.'],
    1: ['🎯 Preferred partnership + KPIs is the gold standard.', '⚠️ Exclusivity is risky long-term.', '❌ Month-to-month signals distrust and gets low priority.', '⚖️ Arbitration is fair but doesn\'t advance the deal.'],
    2: ['✅ Classic value exchange — you both win.', '⚠️ Unconditional concession trains them to ask again.', '❌ Rigidity on standard terms is seen as bad faith.', '🌟 Supply chain financing is sophisticated — shows maturity.'],
    3: ['🏆 Shared dashboards = true partnership. Best outcome.', '✔️ Agreed without bonus — good but could be better.', '⚠️ Annual meetings signal low commitment.', '❌ Optional JBRs undermine the partnership signal.']
  };

  return (
    <div className="screen">
      <div className="container animate-in">
        <Stepper current={4} />
        <div className="section-header">
          <div className="section-eyebrow">Step 4 of 7</div>
          <h2 className="section-title">🤝 Supplier Negotiation</h2>
          <p className="section-desc">
            You're negotiating with your key supplier to secure better terms during the crisis. Every choice affects trust, pricing, and how fast they prioritize your orders.
          </p>
        </div>

        <div className="negotiation-header animate-in">
          <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 16, flexWrap: 'wrap', gap: 12 }}>
            <div style={{ fontFamily: 'var(--font-display)', fontWeight: 700, color: 'var(--text)' }}>
              Round {round + 1} of 4
            </div>
            <div style={{ display: 'flex', gap: 12 }}>
              {[
                { label: 'Trust', value: trust, color: 'var(--accent3)' },
                { label: 'Price', value: price, color: 'var(--accent)' },
                { label: 'Lead Time', value: leadScore, color: 'var(--accent2)' }
              ].map(s => (
                <div key={s.label} style={{ textAlign: 'center' }}>
                  <div style={{ fontFamily: 'var(--font-display)', fontSize: 20, fontWeight: 700, color: s.color }}>{s.value}</div>
                  <div style={{ fontSize: 11, color: 'var(--text3)', textTransform: 'uppercase', letterSpacing: '.06em' }}>{s.label}</div>
                </div>
              ))}
            </div>
          </div>
          <div style={{ marginBottom: 6, fontSize: 12, color: 'var(--text3)' }}>Trust Level</div>
          <div className="trust-bar">
            <div className="trust-fill" style={{ width: `${trust}%` }} />
          </div>
        </div>

        <div className="round-card animate-in delay-1">
          <div className="round-label">🏷 {currentRound.label}</div>
          <div className="round-question">{currentRound.question}</div>
          <div className="round-context">{currentRound.context}</div>

          {currentRound.choices.map((c, i) => (
            <button
              key={i}
              className={`choice-btn ${chosen === i ? 'chosen' : ''}`}
              onClick={() => handleChoice(c, i)}
              disabled={chosen !== null}
            >
              <span className="choice-key">{c.label}</span>
              <span>{c.text}</span>
            </button>
          ))}

          {showFeedback && chosen !== null && (
            <div className={`q-feedback ${currentRound.choices[chosen].trust > 5 ? 'good' : 'bad'}`} style={{ marginTop: 16 }}>
              {feedbackMessages[round][chosen]}
            </div>
          )}
        </div>

        {showFeedback && (
          <div style={{ display: 'flex', justifyContent: 'flex-end' }}>
            <button className="btn btn-primary" onClick={nextRound}>
              {round < NEG_ROUNDS.length - 1 ? `Round ${round + 2} →` : 'View Score →'}
            </button>
          </div>
        )}
      </div>
    </div>
  );
}

// ──────────────────────────────────────────────────────────────
function CEOBoardroom({ onNext }) {
  const [qIndex, setQIndex] = useState(0);
  const [answers, setAnswers] = useState([]);
  const [chosen, setChosen] = useState(null);
  const [score, setScore] = useState(0);

  const q = CEO_QUESTIONS[qIndex];

  const handleAnswer = (opt, idx) => {
    if (chosen !== null) return;
    setChosen(idx);
    if (opt.correct) setScore(s => s + 20);
    setAnswers(prev => [...prev, { q: qIndex, idx, correct: opt.correct }]);
  };

  const next = () => {
    if (qIndex < CEO_QUESTIONS.length - 1) {
      setQIndex(i => i + 1);
      setChosen(null);
    } else {
      onNext(score + (CEO_QUESTIONS[qIndex].options[chosen]?.correct ? 0 : 0));
    }
  };

  return (
    <div className="screen">
      <div className="container animate-in">
        <Stepper current={5} />
        <div className="section-header">
          <div className="section-eyebrow">Step 5 of 7</div>
          <h2 className="section-title">🏛 CEO Boardroom</h2>
          <p className="section-desc">
            The board is watching. Answer 5 executive-level decision questions. There is one best answer for each — and understanding why matters as much as the score.
          </p>
        </div>

        <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 20 }}>
          <div style={{ display: 'flex', gap: 6 }}>
            {CEO_QUESTIONS.map((_, i) => (
              <div key={i} style={{
                width: 28, height: 6, borderRadius: 3,
                background: i < qIndex ? 'var(--accent3)' : i === qIndex ? 'var(--accent)' : 'rgba(255,255,255,0.08)'
              }} />
            ))}
          </div>
          <div style={{ fontSize: 13, color: 'var(--text3)' }}>
            Score: <span style={{ color: 'var(--accent5)', fontWeight: 700 }}>{score}/100</span>
          </div>
        </div>

        <div className="question-card animate-in">
          <div className="q-number">Question {qIndex + 1} of {CEO_QUESTIONS.length}</div>
          <div className="q-text">{q.q}</div>
          <div className="q-context">{q.context}</div>
          <div className="q-options">
            {q.options.map((opt, i) => {
              let cls = '';
              if (chosen !== null) {
                if (opt.correct) cls = 'correct';
                else if (chosen === i) cls = 'wrong';
              }
              return (
                <button
                  key={i}
                  className={`q-opt ${cls}`}
                  onClick={() => handleAnswer(opt, i)}
                  disabled={chosen !== null}
                >
                  <span style={{
                    minWidth: 28, height: 28, borderRadius: 8, background: 'rgba(255,255,255,0.07)',
                    display: 'grid', placeItems: 'center', fontSize: 12, fontWeight: 700, color: 'var(--text3)', flexShrink: 0
                  }}>
                    {String.fromCharCode(65 + i)}
                  </span>
                  {opt.text}
                </button>
              );
            })}
          </div>
          {chosen !== null && (
            <div className={`q-feedback ${q.options[chosen].correct ? 'good' : 'bad'}`}>
              {q.options[chosen].correct ? '✅' : '❌'} {q.options[chosen].feedback}
            </div>
          )}
        </div>

        {chosen !== null && (
          <div style={{ display: 'flex', justifyContent: 'flex-end', marginTop: 8 }}>
            <button className="btn btn-primary" onClick={next}>
              {qIndex < CEO_QUESTIONS.length - 1 ? 'Next Question →' : 'AI Strategy →'}
            </button>
          </div>
        )}
      </div>
    </div>
  );
}

// ──────────────────────────────────────────────────────────────
function AIStrategy({ onNext }) {
  const [selected, setSelected] = useState([]);
  const [notify, setNotify] = useState('');

  const toggle = (id) => {
    setSelected(prev => {
      if (prev.includes(id)) return prev.filter(x => x !== id);
      if (prev.length >= 2) {
        setNotify('Select exactly 2 AI investments.');
        setTimeout(() => setNotify(''), 3000);
        return prev;
      }
      return [...prev, id];
    });
  };

  return (
    <div className="screen">
      <div className="container animate-in">
        <Stepper current={6} />
        <div className="section-header">
          <div className="section-eyebrow">Step 6 of 7</div>
          <h2 className="section-title">🤖 AI Strategy Investment</h2>
          <p className="section-desc">
            Post-crisis, you have budget for <strong style={{ color: 'var(--text)' }}>2 AI investments</strong> to make your supply chain more resilient. Each targets a different vulnerability. Choose wisely.
          </p>
        </div>

        <div className="info-box">
          <strong>💡 What is AI doing in supply chains?</strong> Modern supply chains generate millions of data points daily. AI tools process this data to predict demand, flag risks, and automate decisions — things no human team can do manually at scale.
        </div>

        <div className="card-grid">
          {AI_INVESTMENTS.map(ai => (
            <div
              key={ai.id}
              className={`ai-card ${selected.includes(ai.id) ? 'selected' : ''}`}
              onClick={() => toggle(ai.id)}
            >
              <div className="ai-icon">{ai.icon}</div>
              <div className="ai-name">{ai.name}</div>
              <div className="ai-desc">{ai.desc}</div>
              <div className="ai-roi">
                {ai.roi.map(r => <span key={r} className="roi-tag">{r}</span>)}
              </div>
            </div>
          ))}
        </div>

        <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginTop: 28 }}>
          <div style={{ color: 'var(--text2)', fontSize: 14 }}>
            Selected: <span style={{ color: selected.length === 2 ? 'var(--success)' : 'var(--text)', fontWeight: 700 }}>{selected.length}/2</span>
          </div>
          <button
            className="btn btn-primary"
            disabled={selected.length < 2}
            onClick={() => onNext(selected)}
          >
            View Final Results →
          </button>
        </div>
      </div>
      {notify && <div className="notify">⚠️ {notify}</div>}
    </div>
  );
}

// ──────────────────────────────────────────────────────────────
function FinalDashboard({ data, onReplay }) {
  const { company, crisis, selectedActions, finalMetrics, negScore, ceoScore, aiChoices } = data;

  const selectedActionObjects = ACTIONS.filter(a => selectedActions.includes(a.id));
  const aiObjects = AI_INVESTMENTS.filter(a => aiChoices.includes(a.id));

  const resilience = clamp(Math.round((finalMetrics.inventory + finalMetrics.deliverySpeed) / 2), 0, 100);
  const costControl = clamp(finalMetrics.cost, 0, 100);
  const riskMgmt = clamp(Math.round(negScore * 0.6 + ceoScore * 0.4), 0, 100);
  const custSat = clamp(finalMetrics.satisfaction, 0, 100);
  const leadership = clamp(ceoScore, 0, 100);
  const negotiation = clamp(negScore, 0, 100);

  const overall = clamp(Math.round(
    resilience * 0.2 + costControl * 0.15 + riskMgmt * 0.2 + custSat * 0.2 + leadership * 0.15 + negotiation * 0.1
  ), 0, 100);

  const getGrade = (s) => {
    if (s >= 85) return { grade: 'A+', color: '#00d4aa', label: 'World-Class CSCO' };
    if (s >= 75) return { grade: 'A', color: '#2ed573', label: 'Excellent Executive' };
    if (s >= 65) return { grade: 'B', color: '#ffd700', label: 'Solid Performer' };
    if (s >= 50) return { grade: 'C', color: '#ffa502', label: 'Average Response' };
    return { grade: 'D', color: '#ff4757', label: 'Needs Improvement' };
  };

  const gradeInfo = getGrade(overall);
  const lowestMetric = [
    { name: 'Resilience', v: resilience }, { name: 'Cost Control', v: costControl },
    { name: 'Risk Management', v: riskMgmt }, { name: 'Customer Satisfaction', v: custSat },
    { name: 'Leadership', v: leadership }, { name: 'Negotiation', v: negotiation }
  ].sort((a, b) => a.v - b.v)[0];

  const highestMetric = [
    { name: 'Resilience', v: resilience }, { name: 'Cost Control', v: costControl },
    { name: 'Risk Management', v: riskMgmt }, { name: 'Customer Satisfaction', v: custSat },
    { name: 'Leadership', v: leadership }, { name: 'Negotiation', v: negotiation }
  ].sort((a, b) => b.v - a.v)[0];

  const degrees = (overall / 100) * 360;

  const feedbackMap = {
    'A+': "Exceptional. You navigated this crisis the way seasoned supply chain executives do — balancing short-term stabilization with long-term resilience building. Your decisions under pressure would make any board confident.",
    'A': "Strong performance. You made mostly smart calls and showed real supply chain instinct. A few more data-driven decisions and you'd be in world-class territory.",
    'B': "Solid effort. You handled the crisis without catastrophe and showed good commercial instincts. Focus on improving your weakest areas — they'll be the first to crack in the next disruption.",
    'C': "You survived, but only just. Your company likely took significant revenue damage and lost customer confidence. The good news: you now know exactly what to work on.",
    'D': "The crisis exposed significant gaps in supply chain thinking. The key lesson: resilience requires preparation before the crisis, not reaction during it. Study the frameworks and try again."
  };

  const lessons = [
    "Resilient supply chains are built before the crisis, not during it — redundancy, visibility, and diversification are investments, not costs.",
    "Supplier relationships are strategic assets. Companies with high trust scores get priority treatment when capacity is scarce.",
    "Proactive customer communication during disruptions preserves more revenue than any operational fix.",
    "Data-driven inventory decisions (by SKU, by risk level) always outperform blanket policies set by finance or operations alone.",
    "AI tools provide early warning and pattern recognition that human teams simply cannot match at modern supply chain scale."
  ];

  const recommendation = aiObjects[0]
    ? `Given your ${crisis.name} scenario, your investment in ${aiObjects[0].name} is strategically sound — it directly addresses the root vulnerability exposed by this crisis. Consider pairing it with a supplier diversification audit within 90 days.`
    : 'Review your AI investments in context of the crisis root cause for maximum resilience impact.';

  // Animate the conic gradient
  const [angle, setAngle] = useState(0);
  useEffect(() => {
    const t = setTimeout(() => setAngle(degrees), 300);
    return () => clearTimeout(t);
  }, []);

  const conicStyle = {
    '--angle': `${angle}deg`,
    background: `conic-gradient(${gradeInfo.color} 0deg, ${gradeInfo.color} ${angle}deg, rgba(255,255,255,0.05) ${angle}deg)`,
    transition: 'background 1.5s ease'
  };

  return (
    <div className="screen">
      <div className="wide-container animate-in">
        <Stepper current={7} />
        <div className="section-header">
          <div className="section-eyebrow">Final Results</div>
          <h2 className="section-title">📊 Crisis Performance Dashboard</h2>
          <p className="section-desc">Here's how you performed across every dimension of the simulation.</p>
        </div>

        {/* Hero Score */}
        <div className="card card-glow animate-in" style={{ marginBottom: 24, background: 'linear-gradient(135deg, var(--surface2), rgba(61,114,255,0.06))' }}>
          <div style={{ display: 'flex', alignItems: 'center', gap: 32, flexWrap: 'wrap' }}>
            <div className="score-circle" style={conicStyle}>
              <div className="score-circle-inner">
                <div className="score-number" style={{ color: gradeInfo.color }}>{overall}</div>
                <div className="score-label">Overall</div>
              </div>
            </div>
            <div style={{ flex: 1 }}>
              <div style={{ display: 'flex', alignItems: 'center', gap: 16, flexWrap: 'wrap', marginBottom: 12 }}>
                <div className="grade-badge" style={{ color: gradeInfo.color, background: `rgba(${gradeInfo.color === '#00d4aa' ? '0,212,170' : gradeInfo.color === '#2ed573' ? '46,213,115' : gradeInfo.color === '#ffd700' ? '255,215,0' : '255,165,2'},0.12)` }}>
                  {gradeInfo.grade}
                </div>
                <div>
                  <div style={{ fontFamily: 'var(--font-display)', fontSize: 22, fontWeight: 700, color: 'var(--text)' }}>{gradeInfo.label}</div>
                  <div style={{ fontSize: 14, color: 'var(--text3)' }}>{company.name} · {crisis.name}</div>
                </div>
              </div>
              <p style={{ fontSize: 15, color: 'var(--text2)', lineHeight: 1.7 }}>{feedbackMap[gradeInfo.grade]}</p>
            </div>
          </div>
        </div>

        {/* Score Breakdown */}
        <div className="card-grid-2 animate-in delay-1" style={{ marginBottom: 24 }}>
          <div className="card">
            <div style={{ fontSize: 13, fontWeight: 700, color: 'var(--text3)', textTransform: 'uppercase', letterSpacing: '.06em', marginBottom: 20 }}>Score Breakdown</div>
            <ProgressBar label="Leadership" value={leadership} color="bar-blue" tooltip="Based on CEO boardroom answers" />
            <ProgressBar label="Negotiation" value={negotiation} color="bar-gold" tooltip="Based on supplier negotiation rounds" />
            <ProgressBar label="Resilience" value={resilience} color="bar-green" tooltip="Inventory + delivery speed combined" />
            <ProgressBar label="Cost Control" value={costControl} color="bar-orange" tooltip="How well you managed costs during the crisis" />
            <ProgressBar label="Risk Management" value={riskMgmt} color="bar-blue" tooltip="Blend of negotiation and leadership scores" />
            <ProgressBar label="Customer Satisfaction" value={custSat} color="bar-green" tooltip="How happy customers are with your response" />
          </div>
          <div>
            <div className="feedback-card animate-in delay-2">
              <div className="feedback-title" style={{ color: 'var(--danger)' }}>⚠️ Biggest Vulnerability</div>
              <div className="feedback-text">
                Your weakest area was <strong style={{ color: 'var(--text)' }}>{lowestMetric.name}</strong> ({lowestMetric.v}/100).
                This is the area most likely to cause failure in your next supply chain disruption. Prioritize it in your resilience roadmap.
              </div>
            </div>
            <div className="feedback-card animate-in delay-3">
              <div className="feedback-title" style={{ color: 'var(--success)' }}>✅ Best Decision</div>
              <div className="feedback-text">
                You excelled at <strong style={{ color: 'var(--text)' }}>{highestMetric.name}</strong> ({highestMetric.v}/100).
                Your strongest move was selecting <em>{selectedActionObjects[0]?.name || 'your crisis response strategy'}</em> — the ripple effects protected downstream operations.
              </div>
            </div>
            <div className="feedback-card animate-in delay-4">
              <div className="feedback-title" style={{ color: 'var(--accent3)' }}>🤖 Expert Recommendation</div>
              <div className="feedback-text">{recommendation}</div>
            </div>
          </div>
        </div>

        {/* Actions Summary */}
        <div className="card animate-in delay-2" style={{ marginBottom: 16 }}>
          <div className="feedback-title" style={{ color: 'var(--accent)' }}>⚔️ Your War Room Choices</div>
          <div style={{ display: 'flex', gap: 10, flexWrap: 'wrap' }}>
            {selectedActionObjects.map(a => (
              <div key={a.id} className="card" style={{ flex: '1 1 200px', padding: '14px 16px' }}>
                <div style={{ fontSize: 20, marginBottom: 6 }}>{a.icon}</div>
                <div style={{ fontWeight: 600, fontSize: 14, color: 'var(--text)' }}>{a.name}</div>
              </div>
            ))}
          </div>
        </div>

        {/* AI Choices */}
        <div className="card animate-in delay-3" style={{ marginBottom: 24 }}>
          <div className="feedback-title" style={{ color: 'var(--accent3)' }}>🤖 AI Investments Made</div>
          <div style={{ display: 'flex', gap: 10, flexWrap: 'wrap' }}>
            {aiObjects.map(a => (
              <div key={a.id} className="card" style={{ flex: '1 1 280px', padding: '14px 18px' }}>
                <div style={{ display: 'flex', alignItems: 'center', gap: 10, marginBottom: 8 }}>
                  <span style={{ fontSize: 22 }}>{a.icon}</span>
                  <span style={{ fontWeight: 600, color: 'var(--text)' }}>{a.name}</span>
                </div>
                <div className="ai-roi">
                  {a.roi.map(r => <span key={r} className="roi-tag">{r}</span>)}
                </div>
              </div>
            ))}
          </div>
        </div>

        {/* Lessons */}
        <div className="card animate-in delay-4" style={{ marginBottom: 32 }}>
          <div className="feedback-title" style={{ color: 'var(--accent5)' }}>📚 5 Lessons From This Simulation</div>
          {lessons.map((l, i) => (
            <div key={i} className="lesson-item">
              <div className="lesson-num">{i + 1}</div>
              <div className="lesson-text">{l}</div>
            </div>
          ))}
        </div>

        <div style={{ display: 'flex', justifyContent: 'center', gap: 16, flexWrap: 'wrap' }}>
          <button className="btn btn-primary btn-lg" onClick={onReplay}>
            🎲 New Simulation
          </button>
          <button className="btn btn-secondary btn-lg" onClick={() => window.print()}>
            🖨️ Print Results
          </button>
        </div>
      </div>
    </div>
  );
}

// ──────────────────────────────────────────────────────────────
// ROOT APP
// ──────────────────────────────────────────────────────────────

function App() {
  const [screen, setScreen] = useState('welcome');
  const [company, setCompany] = useState(null);
  const [crisis, setCrisis] = useState(null);
  const [baseMetrics, setBaseMetrics] = useState(null);
  const [warRoomData, setWarRoomData] = useState(null);
  const [negData, setNegData] = useState(null);
  const [ceoScore, setCeoScore] = useState(0);
  const [aiChoices, setAiChoices] = useState([]);

  const start = () => {
    const c = generateCompany();
    const cr = generateCrisis();
    const m = generateMetrics();
    setCompany(c);
    setCrisis(cr);
    setBaseMetrics(m);
    setScreen('company');
  };

  const replay = () => {
    setScreen('welcome');
    setCompany(null);
    setCrisis(null);
    setBaseMetrics(null);
    setWarRoomData(null);
    setNegData(null);
    setCeoScore(0);
    setAiChoices([]);
  };

  if (screen === 'welcome') return <Welcome onStart={start} />;
  if (screen === 'company') return <CompanyScreen company={company} crisis={crisis} onNext={() => setScreen('crisis')} />;
  if (screen === 'crisis') return <CrisisScreen company={company} crisis={crisis} onNext={() => setScreen('warroom')} />;
  if (screen === 'warroom') return (
    <WarRoom
      metrics={baseMetrics}
      onNext={(actions, metrics) => {
        setWarRoomData({ actions, metrics });
        setScreen('negotiation');
      }}
    />
  );
  if (screen === 'negotiation') return (
    <Negotiation
      onNext={(score, trust, price, lead) => {
        setNegData({ score, trust, price, lead });
        setScreen('ceo');
      }}
    />
  );
  if (screen === 'ceo') return (
    <CEOBoardroom
      onNext={(s) => {
        setCeoScore(s);
        setScreen('ai');
      }}
    />
  );
  if (screen === 'ai') return (
    <AIStrategy
      onNext={(choices) => {
        setAiChoices(choices);
        setScreen('final');
      }}
    />
  );
  if (screen === 'final') return (
    <FinalDashboard
      data={{
        company,
        crisis,
        selectedActions: warRoomData?.actions || [],
        finalMetrics: warRoomData?.metrics || baseMetrics,
        negScore: negData?.score || 50,
        ceoScore,
        aiChoices
      }}
      onReplay={replay}
    />
  );

  return null;
}

ReactDOM.createRoot(document.getElementById('root')).render(<App />);
</script>
</body>
</html>
