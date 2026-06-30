# Today I builta Supply Chain Optimizer using claude :

## Key Learnings :
- Learned how supply chain optimization involves balancing cost, delivery speed, inventory levels, and customer satisfaction rather than optimizing a single metric.
- Understood that supplier selection depends on multiple factors such as cost, reliability, lead time, and risk instead of price alone.
- Explored how inventory planning affects stock availability, holding costs, and production continuity.
- Learned the importance of demand forecasting in preventing both stock shortages and excess inventory.
- Understood how warehouse and distribution center allocation directly impacts transportation costs and delivery performance.
- Learned how transportation choices involve trade-offs between cost, transit time, and service reliability.
- Explored how disruptions such as supplier delays, demand spikes, and logistics failures require adaptive decision-making.
- Learned to model supply chain decisions using KPIs and scoring systems to evaluate operational performance.
- Improved my ability to convert complex business workflows into an interactive simulation using AI-assisted development.
- Learned how effective prompt engineering can generate structured dashboards, business logic, and decision workflows with minimal manual coding.

### Output Screenshots :

<img width="1920" height="1080" alt="Screenshot (471)" src="https://github.com/user-attachments/assets/fca6ba6c-ac8b-4ca3-8abd-b57ff879c055" />
<img width="1920" height="1080" alt="Screenshot (470)" src="https://github.com/user-attachments/assets/577f9f20-2abf-4514-adeb-101fd77204d5" />
<img width="1920" height="1080" alt="Screenshot (469)" src="https://github.com/user-attachments/assets/d77fd532-b248-41ec-aea3-2bd19aba50c7" />
<img width="1920" height="1080" alt="Screenshot (468)" src="https://github.com/user-attachments/assets/64321139-5b90-4dad-905d-819d165650f4" />
<img width="1920" height="1080" alt="Screenshot (467)" src="https://github.com/user-attachments/assets/e79fae2e-a26f-420d-bb9e-b433a5fd02a7" />
<img width="1920" height="1080" alt="Screenshot (466)" src="https://github.com/user-attachments/assets/822389c2-c8a8-414d-adb1-acae832c40eb" />
<img width="1920" height="1080" alt="Screenshot (465)" src="https://github.com/user-attachments/assets/f0068b33-6d71-4a87-9ef2-79a48cdf9432" />
<img width="1920" height="1080" alt="Screenshot (464)" src="https://github.com/user-attachments/assets/53e61a4c-6fdd-4a57-bda0-54176a014608" />

