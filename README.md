<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sri Lankan Stock Investment Tracker</title>
<style>
:root{--ink:#172033;--muted:#687386;--line:#e5e9f0;--bg:#f5f7fb;--card:#fff;--navy:#18243b;--blue:#356ae6;--green:#16845b;--amber:#a96a08;--red:#c13c48;--shadow:0 8px 28px rgba(23,32,51,.06)}
*{box-sizing:border-box}body{margin:0;background:var(--bg);color:var(--ink);font:14px/1.5 Inter,ui-sans-serif,system-ui,-apple-system,"Segoe UI",sans-serif}
header{background:linear-gradient(120deg,#17243b,#263d62);color:white;padding:28px max(22px,calc((100% - 1200px)/2))}
header .eyebrow{font-size:11px;letter-spacing:.15em;text-transform:uppercase;color:#b9c8e1;font-weight:700}
header h1{margin:7px 0 4px;font-size:clamp(24px,4vw,34px);letter-spacing:-.03em}
header p{margin:0;color:#d5deec;max-width:720px}
.wrap{max-width:1200px;margin:24px auto;padding:0 20px 48px}
.notice{background:#fff8e9;border:1px solid #f0dfb9;border-radius:12px;padding:12px 15px;color:#73521b;margin-bottom:18px;font-size:12px}
nav{display:flex;gap:7px;flex-wrap:wrap;margin-bottom:18px}
nav button{border:1px solid var(--line);background:#fff;border-radius:10px;padding:10px 14px;color:#566176;font-weight:650;cursor:pointer}
nav button.active{background:var(--navy);color:#fff;border-color:var(--navy)}
.panel{display:none}.panel.active{display:block}
.grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:13px;margin-bottom:18px}
.stat,.card{background:var(--card);border:1px solid var(--line);border-radius:15px;box-shadow:var(--shadow)}
.stat{padding:16px}.stat small{color:var(--muted);font-weight:600}.stat strong{display:block;font-size:24px;margin-top:6px;letter-spacing:-.03em}
.card{padding:18px;margin-bottom:16px}.card h2{font-size:17px;margin:0 0 4px}.sub{color:var(--muted);font-size:12px;margin:0 0 15px}
.toolbar{display:flex;gap:9px;flex-wrap:wrap;align-items:center;justify-content:space-between;margin-bottom:12px}
input,select,textarea{width:100%;border:1px solid #dce2eb;border-radius:9px;padding:10px 11px;font:inherit;color:var(--ink);background:white;outline:none}
input:focus,select:focus,textarea:focus{border-color:#7c9be9;box-shadow:0 0 0 3px #356ae618}
.search{max-width:280px}.btn{border:0;border-radius:9px;padding:10px 13px;font-weight:700;cursor:pointer;background:var(--blue);color:white}
.btn.secondary{background:#edf2ff;color:#3158bd}.btn.dark{background:var(--navy)}.btn.danger{background:#fff0f1;color:var(--red);border:1px solid #f2cdd1}
.btn.small{padding:7px 10px;font-size:12px}
table{width:100%;border-collapse:collapse;min-width:760px}th,td{text-align:left;padding:12px 10px;border-bottom:1px solid var(--line);vertical-align:middle}th{font-size:11px;text-transform:uppercase;letter-spacing:.06em;color:#788397;background:#fafbfd}td{font-size:13px}
.tablewrap{overflow:auto;border:1px solid var(--line);border-radius:11px}
.company{font-weight:750}.ticker{font-size:11px;color:var(--muted);display:block}
.tag{display:inline-block;border-radius:30px;padding:4px 9px;font-size:11px;font-weight:750;background:#eef1f6;color:#596579}
.tag.buy{background:#e7f6ef;color:#13734f}.tag.watch{background:#fff3dc;color:#96600c}.tag.avoid{background:#ffeaec;color:#b4313d}
.fields{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:12px}
.field label{display:block;font-size:12px;color:#596579;font-weight:700;margin:0 0 5px}
.field.full{grid-column:1/-1}
.actions{display:flex;gap:8px;flex-wrap:wrap;margin-top:15px}
.result{border:1px solid var(--line);border-radius:12px;padding:15px;background:#fafbfd;margin-top:15px}
.resulthead{display:flex;align-items:center;gap:10px;margin-bottom:8px}
.result h3{margin:0;font-size:16px}
.result p{margin:7px 0;color:#536075}
.checks{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:7px;margin-top:10px}
.check{background:#fff;border:1px solid var(--line);border-radius:8px;padding:8px 10px;font-size:12px}
.check.yes{border-color:#c6e7d7;background:#f3fbf7}.check.no{border-color:#f0d7d9;background:#fff8f8}
.muted{color:var(--muted)}.empty{text-align:center;color:var(--muted);padding:24px}
canvas{width:100%;height:250px;display:block}
footer{color:#8993a4;text-align:center;font-size:11px;padding:15px}
@media(max-width:850px){.grid{grid-template-columns:repeat(2,1fr)}.fields{grid-template-columns:repeat(2,1fr)}}
@media(max-width:560px){.grid{grid-template-columns:1fr 1fr}.fields{grid-template-columns:1fr}.field.full{grid-column:auto}.wrap{padding:0 12px 35px}.card{padding:14px}}
</style>
</head>
<body>
<header>
 <div class="eyebrow">Personal investing workspace · Colombo Stock Exchange</div>
 <h1>Sri Lankan Stock Investment Tracker</h1>
 <p>Research companies, assess investment opportunities and record purchases separately. Your entries are saved in this browser.</p>
</header>
<main class="wrap">
 <div class="notice"><b>Important:</b> This tracker is an organisational and screening tool, not financial advice. Enter verified, up-to-date figures yourself. A BUY label is only a preliminary screen and is not a recommendation to invest.</div>
 <nav>
  <button class="active" data-tab="overview">Overview</button>
  <button data-tab="companies">Company Watchlist</button>
  <button data-tab="research">Company Research</button>
  <button data-tab="transactions">My Investments</button>
  <button data-tab="history">Price History</button>
 </nav>

 <section id="overview" class="panel active">
  <div class="grid">
   <div class="stat"><small>Companies tracked</small><strong id="statCompanies">11</strong></div>
   <div class="stat"><small>Total invested</small><strong id="statInvested">LKR 0</strong></div>
   <div class="stat"><small>Shares held</small><strong id="statShares">0</strong></div>
   <div class="stat"><small>Recorded purchases</small><strong id="statPurchases">0</strong></div>
  </div>
  <div class="card">
   <h2>Watchlist snapshot</h2><p class="sub">Your selected companies. Add research data to begin assessing them.</p>
   <div class="tablewrap"><table><thead><tr><th>Company</th><th>Latest price (LKR)</th><th>Assessment</th><th>Research status</th></tr></thead><tbody id="overviewRows"></tbody></table></div>
  </div>
  <div class="card"><h2>Investment activity</h2><p class="sub">Total purchase cost recorded by company.</p><canvas id="investmentChart" width="900" height="250"></canvas></div>
 </section>

 <section id="companies" class="panel">
  <div class="card">
   <div class="toolbar"><div><h2>Company watchlist</h2><p class="sub">10 companies included. You can add more at any time.</p></div><input class="search" id="companySearch" placeholder="Search companies…"></div>
   <div class="tablewrap"><table><thead><tr><th>Company</th><th>Group</th><th>Latest price (LKR)</th><th>Decision</th><th>Action</th></tr></thead><tbody id="companyRows"></tbody></table></div>
   <div class="actions"><button class="btn secondary" id="addCompany">+ Add a company</button></div>
  </div>
 </section>

 <section id="research" class="panel">
  <div class="card">
   <h2>Company research & investment decision</h2>
   <p class="sub">Select a company, enter the latest available figures and record your reasoning.</p>
   <div class="fields">
    <div class="field"><label>Company</label><select id="researchCompany"></select></div>
    <div class="field"><label>Current share price (LKR)</label><input id="price" type="number" min="0" step="0.01" placeholder="e.g. 125.50"></div>
    <div class="field"><label>Industry average P/E</label><input id="industryPE" type="number" min="0" step="0.01" placeholder="e.g. 8.5"></div>
    <div class="field"><label>Revenue growth (%)</label><input id="revenue" type="number" step="0.01" placeholder="e.g. 12"></div>
    <div class="field"><label>Net profit growth (%)</label><input id="profit" type="number" step="0.01" placeholder="e.g. 9"></div>
    <div class="field"><label>EPS growth (%)</label><input id="epsGrowth" type="number" step="0.01" placeholder="e.g. 7"></div>
    <div class="field"><label>ROE (%)</label><input id="roe" type="number" step="0.01" placeholder="e.g. 14"></div>
    <div class="field"><label>Company P/E ratio</label><input id="pe" type="number" min="0" step="0.01" placeholder="e.g. 7.2"></div>
    <div class="field"><label>Cash flow</label><select id="cash"><option value="">Select status</option><option value="positive">Positive operating cash flow</option><option value="negative">Negative operating cash flow</option><option value="mixed">Mixed / volatile</option></select></div>
    <div class="field"><label>EPS (LKR)</label><input id="eps" type="number" step="0.01" placeholder="Latest EPS"></div>
    <div class="field"><label>Dividend per share (LKR)</label><input id="dividend" type="number" min="0" step="0.01" placeholder="Optional"></div>
    <div class="field"><label>Research date</label><input id="researchDate" type="date"></div>
    <div class="field full"><label>Business quality & competitive strengths</label><textarea id="quality" rows="3" placeholder="Describe business model, market position, management, competitive advantages and sector outlook…"></textarea></div>
    <div class="field full"><label>Risks and concerns</label><textarea id="risk" rows="3" placeholder="Describe debt, regulation, competition, governance, currency exposure, cyclicality and other risks…"></textarea></div>
    <div class="field full"><label>Your research notes / sources</label><textarea id="notes" rows="2" placeholder="Record annual report, interim report, CSE announcement or other source and date…"></textarea></div>
   </div>
   <div class="actions"><button class="btn" id="assess">Assess company</button><button class="btn secondary" id="saveResearch">Save research</button><button class="btn secondary" id="clearResearch">Clear form</button></div>
   <div id="assessment" class="result" style="display:none"></div>
  </div>
  <div class="card"><h2>How the screening works</h2><p class="sub">A simple first-pass checklist. Thresholds are indicative and may not suit every sector, particularly banks and finance companies.</p>
   <div class="checks">
    <div class="check">Revenue growth above 0%</div><div class="check">Net profit growth above 0%</div>
    <div class="check">EPS growth above 0%</div><div class="check">ROE at least 12%</div>
    <div class="check">P/E no more than 1.2× industry average</div><div class="check">Positive operating cash flow</div>
   </div>
   <p class="muted" style="font-size:12px;margin-top:12px">The screen requires current price, EPS, industry P/E and cash-flow status, plus written quality and risk notes. Review bank-specific measures such as capital adequacy, NPLs, net interest margin and liquidity; for finance companies, review funding costs, asset quality and provisioning. A low P/E alone does not mean a share is undervalued.</p>
  </div>
 </section>

 <section id="transactions" class="panel">
  <div class="card">
   <h2>Record a share purchase</h2><p class="sub">This is a separate step. An assessment never creates a purchase automatically.</p>
   <div class="fields">
    <div class="field"><label>Company</label><select id="buyCompany"></select></div>
    <div class="field"><label>Purchase date</label><input id="buyDate" type="date"></div>
    <div class="field"><label>Number of shares</label><input id="buyQuantity" type="number" min="1" step="1" placeholder="e.g. 100"></div>
    <div class="field"><label>Purchase price per share (LKR)</label><input id="buyPrice" type="number" min="0" step="0.01" placeholder="e.g. 125.50"></div>
    <div class="field"><label>Brokerage / fees (LKR)</label><input id="buyFees" type="number" min="0" step="0.01" value="0"></div>
    <div class="field"><label>Reference / note</label><input id="buyNote" placeholder="Optional note"></div>
   </div>
   <div class="actions"><button class="btn" id="recordBuy">Record purchase</button></div>
  </div>
  <div class="card"><h2>Purchase history</h2><p class="sub">Edit or delete a recorded transaction if you make a mistake.</p>
   <div class="tablewrap"><table><thead><tr><th>Date</th><th>Company</th><th>Shares</th><th>Price/share</th><th>Fees</th><th>Total cost</th><th></th></tr></thead><tbody id="transactionRows"></tbody></table></div>
  </div>
 </section>

 <section id="history" class="panel">
  <div class="card"><h2>Share price history</h2><p class="sub">Manually add closing prices from your chosen source. The chart uses only the entries you record.</p>
   <div class="fields">
    <div class="field"><label>Company</label><select id="historyCompany"></select></div>
    <div class="field"><label>Date</label><input id="historyDate" type="date"></div>
    <div class="field"><label>Closing price (LKR)</label><input id="historyPrice" type="number" min="0" step="0.01" placeholder="Price"></div>
   </div>
   <div class="actions"><button class="btn" id="addPrice">Add price point</button></div>
   <div style="margin-top:18px"><canvas id="priceChart" width="900" height="260"></canvas></div>
   <div class="tablewrap" style="margin-top:12px"><table><thead><tr><th>Date</th><th>Company</th><th>Price (LKR)</th><th></th></tr></thead><tbody id="priceRows"></tbody></table></div>
  </div>
 </section>
 <footer>Independent tracker · Data is entered by you and stored locally in this browser. Export a backup regularly.</footer>
</main>
<script>
const seed=[
{name:"Hatton National Bank",ticker:"HNB",group:"Main watchlist"},
{name:"Sampath Bank",ticker:"SAMP",group:"Main watchlist"},
{name:"Commercial Bank of Ceylon",ticker:"COMB",group:"Main watchlist"},
{name:"Hayleys PLC",ticker:"HAYL",group:"Main watchlist"},
{name:"Dialog Axiata",ticker:"DIAL",group:"Main watchlist"},
{name:"National Development Bank",ticker:"NDB",group:"Additional watchlist"},
{name:"Nations Trust Bank",ticker:"NTB",group:"Additional watchlist"},
{name:"Seylan Bank",ticker:"SEYB",group:"Additional watchlist"},
{name:"LB Finance",ticker:"LFIN",group:"Additional watchlist"},
{name:"Royal Ceramics Lanka",ticker:"RCL",group:"Additional watchlist"}
];
let data=JSON.parse(localStorage.getItem("slStockTracker_v1")||"null")||{companies:seed.map(c=>({...c,price:"",decision:"",research:null})),transactions:[],prices:[]};
const $=id=>document.getElementById(id);
const fmt=n=>"LKR "+Number(n||0).toLocaleString("en-LK",{maximumFractionDigits:2});
const esc=s=>String(s??"").replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]));
function save(){localStorage.setItem("slStockTracker_v1",JSON.stringify(data));render()}
function company(id){return data.companies.find(c=>c.ticker===id)}
function options(selectId,selected){$(selectId).innerHTML=data.companies.map(c=>`<option value="${esc(c.ticker)}" ${c.ticker===selected?"selected":""}>${esc(c.name)} (${esc(c.ticker)})</option>`).join("")}
function render(){
 $("statCompanies").textContent=data.companies.length;
 const total=data.transactions.reduce((s,t)=>s+t.qty*t.price+t.fees,0);
 $("statInvested").textContent=fmt(total);
 $("statShares").textContent=data.transactions.reduce((s,t)=>s+t.qty,0).toLocaleString();
 $("statPurchases").textContent=data.transactions.length;
 const rows=data.companies.map(c=>`<tr><td><span class="company">${esc(c.name)}</span><span class="ticker">${esc(c.ticker)}</span></td><td>${esc(c.group)}</td><td>${c.price?fmt(c.price):"—"}</td><td>${decisionTag(c.decision)}</td><td><button class="btn secondary small" onclick="openResearch('${esc(c.ticker)}')">Research</button></td></tr>`).join("");
 $("companyRows").innerHTML=rows;$("overviewRows").innerHTML=data.companies.map(c=>`<tr><td><b>${esc(c.name)}</b><span class="ticker">${esc(c.ticker)}</span></td><td>${c.price?fmt(c.price):"—"}</td><td>${decisionTag(c.decision)}</td><td>${c.research?"Research saved":"Not researched"}</td></tr>`).join("");
 const q=($("companySearch").value||"").toLowerCase();[...$("companyRows").rows].forEach(r=>r.style.display=r.innerText.toLowerCase().includes(q)?"":"none");
 $("transactionRows").innerHTML=data.transactions.length?data.transactions.map((t,i)=>`<tr><td>${esc(t.date)}</td><td>${esc(company(t.ticker)?.name||t.ticker)}</td><td>${t.qty.toLocaleString()}</td><td>${fmt(t.price)}</td><td>${fmt(t.fees)}</td><td><b>${fmt(t.qty*t.price+t.fees)}</b></td><td><button class="btn danger small" onclick="deleteTx(${i})">Delete</button></td></tr>`).join(""):`<tr><td colspan="7" class="empty">No purchases recorded yet.</td></tr>`;
 $("priceRows").innerHTML=data.prices.length?data.prices.slice().sort((a,b)=>b.date.localeCompare(a.date)).map((p)=>`<tr><td>${esc(p.date)}</td><td>${esc(company(p.ticker)?.name||p.ticker)}</td><td>${fmt(p.price)}</td><td><button class="btn danger small" onclick="deletePrice('${p.id}')">Delete</button></td></tr>`).join(""):`<tr><td colspan="4" class="empty">No price history entered yet.</td></tr>`;
 drawInvestment();drawPrice();
}
function decisionTag(d){return d?`<span class="tag ${d.toLowerCase()}">${esc(d)}</span>`:`<span class="tag">Not assessed</span>`}
function drawInvestment(){
 const c=$("investmentChart"),ctx=c.getContext("2d");ctx.clearRect(0,0,c.width,c.height);
 const vals=data.companies.map(co=>({name:co.ticker,v:data.transactions.filter(t=>t.ticker===co.ticker).reduce((s,t)=>s+t.qty*t.price+t.fees,0)})).filter(x=>x.v>0);
 if(!vals.length){ctx.fillStyle="#8792a4";ctx.font="15px sans-serif";ctx.fillText("Record a purchase to see your investment breakdown.",20,40);return}
 const max=Math.max(...vals.map(x=>x.v));vals.forEach((x,i)=>{let y=20+i*32,w=(x.v/max)*650;ctx.fillStyle="#356ae6";ctx.fillRect(110,y,w,17);ctx.fillStyle="#46536a";ctx.font="12px sans-serif";ctx.fillText(x.name,15,y+13);ctx.fillText(Math.round(x.v).toLocaleString(),120+w,y+13)});
}
function drawPrice(){
 const c=$("priceChart"),ctx=c.getContext("2d");ctx.clearRect(0,0,c.width,c.height);
 const ticker=$("historyCompany").value;const vals=data.prices.filter(p=>p.ticker===ticker).sort((a,b)=>a.date.localeCompare(b.date));
 if(vals.length<2){ctx.fillStyle="#8792a4";ctx.font="15px sans-serif";ctx.fillText(vals.length?"Add another price point to draw a trend.":"Add at least two price points for the selected company to display a chart.",20,40);return}
 const min=Math.min(...vals.map(x=>x.price)),max=Math.max(...vals.map(x=>x.price)),range=max-min||1;
 ctx.strokeStyle="#356ae6";ctx.lineWidth=3;ctx.beginPath();vals.forEach((p,i)=>{let x=35+i*(c.width-70)/(vals.length-1),y=c.height-35-(p.price-min)/range*(c.height-75);i?ctx.lineTo(x,y):ctx.moveTo(x,y)});ctx.stroke();
 vals.forEach((p,i)=>{let x=35+i*(c.width-70)/(vals.length-1),y=c.height-35-(p.price-min)/range*(c.height-75);ctx.fillStyle="#356ae6";ctx.beginPath();ctx.arc(x,y,4,0,Math.PI*2);ctx.fill()});
 ctx.fillStyle="#687386";ctx.font="12px sans-serif";ctx.fillText(fmt(min),5,c.height-25);ctx.fillText(fmt(max),5,22);ctx.fillText(vals[0].date,30,c.height-8);ctx.fillText(vals.at(-1).date,c.width-100,c.height-8);
}
function openResearch(t){$("researchCompany").value=t;loadResearch();document.querySelector('[data-tab="research"]').click()}
window.openResearch=openResearch;
function loadResearch(){
 const c=company($("researchCompany").value),r=c?.research||{};
 ["price","industryPE","revenue","profit","epsGrowth","roe","pe","cash","eps","dividend","researchDate","quality","risk","notes"].forEach(k=>$(k).value=r[k]??(k==="price"?(c?.price||""):""));
 $("assessment").style.display="none";
}
function formData(){const r={};["price","industryPE","revenue","profit","epsGrowth","roe","pe","cash","eps","dividend","researchDate","quality","risk","notes"].forEach(k=>r[k]=$(k).value.trim());return r}
function assess(){
 const r=formData(),required=["price","eps","industryPE","cash"],missing=required.filter(k=>!r[k]);
 const checks=[
 ["Revenue growth above 0%",r.revenue!==""&&+r.revenue>0],
 ["Net profit growth above 0%",r.profit!==""&&+r.profit>0],
 ["EPS growth above 0%",r.epsGrowth!==""&&+r.epsGrowth>0],
 ["ROE at least 12%",r.roe!==""&&+r.roe>=12],
 ["P/E no more than 1.2× industry average",r.pe!==""&&r.industryPE!==""&&+r.pe<=1.2*+r.industryPE],
 ["Positive operating cash flow",r.cash==="positive"]
 ];
 const score=checks.filter(x=>x[1]).length,complete=!missing.length&&r.quality.length>=12&&r.risk.length>=12&&r.pe!==""&&r.revenue!==""&&r.profit!==""&&r.epsGrowth!==""&&r.roe!=="";
 let decision="WATCH",why=[];
 if((r.profit!==""&&+r.profit<0&&r.cash==="negative")||score<=2)decision="AVOID";
 else if(score>=5&&complete)decision="BUY";
 else decision="WATCH";
 if(missing.length)why.push("Missing essential information: "+missing.join(", ")+".");
 if(r.quality.length<12||r.risk.length<12)why.push("Add meaningful business-quality and risk notes before treating the assessment as complete.");
 if(decision==="BUY")why.push("The entered figures pass at least five of the six screening checks and the required research fields are complete. This is a preliminary screen only; verify the latest filings, valuation, governance and sector-specific measures.");
 if(decision==="WATCH")why.push("The evidence is incomplete or mixed. Continue monitoring results, valuation, cash generation and risks before making a decision.");
 if(decision==="AVOID")why.push("The entered figures show several failed checks or a combination of negative profit growth and negative operating cash flow. Investigate the causes before considering the company.");
 $("assessment").style.display="block";
 $("assessment").innerHTML=`<div class="resulthead"><span class="tag ${decision.toLowerCase()}">${decision}</span><h3>${decision==="BUY"?"Screening criteria broadly passed":decision==="AVOID"?"Significant warning signs":"More research needed"}</h3></div><p><b>Screening score:</b> ${score}/6 checks passed. ${complete?"Required fields completed.":"Research is incomplete."}</p><div class="checks">${checks.map(x=>`<div class="check ${x[1]?"yes":"no"}">${x[1]?"✓":"○"} ${esc(x[0])}</div>`).join("")}</div>${why.map(x=>`<p>${esc(x)}</p>`).join("")}<p><b>Next step:</b> Save the research. If you independently decide to buy, go to <b>My Investments</b> and record the purchase there.</p>`;
 const c=company($("researchCompany").value);c.decision=decision;c.price=r.price;c.research=r;localStorage.setItem("slStockTracker_v1",JSON.stringify(data));render();
}
document.querySelectorAll("nav button").forEach(b=>b.addEventListener("click",()=>{document.querySelectorAll("nav button").forEach(x=>x.classList.remove("active"));document.querySelectorAll(".panel").forEach(x=>x.classList.remove("active"));b.classList.add("active");$(b.dataset.tab).classList.add("active")}));
$("researchCompany").addEventListener("change",loadResearch);$("historyCompany").addEventListener("change",drawPrice);$("companySearch").addEventListener("input",render);
$("assess").onclick=assess;
$("saveResearch").onclick=()=>{const c=company($("researchCompany").value);c.research=formData();c.price=c.research.price;save();alert("Research saved in this browser.")};
$("clearResearch").onclick=()=>{if(confirm("Clear the research form?"))loadResearch()};
$("recordBuy").onclick=()=>{let qty=+$("buyQuantity").value,price=+$("buyPrice").value;if(!(qty>0&&price>0)){alert("Enter a valid share quantity and purchase price.");return}data.transactions.push({ticker:$("buyCompany").value,date:$("buyDate").value||new Date().toISOString().slice(0,10),qty,price,fees:+$("buyFees").value||0,note:$("buyNote").value});$("buyQuantity").value="";$("buyPrice").value="";$("buyFees").value="0";$("buyNote").value="";save()};
window.deleteTx=i=>{if(confirm("Delete this purchase record?")){data.transactions.splice(i,1);save()}};
$("addPrice").onclick=()=>{let p=+$("historyPrice").value;if(!(p>0)){alert("Enter a valid share price.");return}data.prices.push({id:Date.now().toString()+Math.random(),ticker:$("historyCompany").value,date:$("historyDate").value||new Date().toISOString().slice(0,10),price:p});$("historyPrice").value="";save()};
window.deletePrice=id=>{data.prices=data.prices.filter(p=>p.id!==id);save()};
$("addCompany").onclick=()=>{let name=prompt("Enter the company name:");if(!name)return;let ticker=prompt("Enter its CSE ticker symbol:");if(!ticker)return;ticker=ticker.trim().toUpperCase();if(data.companies.some(c=>c.ticker===ticker)){alert("That ticker is already on your list.");return}data.companies.push({name:name.trim(),ticker,group:"Added by you",price:"",decision:"",research:null});refreshOptions();save()};
function refreshOptions(){let selected={research:$("researchCompany").value,buy:$("buyCompany").value,history:$("historyCompany").value};options("researchCompany",selected.research);options("buyCompany",selected.buy);options("historyCompany",selected.history)}
// Initialise
const today=new Date().toISOString().slice(0,10);["researchDate","buyDate","historyDate"].forEach(id=>$(id).value=today);
refreshOptions();render();loadResearch();
</script>
</body></html>
