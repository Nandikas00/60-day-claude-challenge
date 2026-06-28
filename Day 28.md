# Today I Built a Hospital Admission Readiness Simulator using claude :

## Key Learnings :

Building this Hospital Admission Readiness Simulator helped me understand how AI can rapidly prototype complex healthcare workflows while exposing the operational dependencies involved in hospital admissions.

1. Hospital admission involves multiple parallel workflows

A patient cannot be admitted simply because a diagnosis exists. Admission readiness depends on several independent processes progressing together, including:

Prior Authorization verification
Insurance validation
Bed assignment
Physician orders
Clinical documentation
Patient consent

This project demonstrated how these workflows collectively determine admission readiness.

2. Readiness can be represented using weighted scoring

Instead of treating admission as a binary outcome, the simulator calculates an overall readiness score by assigning different weights to operational checkpoints.

For example:

PA Status – 25%
Clinical Documentation – 20%
Physician Orders – 20%
Insurance Verification – 15%
Consent – 10%
Bed Assignment – 10%

This helped me understand how healthcare operations often use weighted decision-making rather than simple yes/no logic.

3. Regulatory compliance affects workflow decisions

The simulator introduced healthcare compliance concepts such as:

CMS Observation rules
Prior Authorization requirements
Medical necessity documentation
Medicare observation notifications

I learned that hospital workflows must satisfy regulatory requirements in addition to clinical requirements.

4. Healthcare operations involve multiple coordinated roles

The admission process requires coordination between several departments:

Attending Physician
Nursing Team
Case Manager
Utilization Review Coordinator
Discharge Planner

Each role contributes different information before a patient is considered admission-ready.

5. Workflow visualization improves understanding

Representing the admission lifecycle as:

Readiness indicators
Progress timeline
Status cards
Risk dashboard
Action buttons

made the workflow much easier to understand than reading documentation alone.

6. Risk tracking is an important operational component

The simulator tracks risks across multiple dimensions, including:

Documentation Risk
Insurance Risk
Bed Availability Risk
Clinical Risk

This highlighted how hospitals proactively identify bottlenecks that could delay patient admission.

7. AI can rapidly prototype enterprise healthcare applications

Using Claude, I was able to transform a structured prompt into an interactive simulator featuring:

Multi-step workflow
Readiness assessment
Progress tracking
Operational dashboards
Healthcare-specific UI
Role-based workflow representation

This reinforced how prompt engineering can significantly accelerate the creation of realistic healthcare workflow prototypes.

### Result Screenshots :

<img width="1920" height="1080" alt="Screenshot (441)" src="https://github.com/user-attachments/assets/2e089b04-2f4b-4c47-880f-8343a851c081" />
<img width="1920" height="1080" alt="Screenshot (440)" src="https://github.com/user-attachments/assets/df25270b-c67f-46d7-a6f9-fab2abd946a0" />
<img width="1920" height="1080" alt="Screenshot (439)" src="https://github.com/user-attachments/assets/4ef9ddb0-c180-4387-9e2d-f5d6cf97b26a" />
<img width="1920" height="1080" alt="Screenshot (438)" src="https://github.com/user-attachments/assets/c6776627-eaa1-4b17-a1a4-8b895b70ef53" />
<img width="1920" height="1080" alt="Screenshot (437)" src="https://github.com/user-attachments/assets/43641d1a-5cb0-4ee7-aac4-982f104d5ce7" />