#### HTML File :

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Supply Chain Builder</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/react/18.2.0/umd/react.production.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/react-dom/18.2.0/umd/react-dom.production.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/7.23.2/babel.min.js"></script>
<style>
  *{margin:0;padding:0;box-sizing:border-box}
  :root{
    --bg:#0d1117;--surface:#161b22;--card:#1c2333;--card2:#21283b;
    --border:#30363d;--border2:#3d444d;
    --text:#e6edf3;--muted:#7d8590;--subtle:#4d5566;
    --accent:#58a6ff;--accent2:#1f6feb;--accentbg:#0d2137;
    --green:#3fb950;--greenbg:#0d2818;
    --amber:#d29922;--amberbg:#1d1b0d;
    --red:#f85149;--redbg:#270d0d;
    --purple:#bc8cff;--purplebg:#1a0d2e;
    --teal:#39d353;--radius:12px;--radiusS:8px;
  }
  body{background:var(--bg);color:var(--text);font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;min-height:100vh;line-height:1.6}
  #root{min-height:100vh}

  .app{max-width:1100px;margin:0 auto;padding:24px 16px}

  /* Cards */
  .card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);padding:24px;transition:border-color .2s}
  .card:hover{border-color:var(--border2)}
  .card2{background:var(--card2);border:1px solid var(--border);border-radius:var(--radiusS);padding:16px}

  /* Buttons */
  .btn{display:inline-flex;align-items:center;gap:8px;padding:10px 20px;border-radius:var(--radiusS);border:none;cursor:pointer;font-size:14px;font-weight:500;transition:all .15s;text-decoration:none}
  .btn-primary{background:var(--accent2);color:#fff}
  .btn-primary:hover{background:#388bfd;transform:translateY(-1px)}
  .btn-secondary{background:transparent;color:var(--text);border:1px solid var(--border2)}
  .btn-secondary:hover{background:var(--card2);border-color:var(--accent)}
  .btn-lg{padding:14px 28px;font-size:16px;border-radius:var(--radius)}
  .btn-ghost{background:transparent;color:var(--muted);border:1px solid var(--border)}
  .btn-ghost:hover{color:var(--text);border-color:var(--border2)}

  /* Choice cards */
  .choice{background:var(--card2);border:2px solid var(--border);border-radius:var(--radius);padding:20px;cursor:pointer;transition:all .2s;text-align:left;width:100%}
  .choice:hover{border-color:var(--accent2);background:#1a2234;transform:translateY(-2px)}
  .choice.selected{border-color:var(--accent);background:var(--accentbg)}
  .choices-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px;margin-top:16px}

  /* Progress bar */
  .progress-track{height:8px;background:var(--card2);border-radius:4px;overflow:hidden}
  .progress-fill{height:100%;border-radius:4px;transition:width .6s cubic-bezier(.34,1.56,.64,1)}

  /* Metric bar */
  .metric-bar-track{height:10px;background:var(--card2);border-radius:5px;overflow:hidden;flex:1}
  .metric-bar-fill{height:100%;border-radius:5px;transition:width .7s cubic-bezier(.34,1.56,.64,1)}

  /* Score ring */
  .score-ring{position:relative;width:160px;height:160px;margin:0 auto}
  .score-ring svg{transform:rotate(-90deg)}
  .score-val{position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);text-align:center}

  /* Tags */
  .tag{display:inline-flex;align-items:center;gap:4px;padding:4px 10px;border-radius:20px;font-size:12px;font-weight:500}
  .tag-green{background:var(--greenbg);color:var(--green)}
  .tag-amber{background:var(--amberbg);color:var(--amber)}
  .tag-red{background:var(--redbg);color:var(--red)}
  .tag-blue{background:var(--accentbg);color:var(--accent)}
  .tag-purple{background:var(--purplebg);color:var(--purple)}

  /* Tradeoff box */
  .tradeoff{border-radius:var(--radiusS);padding:16px;margin-top:16px;border-left:3px solid}
  .tradeoff-info{background:var(--accentbg);border-color:var(--accent)}
  .tradeoff-warn{background:var(--amberbg);border-color:var(--amber)}
  .tradeoff-good{background:var(--greenbg);border-color:var(--green)}

  /* Metric cards grid */
  .metrics-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:12px}

  /* Explanation box */
  .explain-box{background:var(--card2);border:1px solid var(--border);border-radius:var(--radiusS);padding:20px;margin-bottom:20px}
  .explain-title{font-size:11px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;color:var(--accent);margin-bottom:8px}

  /* Dashboard */
  .dash-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px}
  @media(max-width:600px){.dash-grid{grid-template-columns:1fr}}

  /* Step nav */
  .steps{display:flex;gap:0;margin-bottom:32px;overflow:hidden;border-radius:var(--radiusS);border:1px solid var(--border)}
  .step{flex:1;padding:10px 4px;text-align:center;font-size:12px;background:var(--card);color:var(--muted);position:relative;transition:all .2s}
  .step.active{background:var(--accentbg);color:var(--accent)}
  .step.done{background:var(--greenbg);color:var(--green)}

  /* Welcome */
  .welcome-hero{text-align:center;padding:40px 20px}
  .logo{font-size:40px;margin-bottom:16px}
  h1{font-size:32px;font-weight:700;background:linear-gradient(135deg,var(--accent),var(--purple));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
  h2{font-size:22px;font-weight:600;color:var(--text)}
  h3{font-size:16px;font-weight:600;color:var(--text)}

  /* Company badge */
  .company-badge{display:flex;align-items:center;gap:16px;background:var(--card2);border:1px solid var(--border2);border-radius:var(--radius);padding:16px 20px;margin-bottom:24px}
  .company-icon{width:48px;height:48px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:24px;flex-shrink:0}

  /* Pulse animation */
  @keyframes pulse{0%,100%{opacity:1}50%{opacity:.5}}
  .pulse{animation:pulse 2s infinite}

  /* Fade in */
  @keyframes fadeIn{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
  .fade-in{animation:fadeIn .35s ease both}

  /* Strength/weakness items */
  .sw-item{display:flex;align-items:flex-start;gap:10px;padding:10px 0;border-bottom:1px solid var(--border)}
  .sw-item:last-child{border-bottom:none}
  .sw-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;margin-top:6px}

  /* Overall score color */
  .score-excellent{color:#3fb950}
  .score-good{color:#58a6ff}
  .score-average{color:#d29922}
  .score-poor{color:#f85149}

  /* Tooltip-like tradeoff section */
  .effect-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:12px}
  @media(max-width:480px){.effect-grid{grid-template-columns:1fr}}

  .scrollable{max-height:80vh;overflow-y:auto}
  ::-webkit-scrollbar{width:6px}
  ::-webkit-scrollbar-track{background:var(--bg)}
  ::-webkit-scrollbar-thumb{background:var(--subtle);border-radius:3px}
</style>
</head>
<body>
<div id="root"></div>
<script type="text/babel">
const {useState,useEffect,useCallback}=React;

// ── Data ──────────────────────────────────────────────────────────────────────

const INDUSTRIES=[
  {name:"Consumer Electronics",icon:"📱",products:["smartphones","tablets","laptops"],margin:"high"},
  {name:"Fashion & Apparel",icon:"👗",products:["clothing","footwear","accessories"],margin:"medium"},
  {name:"Food & Beverage",icon:"🍫",products:["packaged snacks","beverages","frozen meals"],margin:"low"},
  {name:"Pharmaceuticals",icon:"💊",products:["vitamins","OTC medicine","supplements"],margin:"high"},
  {name:"Automotive Parts",icon:"🚗",products:["spare parts","accessories","filters"],margin:"medium"},
  {name:"Home Appliances",icon:"🏠",products:["blenders","air purifiers","coffee makers"],margin:"medium"},
  {name:"Sporting Goods",icon:"⚽",products:["gym equipment","outdoor gear","team sports"],margin:"medium"},
  {name:"Cosmetics",icon:"💄",products:["skincare","makeup","fragrances"],margin:"high"},
];
const COUNTRIES_SERVED=[
  ["USA","UK","Germany"],["India","China","Brazil"],["Japan","Australia","Canada"],
  ["France","Mexico","South Korea"],["UAE","Singapore","Netherlands"],
];
const DEMAND_LEVELS=[
  {level:"High",desc:"Customers want large volumes quickly",icon:"🔥"},
  {level:"Medium",desc:"Steady orders with occasional spikes",icon:"📊"},
  {level:"Low",desc:"Niche market, smaller order volumes",icon:"🌱"},
];
const FACTORY_LOCATIONS=[
  {id:"china",label:"China",desc:"World's largest manufacturing hub",cost:-20,speed:-5,risk:15,sustainability:-10,note:"Lowest cost but furthest from most Western markets. Political tensions can disrupt trade."},
  {id:"vietnam",label:"Vietnam",desc:"Fast-growing low-cost alternative",cost:-15,speed:-5,risk:10,sustainability:-8,note:"Growing alternative to China with competitive wages and improving infrastructure."},
  {id:"mexico",label:"Mexico",desc:"Close to North American markets",cost:-8,speed:10,risk:5,sustainability:0,note:"Nearshoring to Mexico cuts shipping time to the USA dramatically — ideal if North America is your key market."},
  {id:"germany",label:"Germany",desc:"Premium engineering and quality",cost:10,speed:5,risk:-5,sustainability:8,note:"Higher wages but exceptional quality and reliability. Great for premium products."},
  {id:"india",label:"India",desc:"Large skilled workforce, growing hub",cost:-12,speed:0,risk:8,sustainability:-5,note:"Massive skilled labor pool and improving logistics. Particularly strong for pharmaceuticals and IT."},
];
const TRANSPORT_METHODS=[
  {id:"sea",label:"Sea Freight",desc:"Ships carry bulk cargo across oceans",cost:-18,speed:-20,risk:8,sustainability:5,sat:-10,note:"Cheapest for bulk goods but slowest (4–6 weeks). Great for non-urgent, heavy shipments."},
  {id:"air",label:"Air Freight",desc:"Fastest delivery worldwide",cost:25,speed:25,risk:-5,sustainability:-20,sat:20,note:"5–10× more expensive than sea. Justified only for high-value, time-sensitive, or lightweight goods."},
  {id:"rail",label:"Rail Freight",desc:"Efficient overland transport",cost:-5,speed:5,risk:3,sustainability:10,sat:5,note:"A great middle ground for continental distances — faster than sea, greener than trucks."},
  {id:"road",label:"Road (Trucks)",desc:"Flexible door-to-door delivery",cost:5,speed:10,risk:0,sustainability:-8,sat:10,note:"Essential for last-mile delivery. Very flexible but adds to congestion and emissions."},
];
const INVENTORY_STRATEGIES=[
  {id:"low",label:"Lean Inventory",desc:"Just-in-time — keep as little stock as possible",cost:15,speed:-10,risk:20,sustainability:5,sat:-15,note:"You only order what you need, when you need it. Saves warehouse costs but a single delay can empty your shelves."},
  {id:"balanced",label:"Balanced Stock",desc:"A moderate safety buffer of stock",cost:0,speed:5,risk:0,sustainability:0,sat:5,note:"A practical middle ground: enough buffer to handle small disruptions without tying up too much cash."},
  {id:"high",label:"Safety Stock",desc:"Large buffer to never run out",cost:-15,speed:10,risk:-15,sustainability:-8,sat:15,note:"Always available for customers. Costs more in warehousing and ties up cash, but customers love the reliability."},
];
const SUPPLIER_STRATEGIES=[
  {id:"single",label:"Single Supplier",desc:"All eggs in one basket — one trusted partner",cost:10,speed:5,risk:25,sustainability:0,sat:5,note:"Lower prices through volume deals but one disruption (strike, disaster, bankruptcy) halts your entire operation."},
  {id:"dual",label:"Dual Sourcing",desc:"Two suppliers for critical components",cost:0,speed:3,risk:5,sustainability:0,sat:5,note:"Popular choice: a primary supplier for price efficiency and a backup ready if anything goes wrong."},
  {id:"multi",label:"Multi-Supplier",desc:"Several suppliers compete for your business",cost:-8,speed:-5,risk:-15,sustainability:3,sat:3,note:"Maximum resilience. You'll likely pay slightly more per unit but no single disruption can stop you."},
];
const WAREHOUSE_STRATEGIES=[
  {id:"central",label:"Central Warehouse",desc:"One large hub that serves all markets",cost:15,speed:-15,risk:8,sustainability:5,sat:-10,note:"Simple to manage and cheap to run, but customers far from the hub wait longer for deliveries."},
  {id:"regional",label:"Regional Hubs",desc:"Multiple warehouses near key markets",cost:-10,speed:15,risk:-5,sustainability:-5,sat:15,note:"Stock is already close to customers. Faster delivery but more expensive to operate."},
  {id:"3pl",label:"3PL Partner",desc:"Outsource warehousing to a specialist",cost:-5,speed:10,risk:3,sustainability:0,sat:10,note:"Third-Party Logistics (3PL) firms like DHL or FedEx handle storage and distribution. You pay fees but gain their global network."},
];

const STEPS=["Welcome","Company","Suppliers","Factory","Warehouse","Transport","Inventory","Results"];

// ── Utility ───────────────────────────────────────────────────────────────────
function randItem(arr){return arr[Math.floor(Math.random()*arr.length)]}
function clamp(v,lo,hi){return Math.max(lo,Math.min(hi,v))}

function generateCompany(){
  const ind=randItem(INDUSTRIES);
  const prod=randItem(ind.products);
  const countries=randItem(COUNTRIES_SERVED);
  const demand=randItem(DEMAND_LEVELS);
  return{industry:ind.name,icon:ind.icon,product:prod,countries,demand:demand.level,demandDesc:demand.desc,demandIcon:demand.icon,margin:ind.margin};
}

function computeMetrics(choices){
  const base={cost:50,speed:50,risk:50,satisfaction:50,sustainability:50};
  const apply=(src,obj)=>{
    if(!obj)return;
    if(obj.cost!==undefined){base.cost=clamp(base.cost+obj.cost,5,100)}
    if(obj.speed!==undefined){base.speed=clamp(base.speed+obj.speed,5,100)}
    if(obj.risk!==undefined){base.risk=clamp(base.risk+obj.risk,5,100)}
    if(obj.sustainability!==undefined){base.sustainability=clamp(base.sustainability+obj.sustainability,5,100)}
    if(obj.sat!==undefined){base.satisfaction=clamp(base.satisfaction+obj.sat,5,100)}
  };
  [choices.supplier,choices.factory,choices.warehouse,choices.transport,choices.inventory].forEach(id=>{
    if(!id)return;
    const found=[...SUPPLIER_STRATEGIES,...FACTORY_LOCATIONS,...WAREHOUSE_STRATEGIES,...TRANSPORT_METHODS,...INVENTORY_STRATEGIES].find(x=>x.id===id);
    if(found)apply(id,found);
  });
  return base;
}

function overallScore(metrics){
  const{cost,speed,risk,satisfaction,sustainability}=metrics;
  // Risk is bad, so invert it
  return Math.round((cost*.2+speed*.25+(100-risk)*.25+satisfaction*.2+sustainability*.1));
}

function scoreLabel(s){
  if(s>=80)return{label:"Excellent",cls:"score-excellent",color:"#3fb950"};
  if(s>=65)return{label:"Good",cls:"score-good",color:"#58a6ff"};
  if(s>=45)return{label:"Average",cls:"score-average",color:"#d29922"};
  return{label:"Needs Work",cls:"score-poor",color:"#f85149"};
}

function generateInsights(choices,metrics,company){
  const strengths=[],weaknesses=[],improvements=[];
  const sup=SUPPLIER_STRATEGIES.find(x=>x.id===choices.supplier);
  const fac=FACTORY_LOCATIONS.find(x=>x.id===choices.factory);
  const war=WAREHOUSE_STRATEGIES.find(x=>x.id===choices.warehouse);
  const tra=TRANSPORT_METHODS.find(x=>x.id===choices.transport);
  const inv=INVENTORY_STRATEGIES.find(x=>x.id===choices.inventory);

  if(metrics.cost>=60)strengths.push("Cost-efficient supply chain preserves margins");
  if(metrics.speed>=60)strengths.push("Fast delivery builds strong customer loyalty");
  if(metrics.risk<=40)strengths.push("Well-diversified, resilient to disruptions");
  if(metrics.satisfaction>=65)strengths.push("High customer satisfaction drives repeat business");
  if(metrics.sustainability>=60)strengths.push("Strong sustainability credentials attract ESG-conscious buyers");

  if(metrics.cost<40)weaknesses.push("High costs may squeeze profit margins significantly");
  if(metrics.speed<40)weaknesses.push("Slow delivery risks losing impatient customers to competitors");
  if(metrics.risk>65)weaknesses.push("Single points of failure could halt operations");
  if(metrics.satisfaction<40)weaknesses.push("Low customer satisfaction threatens retention and reviews");
  if(metrics.sustainability<35)weaknesses.push("Poor sustainability profile may trigger regulatory scrutiny");

  if(strengths.length===0)strengths.push("Building experience — every playthrough teaches new lessons");

  if(choices.supplier==="single")improvements.push("Add a second supplier as backup — even a 20% capacity agreement prevents catastrophic stockouts");
  if(choices.transport==="air"&&company.margin!=="high")improvements.push("Switch bulk orders to sea freight and reserve air for urgent top-ups to cut transport costs");
  if(choices.inventory==="low")improvements.push("Increase safety stock to 2–4 weeks — the warehouse cost is usually less than a lost-sale");
  if(choices.warehouse==="central"&&metrics.speed<50)improvements.push("Add one regional hub near your highest-volume market to halve delivery times there");
  if(choices.factory==="china"&&metrics.risk>60)improvements.push("Qualify a nearshore factory in Mexico or Vietnam to reduce geopolitical concentration risk");

  while(improvements.length<3){
    const generic=[
      "Invest in demand forecasting software to reduce inventory waste by 15–30%",
      "Negotiate longer payment terms with suppliers to free up working capital",
      "Implement real-time shipment tracking to proactively catch delays",
      "Consider vertical integration of your most critical component",
      "Build supplier scorecards to drive continuous quality improvement",
    ];
    const pick=generic[improvements.length%generic.length];
    if(!improvements.includes(pick))improvements.push(pick);
    else break;
  }

  let bigRisk="Unknown";
  if(metrics.risk>=70)bigRisk=`Heavy reliance on ${sup?.label||"single supplier"} creates a critical vulnerability`;
  else if(metrics.speed<35)bigRisk="Slow delivery speed may trigger customer churn as competitors offer faster service";
  else if(metrics.cost<30)bigRisk="Cost structure is unsustainable — margins may not survive a pricing war";
  else if(metrics.sustainability<30)bigRisk="Regulatory carbon/ESG requirements could force costly supply chain restructuring";
  else bigRisk="Overall risk is manageable — focus on continuous improvement";

  return{strengths,weaknesses,improvements,bigRisk};
}

// ── Sub-components ────────────────────────────────────────────────────────────

function MetricBar({label,value,color}){
  const pct=Math.round(value);
  const col=color||(value>=65?"var(--green)":value>=40?"var(--accent)":"var(--red)");
  return(
    <div style={{marginBottom:14}}>
      <div style={{display:"flex",justifyContent:"space-between",marginBottom:6}}>
        <span style={{fontSize:13,color:"var(--muted)"}}>{label}</span>
        <span style={{fontSize:13,fontWeight:600,color:col}}>{pct}</span>
      </div>
      <div className="metric-bar-track">
        <div className="metric-bar-fill" style={{width:`${pct}%`,background:col}}/>
      </div>
    </div>
  );
}

function MetricCard({label,value,icon,good}){
  const v=Math.round(value);
  const isGood=good!==undefined?good:v>=50;
  const col=isGood?"var(--green)":"var(--red)";
  return(
    <div className="card2" style={{textAlign:"center"}}>
      <div style={{fontSize:22,marginBottom:4}}>{icon}</div>
      <div style={{fontSize:11,color:"var(--muted)",marginBottom:4,textTransform:"uppercase",letterSpacing:".06em"}}>{label}</div>
      <div style={{fontSize:26,fontWeight:700,color:col}}>{v}</div>
      <div style={{fontSize:10,color:"var(--muted)"}}>/ 100</div>
    </div>
  );
}

function LiveMetrics({metrics}){
  return(
    <div className="card" style={{marginBottom:24}}>
      <h3 style={{marginBottom:16,color:"var(--muted)",fontSize:12,letterSpacing:".08em",textTransform:"uppercase"}}>Live Business Metrics</h3>
      <MetricBar label="💰 Cost Efficiency" value={metrics.cost}/>
      <MetricBar label="⚡ Delivery Speed" value={metrics.speed}/>
      <MetricBar label="🛡️ Risk Level" value={100-metrics.risk} color={metrics.risk<=35?"var(--green)":metrics.risk>=65?"var(--red)":"var(--amber)"}/>
      <MetricBar label="😊 Customer Satisfaction" value={metrics.satisfaction}/>
      <MetricBar label="🌱 Sustainability" value={metrics.sustainability}/>
    </div>
  );
}

function ChoiceCard({option,selected,onSelect}){
  return(
    <button className={`choice${selected?" selected":""}`} onClick={()=>onSelect(option.id)}>
      <div style={{fontWeight:600,fontSize:15,marginBottom:6}}>{option.label}</div>
      <div style={{fontSize:13,color:"var(--muted)",marginBottom:10}}>{option.desc}</div>
      <div style={{display:"flex",gap:6,flexWrap:"wrap"}}>
        {option.cost>0&&<span className="tag tag-green">+Cost Saving</span>}
        {option.cost<-5&&<span className="tag tag-amber">Higher Cost</span>}
        {option.speed>5&&<span className="tag tag-blue">+Faster</span>}
        {option.speed<-5&&<span className="tag tag-amber">Slower</span>}
        {option.risk>10&&<span className="tag tag-red">+Risk</span>}
        {option.risk<-5&&<span className="tag tag-green">-Risk</span>}
        {option.sustainability>5&&<span className="tag tag-green">+Eco</span>}
        {option.sustainability<-5&&<span className="tag tag-amber">-Eco</span>}
      </div>
    </button>
  );
}

function ExplainBox({title,children}){
  return(
    <div className="explain-box fade-in">
      <div className="explain-title">{title}</div>
      <div style={{fontSize:14,color:"var(--muted)",lineHeight:1.7}}>{children}</div>
    </div>
  );
}

function TradeoffBox({selected,options}){
  const obj=options.find(x=>x.id===selected);
  if(!obj)return null;
  return(
    <div className="tradeoff tradeoff-info fade-in">
      <div style={{fontWeight:600,fontSize:14,marginBottom:6,color:"var(--accent)"}}>💡 What this means for your business</div>
      <div style={{fontSize:13,color:"var(--muted)",lineHeight:1.7}}>{obj.note}</div>
    </div>
  );
}

function StepBar({currentStep}){
  const names=["Company","Suppliers","Factory","Warehouse","Transport","Inventory","Results"];
  return(
    <div className="steps" style={{marginBottom:24}}>
      {names.map((n,i)=>{
        const stepIdx=i+1;
        const cls=currentStep>stepIdx?"done":currentStep===stepIdx?"active":"";
        return<div key={n} className={`step ${cls}`}>{currentStep>stepIdx?"✓ ":""}{n}</div>;
      })}
    </div>
  );
}

// ── Screens ───────────────────────────────────────────────────────────────────

function WelcomeScreen({onStart}){
  return(
    <div className="welcome-hero fade-in">
      <div className="logo">🏭</div>
      <h1>Supply Chain Builder</h1>
      <p style={{fontSize:18,color:"var(--muted)",marginTop:12,marginBottom:32,maxWidth:600,margin:"12px auto 32px"}}>
        Every product you buy — a phone, a t-shirt, a chocolate bar — traveled through an invisible network called a <strong style={{color:"var(--text)"}}>supply chain</strong> before reaching you. In this simulation, you'll build one from scratch.
      </p>

      <div style={{display:"grid",gridTemplateColumns:"repeat(auto-fit,minmax(200px,1fr))",gap:16,maxWidth:800,margin:"0 auto 40px",textAlign:"left"}}>
        {[
          {icon:"🏭",title:"Make it",desc:"Choose where your products are manufactured and by whom"},
          {icon:"🚢",title:"Move it",desc:"Decide how goods travel across the world to reach customers"},
          {icon:"📦",title:"Store it",desc:"Pick a warehouse strategy to balance cost and speed"},
          {icon:"📊",title:"Score it",desc:"See how your decisions affect real business metrics"},
        ].map(c=>(
          <div key={c.title} className="card2" style={{padding:"20px 16px"}}>
            <div style={{fontSize:28,marginBottom:8}}>{c.icon}</div>
            <div style={{fontWeight:600,marginBottom:4}}>{c.title}</div>
            <div style={{fontSize:13,color:"var(--muted)"}}>{c.desc}</div>
          </div>
        ))}
      </div>

      <div className="card" style={{maxWidth:600,margin:"0 auto 32px",textAlign:"left"}}>
        <div style={{fontWeight:600,marginBottom:8}}>🎓 What you'll learn</div>
        <ul style={{fontSize:14,color:"var(--muted)",lineHeight:2,paddingLeft:20}}>
          <li>Why Apple makes iPhones in China but Zara makes clothes in Spain</li>
          <li>Why Amazon has thousands of small warehouses instead of one giant one</li>
          <li>Why your online order sometimes arrives in 1 day and sometimes in 3 weeks</li>
          <li>What "just-in-time" manufacturing means and why it failed during COVID</li>
        </ul>
      </div>

      <button className="btn btn-primary btn-lg" onClick={onStart}>
        Start Building ↗
      </button>
      <p style={{marginTop:12,fontSize:12,color:"var(--subtle)"}}>Takes about 5–8 minutes · No sign-up required</p>
    </div>
  );
}

function CompanyScreen({company,onNext}){
  return(
    <div className="fade-in">
      <StepBar currentStep={1}/>
      <h2 style={{marginBottom:8}}>Your Company</h2>
      <p style={{color:"var(--muted)",fontSize:14,marginBottom:24}}>You've been appointed CEO of a growing business. Here's what you're working with:</p>

      <div className="company-badge" style={{marginBottom:20}}>
        <div className="company-icon" style={{background:"var(--accentbg)"}}>
          <span>{company.icon}</span>
        </div>
        <div>
          <div style={{fontWeight:700,fontSize:18}}>{company.industry}</div>
          <div style={{color:"var(--muted)",fontSize:14}}>Main product: <strong style={{color:"var(--text)"}}>{company.product}</strong></div>
        </div>
      </div>

      <div style={{display:"grid",gridTemplateColumns:"repeat(auto-fit,minmax(200px,1fr))",gap:12,marginBottom:24}}>
        <div className="card2">
          <div style={{fontSize:11,color:"var(--muted)",textTransform:"uppercase",letterSpacing:".06em",marginBottom:6}}>Markets Served</div>
          <div style={{fontSize:14,fontWeight:500}}>{company.countries.join(", ")}</div>
        </div>
        <div className="card2">
          <div style={{fontSize:11,color:"var(--muted)",textTransform:"uppercase",letterSpacing:".06em",marginBottom:6}}>Customer Demand</div>
          <div style={{fontSize:14,fontWeight:500}}>{company.demandIcon} {company.demand}</div>
          <div style={{fontSize:12,color:"var(--muted)",marginTop:2}}>{company.demandDesc}</div>
        </div>
        <div className="card2">
          <div style={{fontSize:11,color:"var(--muted)",textTransform:"uppercase",letterSpacing:".06em",marginBottom:6}}>Profit Margin</div>
          <div style={{fontSize:14,fontWeight:500,textTransform:"capitalize"}}>{company.margin}</div>
          <div style={{fontSize:12,color:"var(--muted)",marginTop:2}}>
            {company.margin==="high"?"More room to absorb supply chain costs":company.margin==="medium"?"Moderate tolerance for cost variations":"Tight margins — costs matter a lot"}
          </div>
        </div>
      </div>

      <ExplainBox title="Why does this matter?">
        Your industry, markets, and demand level shape every supply chain decision. A high-demand electronics company serving three continents needs a very different setup than a niche food brand serving one country. Throughout this simulation, keep these facts in mind — they are your business context.
      </ExplainBox>

      <div style={{marginTop:24,textAlign:"right"}}>
        <button className="btn btn-primary" onClick={onNext}>Begin Building My Supply Chain →</button>
      </div>
    </div>
  );
}

function SupplierScreen({selected,onSelect,onNext,onBack,metrics}){
  return(
    <div className="fade-in">
      <StepBar currentStep={2}/>
      <div style={{display:"grid",gridTemplateColumns:"1fr 300px",gap:24,alignItems:"start"}}>
        <div>
          <h2 style={{marginBottom:4}}>Step 1: Choose Your Supplier Strategy</h2>
          <p style={{color:"var(--muted)",fontSize:14,marginBottom:20}}>A <strong style={{color:"var(--text)"}}>supplier</strong> is the company that provides you with raw materials or components to manufacture your product. Without suppliers, you have nothing to sell.</p>

          <ExplainBox title="What is a supplier?">
            Imagine you make smartphones. You need glass for screens, lithium for batteries, and rare metals for chips — all from different specialist companies called suppliers. Your relationship with them determines your costs, quality, and how vulnerable you are to disruptions like strikes or natural disasters.
          </ExplainBox>

          <div className="choices-grid">
            {SUPPLIER_STRATEGIES.map(s=>(
              <ChoiceCard key={s.id} option={s} selected={selected===s.id} onSelect={onSelect}/>
            ))}
          </div>

          {selected&&<TradeoffBox selected={selected} options={SUPPLIER_STRATEGIES}/>}

          <div style={{display:"flex",gap:12,marginTop:24}}>
            <button className="btn btn-ghost" onClick={onBack}>← Back</button>
            <button className="btn btn-primary" disabled={!selected} onClick={onNext} style={{opacity:selected?1:.4}}>Next: Factory Location →</button>
          </div>
        </div>
        <LiveMetrics metrics={metrics}/>
      </div>
    </div>
  );
}

function FactoryScreen({selected,onSelect,onNext,onBack,metrics,company}){
  return(
    <div className="fade-in">
      <StepBar currentStep={3}/>
      <div style={{display:"grid",gridTemplateColumns:"1fr 300px",gap:24,alignItems:"start"}}>
        <div>
          <h2 style={{marginBottom:4}}>Step 2: Choose a Factory Location</h2>
          <p style={{color:"var(--muted)",fontSize:14,marginBottom:20}}>Where you manufacture your <strong style={{color:"var(--text)"}}>{company.product}</strong> affects cost, quality, speed, and political risk.</p>

          <ExplainBox title="Why does factory location matter?">
            Labor costs vary massively across the world — a factory worker in Germany earns ~10× more than one in Vietnam. But cheaper isn't always better: distance adds shipping time and cost, political tensions can close borders, and some premium customers won't buy products made in certain countries. The best location depends on your product, your markets, and your values.
          </ExplainBox>

          <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:12,marginTop:16}}>
            {FACTORY_LOCATIONS.map(f=>(
              <ChoiceCard key={f.id} option={f} selected={selected===f.id} onSelect={onSelect}/>
            ))}
          </div>

          {selected&&<TradeoffBox selected={selected} options={FACTORY_LOCATIONS}/>}

          <div style={{display:"flex",gap:12,marginTop:24}}>
            <button className="btn btn-ghost" onClick={onBack}>← Back</button>
            <button className="btn btn-primary" disabled={!selected} onClick={onNext} style={{opacity:selected?1:.4}}>Next: Warehouse Strategy →</button>
          </div>
        </div>
        <LiveMetrics metrics={metrics}/>
      </div>
    </div>
  );
}

function WarehouseScreen({selected,onSelect,onNext,onBack,metrics}){
  return(
    <div className="fade-in">
      <StepBar currentStep={4}/>
      <div style={{display:"grid",gridTemplateColumns:"1fr 300px",gap:24,alignItems:"start"}}>
        <div>
          <h2 style={{marginBottom:4}}>Step 3: Warehouse Strategy</h2>
          <p style={{color:"var(--muted)",fontSize:14,marginBottom:20}}>A <strong style={{color:"var(--text)"}}>warehouse</strong> is where your finished goods are stored before being shipped to customers. Where and how you store stock is a major lever on delivery speed and cost.</p>

          <ExplainBox title="Why does warehousing matter?">
            Amazon's biggest competitive advantage isn't its website — it's having warehouses within 20 miles of most major cities. When stock is close to the customer, delivery is fast and cheap. But running many warehouses costs a lot. Businesses constantly balance the "one big warehouse vs many small ones" trade-off.
          </ExplainBox>

          <div className="choices-grid">
            {WAREHOUSE_STRATEGIES.map(w=>(
              <ChoiceCard key={w.id} option={w} selected={selected===w.id} onSelect={onSelect}/>
            ))}
          </div>

          {selected&&<TradeoffBox selected={selected} options={WAREHOUSE_STRATEGIES}/>}

          <div style={{display:"flex",gap:12,marginTop:24}}>
            <button className="btn btn-ghost" onClick={onBack}>← Back</button>
            <button className="btn btn-primary" disabled={!selected} onClick={onNext} style={{opacity:selected?1:.4}}>Next: Transport Method →</button>
          </div>
        </div>
        <LiveMetrics metrics={metrics}/>
      </div>
    </div>
  );
}

function TransportScreen({selected,onSelect,onNext,onBack,metrics}){
  return(
    <div className="fade-in">
      <StepBar currentStep={5}/>
      <div style={{display:"grid",gridTemplateColumns:"1fr 300px",gap:24,alignItems:"start"}}>
        <div>
          <h2 style={{marginBottom:4}}>Step 4: Transportation Method</h2>
          <p style={{color:"var(--muted)",fontSize:14,marginBottom:20}}>How do your goods travel from the factory to customers? Each method involves fundamental cost vs. speed trade-offs.</p>

          <ExplainBox title="The transport trilemma">
            In logistics, you're always choosing between <strong style={{color:"var(--text)"}}>speed</strong>, <strong style={{color:"var(--text)"}}>cost</strong>, and <strong style={{color:"var(--text)"}}>capacity</strong>. A shipping container can carry 20,000 boxes for the price of 2 air pallets — but it takes 6 weeks. Most businesses use multiple modes: bulk stock by sea, top-ups by air, final delivery by road.
          </ExplainBox>

          <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:12,marginTop:16}}>
            {TRANSPORT_METHODS.map(t=>(
              <ChoiceCard key={t.id} option={t} selected={selected===t.id} onSelect={t=>onSelect(t)}/>
            ))}
          </div>

          {selected&&<TradeoffBox selected={selected} options={TRANSPORT_METHODS}/>}

          <div style={{display:"flex",gap:12,marginTop:24}}>
            <button className="btn btn-ghost" onClick={onBack}>← Back</button>
            <button className="btn btn-primary" disabled={!selected} onClick={onNext} style={{opacity:selected?1:.4}}>Next: Inventory Strategy →</button>
          </div>
        </div>
        <LiveMetrics metrics={metrics}/>
      </div>
    </div>
  );
}

