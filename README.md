# NEXORA
<!DOCTYPE html>
<html lang="kk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NEXORA — Smart City</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:Arial,sans-serif;background:#080e1b;color:#f4f7ff}
button,input,select,textarea{font:inherit}
button{cursor:pointer}
.app{display:flex;min-height:100vh}
.sidebar{width:230px;position:fixed;inset:0 auto 0 0;background:#0d1728;border-right:1px solid #26364d;padding:25px 17px;z-index:5}
.logo{font-size:23px;font-weight:900;letter-spacing:2px;margin:8px 5px 40px;color:#50e4dc}
.logo span{color:white}
.nav-title{font-size:10px;color:#70819c;letter-spacing:2px;margin:22px 10px 12px}
.nav button{display:block;width:100%;text-align:left;padding:13px;border:0;border-radius:11px;background:transparent;color:#a5b3c9;margin:5px 0;font-size:13px}
.nav button:hover,.nav button.active{background:#1b3048;color:#50e4dc}
.sidebar-bottom{position:absolute;bottom:25px;left:17px;right:17px;background:#142238;border:1px solid #2b405b;padding:15px;border-radius:14px;font-size:11px;color:#9cacc3}
.sidebar-bottom b{color:#50e4dc}
.main{margin-left:230px;padding:28px;width:calc(100% - 230px);max-width:1600px}
.topbar{display:flex;justify-content:space-between;align-items:center;gap:15px;margin-bottom:25px}
.topbar small{color:#50e4dc;letter-spacing:2px;font-size:10px}
h1{font-size:27px;margin-top:8px}
.top-right{display:flex;gap:9px;align-items:center}
.search{background:#121e31;border:1px solid #2a3b54;border-radius:10px;padding:11px;color:white;width:190px}
.avatar{width:39px;height:39px;border-radius:12px;background:linear-gradient(135deg,#50e4dc,#788cff);display:grid;place-items:center;color:#08111c;font-weight:bold}
.section{display:none;animation:show .3s}
.section.active{display:block}
@keyframes show{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
.hero{padding:27px;border-radius:20px;border:1px solid #334e69;background:linear-gradient(110deg,#16344b,#1b2445,#2b2750);margin-bottom:18px;display:flex;justify-content:space-between;align-items:center;gap:15px;overflow:hidden}
.hero small{color:#50e4dc;letter-spacing:2px;font-weight:bold}
.hero h2{font-size:25px;margin:14px 0 9px}
.hero p{color:#bdc9dc;font-size:12px;line-height:1.7;max-width:470px}
.hero-time{text-align:right;min-width:115px}
.hero-time strong{font-size:30px;display:block}
.hero-time span{font-size:10px;color:#b1bfd3}
.btn{border:0;border-radius:10px;padding:11px 15px;background:linear-gradient(100deg,#50e4dc,#83b7ff);color:#08121c;font-weight:bold;font-size:11px;margin-top:15px}
.stats{display:grid;grid-template-columns:repeat(4,1fr);gap:13px;margin-bottom:18px}
.card{background:linear-gradient(145deg,#152239,#101a2a);border:1px solid #293b54;border-radius:16px;padding:18px;min-width:0}
.stat-top{display:flex;justify-content:space-between;color:#9babc3;font-size:11px}
.stat-icon{font-size:20px}
.stat h2{font-size:27px;margin:15px 0 6px}
.green{color:#50e4dc;font-size:10px}
.grid{display:grid;grid-template-columns:1.3fr 1fr;gap:15px;margin-bottom:17px}
.card-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:18px}
.card-head h3{font-size:14px}
.card-head span{color:#8799b3;font-size:10px}
.chart{height:170px;display:flex;align-items:end;gap:12px;border-bottom:1px solid #293b54;padding:0 5px}
.bar-wrap{height:100%;display:flex;flex-direction:column;justify-content:end;align-items:center;gap:8px;flex:1}
.bar{width:100%;max-width:34px;border-radius:7px 7px 2px 2px;background:linear-gradient(180deg,#50e4dc,#557bda);min-height:5px}
.bar-wrap small{font-size:9px;color:#899ab4}
.map{height:220px;border-radius:13px;position:relative;overflow:hidden;background-color:#102039;background-image:linear-gradient(30deg,transparent 47%,#36516a 48%,#36516a 50%,transparent 51%),linear-gradient(120deg,transparent 47%,#36516a 48%,#36516a 50%,transparent 51%);background-size:80px 80px}
.pin{position:absolute;width:16px;height:16px;border-radius:50%;background:#50e4dc;box-shadow:0 0 0 7px #50e4dc22,0 0 20px #50e4dc;cursor:pointer}
.pin.one{left:20%;top:25%}.pin.two{left:60%;top:55%;background:#b18aff}.pin.three{left:80%;top:20%;background:#ffbf69}.pin.four{left:35%;top:75%;background:#7194ff}
.map-label{position:absolute;background:#0b1729;color:white;padding:6px 8px;border-radius:6px;font-size:9px}
.map-label.one{left:12%;top:40%}.map-label.two{left:53%;top:68%}.map-label.three{right:3%;top:33%}
.system-list{display:grid;gap:10px}
.system{display:flex;align-items:center;gap:10px;background:#1a2a41;padding:11px;border-radius:11px}
.system-icon{font-size:19px}
.system-info{flex:1}
.system-info b{font-size:11px;display:block}
.system-info small{font-size:9px;color:#91a0b9}
.switch{width:38px;height:21px;border:0;border-radius:20px;background:#485a70;position:relative;flex-shrink:0}
.switch:after{content:"";position:absolute;left:3px;top:3px;width:15px;height:15px;background:white;border-radius:50%;transition:.2s}
.switch.on{background:#50e4dc}
.switch.on:after{left:20px;background:#10202b}
.activity{display:grid;gap:13px}
.activity-item{display:flex;gap:11px}
.activity-icon{width:32px;height:32px;background:#253a55;border-radius:9px;display:grid;place-items:center}
.activity-item b{font-size:11px}
.activity-item p{font-size:10px;color:#91a0b9;margin-top:5px}
.activity-item small{font-size:9px;color:#657994}
.page-title{margin-bottom:20px}
.page-title h2{font-size:23px}
.page-title p{font-size:11px;color:#91a0b9;margin-top:8px}
.feature-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:14px}
.feature{padding:22px;background:#142138;border:1px solid #293b54;border-radius:16px}
.feature span{font-size:27px}
.feature h3{font-size:13px;margin:14px 0 8px}
.feature p{font-size:10px;color:#91a0b9;line-height:1.7}
.form-card{max-width:650px}
label{display:block;font-size:11px;color:#a9b8ce;margin:14px 0 7px}
input,select,textarea{width:100%;padding:12px;border-radius:9px;background:#0c1728;color:white;border:1px solid #2a3b54;outline:none}
textarea{min-height:100px}
.report-list{display:grid;gap:10px;margin-top:18px}
.report{background:#17253a;border:1px solid #2a3b54;padding:14px;border-radius:11px;font-size:11px}
.report small{display:block;color:#50e4dc;margin-top:7px}
.table{width:100%;border-collapse:collapse;font-size:11px}
.table td,.table th{text-align:left;padding:13px 8px;border-bottom:1px solid #293b54}
.table th{color:#91a0b9;font-weight:normal}
.toast{position:fixed;bottom:20px;right:20px;background:#1b3547;border:1px solid #50e4dc;padding:14px 18px;border-radius:12px;font-size:12px;display:none;z-index:20}
@media(max-width:950px){.sidebar{width:190px}.main{margin-left:190px;width:calc(100% - 190px);padding:20px}.stats{grid-template-columns:repeat(2,1fr)}.grid{grid-template-columns:1fr}.feature-grid{grid-template-columns:repeat(2,1fr)}}
@media(max-width:650px){.sidebar{width:65px;padding:20px 8px}.logo{font-size:0;margin:5px 4px 30px}.logo:after{content:"N";font-size:21px}.nav-title,.sidebar-bottom{display:none}.nav button{font-size:0;text-align:center;padding:13px 4px}.nav button span{font-size:19px;width:auto}.main{margin-left:65px;width:calc(100% - 65px);padding:15px 12px}.topbar{align-items:flex-start}.topbar h1{font-size:20px}.search{width:105px;font-size:10px}.hero{padding:19px}.hero h2{font-size:20px}.hero-time strong{font-size:22px}.stats{gap:8px}.stat{padding:13px}.stat h2{font-size:22px}.feature-grid{grid-template-columns:1fr}.grid{grid-template-columns:1fr}.top-right{gap:5px}}
</style>
</head>
<body>
<div class="app">
<aside class="sidebar">
 <div class="logo">◈ <span>NEXORA</span></div>
 <div class="nav-title">БАСҚАРУ</div>
 <div class="nav">
  <button class="active" onclick="go('home',this)"><span>▦</span> Басты бет</button>
  <button onclick="go('map',this)"><span>⌖</span> Қала картасы</button>
  <button onclick="go('systems',this)"><span>◉</span> Smart жүйелер</button>
  <button onclick="go('analytics',this)"><span>▥</span> Аналитика</button>
  <button onclick="go('reports',this)"><span>✉</span> Өтініштер</button>
  <button onclick="go('about',this)"><span>✧</span> Жоба туралы</button>
 </div>
 <div class="sidebar-bottom"><b>● Жүйе белсенді</b><p>Барлық демонстрациялық модульдер жұмыс істеп тұр.</p></div>
</aside>

<main class="main">
<header class="topbar">
 <div><small>SMART CITY PLATFORM</small><h1 id="heading">Қала бақылау орталығы</h1></div>
 <div class="top-right">
  <input class="search" id="search" placeholder="Іздеу..." oninput="searchContent()">
  <button class="icon-btn" onclick="notify()">♧</button>
  <div class="avatar">N</div>
 </div>
</header>

<section class="section active" id="home">
 <div class="hero">
  <div><small>✦ NEXORA DIGITAL CITY</small><h2>Болашақ қаласы<br>бүгіннен басталады.</h2><p>Қалалық инфрақұрылымды бір орталықтан бақылау, басқару және талдау платформасы.</p><button onclick="goByName('systems')">Жүйелерді басқару →</button></div>
  <div class="hero-time"><strong id="clock">00:00</strong><span id="date">Күн жүктелуде...</span></div>
 </div>
 <div class="stats">
  <div class="stat"><div class="stat-top">Ауа сапасы <span class="stat-icon">🌿</span></div><h2>92 AQI</h2><div class="green">● Жақсы көрсеткіш</div></div>
  <div class="stat"><div class="stat-top">Энергия <span class="stat-icon">⚡</span></div><h2>68.4 <small style="font-size:12px">МВт</small></h2><div class="green">↓ 4.2% үнемдеу</div></div>
  <div class="stat"><div class="stat-top">Көлік ағыны <span class="stat-icon">🚘</span></div><h2>1,284</h2><div class="green">Қалыпты қозғалыс</div></div>
  <div class="stat"><div class="stat-top">Өтініштер <span class="stat-icon">📩</span></div><h2 id="reportCount">24</h2><div class="green">Жалпы өтініш саны</div></div>
 </div>
 <div class="grid">
  <div class="card"><div class="card-head"><h3>⚡ Энергия тұтыну</h3><span>Апталық есеп</span></div><div class="chart" id="chart"></div><p style="font-size:10px;color:#91a0b9;margin-top:13px">Энергия көрсеткіштері — демонстрациялық мәліметтер</p></div>
  <div class="card"><div class="card-head"><h3>🗺 Қала картасы</h3><span>Интерактивті</span></div><div class="map"><div class="pin one" onclick="toast('Орталық аудан таңдалды')"></div><div class="pin two" onclick="toast('Жаңа аудан таңдалды')"></div><div class="pin three" onclick="toast('Солтүстік аудан таңдалды')"></div><div class="pin four" onclick="toast('Оңтүстік аудан таңдалды')"></div><div class="map-label one">Орталық</div><div class="map-label two">Жаңа аудан</div><div class="map-label three">Солтүстік</div></div></div>
 </div>
 <div class="grid">
  <div class="card"><div class="card-head"><h3>◉ Ақылды жүйелер</h3><span>Басқару</span></div><div class="system-list" id="homeSystems"></div></div>
  <div class="card"><div class="card-head"><h3>🔔 Соңғы оқиғалар</h3><span>Жаңартулар</span></div><div class="activity"><div class="activity-item"><div class="activity-icon">💡</div><div><b>Көше жарығы жаңартылды</b><p>Орталық аудан жүйесі қосылды</p><small>10 минут бұрын</small></div></div><div class="activity-item"><div class="activity-icon">🌱</div><div><b>Экобақылау белсенді</b><p>Ауа сапасы көрсеткіші қалыпты</p><small>35 минут бұрын</small></div></div><div class="activity-item"><div class="activity-icon">🚦</div><div><b>Бағдаршам жүйесі</b><p>Қозғалыс автоматты бақылануда</p><small>1 сағат бұрын</small></div></div></div></div>
 </div>
</section>

<section class="section" id="map">
 <div class="page-title"><h2>Қала картасы</h2><p>Қалалық аудандар мен бақылау нүктелері</p></div>
 <div class="card"><div class="card-head"><h3>Интерактивті карта</h3><span>Демонстрациялық карта</span></div><div class="map" style="height:390px"><div class="pin one" onclick="toast('Орталық аудан: барлық жүйе қалыпты')"></div><div class="pin two" onclick="toast('Шығыс аудан: бақылау белсенді')"></div><div class="pin three" onclick="toast('Солтүстік аудан: ауа сапасы жақсы')"></div><div class="pin four" onclick="toast('Оңтүстік аудан: жарық жүйесі белсенді')"></div><div class="map-label one">Орталық аудан</div><div class="map-label two">Шығыс аудан</div><div class="map-label three">Солтүстік аудан</div></div><p style="font-size:11px;color:#91a0b9;margin-top:14px">Картадағы нүктелерді басып, аудандар туралы ақпарат алыңыз.</p></div>
</section>

<section class="section" id="systems">
 <div class="page-title"><h2>Ақылды басқару жүйелері</h2><p>Қалалық қызметтерді қосу немесе өшіру</p></div>
 <div class="card"><div class="system-list" id="allSystems"></div></div>
</section>

<section class="section" id="analytics">
 <div class="page-title"><h2>Қалалық аналитика</h2><p>Негізгі көрсеткіштер мен статистикалық мәліметтер</p></div>
 <div class="stats">
  <div class="stat"><div class="stat-top">Энергия үнемдеу</div><h2>18.6%</h2><div class="green">Оң көрсеткіш</div></div>
  <div class="stat"><div class="stat-top">Экология индексі</div><h2>92/100</h2><div class="green">Жақсы деңгей</div></div>
  <div class="stat"><div class="stat-top">Жүйе белсенділігі</div><h2 id="activeCount">4/4</h2><div class="green">Басқару модульдері</div></div>
  <div class="stat"><div class="stat-top">Өтініштер</div><h2 id="analyticsReports">24</h2><div class="green">Тіркелген саны</div></div>
 </div>
 <div class="card"><div class="card-head"><h3>Апталық энергия графигі</h3><span>МВт</span></div><div class="chart" id="chart2"></div></div>
</section>

<section class="section" id="reports">
 <div class="page-title"><h2>Тұрғындар өтініші</h2><p>Қаладағы мәселе туралы хабарлама қалдырыңыз</p></div>
 <div class="card form-card">
  <h3 style="font-size:15px">Жаңа өтініш жіберу</h3>
  <form id="reportForm">
   <label>Аты-жөніңіз</label><input id="person" required placeholder="Атыңызды енгізіңіз">
   <label>Мәселе түрі</label><select id="type"><option>Көше жарығы</option><option>Жол мәселесі</option><option>Қоқыс және тазалық</option><option>Су жүйесі</option><option>Экология</option><option>Басқа мәселе</option></select>
   <label>Аудан</label><select id="district"><option>Орталық аудан</option><option>Солтүстік аудан</option><option>Оңтүстік аудан</option><option>Шығыс аудан</option></select>
   <label>Мәселенің сипаттамасы</label><textarea id="description" required placeholder="Мәселені толық сипаттаңыз..."></textarea>
   <button class="btn" type="submit">Өтініш жіберу →</button>
  </form>
 </div>
 <div class="card" style="margin-top:17px"><div class="card-head"><h3>Соңғы өтініштер</h3><span>Сақталған тізім</span></div><div class="report-list" id="reportsList"></div></div>
</section>

<section class="section" id="about">
 <div class="page-title"><h2>NEXORA жобасы</h2><p>Цифрлық қаланың жаңа басқару моделі</p></div>
 <div class="hero"><div><small>OUR MISSION</small><h2>Ақылды қала. Қауіпсіз өмір.</h2><p>NEXORA — қалалық инфрақұрылымды цифрлық технологиялар арқылы басқаруға арналған веб-платформа үлгісі.</p></div><div style="font-size:65px">🏙️</div></div>
 <div class="feature-grid">
  <div class="feature"><span>🌐</span><h3>Бір орталықтан басқару</h3><p>Қаланың негізгі қызметтерін бір интерфейсте бақылау.</p></div>
  <div class="feature"><span>📊</span><h3>Деректер аналитикасы</h3><p>Көрсеткіштерді графиктер арқылы талдау.</p></div>
  <div class="feature"><span>🚦</span><h3>Ақылды инфрақұрылым</h3><p>Жарық, бағдаршам және су жүйелерін басқару.</p></div>
  <div class="feature"><span>🌱</span><h3>Экологиялық бақылау</h3><p>Қоршаған орта сапасын бақылау модулі.</p></div>
  <div class="feature"><span>📩</span><h3>Тұрғындармен байланыс</h3><p>Өтініш қабылдау және оларды сақтау.</p></div>
  <div class="feature"><span>🔐</span><h3>Цифрлық қауіпсіздік</h3><p>Басқару жүйесінің интерфейсіндегі қауіпсіздік бөлімі.</p></div>
 </div>
 <div class="card" style="margin-top:17px"><h3 style="font-size:14px">Технологиялар</h3><p style="font-size:12px;color:#91a0b9;margin-top:12px;line-height:2">HTML5 — сайт құрылымы<br>CSS3 — заманауи дизайн және анимация<br>JavaScript — интерактивті функциялар<br>LocalStorage — өтініштерді браузерде сақтау</p></div>
</section>
</main>
</div>
<div class="toast" id="toast"></div>

<script>
const systems=[
 {icon:"💡",name:"Көше жарығы",desc:"Ақылды жарықтандыру"},
 {icon:"🚦",name:"Бағдаршам жүйесі",desc:"Көлік қозғалысын басқару"},
 {icon:"💧",name:"Су мониторингі",desc:"Су жүйесін бақылау"},
 {icon:"🌿",name:"Экобақылау",desc:"Қоршаған ортаны бақылау"}
];
let enabled=[true,true,true,true];
function renderSystems(){
 const html=systems.map((s,i)=>`<div class="system"><div class="sys-icon">${s.icon}</div><div class="system-info"><b>${s.name}</b><small>${s.desc}</small></div><button class="switch ${enabled[i]?'on':''}" onclick="toggleSystem(${i})" aria-label="${s.name} қосу немесе өшіру"></button></div>`).join("");
 document.getElementById("homeSystems").innerHTML=html;
 document.getElementById("allSystems").innerHTML=html;
 document.getElementById("activeCount").textContent=enabled.filter(Boolean).length+"/4";
}
function toggleSystem(i){enabled[i]=!enabled[i];renderSystems();toast(systems[i].name+(enabled[i]?" қосылды":" өшірілді"))}
function go(id,button){
 document.querySelectorAll(".section").forEach(s=>s.classList.remove("active"));
 document.getElementById(id).classList.add("active");
 document.querySelectorAll(".nav button").forEach(b=>b.classList.remove("active"));
 if(button)button.classList.add("active");
 const names={home:"Қала бақылау орталығы",map:"Қала картасы",systems:"Ақылды жүйелер",analytics:"Қалалық аналитика",reports:"Тұрғындар өтініші",about:"Жоба туралы"};
 document.getElementById("heading").textContent=names[id];
}
function goByName(id){go(id,document.querySelectorAll(".nav button")[2])}
function toast(msg){
 const t=document.getElementById("toast");t.textContent=msg;t.style.display="block";
 clearTimeout(window.toastTimer);window.toastTimer=setTimeout(()=>t.style.display="none",2500);
}
function notify(){toast("🔔 Жаңа хабарламалар жоқ")}
function updateClock(){
 const d=new Date();
 document.getElementById("clock").textContent=d.toLocaleTimeString("kk-KZ",{hour:"2-digit",minute:"2-digit"});
 document.getElementById("date").textContent=d.toLocaleDateString("kk-KZ",{day:"numeric",month:"long",weekday:"long"});
}
setInterval(updateClock,1000);updateClock();
const values=[45,70,55,88,63,76,48];
function drawChart(id){
 document.getElementById(id).innerHTML=values.map((v,i)=>`<div class="bar-wrap"><div class="bar" style="height:${v}%"></div><small>${["Дс","Сс","Ср","Бс","Жм","Сб","Жс"][i]}</small></div>`).join("");
}
drawChart("chart");drawChart("chart2");
function getReports(){try{return JSON.parse(localStorage.getItem("nexoraReports")||"[]")}catch(e){return []}}
function renderReports(){
 const list=getReports();
 document.getElementById("reportCount").textContent=24+list.length;
 document.getElementById("analyticsReports").textContent=24+list.length;
 document.getElementById("reportsList").innerHTML=list.length?list.slice().reverse().map(r=>`<div class="report"><b>${escapeHTML(r.type)}</b> — ${escapeHTML(r.district)}<p style="color:#aab8ce;margin-top:7px">${escapeHTML(r.description)}</p><small>${escapeHTML(r.person)} · ${escapeHTML(r.date)}</small></div>`).join(""):'<p style="color:#91a0b9;font-size:11px">Әзірге жаңа өтініш жоқ.</p>';
}
function escapeHTML(s){return String(s).replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]))}
document.getElementById("reportForm").addEventListener("submit",e=>{
 e.preventDefault();
 const list=getReports();
 list.push({
 person:document.getElementById("person").value.trim(),
 type:document.getElementById("type").value,
 district:document.getElementById("district").value,
 description:document.getElementById("description").value.trim(),
 date:new Date().toLocaleString("kk-KZ")
 });
 try{localStorage.setItem("nexoraReports",JSON.stringify(list))}
 catch(err){toast("Сақтау мүмкін болмады. Браузер жадысын тексеріңіз.");return}
 e.target.reset();renderReports();toast("✓ Өтініш сәтті сақталды!");
});
function searchContent(){
 const q=document.getElementById("search").value.toLowerCase().trim();
 if(!q)return;
 const match=[...document.querySelectorAll(".nav button")].find(b=>b.textContent.toLowerCase().includes(q));
 if(match)match.click();
}
renderSystems();renderReports();
</script>
</body>
</html>