#### Html File :

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Hospital Admission Coordinator — Training Simulation</title>
<script src="https://cdn.tailwindcss.com"></script>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600&family=IBM+Plex+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet"/>
<style>
  :root {
    --navy: #0B1F3A;
    --navy-mid: #132848;
    --navy-light: #1D3A5F;
    --steel: #2C4A6E;
    --teal: #0E7B6C;
    --teal-bright: #10A98F;
    --amber: #D4860F;
    --amber-light: #F0A428;
    --red: #C0392B;
    --red-light: #E74C3C;
    --green: #1A7A4A;
    --green-bright: #27AE60;
    --slate: #8EAABF;
    --slate-light: #B8CEDD;
    --off-white: #EDF1F5;
    --text-dim: #6B8CAE;
  }
  * { box-sizing: border-box; }
  body {
    font-family: 'IBM Plex Sans', sans-serif;
    background: var(--navy);
    color: var(--off-white);
    min-height: 100vh;
  }
  .mono { font-family: 'IBM Plex Mono', monospace; }
  .header-bar {
    background: var(--navy-mid);
    border-bottom: 1px solid var(--steel);
  }
  .badge {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 2px 8px;
    border-radius: 2px;
  }
  .badge-training { background: var(--amber); color: #000; }
  .badge-cms { background: var(--teal); color: #fff; }
  .badge-risk { background: var(--red); color: #fff; }
  
  .panel {
    background: var(--navy-mid);
    border: 1px solid var(--steel);
    border-radius: 6px;
  }
  .panel-header {
    background: var(--navy-light);
    border-bottom: 1px solid var(--steel);
    padding: 10px 16px;
    border-radius: 6px 6px 0 0;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.72rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--slate-light);
  }
  .field-label {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.68rem;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    color: var(--slate);
    margin-bottom: 4px;
  }
  input, select, textarea {
    background: var(--navy);
    border: 1px solid var(--steel);
    color: var(--off-white);
    border-radius: 4px;
    padding: 8px 12px;
    width: 100%;
    font-family: 'IBM Plex Sans', sans-serif;
    font-size: 0.875rem;
    outline: none;
    transition: border-color 0.15s;
  }
  input:focus, select:focus, textarea:focus {
    border-color: var(--teal-bright);
  }
  select option { background: var(--navy-mid); }

  .btn-primary {
    background: var(--teal);
    color: #fff;
    border: none;
    padding: 12px 28px;
    border-radius: 4px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.8rem;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    cursor: pointer;
    transition: background 0.15s, transform 0.1s;
  }
  .btn-primary:hover { background: var(--teal-bright); transform: translateY(-1px); }
  .btn-primary:active { transform: translateY(0); }
  .btn-primary:disabled { background: var(--steel); cursor: not-allowed; transform: none; }

  .btn-action {
    background: transparent;
    border: 1px solid var(--steel);
    color: var(--slate-light);
    padding: 7px 14px;
    border-radius: 4px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.05em;
    cursor: pointer;
    transition: all 0.15s;
  }
  .btn-action:hover { border-color: var(--teal-bright); color: var(--teal-bright); background: rgba(14,123,108,0.08); }
  .btn-action.active { border-color: var(--teal-bright); color: var(--teal-bright); background: rgba(14,123,108,0.15); }
  .btn-action:disabled { opacity: 0.4; cursor: not-allowed; }

  .status-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    display: inline-block;
    margin-right: 6px;
    flex-shrink: 0;
  }
  .dot-green { background: var(--green-bright); box-shadow: 0 0 4px var(--green-bright); }
  .dot-amber { background: var(--amber-light); box-shadow: 0 0 4px var(--amber-light); }
  .dot-red { background: var(--red-light); box-shadow: 0 0 4px var(--red-light); }
  .dot-gray { background: var(--steel); }

  .score-bar-track {
    background: var(--navy);
    border: 1px solid var(--steel);
    border-radius: 3px;
    height: 12px;
    overflow: hidden;
  }
  .score-bar-fill {
    height: 100%;
    border-radius: 2px;
    transition: width 0.8s ease;
  }
  .score-low { background: linear-gradient(90deg, var(--red), var(--amber)); }
  .score-mid { background: linear-gradient(90deg, var(--amber), #e8c043); }
  .score-high { background: linear-gradient(90deg, var(--teal), var(--green-bright)); }

  .timeline-step {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    padding: 8px 0;
    position: relative;
  }
  .timeline-step:not(:last-child)::after {
    content: '';
    position: absolute;
    left: 12px;
    top: 32px;
    bottom: -8px;
    width: 1px;
    background: var(--steel);
  }
  .timeline-node {
    width: 24px; height: 24px;
    border-radius: 50%;
    border: 2px solid var(--steel);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.6rem;
    background: var(--navy);
    margin-top: 2px;
  }
  .timeline-node.done { border-color: var(--teal-bright); background: var(--teal); color: #fff; }
  .timeline-node.active { border-color: var(--amber-light); background: var(--amber); color: #000; }
  .timeline-node.pending { border-color: var(--steel); color: var(--text-dim); }

  .care-card {
    background: var(--navy);
    border: 1px solid var(--steel);
    border-radius: 4px;
    padding: 12px;
  }
  .care-card-role {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.62rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--teal-bright);
    margin-bottom: 4px;
  }

  .risk-pill {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 4px 10px;
    border-radius: 3px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.68rem;
  }
  .risk-low { background: rgba(26,122,74,0.2); border: 1px solid var(--green); color: #7DE8AE; }
  .risk-med { background: rgba(212,134,15,0.2); border: 1px solid var(--amber); color: var(--amber-light); }
  .risk-high { background: rgba(192,57,43,0.2); border: 1px solid var(--red); color: #FF8A7A; }

  .obs-banner {
    background: rgba(14,123,108,0.12);
    border: 1px solid var(--teal);
    border-left: 4px solid var(--teal-bright);
    border-radius: 4px;
    padding: 12px 16px;
  }
  .interqual-banner {
    background: rgba(212,134,15,0.1);
    border: 1px solid var(--amber);
    border-left: 4px solid var(--amber-light);
    border-radius: 4px;
    padding: 12px 16px;
  }
  .moon-banner {
    background: rgba(192,57,43,0.1);
    border: 1px solid var(--red);
    border-left: 4px solid var(--red-light);
    border-radius: 4px;
    padding: 10px 14px;
  }
  .governance-box {
    background: rgba(44,74,110,0.3);
    border: 1px solid var(--steel);
    border-top: 3px solid var(--teal-bright);
    border-radius: 4px;
    padding: 16px;
  }
  .final-admit {
    background: rgba(26,122,74,0.15);
    border: 2px solid var(--green-bright);
    border-radius: 6px;
    padding: 20px;
  }
  .final-reject {
    background: rgba(212,134,15,0.1);
    border: 2px solid var(--amber-light);
    border-radius: 6px;
    padding: 20px;
  }

  .separator {
    border: none;
    border-top: 1px solid var(--steel);
    margin: 16px 0;
  }

  .weight-tag {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.62rem;
    color: var(--text-dim);
    background: var(--navy);
    padding: 1px 6px;
    border-radius: 2px;
    border: 1px solid var(--steel);
  }

  .section-eyebrow {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--teal-bright);
    margin-bottom: 6px;
  }

  .hidden { display: none !important; }
  .fade-in { animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity:0; transform:translateY(8px); } to { opacity:1; transform:translateY(0); } }

  .pa-branch {
    background: var(--navy);
    border: 1px solid var(--steel);
    border-radius: 4px;
    padding: 14px;
  }

  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: var(--navy); }
  ::-webkit-scrollbar-thumb { background: var(--steel); border-radius: 3px; }
</style>
</head>
<body>

<!-- HEADER -->
<div class="header-bar px-6 py-3 flex items-center justify-between sticky top-0 z-50">
  <div class="flex items-center gap-4">
    <span class="mono text-sm font-semibold tracking-widest text-teal-300" style="color:var(--teal-bright)">HAC·SIM</span>
    <span class="text-xs" style="color:var(--slate)">Hospital Admission Coordinator</span>
  </div>
  <div class="flex items-center gap-3">
    <span class="badge badge-training">Illustrative Training Data</span>
    <span class="badge badge-cms">CMS Compliance Module</span>
  </div>
</div>

<!-- MAIN -->
<div class="max-w-5xl mx-auto px-4 py-8">

  <!-- TASK HEADER -->
  <div class="mb-8">
    <div class="section-eyebrow">Active Task</div>
    <h1 class="text-2xl font-semibold tracking-tight" style="letter-spacing:-0.02em">Admission Readiness Assessment</h1>
    <p class="text-sm mt-1" style="color:var(--slate)">Complete the intake form to initiate admission workflow analysis.</p>
  </div>

  <!-- SETUP FORM -->
  <div id="setupPanel" class="panel mb-6">
    <div class="panel-header">01 — Admission Setup</div>
    <div class="p-5 grid grid-cols-1 md:grid-cols-2 gap-5">

      <div>
        <div class="field-label">Provider / Facility</div>
        <select id="provider">
          <option value="">Select provider…</option>
          <option>Northgate General Hospital (Illustrative)</option>
          <option>Riverside Medical Center (Illustrative)</option>
          <option>Summit Health System (Illustrative)</option>
          <option>Lakewood Regional (Illustrative)</option>
        </select>
      </div>

      <div>
        <div class="field-label">Attending Physician</div>
        <select id="physician">
          <option value="">Select physician…</option>
          <option>Dr. Anita Sharma, MD — Internal Medicine (Illustrative)</option>
          <option>Dr. Carlos Reyes, DO — Cardiology (Illustrative)</option>
          <option>Dr. Priya Nair, MD — Pulmonology (Illustrative)</option>
          <option>Dr. James Whitfield, MD — Hospitalist (Illustrative)</option>
          <option>Dr. Leila Hassan, MD — Orthopedics (Illustrative)</option>
        </select>
      </div>

      <div>
        <div class="field-label">Primary Diagnosis</div>
        <select id="diagnosis" onchange="onDiagnosisChange()">
          <option value="">Select diagnosis…</option>
          <option value="ami">Acute MI</option>
          <option value="chf">CHF (Congestive Heart Failure)</option>
          <option value="pneumonia">Pneumonia</option>
          <option value="elective">Elective Surgery</option>
          <option value="hip">Hip Fracture</option>
        </select>
      </div>

      <div>
        <div class="field-label">Admission Type</div>
        <select id="admissionType" onchange="onAdmissionTypeChange()">
          <option value="">Select type…</option>
          <option value="inpatient">Inpatient</option>
          <option value="observation">Observation</option>
          <option value="emergency">Emergency</option>
          <option value="icu">ICU</option>
          <option value="sameday">Same-Day Surgery</option>
        </select>
      </div>

      <div>
        <div class="field-label">PA (Prior Authorization) Status</div>
        <select id="paStatus">
          <option value="">Select PA status…</option>
          <option value="approved">Approved</option>
          <option value="pending">Pending</option>
          <option value="denied">Denied</option>
          <option value="na">Not Required</option>
        </select>
      </div>

      <div>
        <div class="field-label">Admission Date</div>
        <input type="date" id="admissionDate"/>
      </div>

      <!-- Observation Banner -->
      <div id="obsBanner" class="md:col-span-2 obs-banner hidden">
        <div class="flex items-start gap-2">
          <span style="color:var(--teal-bright)">⚠</span>
          <div>
            <div class="mono text-xs font-semibold mb-1" style="color:var(--teal-bright)">Observation Status Notice — CMS 2-Midnight Rule</div>
            <p class="text-xs" style="color:var(--slate-light)">CMS 2-Midnight Rule applies — different cost-sharing, SNF eligibility, and billing than inpatient. Medicare patients require written MOON notification (Medicare Outpatient Observation Notice) under NOTICE Act requirements.</p>
          </div>
        </div>
      </div>

      <!-- InterQual Banner -->
      <div id="interqualBanner" class="md:col-span-2 interqual-banner hidden">
        <div class="flex items-start gap-2">
          <span style="color:var(--amber-light)">📋</span>
          <div>
            <div class="mono text-xs font-semibold mb-1" style="color:var(--amber-light)">Medical Necessity Alert</div>
            <p class="text-xs" style="color:var(--slate-light)">InterQual/Milliman thresholds apply — ensure documentation meets medical necessity standards before UR review. Clinical criteria must be explicitly documented in the record prior to submission.</p>
          </div>
        </div>
      </div>

    </div>
    <div class="px-5 pb-5">
      <button class="btn-primary w-full text-center" onclick="analyzeAdmission()">🏥 Analyze Admission Readiness</button>
    </div>
  </div>

  <!-- ANALYSIS OUTPUT (hidden until submitted) -->
  <div id="analysisOutput" class="hidden fade-in">

    <!-- INITIAL ANALYSIS -->
    <div class="panel mb-6">
      <div class="panel-header">02 — Initial Readiness Analysis</div>
      <div class="p-5">
        <div class="grid grid-cols-2 md:grid-cols-3 gap-3 mb-5" id="statusCards"></div>

        <!-- Score -->
        <div class="mb-4">
          <div class="flex justify-between items-center mb-2">
            <span class="field-label">Readiness Score</span>
            <span class="mono font-semibold text-lg" id="scoreDisplay">—</span>
          </div>
          <div class="score-bar-track">
            <div class="score-bar-fill" id="scoreBar" style="width:0%"></div>
          </div>
          <div class="flex justify-between mt-1">
            <span class="mono text-xs" style="color:var(--text-dim)">0%</span>
            <span class="mono text-xs" style="color:var(--text-dim)">90% threshold</span>
            <span class="mono text-xs" style="color:var(--text-dim)">100%</span>
          </div>
        </div>

        <div class="separator"></div>

        <!-- Score Weights -->
        <div class="mb-4">
          <div class="section-eyebrow">Score Weighting</div>
          <div class="grid grid-cols-2 md:grid-cols-3 gap-2 text-xs mt-2" style="color:var(--slate-light)">
            <div class="flex justify-between items-center"><span>PA Status</span><span class="weight-tag">25%</span></div>
            <div class="flex justify-between items-center"><span>Clinical Documentation</span><span class="weight-tag">20%</span></div>
            <div class="flex justify-between items-center"><span>Physician Orders</span><span class="weight-tag">20%</span></div>
            <div class="flex justify-between items-center"><span>Insurance Verification</span><span class="weight-tag">15%</span></div>
            <div class="flex justify-between items-center"><span>Consent</span><span class="weight-tag">10%</span></div>
            <div class="flex justify-between items-center"><span>Bed Assignment</span><span class="weight-tag">10%</span></div>
          </div>
        </div>

        <!-- PA Branch -->
        <div id="paBranchPanel"></div>
      </div>
    </div>

    <!-- WORKFLOW ACTIONS -->
    <div class="panel mb-6">
      <div class="panel-header">03 — Workflow Actions</div>
      <div class="p-5">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-3" id="workflowActions"></div>
      </div>
    </div>

    <!-- TIMELINE -->
    <div class="panel mb-6">
      <div class="panel-header">04 — Admission Timeline</div>
      <div class="p-5">
        <div id="timelinePanel"></div>
      </div>
    </div>

    <!-- CARE COORDINATION -->
    <div class="panel mb-6">
      <div class="panel-header">05 — Care Coordination</div>
      <div class="p-5 grid grid-cols-1 md:grid-cols-2 gap-3">
        <div class="care-card">
          <div class="care-card-role">Attending Physician</div>
          <div class="text-sm font-medium" id="cc-attending">—</div>
          <div class="text-xs mt-1" style="color:var(--slate)">Clinical decision authority · Order entry · Certification of medical necessity</div>
        </div>
        <div class="care-card">
          <div class="care-card-role">Case Manager</div>
          <div class="text-sm font-medium">TBD — Assigned on admission</div>
          <div class="text-xs mt-1" style="color:var(--slate)">Care coordination · Resource utilization · Discharge planning liaison</div>
        </div>
        <div class="care-card">
          <div class="care-card-role">Nursing</div>
          <div class="text-sm font-medium">Charge Nurse — Unit pending</div>
          <div class="text-xs mt-1" style="color:var(--slate)">Patient arrival preparation · Initial assessment · MOON delivery (if applicable)</div>
        </div>
        <div class="care-card" style="border-color:var(--amber);background:rgba(212,134,15,0.06)">
          <div class="care-card-role" style="color:var(--amber-light)">Utilization Review</div>
          <div class="text-sm font-medium">UR Coordinator — Pending assignment</div>
          <div class="text-xs mt-2" style="color:var(--slate)">
            <span style="color:var(--amber-light)">●</span> Concurrent review upon admission<br/>
            <span style="color:var(--amber-light)">●</span> Denial risk identification &amp; escalation<br/>
            <span style="color:var(--amber-light)">●</span> InterQual criteria validation<br/>
            <span style="color:var(--amber-light)">●</span> Milliman Care Guidelines cross-check
          </div>
        </div>
        <div class="care-card">
          <div class="care-card-role">Discharge Planner</div>
          <div class="text-sm font-medium">Social Work / Case Mgmt Hybrid</div>
          <div class="text-xs mt-1" style="color:var(--slate)">SNF eligibility determination · Post-acute planning · Payer-specific LOS targets</div>
        </div>
      </div>
    </div>

    <!-- RISK TRACKING -->
    <div class="panel mb-6">
      <div class="panel-header">06 — Risk Tracking</div>
      <div class="p-5">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-3" id="riskPanel"></div>
      </div>
    </div>

    <!-- GOVERNANCE SNAPSHOT (conditional) -->
    <div id="governancePanel" class="hidden mb-6 fade-in">
      <div class="governance-box">
        <div class="section-eyebrow mb-2">Governance Snapshot</div>
        <p class="text-xs mb-3" style="color:var(--slate)">Industry benchmarks — estimates only, for training purposes:</p>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
          <div>
            <div class="mono text-lg font-semibold" style="color:var(--teal-bright)">3–5 days</div>
            <div class="text-xs" style="color:var(--slate)">Typical PA turnaround time</div>
          </div>
          <div>
            <div class="mono text-lg font-semibold" style="color:var(--amber-light)">~8–10%</div>
            <div class="text-xs" style="color:var(--slate)">Inpatient denial rate (CMS estimate)</div>
          </div>
          <div>
            <div class="mono text-lg font-semibold" style="color:var(--slate-light)">~$11</div>
            <div class="text-xs" style="color:var(--slate)">PA rework cost per transaction (CAQH)</div>
          </div>
        </div>
      </div>
    </div>

    <!-- FINAL DECISION -->
    <div id="finalDecision" class="hidden fade-in"></div>

    <!-- REASSESS BUTTON -->
    <div class="mt-6 flex gap-3">
      <button class="btn-action" onclick="computeFinalDecision()">🔄 Reassess Readiness</button>
      <button class="btn-action" onclick="resetSim()">↩ New Admission</button>
    </div>
  </div>

</div>

<script>
// ── STATE ──────────────────────────────────────────────────────────────────
const state = {
  provider: '', physician: '', diagnosis: '', admissionType: '',
  paStatus: '', admissionDate: '',
  score: 0,
  actionsCompleted: new Set(),
  paAppealed: false,
  paResolved: false, // denied→appealed→approved
};

// ── FIELD CHANGE HANDLERS ─────────────────────────────────────────────────
function onAdmissionTypeChange() {
  const v = document.getElementById('admissionType').value;
  document.getElementById('obsBanner').classList.toggle('hidden', v !== 'observation');
}
function onDiagnosisChange() {
  const v = document.getElementById('diagnosis').value;
  const show = v === 'ami' || v === 'chf';
  document.getElementById('interqualBanner').classList.toggle('hidden', !show);
}

// ── SCORE CALCULATOR ──────────────────────────────────────────────────────
function calcScore() {
  const pa = state.paStatus === 'na' ? 'approved' : (state.paResolved ? 'approved' : state.paStatus);
  const done = state.actionsCompleted;
  const isICU = state.admissionType === 'icu';
  const isHighClinical = ['ami','chf'].includes(state.diagnosis) || isICU;

  // Base weights
  let weights = { pa: 25, doc: 20, orders: 20, ins: 15, consent: 10, bed: 10 };

  // PA component
  let paScore = 0;
  if (pa === 'approved' || pa === 'na') paScore = weights.pa;
  else if (pa === 'pending') paScore = weights.pa * 0.3;
  else if (pa === 'denied') paScore = 0;

  // Action-based components
  let docScore = 0, ordersScore = 0, insScore = 0, consentScore = 0, bedScore = 0;

  if (done.has('upload_docs')) docScore += weights.doc * 0.6;
  if (done.has('contact_physician')) { docScore += weights.doc * 0.4; ordersScore += weights.orders * 0.7; }
  if (done.has('verify_insurance')) insScore = weights.ins;
  if (done.has('complete_consent')) consentScore = weights.consent;
  if (done.has('assign_bed')) bedScore = weights.bed;
  if (done.has('notify_nursing')) ordersScore += weights.orders * 0.3;
  if (done.has('prepare_arrival')) { } // minor, absorbed

  // Physician orders cap if no physician contact
  ordersScore = Math.min(ordersScore, weights.orders);

  // Denied + ICU cap: cannot reach 70% from admin tasks alone when pa=denied & icu
  let raw = paScore + docScore + ordersScore + insScore + consentScore + bedScore;

  if (state.paStatus !== 'na' && !state.paResolved && state.paStatus === 'denied' && isICU) {
    raw = Math.min(raw, 69);
  }

  // Initial analysis: cap at 60% on first load
  return Math.min(Math.round(raw), 100);
}

// ── INITIAL ANALYSIS ──────────────────────────────────────────────────────
function analyzeAdmission() {
  // Collect form
  state.provider = document.getElementById('provider').value;
  state.physician = document.getElementById('physician').value;
  state.diagnosis = document.getElementById('diagnosis').value;
  state.admissionType = document.getElementById('admissionType').value;
  state.paStatus = document.getElementById('paStatus').value;
  state.admissionDate = document.getElementById('admissionDate').value;

  if (!state.provider || !state.physician || !state.diagnosis || !state.admissionType || !state.paStatus || !state.admissionDate) {
    alert('Please complete all fields before analyzing.');
    return;
  }

  state.actionsCompleted.clear();
  state.paAppealed = false;
  state.paResolved = false;

  document.getElementById('cc-attending').textContent = state.physician;

  renderStatusCards();
  renderScore(true); // initial cap 30–60
  renderPABranch();
  renderWorkflow();
  renderTimeline();
  renderRisks();
  renderGovernance();
  renderFinalDecision();

  document.getElementById('analysisOutput').classList.remove('hidden');
  document.getElementById('analysisOutput').classList.add('fade-in');
  document.getElementById('analysisOutput').scrollIntoView({ behavior: 'smooth', block: 'start' });
}

// ── STATUS CARDS ──────────────────────────────────────────────────────────
function renderStatusCards() {
  const pa = state.paStatus;
  const done = state.actionsCompleted;

  const cards = [
    {
      label: 'PA Status',
      value: pa === 'na' ? 'Not Required' : pa.charAt(0).toUpperCase()+pa.slice(1),
      dot: pa === 'approved' || pa === 'na' ? 'dot-green' : pa === 'pending' ? 'dot-amber' : 'dot-red',
      weight: '25%'
    },
    {
      label: 'Insurance',
      value: done.has('verify_insurance') ? 'Verified' : 'Pending Verification',
      dot: done.has('verify_insurance') ? 'dot-green' : 'dot-amber',
      weight: '15%'
    },
    {
      label: 'Bed Assignment',
      value: done.has('assign_bed') ? 'Assigned' : 'Pending',
      dot: done.has('assign_bed') ? 'dot-green' : 'dot-amber',
      weight: '10%'
    },
    {
      label: 'Clinical Documentation',
      value: done.has('upload_docs') && done.has('contact_physician') ? 'Complete' : done.has('upload_docs') ? 'Partial' : 'Incomplete',
      dot: done.has('upload_docs') && done.has('contact_physician') ? 'dot-green' : done.has('upload_docs') ? 'dot-amber' : 'dot-red',
      weight: '20%'
    },
    {
      label: 'Physician Orders',
      value: done.has('contact_physician') ? 'Entered' : 'Not Entered',
      dot: done.has('contact_physician') ? 'dot-green' : 'dot-red',
      weight: '20%'
    },
    {
      label: 'Consent',
      value: done.has('complete_consent') ? 'Obtained' : 'Pending',
      dot: done.has('complete_consent') ? 'dot-green' : 'dot-red',
      weight: '10%'
    },
  ];

  document.getElementById('statusCards').innerHTML = cards.map(c => `
    <div class="care-card flex flex-col gap-1">
      <div class="flex items-center justify-between">
        <span class="care-card-role">${c.label}</span>
        <span class="weight-tag">${c.weight}</span>
      </div>
      <div class="flex items-center mt-1">
        <span class="status-dot ${c.dot}"></span>
        <span class="text-sm font-medium">${c.value}</span>
      </div>
    </div>
  `).join('');
}

function renderScore(initial = false) {
  let s = calcScore();
  if (initial) s = Math.min(Math.max(s, 30), 60); // clamp on first render
  state.score = s;

  document.getElementById('scoreDisplay').textContent = s + '%';
  const bar = document.getElementById('scoreBar');
  bar.style.width = s + '%';
  bar.className = 'score-bar-fill ' + (s >= 75 ? 'score-high' : s >= 50 ? 'score-mid' : 'score-low');
}

// ── PA BRANCH ─────────────────────────────────────────────────────────────
function renderPABranch() {
  const pa = state.paStatus === 'na' ? 'approved' : (state.paResolved ? 'approved' : state.paStatus);
  const el = document.getElementById('paBranchPanel');

  if (pa === 'approved') {
    el.innerHTML = `<div class="pa-branch" style="border-color:var(--green)">
      <div class="mono text-xs font-semibold mb-2" style="color:var(--green-bright)">✓ PA Approved — Workflow May Proceed</div>
      <p class="text-xs" style="color:var(--slate-light)">Prior authorization is confirmed. Continue with bed assignment, documentation, and consent workflows.</p>
    </div>`;
  } else if (pa === 'pending') {
    el.innerHTML = `<div class="pa-branch" style="border-color:var(--amber)">
      <div class="mono text-xs font-semibold mb-2" style="color:var(--amber-light)">⏳ PA Pending — Required Actions</div>
      <div class="flex flex-wrap gap-2 mt-3">
        <button class="btn-action ${state.actionsCompleted.has('followup_pa') ? 'active' : ''}" onclick="doAction('followup_pa')">📞 Follow Up with Payer</button>
        <button class="btn-action ${state.actionsCompleted.has('upload_docs') ? 'active' : ''}" onclick="doAction('upload_docs')">📄 Upload Clinical Docs</button>
        <button class="btn-action ${state.actionsCompleted.has('contact_physician') ? 'active' : ''}" onclick="doAction('contact_physician')">🩺 Contact Physician</button>
      </div>
    </div>`;
  } else if (pa === 'denied') {
    el.innerHTML = `<div class="pa-branch" style="border-color:var(--red)">
      <div class="mono text-xs font-semibold mb-2" style="color:var(--red-light)">✗ PA Denied — Appeal Required</div>
      <p class="text-xs mb-3" style="color:var(--slate-light)">Prior authorization has been denied. Initiate appeal process. Denied PA + ICU admission cannot reach 70% readiness from administrative tasks alone.</p>
      <div class="flex flex-wrap gap-2">
        <button class="btn-action ${state.actionsCompleted.has('review_denial') ? 'active' : ''}" onclick="doAction('review_denial')">🔍 Review Denial Reason</button>
        <button class="btn-action ${state.actionsCompleted.has('contact_insurance') ? 'active' : ''}" onclick="doAction('contact_insurance')">📞 Contact Insurance</button>
        <button class="btn-action ${state.actionsCompleted.has('submit_appeal') ? 'active' : ''}" onclick="doAction('submit_appeal')" ${!state.actionsCompleted.has('review_denial') || !state.actionsCompleted.has('contact_insurance') ? 'disabled' : ''}>⚖ Submit Appeal</button>
      </div>
      ${state.actionsCompleted.has('submit_appeal') && !state.paResolved ? `
      <div class="mt-3 p-3 rounded" style="background:rgba(26,122,74,0.12);border:1px solid var(--green)">
        <div class="text-xs mb-2" style="color:var(--green-bright)">Appeal submitted. Simulate outcome:</div>
        <div class="flex gap-2">
          <button class="btn-action" style="color:var(--green-bright);border-color:var(--green)" onclick="resolveAppeal(true)">✓ Appeal Approved</button>
          <button class="btn-action" style="color:var(--red-light);border-color:var(--red)" onclick="resolveAppeal(false)">✗ Appeal Denied</button>
        </div>
      </div>` : ''}
      ${state.paResolved ? `<div class="mt-3 mono text-xs" style="color:var(--green-bright)">✓ Appeal approved — PA converted to Approved status.</div>` : ''}
    </div>`;
  }
}

function resolveAppeal(success) {
  if (success) {
    state.paResolved = true;
  }
  refreshAll();
}

// ── WORKFLOW ACTIONS ──────────────────────────────────────────────────────
const ACTIONS = [
  { id: 'assign_bed', label: '🛏 Assign Bed' },
  { id: 'verify_insurance', label: '🔐 Verify Insurance' },
  { id: 'upload_docs', label: '📄 Upload Documentation' },
  { id: 'complete_consent', label: '✍ Complete Consent' },
  { id: 'contact_physician', label: '🩺 Contact Physician' },
  { id: 'notify_nursing', label: '🔔 Notify Nursing' },
  { id: 'prepare_arrival', label: '🚑 Prepare Patient Arrival' },
];

function renderWorkflow() {
  document.getElementById('workflowActions').innerHTML = ACTIONS.map(a => `
    <button class="btn-action ${state.actionsCompleted.has(a.id) ? 'active' : ''}" onclick="doAction('${a.id}')">
      ${a.label}${state.actionsCompleted.has(a.id) ? ' ✓' : ''}
    </button>
  `).join('');
}

function doAction(id) {
  state.actionsCompleted.add(id);
  refreshAll();
}

// ── TIMELINE ─────────────────────────────────────────────────────────────
function renderTimeline() {
  const done = state.actionsCompleted;
  const steps = [
    { label: 'PA Review', done: ['approved','na'].includes(state.paStatus === 'na' ? 'na' : state.paResolved ? 'approved' : state.paStatus), active: state.paStatus === 'pending' },
    { label: 'Insurance Verification', done: done.has('verify_insurance') },
    { label: 'Bed Assignment', done: done.has('assign_bed') },
    { label: 'Documentation', done: done.has('upload_docs') },
    { label: 'Consent', done: done.has('complete_consent') },
    { label: 'Patient Arrival', done: done.has('prepare_arrival') },
    { label: 'Registration', done: done.has('prepare_arrival') && done.has('verify_insurance') },
    { label: 'Clinical Assessment', done: done.has('contact_physician') && done.has('prepare_arrival') },
    { label: 'Admission Complete', done: state.score >= 90 },
  ];

  document.getElementById('timelinePanel').innerHTML = steps.map((s, i) => {
    const cls = s.done ? 'done' : s.active ? 'active' : 'pending';
    const icon = s.done ? '✓' : (i+1).toString();
    return `<div class="timeline-step">
      <div class="timeline-node ${cls}">${icon}</div>
      <div>
        <div class="text-sm font-medium ${s.done ? '' : 'opacity-60'}">${s.label}</div>
        ${s.done ? '<div class="mono text-xs" style="color:var(--teal-bright)">Complete</div>' : s.active ? '<div class="mono text-xs" style="color:var(--amber-light)">In Progress</div>' : '<div class="mono text-xs" style="color:var(--text-dim)">Pending</div>'}
      </div>
    </div>`;
  }).join('');
}

// ── RISKS ─────────────────────────────────────────────────────────────────
function renderRisks() {
  const done = state.actionsCompleted;
  const pa = state.paStatus === 'na' ? 'approved' : (state.paResolved ? 'approved' : state.paStatus);
  const isHighClinical = ['ami','chf'].includes(state.diagnosis) || state.admissionType === 'icu';

  const docRisk = !done.has('upload_docs') ? 'high' : !done.has('contact_physician') ? 'med' : 'low';
  const insRisk = !done.has('verify_insurance') ? 'med' : 'low';
  const bedRisk = !done.has('assign_bed') ? 'med' : 'low';
  const clinRisk = isHighClinical ? (!done.has('contact_physician') ? 'high' : 'med') : (!done.has('contact_physician') ? 'med' : 'low');

  const risks = [
    { label: 'Documentation Risk', level: docRisk },
    { label: 'Insurance Risk', level: insRisk },
    { label: 'Bed Risk', level: bedRisk },
    { label: 'Clinical Risk', level: clinRisk, elevated: isHighClinical },
  ];

  const labels = { low: 'Low', med: 'Moderate', high: 'High' };
  const cls = { low: 'risk-low', med: 'risk-med', high: 'risk-high' };

  document.getElementById('riskPanel').innerHTML = risks.map(r => `
    <div class="care-card">
      <div class="care-card-role">${r.label}${r.elevated ? ' ⬆' : ''}</div>
      <div class="mt-2"><span class="risk-pill ${cls[r.level]}"><span>●</span>${labels[r.level]}</span></div>
      ${r.elevated ? '<div class="text-xs mt-2" style="color:var(--amber)">Weighted higher for this diagnosis/type</div>' : ''}
    </div>
  `).join('');
}

// ── GOVERNANCE ────────────────────────────────────────────────────────────
function renderGovernance() {
  const s = calcScore();
  document.getElementById('governancePanel').classList.toggle('hidden', s < 75);
}

// ── FINAL DECISION ────────────────────────────────────────────────────────
function renderFinalDecision() {}

function computeFinalDecision() {
  const s = calcScore();
  state.score = s;
  renderStatusCards();
  const bar = document.getElementById('scoreBar');
  bar.style.width = s + '%';
  bar.className = 'score-bar-fill ' + (s >= 75 ? 'score-high' : s >= 50 ? 'score-mid' : 'score-low');
  document.getElementById('scoreDisplay').textContent = s + '%';

  renderGovernance();

  const done = state.actionsCompleted;
  const pa = state.paStatus === 'na' ? 'approved' : (state.paResolved ? 'approved' : state.paStatus);

  const el = document.getElementById('finalDecision');
  el.classList.remove('hidden');
  el.classList.add('fade-in');

  const diagLabels = { ami:'Acute MI', chf:'CHF', pneumonia:'Pneumonia', elective:'Elective Surgery', hip:'Hip Fracture' };
  const typeLabels = { inpatient:'Inpatient', observation:'Observation', emergency:'Emergency', icu:'ICU', sameday:'Same-Day Surgery' };

  if (s >= 90) {
    const moonNote = state.admissionType === 'observation' ? `<div class="moon-banner mt-3"><span class="mono text-xs font-semibold" style="color:var(--red-light)">ACTION REQUIRED — MOON Notification</span><p class="text-xs mt-1" style="color:var(--slate-light)">Patient is under Observation status. Written Medicare Outpatient Observation Notice (MOON) must be delivered to the patient within 36 hours of start of observation services.</p></div>` : '';
    el.innerHTML = `
      <div class="final-admit fade-in">
        <div class="mono text-xs font-semibold mb-1" style="color:var(--green-bright)">FINAL DECISION</div>
        <div class="flex items-center gap-3 mb-4">
          <span class="text-3xl">✅</span>
          <div>
            <div class="text-xl font-semibold">Admit — Readiness Confirmed</div>
            <div class="mono text-sm" style="color:var(--green-bright)">Score: ${s}% — Threshold met</div>
          </div>
        </div>
        <div class="separator"></div>
        <div class="grid grid-cols-2 md:grid-cols-3 gap-4 text-sm mt-3">
          <div><div class="field-label">Provider</div>${state.provider}</div>
          <div><div class="field-label">Physician</div>${state.physician}</div>
          <div><div class="field-label">Diagnosis</div>${diagLabels[state.diagnosis]}</div>
          <div><div class="field-label">Admission Type</div>${typeLabels[state.admissionType]}</div>
          <div><div class="field-label">PA Status</div>${pa.charAt(0).toUpperCase()+pa.slice(1)}</div>
          <div><div class="field-label">Admission Date</div>${state.admissionDate}</div>
        </div>
        <div class="separator"></div>
        <div class="grid grid-cols-2 gap-2 text-xs">
          ${[...done].map(a => `<div style="color:var(--teal-bright)">✓ ${ACTIONS.find(x=>x.id===a)?.label || a}</div>`).join('')}
        </div>
        ${moonNote}
      </div>`;
  } else {
    // Build missing items
    const missing = [];
    if (pa === 'denied') missing.push('PA denial must be resolved via successful appeal');
    if (pa === 'pending') missing.push('PA approval must be confirmed before full readiness');
    if (!done.has('verify_insurance')) missing.push('Insurance verification incomplete');
    if (!done.has('upload_docs')) missing.push('Clinical documentation not uploaded');
    if (!done.has('contact_physician')) missing.push('Physician orders not confirmed');
    if (!done.has('complete_consent')) missing.push('Patient consent not obtained');
    if (!done.has('assign_bed')) missing.push('Bed not assigned');

    el.innerHTML = `
      <div class="final-reject fade-in">
        <div class="mono text-xs font-semibold mb-1" style="color:var(--amber-light)">FINAL DECISION</div>
        <div class="flex items-center gap-3 mb-4">
          <span class="text-3xl">⚠</span>
          <div>
            <div class="text-xl font-semibold">Not Ready — Admission Blocked</div>
            <div class="mono text-sm" style="color:var(--amber-light)">Score: ${s}% — Requires ≥ 90%</div>
          </div>
        </div>
        <div class="separator"></div>
        <div class="mb-3">
          <div class="field-label mb-2">Missing Items / Required Actions</div>
          ${missing.map(m => `<div class="flex items-start gap-2 mb-1"><span style="color:var(--red-light)">✗</span><span class="text-sm">${m}</span></div>`).join('')}
        </div>
        ${state.admissionType === 'icu' && pa === 'denied' ? `<div class="moon-banner mt-3"><span class="mono text-xs font-semibold" style="color:var(--red-light)">ICU + Denied PA</span><p class="text-xs mt-1" style="color:var(--slate-light)">Per simulation rules, denied PA combined with ICU admission cannot reach 70% readiness from administrative tasks alone. Resolve PA status first.</p></div>` : ''}
      </div>`;
  }
  el.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
}

// ── REFRESH ALL ───────────────────────────────────────────────────────────
function refreshAll() {
  renderStatusCards();
  renderScore(false);
  renderPABranch();
  renderWorkflow();
  renderTimeline();
  renderRisks();
  renderGovernance();
  document.getElementById('finalDecision').classList.add('hidden');
}

// ── RESET ─────────────────────────────────────────────────────────────────
function resetSim() {
  state.provider=''; state.physician=''; state.diagnosis=''; state.admissionType='';
  state.paStatus=''; state.admissionDate=''; state.score=0;
  state.actionsCompleted.clear(); state.paAppealed=false; state.paResolved=false;
  ['provider','physician','diagnosis','admissionType','paStatus','admissionDate'].forEach(id => {
    document.getElementById(id).value='';
  });
  document.getElementById('analysisOutput').classList.add('hidden');
  document.getElementById('obsBanner').classList.add('hidden');
  document.getElementById('interqualBanner').classList.add('hidden');
  window.scrollTo({ top: 0, behavior: 'smooth' });
}
</script>
</body>
</html>