function InventoryScreen({selected,onSelect,onNext,onBack,metrics}){
  return(
    <div className="fade-in">
      <StepBar currentStep={6}/>
      <div style={{display:"grid",gridTemplateColumns:"1fr 300px",gap:24,alignItems:"start"}}>
        <div>
          <h2 style={{marginBottom:4}}>Step 5: Inventory Strategy</h2>
          <p style={{color:"var(--muted)",fontSize:14,marginBottom:20}}>How much <strong style={{color:"var(--text)"}}>stock</strong> should you keep on hand at all times? This decision affects your cash flow, storage costs, and ability to meet demand.</p>

          <ExplainBox title="What is inventory strategy?">
            Every product sitting in a warehouse is cash you've spent but haven't earned back yet. Keep too little and you'll sell out when demand spikes (losing sales and customers). Keep too much and you pay enormous storage costs and risk stock becoming obsolete. Toyota made "just-in-time" famous — but when COVID hit, factories without buffer stock shut down overnight.
          </ExplainBox>

          <div className="choices-grid">
            {INVENTORY_STRATEGIES.map(i=>(
              <ChoiceCard key={i.id} option={i} selected={selected===i.id} onSelect={onSelect}/>
            ))}
          </div>

          {selected&&<TradeoffBox selected={selected} options={INVENTORY_STRATEGIES}/>}

          <div style={{display:"flex",gap:12,marginTop:24}}>
            <button className="btn btn-ghost" onClick={onBack}>← Back</button>
            <button className="btn btn-primary" disabled={!selected} onClick={onNext} style={{opacity:selected?1:.4}}>See My Results →</button>
          </div>
        </div>
        <LiveMetrics metrics={metrics}/>
      </div>
    </div>
  );
}

