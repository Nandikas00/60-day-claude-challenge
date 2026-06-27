# Today, I Built a Prior Authorization Story Simulator using claude :

## 📚 Key Learnings

Building this Prior Authorization Story Simulator helped me understand both the healthcare authorization process and interactive application design.

### Healthcare Domain
- Learned the end-to-end Prior Authorization workflow from request initiation to final decision.
- Understood the importance of medical necessity, supporting clinical documentation, and payer review.
- Explored different outcomes including approvals, denials, pending requests, and appeals.
- Gained insight into the responsibilities of patients, providers, and insurance companies during the authorization process.

### Technical Learnings
- Used Claude AI to rapidly prototype and refine a story-driven simulator.
- Improved prompt engineering skills by iteratively guiding AI to generate application logic and interactive scenarios.
- Designed branching story paths where user decisions determine the final outcome.
- Implemented state management to track story progression and user choices.
- Built reusable UI components for dialogs, story cards, and navigation.
- Enhanced debugging skills by reviewing and refining AI-generated code to improve functionality and user experience.

### Overall Takeaway
This project demonstrated how AI-assisted development can accelerate the creation of educational simulations while still requiring thoughtful prompt design, testing, and customization to deliver an engaging and realistic user experience.

#### Output Screenshots :
<img width="1768" height="879" alt="Screenshot (435)" src="https://github.com/user-attachments/assets/aa33fce3-abd0-43b9-a590-a6dc6c73b8cd" />
<img width="1666" height="912" alt="Screenshot (434)" src="https://github.com/user-attachments/assets/3c3b4bff-a7c5-49d9-8410-353e2b3214c5" />
<img width="1180" height="917" alt="Screenshot (433)" src="https://github.com/user-attachments/assets/bd5f8840-ed77-4e2d-8154-a3a622df4315" />
<img width="1212" height="893" alt="Screenshot (432)" src="https://github.com/user-attachments/assets/4fa56e8e-e857-4f97-8997-922f9731811d" />
<img width="1195" height="916" alt="Screenshot (431)" src="https://github.com/user-attachments/assets/6a7054e8-12ff-4f09-8b65-333074a9aa6c" />
<img width="1352" height="862" alt="Screenshot (429)" src="https://github.com/user-attachments/assets/509082c4-c07e-4f75-ba6d-97ab1bb9685a" />

