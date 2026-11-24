
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#101827">
<title>Shakil Trade Analyzer</title>
<link rel="manifest" href="manifest.json">
<style>
*{box-sizing:border-box}
body{margin:0;background:#0b1220;color:#e5e7eb;font-family:Tahoma,Arial,sans-serif}
header{padding:20px;background:#111c2e;border-bottom:1px solid #26354b}
h1{font-size:21px;margin:0 0 8px;color:#f4c76b}
small,.muted{color:#9ca3af}
main{max-width:1100px;margin:auto;padding:16px}
.panel{background:#111c2e;border:1px solid #26354b;border-radius:13px;padding:15px;margin-bottom:14px}
.controls{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
label{font-size:12px;color:#aab6c8}
input,select,button{width:100%;padding:11px;margin-top:6px;border-radius:8px;border:1px solid #34445d;background:#0b1220;color:white}
button{background:#d6a94f;color:#111827;font-weight:bold;border:0;cursor:pointer}
button:disabled{opacity:.5}
.status{padding:10px;background:#0b1220;border-radius:8px;margin-top:12px;font-size:13px}
.cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:12px}
.trade{background:#111c2e;border:1px solid #26354b;border-radius:12px;padding:14px}
.trade h3{margin:0 0 10px}
.long{color:#35d49a}.short{color:#ff7373}.wait{color:#f3c969}
.metrics{display:grid;grid-template-columns:1fr 1fr;gap:8px;font-size:13px}
.metric{background:#0b1220;padding:8px;border-radius:7px}
.metric b{display:block;color:#fff;margin-top:4px;direction:ltr;text-align:right}
footer{padding:20px;text-align:center;color:#8491a5;font-size:11px}
@media(max-width:600px){.controls{grid-template-columns:1fr 1fr}}
</style>
</head>
<body>
<header>
<h1>Shakil Trade Analyzer</h1>
<div class="muted">اسکنر تحلیل بازار فیوچرز | نسخه آزمایشی ۱.۰</div>
</header>
<main>
<section class="panel">
<div class="controls">
<div><label>سرمایه (USDT)</label><input id="capital" type="number" value="50" min="1"></div>
<div><label>ریسک هر معامله (USDT)</label><input id="risk" type="number" value="1" min="0.1" step="0.1"></div>
<div><label>اهرم</label><input id="leverage" type="number" value="20" min="1" max="125"></div>
<div><label>تعداد ارزها</label><select id="limit"><option>10</option><option selected>30</option><option>50</option></select></div>
<div><label>حداقل امتیاز سیگنال</label><select id="threshold"><option value="5">۵ از ۷</option><option value="6">۶ از ۷</option><option value="7">۷ از ۷</option></select></div>
<div style="display:flex;align-items:end"><button id="scan">اسکن بازار</button></div>
</div>
<div class="status" id="status">آماده دریافت داده‌های عمومی Binance Futures</div>
</section>
<section class="panel">
<b>نتایج اسکن</b>
<p class="muted" style="font-size:12px">سیگنال‌ها بر اساس کندل‌های بسته‌شده 4H، 1H و 5m محاسبه می‌شوند. قبل از معامله، قیمت و شرایط بازار را در صرافی بررسی کنید.</p>
<div id="results" class="cards"></div>
</section>
<section class="panel">
<b>روش تحلیل</b>
<p class="muted" style="font-size:12px;line-height:2">
جهت 4H: EMA50 و EMA200<br>
تأیید 1H: EMA20 و EMA50<br>
ورود 5m: RSI، کندل Engulfing و EMA20<br>
حد ضرر: ۱.۵ برابر ATR؛ اهداف: ۱R، ۲R و ۳R<br>
کارمزد تخمینی رفت‌وبرگشت در محاسبه اندازه موقعیت لحاظ می‌شود.
</p>
</section>
</main>
<footer>این ابزار صرفاً تحلیلی است؛ سفارش ثبت نمی‌کند و سود را تضمین نمی‌کند.</footer>
<script>
const API="https://fapi.binance.com";
const $=id=>document.getElementById(id);
const sleep=ms=>new Promise(r=>setTimeout(r,ms));

async function getJSON(url){
  const r=await fetch(url);
  if(!r.ok) throw new Error("HTTP "+r.status);
  return r.json();
}
function ema(a,n){
  if(a.length<n)return null;
  const k=2/(n+1);
  let v=a.slice(0,n).reduce((x,y)=>x+y,0)/n;
  for(let i=n;i<a.length;i++)v=a[i]*k+v*(1-k);
  return v;
}
function rsi(a,n=14){
  if(a.length<n+1)return null;
  let up=0,dn=0;
  for(let i=a.length-n;i<a.length;i++){
    const d=a[i]-a[i-1];
    if(d>0)up+=d;else dn-=d;
  }
  if(dn===0)return 100;
  return 100-(100/(1+up/dn));
}
function atr(k,n=14){
  if(k.length<n+1)return null;
  let s=0;
  for(let i=k.length-n;i<k.length;i++){
    const h=+k[i][2],l=+k[i][3],pc=+k[i-1][4];
    s+=Math.max(h-l,Math.abs(h-pc),Math.abs(l-pc));
  }
  return s/n;
}
function candles(raw){
  // آخرین کندل حذف می‌شود تا فقط کندل بسته‌شده تحلیل شود
  return raw.slice(0,-1).map(x=>({
    t:+x[6],o:+x[1],h:+x[2],l:+x[3],c:+x[4],v:+x[5]
  }));
}
function engulf(k){
  if(k.length<2)return "";
  const a=k[k.length-2],b=k[k.length-1];
  if(a.c<a.o && b.c>b.o && b.o<=a.c && b.c>=a.o)return "bull";
  if(a.c>a.o && b.c<b.o && b.o>=a.c && b.c<=a.o)return "bear";
  return "";
}
function fmt(x){
  if(!Number.isFinite(x))return "—";
  return x<1?x.toFixed(6):x.toFixed(4);
}
async function analyze(symbol){
  const [a,b,c]=await Promise.all([
    getJSON(`${API}/fapi/v1/klines?symbol=${symbol}&interval=4h&limit=220`),
    getJSON(`${API}/fapi/v1/klines?symbol=${symbol}&interval=1h&limit=220`),
    getJSON(`${API}/fapi/v1/klines?symbol=${symbol}&interval=5m&limit=100`)
  ]);
  const h4=candles(a),h1=candles(b),m5=candles(c);
  if(h4.length<200||h1.length<60||m5.length<30)throw Error("داده ناکافی");
  const p4=h4.map(x=>x.c),p1=h1.map(x=>x.c),p5=m5.map(x=>x.c);
  const e4a=ema(p4,50),e4b=ema(p4,200);
  const e1a=ema(p1,20),e1b=ema(p1,50),e5=ema(p5,20);
  const rv=rsi(p5),av=atr(m5),last=m5.at(-1);
  if(!av||!e5||rv===null)throw Error("اندیکاتور نامعتبر");
  const age=Date.now()-last.t;
  if(age>10*60*1000)throw Error("کندل ۵ دقیقه‌ای قدیمی است");

  let long=0,short=0;
  if(e4a>e4b && p4.at(-1)>e4a)long++;
  if(e4a<e4b && p4.at(-1)<e4a)short++;
  if(e1a>e1b)long++;
  if(e1a<e1b)short++;
  if(last.c>e5)long++;
  if(last.c<e5)short++;
  if(rv>=50&&rv<=70)long++;
  if(rv<=50&&rv>=30)short++;
  const pattern=engulf(m5);
  if(pattern==="bull")long++;
  if(pattern==="bear")short++;
  if(last.c>last.o)long++;
  if(last.c<last.o)short++;
  const volAvg=m5.slice(-21,-1).reduce((s,x)=>s+x.v,0)/20;
  if(last.v>volAvg*1.3){
    if(last.c>last.o)long++;
    if(last.c<last.o)short++;
  }
  const side=long>=short?"LONG":"SHORT";
  const score=Math.max(long,short);
  const aligned=(side==="LONG"&&e4a>e4b&&e1a>e1b)||
                (side==="SHORT"&&e4a<e4b&&e1a<e1b);
  const min=+$("threshold").value;
  let signal=score>=min&&aligned?side:"WAIT";
  const entry=last.c;
  const distance=av*1.5;
  const stop=side==="LONG"?entry-distance:entry+distance;
  const r=Math.abs(entry-stop);
  const capital=+$("capital").value;
  const risk=+$("risk").value;
  const lev=Math.max(1,+$("leverage").value);
  // کارمزد فرضی ۰.۰۶٪ برای هر سمت؛ مقدار واقعی صرافی ممکن است متفاوت باشد
  const feePerUnit=entry*0.0012;
  const qty=risk/(r+feePerUnit);
  const margin=qty*entry/lev;
  const maxMargin=capital*0.8;
  const safeQty=Math.min(qty,maxMargin*lev/entry);
  const actualRisk=safeQty*(r+feePerUnit);
  const target=(multiple)=>side==="LONG"?entry+r*multiple:entry-r*multiple;
  return {symbol,signal,side,score,long,short,entry,stop,
    tp1:target(1),tp2:target(2),tp3:target(3),
    qty:safeQty,margin:safeQty*entry/lev,actualRisk,
    rsi:rv,atr:av,pattern,aligned};
}
function card(x){
  const cls=x.signal==="LONG"?"long":x.signal==="SHORT"?"short":"wait";
  const title=x.signal==="WAIT"?"بدون سیگنال":x.signal;
  return `<article class="trade">
  <h3>${x.symbol} — <span class="${cls}">${title}</span></h3>
  <div class="muted" style="font-size:12px;margin-bottom:10px">امتیاز ${x.score}/7 | LONG ${x.long} — SHORT ${x.short}</div>
  <div class="metrics">
  ${metric("ورود",x.entry)}${metric("حد ضرر",x.stop)}
  ${metric("هدف اول",x.tp1)}${metric("هدف دوم",x.tp2)}
  ${metric("هدف سوم",x.tp3)}${metric("RSI",x.rsi.toFixed(1))}
  ${metric("حجم موقعیت",x.qty.toFixed(4))}${metric("مارجین تقریبی",x.margin.toFixed(2)+" USDT")}
  ${metric("ریسک تخمینی",x.actualRisk.toFixed(2)+" USDT")}${metric("ATR",fmt(x.atr))}
  </div>
  <p class="muted" style="font-size:11px">الگو: ${x.pattern||"ندارد"} | هم‌جهتی تایم‌فریم‌ها: ${x.aligned?"بله":"خیر"}</p>
  </article>`;
}
function metric(k,v){return `<div class="metric">${k}<b>${v}</b></div>`}
async function scan(){
  const btn=$("scan"),status=$("status"),out=$("results");
  btn.disabled=true;out.innerHTML="";
  try{
    status.textContent="دریافت فهرست قراردادها...";
    const info=await getJSON(API+"/fapi/v1/exchangeInfo");
    const tickers=await getJSON(API+"/fapi/v1/ticker/24hr");
    const valid=new Set(info.symbols.filter(s=>
      s.contractType==="PERPETUAL"&&s.quoteAsset==="USDT"&&s.status==="TRADING"
    ).map(s=>s.symbol));
    const list=tickers.filter(t=>valid.has(t.symbol))
      .sort((a,b)=>+b.quoteVolume-(+a.quoteVolume))
      .slice(0,+$("limit").value);
    const results=[];
    for(let i=0;i<list.length;i+=4){
      status.textContent=`تحلیل بازار: ${Math.min(i+4,list.length)} از ${list.length}`;
      const batch=await Promise.all(list.slice(i,i+4).map(async t=>{
        try{return await analyze(t.symbol)}catch(e){
          return {symbol:t.symbol,error:e.message};
        }
      }));
      results.push(...batch);
      await sleep(200);
    }
    results.sort((a,b)=>(b.score||0)-(a.score||0));
    const good=results.filter(x=>!x.error);
    out.innerHTML=good.map(card).join("")||
      "<p>داده قابل تحلیل دریافت نشد.</p>";
    const errors=results.filter(x=>x.error).length;
    status.textContent=`پایان اسکن | ${good.length} تحلیل موفق | ${errors} خطا`;
  }catch(e){
    status.textContent="خطا در دریافت داده: "+e.message;
  }finally{btn.disabled=false}
}
$("scan").addEventListener("click",scan);
if("serviceWorker" in navigator){
  window.addEventListener("load",()=>navigator.serviceWorker.register("./sw.js").catch(()=>{}));
}
</script>
</body>
</html>