function ResultsScreen({company,choices,metrics,onReplay}){
  const score=overallScore(metrics);
  const{label,cls,color}=scoreLabel(score);
  const insights=generateInsights(choices,metrics,company);
  const circumference=2*Math.PI*60;
  const dashOffset=circumference*(1-score/100);

  const sup=SUPPLIER_STRATEGIES.find(x=>x.id===choices.supplier);
  const fac=FACTORY_LOCATIONS.find(x=>x.id===choices.factory);
  const war=WAREHOUSE_STRATEGIES.find(x=>x.id===choices.warehouse);
  const tra=TRANSPORT_METHODS.find(x=>x.id===choices.transport);
  const inv=INVENTORY_STRATEGIES.find(x=>x.id===choices.inventory);

  return(
    <div className="fade-in">
      <StepBar currentStep={7}/>

      {/* Score hero */}
      <div className="card" style={{textAlign:"center",marginBottom:24,padding:"40px 24px"}}>
        <div style={{fontSize:12,letterSpacing:".1em",textTransform:"uppercase",color:"var(--muted)",marginBottom:20}}>Overall Supply Chain Score</div>
        <div className="score-ring">
          <svg width="160" height="160" viewBox="0 0 160 160">
            <circle cx="80" cy="80" r="60" fill="none" stroke="var(--card2)" strokeWidth="14"/>
            <circle cx="80" cy="80" r="60" fill="none" stroke={color} strokeWidth="14"
              strokeDasharray={circumference} strokeDashoffset={dashOffset}
              strokeLinecap="round" style={{transition:"stroke-dashoffset 1.2s cubic-bezier(.34,1.56,.64,1)"}}/>
          </svg>
          <div className="score-val">
            <div style={{fontSize:40,fontWeight:700,color,lineHeight:1}}>{score}</div>
            <div style={{fontSize:13,color:"var(--muted)"}}>{label}</div>
          </div>
        </div>
        <p style={{color:"var(--muted)",fontSize:14,maxWidth:500,margin:"20px auto 0"}}>
          Your supply chain score reflects cost efficiency, delivery speed, resilience, customer satisfaction, and sustainability.
        </p>
      </div>

      {/* Metric cards */}
      <div className="metrics-grid" style={{marginBottom:24}}>
        <MetricCard label="Cost Efficiency" value={metrics.cost} icon="💰"/>
        <MetricCard label="Delivery Speed" value={metrics.speed} icon="⚡"/>
        <MetricCard label="Risk Resilience" value={100-metrics.risk} icon="🛡️"/>
        <MetricCard label="Customer Satisfaction" value={metrics.satisfaction} icon="😊"/>
        <MetricCard label="Sustainability" value={metrics.sustainability} icon="🌱"/>
      </div>

      {/* Decisions summary */}
      <div className="card" style={{marginBottom:24}}>
        <h3 style={{marginBottom:16}}>Your Decisions</h3>
        <div style={{display:"grid",gridTemplateColumns:"repeat(auto-fit,minmax(180px,1fr))",gap:12}}>
          {[
            {label:"Supplier",val:sup?.label,icon:"🤝"},
            {label:"Factory",val:fac?.label,icon:"🏭"},
            {label:"Warehouse",val:war?.label,icon:"📦"},
            {label:"Transport",val:tra?.label,icon:"🚢"},
            {label:"Inventory",val:inv?.label,icon:"📊"},
          ].map(d=>(
            <div key={d.label} className="card2" style={{display:"flex",alignItems:"center",gap:10}}>
              <span style={{fontSize:20}}>{d.icon}</span>
              <div>
                <div style={{fontSize:11,color:"var(--muted)",textTransform:"uppercase",letterSpacing:".05em"}}>{d.label}</div>
                <div style={{fontWeight:600,fontSize:14}}>{d.val}</div>
              </div>
            </div>
          ))}
        </div>
      </div>

      {/* Strengths & Weaknesses */}
      <div className="dash-grid" style={{marginBottom:24}}>
        <div className="card">
          <h3 style={{marginBottom:12,color:"var(--green)"}}>✅ Strengths</h3>
          {insights.strengths.map((s,i)=>(
            <div key={i} className="sw-item">
              <div className="sw-dot" style={{background:"var(--green)"}}/>
              <span style={{fontSize:14,color:"var(--muted)"}}>{s}</span>
            </div>
          ))}
        </div>
        <div className="card">
          <h3 style={{marginBottom:12,color:"var(--amber)"}}>⚠️ Weaknesses</h3>
          {insights.weaknesses.length>0?insights.weaknesses.map((w,i)=>(
            <div key={i} className="sw-item">
              <div className="sw-dot" style={{background:"var(--amber)"}}/>
              <span style={{fontSize:14,color:"var(--muted)"}}>{w}</span>
            </div>
          )):<div style={{fontSize:14,color:"var(--muted)"}}>No major weaknesses identified — impressive!</div>}
        </div>
      </div>

      {/* Biggest Risk */}
      <div className="card" style={{marginBottom:24,borderColor:"var(--amber)"}}>
        <h3 style={{marginBottom:8,color:"var(--amber)"}}>⚠️ Biggest Risk</h3>
        <p style={{fontSize:14,color:"var(--muted)"}}>{insights.bigRisk}</p>
      </div>

      {/* Improvements */}
      <div className="card" style={{marginBottom:32}}>
        <h3 style={{marginBottom:16,color:"var(--accent)"}}>🚀 Three Practical Improvements</h3>
        {insights.improvements.slice(0,3).map((imp,i)=>(
          <div key={i} style={{display:"flex",gap:14,padding:"12px 0",borderBottom:i<2?"1px solid var(--border)":"none"}}>
            <div style={{width:28,height:28,borderRadius:"50%",background:"var(--accentbg)",color:"var(--accent)",display:"flex",alignItems:"center",justifyContent:"center",fontWeight:700,fontSize:13,flexShrink:0}}>
              {i+1}
            </div>
            <span style={{fontSize:14,color:"var(--muted)",lineHeight:1.7}}>{imp}</span>
          </div>
        ))}
      </div>

      {/* Company summary */}
      <div className="explain-box" style={{marginBottom:32}}>
        <div className="explain-title">Supply Chain Summary</div>
        <p style={{fontSize:14,color:"var(--muted)",lineHeight:1.8}}>
          You built a supply chain for <strong style={{color:"var(--text)"}}>{company.industry}</strong> (product: <strong style={{color:"var(--text)"}}>{company.product}</strong>) serving <strong style={{color:"var(--text)"}}>{company.countries.join(", ")}</strong> with <strong style={{color:"var(--text)"}}>{company.demand.toLowerCase()}</strong> customer demand. You sourced from <strong style={{color:"var(--text)"}}>{sup?.label}</strong>, manufactured in <strong style={{color:"var(--text)"}}>{fac?.label}</strong>, stored using <strong style={{color:"var(--text)"}}>{war?.label}</strong>, shipped via <strong style={{color:"var(--text)"}}>{tra?.label}</strong>, and ran a <strong style={{color:"var(--text)"}}>{inv?.label}</strong> inventory policy.
        </p>
      </div>

      <div style={{textAlign:"center"}}>
        <button className="btn btn-primary btn-lg" onClick={onReplay}>
          🔄 Play Again with a New Company
        </button>
        <p style={{marginTop:12,fontSize:12,color:"var(--subtle)"}}>Each playthrough generates a different company, products, and markets</p>
      </div>
    </div>
  );
}

