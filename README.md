<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TechLab Academy · IA Básico 1</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;600;700&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@500;600&display=swap" rel="stylesheet">
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
<style>
:root{
  --bg: #0B0D12;
  --panel: #12151C;
  --card: #171B24;
  --card-2: #1D2230;
  --border: #252A35;
  --border-soft: #1C212B;
  --text: #FFFFFF;
  --text-dim: #9299A8;
  --text-faint: #5C6270;
  --violet: #7C6FFF;
  --violet-soft: rgba(124,111,255,.14);
  --blue: #4F8CFF;
  --cyan: #34E4C9;
  --amber: #F2B84B;
  --red: #FF6B6B;
  --grad: linear-gradient(135deg,#7C6FFF 0%, #4F8CFF 55%, #34E4C9 100%);
  --radius-lg: 20px;
  --radius-md: 14px;
  --radius-sm: 10px;
  --shadow-card: 0 1px 0 rgba(255,255,255,.02) inset, 0 14px 32px -16px rgba(0,0,0,.65);
  --shadow-glow: 0 0 0 1px rgba(124,111,255,.28), 0 14px 36px -10px rgba(124,111,255,.4);
  --font-display: 'Space Grotesk', sans-serif;
  --font-body: 'Inter', sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
  --sidebar-w: 272px;
}
*,*::before,*::after{box-sizing:border-box}
html,body{height:100%; margin:0;}
body{
  background:
    radial-gradient(1100px 520px at 88% -8%, rgba(124,111,255,.18), transparent 60%),
    radial-gradient(900px 480px at -10% 8%, rgba(52,228,201,.09), transparent 55%),
    var(--bg);
  color:var(--text);
  font-family:var(--font-body);
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
}
h1,h2,h3,h4{font-family:var(--font-display); margin:0; letter-spacing:-.01em; color:var(--text);}
p{margin:0}
button{font-family:inherit; cursor:pointer; -webkit-appearance:none; appearance:none;}
input,textarea{font-family:inherit; -webkit-appearance:none; appearance:none;}
.mono{font-family:var(--font-mono); font-variant-numeric:tabular-nums;}
::selection{background:var(--violet-soft)}
a{color:inherit; text-decoration:none;}
i[data-lucide]{display:block;}
svg{display:block;}
:focus-visible{outline:2px solid var(--cyan); outline-offset:2px; border-radius:6px;}
table{border-collapse:collapse; width:100%;}

.app{display:flex; min-height:100vh; width:100%;}
.sidebar-overlay{position:fixed; inset:0; background:rgba(4,6,10,.65); backdrop-filter:blur(2px); z-index:40; opacity:0; pointer-events:none; transition:opacity .25s ease;}
.app.sidebar-open .sidebar-overlay{opacity:1; pointer-events:auto;}
.sidebar{
  width:var(--sidebar-w); flex-shrink:0;
  background:linear-gradient(180deg, var(--panel), var(--bg));
  border-right:1px solid var(--border-soft);
  display:flex; flex-direction:column;
  position:sticky; top:0; height:100vh; z-index:50;
}
.sidebar-brand{display:flex; align-items:center; gap:11px; padding:24px 20px 20px;}
.brand-mark{width:38px;height:38px;border-radius:11px; background:var(--grad); display:flex;align-items:center;justify-content:center; color:#0A0D14; flex-shrink:0; box-shadow:var(--shadow-glow);}
.brand-text{display:flex; flex-direction:column; line-height:1.15; min-width:0;}
.brand-name{font-family:var(--font-display); font-weight:700; font-size:15.5px; color:#fff; white-space:nowrap;}
.brand-sub{font-size:11px; color:var(--text-faint); letter-spacing:.07em; text-transform:uppercase;}
.sidebar-close{display:none; margin-left:auto; background:none; border:none; color:var(--text-dim); padding:6px;}
.sidebar-nav{display:flex; flex-direction:column; gap:3px; padding:10px 14px; overflow-y:auto;}
.nav-item{display:flex; align-items:center; gap:12px; background:none; border:none; color:var(--text-dim); padding:11px 13px; border-radius:var(--radius-sm); font-size:14px; font-weight:500; text-align:left; transition:background .15s ease, color .15s ease;}
.nav-icon{display:flex; opacity:.85; flex-shrink:0;}
.nav-item:hover{background:var(--card); color:var(--text);}
.nav-item.active{background:var(--violet-soft); color:#fff; box-shadow:inset 0 0 0 1px rgba(124,111,255,.4);}
.nav-item.active .nav-icon{color:var(--cyan); opacity:1;}
.sidebar-footer{margin-top:auto; padding:16px 20px 24px;}
.mini-progress{background:var(--card); border:1px solid var(--border-soft); border-radius:var(--radius-md); padding:13px 15px;}
.mini-progress-head{display:flex; justify-content:space-between; font-size:11.5px; color:var(--text-dim); margin-bottom:9px;}
.bar{height:6px; border-radius:99px; background:var(--card-2); overflow:hidden;}
.bar-fill{height:100%; border-radius:99px; background:var(--grad); width:0%; transition:width .5s ease;}
.main{flex:1; min-width:0; display:flex; flex-direction:column;}

.topbar{display:flex; align-items:center; gap:16px; padding:16px 30px; border-bottom:1px solid var(--border-soft); background:rgba(11,13,18,.75); backdrop-filter:blur(12px); position:sticky; top:0; z-index:30;}
.menu-toggle{display:none;}
.icon-btn{width:40px;height:40px; border-radius:11px; border:1px solid var(--border-soft); background:var(--card); color:var(--text-dim); display:flex; align-items:center;justify-content:center; position:relative; flex-shrink:0; transition:border-color .15s ease, color .15s ease;}
.icon-btn:hover{color:var(--text); border-color:var(--border);}
.icon-btn .dot{position:absolute; top:9px; right:10px; width:6px;height:6px;border-radius:50%; background:var(--cyan); box-shadow:0 0 0 2px var(--card);}
.topbar-title{font-family:var(--font-display); font-weight:600; font-size:15.5px; white-space:nowrap; display:none; color:#fff;}
.search-wrap{flex:1; max-width:440px; display:flex; align-items:center; gap:10px; background:var(--card); border:1px solid var(--border-soft); border-radius:12px; padding:10px 15px; color:var(--text-faint);}
.search-wrap i{flex-shrink:0;}
.search-wrap input{background:none; border:none; outline:none; color:var(--text); font-size:13.5px; width:100%;}
.search-wrap input::placeholder{color:var(--text-faint);}
.topbar-actions{display:flex; align-items:center; gap:10px; margin-left:auto;}
.profile-btn{display:flex; align-items:center; gap:10px; background:var(--card); border:1px solid var(--border-soft); border-radius:12px; padding:6px 13px 6px 6px; color:var(--text); transition:border-color .15s ease;}
.profile-btn:hover{border-color:var(--border);}
.avatar{width:29px;height:29px;border-radius:9px; background:var(--grad); color:#0A0D14; font-family:var(--font-display); font-weight:700; font-size:11.5px; display:flex; align-items:center; justify-content:center; flex-shrink:0;}
.profile-name{font-size:13.5px; font-weight:500; white-space:nowrap;}
.dropdown-wrap{position:relative;}
.dropdown{position:absolute; top:calc(100% + 10px); right:0; width:252px; background:var(--card-2); border:1px solid var(--border); border-radius:var(--radius-md); box-shadow:0 22px 44px -12px rgba(0,0,0,.6); padding:9px; opacity:0; transform:translateY(-6px) scale(.98); pointer-events:none; transition:all .16s ease; z-index:60;}
.dropdown.open{opacity:1; transform:none; pointer-events:auto;}
.dropdown-head{font-size:11px; text-transform:uppercase; letter-spacing:.06em; color:var(--text-faint); padding:8px 10px 6px;}
.dropdown-link{display:flex; align-items:center; gap:9px; width:100%; text-align:left; background:none; border:none; color:var(--text-dim); font-size:13.5px; padding:10px; border-radius:9px;}
.dropdown-link:hover{background:var(--card); color:var(--text);}
.dropdown-link i{width:15px; height:15px; flex-shrink:0;}
.notif-item{display:flex; gap:11px; padding:10px; border-radius:9px;}
.notif-item:hover{background:var(--card);}
.notif-item strong{font-size:13px; display:block; color:#fff; font-weight:600;}
.notif-item p{font-size:12px; color:var(--text-dim); margin-top:2px;}
.notif-dot{width:8px;height:8px;border-radius:50%; background:var(--violet); margin-top:5px; flex-shrink:0;}
.notif-dot.ok{background:var(--cyan);}
.notif-dot.warn{background:var(--amber);}
.content{padding:30px; max-width:1200px; width:100%; margin:0 auto;}

.eyebrow{font-size:11.5px; font-weight:600; letter-spacing:.09em; text-transform:uppercase; color:var(--cyan);}
.page-head{margin-bottom:26px;}
.page-head h1{font-size:27px; margin-top:7px;}
.page-head p{color:var(--text-dim); font-size:14.5px; margin-top:7px; max-width:680px; line-height:1.55;}
.card{background:var(--card); border:1px solid var(--border-soft); border-radius:var(--radius-lg); box-shadow:var(--shadow-card);}
.btn{display:inline-flex; align-items:center; gap:8px; justify-content:center; border-radius:12px; padding:12px 22px; font-size:13.5px; font-weight:600; border:1px solid transparent; transition:transform .12s ease, box-shadow .12s ease, filter .12s ease, border-color .12s ease; white-space:nowrap;}
.btn:active{transform:scale(.98);}
.btn-primary{background:var(--grad); color:#08090D; box-shadow:var(--shadow-glow);}
.btn-primary:hover{filter:brightness(1.08);}
.btn-ghost{background:var(--card-2); border-color:var(--border); color:var(--text);}
.btn-ghost:hover{border-color:var(--violet);}
.btn-sm{padding:9px 15px; font-size:12.5px; border-radius:10px;}
.btn:disabled{opacity:.4; cursor:not-allowed;}
.btn i{width:16px; height:16px;}

.hero{position:relative; overflow:hidden; padding:32px; display:grid; grid-template-columns:1.3fr 1fr; gap:30px; align-items:center;}
.hero::before{content:""; position:absolute; inset:0; background:var(--grad); opacity:.07; pointer-events:none;}
.hero-greeting{font-size:24px; margin-top:9px; color:#fff;}
.hero-greeting span{color:var(--cyan);}
.hero-sub{color:var(--text-dim); font-size:14px; margin-top:9px; max-width:430px; line-height:1.55;}
.hero-cta{margin-top:24px; display:flex; align-items:center; gap:15px; flex-wrap:wrap;}
.hero-cta-note{font-size:12.5px; color:var(--text-faint);}
.hero-ring-wrap{display:flex; flex-direction:column; align-items:center; gap:11px; justify-self:end;}
.ring-percent{position:relative; width:152px; height:152px;}
.ring-percent svg{transform:rotate(-90deg);}
.ring-percent .ring-num{position:absolute; inset:0; display:flex; align-items:center; justify-content:center; flex-direction:column;}
.ring-percent .ring-num b{font-family:var(--font-display); font-size:27px; color:#fff;}
.ring-percent .ring-num small{font-size:10.5px; color:var(--text-faint); letter-spacing:.05em; text-transform:uppercase;}
.ring-label{font-size:12px; color:var(--text-dim);}

.stat-row{display:grid; grid-template-columns:repeat(4,1fr); gap:16px; margin-top:22px;}
.stat-card{padding:19px; display:flex; flex-direction:column; gap:7px; transition:border-color .15s ease, transform .15s ease;}
.stat-card:hover{border-color:var(--border); transform:translateY(-2px);}
.stat-card .stat-icon{width:34px;height:34px;border-radius:10px; display:flex;align-items:center;justify-content:center; margin-bottom:4px;}
.stat-card .stat-icon i{width:17px; height:17px;}
.stat-card .stat-icon.v{background:var(--violet-soft); color:var(--violet);}
.stat-card .stat-icon.c{background:rgba(52,228,201,.14); color:var(--cyan);}
.stat-card .stat-icon.a{background:rgba(242,184,75,.14); color:var(--amber);}
.stat-card .stat-icon.b{background:rgba(79,140,255,.14); color:var(--blue);}
.stat-value{font-family:var(--font-display); font-size:21px; color:#fff;}
.stat-label{font-size:12.5px; color:var(--text-dim);}

.continue-card{margin-top:22px; padding:20px 22px; display:flex; align-items:center; gap:18px; transition:border-color .15s ease; cursor:pointer;}
.continue-card:hover{border-color:var(--violet);}
.continue-thumb{width:66px;height:66px; border-radius:14px; background:var(--grad); flex-shrink:0; display:flex; align-items:center; justify-content:center; color:#0A0D14; box-shadow:var(--shadow-glow);}
.continue-thumb i{width:26px; height:26px;}
.continue-info{flex:1; min-width:0;}
.continue-info .tag{font-size:11px; color:var(--text-faint); text-transform:uppercase; letter-spacing:.05em; font-weight:600;}
.continue-info h4{font-size:16px; margin-top:4px; color:#fff;}
.continue-info p{font-size:12.5px; color:var(--text-dim); margin-top:4px;}

.section-title{display:flex; align-items:center; justify-content:space-between; margin:36px 0 17px;}
.section-title h2{font-size:19px; color:#fff;}
.section-title .link-btn{font-size:12.5px; color:var(--violet); background:none; border:none; font-weight:600; display:flex; align-items:center; gap:4px;}
.section-title .link-btn i{width:14px; height:14px;}

.unit-path{display:flex; flex-direction:column; gap:0; margin-top:6px;}
.unit-node-row{display:flex; align-items:stretch; gap:0;}
.unit-node-col{display:flex; flex-direction:column; align-items:center; width:46px; flex-shrink:0;}
.unit-node{width:37px;height:37px;border-radius:50%; display:flex;align-items:center;justify-content:center; font-family:var(--font-mono); font-size:12px; font-weight:600; flex-shrink:0; border:2px solid var(--border); background:var(--card-2); color:var(--text-faint); z-index:2;}
.unit-node i{width:15px; height:15px;}
.unit-node.done{border-color:var(--cyan); background:rgba(52,228,201,.12); color:var(--cyan);}
.unit-node.active{border-color:var(--violet); background:var(--violet-soft); color:#fff; box-shadow:0 0 0 4px var(--violet-soft);}
.unit-connector{width:2px; flex:1; min-height:24px; background:var(--border); margin:2px 0;}
.unit-connector.done{background:var(--cyan);}

.units-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(300px,1fr)); gap:18px;}
.unit-card{padding:22px; display:flex; flex-direction:column; gap:12px; cursor:pointer; transition:border-color .15s ease, transform .15s ease, box-shadow .15s ease;}
.unit-card:hover{border-color:var(--violet); transform:translateY(-3px); box-shadow:0 18px 34px -16px rgba(124,111,255,.35);}
.unit-card-top{display:flex; align-items:flex-start; justify-content:space-between; gap:10px;}
.unit-badge{width:40px;height:40px;border-radius:11px; background:var(--violet-soft); color:var(--violet); display:flex; align-items:center; justify-content:center; font-family:var(--font-mono); font-weight:600; font-size:13px; flex-shrink:0;}
.unit-card h3{font-size:15.5px; line-height:1.35; color:#fff;}
.unit-card .unit-weeks{font-size:11px; color:var(--text-faint); text-transform:uppercase; letter-spacing:.04em; font-weight:600; margin-top:-6px;}
.unit-card .unit-meta{font-size:12px; color:var(--text-dim);}
.unit-card .unit-desc{font-size:12.5px; color:var(--text-dim); line-height:1.5;}
.unit-progress-row{display:flex; align-items:center; gap:10px;}
.unit-progress-row .bar{flex:1;}
.unit-progress-row .mono{font-size:11.5px; color:var(--text-dim); width:36px; text-align:right;}
.unit-card-footer{display:flex; align-items:center; justify-content:space-between; margin-top:2px;}
.unit-enter-link{font-size:12.5px; font-weight:600; color:var(--violet); display:flex; align-items:center; gap:5px;}
.unit-enter-link i{width:14px; height:14px;}
.pill{font-size:10.5px; font-weight:600; padding:5px 10px; border-radius:99px; letter-spacing:.02em; display:inline-flex; align-items:center; gap:5px; width:fit-content;}
.pill i{width:11px; height:11px;}
.pill-done{background:rgba(52,228,201,.14); color:var(--cyan);}
.pill-active{background:var(--violet-soft); color:var(--violet);}
.pill-locked{background:var(--card-2); color:var(--text-faint);}

.course-banner{padding:28px; display:flex; gap:26px; align-items:center; flex-wrap:wrap;}
.course-banner-icon{width:66px;height:66px;border-radius:17px; background:var(--grad); flex-shrink:0; display:flex;align-items:center;justify-content:center; color:#08090D; box-shadow:var(--shadow-glow);}
.course-banner-icon i{width:28px; height:28px;}
.course-banner h1{font-size:23px;}
.course-banner p{color:var(--text-dim); font-size:13.5px; margin-top:9px; max-width:620px; line-height:1.55;}
.course-banner-stats{display:flex; gap:24px; margin-top:14px; flex-wrap:wrap;}
.course-banner-stats div{font-size:12px; color:var(--text-faint);}
.course-banner-stats b{display:block; font-family:var(--font-mono); color:#fff; font-size:16px;}
.objective-block{padding:22px; margin-top:18px;}
.objective-block h3{font-size:14px; margin-bottom:11px; display:flex; align-items:center; gap:9px; color:#fff;}
.objective-block h3 i{width:16px; height:16px; color:var(--cyan);}
.objective-block p{font-size:13.5px; color:var(--text-dim); line-height:1.65;}

.lesson-list{display:flex; flex-direction:column; gap:11px;}
.lesson-card{display:flex; align-items:center; gap:16px; padding:16px 19px; cursor:pointer; transition:border-color .15s ease, transform .15s ease;}
.lesson-card:hover{border-color:var(--violet); transform:translateX(2px);}
.lesson-card.locked{cursor:not-allowed; opacity:.5;}
.lesson-card.locked:hover{border-color:var(--border-soft); transform:none;}
.lesson-num{width:39px;height:39px; border-radius:11px; flex-shrink:0; display:flex; align-items:center; justify-content:center; font-family:var(--font-mono); font-size:12.5px; font-weight:600; background:var(--card-2); color:var(--text-dim); border:1px solid var(--border-soft);}
.lesson-num i{width:15px; height:15px;}
.lesson-num.done{background:rgba(52,228,201,.14); color:var(--cyan); border-color:transparent;}
.lesson-num.active{background:var(--violet-soft); color:var(--violet); border-color:transparent;}
.lesson-main{flex:1; min-width:0;}
.lesson-main .unit-tag{font-size:11px; color:var(--text-faint); text-transform:uppercase; letter-spacing:.04em; font-weight:600;}
.lesson-main h4{font-size:14.5px; margin-top:3px; font-weight:600; color:#fff;}
.lesson-main p{font-size:12.5px; color:var(--text-dim); margin-top:4px; overflow:hidden; text-overflow:ellipsis; white-space:nowrap;}
.lesson-meta{display:flex; align-items:center; gap:16px; flex-shrink:0;}
.lesson-duration{display:flex; align-items:center; gap:6px; font-size:12px; color:var(--text-dim); font-family:var(--font-mono);}
.lesson-duration i{width:13px; height:13px;}
.lesson-video-icon{color:var(--text-faint); display:flex;}
.lesson-video-icon i{width:16px; height:16px;}
.lesson-card.done .lesson-video-icon, .lesson-card.active .lesson-video-icon{color:var(--violet);}

.lesson-layout{display:grid; grid-template-columns:1.7fr 1fr; gap:24px; align-items:start;}
.video-shell{aspect-ratio:16/9; border-radius:var(--radius-lg); overflow:hidden; position:relative; background:radial-gradient(circle at 30% 20%, rgba(124,111,255,.38), transparent 60%), var(--panel); border:1px solid var(--border-soft); display:flex; align-items:center; justify-content:center;}
.video-shell::after{content:""; position:absolute; inset:0; background:repeating-linear-gradient(115deg, rgba(255,255,255,.02) 0 2px, transparent 2px 60px);}
.play-fab{width:68px;height:68px;border-radius:50%; background:rgba(255,255,255,.08); backdrop-filter:blur(6px); border:1px solid rgba(255,255,255,.25); display:flex; align-items:center; justify-content:center; color:#fff; z-index:2; transition:transform .15s ease;}
.play-fab i{width:26px; height:26px;}
.play-fab:hover{transform:scale(1.07);}
.lesson-head{margin-top:20px;}
.lesson-head .tag-row{display:flex; align-items:center; gap:11px; flex-wrap:wrap;}
.lesson-head h1{font-size:23px; margin-top:9px;}
.lesson-head-meta{display:flex; gap:18px; margin-top:11px; color:var(--text-dim); font-size:12.5px; flex-wrap:wrap;}
.lesson-head-meta span{display:flex; align-items:center; gap:6px;}
.lesson-head-meta i{width:14px; height:14px;}
.lesson-desc{margin-top:17px; color:var(--text-dim); font-size:14px; line-height:1.65;}
.block{padding:22px; margin-top:17px;}
.block h3{font-size:14px; margin-bottom:13px; display:flex; align-items:center; gap:9px; color:#fff;}
.block h3 i{width:16px; height:16px; color:var(--cyan);}
.obj-list{display:flex; flex-direction:column; gap:11px; padding:0; margin:0; list-style:none;}
.obj-list li{display:flex; gap:11px; font-size:13.5px; color:var(--text-dim); line-height:1.5;}
.obj-list li i{flex-shrink:0; margin-top:2px; color:var(--cyan); width:16px; height:16px;}
.material-item{display:flex; align-items:center; gap:11px; padding:11px 13px; border-radius:11px; background:var(--card-2); border:1px solid var(--border-soft); font-size:13px; margin-top:9px;}
.material-item i{color:var(--violet); flex-shrink:0; width:16px; height:16px;}
.notes-box textarea{width:100%; min-height:112px; background:var(--card-2); border:1px solid var(--border-soft); border-radius:11px; color:var(--text); font-family:inherit; font-size:13.5px; padding:13px; resize:vertical; outline:none;}
.notes-box textarea:focus{border-color:var(--violet);}
.notes-save{margin-top:11px; display:flex; align-items:center; gap:11px;}
.notes-status{font-size:12px; color:var(--text-faint);}
.lesson-sidebar .card{padding:19px; margin-bottom:17px;}
.lesson-sidebar h4{font-size:13px; margin-bottom:13px; color:var(--text-dim); text-transform:uppercase; letter-spacing:.04em; font-weight:600;}
.mini-lesson{display:flex; align-items:center; gap:11px; padding:9px 7px; border-radius:9px; font-size:12.5px; cursor:pointer; color:var(--text-dim);}
.mini-lesson:hover{background:var(--card-2);}
.mini-lesson.current{background:var(--violet-soft); color:#fff;}
.mini-lesson .lesson-num{width:27px;height:27px; font-size:10.5px;}
.mini-lesson .lesson-num i{width:13px;height:13px;}
.lesson-actions{display:flex; align-items:center; gap:11px; margin-top:22px; flex-wrap:wrap;}
.complete-toggle{display:flex; align-items:center; gap:9px; padding:12px 19px; border-radius:12px; font-size:13.5px; font-weight:600; border:1px solid var(--border); background:var(--card-2); color:var(--text-dim);}
.complete-toggle i{width:16px; height:16px;}
.complete-toggle.done{background:rgba(52,228,201,.14); border-color:transparent; color:var(--cyan);}
.nav-btns{display:flex; gap:11px; margin-left:auto;}

.progress-grid{display:grid; grid-template-columns:repeat(4,1fr); gap:18px;}
.progress-grid .stat-card{padding:21px;}
.progress-grid .stat-value{font-size:24px;}
.unit-progress-list{display:flex; flex-direction:column; gap:15px; margin-top:8px;}
.unit-progress-item{padding:17px 19px;}
.unit-progress-item-top{display:flex; justify-content:space-between; align-items:center; margin-bottom:11px;}
.unit-progress-item-top h4{font-size:13.5px; font-weight:600; color:#fff;}
.unit-progress-item-top span{font-size:12px; color:var(--text-dim); font-family:var(--font-mono);}

.eval-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(240px,1fr)); gap:18px; margin-top:8px;}
.eval-card{padding:24px; display:flex; flex-direction:column; gap:14px;}
.eval-card-top{display:flex; align-items:center; justify-content:space-between;}
.eval-icon{width:38px;height:38px;border-radius:10px; display:flex; align-items:center; justify-content:center;}
.eval-icon i{width:18px;height:18px;}
.eval-pct{font-family:var(--font-display); font-size:30px; color:#fff;}
.eval-card h4{font-size:13.5px; font-weight:600; color:var(--text-dim);}
.eval-donut{position:relative; width:64px; height:64px;}
.eval-donut svg{transform:rotate(-90deg);}
.eval-summary-row{display:flex; gap:1px; border-radius:99px; overflow:hidden; height:14px; margin-top:6px;}
.eval-summary-legend{display:flex; flex-wrap:wrap; gap:14px; margin-top:16px;}
.eval-legend-item{display:flex; align-items:center; gap:8px; font-size:12.5px; color:var(--text-dim);}
.eval-legend-dot{width:9px;height:9px;border-radius:3px; flex-shrink:0;}

.activities-table{width:100%; border-collapse:separate; border-spacing:0;}
.activities-table thead th{text-align:left; font-size:11px; text-transform:uppercase; letter-spacing:.05em; color:var(--text-faint); font-weight:600; padding:0 16px 12px;}
.activities-table tbody tr{background:var(--card);}
.activities-table tbody td{padding:15px 16px; font-size:13px; color:var(--text-dim); border-top:1px solid var(--border-soft);}
.activities-table tbody tr td:first-child{border-left:1px solid var(--border-soft); border-top-left-radius:12px; border-bottom-left-radius:12px;}
.activities-table tbody tr td:last-child{border-right:1px solid var(--border-soft); border-top-right-radius:12px; border-bottom-right-radius:12px;}
.activities-table tbody tr{box-shadow:var(--shadow-card);}
.activities-table tbody tr + tr{margin-top:8px;}
.activities-table tbody td:first-child strong{color:#fff; font-weight:600; display:block;}
.grade-pill{font-family:var(--font-mono); font-weight:600; color:#fff; background:var(--card-2); padding:4px 10px; border-radius:8px; font-size:12.5px;}
.activities-cards{display:none; flex-direction:column; gap:12px;}
.activity-row-card{padding:16px 18px;}
.activity-row-top{display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;}
.activity-row-top strong{color:#fff; font-size:13.5px;}
.activity-row-meta{display:flex; justify-content:space-between; font-size:12px; color:var(--text-dim);}

.cert-wrap{display:flex; flex-direction:column; align-items:center; gap:24px; padding:10px 0 32px;}
.cert-locked{text-align:center; padding:52px 32px; max-width:520px;}
.cert-locked .lock-badge{width:58px;height:58px; border-radius:17px; background:var(--card-2); margin:0 auto 19px; display:flex; align-items:center; justify-content:center; color:var(--text-faint);}
.cert-locked .lock-badge i{width:24px; height:24px;}
.cert-locked h3{font-size:17.5px; margin-bottom:9px; color:#fff;}
.cert-locked p{color:var(--text-dim); font-size:13.5px; line-height:1.6;}
.cert-locked .bar{margin:19px auto 7px; max-width:280px;}
.cert-req-list{text-align:left; margin-top:20px; display:flex; flex-direction:column; gap:10px;}
.cert-req{display:flex; align-items:center; gap:10px; font-size:13px; color:var(--text-dim);}
.cert-req i{width:16px;height:16px; flex-shrink:0; color:var(--text-faint);}
.cert-req.met i{color:var(--cyan);}
.certificate{width:100%; max-width:760px; aspect-ratio:1.55/1; border-radius:22px; position:relative; overflow:hidden; background:linear-gradient(160deg,#12151C 0%, #0A0C11 100%); border:1px solid var(--border); box-shadow:0 32px 64px -20px rgba(0,0,0,.65); display:flex; flex-direction:column; align-items:center; justify-content:center; text-align:center; padding:42px;}
.certificate::before{content:""; position:absolute; inset:0; background:var(--grad); opacity:.07;}
.certificate::after{content:""; position:absolute; inset:15px; border:1px solid rgba(124,111,255,.32); border-radius:16px; pointer-events:none;}
.cert-crest{width:54px;height:54px;border-radius:50%; background:var(--grad); display:flex; align-items:center;justify-content:center; color:#08090D; margin-bottom:17px; box-shadow:var(--shadow-glow); z-index:1;}
.cert-crest i{width:24px; height:24px;}
.cert-eyebrow{font-size:11px; letter-spacing:.16em; text-transform:uppercase; color:var(--text-faint); z-index:1;}
.cert-title{font-family:var(--font-display); font-size:15px; letter-spacing:.06em; text-transform:uppercase; color:var(--cyan); margin-top:7px; z-index:1;}
.cert-name{font-family:var(--font-display); font-size:35px; margin-top:19px; z-index:1; color:#fff;}
.cert-course{font-size:14.5px; color:var(--text-dim); margin-top:11px; z-index:1;}
.cert-course b{color:#fff;}
.cert-date{margin-top:21px; font-size:12px; color:var(--text-faint); font-family:var(--font-mono); z-index:1;}
.cert-sign-row{display:flex; gap:62px; margin-top:27px; z-index:1;}
.cert-sign{font-size:11px; color:var(--text-faint);}
.cert-sign span{display:block; font-family:var(--font-display); font-size:13px; color:#fff; margin-bottom:5px;}

.activity-card{padding:19px 21px; display:flex; align-items:center; gap:17px; transition:border-color .15s ease;}
.activity-card:hover{border-color:var(--border);}
.activity-icon{width:44px;height:44px;border-radius:12px; background:var(--violet-soft); color:var(--violet); display:flex; align-items:center; justify-content:center; flex-shrink:0;}
.activity-icon i{width:19px; height:19px;}
.activity-icon.locked{background:var(--card-2); color:var(--text-faint);}
.activity-info{flex:1;}
.activity-info h4{font-size:14.5px; color:#fff;}
.activity-info p{font-size:12.5px; color:var(--text-dim); margin-top:4px;}

.settings-form{display:flex; flex-direction:column; gap:19px; max-width:480px;}
.field label{font-size:12.5px; color:var(--text-dim); display:block; margin-bottom:8px; font-weight:500;}
.field input{width:100%; background:var(--card-2); border:1px solid var(--border-soft); border-radius:11px; padding:12px 14px; color:var(--text); font-size:13.5px; outline:none; transition:border-color .15s ease;}
.field input:focus{border-color:var(--violet);}
.toggle-row{display:flex; align-items:center; justify-content:space-between; padding:15px 0; border-top:1px solid var(--border-soft);}
.toggle-row div span{display:block; font-size:13px; font-weight:500; color:#fff;}
.toggle-row div small{color:var(--text-faint); font-size:11.5px;}
.switch{width:43px;height:25px; border-radius:99px; background:var(--card-2); border:1px solid var(--border); position:relative; flex-shrink:0; cursor:pointer;}
.switch::after{content:""; position:absolute; width:19px;height:19px; border-radius:50%; background:var(--text-faint); top:2px; left:2px; transition:all .2s ease;}
.switch.on{background:var(--violet-soft); border-color:var(--violet);}
.switch.on::after{left:21px; background:var(--violet);}

.empty-state{text-align:center; padding:64px 20px; color:var(--text-dim);}
.empty-state i{width:46px; height:46px; color:var(--text-faint); margin:0 auto 16px;}
.empty-state h3{color:#fff; font-size:16px; margin-bottom:7px;}
.empty-state p{font-size:13.5px; max-width:340px; margin:0 auto;}

.toast{position:fixed; bottom:26px; left:50%; transform:translateX(-50%) translateY(20px); background:var(--card-2); border:1px solid var(--violet); color:var(--text); padding:13px 21px; border-radius:12px; font-size:13.5px; font-weight:500; display:flex; align-items:center; gap:10px; box-shadow:0 22px 44px -12px rgba(0,0,0,.55); z-index:100; opacity:0; pointer-events:none; transition:all .25s ease;}
.toast.show{opacity:1; transform:translateX(-50%) translateY(0);}
.toast i{width:16px; height:16px; color:var(--cyan); flex-shrink:0;}

@media (min-width:860px){ .topbar-title{display:block;} }
@media (max-width:1024px){
  .lesson-layout{grid-template-columns:1fr;}
  .progress-grid{grid-template-columns:repeat(2,1fr);}
  .stat-row{grid-template-columns:repeat(2,1fr);}
}
@media (max-width:860px){
  .sidebar{position:fixed; left:0; top:0; height:100vh; transform:translateX(-100%); transition:transform .25s ease; box-shadow:0 0 60px rgba(0,0,0,.5);}
  .app.sidebar-open .sidebar{transform:translateX(0);}
  .sidebar-close{display:flex; align-items:center; justify-content:center;}
  .menu-toggle{display:flex;}
  .hero{grid-template-columns:1fr;}
  .hero-ring-wrap{justify-self:center;}
  .content{padding:20px;}
  .activities-table{display:none;}
  .activities-cards{display:flex;}
}
@media (max-width:640px){
  .topbar{padding:13px 16px; gap:10px;}
  .search-wrap{display:none;}
  .stat-row{grid-template-columns:1fr;}
  .progress-grid{grid-template-columns:1fr 1fr;}
  .course-banner{flex-direction:column; align-items:flex-start;}
  .lesson-card{flex-wrap:wrap;}
  .lesson-meta{margin-left:55px;}
  .cert-sign-row{gap:32px;}
  .cert-name{font-size:27px;}
  .profile-name{display:none;}
  .eval-grid{grid-template-columns:1fr;}
}
</style>
</head>
<body>
<div class="app" id="app">
  <div class="sidebar-overlay" id="sidebarOverlay" onclick="closeSidebar()"></div>
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-brand">
      <div class="brand-mark"><i data-lucide="cpu" style="width:20px;height:20px;"></i></div>
      <div class="brand-text"><span class="brand-name">TechLab Academy</span><span class="brand-sub">IA Básico 1</span></div>
      <button class="sidebar-close" onclick="closeSidebar()" aria-label="Cerrar menú"><i data-lucide="x" style="width:18px;height:18px;"></i></button>
    </div>
    <nav class="sidebar-nav">
      <button class="nav-item" data-view="dashboard" onclick="showView('dashboard')"><span class="nav-icon"><i data-lucide="home"></i></span><span>Inicio</span></button>
      <button class="nav-item" data-view="course" onclick="showView('course')"><span class="nav-icon"><i data-lucide="book-open"></i></span><span>Mi curso</span></button>
      <button class="nav-item" data-view="units" onclick="showView('units')"><span class="nav-icon"><i data-lucide="layers"></i></span><span>Unidades</span></button>
      <button class="nav-item" data-view="lessons" onclick="showView('lessons')"><span class="nav-icon"><i data-lucide="play-circle"></i></span><span>Clases</span></button>
      <button class="nav-item" data-view="activities" onclick="showView('activities')"><span class="nav-icon"><i data-lucide="clipboard-list"></i></span><span>Actividades</span></button>
      <button class="nav-item" data-view="evaluations" onclick="showView('evaluations')"><span class="nav-icon"><i data-lucide="pie-chart"></i></span><span>Evaluaciones</span></button>
      <button class="nav-item" data-view="progress" onclick="showView('progress')"><span class="nav-icon"><i data-lucide="bar-chart-3"></i></span><span>Mi progreso</span></button>
      <button class="nav-item" data-view="certificate" onclick="showView('certificate')"><span class="nav-icon"><i data-lucide="award"></i></span><span>Certificado</span></button>
      <button class="nav-item" data-view="settings" onclick="showView('settings')"><span class="nav-icon"><i data-lucide="settings"></i></span><span>Configuración</span></button>
    </nav>
    <div class="sidebar-footer">
      <div class="mini-progress">
        <div class="mini-progress-head"><span>Progreso del curso</span><span id="sidebarPercent" class="mono">0%</span></div>
        <div class="bar"><div class="bar-fill" id="sidebarBarFill"></div></div>
      </div>
    </div>
  </aside>
  <div class="main">
    <header class="topbar">
      <button class="icon-btn menu-toggle" onclick="openSidebar()" aria-label="Abrir menú"><i data-lucide="menu"></i></button>
      <div class="topbar-title" id="topbarTitle">Inicio</div>
      <div class="search-wrap"><i data-lucide="search" style="width:16px;height:16px;"></i><input type="text" id="searchInput" placeholder="Buscar clases, unidades…" oninput="handleSearch(this.value)"></div>
      <div class="topbar-actions">
        <div class="dropdown-wrap">
          <button class="icon-btn" onclick="toggleNotif(event)" aria-label="Notificaciones"><i data-lucide="bell" style="width:18px;height:18px;"></i><span class="dot"></span></button>
          <div class="dropdown" id="notifDropdown">
            <div class="dropdown-head">Notificaciones</div>
            <div class="notif-item"><span class="notif-dot"></span><div><strong>Nueva clase disponible</strong><p>Unidad 2 ya está lista para ti.</p></div></div>
            <div class="notif-item"><span class="notif-dot ok"></span><div><strong>¡Buen avance!</strong><p>Completaste actividades esta semana.</p></div></div>
            <div class="notif-item"><span class="notif-dot warn"></span><div><strong>Recordatorio</strong><p>Tu próxima clase te espera.</p></div></div>
          </div>
        </div>
        <div class="dropdown-wrap">
          <button class="profile-btn" onclick="toggleProfile(event)">
            <span class="avatar" id="avatarInitials">CT</span><span class="profile-name" id="profileName">Camila Torres</span>
            <i data-lucide="chevron-down" style="width:14px;height:14px;"></i>
          </button>
          <div class="dropdown" id="profileDropdown">
            <div class="dropdown-head">Mi cuenta</div>
            <button class="dropdown-link" onclick="showView('settings')"><i data-lucide="settings"></i>Configuración</button>
            <button class="dropdown-link" onclick="showView('progress')"><i data-lucide="bar-chart-3"></i>Mi progreso</button>
            <button class="dropdown-link" onclick="alert('Sesión cerrada (demo)')"><i data-lucide="log-out"></i>Cerrar sesión</button>
          </div>
        </div>
      </div>
    </header>
    <main class="content" id="content"></main>
  </div>
</div>
<script>
function icon(name, extra){ return '<i data-lucide="'+name+'"'+(extra?(' style="'+extra+'"'):'')+'></i>'; }

/* =========================================================
   TechLab Academy — IA Básico 1 — contenido oficial del sílabo
   ========================================================= */
const COURSE = {
  brand: "TechLab Academy",
  code: "IA BÁSICO 1",
  title: "IA Básico 1",
  description: "Aprende los fundamentos de la Inteligencia Artificial, conoce sus principales herramientas y descubre cómo utilizarla para estudiar, trabajar y crear.",
  objective: "Entender qué es la Inteligencia Artificial, reconocer sus principales aplicaciones, utilizar herramientas como ChatGPT, Claude y Gemini, escribir instrucciones efectivas, utilizar IA para estudiar y trabajar, crear contenido con IA y utilizar estas herramientas de manera responsable y segura.",
  evaluation: [
    { label: "Participación y actividades", pct: 20, color: "#7C6FFF" },
    { label: "Prácticas con herramientas de IA", pct: 30, color: "#4F8CFF" },
    { label: "Proyecto", pct: 30, color: "#34E4C9" },
    { label: "Presentación final", pct: 20, color: "#F2B84B" },
  ],
  units: [
    { title: "Fundamentos de la Inteligencia Artificial", weeks: "Semanas 1–2",
      desc: "Los conceptos base para entender qué es la IA, su historia y su presencia en la vida cotidiana.",
      lessons: [
        { title: "¿Qué es la Inteligencia Artificial?", desc: "Introducción al concepto de IA y a las ideas que lo sostienen.", duration: 12 },
        { title: "Historia de la IA", desc: "Los hitos principales que marcaron el desarrollo de la Inteligencia Artificial.", duration: 11 },
        { title: "¿Cómo ha evolucionado?", desc: "El camino desde los primeros sistemas hasta la IA actual.", duration: 10 },
        { title: "¿Dónde encontramos IA actualmente?", desc: "Un recorrido por los lugares donde la IA ya está presente.", duration: 9 },
        { title: "Ejemplos cotidianos de IA", desc: "Casos reales y cercanos de uso de IA en el día a día.", duration: 9 },
        { title: "Qué puede y qué no puede hacer una IA", desc: "Los límites reales de la tecnología frente a las expectativas.", duration: 10 },
        { title: "Mitos y realidades sobre la IA", desc: "Aclarando ideas erróneas comunes sobre la Inteligencia Artificial.", duration: 8 },
      ] },
    { title: "Conociendo las herramientas de IA", weeks: "Semanas 3–4",
      desc: "Un primer contacto con los modelos y asistentes de IA más utilizados.",
      lessons: [
        { title: "¿Qué son los modelos de IA?", desc: "Una explicación sencilla de qué es un modelo de IA.", duration: 10 },
        { title: "Chatbots y asistentes virtuales", desc: "Cómo funcionan los asistentes conversacionales de IA.", duration: 9 },
        { title: "Introducción a ChatGPT", desc: "Primeros pasos para usar ChatGPT.", duration: 12 },
        { title: "Introducción a Claude", desc: "Primeros pasos para usar Claude.", duration: 12 },
        { title: "Introducción a Gemini", desc: "Primeros pasos para usar Gemini.", duration: 11 },
        { title: "Comparación entre diferentes herramientas", desc: "Similitudes y diferencias entre las principales herramientas de IA.", duration: 10 },
        { title: "Cómo elegir una herramienta dependiendo de la tarea", desc: "Criterios prácticos para elegir la herramienta correcta.", duration: 9 },
      ] },
    { title: "Aprender a hablar con la IA", weeks: "Semanas 5–7",
      desc: "La habilidad central del curso: comunicarte de forma clara y efectiva con la IA.",
      lessons: [
        { title: "¿Qué es un prompt?", desc: "El concepto base para instruir a una IA.", duration: 9 },
        { title: "Cómo hacer buenas preguntas", desc: "Principios para formular preguntas claras.", duration: 10 },
        { title: "Cómo dar contexto", desc: "Por qué el contexto mejora las respuestas de la IA.", duration: 10 },
        { title: "Cómo pedir respuestas específicas", desc: "Técnicas para obtener resultados concretos.", duration: 11 },
        { title: "Cómo pedir que la IA explique algo", desc: "Formas de solicitar explicaciones claras y a tu nivel.", duration: 9 },
        { title: "Cómo corregir y mejorar una respuesta", desc: "Iterar sobre una respuesta hasta obtener lo que necesitas.", duration: 10 },
        { title: "Errores comunes al utilizar IA", desc: "Los errores más frecuentes al escribir instrucciones.", duration: 9 },
        { title: "Introducción al Prompt Engineering", desc: "Una mirada inicial a la disciplina detrás de los buenos prompts.", duration: 12 },
      ] },
    { title: "IA para estudiar y trabajar", weeks: "Semanas 8–10",
      desc: "Aplicaciones prácticas de la IA en el entorno académico y laboral.",
      lessons: [
        { title: "Resumir textos", desc: "Usar IA para condensar información clave.", duration: 9 },
        { title: "Explicar conceptos difíciles", desc: "Pedir explicaciones adaptadas a tu nivel de comprensión.", duration: 9 },
        { title: "Crear esquemas y apuntes", desc: "Organizar información en esquemas claros con ayuda de IA.", duration: 10 },
        { title: "Generar ideas", desc: "Usar IA como apoyo para la lluvia de ideas.", duration: 8 },
        { title: "Revisar textos", desc: "Mejorar la calidad de un texto con asistencia de IA.", duration: 9 },
        { title: "Traducir y corregir", desc: "Traducción y corrección de textos usando IA.", duration: 8 },
        { title: "Crear presentaciones", desc: "Apoyarte en IA para estructurar presentaciones.", duration: 10 },
        { title: "Organizar información", desc: "Ordenar y clasificar información con ayuda de IA.", duration: 9 },
        { title: "Crear planes de estudio y trabajo", desc: "Diseñar planes personalizados con asistencia de IA.", duration: 10 },
        { title: "Uso responsable de IA en tareas académicas", desc: "Buenas prácticas éticas al usar IA en el estudio.", duration: 9 },
      ] },
    { title: "IA generativa", weeks: "Semanas 11–13",
      desc: "Cómo la IA crea texto, imágenes, audio y video, y sus límites actuales.",
      lessons: [
        { title: "¿Qué es la IA generativa?", desc: "El concepto central detrás de la creación de contenido con IA.", duration: 10 },
        { title: "Generación de texto", desc: "Cómo la IA genera contenido escrito.", duration: 10 },
        { title: "Generación de imágenes", desc: "Fundamentos de la creación de imágenes con IA.", duration: 11 },
        { title: "Generación de audio", desc: "Cómo la IA genera y transforma audio.", duration: 9 },
        { title: "Generación de video", desc: "Una introducción a la creación de video con IA.", duration: 11 },
        { title: "Herramientas populares", desc: "Un vistazo a las herramientas generativas más usadas.", duration: 9 },
        { title: "Cómo crear contenido utilizando IA", desc: "Un flujo práctico para crear contenido con apoyo de IA.", duration: 10 },
        { title: "Limitaciones de la IA generativa", desc: "Lo que la IA generativa todavía no hace bien.", duration: 9 },
        { title: "Información falsa y errores de la IA", desc: "Cómo identificar errores y contenido poco confiable.", duration: 9 },
      ] },
    { title: "IA, seguridad y futuro", weeks: "Semanas 14–15",
      desc: "Privacidad, uso responsable y el papel de la IA en el futuro del trabajo.",
      lessons: [
        { title: "Privacidad", desc: "Qué considerar sobre tu privacidad al usar IA.", duration: 9 },
        { title: "Datos personales", desc: "Cómo se manejan tus datos al interactuar con IA.", duration: 9 },
        { title: "Seguridad al utilizar herramientas de IA", desc: "Buenas prácticas de seguridad digital.", duration: 9 },
        { title: "Sesgos", desc: "Qué son los sesgos en los modelos de IA y por qué ocurren.", duration: 9 },
        { title: "Derechos de autor", desc: "Consideraciones sobre propiedad intelectual y contenido de IA.", duration: 9 },
        { title: "Uso responsable", desc: "Principios para un uso ético de la IA.", duration: 8 },
        { title: "IA en el trabajo", desc: "El impacto de la IA en distintos entornos laborales.", duration: 9 },
        { title: "Profesiones e IA", desc: "Cómo la IA transforma distintas profesiones.", duration: 9 },
        { title: "Qué podemos esperar de la IA en el futuro", desc: "Una mirada a las tendencias futuras de la IA.", duration: 10 },
      ] },
  ]
};

const ACTIVITIES_LOG = [
  { name: "Actividad · Mitos y realidades sobre la IA", unit: 1, status: "Calificada", grade: "18/20", date: "03 mar 2026" },
  { name: "Práctica · Comparación de herramientas de IA", unit: 2, status: "Calificada", grade: "19/20", date: "17 mar 2026" },
  { name: "Práctica · Escribir un prompt efectivo", unit: 3, status: "Calificada", grade: "17/20", date: "02 abr 2026" },
  { name: "Actividad · Corregir y mejorar una respuesta de IA", unit: 3, status: "En revisión", grade: "—", date: "09 abr 2026" },
  { name: "Práctica · Crear un esquema con IA", unit: 4, status: "Pendiente", grade: "—", date: "—" },
];

const LESSONS = [];
COURSE.units.forEach((u, ui) => {
  u.lessons.forEach((l, li) => {
    LESSONS.push({ ...l, unitIndex: ui, unitTitle: u.title, indexInUnit: li, globalIndex: LESSONS.length });
  });
});
const TOTAL_LESSONS = LESSONS.length;

/* =========================================================
   Estado de la aplicación (en memoria)
   ========================================================= */
const state = {
  studentName: "Camila Torres",
  currentIndex: Math.round(TOTAL_LESSONS * 0.35),
  view: "dashboard",
  activeLesson: null,
  searchTerm: "",
  notes: {},
};

function lessonStatus(i){
  if(i < state.currentIndex) return "done";
  if(i === state.currentIndex) return "active";
  return "locked";
}
function unitStats(ui){
  const lessons = LESSONS.filter(l => l.unitIndex === ui);
  const done = lessons.filter(l => lessonStatus(l.globalIndex) === "done").length;
  return { total: lessons.length, done, pct: Math.round((done/lessons.length)*100) };
}
function overallStats(){
  const done = Math.min(state.currentIndex, TOTAL_LESSONS);
  const pct = Math.round((done/TOTAL_LESSONS)*100);
  const unitsDone = COURSE.units.filter((_,ui)=> unitStats(ui).pct === 100).length;
  const minutes = LESSONS.slice(0, done).reduce((s,l)=> s + l.duration, 0);
  const activitiesDone = ACTIVITIES_LOG.filter(a=>a.status==="Calificada").length;
  return { done, pending: TOTAL_LESSONS-done, pct, unitsDone, minutes, totalUnits: COURSE.units.length, activitiesDone, activitiesTotal: ACTIVITIES_LOG.length };
}
function fmtTime(min){
  if(min < 60) return min + " min";
  const h = Math.floor(min/60), m = min%60;
  return m ? (h + " h " + m + " min") : (h + " h");
}
function initials(name){ return name.split(" ").filter(Boolean).slice(0,2).map(w=>w[0].toUpperCase()).join(""); }

const VIEW_TITLES = {
  dashboard: "Inicio", course: "Mi curso", units: "Unidades", lessons: "Clases",
  activities: "Actividades", evaluations: "Evaluaciones", progress: "Mi progreso", certificate: "Certificado",
  settings: "Configuración", lessonDetail: "Clase",
};

function refreshIcons(){ if(window.lucide) lucide.createIcons(); }

function showView(view){
  state.view = view;
  if(view !== "lessonDetail") state.activeLesson = null;
  closeSidebar();
  closeDropdowns();
  document.getElementById("topbarTitle").textContent = VIEW_TITLES[view] || "";
  document.querySelectorAll(".nav-item").forEach(btn=>{
    btn.classList.toggle("active", btn.dataset.view === view || (view==="lessonDetail" && btn.dataset.view==="lessons"));
  });
  render();
  window.scrollTo(0,0);
}

function openLesson(globalIndex){
  if(lessonStatus(globalIndex) === "locked"){ showToast("Completa las clases anteriores para desbloquear esta clase."); return; }
  state.activeLesson = globalIndex;
  state.view = "lessonDetail";
  closeSidebar();
  document.getElementById("topbarTitle").textContent = "Clase";
  document.querySelectorAll(".nav-item").forEach(b=>b.classList.toggle("active", b.dataset.view==="lessons"));
  render();
  window.scrollTo(0,0);
}
function continueLearning(){ openLesson(Math.min(state.currentIndex, TOTAL_LESSONS-1)); }
function markCompleted(){
  const i = state.activeLesson;
  if(i == null) return;
  if(i === state.currentIndex && state.currentIndex < TOTAL_LESSONS){
    state.currentIndex++;
    showToast("¡Clase marcada como completada!", true);
  }
  render();
}
function goNext(){
  const i = state.activeLesson;
  if(i == null || i+1 >= TOTAL_LESSONS) return;
  if(lessonStatus(i+1) === "locked"){ showToast("Completa la clase actual para continuar."); return; }
  openLesson(i+1);
}
function goPrev(){
  const i = state.activeLesson;
  if(i == null || i-1 < 0) return;
  openLesson(i-1);
}

function openSidebar(){ document.getElementById("app").classList.add("sidebar-open"); }
function closeSidebar(){ document.getElementById("app").classList.remove("sidebar-open"); }
function closeDropdowns(){
  const n = document.getElementById("notifDropdown"), p = document.getElementById("profileDropdown");
  if(n) n.classList.remove("open");
  if(p) p.classList.remove("open");
}
function toggleNotif(e){ e.stopPropagation(); document.getElementById("profileDropdown").classList.remove("open"); document.getElementById("notifDropdown").classList.toggle("open"); }
function toggleProfile(e){ e.stopPropagation(); document.getElementById("notifDropdown").classList.remove("open"); document.getElementById("profileDropdown").classList.toggle("open"); }
document.addEventListener("click", closeDropdowns);

function handleSearch(term){
  state.searchTerm = term.trim().toLowerCase();
  if(state.searchTerm && state.view !== "lessons"){
    state.view = "lessons";
    document.getElementById("topbarTitle").textContent = "Clases";
    document.querySelectorAll(".nav-item").forEach(b=>b.classList.toggle("active", b.dataset.view==="lessons"));
    render();
    const input = document.getElementById("searchInput");
    input.value = term; input.focus();
  } else if(state.view === "lessons"){
    renderContent();
  }
}

let toastTimer;
function showToast(msg, positive){
  const el = document.getElementById("toastEl");
  if(!el) return;
  el.innerHTML = icon(positive ? "check-circle-2" : "lock") + "<span>" + msg + "</span>";
  refreshIcons();
  el.classList.add("show");
  clearTimeout(toastTimer);
  toastTimer = setTimeout(()=> el.classList.remove("show"), 2600);
}

function updateGlobalProgressUI(){
  const s = overallStats();
  const fill = document.getElementById("sidebarBarFill");
  const pct = document.getElementById("sidebarPercent");
  if(fill) fill.style.width = s.pct + "%";
  if(pct) pct.textContent = s.pct + "%";
}

function render(){
  document.getElementById("avatarInitials").textContent = initials(state.studentName);
  document.getElementById("profileName").textContent = state.studentName;
  updateGlobalProgressUI();
  renderContent();
  if(!document.getElementById("toastEl")){
    const t = document.createElement("div");
    t.className = "toast"; t.id = "toastEl";
    document.body.appendChild(t);
  }
  refreshIcons();
}

function renderContent(){
  const c = document.getElementById("content");
  switch(state.view){
    case "dashboard": c.innerHTML = viewDashboard(); break;
    case "course": c.innerHTML = viewCourse(); break;
    case "units": c.innerHTML = viewCourse(true); break;
    case "lessons": c.innerHTML = viewLessons(); break;
    case "activities": c.innerHTML = viewActivities(); break;
    case "evaluations": c.innerHTML = viewEvaluations(); break;
    case "progress": c.innerHTML = viewProgress(); break;
    case "certificate": c.innerHTML = viewCertificate(); break;
    case "settings": c.innerHTML = viewSettings(); break;
    case "lessonDetail": c.innerHTML = viewLessonDetail(); break;
  }
  refreshIcons();
}

/* ---------- Dashboard ---------- */
function viewDashboard(){
  const s = overallStats();
  const cur = LESSONS[Math.min(state.currentIndex, TOTAL_LESSONS-1)];
  const r = 62, circ = 2*Math.PI*r;
  const dash = circ * s.pct/100;
  return '' +
    '<div class="card hero">' +
      '<div>' +
        '<span class="eyebrow">' + COURSE.brand + '</span>' +
        '<h1 class="hero-greeting">Hola, ' + firstName() + ' \uD83D\uDC4B</h1>' +
        '<p class="hero-sub">Continúa aprendiendo Inteligencia Artificial.</p>' +
        '<div class="hero-cta">' +
          '<button class="btn btn-primary" onclick="continueLearning()">Continuar aprendiendo ' + icon('arrow-right','width:16px;height:16px;') + '</button>' +
          '<span class="hero-cta-note">Próxima clase: ' + escapeHtml(cur.title) + '</span>' +
        '</div>' +
      '</div>' +
      '<div class="hero-ring-wrap">' +
        '<div class="ring-percent"><svg width="152" height="152" viewBox="0 0 152 152">' +
          '<circle cx="76" cy="76" r="' + r + '" stroke="var(--border)" stroke-width="10" fill="none"/>' +
          '<circle cx="76" cy="76" r="' + r + '" stroke="url(#gradRing)" stroke-width="10" fill="none" stroke-linecap="round" stroke-dasharray="' + circ + '" stroke-dashoffset="' + (circ-dash) + '"/>' +
          '<defs><linearGradient id="gradRing" x1="0" y1="0" x2="1" y2="1"><stop offset="0%" stop-color="#7C6FFF"/><stop offset="100%" stop-color="#34E4C9"/></linearGradient></defs>' +
        '</svg><div class="ring-num"><b class="mono">' + s.pct + '%</b><small>Completado</small></div></div>' +
        '<span class="ring-label">' + s.done + ' de ' + TOTAL_LESSONS + ' clases</span>' +
      '</div>' +
    '</div>' +

    '<div class="card block" style="margin-top:22px;">' +
      '<div style="display:flex; align-items:center; gap:16px; flex-wrap:wrap;">' +
        '<div class="course-banner-icon" style="width:52px;height:52px;border-radius:14px;">' + icon('sparkles','width:22px;height:22px;') + '</div>' +
        '<div style="flex:1; min-width:220px;"><span class="eyebrow">' + COURSE.code + '</span><h3 style="font-size:17px; margin-top:6px; color:#fff;">' + COURSE.title + '</h3></div>' +
      '</div>' +
      '<p style="font-size:13.5px; color:var(--text-dim); margin-top:14px; line-height:1.6;">' + COURSE.description + '</p>' +
    '</div>' +

    '<div class="stat-row">' +
      '<div class="card stat-card"><div class="stat-icon v">' + icon('book-open') + '</div><div class="stat-value mono">' + s.pct + '%</div><div class="stat-label">Progreso general</div></div>' +
      '<div class="card stat-card"><div class="stat-icon c">' + icon('check') + '</div><div class="stat-value mono">' + s.done + '/' + TOTAL_LESSONS + '</div><div class="stat-label">Clases completadas</div></div>' +
      '<div class="card stat-card"><div class="stat-icon a">' + icon('layers') + '</div><div class="stat-value mono">' + s.unitsDone + '/' + s.totalUnits + '</div><div class="stat-label">Unidades completadas</div></div>' +
      '<div class="card stat-card"><div class="stat-icon b">' + icon('clock') + '</div><div class="stat-value mono">' + fmtTime(s.minutes) + '</div><div class="stat-label">Tiempo de aprendizaje</div></div>' +
    '</div>' +

    '<div class="section-title"><h2>Continúa aprendiendo</h2></div>' +
    '<div class="card continue-card" onclick="continueLearning()">' +
      '<div class="continue-thumb">' + icon('play') + '</div>' +
      '<div class="continue-info">' +
        '<span class="tag">Unidad ' + (cur.unitIndex+1) + '</span>' +
        '<h4>' + escapeHtml(cur.title) + '</h4>' +
        '<p>Duración: ' + cur.duration + ' min &nbsp;\u00B7&nbsp; Estado: En progreso</p>' +
      '</div>' +
      '<button class="btn btn-primary" onclick="event.stopPropagation(); continueLearning()">Continuar clase ' + icon('arrow-right','width:16px;height:16px;') + '</button>' +
    '</div>' +

    '<div class="section-title"><h2>Contenido del curso</h2><button class="link-btn" onclick="showView(\'units\')">Ver todas ' + icon('arrow-right') + '</button></div>' +
    '<div class="units-grid">' + COURSE.units.map((u,ui)=>unitCard(ui)).join("") + '</div>';
}

function firstName(){ return state.studentName.split(" ")[0]; }

/* ---------- Mi curso / Unidades ---------- */
function unitCard(ui){
  const u = COURSE.units[ui];
  const st = unitStats(ui);
  const pillClass = st.pct===100 ? "pill-done" : st.done>0 ? "pill-active" : "pill-locked";
  const pillText = st.pct===100 ? "Completada" : st.done>0 ? "En progreso" : "Bloqueada";
  const pillIcon = st.pct===100 ? icon('check','width:11px;height:11px;') : st.done>0 ? "" : icon('lock','width:11px;height:11px;');
  return '' +
    '<div class="card unit-card" onclick="openUnit(' + ui + ')">' +
      '<div class="unit-card-top"><div class="unit-badge">' + String(ui+1).padStart(2,"0") + '</div><span class="pill ' + pillClass + '">' + pillIcon + pillText + '</span></div>' +
      '<h3>' + escapeHtml(u.title) + '</h3>' +
      '<span class="unit-weeks">' + u.weeks + '</span>' +
      '<p class="unit-desc">' + escapeHtml(u.desc) + '</p>' +
      '<div class="unit-meta">' + u.lessons.length + ' clases</div>' +
      '<div class="unit-progress-row"><div class="bar"><div class="bar-fill" style="width:' + st.pct + '%"></div></div><span class="mono">' + st.pct + '%</span></div>' +
      '<div class="unit-card-footer"><span class="unit-enter-link">Ver unidad ' + icon('arrow-right') + '</span></div>' +
    '</div>';
}
function openUnit(ui){
  state.searchTerm = "";
  showView("lessons");
  setTimeout(function(){
    const el = document.getElementById("unit-block-"+ui);
    if(el) el.scrollIntoView({behavior:"smooth", block:"start"});
  }, 30);
}

function viewCourse(unitsOnly){
  const s = overallStats();
  return '' +
    '<div class="card course-banner">' +
      '<div class="course-banner-icon">' + icon('cpu') + '</div>' +
      '<div>' +
        '<span class="eyebrow">' + COURSE.brand + ' \u00B7 ' + COURSE.code + '</span>' +
        '<h1>' + COURSE.title + '</h1>' +
        '<p>' + COURSE.description + '</p>' +
        '<div class="course-banner-stats">' +
          '<div><b class="mono">' + COURSE.units.length + '</b>Unidades</div>' +
          '<div><b class="mono">' + TOTAL_LESSONS + '</b>Clases</div>' +
          '<div><b class="mono">15</b>Semanas</div>' +
          '<div><b class="mono">' + s.pct + '%</b>Progreso</div>' +
        '</div>' +
      '</div>' +
      '<button class="btn btn-primary" style="margin-left:auto" onclick="continueLearning()">' + icon('play','width:16px;height:16px;') + ' Continuar</button>' +
    '</div>' +
    '<div class="card objective-block"><h3>' + icon('target') + 'Objetivo del curso</h3><p>' + COURSE.objective + '</p></div>' +
    '<div class="section-title"><h2>' + (unitsOnly ? "Contenido del curso" : "Unidades del curso") + '</h2></div>' +
    '<div class="units-grid">' + COURSE.units.map((u,ui)=>unitCard(ui)).join("") + '</div>';
}

/* ---------- Clases ---------- */
function viewLessons(){
  const term = state.searchTerm;
  const filtered = LESSONS.filter(function(l){ return !term || l.title.toLowerCase().indexOf(term) !== -1 || l.unitTitle.toLowerCase().indexOf(term) !== -1; });

  if(term){
    return '' +
      '<div class="page-head"><span class="eyebrow">Resultados de búsqueda</span><h1>\u201C' + escapeHtml(state.searchTerm) + '\u201D</h1>' +
      '<p>' + filtered.length + ' clase' + (filtered.length===1?"":"s") + ' encontrada' + (filtered.length===1?"":"s") + '.</p></div>' +
      '<div class="lesson-list">' + (filtered.length ? filtered.map(lessonRow).join("") : emptyState("Sin resultados", "Intenta con otra palabra clave, como el nombre de una unidad o herramienta.")) + '</div>';
  }

  return '' +
    '<div class="page-head"><span class="eyebrow">Todas las clases</span><h1>Clases del curso</h1>' +
    '<p>Recorre las ' + TOTAL_LESSONS + ' clases de ' + COURSE.title + ', organizadas por unidad según el sílabo oficial.</p></div>' +
    COURSE.units.map(function(u,ui){
      return '<div id="unit-block-' + ui + '" class="section-title"><h2>Unidad ' + (ui+1) + ' \u00B7 ' + escapeHtml(u.title) + '</h2></div>' +
        '<div class="lesson-list" style="margin-bottom:10px;">' + LESSONS.filter(function(l){return l.unitIndex===ui;}).map(lessonRow).join("") + '</div>';
    }).join("");
}

function lessonRow(l){
  const st = lessonStatus(l.globalIndex);
  const numInner = st==="done" ? icon('check') : st==="locked" ? icon('lock') : String(l.indexInUnit+1).padStart(2,"0");
  return '' +
    '<div class="card lesson-card ' + st + '" onclick="openLesson(' + l.globalIndex + ')">' +
      '<div class="lesson-num ' + st + '">' + numInner + '</div>' +
      '<div class="lesson-main"><span class="unit-tag">Unidad ' + (l.unitIndex+1) + ' \u00B7 Clase ' + (l.indexInUnit+1) + '</span>' +
      '<h4>' + escapeHtml(l.title) + '</h4><p>' + escapeHtml(l.desc) + '</p></div>' +
      '<div class="lesson-meta"><span class="lesson-video-icon">' + icon('play-circle') + '</span><span class="lesson-duration">' + icon('clock') + l.duration + ' min</span></div>' +
    '</div>';
}
function emptyState(title, text){ return '<div class="empty-state">' + icon('search-x') + '<h3>' + title + '</h3><p>' + text + '</p></div>'; }

/* ---------- Página de clase ---------- */
function viewLessonDetail(){
  const i = state.activeLesson == null ? state.currentIndex : state.activeLesson;
  const l = LESSONS[i];
  const st = lessonStatus(i);
  const noteVal = state.notes[i] || "";
  const pillHtml = st==='done' ? ('<span class="pill pill-done">' + icon('check','width:11px;height:11px;') + ' Completada</span>')
    : st==='active' ? ('<span class="pill pill-active">' + icon('play','width:11px;height:11px;') + ' En progreso</span>') : ('<span class="pill pill-locked">' + icon('lock','width:11px;height:11px;') + ' Bloqueada</span>');

  const objectives = [
    "Comprender la idea central de \u201C" + l.title + "\u201D",
    "Relacionar este contenido con lo visto en " + l.unitTitle,
    "Aplicar lo aprendido en la actividad práctica de esta unidad"
  ];
  const materials = ["Guía PDF de la clase", "Resumen descargable de la unidad " + (l.unitIndex+1)];

  let miniLessons = "";
  COURSE.units[l.unitIndex].lessons.forEach(function(ll,li){
    const gi = LESSONS.findIndex(function(x){ return x.unitIndex===l.unitIndex && x.indexInUnit===li; });
    const s2 = lessonStatus(gi);
    miniLessons += '<div class="mini-lesson ' + (gi===i?'current':'') + '" onclick="openLesson(' + gi + ')">' +
      '<div class="lesson-num ' + s2 + '" style="width:27px;height:27px;font-size:10.5px;">' + (s2==='done'?icon('check'):s2==='locked'?icon('lock'):(li+1)) + '</div>' +
      '<span>' + escapeHtml(ll.title) + '</span></div>';
  });

  return '' +
    '<div class="lesson-layout">' +
      '<div>' +
        '<div class="video-shell"><button class="play-fab" onclick="showToast(\'Reproduciendo (demo): ' + escapeAttr(l.title) + '\', true)">' + icon('play') + '</button></div>' +
        '<div class="lesson-head">' +
          '<div class="tag-row">' + pillHtml + '<span class="hero-cta-note">Unidad ' + (l.unitIndex+1) + ' \u00B7 Clase ' + (l.indexInUnit+1) + ' de ' + COURSE.units[l.unitIndex].lessons.length + '</span></div>' +
          '<h1>' + escapeHtml(l.title) + '</h1>' +
          '<div class="lesson-head-meta"><span>' + icon('clock') + l.duration + ' minutos</span><span>' + icon('layers') + escapeHtml(l.unitTitle) + '</span></div>' +
          '<p class="lesson-desc">' + escapeHtml(l.desc) + '</p>' +
        '</div>' +
        '<div class="card block"><h3>' + icon('target') + 'Objetivos de aprendizaje</h3><ul class="obj-list">' +
          objectives.map(function(o){ return '<li>' + icon('check-circle-2') + '<span>' + escapeHtml(o) + '</span></li>'; }).join("") +
        '</ul></div>' +
        '<div class="card block"><h3>' + icon('file-text') + 'Material complementario</h3>' +
          materials.map(function(m){ return '<div class="material-item">' + icon('file-text') + '<span>' + escapeHtml(m) + '</span></div>'; }).join("") +
        '</div>' +
        '<div class="card block notes-box"><h3>' + icon('pencil-line') + 'Mis notas</h3>' +
          '<textarea id="notesArea" placeholder="Escribe aquí tus notas sobre esta clase…">' + escapeHtml(noteVal) + '</textarea>' +
          '<div class="notes-save"><button class="btn btn-ghost btn-sm" onclick="saveNote(' + i + ')">Guardar nota</button><span class="notes-status" id="noteStatus"></span></div>' +
        '</div>' +
        '<div class="lesson-actions">' +
          '<button class="complete-toggle ' + (st==='done'?'done':'') + '" onclick="markCompleted()" ' + (st==='locked'?'disabled':'') + '>' +
            (st==='done' ? (icon('check-circle-2') + 'Clase completada') : 'Marcar como completada') +
          '</button>' +
          '<div class="nav-btns">' +
            '<button class="btn btn-ghost btn-sm" onclick="goPrev()" ' + (i===0?'disabled':'') + '>' + icon('arrow-left') + ' Clase anterior</button>' +
            '<button class="btn btn-ghost btn-sm" onclick="goNext()" ' + (i===TOTAL_LESSONS-1?'disabled':'') + '>Siguiente clase ' + icon('arrow-right') + '</button>' +
          '</div>' +
        '</div>' +
      '</div>' +
      '<div class="lesson-sidebar">' +
        '<div class="card"><h4>Contenido de la unidad</h4>' + miniLessons + '</div>' +
        '<div class="card"><h4>Tu progreso</h4>' +
          '<div class="unit-progress-row" style="margin-bottom:7px;"><div class="bar"><div class="bar-fill" style="width:' + overallStats().pct + '%"></div></div><span class="mono">' + overallStats().pct + '%</span></div>' +
          '<p style="font-size:12px; color:var(--text-dim);">' + overallStats().done + ' de ' + TOTAL_LESSONS + ' clases completadas en todo el curso.</p>' +
        '</div>' +
      '</div>' +
    '</div>';
}
function saveNote(i){
  const val = document.getElementById("notesArea").value;
  state.notes[i] = val;
  const status = document.getElementById("noteStatus");
  if(status){ status.textContent = "Guardado \u2713"; setTimeout(function(){ if(status) status.textContent=""; }, 1800); }
}

/* ---------- Actividades ---------- */
function viewActivities(){
  const rowsTable = ACTIVITIES_LOG.map(function(a){
    const badge = a.status==="Calificada" ? '<span class="pill pill-done">'+icon('check','width:11px;height:11px;')+' Calificada</span>'
      : a.status==="En revisión" ? '<span class="pill pill-active">'+icon('clock','width:11px;height:11px;')+' En revisión</span>'
      : '<span class="pill pill-locked">'+icon('circle-dashed','width:11px;height:11px;')+' Pendiente</span>';
    return '<tr><td><strong>'+escapeHtml(a.name)+'</strong></td><td>Unidad '+a.unit+'</td><td>'+badge+'</td><td>'+(a.grade!=="—"?'<span class="grade-pill">'+a.grade+'</span>':'<span style="color:var(--text-faint)">—</span>')+'</td><td class="mono">'+a.date+'</td></tr>';
  }).join("");
  const cardsList = ACTIVITIES_LOG.map(function(a){
    const badge = a.status==="Calificada" ? '<span class="pill pill-done">Calificada</span>' : a.status==="En revisión" ? '<span class="pill pill-active">En revisión</span>' : '<span class="pill pill-locked">Pendiente</span>';
    return '<div class="card activity-row-card"><div class="activity-row-top"><strong>'+escapeHtml(a.name)+'</strong>'+badge+'</div>' +
      '<div class="activity-row-meta"><span>Unidad '+a.unit+' \u00B7 '+a.date+'</span>' + (a.grade!=="—"?'<span class="grade-pill">'+a.grade+'</span>':'') + '</div></div>';
  }).join("");

  return '' +
    '<div class="page-head"><span class="eyebrow">Seguimiento</span><h1>Actividades</h1><p>Actividades y prácticas realizadas a lo largo de ' + COURSE.title + '.</p></div>' +
    '<div class="card" style="padding:20px; overflow-x:auto;">' +
      '<table class="activities-table"><thead><tr><th>Actividad</th><th>Unidad</th><th>Estado</th><th>Calificación</th><th>Fecha</th></tr></thead>' +
      '<tbody>' + rowsTable + '</tbody></table>' +
      '<div class="activities-cards">' + cardsList + '</div>' +
    '</div>';
}

/* ---------- Evaluaciones ---------- */
function evalDonut(pct, color){
  const r = 26, circ = 2*Math.PI*r, dash = circ*pct/100;
  return '<div class="eval-donut"><svg width="64" height="64" viewBox="0 0 64 64">' +
    '<circle cx="32" cy="32" r="'+r+'" stroke="var(--border)" stroke-width="7" fill="none"/>' +
    '<circle cx="32" cy="32" r="'+r+'" stroke="'+color+'" stroke-width="7" fill="none" stroke-linecap="round" stroke-dasharray="'+circ+'" stroke-dashoffset="'+(circ-dash)+'"/>' +
    '</svg></div>';
}
function viewEvaluations(){
  const icons = ["clipboard-check","cpu","folder-kanban","presentation"];
  const cards = COURSE.evaluation.map(function(e,idx){
    return '<div class="card eval-card">' +
      '<div class="eval-card-top">' + evalDonut(e.pct, e.color) + '<div class="eval-icon" style="background:'+e.color+'22; color:'+e.color+';">'+icon(icons[idx])+'</div></div>' +
      '<div><div class="eval-pct" style="color:'+e.color+'">'+e.pct+'%</div><h4>'+e.label+'</h4></div>' +
    '</div>';
  }).join("");
  const bar = COURSE.evaluation.map(function(e){ return '<div style="flex:'+e.pct+'; background:'+e.color+';"></div>'; }).join("");
  const legend = COURSE.evaluation.map(function(e){ return '<div class="eval-legend-item"><span class="eval-legend-dot" style="background:'+e.color+'"></span>'+e.label+' \u00B7 '+e.pct+'%</div>'; }).join("");

  return '' +
    '<div class="page-head"><span class="eyebrow">Sistema de calificación</span><h1>Evaluación del curso</h1><p>Así se compone la calificación final de ' + COURSE.title + '.</p></div>' +
    '<div class="eval-grid">' + cards + '</div>' +
    '<div class="section-title"><h2>Distribución total</h2></div>' +
    '<div class="card" style="padding:24px;">' +
      '<div class="eval-summary-row">' + bar + '</div>' +
      '<div class="eval-summary-legend">' + legend + '</div>' +
    '</div>';
}

/* ---------- Mi progreso ---------- */
function viewProgress(){
  const s = overallStats();
  let pathHtml = "";
  COURSE.units.forEach(function(u,ui){
    const st = unitStats(ui);
    const cls = st.pct===100 ? "done" : st.done>0 ? "active" : "";
    const last = ui===COURSE.units.length-1;
    pathHtml += '<div class="unit-node-row"><div class="unit-node-col">' +
      '<div class="unit-node ' + cls + '">' + (st.pct===100?icon('check'):(ui+1)) + '</div>' +
      (!last ? '<div class="unit-connector ' + (st.pct===100?'done':'') + '"></div>' : '') +
      '</div><div style="flex:1; padding:' + (last?'0 0 4px 16px':'0 0 28px 16px') + ';">' +
      '<div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:7px;">' +
      '<strong style="font-size:13.5px; color:#fff;">' + escapeHtml(u.title) + '</strong>' +
      '<span class="mono" style="font-size:12px; color:var(--text-dim);">' + st.done + '/' + st.total + '</span></div>' +
      '<div class="bar"><div class="bar-fill" style="width:' + st.pct + '%"></div></div></div></div>';
  });

  let unitList = "";
  COURSE.units.forEach(function(u,ui){
    const st = unitStats(ui);
    unitList += '<div class="card unit-progress-item"><div class="unit-progress-item-top"><h4>Unidad ' + (ui+1) + ' \u00B7 ' + escapeHtml(u.title) + '</h4><span>' + st.pct + '%</span></div>' +
      '<div class="bar"><div class="bar-fill" style="width:' + st.pct + '%"></div></div></div>';
  });

  return '' +
    '<div class="page-head"><span class="eyebrow">Tu avance</span><h1>Mi progreso</h1><p>Visualiza cuánto has avanzado en ' + COURSE.title + ' y qué te falta para terminar.</p></div>' +
    '<div class="card" style="padding:26px;">' +
      '<span class="eyebrow">' + COURSE.title + '</span><h3 style="font-size:19px; margin-top:8px; color:#fff;">Tu progreso \u00B7 ' + s.pct + '% completado</h3>' +
      '<div class="bar" style="margin-top:16px; height:9px;"><div class="bar-fill" style="width:' + s.pct + '%"></div></div>' +
    '</div>' +
    '<div class="progress-grid" style="margin-top:20px;">' +
      '<div class="card stat-card"><div class="stat-icon v">' + icon('check') + '</div><div class="stat-value mono">' + s.done + '</div><div class="stat-label">Clases completadas</div></div>' +
      '<div class="card stat-card"><div class="stat-icon a">' + icon('hourglass') + '</div><div class="stat-value mono">' + s.pending + '</div><div class="stat-label">Clases pendientes</div></div>' +
      '<div class="card stat-card"><div class="stat-icon c">' + icon('layers') + '</div><div class="stat-value mono">' + s.unitsDone + '/' + s.totalUnits + '</div><div class="stat-label">Unidades completadas</div></div>' +
      '<div class="card stat-card"><div class="stat-icon b">' + icon('clipboard-list') + '</div><div class="stat-value mono">' + s.activitiesDone + '/' + s.activitiesTotal + '</div><div class="stat-label">Actividades realizadas</div></div>' +
    '</div>' +
    '<div class="stat-row" style="grid-template-columns:repeat(3,1fr); margin-top:18px;">' +
      '<div class="card stat-card"><div class="stat-icon v">' + icon('percent') + '</div><div class="stat-value mono">18/20</div><div class="stat-label">Promedio actual</div></div>' +
      '<div class="card stat-card"><div class="stat-icon c">' + icon('folder-kanban') + '</div><div class="stat-value mono">En curso</div><div class="stat-label">Proyecto</div></div>' +
      '<div class="card stat-card"><div class="stat-icon a">' + icon('presentation') + '</div><div class="stat-value mono">Pendiente</div><div class="stat-label">Presentación final</div></div>' +
    '</div>' +
    '<div class="section-title"><h2>Ruta del curso</h2></div>' +
    '<div class="card" style="padding:26px;"><div class="unit-path">' + pathHtml + '</div></div>' +
    '<div class="section-title"><h2>Progreso por unidad</h2></div>' +
    '<div class="unit-progress-list">' + unitList + '</div>';
}

/* ---------- Certificado ---------- */
function viewCertificate(){
  const s = overallStats();
  if(s.pct < 100){
    const reqs = [
      { met: s.pct>=100, label: "Completar el 100% de las clases del curso" },
      { met: false, label: "Entregar el proyecto final" },
      { met: false, label: "Realizar la presentación final" },
    ];
    return '' +
      '<div class="page-head"><span class="eyebrow">Certificación</span><h1>Certificado</h1></div>' +
      '<div class="cert-wrap"><div class="card cert-locked">' +
        '<div class="lock-badge">' + icon('lock') + '</div>' +
        '<h3>' + COURSE.brand + ' \u00B7 Certificado de finalización</h3>' +
        '<p><strong>' + COURSE.title + '</strong> \u00B7 ' + escapeHtml(state.studentName) + '<br>Tu certificado se habilitará cuando cumplas los requisitos del curso. Vas en ' + s.pct + '%.</p>' +
        '<div class="bar"><div class="bar-fill" style="width:' + s.pct + '%"></div></div>' +
        '<div class="cert-req-list">' + reqs.map(function(r){ return '<div class="cert-req '+(r.met?'met':'')+'">'+icon(r.met?'check-circle-2':'circle')+'<span>'+r.label+'</span></div>'; }).join("") + '</div>' +
        '<button class="btn btn-primary" style="margin-top:22px;" onclick="continueLearning()">Continuar aprendiendo</button>' +
      '</div></div>';
  }
  const today = new Date().toLocaleDateString("es-ES", { day:"numeric", month:"long", year:"numeric" });
  return '' +
    '<div class="page-head"><span class="eyebrow">Certificación</span><h1>¡Felicidades, completaste el curso!</h1><p>Vista previa de tu certificado de ' + COURSE.brand + '.</p></div>' +
    '<div class="cert-wrap"><div class="certificate" id="certPrint">' +
      '<div class="cert-crest">' + icon('award') + '</div>' +
      '<span class="cert-eyebrow">Certificado de finalización</span>' +
      '<span class="cert-title">' + COURSE.brand + '</span>' +
      '<h2 class="cert-name">' + escapeHtml(state.studentName) + '</h2>' +
      '<p class="cert-course">Ha completado satisfactoriamente el curso <b>' + COURSE.title + '</b></p>' +
      '<div class="cert-sign-row"><div class="cert-sign"><span>' + COURSE.brand + '</span>Institución emisora</div><div class="cert-sign"><span>' + TOTAL_LESSONS + ' clases</span>Carga del curso</div></div>' +
      '<div class="cert-date">Emitido el ' + today + '</div>' +
    '</div><button class="btn btn-primary" onclick="window.print()">Descargar / Imprimir certificado</button></div>';
}

/* ---------- Configuración ---------- */
function viewSettings(){
  return '' +
    '<div class="page-head"><span class="eyebrow">Tu cuenta</span><h1>Configuración</h1><p>Datos de demostración del estudiante para esta plataforma.</p></div>' +
    '<div class="card block"><div class="settings-form">' +
      '<div class="field"><label>Nombre completo</label><input type="text" id="nameInput" value="' + escapeAttr(state.studentName) + '"></div>' +
      '<button class="btn btn-primary" style="width:fit-content;" onclick="saveName()">Guardar cambios</button>' +
      '<div class="toggle-row"><div><span>Notificaciones por correo</span><small>Recibe recordatorios de tus clases pendientes</small></div><div class="switch on" onclick="this.classList.toggle(\'on\')"></div></div>' +
      '<div class="toggle-row"><div><span>Recordatorios diarios</span><small>Un aviso breve para mantener tu racha de estudio</small></div><div class="switch" onclick="this.classList.toggle(\'on\')"></div></div>' +
    '</div></div>';
}
function saveName(){
  const val = document.getElementById("nameInput").value.trim();
  if(val){ state.studentName = val; render(); showToast("Perfil actualizado", true); }
}

/* ---------- Utilidades ---------- */
function escapeHtml(str){
  str = str || "";
  return str.replace(/[&<>"']/g, function(c){ return {"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]; });
}
function escapeAttr(str){ return escapeHtml(str).replace(/`/g, "&#96;"); }

document.addEventListener("DOMContentLoaded", function(){ showView("dashboard"); });
</script>
</body>
</html>
