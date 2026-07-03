# Key Learnings :
- Learned how to approach business problems from a marketing strategist's perspective instead of focusing only on product features.
- Improved the ability to identify the target audience by understanding customer needs, pain points, and motivations.
- Practiced creating clear value propositions that communicate why a product or service stands out.
- Explored methods for conducting competitor analysis to identify market opportunities and areas for differentiation.
- Understood the importance of customer segmentation for developing more personalized marketing strategies.
- Learned how to align marketing goals with overall business objectives to create measurable outcomes.
- Practiced structuring marketing campaigns with clear objectives, target audience, messaging, and success metrics.
- Improved prompt engineering skills by using Claude to generate, refine, and evaluate strategic marketing ideas.
- Gained experience in breaking down complex marketing problems into actionable strategies.
- Recognized the importance of data-driven decision-making and continuous optimization in marketing.

## Output Screenshots :
<img width="1054" height="916" alt="Screenshot (523)" src="https://github.com/user-attachments/assets/a9704274-2361-4bea-8697-84acb8a6978d" />

### HTML File :
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Think Like a Marketing Strategist</title>
<style>
  :root{
    --bg:#0F1115;
    --panel:#171A21;
    --panel-2:#1D212A;
    --line:#2A2F3A;
    --ink:#E7E5E0;
    --ink-dim:#9199A6;
    --amber:#E8A33D;
    --amber-dim:#8a6528;
    --teal:#4FD1C5;
    --rose:#E36969;
    --serif: Georgia, 'Times New Roman', serif;
    --sans: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
    --mono: 'Courier New', Courier, monospace;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:
      radial-gradient(1200px 600px at 10% -10%, #1a1f2b 0%, transparent 60%),
      radial-gradient(1000px 700px at 110% 10%, #17202033 0%, transparent 55%),
      var(--bg);
    color:var(--ink);
    font-family:var(--sans);
    min-height:100vh;
    -webkit-font-smoothing:antialiased;
  }
  #root{max-width:980px;margin:0 auto;padding:28px 20px 80px;}

  ::selection{background:var(--amber);color:#1a1200;}

  /* Folder tab progress bar - signature element */
  .tabs{
    display:flex;
    gap:2px;
    margin-bottom:26px;
    border-bottom:1px solid var(--line);
    overflow-x:auto;
    scrollbar-width:none;
  }
  .tabs::-webkit-scrollbar{display:none;}
  .tab{
    flex:0 0 auto;
    padding:9px 14px 8px;
    font-family:var(--mono);
    font-size:11px;
    letter-spacing:.04em;
    text-transform:uppercase;
    color:var(--ink-dim);
    background:var(--panel);
    border:1px solid var(--line);
    border-bottom:none;
    border-radius:6px 6px 0 0;
    white-space:nowrap;
    position:relative;
    top:1px;
    transition:color .25s, background .25s;
  }
  .tab.active{
    color:var(--amber);
    background:var(--panel-2);
    border-color:var(--amber-dim);
  }
  .tab.done{color:var(--teal);}

  .brand-header{
    display:flex;
    align-items:baseline;
    justify-content:space-between;
    margin-bottom:24px;
    flex-wrap:wrap;
    gap:10px;
  }
  .brand-header h1{
    font-family:var(--serif);
    font-weight:400;
    font-size:22px;
    margin:0;
    color:var(--ink);
  }
  .brand-header .eyebrow{
    font-family:var(--mono);
    font-size:11px;
    color:var(--amber);
    letter-spacing:.08em;
    text-transform:uppercase;
    display:block;
    margin-bottom:4px;
  }
  .badge{
    font-family:var(--mono);
    font-size:11px;
    color:var(--ink-dim);
    border:1px solid var(--line);
    padding:4px 9px;
    border-radius:20px;
  }

  .card{
    background:var(--panel);
    border:1px solid var(--line);
    border-radius:10px;
    padding:22px 24px;
    margin-bottom:18px;
    animation:rise .45s ease both;
  }
  @keyframes rise{
    from{opacity:0; transform:translateY(10px);}
    to{opacity:1; transform:translateY(0);}
  }
  .card h2{
    font-family:var(--serif);
    font-weight:400;
    font-size:20px;
    margin:0 0 4px;
    color:var(--ink);
  }
  .card .sub{
    color:var(--ink-dim);
    font-size:14px;
    margin:0 0 16px;
    line-height:1.5;
  }
  .why-box{
    background:linear-gradient(180deg, #221a0f, #1c1710);
    border:1px solid var(--amber-dim);
    border-left:3px solid var(--amber);
    border-radius:6px;
    padding:12px 14px;
    margin:14px 0;
    font-size:13.5px;
    line-height:1.55;
    color:#e8d9b8;
  }
  .why-box b{color:var(--amber);}

  .grid{
    display:grid;
    grid-template-columns:repeat(auto-fit, minmax(220px,1fr));
    gap:12px;
  }
  .option{
    background:var(--panel-2);
    border:1px solid var(--line);
    border-radius:8px;
    padding:16px;
    cursor:pointer;
    transition:border-color .2s, transform .15s, background .2s;
    text-align:left;
  }
  .option:hover{border-color:var(--amber-dim); transform:translateY(-2px);}
  .option.selected{border-color:var(--amber); background:#20241c1a;}
  .option .icon{font-size:26px; display:block; margin-bottom:8px;}
  .option h3{margin:0 0 4px; font-size:15px; font-family:var(--sans); font-weight:600;}
  .option p{margin:0; font-size:12.5px; color:var(--ink-dim); line-height:1.5;}

  button.btn{
    font-family:var(--sans);
    font-weight:600;
    font-size:14px;
    color:#161005;
    background:var(--amber);
    border:none;
    padding:11px 20px;
    border-radius:7px;
    cursor:pointer;
    transition:transform .15s, box-shadow .2s, opacity .2s;
  }
  button.btn:hover{transform:translateY(-1px); box-shadow:0 6px 18px -6px #E8A33D66;}
  button.btn:disabled{opacity:.35; cursor:not-allowed; transform:none; box-shadow:none;}
  button.btn.ghost{
    background:transparent;
    color:var(--ink-dim);
    border:1px solid var(--line);
  }
  button.btn.ghost:hover{color:var(--ink); border-color:var(--ink-dim); box-shadow:none;}
  button.btn.teal{background:var(--teal); color:#04211d;}
  button.btn.rose{background:var(--rose); color:#2a0808;}

  .btn-row{display:flex; gap:10px; margin-top:18px; flex-wrap:wrap;}

  .platform-card{
    background:var(--panel-2);
    border:1px solid var(--line);
    border-radius:8px;
    padding:14px 16px;
    margin-bottom:10px;
    cursor:pointer;
    display:flex;
    align-items:flex-start;
    gap:12px;
    transition:border-color .2s;
  }
  .platform-card:hover{border-color:var(--amber-dim);}
  .platform-card.selected{border-color:var(--teal);}
  .platform-card .check{
    width:20px;height:20px;border-radius:5px;border:1px solid var(--ink-dim);
    flex:0 0 auto; display:flex; align-items:center; justify-content:center;
    font-size:12px; color:transparent; margin-top:2px;
  }
  .platform-card.selected .check{background:var(--teal); border-color:var(--teal); color:#04211d;}
  .platform-name{font-weight:700; font-size:14.5px; margin-bottom:3px;}
  .platform-fit{
    font-family:var(--mono); font-size:10.5px; letter-spacing:.05em; text-transform:uppercase;
    padding:2px 7px; border-radius:10px; margin-left:8px;
  }
  .fit-strong{background:#123b2f; color:#5be0b7;}
  .fit-weak{background:#3b1616; color:#e29494;}
  .platform-reason{font-size:13px; color:var(--ink-dim); line-height:1.5;}

  .pillar-card{
    background:var(--panel-2);
    border:1px solid var(--line);
    border-radius:8px;
    padding:15px 16px;
    cursor:pointer;
    transition:border-color .2s, background .2s;
  }
  .pillar-card.selected{border-color:var(--amber); background:#241d0e;}
  .pillar-card h3{margin:0 0 5px; font-size:14.5px;}
  .pillar-card p{margin:0; font-size:12.5px; color:var(--ink-dim); line-height:1.5;}
  .pillar-count{
    font-family:var(--mono); font-size:12px; color:var(--ink-dim); margin-bottom:14px;
  }
  .pillar-count b{color:var(--amber);}

  .week-card{
    border-left:3px solid var(--amber-dim);
    padding:10px 16px;
    margin-bottom:12px;
    background:var(--panel-2);
    border-radius:0 8px 8px 0;
  }
  .week-card .wk-label{
    font-family:var(--mono); font-size:11px; color:var(--amber); letter-spacing:.06em; text-transform:uppercase;
  }
  .week-card h4{margin:5px 0 5px; font-size:15px;}
  .week-card p{margin:0; font-size:13px; color:var(--ink-dim); line-height:1.55;}

  .event-box{
    background:linear-gradient(180deg,#1d1620,#171219);
    border:1px solid #4a2e5c;
    border-radius:8px;
    padding:18px 20px;
    margin-bottom:16px;
  }
  .event-box .tag{
    font-family:var(--mono); font-size:11px; color:#c98cf0; letter-spacing:.06em; text-transform:uppercase;
  }
  .event-box p{font-size:14.5px; line-height:1.6; margin:8px 0 0;}

  .consequence{
    margin-top:14px;
    padding:14px 16px;
    border-radius:8px;
    background:#10151a;
    border:1px solid var(--line);
    font-size:13.5px;
    line-height:1.6;
    animation:rise .4s ease both;
  }

  .report-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(260px,1fr));
    gap:14px;
    margin-top:6px;
  }
  .report-item{
    background:var(--panel-2);
    border:1px solid var(--line);
    border-radius:8px;
    padding:14px 16px;
  }
  .report-item .label{
    font-family:var(--mono); font-size:11px; color:var(--amber);
    text-transform:uppercase; letter-spacing:.06em; margin-bottom:6px; display:block;
  }
  .report-item p{margin:0; font-size:13.5px; color:var(--ink); line-height:1.55;}

  .lesson{
    display:flex; gap:10px; margin-bottom:10px; font-size:14px; line-height:1.55;
  }
  .lesson .n{color:var(--teal); font-family:var(--mono); font-weight:700;}

  .claude-card{
    background:#0f1720;
    border:1px dashed #2c4a52;
    border-radius:8px;
    padding:14px 16px;
    margin-top:16px;
  }
  .claude-card .cc-label{
    font-family:var(--mono); font-size:11px; color:var(--teal);
    text-transform:uppercase; letter-spacing:.06em; display:flex; align-items:center; gap:6px; margin-bottom:8px;
  }
  .claude-card pre{
    white-space:pre-wrap;
    word-break:break-word;
    font-family:var(--mono);
    font-size:12.5px;
    color:#c9d4d6;
    margin:0 0 10px;
    line-height:1.55;
  }
  .copy-btn{
    font-family:var(--mono);
    font-size:11px;
    background:transparent;
    border:1px solid #2c4a52;
    color:var(--teal);
    padding:5px 10px;
    border-radius:5px;
    cursor:pointer;
  }
  .copy-btn:hover{background:#12262a;}

  .text-input, textarea.text-input{
    width:100%;
    background:var(--panel-2);
    border:1px solid var(--line);
    border-radius:7px;
    color:var(--ink);
    padding:10px 12px;
    font-family:var(--sans);
    font-size:14px;
    margin-bottom:12px;
    resize:vertical;
  }
  .text-input:focus, textarea.text-input:focus{outline:2px solid var(--amber-dim); border-color:var(--amber);}
  label.field-label{font-size:12.5px; color:var(--ink-dim); display:block; margin-bottom:5px; font-family:var(--mono); text-transform:uppercase; letter-spacing:.04em;}

  .hero{
    text-align:center;
    padding:40px 10px 10px;
  }
  .hero .eyebrow{
    font-family:var(--mono); color:var(--amber); font-size:12px; letter-spacing:.15em; text-transform:uppercase;
  }
  .hero h1{
    font-family:var(--serif);
    font-size:38px;
    font-weight:400;
    margin:12px 0 14px;
    line-height:1.25;
  }
  .hero h1 em{color:var(--amber); font-style:normal;}
  .hero p.lead{
    color:var(--ink-dim);
    max-width:560px;
    margin:0 auto 30px;
    font-size:15.5px;
    line-height:1.6;
  }

  .footer-nav{
    display:flex; justify-content:space-between; align-items:center;
    margin-top:8px;
  }

  @media (max-width:640px){
    .hero h1{font-size:28px;}
    .card{padding:18px;}
  }

  .fade-in{animation:rise .4s ease both;}
  .kicker{
    font-family:var(--mono); font-size:11px; color:var(--ink-dim); letter-spacing:.05em;
    text-transform:uppercase; margin-bottom:8px; display:block;
  }
</style>
</head>
<body>
<div id="root"></div>

<script src="https://unpkg.com/react@18/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

<script type="text/babel">
const {useState, useMemo} = React;

/* ---------------- DATA ---------------- */

const INDUSTRIES = [
  {industry:"Cold-brew coffee subscription", audience:"Busy urban professionals, 25-40, who value convenience and quality", budget:"$3,000/month", competitors:["Blue Bottle", "Trade Coffee", "a growing list of local roasters on Instagram"], challenge:"Customers try the first box, love it, then quietly cancel after month two."},
  {industry:"Handmade ceramic homeware", audience:"Design-conscious renters and homeowners, 28-45, who follow interior design accounts", budget:"$1,200/month", competitors:["Etsy sellers", "West Elm's 'local finds' shelf", "a popular ceramicist with 400k followers"], challenge:"Beautiful product, but almost nobody outside a small local audience has heard of it."},
  {industry:"Budgeting app for freelancers", audience:"Freelancers and gig workers, 22-38, anxious about irregular income", budget:"$8,000/month", competitors:["Mint's freelancer-adjacent features", "QuickBooks Self-Employed", "a viral TikTok finance creator turned app founder"], challenge:"Lots of downloads, almost no one finishes onboarding."},
  {industry:"Boutique fitness studio", audience:"Local residents, 25-50, who want community as much as exercise", budget:"$2,000/month", competitors:["a national gym chain nearby", "two other boutique studios in the neighborhood"], challenge:"Great first-class experience, but very few people book a second class."},
  {industry:"Sustainable kids' clothing brand", audience:"Millennial parents, 28-42, who care about ethical sourcing", budget:"$5,000/month", competitors:["Primary", "Hanna Andersson", "a fast-fashion giant undercutting on price"], challenge:"Customers say they love the mission but choose the cheaper competitor at checkout."},
  {industry:"B2B project management software", audience:"Operations managers at 20-200 person companies", budget:"$15,000/month", competitors:["Asana", "Monday.com", "a well-funded startup with a flashy launch video"], challenge:"Sales calls go well, but almost no one signs up for the free trial first."},
  {industry:"Plant-based meal kit service", audience:"Health-focused households, 24-45, short on time", budget:"$6,000/month", competitors:["HelloFresh's plant-based line", "a regional competitor with cult-like reviews"], challenge:"Strong reviews, but the brand has zero recognition outside existing customers."},
  {industry:"Independent bookstore with a cafe", audience:"Local readers and remote workers, 20-55, who want a 'third place'", budget:"$800/month", competitors:["Amazon", "a big-box bookstore chain", "the coffee shop next door"], challenge:"Regulars love it, but foot traffic from new visitors has been flat for a year."},
];

const PLATFORM_LIBRARY = {
  business: [
    {id:"instagram", name:"Instagram", strong:true, reasonStrong:"Visual product, lifestyle-driven audience, and strong discovery via Reels and hashtags make this a natural home base.", reasonWeak:"Skews visual and casual — if the product isn't photogenic or the message needs long explanation, it will underperform."},
    {id:"tiktok", name:"TikTok", strong:true, reasonStrong:"Best platform for reaching new people who've never heard of the brand, especially with a younger or trend-aware audience.", reasonWeak:"Rewards volume and trend-fluency; a slow, low-frequency posting plan will struggle to get traction here."},
    {id:"facebook", name:"Facebook", strong:false, reasonStrong:"Useful for local businesses and community-driven audiences, plus strong ad targeting for older demographics.", reasonWeak:"Organic reach is weak and the audience skews older — a poor fit if the target customer is under 30."},
    {id:"linkedin", name:"LinkedIn", strong:false, reasonStrong:"The right home for B2B products or anything selling to a professional buyer.", reasonWeak:"Consumer lifestyle products get little traction here — the audience is in 'work mode,' not 'browse and buy' mode."},
    {id:"twitter", name:"X / Twitter", strong:false, reasonStrong:"Good for real-time conversation, customer service, and building a voice in a niche community.", reasonWeak:"Weak for product discovery and visual storytelling — better as a supporting channel than a primary one."},
    {id:"youtube", name:"YouTube", strong:false, reasonStrong:"Great for building deep trust through tutorials, behind-the-scenes, or demos that a 15-second clip can't cover.", reasonWeak:"High production effort for return — risky as a first channel with a small budget."},
    {id:"pinterest", name:"Pinterest", strong:true, reasonStrong:"Ideal for products people plan around — home, food, fashion — since users search here with buying intent.", reasonWeak:"Almost no value for service businesses or anything without a strong visual, 'save for later' quality."},
    {id:"email", name:"Email Newsletter", strong:true, reasonStrong:"The only channel the brand fully owns — not subject to an algorithm, and best for retention, not just discovery.", reasonWeak:"Won't help attract brand-new audiences on its own — it needs another channel feeding it new subscribers."},
  ],
  personal: [
    {id:"linkedin", name:"LinkedIn", strong:true, reasonStrong:"The default home for professional expertise — ideal for thought leadership, career story, and building credibility with decision-makers.", reasonWeak:"If the niche is purely creative or entertainment-based with no professional angle, LinkedIn's audience mismatch shows quickly."},
    {id:"twitter", name:"X / Twitter", strong:true, reasonStrong:"Best place to build a public reputation in real time — sharing opinions, engaging in your niche's conversations, and being discovered by peers.", reasonWeak:"Fast-moving and noisy; without consistent posting, momentum disappears quickly."},
    {id:"youtube", name:"YouTube", strong:true, reasonStrong:"Unmatched for demonstrating expertise in depth — tutorials, breakdowns, and long-form trust-building that text can't replicate.", reasonWeak:"High time cost per piece of content — hard to sustain without a real production habit."},
    {id:"newsletter", name:"Newsletter", strong:true, reasonStrong:"Builds a direct, algorithm-free relationship with an audience — the strongest long-term asset for a personal brand.", reasonWeak:"Slow to grow on its own; needs a louder platform to consistently funnel new subscribers in."},
    {id:"instagram", name:"Instagram", strong:false, reasonStrong:"Works well if the personal brand has a strong visual or lifestyle component alongside the expertise.", reasonWeak:"For purely text/idea-driven expertise, Instagram forces awkward visual packaging that dilutes the message."},
    {id:"tiktok", name:"TikTok", strong:false, reasonStrong:"Can rapidly grow reach if the niche translates well to short, punchy video.", reasonWeak:"Rewards entertainment value over depth — a poor fit for nuanced or highly technical expertise."},
    {id:"facebook", name:"Facebook", strong:false, reasonStrong:"Can work for community-building around a specific local or niche group.", reasonWeak:"Rarely where professional reputations are built today — mostly used by an older demographic for personal, not professional, content."},
    {id:"pinterest", name:"Pinterest", strong:false, reasonStrong:"Only useful if the personal brand centers on a highly visual skill, like design or crafts.", reasonWeak:"Almost never useful for building authority as a thinker, consultant, or expert."},
  ]
};

const PILLARS_LIBRARY = {
  business: [
    {id:"education", name:"Product Education", desc:"Teach the audience how to use or understand the product. Builds trust and reduces buyer hesitation."},
    {id:"social_proof", name:"Social Proof", desc:"Customer stories, reviews, and testimonials. Reduces risk in the buyer's mind — 'people like me already trust this.'"},
    {id:"behind_scenes", name:"Behind the Scenes", desc:"Show the process, the people, or the making of the product. Builds emotional connection and authenticity."},
    {id:"entertainment", name:"Entertainment / Trend", desc:"Light, trend-driven, or funny content. Optimized for reach and new-audience discovery, not conversion."},
    {id:"community", name:"Community Spotlight", desc:"Feature the audience itself — user-generated content, Q&As, polls. Builds loyalty and retention."},
    {id:"offer", name:"Promotions & Offers", desc:"Direct calls to purchase. Necessary, but only effective once trust from other pillars is already built."},
  ],
  personal: [
    {id:"thought_leadership", name:"Thought Leadership", desc:"Sharing opinions and frameworks in your niche. Builds authority and gets you seen as a go-to voice."},
    {id:"personal_story", name:"Personal Story", desc:"The journey, struggles, and turning points that shaped your expertise. Builds emotional connection and relatability."},
    {id:"behind_scenes", name:"Behind the Scenes", desc:"How you actually work — process, tools, routines. Builds trust through transparency."},
    {id:"audience_education", name:"Audience Education", desc:"Teaching what you know in digestible pieces. Builds credibility and gives people a reason to follow long-term."},
    {id:"community_voice", name:"Community & Conversation", desc:"Engaging with others' ideas, replying, amplifying peers. Builds relationships and expands reach through association."},
    {id:"offer", name:"Offer / Call to Action", desc:"Direct invitations — book a call, join a list, buy a course. Necessary occasionally, but overusing it burns trust fast."},
  ]
};

const EVENTS_BUSINESS = [
  {tag:"Sudden Attention", text:"A mid-size influencer posted about the product unprompted, and orders just tripled overnight. The website is holding, barely."},
  {tag:"Copycat", text:"A competitor launched a suspiciously similar product line two weeks after seeing the brand's campaign go semi-viral."},
  {tag:"Public Complaint", text:"A customer's frustrated post about a shipping delay is gaining traction, and people are starting to ask the brand to respond publicly."},
  {tag:"Budget Cut", text:"Leadership just cut the marketing budget by 40% for next quarter, effective immediately."},
  {tag:"Platform Shift", text:"The main platform the brand relies on just changed its algorithm, and organic reach has dropped by half this week."},
];

const EVENTS_PERSONAL = [
  {tag:"Viral Post", text:"One post unexpectedly took off overnight, and thousands of new people are now looking at your profile for the first time."},
  {tag:"Podcast Invite", text:"A well-known podcast in your niche just invited you on as a guest, with almost no notice — recording is in five days."},
  {tag:"Public Disagreement", text:"A respected figure in your space publicly disagreed with one of your recent posts, and people are watching to see how you respond."},
  {tag:"Someone Copied You", text:"You noticed another creator posted an idea that closely mirrors one of your original frameworks, word for word in places."},
  {tag:"Follower Spike", text:"Your following jumped significantly this week for no obvious reason, and engagement on old posts is picking back up too."},
];

const RESPONSE_OPTIONS = {
  business: [
    {id:"lean_in", label:"Lean in fully — reallocate budget to ride the momentum", consequence:"Short-term wins often compound if you act fast, but chasing every spike without a plan can drain budget from the strategy that was already working."},
    {id:"stay_course", label:"Acknowledge it, but stay disciplined on the existing plan", consequence:"Protects long-term consistency and avoids reactive decisions, though it risks leaving real opportunity on the table if the moment doesn't return."},
    {id:"go_quiet", label:"Say nothing and wait to see what happens", consequence:"Avoids overreacting, but silence can be read as indifference or even guilt — especially with public complaints or disputes."},
  ],
  personal: [
    {id:"lean_in", label:"Lean in fully — post more, engage everywhere, ride the wave", consequence:"Momentum is real and algorithms reward it, but posting reactively without a clear point of view can make the brand feel scattered once the spike fades."},
    {id:"stay_course", label:"Acknowledge it briefly, then return to your planned content", consequence:"Signals consistency and confidence in your niche, though it may underuse a rare moment of visibility that won't come back easily."},
    {id:"go_quiet", label:"Say nothing and let it play out on its own", consequence:"Sometimes the right call for low-stakes moments, but for public disagreements or copying, silence can be mistaken for having no position at all."},
  ]
};

/* ---------------- HELPERS ---------------- */

function rand(arr){ return arr[Math.floor(Math.random()*arr.length)]; }

function copyToClipboard(text){
  if(navigator.clipboard){ navigator.clipboard.writeText(text).catch(()=>{}); }
}

/* ---------------- SMALL COMPONENTS ---------------- */

function WhyBox({children}){
  return <div className="why-box"><b>Why this matters:</b> {children}</div>;
}

function ClaudeCard({prompt}){
  const [copied, setCopied] = useState(false);
  return (
    <div className="claude-card">
      <div className="cc-label">💬 How to ask Claude</div>
      <pre>{prompt}</pre>
      <button className="copy-btn" onClick={()=>{copyToClipboard(prompt); setCopied(true); setTimeout(()=>setCopied(false),1500);}}>
        {copied ? "Copied ✓" : "Copy prompt"}
      </button>
    </div>
  );
}

function ProgressTabs({stage, stages}){
  return (
    <div className="tabs">
      {stages.map((s,i)=>(
        <div key={s} className={"tab " + (i===stage ? "active" : i<stage ? "done":"")}>
          {String(i+1).padStart(2,"0")} · {s}
        </div>
      ))}
    </div>
  );
}

/* ---------------- MAIN SECTIONS ---------------- */

function Welcome({onSelectMode}){
  return (
    <div className="hero fade-in">
      <span className="eyebrow">A hands-on marketing strategy simulator</span>
      <h1>Think Like a <em>Marketing Strategist</em></h1>
      <p className="lead">
        Marketing isn't about making content — it's about making decisions.
        You'll take on a brand, understand its audience, choose the right platforms,
        plan real content, and react when things don't go as expected. Every step
        explains what you're doing and why it matters, the way a strategist would think it through.
      </p>
      <div className="grid" style={{maxWidth:720, margin:"0 auto"}}>
        <div className="option" onClick={()=>onSelectMode("business")}>
          <span className="icon">🏢</span>
          <h3>Use My Own Business</h3>
          <p>Bring a real or planned business and build a strategy around it.</p>
        </div>
        <div className="option" onClick={()=>onSelectMode("personal")}>
          <span className="icon">🙋</span>
          <h3>Build My Personal Brand</h3>
          <p>No business yet? Use your own name, expertise, and story as the brand.</p>
        </div>
        <div className="option" onClick={()=>onSelectMode("random")}>
          <span className="icon">🎲</span>
          <h3>A New Client Has Arrived</h3>
          <p>Get a randomly generated business, audience, and challenge to solve.</p>
        </div>
      </div>
    </div>
  );
}

function BusinessSetup({mode, onComplete}){
  const [randomBiz] = useState(()=> mode==="random" ? rand(INDUSTRIES) : null);
  const [form, setForm] = useState({
    name:"", industry:"", audience:"", budget:"", competitors:"", challenge:""
  });

  const isRandom = mode==="random";
  const isPersonal = mode==="personal";

  const set = (k,v) => setForm(f=>({...f,[k]:v}));

  const canContinue = isRandom ? true :
    isPersonal ? (form.name && form.industry && form.audience) :
    (form.name && form.industry && form.audience);

  const handleContinue = () => {
    if(isRandom){
      onComplete({
        mode,
        name: "Client Brief #" + (100+Math.floor(Math.random()*900)),
        industry: randomBiz.industry,
        audience: randomBiz.audience,
        budget: randomBiz.budget,
        competitors: randomBiz.competitors.join(", "),
        challenge: randomBiz.challenge,
      });
    } else {
      onComplete({...form, mode});
    }
  };

  return (
    <div className="card fade-in">
      <h2>{isPersonal ? "Define Your Personal Brand" : isRandom ? "Meet Your New Client" : "Tell Us About the Business"}</h2>
      <p className="sub">
        {isPersonal
          ? "For a personal brand, the 'product' is you — your expertise, story, and point of view. Understanding it clearly is step one of any real strategy."
          : isRandom
          ? "A strategist rarely gets to pick their client. Read the brief carefully — everything after this builds on it."
          : "A strategist always starts here: who is this for, what do they sell, and who are they trying to reach?"}
      </p>

      {isRandom ? (
        <div className="grid" style={{gridTemplateColumns:"1fr"}}>
          <div className="report-item">
            <span className="label">Industry</span>
            <p>{randomBiz.industry}</p>
          </div>
          <div className="report-item">
            <span className="label">Target Audience</span>
            <p>{randomBiz.audience}</p>
          </div>
          <div className="report-item">
            <span className="label">Monthly Marketing Budget</span>
            <p>{randomBiz.budget}</p>
          </div>
          <div className="report-item">
            <span className="label">Competitors</span>
            <p>{randomBiz.competitors.join(", ")}</p>
          </div>
          <div className="report-item">
            <span className="label">Marketing Challenge</span>
            <p>{randomBiz.challenge}</p>
          </div>
        </div>
      ) : (
        <div>
          <label className="field-label">{isPersonal ? "Your Name" : "Business Name"}</label>
          <input className="text-input" value={form.name} onChange={e=>set("name", e.target.value)}
            placeholder={isPersonal ? "e.g. Priya Sharma" : "e.g. Northbound Coffee Co."} />

          <label className="field-label">{isPersonal ? "Your Area of Expertise" : "Industry / What You Sell"}</label>
          <input className="text-input" value={form.industry} onChange={e=>set("industry", e.target.value)}
            placeholder={isPersonal ? "e.g. Career coaching for early-career engineers" : "e.g. Handmade ceramic homeware"} />

          <label className="field-label">Target Audience</label>
          <input className="text-input" value={form.audience} onChange={e=>set("audience", e.target.value)}
            placeholder="Who are you trying to reach? Be specific." />

          <label className="field-label">{isPersonal ? "Budget (time or money you can invest)" : "Monthly Marketing Budget"}</label>
          <input className="text-input" value={form.budget} onChange={e=>set("budget", e.target.value)}
            placeholder="e.g. $500/month or 5 hours/week" />

          <label className="field-label">{isPersonal ? "People in your space you admire" : "Competitors"}</label>
          <input className="text-input" value={form.competitors} onChange={e=>set("competitors", e.target.value)}
            placeholder={isPersonal ? "Who's doing this well already?" : "Who else is competing for this audience?"} />

          <label className="field-label">{isPersonal ? "Your Biggest Challenge Right Now" : "Marketing Challenge"}</label>
          <textarea className="text-input" rows="2" value={form.challenge} onChange={e=>set("challenge", e.target.value)}
            placeholder="What's the obstacle you're trying to solve?" />
        </div>
      )}

      <WhyBox>
        Every strategy decision — platform, content, budget — flows from clearly understanding
        {isPersonal ? " who you are and who you're trying to reach." : " the audience and the problem you're solving for them."}
        Skip this step and you're just guessing.
      </WhyBox>

      <ClaudeCard prompt={
        isPersonal
        ? `I'm building a personal brand around my expertise in [your niche]. Help me clarify: who is my ideal audience, what makes my perspective different from others in this space, and what's the one problem I want to be known for solving?`
        : `I run a [type of business] targeting [audience]. Help me sharpen my understanding of this audience's needs, and identify the real marketing challenge behind the surface-level problem of "${form.challenge || 'low awareness or low conversion'}".`
      } />

      <div className="btn-row">
        <button className="btn" disabled={!canContinue} onClick={handleContinue}>Continue to Platform Strategy →</button>
      </div>
    </div>
  );
}

function PlatformStrategy({brand, onComplete}){
  const [selected, setSelected] = useState([]);
  const list = brand.mode==="personal" ? PLATFORM_LIBRARY.personal : PLATFORM_LIBRARY.business;

  const toggle = (id) => {
    setSelected(s => s.includes(id) ? s.filter(x=>x!==id) : [...s, id]);
  };

  return (
    <div className="card fade-in">
      <h2>Choose Your Platforms</h2>
      <p className="sub">
        Not every platform deserves your effort. A strategist picks channels based on where the
        audience already spends attention — not personal preference. Select the platforms
        you'd actually invest in for {brand.name || "this brand"}.
      </p>

      {list.map(p=>(
        <div key={p.id} className={"platform-card " + (selected.includes(p.id) ? "selected":"")} onClick={()=>toggle(p.id)}>
          <div className="check">{selected.includes(p.id) ? "✓" : ""}</div>
          <div>
            <div className="platform-name">
              {p.name}
              <span className={"platform-fit " + (p.strong ? "fit-strong":"fit-weak")}>
                {p.strong ? "Strong Fit" : "Weaker Fit"}
              </span>
            </div>
            <div className="platform-reason">
              {p.strong ? p.reasonStrong : p.reasonWeak}
            </div>
          </div>
        </div>
      ))}

      <WhyBox>
        {brand.mode==="personal"
          ? "Personal brands grow fastest where credibility compounds — LinkedIn, X, YouTube, and newsletters let expertise build over time, instead of chasing fleeting reach."
          : "Being everywhere with no strategy is worse than being excellent on two platforms. Every platform you add multiplies the effort required to stay consistent."}
      </WhyBox>

      <ClaudeCard prompt={
        brand.mode==="personal"
        ? `I'm building a personal brand in [your niche] as [Your Name]. Based on my goals of [thought leadership / audience growth / job opportunities], which 2-3 platforms should I focus on first, and why?`
        : `I run a [type of business] targeting [audience] with a budget of [amount]. Which social platforms should I prioritize, and why would you rule out the others given this budget and audience?`
      } />

      <div className="btn-row">
        <button className="btn" disabled={selected.length===0} onClick={()=>onComplete(selected.map(id=>list.find(p=>p.id===id)))}>
          Continue to Content Pillars →
        </button>
      </div>
    </div>
  );
}

function ContentPillars({brand, onComplete}){
  const [selected, setSelected] = useState([]);
  const list = brand.mode==="personal" ? PILLARS_LIBRARY.personal : PILLARS_LIBRARY.business;

  const toggle = (id) => {
    setSelected(s=>{
      if(s.includes(id)) return s.filter(x=>x!==id);
      if(s.length>=3) return s;
      return [...s, id];
    });
  };

  return (
    <div className="card fade-in">
      <h2>Pick Your Content Pillars</h2>
      <p className="sub">
        Content pillars are the recurring themes that give a content plan structure and purpose —
        instead of posting randomly, every piece of content serves one clear goal.
      </p>
      <div className="pillar-count">Selected: <b>{selected.length} / 3</b></div>

      <div className="grid">
        {list.map(p=>(
          <div key={p.id} className={"pillar-card " + (selected.includes(p.id)?"selected":"")} onClick={()=>toggle(p.id)}>
            <h3>{p.name}</h3>
            <p>{p.desc}</p>
          </div>
        ))}
      </div>

      <WhyBox>
        Three pillars is a deliberate constraint. Too few and content gets repetitive; too many
        and there's no clear identity. {brand.mode==="personal"
          ? "Most strong personal brands are remembered for one core idea, told through 2-3 recurring angles."
          : "Strategists limit pillars so the audience can quickly learn what to expect — and what to expect is what builds a habit of following."}
      </WhyBox>

      <ClaudeCard prompt={
        brand.mode==="personal"
        ? `As [Your Name], an expert in [your niche], help me choose 3 content pillars from this list: Thought Leadership, Personal Story, Behind the Scenes, Audience Education. Which 3 best support my goal of [building authority / growing an audience / attracting clients]?`
        : `For my [type of business] targeting [audience], help me choose the best 3 content pillars from a mix of Product Education, Social Proof, Behind the Scenes, Entertainment, Community, and Promotions. Explain the tradeoffs of my choice.`
      } />

      <div className="btn-row">
        <button className="btn" disabled={selected.length!==3} onClick={()=>onComplete(selected.map(id=>list.find(p=>p.id===id)))}>
          Continue to 30-Day Roadmap →
        </button>
      </div>
    </div>
  );
}

function Roadmap({brand, pillars, onComplete}){
  const isPersonal = brand.mode==="personal";

  const weeks = isPersonal ? [
    {label:"Week 1", title:"Define Your POV & Optimize Your Profile", desc:"Before posting content, nail down what you want to be known for. Rewrite your bio, headline, and profile links so a stranger understands your expertise in five seconds."},
    {label:"Week 2", title:`Establish ${pillars[0]?.name || "Your Core Pillar"}`, desc:`Start publishing consistently around your strongest pillar to establish a clear pattern for new followers.`},
    {label:"Week 3", title:`Introduce ${pillars[1]?.name || "a Second Pillar"}`, desc:`Layer in a second content theme to add depth and keep existing followers engaged without repeating yourself.`},
    {label:"Week 4", title:`Add ${pillars[2]?.name || "a Third Pillar"} & Review`, desc:`Round out the rotation with your third pillar, then review what resonated most before planning month two.`},
  ] : [
    {label:"Week 1", title:"Foundation & Audience Research", desc:"Set up profiles properly, study where the audience already gathers, and establish a consistent visual and voice identity."},
    {label:"Week 2", title:`Launch ${pillars[0]?.name || "Core Pillar"}`, desc:`Begin regular posting around the strongest content pillar to establish presence and start building an audience habit.`},
    {label:"Week 3", title:`Layer in ${pillars[1]?.name || "Second Pillar"}`, desc:`Introduce a second content theme to build trust and depth, while tracking which formats get the most engagement.`},
    {label:"Week 4", title:`Add ${pillars[2]?.name || "Third Pillar"} & Optimize`, desc:`Round out the mix, then use the first month's data to double down on what's working going into month two.`},
  ];

  return (
    <div className="card fade-in">
      <h2>30-Day Content Roadmap</h2>
      <p className="sub">
        This is a strategy, not a posting calendar — weekly goals that build on each other,
        rather than a list of individual posts.
      </p>

      {weeks.map(w=>(
        <div key={w.label} className="week-card">
          <div className="wk-label">{w.label}</div>
          <h4>{w.title}</h4>
          <p>{w.desc}</p>
        </div>
      ))}

      <WhyBox>
        Growth compounds when structure comes before volume. Jumping straight to daily posting
        without a clear sequence usually produces content with no throughline — {isPersonal
          ? "and for a personal brand, an unclear throughline is the fastest way to be forgotten."
          : "and for a business, that inconsistency is what makes an audience lose trust."}
      </WhyBox>

      <ClaudeCard prompt={
        isPersonal
        ? `Help me build a 30-day content roadmap for my personal brand as [Your Name] in [your niche], using these 3 pillars: ${pillars.map(p=>p.name).join(", ")}. Structure it by weekly goals, not individual posts, starting with defining my POV and optimizing my profile.`
        : `Help me build a 30-day content roadmap for [business name] using these 3 content pillars: ${pillars.map(p=>p.name).join(", ")}. Structure it by weekly strategic goals, not individual posts.`
      } />

      <div className="btn-row">
        <button className="btn" onClick={onComplete}>Continue to the Unexpected Event →</button>
      </div>
    </div>
  );
}

function UnexpectedEvent({brand, onComplete}){
  const [event] = useState(()=> rand(brand.mode==="personal" ? EVENTS_PERSONAL : EVENTS_BUSINESS));
  const [choice, setChoice] = useState(null);
  const options = RESPONSE_OPTIONS[brand.mode==="personal" ? "personal" : "business"];

  return (
    <div className="card fade-in">
      <h2>An Unexpected Event Just Happened</h2>
      <p className="sub">Real strategy isn't just planning — it's how you respond when the plan meets reality.</p>

      <div className="event-box">
        <div className="tag">{event.tag}</div>
        <p>{event.text}</p>
      </div>

      <div className="grid">
        {options.map(opt=>(
          <div key={opt.id} className={"option " + (choice?.id===opt.id ? "selected":"")} onClick={()=>setChoice(opt)}>
            <h3>{opt.label}</h3>
          </div>
        ))}
      </div>

      {choice && (
        <div className="consequence">
          <b style={{color:"var(--teal)"}}>Likely consequence:</b> {choice.consequence}
        </div>
      )}

      <WhyBox>
        Every response has a tradeoff — there's rarely a purely "correct" answer. A good strategist
        weighs momentum against consistency, and speed against risk, every time.
      </WhyBox>

      <ClaudeCard prompt={
        brand.mode==="personal"
        ? `Something unexpected just happened to my personal brand: "${event.text}" As [Your Name], how should I respond in a way that stays authentic to my niche in [your niche] and doesn't damage long-term trust?`
        : `Something unexpected just happened to my business: "${event.text}" What are the tradeoffs of reacting quickly versus staying disciplined on our existing marketing plan?`
      } />

      <div className="btn-row">
        <button className="btn" disabled={!choice} onClick={()=>onComplete(event, choice)}>See Your Growth Report →</button>
      </div>
    </div>
  );
}

function GrowthReport({brand, platforms, pillars, event, choice, onRestart}){
  const isPersonal = brand.mode==="personal";
  const strongPlatforms = platforms.filter(p=>p.strong).length;

  const growthPotential = strongPlatforms >= 2
    ? "High — the platform mix leans into where the audience already pays attention."
    : "Moderate — consider shifting effort toward platforms with a stronger natural fit.";

  const bestDecision = pillars[0]
    ? `Choosing "${pillars[0].name}" as a lead pillar gives the content a clear, recognizable identity from day one.`
    : "Selecting focused content pillars instead of posting without a plan.";

  const biggestMistake = choice?.id === "go_quiet"
    ? "Staying silent during a moment of real attention risks looking indifferent right when people were paying closest attention."
    : choice?.id === "lean_in"
    ? "Reallocating heavily toward one moment risks pulling focus and budget away from the long-term strategy that was already working."
    : "Playing it too safe during a real inflection point can mean missing a rare window of attention.";

  const lessons = isPersonal ? [
    "Authenticity beats polish — audiences follow people, not performances.",
    "Consistency compounds — a clear, recognizable rhythm builds trust faster than occasional brilliance.",
    "Niche clarity attracts the right audience — trying to appeal to everyone dilutes who remembers you at all.",
  ] : [
    "Strategy comes before content — knowing who you're talking to changes everything you make.",
    "Fewer, sharper channels outperform being everywhere at once.",
    "Trust is built in layers — education and proof have to come before you ask people to buy.",
  ];

  return (
    <div className="card fade-in">
      <h2>Growth Report</h2>
      <p className="sub">Here's how the strategy for {brand.name || "this brand"} came together.</p>

      <div className="report-grid">
        <div className="report-item">
          <span className="label">Audience Understanding</span>
          <p>{brand.audience || "Audience defined through the setup stage."}</p>
        </div>
        <div className="report-item">
          <span className="label">Platform Strategy</span>
          <p>{platforms.map(p=>p.name).join(", ")} — chosen based on natural audience fit rather than habit.</p>
        </div>
        <div className="report-item">
          <span className="label">Content Strategy</span>
          <p>Built around {pillars.map(p=>p.name).join(", ")}, giving the content a clear and repeatable identity.</p>
        </div>
        <div className="report-item">
          <span className="label">Growth Potential</span>
          <p>{growthPotential}</p>
        </div>
        <div className="report-item">
          <span className="label">Best Decision</span>
          <p>{bestDecision}</p>
        </div>
        <div className="report-item">
          <span className="label">Biggest Mistake to Watch</span>
          <p>{biggestMistake}</p>
        </div>
      </div>

      <h2 style={{marginTop:26}}>Three Marketing Lessons</h2>
      {lessons.map((l,i)=>(
        <div key={i} className="lesson"><span className="n">{i+1}.</span><span>{l}</span></div>
      ))}

      <WhyBox>
        Strategy isn't a document you write once — it's a set of decisions you keep revisiting as
        reality changes. Every choice you made here is one a real strategist makes weekly.
      </WhyBox>

      <ClaudeCard prompt={
        isPersonal
        ? `Summarize a personal branding strategy for [Your Name] in [your niche], covering audience understanding, platform choice, content pillars, and one lesson about authenticity, consistency, or niche clarity I should apply going forward.`
        : `Summarize a marketing strategy for [business name], covering audience understanding, platform choice, content pillars, and one key lesson about building trust before asking for a sale.`
      } />

      <div className="btn-row">
        <button className="btn teal" onClick={onRestart}>Start a New Brand →</button>
      </div>
    </div>
  );
}

/* ---------------- APP ---------------- */

function App(){
  const [stage, setStage] = useState(0); // 0 welcome, 1 setup, 2 platforms, 3 pillars, 4 roadmap, 5 event, 6 report
  const [brand, setBrand] = useState(null);
  const [platforms, setPlatforms] = useState([]);
  const [pillars, setPillars] = useState([]);
  const [eventData, setEventData] = useState(null);
  const [choiceData, setChoiceData] = useState(null);

  const stages = ["Welcome","Brand","Platforms","Pillars","Roadmap","Event","Report"];

  const restart = () => {
    setStage(0); setBrand(null); setPlatforms([]); setPillars([]); setEventData(null); setChoiceData(null);
  };

  return (
    <div className="app-shell">
      {stage > 0 && (
        <div className="brand-header fade-in">
          <div>
            <span className="eyebrow">{brand?.mode === "personal" ? "Personal Brand" : brand?.mode === "random" ? "New Client" : "Business"}</span>
            <h1>{brand?.name || "Untitled Brand"}</h1>
          </div>
          <span className="badge">{brand?.industry}</span>
        </div>
      )}
      {stage > 0 && <ProgressTabs stage={stage} stages={stages} />}

      {stage === 0 && <Welcome onSelectMode={(mode)=>{ setBrand({mode}); setStage(1); }} />}

      {stage === 1 && brand && (
        <BusinessSetup mode={brand.mode} onComplete={(data)=>{ setBrand(data); setStage(2); }} />
      )}

      {stage === 2 && brand && (
        <PlatformStrategy brand={brand} onComplete={(p)=>{ setPlatforms(p); setStage(3); }} />
      )}

      {stage === 3 && brand && (
        <ContentPillars brand={brand} onComplete={(p)=>{ setPillars(p); setStage(4); }} />
      )}

      {stage === 4 && brand && (
        <Roadmap brand={brand} pillars={pillars} onComplete={()=>setStage(5)} />
      )}

      {stage === 5 && brand && (
        <UnexpectedEvent brand={brand} onComplete={(ev, ch)=>{ setEventData(ev); setChoiceData(ch); setStage(6); }} />
      )}

      {stage === 6 && brand && (
        <GrowthReport brand={brand} platforms={platforms} pillars={pillars} event={eventData} choice={choiceData} onRestart={restart} />
      )}
    </div>
  );
}

ReactDOM.createRoot(document.getElementById("root")).render(<App/>);
</script>
</body>
</html>