// ── Main App ──────────────────────────────────────────────────────────────────
function App(){
  const[screen,setScreen]=useState("welcome");
  const[company,setCompany]=useState(null);
  const[choices,setChoices]=useState({supplier:null,factory:null,warehouse:null,transport:null,inventory:null});
  const[metrics,setMetrics]=useState({cost:50,speed:50,risk:50,satisfaction:50,sustainability:50});

  const updateChoice=(key,val)=>{
    const next={...choices,[key]:val};
    setChoices(next);
    setMetrics(computeMetrics(next));
  };

  const startGame=()=>{
    const c=generateCompany();
    setCompany(c);
    setChoices({supplier:null,factory:null,warehouse:null,transport:null,inventory:null});
    setMetrics({cost:50,speed:50,risk:50,satisfaction:50,sustainability:50});
    setScreen("company");
  };

  const replay=()=>{
    setScreen("welcome");
  };

  return(
    <div className="app">
      {/* Header */}
      <div style={{display:"flex",alignItems:"center",justifyContent:"space-between",marginBottom:32,paddingBottom:16,borderBottom:"1px solid var(--border)"}}>
        <div style={{display:"flex",alignItems:"center",gap:10}}>
          <span style={{fontSize:22}}>🏭</span>
          <span style={{fontWeight:700,fontSize:16}}>Supply Chain Builder</span>
          <span className="tag tag-blue" style={{marginLeft:4}}>Educational Sim</span>
        </div>
        {screen!=="welcome"&&(
          <button className="btn btn-ghost" style={{fontSize:13}} onClick={replay}>↺ Restart</button>
        )}
      </div>

      {/* Screens */}
      {screen==="welcome"&&<WelcomeScreen onStart={startGame}/>}
      {screen==="company"&&company&&<CompanyScreen company={company} onNext={()=>setScreen("supplier")}/>}
      {screen==="supplier"&&<SupplierScreen
        selected={choices.supplier}
        onSelect={v=>updateChoice("supplier",v)}
        onNext={()=>setScreen("factory")}
        onBack={()=>setScreen("company")}
        metrics={metrics}
      />}
      {screen==="factory"&&<FactoryScreen
        selected={choices.factory}
        onSelect={v=>updateChoice("factory",v)}
        onNext={()=>setScreen("warehouse")}
        onBack={()=>setScreen("supplier")}
        metrics={metrics}
        company={company}
      />}
      {screen==="warehouse"&&<WarehouseScreen
        selected={choices.warehouse}
        onSelect={v=>updateChoice("warehouse",v)}
        onNext={()=>setScreen("transport")}
        onBack={()=>setScreen("factory")}
        metrics={metrics}
      />}
      {screen==="transport"&&<TransportScreen
        selected={choices.transport}
        onSelect={v=>updateChoice("transport",v)}
        onNext={()=>setScreen("inventory")}
        onBack={()=>setScreen("warehouse")}
        metrics={metrics}
      />}
      {screen==="inventory"&&<InventoryScreen
        selected={choices.inventory}
        onSelect={v=>updateChoice("inventory",v)}
        onNext={()=>setScreen("results")}
        onBack={()=>setScreen("transport")}
        metrics={metrics}
      />}
      {screen==="results"&&<ResultsScreen
        company={company}
        choices={choices}
        metrics={metrics}
        onReplay={replay}
      />}

      <div style={{height:40}}/>
    </div>
  );
}

ReactDOM.createRoot(document.getElementById("root")).render(<App/>);
</script>
</body>
</html>