#### HTML File :
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rahul's PA Journey — Understanding Prior Authorization</title>
<script src="https://cdn.tailwindcss.com"></script>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:ital,wght@0,400;0,500;0,600;1,400&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --teal-deep: #0D6E6E;
    --teal-mid: #1A9090;
    --teal-pale: #E6F4F4;
    --amber: #D97706;
    --amber-pale: #FEF3C7;
    --red-soft: #DC2626;
    --red-pale: #FEE2E2;
    --green-soft: #059669;
    --green-pale: #D1FAE5;
    --slate: #1E293B;
    --muted: #64748B;
    --surface: #F8FAFA;
    --white: #FFFFFF;
    --border: #CBD5E1;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: 'IBM Plex Sans', sans-serif;
    background: var(--surface);
    color: var(--slate);
    min-height: 100vh;
  }
  .mono { font-family: 'IBM Plex Mono', monospace; }

  /* Progress bar */
  #progress-bar-fill {
    transition: width 0.6s cubic-bezier(.4,0,.2,1);
    background: linear-gradient(90deg, var(--teal-deep), var(--teal-mid));
  }

  /* Bubbles */
  .bubble-rahul {
    background: var(--white);
    border: 1.5px solid var(--border);
    border-radius: 0 16px 16px 16px;
    color: var(--slate);
  }
  .bubble-priya {
    background: var(--teal-deep);
    border-radius: 16px 0 16px 16px;
    color: var(--white);
  }
  .bubble-priya .label-tag {
    background: rgba(255,255,255,0.15);
    color: rgba(255,255,255,0.9);
  }
  .label-tag {
    display: inline-block;
    font-size: 10px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 2px 8px;
    border-radius: 99px;
    background: var(--teal-pale);
    color: var(--teal-deep);
    margin-bottom: 4px;
  }
  .narrator-line {
    font-style: italic;
    color: var(--muted);
    font-size: 0.82rem;
    text-align: center;
    padding: 6px 24px;
  }
  .info-card {
    background: var(--amber-pale);
    border-left: 3px solid var(--amber);
    border-radius: 8px;
    padding: 10px 14px;
    font-size: 0.82rem;
    color: #78350f;
    margin-top: 6px;
  }
  .denial-card {
    background: var(--red-pale);
    border-left: 3px solid var(--red-soft);
    border-radius: 8px;
    padding: 10px 14px;
    font-size: 0.82rem;
    color: #7f1d1d;
    margin-top: 6px;
  }
  .success-card {
    background: var(--green-pale);
    border-left: 3px solid var(--green-soft);
    border-radius: 8px;
    padding: 10px 14px;
    font-size: 0.82rem;
    color: #064e3b;
    margin-top: 6px;
  }
  .flow-diagram {
    background: var(--white);
    border: 1.5px solid var(--border);
    border-radius: 10px;
    padding: 12px 16px;
    font-size: 0.78rem;
    margin-top: 8px;
    color: var(--slate);
  }
  .flow-step {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    background: var(--teal-pale);
    color: var(--teal-deep);
    border-radius: 6px;
    padding: 4px 10px;
    font-weight: 600;
    font-size: 0.75rem;
  }
  .flow-arrow {
    color: var(--muted);
    font-size: 1.1rem;
    font-weight: 300;
  }

  /* Choice buttons */
  .choice-btn {
    border: 1.5px solid var(--teal-deep);
    color: var(--teal-deep);
    background: var(--white);
    border-radius: 8px;
    padding: 8px 16px;
    font-size: 0.82rem;
    font-weight: 500;
    cursor: pointer;
    transition: background 0.18s, color 0.18s, transform 0.1s;
    font-family: 'IBM Plex Sans', sans-serif;
  }
  .choice-btn:hover {
    background: var(--teal-deep);
    color: var(--white);
    transform: translateY(-1px);
  }
  .choice-btn:disabled {
    opacity: 0.45;
    cursor: not-allowed;
    transform: none;
  }
  .choice-btn.selected {
    background: var(--teal-deep);
    color: var(--white);
  }

  /* Scene title */
  .scene-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: var(--white);
    border: 1.5px solid var(--border);
    border-radius: 99px;
    padding: 5px 14px 5px 8px;
    font-size: 0.75rem;
    font-weight: 600;
    color: var(--muted);
    letter-spacing: 0.05em;
  }
  .scene-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    background: var(--teal-mid);
    display: inline-block;
  }

  /* Chat scroll */
  #chat-feed {
    scroll-behavior: smooth;
  }
  .bubble-wrap {
    animation: fadeUp 0.35s ease both;
  }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(10px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  .cite-tag {
    font-size: 0.7rem;
    font-style: italic;
    opacity: 0.75;
    margin-top: 4px;
    display: block;
  }
  .checklist-item {
    display: flex;
    align-items: flex-start;
    gap: 6px;
    margin-bottom: 5px;
    font-size: 0.83rem;
  }
  .check-icon {
    flex-shrink: 0;
    margin-top: 2px;
    color: var(--teal-mid);
  }
  .check-icon-red { color: #dc2626; }
  .check-icon-amber { color: var(--amber); }

  /* Header */
  .header-pill {
    background: var(--teal-pale);
    color: var(--teal-deep);
    font-size: 0.7rem;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    border-radius: 99px;
    padding: 3px 10px;
  }
</style>
</head>
<body>

<!-- HEADER -->
<div style="background:var(--white); border-bottom:1.5px solid var(--border); position:sticky; top:0; z-index:50;">
  <div style="max-width:720px; margin:0 auto; padding:12px 20px; display:flex; align-items:center; justify-content:space-between; gap:12px; flex-wrap:wrap;">
    <div>
      <div class="header-pill" style="margin-bottom:4px;">Healthcare Education</div>
      <div style="font-weight:600; font-size:1rem; color:var(--slate); line-height:1.2;">Prior Authorization — A Patient's Journey</div>
    </div>
    <div style="font-size:0.75rem; color:var(--muted); text-align:right;">
      <span class="mono" id="scene-counter">Scene 1 of 8</span>
    </div>
  </div>
  <!-- Progress bar -->
  <div style="height:3px; background:var(--teal-pale);">
    <div id="progress-bar-fill" style="height:100%; width:0%;"></div>
  </div>
</div>

<!-- MAIN LAYOUT -->
<div style="max-width:720px; margin:0 auto; padding:24px 16px 120px;">

  <!-- Characters legend -->
  <div style="display:flex; gap:10px; justify-content:center; margin-bottom:20px; flex-wrap:wrap;">
    <div style="display:flex; align-items:center; gap:6px; font-size:0.78rem; color:var(--muted);">
      <span style="font-size:1.2rem;">👦</span>
      <span><strong style="color:var(--slate);">Rahul</strong> — Patient</span>
    </div>
    <div style="color:var(--border);">•</div>
    <div style="display:flex; align-items:center; gap:6px; font-size:0.78rem; color:var(--muted);">
      <span style="font-size:1.2rem;">👧</span>
      <span><strong style="color:var(--slate);">Priya</strong> — Healthcare Operations</span>
    </div>
    <div style="color:var(--border);">•</div>
    <div style="display:flex; align-items:center; gap:6px; font-size:0.78rem; color:var(--muted);">
      <span style="font-size:1rem; font-style:italic;">italic</span>
      <span>Narrator / Doctor</span>
    </div>
  </div>

  <!-- Chat feed -->
  <div id="chat-feed" style="display:flex; flex-direction:column; gap:10px;"></div>

  <!-- Choices area -->
  <div id="choices-area" style="margin-top:24px; display:flex; flex-direction:column; gap:8px; align-items:center;"></div>

</div>

<script>
// ─── DATA ──────────────────────────────────────────────────────────────────

const SCENES = [

  // SCENE 1 — Doctor Visit
  {
    id: 1,
    title: "Scene 1 — Doctor Visit",
    messages: [
      { type: "narrator", text: "City Medical Center, Rheumatology Department." },
      { type: "rahul", label: "Symptoms", text: "Doctor, my joints have been stiff and swollen for months — especially in the mornings. It lasts for hours sometimes." },
      { type: "narrator", text: "Dr. Patel reviews Rahul's blood work, imaging, and history." },
      { type: "narrator", text: "Dr. Patel: \"Rahul, your lab results show elevated CRP and RF levels. Combined with your symptoms, this looks like Rheumatoid Arthritis — an autoimmune condition where your immune system attacks your joints.\"" },
      { type: "rahul", label: "Worried", text: "That sounds serious. What do we do?" },
      { type: "narrator", text: "Dr. Patel: \"I'd like to start you on Humira — a biologic drug that targets inflammation at its source. It's effective for moderate-to-severe RA. But first, your insurance will likely require prior authorization before they'll cover it.\"" },
      { type: "rahul", label: "Confused", text: "Prior authorization? What does that mean?" },
      { type: "priya", label: "Intro", text: "Hi Rahul! I'm Priya, a healthcare operations specialist. I'm here to walk you through the whole process — step by step, in plain language. Prior auth, or PA, is basically your insurer's permission slip before covering certain medications. Let's go through it together." },
    ],
    choices: [
      { label: "🤔 \"Why does insurance need to approve my doctor's decision?\"", key: "skeptical" },
      { label: "📋 \"Okay, what's the first step?\"", key: "ready" },
    ],
    choiceResponses: {
      skeptical: [
        { type: "rahul", label: "Skeptical", text: "Why does insurance need to approve what my doctor prescribed? Isn't that the doctor's job?" },
        { type: "priya", label: "Honest", text: "Completely fair question — and honestly, it's one a lot of patients ask. PA exists so insurers can verify the prescription is medically appropriate, that cheaper alternatives were tried first, and that there's no billing error. It's a cost-control mechanism. That said, when it delays treatment, the human cost can be real. We'll talk more about that." },
      ],
      ready: [
        { type: "rahul", label: "Ready", text: "Okay, let's do it. What happens next?" },
        { type: "priya", label: "Guiding", text: "Great attitude! The first step happens at Dr. Patel's office — not at the pharmacy. Her team submits a PA request directly to your insurer, StarCare Health. Let me explain exactly what that looks like." },
      ],
    },
  },

  // SCENE 2 — Insurance Roadblock
  {
    id: 2,
    title: "Scene 2 — Insurance Roadblock",
    messages: [
      { type: "narrator", text: "Dr. Patel's office submits the Prior Authorization request." },
      { type: "priya", label: "Process", text: "Here's exactly how the PA flow works for Rahul's case:", isFlow: true },
      { type: "narrator", text: "Note: The pharmacy is not involved at this stage. This is a direct conversation between the provider and the payer." },
      { type: "priya", label: "Clarifying", text: "StarCare Health (an illustrative example of a commercial payer) now has Rahul's PA request. They'll review it — usually within 3–5 business days for non-urgent cases, or 72 hours for urgent ones." },
      { type: "rahul", label: "Waiting", text: "So I just… wait? What are they actually looking at?" },
      { type: "priya", label: "Preview", text: "Good question — the next scene covers exactly that. But the short answer: they're checking your diagnosis, your history, and whether Humira is the right drug at this stage of treatment." },
      {
        type: "priya", label: "Key Fact", text: "One thing to know: once a PA is approved, it's saved on file. For Humira, you typically won't need to re-request every time you fill the prescription — the approval covers a set period.", isSuccess: true,
      },
    ],
    choices: [
      { label: "📊 \"What documents did Dr. Patel's office send?\"", key: "docs" },
      { label: "⏱️ \"Can the timeline be expedited?\"", key: "timeline" },
    ],
    choiceResponses: {
      docs: [
        { type: "rahul", label: "Curious", text: "What exactly did Dr. Patel's office include in the PA request?" },
        { type: "priya", label: "Detail", text: "Great question. A PA submission typically includes: Rahul's ICD-10 diagnosis code (M06.9 for RA), clinical notes, lab results, the specific drug requested (Humira / adalimumab), and a treatment history showing what prior therapies were tried. We call this a clinical package." },
      ],
      timeline: [
        { type: "rahul", label: "Anxious", text: "3–5 days feels long. Can this be sped up?" },
        { type: "priya", label: "Practical", text: "Yes — if the case is clinically urgent, Dr. Patel can request an expedited review. Insurers are required by law to respond within 72 hours in those cases. The office would note clinical urgency in the submission." },
      ],
    },
  },

  // SCENE 3 — What is PA?
  {
    id: 3,
    title: "Scene 3 — What is PA?",
    messages: [
      { type: "narrator", text: "Priya takes a step back to explain prior authorization in plain terms." },
      { type: "rahul", label: "Genuinely lost", text: "I still don't fully understand what prior authorization actually is. Can you explain it like I'm completely new to this?" },
      { type: "priya", label: "Plain language", text: "Of course. Think of PA like a second opinion from the insurance company before they agree to pay. Your doctor says you need Humira. But your insurer wants to check: Is this the right diagnosis? Is this the right drug for this stage? Did you try less expensive options first? Only after they say yes does the coverage kick in." },
      { type: "priya", label: "Step Therapy", text: "That last part — trying cheaper options first — is called step therapy. The insurer essentially says: start with Drug A (maybe a generic like methotrexate). If it doesn't work, then we'll approve Drug B (like Humira). The idea is to start with lower-cost treatments and only escalate if needed." },
      {
        type: "priya", label: "Important Nuance", text: "Here's where it gets complicated: for aggressive autoimmune conditions like Rheumatoid Arthritis, delays can matter. The longer inflammation goes uncontrolled, the more joint damage can occur. PA isn't always just paperwork — it can have real clinical consequences.", isDenial: false, isWarning: true,
      },
      {
        type: "priya", label: "Research", text: "AMA 2023 PA Survey: PA causes treatment delays in the majority of cases — with many physicians reporting patient harm as a result.", isCite: true,
      },
      { type: "rahul", label: "Concerned", text: "So this bureaucratic process can actually hurt people?" },
      { type: "priya", label: "Balanced", text: "It can, when it isn't handled well — or when it's used to deny medically necessary care. But when it works correctly, PA helps prevent unnecessary treatments, billing errors, and drug interactions. The system matters. So does how it's administered." },
    ],
    choices: [
      { label: "💊 \"What if I just paid out of pocket for Humira?\"", key: "oop" },
      { label: "📚 \"Has step therapy reform happened anywhere?\"", key: "reform" },
    ],
    choiceResponses: {
      oop: [
        { type: "rahul", label: "Weighing Options", text: "What if I just paid for Humira myself and skipped the PA process?" },
        { type: "priya", label: "Reality Check", text: "Humira can cost $6,000–$8,000 per month without insurance. That's not realistic for most people. That's exactly why insurance coverage — and navigating PA — matters so much. The financial stakes of getting this right are high." },
      ],
      reform: [
        { type: "rahul", label: "Hopeful", text: "Has anything changed around step therapy rules? This seems broken." },
        { type: "priya", label: "Reform-aware", text: "Yes — several states have passed step therapy reform laws requiring insurers to grant exceptions when a patient has already failed a drug, or when step therapy poses health risks. In 2018, Congress passed the Patient Access to Treatments Act for Medicare Advantage plans. It's a growing area of reform." },
      ],
    },
  },

  // SCENE 4 — Insurance Review
  {
    id: 4,
    title: "Scene 4 — Insurance Review",
    messages: [
      { type: "narrator", text: "StarCare Health (illustrative example) begins its clinical review." },
      { type: "priya", label: "Inside the Review", text: "Let me walk you through exactly what a payer like StarCare Health checks — and why each piece matters." },
      {
        type: "priya", label: "Check 1: Eligibility", text: "✅ Is Rahul actually covered under this plan? Is his coverage active? This sounds basic — but coverage lapses or enrollment errors can block a PA before it starts. Always verify eligibility first.", isChecklist: true, checks: [
          { icon: "✅", text: "Is Rahul enrolled in an active StarCare Health plan?" },
          { icon: "✅", text: "Is Humira on the plan's formulary (approved drug list)?" },
        ],
      },
      {
        type: "priya", label: "Check 2: Clinical Documentation", text: "The insurer reviews Dr. Patel's clinical notes, labs, and imaging. They're asking: does the documentation actually support this diagnosis and this drug?", isChecklist: true, checks: [
          { icon: "📄", text: "Lab values (CRP, RF, anti-CCP)" },
          { icon: "📄", text: "Clinical notes from visit" },
          { icon: "📄", text: "Duration and severity of symptoms" },
        ],
      },
      {
        type: "priya", label: "Check 3: ICD-10 Match", text: "ICD-10 is the universal code system for diagnoses. Rahul's code is M06.9 — Rheumatoid Arthritis, unspecified. The insurer checks: does the code submitted match the drug being requested? A mismatch = automatic flag.", isInfo: true,
      },
      {
        type: "priya", label: "Check 4: Step Therapy History", text: "This is often the trickiest part. The insurer checks: has Rahul tried first-line RA drugs like methotrexate or hydroxychloroquine? If yes, and they failed — the PA for Humira is much stronger. If there's no record of prior treatment, they may require it before approving a biologic.", isWarning: true,
      },
      { type: "rahul", label: "Nervous", text: "What if something's missing from my file?" },
      { type: "priya", label: "Heads up", text: "That's exactly how denials happen. Missing documentation is one of the top reasons for PA denial — even when the prescription is clinically appropriate. The next scene covers a denial, and what to do about it." },
    ],
    choices: [
      { label: "🔍 \"Who actually reviews my PA — a doctor or a computer?\"", key: "reviewer" },
      { label: "📁 \"How does the office track all this paperwork?\"", key: "tracking" },
    ],
    choiceResponses: {
      reviewer: [
        { type: "rahul", label: "Skeptical", text: "Who actually reads my PA at StarCare Health? Is it a doctor? An algorithm?" },
        { type: "priya", label: "Transparent", text: "Often both. Initial screening may be automated — checking for correct codes and completeness. But clinical review is typically done by a nurse or physician reviewer at the payer. For complex cases or appeals, you have the right to request a peer-to-peer review — meaning Dr. Patel talks directly to the insurer's medical reviewer." },
      ],
      tracking: [
        { type: "rahul", label: "Process-curious", text: "Dr. Patel's office must deal with dozens of these. How do they keep track?" },
        { type: "priya", label: "Operational", text: "Larger practices use PA management software or clearinghouses that integrate with EHR systems. Smaller offices often track via spreadsheets or manual logs. It's one reason PA is so staff-intensive — and why 2+ hours of staff time per denial is common. We'll come back to that." },
      ],
    },
  },

  // SCENE 5 — Denial
  {
    id: 5,
    title: "Scene 5 — Denial",
    messages: [
      { type: "narrator", text: "StarCare Health issues a determination." },
      {
        type: "priya", label: "Decision", text: "❌ PA DENIED — Reason: Insufficient documentation of step therapy. Humira is a biologic agent. StarCare Health requires documented evidence that the patient has tried and failed at least one conventional DMARD (like methotrexate) for RA before a biologic will be approved.", isDenial: true,
      },
      { type: "rahul", label: "Crushed", text: "Denied? That means I can't get the medication?" },
      { type: "priya", label: "Reassuring", text: "This is not the end. A denial is not permanent — it's a request for more information, or a starting point for an appeal. Most denials can be overturned with the right documentation and process." },
      {
        type: "priya", label: "What Denial Means Operationally", text: "PA denials cost physician offices an average of 2+ staff hours to resolve — per denial. That's time spent gathering records, filing appeals, and making calls to the insurer. This is a significant hidden cost in healthcare operations.", isCite: true,
      },
      { type: "priya", label: "Why This Happened", text: "In Rahul's case, Dr. Patel's notes documented that methotrexate was discussed and declined due to Rahul's liver concerns — but that wasn't stated explicitly enough in the submission. StarCare Health's reviewer didn't see documented failure of a prior DMARD, so they applied their step therapy policy." },
      { type: "rahul", label: "Frustrated", text: "So it was a paperwork issue, not a medical issue?" },
      { type: "priya", label: "Honest", text: "Largely, yes. The clinical case for Humira is strong. The documentation didn't tell the full story. That's fixable — through an appeal." },
    ],
    choices: [
      { label: "😤 \"Can we file a complaint about this?\"", key: "complaint" },
      { label: "📝 \"Let's appeal. What do we need?\"", key: "appeal" },
    ],
    choiceResponses: {
      complaint: [
        { type: "rahul", label: "Upset", text: "Is there someone we can report this to? This feels wrong." },
        { type: "priya", label: "Empowered", text: "Yes. Patients can file a grievance with the insurer, contact their State Insurance Commissioner, or in extreme cases escalate to the ACA's external review process. For now, the fastest path is appealing — which puts the clinical evidence front and center. Complaints can happen in parallel." },
      ],
      appeal: [
        { type: "rahul", label: "Determined", text: "Let's focus on the appeal. What do we need to gather?" },
        { type: "priya", label: "Action-oriented", text: "That's the right move. The appeal requires three things: updated clinical documentation, a Letter of Medical Necessity from Dr. Patel, and a formal appeal submission to StarCare Health. Let's go through each one." },
      ],
    },
  },

  // SCENE 6 — Appeal
  {
    id: 6,
    title: "Scene 6 — Appeal",
    messages: [
      { type: "narrator", text: "Dr. Patel's office begins the appeal process." },
      { type: "priya", label: "Appeal Process", text: "An appeal is a formal request for StarCare Health to reconsider their decision. Here's what needs to happen:" },
      {
        type: "priya", label: "Step 1: Update Clinical Docs", text: "", isChecklist: true, checks: [
          { icon: "📋", text: "Add explicit documentation: methotrexate was contraindicated due to Rahul's elevated liver enzymes." },
          { icon: "📋", text: "Attach lab reports showing liver function values." },
          { icon: "📋", text: "Note that step therapy alternatives carry clinical risk in this case." },
        ],
      },
      { type: "narrator", text: "Dr. Patel: \"I'll write the Letter of Medical Necessity today. We need to be explicit that methotrexate was not safe for Rahul — not just inconvenient.\"" },
      {
        type: "priya", label: "Step 2: Letter of Medical Necessity (LMN)", text: "", isChecklist: true, checks: [
          { icon: "✍️", text: "Written by Dr. Patel on clinic letterhead." },
          { icon: "✍️", text: "Explains why Humira is medically necessary for Rahul specifically." },
          { icon: "✍️", text: "Addresses the step therapy requirement directly — with clinical rationale for the exception." },
          { icon: "✍️", text: "Cites Rahul's diagnosis (ICD-10: M06.9), severity, and risk of disease progression." },
        ],
      },
      {
        type: "priya", label: "Step 3: Submit Formal Appeal", text: "", isChecklist: true, checks: [
          { icon: "📬", text: "Appeal filed within StarCare Health's deadlines (typically 180 days from denial)." },
          { icon: "📬", text: "Request a peer-to-peer review — Dr. Patel speaks directly with StarCare's medical reviewer." },
          { icon: "📬", text: "Keep copies of everything submitted (reference numbers, timestamps)." },
        ],
      },
      { type: "rahul", label: "Engaged", text: "Can I do anything as the patient?" },
      { type: "priya", label: "Patient Role", text: "Absolutely. You can write a personal statement describing how your symptoms affect daily life. You can ask Dr. Patel's office for copies of everything submitted. And you can follow up directly with StarCare Health using your case reference number. You're not a passive bystander in this process." },
    ],
    choices: [
      { label: "🤝 \"What is a peer-to-peer review exactly?\"", key: "p2p" },
      { label: "⏳ \"How long does the appeal take?\"", key: "timing" },
    ],
    choiceResponses: {
      p2p: [
        { type: "rahul", label: "Curious", text: "You mentioned a peer-to-peer review. What's that?" },
        { type: "priya", label: "Key Tool", text: "A peer-to-peer (P2P) review is when Dr. Patel gets on a call directly with StarCare Health's medical reviewer. She can explain the clinical picture, answer questions, and advocate for Rahul in real time. Studies show P2P reviews overturn denials in a large share of cases — it's one of the most effective tools in an appeal." },
      ],
      timing: [
        { type: "rahul", label: "Practical", text: "How long will this appeal take? I'm still in pain." },
        { type: "priya", label: "Timeframes", text: "Internal appeals must be resolved within 30 days for non-urgent cases, or 72 hours for urgent/expedited appeals. StarCare Health's denial notice should include exact deadlines. If the internal appeal fails, Rahul has the right to an external review by an independent organization." },
      ],
    },
  },

  // SCENE 7 — Approval
  {
    id: 7,
    title: "Scene 7 — Approval",
    messages: [
      { type: "narrator", text: "StarCare Health completes its appeal review." },
      {
        type: "priya", label: "Decision", text: "✅ PA APPROVED — Humira (adalimumab) authorized for Rahul. Reference #: SCH-2024-RA-00847. Authorization period: 12 months. Step therapy exception granted based on clinical documentation of methotrexate contraindication.", isSuccess: true,
      },
      { type: "rahul", label: "Relieved", text: "Finally! So I can get my prescription now?" },
      { type: "priya", label: "Next Steps", text: "Yes! Here's what happens now: Dr. Patel's office sends the approved PA reference number to your pharmacy. The pharmacy verifies it with StarCare Health. Humira gets dispensed — often through a specialty pharmacy since it's a biologic that requires refrigeration and injection training." },
      {
        type: "priya", label: "On File", text: "The approved PA is saved permanently in StarCare Health's system. You won't need to repeat this PA for Humira throughout the 12-month authorization period — as long as your coverage stays active and you refill within the approved window.", isSuccess: true,
      },
      { type: "rahul", label: "Grateful", text: "I had no idea how much went into getting a single prescription filled." },
      { type: "priya", label: "Validating", text: "Most people don't — until they're in it. And that's exactly why understanding the system matters. When you know the process, you can advocate for yourself, ask the right questions, and flag problems early." },
      { type: "narrator", text: "Dr. Patel: \"Rahul, starting Humira now is important. RA is a progressive condition — every month of uncontrolled inflammation matters. I'm glad we got here.\"" },
    ],
    choices: [
      { label: "💊 \"What do I need to know about taking Humira?\"", key: "medication" },
      { label: "📊 \"What does this look like from the system's perspective?\"", key: "system" },
    ],
    choiceResponses: {
      medication: [
        { type: "rahul", label: "Preparing", text: "What should I expect when I start Humira?" },
        { type: "priya", label: "Practical", text: "Humira is a self-injected biologic — usually given every two weeks. You'll get injection training from the specialty pharmacy or a nurse. Common early effects include injection-site reactions. It can take 8–12 weeks for full clinical effect. Keep Dr. Patel updated on how you're feeling throughout." },
      ],
      system: [
        { type: "rahul", label: "Big picture", text: "How does StarCare Health look at all of this from their side?" },
        { type: "priya", label: "System View", text: "Payers track key metrics: initial denial rate (what percentage of PAs are denied), appeal rate (how many denials are appealed), overturn rate (how many appeals succeed), and average resolution time. A high overturn rate signals that initial denials may be too aggressive. These metrics drive policy changes. Rahul's appeal is data." },
      ],
    },
  },

  // SCENE 8 — Takeaways
  {
    id: 8,
    title: "Scene 8 — Takeaways",
    messages: [
      { type: "narrator", text: "Looking back at Rahul's journey — and what it reveals about the healthcare system." },
      { type: "priya", label: "Patient Perspective", text: "Here's what Rahul learned as a patient:" },
      {
        type: "priya", label: "Patient Takeaways", text: "", isChecklist: true, checks: [
          { icon: "💡", text: "PA is your insurer's approval process — not your doctor's recommendation. The two are separate." },
          { icon: "💡", text: "A denial is not the end. It's often a documentation issue, not a medical decision." },
          { icon: "💡", text: "You have rights: to appeal, to request peer-to-peer review, to external review if needed." },
          { icon: "💡", text: "Ask your doctor's office: \"What's the PA status?\" — don't assume it's handled." },
          { icon: "💡", text: "For chronic conditions, delays in treatment can have real consequences. Urgency matters." },
        ],
      },
      { type: "rahul", label: "Reflective", text: "I went from not knowing what PA stood for to navigating an appeal. I wish this was taught somewhere." },
      { type: "priya", label: "System Perspective", text: "And here's how health systems and payers look at this journey in aggregate:" },
      {
        type: "priya", label: "System Metrics", text: "", isChecklist: true, checks: [
          { icon: "📊", text: "Denial Rate — % of PA requests initially denied. Industry average: 5–15% depending on drug class." },
          { icon: "📊", text: "Appeal Rate — % of denials that are appealed. Low appeal rates may mean patients are giving up." },
          { icon: "📊", text: "Overturn Rate — % of appeals that succeed. High rates signal the initial denial was unjustified." },
          { icon: "📊", text: "Resolution Time — Average days from PA request to final decision. Shorter = better patient outcomes." },
          { icon: "📊", text: "Staff Hours per PA — Average burden on provider offices. 2+ hours per denial case is well-documented." },
        ],
      },
      {
        type: "priya", label: "Closing Thought", text: "Rahul's journey isn't unusual — it's the norm for biologic drugs. The prior authorization system can protect against unnecessary treatments, but it can also delay life-changing care. Understanding it — as a patient, caregiver, or healthcare professional — is the first step to navigating it well.", isSuccess: true,
      },
      { type: "rahul", label: "Thank you", text: "Thanks, Priya. I feel like I actually understand what happened to me — and what to do next time." },
      { type: "priya", label: "Empowered", text: "That's exactly it. You're not just a patient anymore — you're an informed advocate. And that changes everything." },
      { type: "narrator", text: "End of Rahul's PA Journey. StarCare Health is used throughout as an illustrative example of a commercial payer." },
    ],
    choices: [
      { label: "🔁 Start over from Scene 1", key: "restart" },
      { label: "📖 Review key terms glossary", key: "glossary" },
    ],
    choiceResponses: {
      restart: [],
      glossary: [
        { type: "priya", label: "Glossary", text: "", isGlossary: true },
      ],
    },
  },
];

// ─── STATE ──────────────────────────────────────────────────────────────────
let currentScene = 0;
let messageQueue = [];
let isAnimating = false;

// ─── DOM REFS ───────────────────────────────────────────────────────────────
const feed = document.getElementById('chat-feed');
const choicesArea = document.getElementById('choices-area');
const progressFill = document.getElementById('progress-bar-fill');
const sceneCounter = document.getElementById('scene-counter');

// ─── HELPERS ─────────────────────────────────────────────────────────────────

function setProgress(scene) {
  const pct = (scene / 8) * 100;
  progressFill.style.width = pct + '%';
  sceneCounter.textContent = `Scene ${scene} of 8`;
}

function createEl(tag, cls, text) {
  const el = document.createElement(tag);
  if (cls) el.className = cls;
  if (text) el.textContent = text;
  return el;
}

function appendNarrator(text) {
  const wrap = createEl('div', 'bubble-wrap narrator-line');
  wrap.textContent = text;
  feed.appendChild(wrap);
}

function appendSceneBadge(title) {
  const wrap = createEl('div', 'bubble-wrap');
  wrap.style.cssText = 'display:flex;justify-content:center;margin:16px 0 8px;';
  const badge = createEl('div', 'scene-badge');
  const dot = createEl('span', 'scene-dot');
  badge.appendChild(dot);
  badge.appendChild(document.createTextNode(' ' + title));
  wrap.appendChild(badge);
  feed.appendChild(wrap);
}

function appendRahul(msg) {
  const wrap = createEl('div', 'bubble-wrap');
  wrap.style.cssText = 'display:flex;align-items:flex-end;gap:8px;';

  const avatar = createEl('div');
  avatar.style.cssText = 'font-size:1.5rem;flex-shrink:0;';
  avatar.textContent = '👦';

  const col = createEl('div');
  col.style.cssText = 'display:flex;flex-direction:column;max-width:72%;';

  if (msg.label) {
    const tag = createEl('span', 'label-tag');
    tag.textContent = msg.label;
    tag.style.cssText = 'background:#f1f5f9;color:#475569;font-size:10px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;padding:2px 8px;border-radius:99px;margin-bottom:4px;display:inline-block;width:fit-content;';
    col.appendChild(tag);
  }

  const bubble = createEl('div', 'bubble-rahul');
  bubble.style.cssText = 'padding:10px 14px;font-size:.875rem;line-height:1.6;';
  bubble.textContent = msg.text;
  col.appendChild(bubble);

  wrap.appendChild(avatar);
  wrap.appendChild(col);
  feed.appendChild(wrap);
}

function appendPriya(msg) {
  const wrap = createEl('div', 'bubble-wrap');
  wrap.style.cssText = 'display:flex;align-items:flex-end;gap:8px;flex-direction:row-reverse;';

  const avatar = createEl('div');
  avatar.style.cssText = 'font-size:1.5rem;flex-shrink:0;';
  avatar.textContent = '👧';

  const col = createEl('div');
  col.style.cssText = 'display:flex;flex-direction:column;align-items:flex-end;max-width:80%;';

  if (msg.label) {
    const tag = createEl('span', 'label-tag');
    tag.textContent = msg.label;
    tag.style.cssText = 'background:rgba(13,110,110,0.12);color:#0D6E6E;font-size:10px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;padding:2px 8px;border-radius:99px;margin-bottom:4px;display:inline-block;';
    col.appendChild(tag);
  }

  const bubble = createEl('div', 'bubble-priya');
  bubble.style.cssText = 'padding:10px 14px;font-size:.875rem;line-height:1.6;';

  if (msg.text) {
    const t = createEl('p');
    t.textContent = msg.text;
    bubble.appendChild(t);
  }

  // Flow diagram
  if (msg.isFlow) {
    const flow = createEl('div', 'flow-diagram');
    flow.style.cssText = 'background:#fff;border:1.5px solid #CBD5E1;border-radius:10px;padding:12px 16px;margin-top:8px;font-size:.78rem;';
    const label = createEl('div');
    label.style.cssText = 'font-weight:600;color:#1E293B;margin-bottom:8px;font-size:.78rem;letter-spacing:.03em;text-transform:uppercase;';
    label.textContent = 'PA Flow — Rahul\'s Case';
    flow.appendChild(label);
    const steps = createEl('div');
    steps.style.cssText = 'display:flex;align-items:center;gap:6px;flex-wrap:wrap;';
    const items = [
      { icon: '🏥', label: 'Dr. Patel\'s Office' },
      null,
      { icon: '📄', label: 'PA Request' },
      null,
      { icon: '🏢', label: 'StarCare Health (Payer)' },
    ];
    items.forEach(item => {
      if (!item) {
        const arr = createEl('span', 'flow-arrow');
        arr.textContent = '→';
        arr.style.color = '#94a3b8';
        steps.appendChild(arr);
      } else {
        const s = createEl('span', 'flow-step');
        s.style.cssText = 'display:inline-flex;align-items:center;gap:5px;background:#E6F4F4;color:#0D6E6E;border-radius:6px;padding:4px 10px;font-weight:600;font-size:.73rem;';
        s.textContent = item.icon + ' ' + item.label;
        steps.appendChild(s);
      }
    });
    flow.appendChild(steps);
    const note = createEl('div');
    note.style.cssText = 'font-size:.72rem;color:#64748B;margin-top:8px;font-style:italic;';
    note.textContent = 'No pharmacy involved at this stage. Provider ↔ Payer only.';
    flow.appendChild(note);
    bubble.appendChild(flow);
  }

  // Checklist
  if (msg.isChecklist && msg.checks) {
    const list = createEl('div');
    list.style.cssText = 'margin-top:8px;background:rgba(255,255,255,0.12);border-radius:8px;padding:10px 12px;';
    msg.checks.forEach(c => {
      const row = createEl('div');
      row.style.cssText = 'display:flex;align-items:flex-start;gap:6px;margin-bottom:6px;font-size:.82rem;';
      const icon = createEl('span');
      icon.style.cssText = 'flex-shrink:0;font-size:.95rem;';
      icon.textContent = c.icon;
      const txt = createEl('span');
      txt.textContent = c.text;
      row.appendChild(icon);
      row.appendChild(txt);
      list.appendChild(row);
    });
    bubble.appendChild(list);
  }

  // Info card (amber)
  if (msg.isInfo) {
    const card = createEl('div');
    card.style.cssText = 'background:rgba(255,255,255,0.15);border-left:3px solid #FCD34D;border-radius:8px;padding:10px 14px;font-size:.82rem;margin-top:8px;';
    card.textContent = '💡 ICD-10 Code Note: Always confirm the diagnosis code matches the drug being requested. Mismatches are the #1 administrative trigger for PA flags.';
    bubble.appendChild(card);
  }

  // Warning
  if (msg.isWarning) {
    const card = createEl('div');
    card.style.cssText = 'background:rgba(255,255,255,0.15);border-left:3px solid #FCD34D;border-radius:8px;padding:10px 14px;font-size:.82rem;margin-top:8px;';
    card.textContent = '⚠️ For aggressive autoimmune conditions like RA, uncontrolled inflammation during PA delays can contribute to irreversible joint damage.';
    bubble.appendChild(card);
  }

  // Denial card
  if (msg.isDenial) {
    bubble.style.background = '#7f1d1d';
  }

  // Success card
  if (msg.isSuccess) {
    bubble.style.background = '#065f46';
  }

  // Cite
  if (msg.isCite) {
    const cite = createEl('div');
    cite.style.cssText = 'font-size:.72rem;font-style:italic;opacity:.8;margin-top:6px;border-top:1px solid rgba(255,255,255,.2);padding-top:6px;';
    cite.textContent = '📎 Source: AMA 2023 Prior Authorization Physician Survey';
    bubble.appendChild(cite);
  }

  // Glossary
  if (msg.isGlossary) {
    const terms = [
      ['Prior Authorization (PA)', 'Insurer approval required before certain drugs/procedures are covered.'],
      ['Step Therapy', 'Requirement to try lower-cost treatments before approving a more expensive one.'],
      ['ICD-10', 'Universal diagnosis code system used in billing and PA submissions.'],
      ['LMN', 'Letter of Medical Necessity — a physician-written explanation of clinical need.'],
      ['DMARD', 'Disease-Modifying Antirheumatic Drug — first-line RA treatments (e.g., methotrexate).'],
      ['Biologic', 'Complex drugs derived from living organisms, like Humira (adalimumab). Often requires PA.'],
      ['Peer-to-Peer Review', 'A call between the prescribing physician and the payer\'s medical reviewer to discuss the case.'],
      ['Formulary', 'The insurer\'s approved list of covered drugs.'],
    ];
    const g = createEl('div');
    g.style.cssText = 'margin-top:8px;';
    terms.forEach(([term, def]) => {
      const row = createEl('div');
      row.style.cssText = 'margin-bottom:8px;font-size:.8rem;';
      const t = createEl('span');
      t.style.cssText = 'font-weight:700;display:block;';
      t.textContent = term;
      const d = createEl('span');
      d.style.cssText = 'opacity:.85;';
      d.textContent = def;
      row.appendChild(t);
      row.appendChild(d);
      g.appendChild(row);
    });
    bubble.appendChild(g);
  }

  col.appendChild(bubble);
  wrap.appendChild(avatar);
  wrap.appendChild(col);
  feed.appendChild(wrap);
}

function appendMessage(msg) {
  if (msg.type === 'narrator') {
    appendNarrator(msg.text);
  } else if (msg.type === 'rahul') {
    appendRahul(msg);
  } else if (msg.type === 'priya') {
    appendPriya(msg);
  }
  feed.lastElementChild.scrollIntoView({ behavior: 'smooth', block: 'end' });
}

function clearChoices() {
  while (choicesArea.firstChild) choicesArea.removeChild(choicesArea.firstChild);
}

async function sleep(ms) {
  return new Promise(r => setTimeout(r, ms));
}

async function playMessages(messages, delay = 420) {
  for (const msg of messages) {
    await sleep(delay);
    appendMessage(msg);
  }
}

async function showScene(index) {
  if (index >= SCENES.length) return;
  const scene = SCENES[index];

  appendSceneBadge(scene.title);
  await playMessages(scene.messages, 380);

  // Show choices
  clearChoices();
  setProgress(index + 1);

  const label = createEl('div');
  label.style.cssText = 'font-size:.73rem;font-weight:600;color:var(--muted);letter-spacing:.08em;text-transform:uppercase;margin-bottom:8px;text-align:center;';
  label.textContent = 'How would you like to respond?';
  choicesArea.appendChild(label);

  const btnRow = createEl('div');
  btnRow.style.cssText = 'display:flex;flex-wrap:wrap;gap:8px;justify-content:center;';

  scene.choices.forEach(choice => {
    const btn = createEl('button', 'choice-btn');
    btn.textContent = choice.label;
    btn.addEventListener('click', () => handleChoice(index, choice.key, btnRow));
    btnRow.appendChild(btn);
  });

  choicesArea.appendChild(btnRow);
  choicesArea.scrollIntoView({ behavior: 'smooth', block: 'end' });
}

async function handleChoice(sceneIndex, choiceKey, btnRow) {
  if (isAnimating) return;
  isAnimating = true;

  // Disable all buttons, highlight selected
  Array.from(btnRow.children).forEach(b => {
    b.disabled = true;
    if (b.dataset.key === choiceKey) b.classList.add('selected');
  });

  const scene = SCENES[sceneIndex];
  const responses = scene.choiceResponses[choiceKey] || [];

  // Mark selected button
  Array.from(btnRow.children).forEach(b => {
    const lbl = scene.choices.find(c => c.key === choiceKey)?.label;
    if (b.textContent === lbl) b.classList.add('selected');
  });

  // Play choice responses
  if (choiceKey === 'restart') {
    await sleep(400);
    clearChoices();
    currentScene = 0;
    while (feed.firstChild) feed.removeChild(feed.firstChild);
    setProgress(0);
    sceneCounter.textContent = 'Scene 1 of 8';
    isAnimating = false;
    showScene(0);
    return;
  }

  await playMessages(responses, 380);
  await sleep(500);

  clearChoices();

  // Advance to next scene
  currentScene = sceneIndex + 1;
  if (currentScene < SCENES.length) {
    await sleep(600);
    showScene(currentScene);
  } else {
    const done = createEl('div');
    done.style.cssText = 'text-align:center;color:var(--muted);font-size:.82rem;font-style:italic;padding:20px;';
    done.textContent = '✓ You\'ve completed Rahul\'s PA Journey.';
    choicesArea.appendChild(done);
  }

  isAnimating = false;
}

// ─── INIT ────────────────────────────────────────────────────────────────────
setProgress(0);
showScene(0);
</script>
</body>
</html>

