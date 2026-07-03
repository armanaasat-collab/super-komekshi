<!doctype html>
<html lang="kk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="theme-color" content="#E8A33D">
<meta name="description" content="Дүкен тізімі, бюджет және аударым көмекшісі">
<link rel="manifest" href="manifest.json">
<link rel="icon" href="icon-192.png" type="image/png">
<link rel="apple-touch-icon" href="apple-touch-icon.png">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Супер Көмекші">
<meta name="mobile-web-app-capable" content="yes">
<title>Супер Көмекші</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Unbounded:wght@400;600;700;800&family=Manrope:wght@400;500;600;700;800&display=swap');

:root{
  --bg: #202B21;
  --bg-deep: #171F18;
  --card: #283428;
  --card-raised: #2F3D2E;
  --tag: #EFE7D4;
  --tag-shadow: #C9BFA6;
  --apricot: #E8A33D;
  --apricot-dark: #C6821F;
  --tomato: #D4573B;
  --steppe: #86A667;
  --steppe-dark: #5E7E45;
  --cream: #F5EFDF;
  --muted: #93A38C;
  --line: rgba(245,239,223,0.12);
  --radius: 18px;
  --font-display: 'Unbounded', sans-serif;
  --font-body: 'Manrope', sans-serif;
}

*{box-sizing:border-box; -webkit-tap-highlight-color: transparent;}
html,body{margin:0; padding:0;}
body{
  font-family: var(--font-body);
  background: var(--bg-deep);
  color: var(--cream);
  min-height: 100vh;
  display:flex;
  justify-content:center;
}

#app{
  width:100%;
  max-width: 460px;
  min-height: 100vh;
  background:
    radial-gradient(ellipse 600px 300px at 50% -10%, rgba(232,163,61,0.10), transparent),
    var(--bg);
  display:none; 
  flex-direction:column;
  position:relative;
  overflow-x:hidden;
}

/* ===== Сплэш Экран (Loader) ===== */
#splash {
  position: fixed;
  top: 0; left: 0; width: 100%; height: 100%;
  background: var(--bg-deep);
  z-index: 9999;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  transition: opacity 0.5s ease;
}
#splash-brand {
  width: 70px; height: 70px;
  border-radius: 20px;
  background: linear-gradient(155deg, var(--apricot), var(--apricot-dark));
  display: flex; align-items: center; justify-content: center;
  margin-bottom: 20px;
  box-shadow: 0 8px 0 rgba(0,0,0,0.25);
  animation: pulse 1s infinite alternate;
}
#splash-brand svg { width: 40px; height: 40px; }
@keyframes pulse { from { transform: scale(1); } to { transform: scale(1.05); } }

/* ===== Елді таңдау терезесі ===== */
#country-modal {
  position: fixed;
  top: 0; left: 0; width: 100%; height: 100%;
  background: rgba(23,31,24,0.95);
  backdrop-filter: blur(10px);
  z-index: 9998;
  display: none;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
}
.country-box {
  background: var(--card);
  border: 1px solid var(--line);
  border-radius: var(--radius);
  width: 100%;
  max-width: 360px;
  padding: 24px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
}
.country-box h2 {
  font-family: var(--font-display);
  font-size: 18px;
  text-align: center;
  margin: 0 0 20px;
}
.country-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-height: 60vh;
  overflow-y: auto;
}
.country-btn {
  display: flex;
  align-items: center;
  gap: 12px;
  background: var(--bg-deep);
  border: 1px solid var(--line);
  padding: 14px;
  border-radius: 14px;
  color: var(--cream);
  font-family: var(--font-body);
  font-size: 16px;
  font-weight: 700;
  cursor: pointer;
  transition: transform 0.1s, background 0.2s;
}
.country-btn:active { transform: scale(0.97); background: var(--card-raised); }
.country-btn .flag { font-size: 24px; }
.country-btn .name { flex: 1; text-align: left; }
.country-btn .currency { color: var(--muted); font-size: 14px; }

/* ===== Header ===== */
.topbar{
  padding: 22px 20px 14px;
  display:flex;
  align-items:center;
  justify-content:space-between;
  border-bottom: 1px solid var(--line);
}
.brand{
  display:flex;
  align-items:center;
  gap:10px;
}
.brand-mark{
  width:38px; height:38px;
  border-radius: 10px;
  background: linear-gradient(155deg, var(--apricot), var(--apricot-dark));
  display:flex; align-items:center; justify-content:center;
  transform: rotate(-6deg);
  box-shadow: 0 4px 0 rgba(0,0,0,0.25);
}
.brand-mark svg{ width:20px; height:20px; }
.brand-text h1{
  font-family: var(--font-display);
  font-size: 16.5px;
  font-weight:700;
  margin:0;
  letter-spacing: 0.2px;
  line-height:1.1;
}
.brand-text span{
  font-size: 11px;
  color: var(--muted);
  font-weight:600;
  letter-spacing: 0.4px;
  text-transform: uppercase;
}
.header-total{
  text-align:right;
}
.header-total .num{
  font-family: var(--font-display);
  font-size: 19px;
  font-weight:700;
  color: var(--apricot);
  line-height:1;
}
.header-total .lbl{
  font-size:10px;
  color: var(--muted);
  text-transform:uppercase;
  letter-spacing:0.5px;
  font-weight:700;
}

/* ===== Pages ===== */
.page{
  flex:1;
  padding: 18px 16px 100px;
  display:none;
  animation: fadein 0.25s ease;
}
.page.active{ display:block; }
@keyframes fadein{ from{opacity:0; transform:translateY(6px);} to{opacity:1; transform:translateY(0);} }

/* ===== Add row ===== */
.add-panel{
  background: var(--card);
  border-radius: var(--radius);
  padding: 14px;
  margin-bottom: 18px;
  border: 1px solid var(--line);
}
.add-row{
  display:flex;
  gap:8px;
  margin-bottom:10px;
}
.add-row input{
  flex:1;
  min-width:0;
  background: var(--bg-deep);
  border: 1px solid var(--line);
  border-radius: 12px;
  padding: 12px 14px;
  color: var(--cream);
  font-family: var(--font-body);
  font-size: 14.5px;
  font-weight:600;
  outline:none;
}
.add-row input::placeholder{ color: var(--muted); font-weight:500; }
.add-row input.price-input{
  flex: 0 0 96px;
  text-align:right;
}
.btn-add-full{
  width:100%;
  background: var(--steppe);
  border:none;
  color:#16210F;
  font-family: var(--font-body);
  font-weight:800;
  font-size:14.5px;
  padding:13px;
  border-radius:12px;
  cursor:pointer;
  display:flex; align-items:center; justify-content:center; gap:8px;
  transition: transform 0.12s ease;
}
.btn-add-full:active{ transform: scale(0.97); }
.btn-add-full svg{ width:18px; height:18px; }

.quick-add-wrap{
  display:flex;
  flex-wrap:wrap;
  gap:8px;
  margin-top:2px;
}
.quick-chip{
  background: var(--card);
  border: 1px solid var(--line);
  color: var(--cream);
  border-radius: 20px;
  padding: 8px 14px 8px 10px;
  font-size: 12.5px;
  font-weight: 700;
  font-family: var(--font-body);
  cursor: pointer;
  display:flex;
  align-items:center;
  gap:6px;
  transition: transform 0.12s ease;
}
.quick-chip:active{ transform: scale(0.95); }
.quick-chip svg{ width:13px; height:13px; color: var(--apricot); flex:0 0 13px; }

/* ===== Tag list ===== */
.list-empty{
  text-align:center;
  padding: 50px 20px;
  color: var(--muted);
}
.list-empty svg{ width:52px; height:52px; opacity:0.5; margin-bottom:10px; }
.list-empty p{ font-size:13.5px; font-weight:600; margin:0; line-height:1.5; }

.tag-item{
  background: var(--tag);
  color: #2A2410;
  border-radius: 10px;
  padding: 10px 12px;
  margin-bottom: 10px;
  display:flex;
  align-items:center;
  gap:8px;
  position:relative;
  box-shadow: 0 3px 0 var(--tag-shadow);
  transition: transform 0.15s ease, opacity 0.15s ease;
}
.tag-item::before{
  content:'';
  position:absolute;
  left:-5px; top:50%;
  transform:translateY(-50%);
  width:11px; height:11px;
  border-radius:50%;
  background: var(--bg-deep);
  border: 2px solid var(--tag-shadow);
}
.tag-item.bought{
  opacity: 0.5;
}
.tag-item.bought .tag-name{
  text-decoration: line-through;
}
.tag-check{
  width:24px; height:24px;
  border-radius:7px;
  border: 2px solid #2A2410;
  flex:0 0 24px;
  display:flex; align-items:center; justify-content:center;
  cursor:pointer;
  background: transparent;
}
.tag-item.bought .tag-check{
  background: var(--steppe-dark);
  border-color: var(--steppe-dark);
}
.tag-check svg{ width:14px; height:14px; display:none; stroke:#fff; }
.tag-item.bought .tag-check svg{ display:block; }
.tag-name{
  flex:1;
  font-weight:700;
  font-size: 14.5px;
  min-width:0;
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
}
.tag-counter{
  display:flex;
  align-items:center;
  background: rgba(42,36,16,0.06);
  border-radius: 8px;
  padding: 2px;
}
.count-input{
  width: 30px;
  border: none;
  background: transparent;
  color: #2A2410;
  font-weight: 700;
  font-size: 12.5px;
  text-align: center;
  padding: 5px 0;
  font-family: var(--font-body);
}
.count-input:focus{ outline: none; background: rgba(42,36,16,0.10); border-radius:6px; }
.tag-price{
  font-family: var(--font-display);
  font-weight:700;
  font-size: 13.5px;
  background: rgba(42,36,16,0.08);
  border-radius: 8px;
  padding: 6px 8px;
  border:none;
  width: 75px;
  text-align:right;
  color:#2A2410;
  font-family: var(--font-body);
}
.tag-del{
  width:26px; height:26px;
  border-radius:7px;
  border:none;
  background:transparent;
  display:flex; align-items:center; justify-content:center;
  cursor:pointer;
  color:#8a7f55;
}
.tag-del svg{ width:16px; height:16px; }

/* ===== Section headers ===== */
.section-title-row{
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 4px 0 12px;
}
.section-title{
  font-family: var(--font-display);
  font-size: 12.5px;
  text-transform:uppercase;
  letter-spacing: 0.6px;
  color: var(--muted);
  font-weight:700;
  margin: 0;
}
.share-btn{
  background: none;
  border: none;
  color: var(--apricot);
  font-size: 12px;
  font-weight: 700;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 4px;
  padding: 4px 8px;
}
.share-btn svg{ width: 14px; height: 14px; }
.share-menu-wrap{ position:relative; }
.share-menu{
  display:none;
  position:absolute;
  top:32px; right:0;
  background: var(--card-raised);
  border:1px solid var(--line);
  border-radius:14px;
  padding:8px;
  width:180px;
  z-index:30;
  box-shadow: 0 10px 28px rgba(0,0,0,0.4);
}
.share-menu.open{ display:block; }
.share-menu button{
  width:100%;
  display:flex; align-items:center; gap:10px;
  background:none; border:none;
  color: var(--cream);
  font-family: var(--font-body);
  font-weight:700;
  font-size:13px;
  padding:10px 8px;
  border-radius:9px;
  cursor:pointer;
  text-align:left;
}
.share-menu button:active{ background: rgba(245,239,223,0.08); }
.share-menu button svg{ width:17px; height:17px; flex:0 0 17px; }
.share-menu .sm-wa{ color:#25D366; }
.share-menu .sm-tg{ color:#3AA4E9; }
.share-menu .sm-copy{ color: var(--apricot); }

/* ===== Header options menu ===== */
.topbar-right{ display:flex; align-items:center; gap:10px; }
.menu-wrap{ position:relative; }
.menu-btn{
  width:34px; height:34px;
  border-radius:10px;
  border:1px solid var(--line);
  background: var(--card);
  color: var(--cream);
  display:flex; align-items:center; justify-content:center;
  cursor:pointer;
  flex:0 0 34px;
}
.menu-btn svg{ width:18px; height:18px; }
.menu-dropdown{
  display:none;
  position:absolute;
  top:42px; right:0;
  background: var(--card-raised);
  border:1px solid var(--line);
  border-radius:14px;
  padding:8px;
  width:200px;
  z-index:40;
  box-shadow: 0 10px 28px rgba(0,0,0,0.4);
}
.menu-dropdown.open{ display:block; }
.menu-dropdown button{
  width:100%;
  display:flex; align-items:center; gap:10px;
  background:none; border:none;
  color: var(--cream);
  font-family: var(--font-body);
  font-weight:700;
  font-size:13px;
  padding:11px 9px;
  border-radius:9px;
  cursor:pointer;
  text-align:left;
}
.menu-dropdown button:active{ background: rgba(245,239,223,0.08); }
.menu-dropdown button svg{ width:17px; height:17px; flex:0 0 17px; }
.menu-dropdown .mi-clear{ color: var(--apricot); }
.menu-dropdown .mi-exit{ color: var(--tomato); }
.menu-divider{ height:1px; background: var(--line); margin:6px 2px; }

/* ===== Exit confirm modal ===== */
/* ===== Settings gear ===== */
.settings-btn{
  width:38px; height:38px;
  border-radius:12px;
  border:1px solid var(--line);
  background: var(--card);
  color: var(--cream);
  display:flex; align-items:center; justify-content:center;
  cursor:pointer;
}
.settings-btn svg{ width:19px; height:19px; }
.settings-btn:active{ background: var(--card-raised); transform: scale(0.95); }

/* ===== Settings / Lock overlays (shared) ===== */
.overlay-screen{
  position: fixed;
  top:0; left:0; width:100%; height:100%;
  background: var(--bg-deep);
  z-index: 9990;
  display:none;
  flex-direction:column;
  align-items:center;
}
.overlay-screen.open{ display:flex; }
.overlay-inner{
  width:100%; max-width:460px;
  height:100%;
  display:flex; flex-direction:column;
  overflow-y:auto;
}
.overlay-topbar{
  display:flex; align-items:center; gap:12px;
  padding: 22px 20px 14px;
  border-bottom: 1px solid var(--line);
  flex: 0 0 auto;
}
.overlay-back{
  width:36px; height:36px;
  border-radius:10px;
  border:1px solid var(--line);
  background: var(--card);
  color: var(--cream);
  display:flex; align-items:center; justify-content:center;
  cursor:pointer;
}
.overlay-back svg{ width:18px; height:18px; }
.overlay-title{
  font-family: var(--font-display);
  font-size: 17px;
  font-weight:700;
}
.overlay-body{ padding: 18px 16px 40px; flex:1; }

.settings-card{
  background: var(--card);
  border: 1px solid var(--line);
  border-radius: var(--radius);
  padding: 18px;
  margin-bottom: 16px;
}
.settings-card-title{
  font-family: var(--font-display);
  font-size: 13px;
  font-weight:700;
  color: var(--apricot);
  text-transform:uppercase;
  letter-spacing:0.4px;
  margin-bottom: 12px;
}
.settings-row{
  display:flex; align-items:center; justify-content:space-between;
  gap:10px;
  padding: 10px 0;
}
.settings-row-label{ font-size:14.5px; font-weight:600; }
.settings-row-sub{ font-size:12px; color:var(--muted); margin-top:2px; }
.lock-status-badge{
  font-size:12px; font-weight:700; padding:5px 10px; border-radius:20px;
}
.lock-status-badge.on{ background: rgba(134,166,103,0.18); color: var(--steppe); }
.lock-status-badge.off{ background: rgba(245,239,223,0.08); color: var(--muted); }

.lock-type-grid{ display:flex; flex-direction:column; gap:10px; margin-top:6px; }
.lock-type-btn{
  display:flex; align-items:center; gap:12px;
  background: var(--bg-deep);
  border:1px solid var(--line);
  border-radius:14px;
  padding:14px;
  color:var(--cream);
  cursor:pointer;
  font-family: var(--font-body);
}
.lock-type-btn:active{ transform:scale(0.98); background: var(--card-raised); }
.lock-type-icon{
  width:38px; height:38px; border-radius:10px;
  background: linear-gradient(155deg, var(--apricot), var(--apricot-dark));
  display:flex; align-items:center; justify-content:center; flex:0 0 auto;
}
.lock-type-icon svg{ width:19px; height:19px; }
.lock-type-name{ font-weight:700; font-size:14.5px; }
.lock-type-desc{ font-size:12px; color:var(--muted); margin-top:1px; }

.settings-plain-btn{
  width:100%;
  display:flex; align-items:center; gap:12px;
  background: transparent;
  border:none;
  border-top: 1px solid var(--line);
  padding:15px 2px;
  color:var(--cream);
  font-family: var(--font-body);
  font-size:14.5px;
  font-weight:600;
  cursor:pointer;
  text-align:left;
}
.settings-plain-btn:first-child{ border-top:none; }
.settings-plain-btn svg{ width:18px; height:18px; flex:0 0 18px; }
.settings-plain-btn.danger{ color: var(--tomato); }

/* ===== Lock entry UI (used in setup modal + lock screen) ===== */
.lock-entry-wrap{
  display:flex; flex-direction:column; align-items:center;
  padding: 30px 10px 10px;
}
.lock-entry-title{
  font-family: var(--font-display);
  font-size:16px; font-weight:700; margin-bottom:6px; text-align:center;
}
.lock-entry-sub{ font-size:13px; color:var(--muted); margin-bottom:26px; text-align:center; }
.lock-entry-error{ color:var(--tomato); font-size:13px; font-weight:700; min-height:18px; margin-top:14px; text-align:center; }

.pin-dots{ display:flex; gap:16px; margin-bottom:30px; }
.pin-dot{
  width:16px; height:16px; border-radius:50%;
  border:2px solid var(--muted);
  transition: background 0.15s, border-color 0.15s;
}
.pin-dot.filled{ background: var(--apricot); border-color: var(--apricot); }
.pin-pad{
  display:grid; grid-template-columns: repeat(3, 1fr);
  gap:14px; width:100%; max-width:280px;
}
.pin-key{
  aspect-ratio:1;
  border-radius:50%;
  border:1px solid var(--line);
  background: var(--card);
  color:var(--cream);
  font-family: var(--font-display);
  font-size:20px; font-weight:700;
  display:flex; align-items:center; justify-content:center;
  cursor:pointer;
}
.pin-key:active{ background: var(--card-raised); transform: scale(0.95); }
.pin-key.pin-del svg{ width:20px; height:20px; }
.pin-key.pin-empty{ visibility:hidden; }

.pattern-grid-wrap{ position:relative; width:240px; height:240px; margin-bottom:10px; touch-action:none; }
.pattern-grid{
  position:relative; width:100%; height:100%;
  display:grid; grid-template-columns: repeat(3,1fr); grid-template-rows: repeat(3,1fr);
}
.pattern-dot-cell{ display:flex; align-items:center; justify-content:center; }
.pattern-dot{
  width:22px; height:22px; border-radius:50%;
  border:2px solid var(--muted);
  background: var(--card);
  transition: background 0.12s, border-color 0.12s, transform 0.12s;
  pointer-events:none;
}
.pattern-dot.active{ background: var(--apricot); border-color: var(--apricot); transform: scale(1.2); }
.pattern-svg{ position:absolute; top:0; left:0; width:100%; height:100%; pointer-events:none; }
.pattern-svg line{ stroke: var(--apricot); stroke-width:4; stroke-linecap:round; }

.alpha-input-wrap{ width:100%; max-width:280px; }
.alpha-input{
  width:100%;
  background: var(--card);
  border:1px solid var(--line);
  border-radius:14px;
  padding:14px 16px;
  color:var(--cream);
  font-family: var(--font-body);
  font-size:16px;
  font-weight:700;
  outline:none;
  margin-bottom:16px;
  text-align:center;
}
.alpha-input::placeholder{ color: var(--muted); font-weight:600; }
.alpha-submit-btn{
  width:100%;
  background: linear-gradient(155deg, var(--apricot), var(--apricot-dark));
  border:none;
  border-radius:14px;
  padding:14px;
  color: #2A2410;
  font-family: var(--font-display);
  font-size:14.5px; font-weight:700;
  cursor:pointer;
}
.alpha-submit-btn:active{ transform: scale(0.98); }

.shake{ animation: shakeErr 0.4s; }
@keyframes shakeErr{
  10%,90%{ transform: translateX(-2px); }
  20%,80%{ transform: translateX(4px); }
  30%,50%,70%{ transform: translateX(-8px); }
  40%,60%{ transform: translateX(8px); }
}

#lock-screen{ z-index: 9999; }
#lock-screen .overlay-topbar{ border-bottom:none; justify-content:center; }
.lock-forgot-link{
  display:block;
  margin: 26px auto 0;
  background: none;
  border: none;
  color: var(--tomato);
  font-family: var(--font-body);
  font-size: 13px;
  font-weight:700;
  text-decoration: underline;
  cursor: pointer;
  padding: 8px;
}
#settings-modal{ z-index: 9985; }
#lock-setup-modal{ z-index: 9995; }

#exit-modal{
  position: fixed;
  top: 0; left: 0; width: 100%; height: 100%;
  background: rgba(23,31,24,0.95);
  backdrop-filter: blur(10px);
  z-index: 9998;
  display: none;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
}
.exit-box{
  background: var(--card);
  border: 1px solid var(--line);
  border-radius: var(--radius);
  width: 100%;
  max-width: 340px;
  padding: 24px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
}
.exit-box h2{
  font-family: var(--font-display);
  font-size: 17px;
  text-align: center;
  margin: 0 0 8px;
}
.exit-box p{
  font-size: 12.5px;
  color: var(--muted);
  font-weight:600;
  text-align:center;
  line-height:1.5;
  margin: 0 0 20px;
}
.exit-btn{
  width:100%;
  border:none;
  font-family: var(--font-body);
  font-weight:800;
  font-size:14px;
  padding:13px;
  border-radius:12px;
  cursor:pointer;
  margin-bottom:10px;
}
.exit-btn-danger{ background: var(--tomato); color:#fff; }
.exit-btn-safe{ background: var(--steppe); color:#16210F; }
.exit-cancel{
  width:100%;
  background:none;
  border:none;
  color: var(--muted);
  font-family: var(--font-body);
  font-weight:700;
  font-size:13px;
  padding:8px;
  cursor:pointer;
  margin-bottom:0;
}

/* ===== Budget page ===== */
.budget-card{
  background: var(--card);
  border-radius: var(--radius);
  padding: 20px;
  border:1px solid var(--line);
  margin-bottom:18px;
}
.budget-set{
  display:flex;
  align-items:center;
  gap:8px;
  margin-bottom:16px;
}
.budget-set label{
  font-size:12px;
  color:var(--muted);
  font-weight:700;
  text-transform:uppercase;
  letter-spacing:0.4px;
}
.budget-set input{
  flex:1;
  background: var(--bg-deep);
  border:1px solid var(--line);
  border-radius:10px;
  padding:9px 12px;
  color:var(--cream);
  font-family: var(--font-body);
  font-weight:700;
  font-size:14px;
  outline:none;
  text-align:right;
}
.gauge-wrap{
  text-align:center;
  padding: 6px 0 4px;
}
.gauge-num{
  font-family: var(--font-display);
  font-weight:800;
  font-size: 34px;
  letter-spacing:-0.5px;
}
.gauge-sub{
  font-size:12.5px;
  color:var(--muted);
  font-weight:600;
  margin-top:2px;
}
.gauge-bar{
  height:14px;
  border-radius:8px;
  background: var(--bg-deep);
  margin-top:16px;
  overflow:hidden;
  border:1px solid var(--line);
  position:relative;
}
.gauge-fill{
  height:100%;
  border-radius:8px;
  background: linear-gradient(90deg, var(--steppe-dark), var(--steppe));
  transition: width 0.4s ease, background 0.4s ease;
}
.gauge-fill.over{
  background: linear-gradient(90deg, var(--apricot-dark), var(--tomato));
}
.gauge-labels{
  display:flex;
  justify-content:space-between;
  margin-top:8px;
  font-size:11px;
  color:var(--muted);
  font-weight:700;
}

.stat-row{
  display:flex;
  justify-content:space-between;
  align-items:center;
  padding: 12px 4px;
  border-bottom: 1px solid var(--line);
}
.stat-row:last-child{ border-bottom:none; }
.stat-row .name{ font-size:13.5px; font-weight:600; color:var(--cream); }
.stat-row .val{ font-family: var(--font-display); font-size:13.5px; font-weight:700; color:var(--apricot); }

.checkout-btn{
  width:100%;
  background: var(--steppe-dark);
  border:none;
  color: var(--cream);
  font-family: var(--font-body);
  font-weight:800;
  font-size:14px;
  padding:14px;
  border-radius:14px;
  cursor:pointer;
  display:flex; align-items:center; justify-content:center; gap:8px;
  box-shadow: 0 3px 0 #46602f;
  transition: transform 0.1s;
}
.checkout-btn:active{ transform: translateY(2px); box-shadow:none; }
.checkout-btn svg{ width:17px; height:17px; }

/* ===== Stats page ===== */
.month-card{
  background: var(--card);
  border-radius: var(--radius);
  padding: 18px;
  border:1px solid var(--line);
  margin-bottom: 18px;
}
.bars{
  display:flex;
  align-items:flex-end;
  gap: 8px;
  height: 130px;
  padding-top:10px;
}
.bar-col{
  flex:1;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:flex-end;
  height:100%;
  gap:6px;
}
.bar-fill{
  width: 100%;
  max-width:26px;
  border-radius: 6px 6px 3px 3px;
  background: linear-gradient(180deg, var(--apricot), var(--apricot-dark));
  min-height:4px;
}
.bar-label{
  font-size: 9.5px;
  color: var(--muted);
  font-weight:700;
  text-transform:uppercase;
}
.top-item{
  display:flex;
  align-items:center;
  gap:10px;
  padding: 11px 4px;
  border-bottom:1px solid var(--line);
}
.top-item:last-child{ border-bottom:none; }
.top-rank{
  width:24px; height:24px;
  border-radius:7px;
  background: var(--card-raised);
  color: var(--apricot);
  font-family: var(--font-display);
  font-weight:700;
  font-size:11px;
  display:flex; align-items:center; justify-content:center;
  flex:0 0 24px;
}
.top-item .name{ flex:1; font-size:13.5px; font-weight:600; }
.top-item .val{ font-family: var(--font-display); font-weight:700; font-size:13px; color:var(--apricot); }

.empty-stats{
  text-align:center;
  padding:40px 20px;
  color:var(--muted);
}
.empty-stats svg{ width:46px; height:46px; opacity:0.5; margin-bottom:10px; }
.empty-stats p{ font-size:13px; font-weight:600; line-height:1.5; }

/* ===== Transfer / split page ===== */
.transfer-total-row{
  display:flex;
  justify-content:space-between;
  align-items:center;
  padding: 14px 4px;
  margin-top:2px;
}
.transfer-total-row .lbl{
  font-size:12.5px;
  color: var(--muted);
  font-weight:700;
  text-transform:uppercase;
  letter-spacing:0.4px;
}
.transfer-total-row .num{
  font-family: var(--font-display);
  font-size:22px;
  font-weight:800;
  color: var(--apricot);
}
.phone-row{
  display:flex;
  align-items:center;
  gap:10px;
  background: var(--bg-deep);
  border: 1px solid var(--line);
  border-radius: 12px;
  padding: 12px 14px;
  margin-bottom:14px;
}
.phone-row svg{ width:19px; height:19px; color: var(--apricot); flex:0 0 19px; }
.phone-row input{
  flex:1;
  min-width:0;
  background:none;
  border:none;
  color: var(--cream);
  font-family: var(--font-body);
  font-size: 15px;
  font-weight:700;
  outline:none;
  letter-spacing:0.4px;
}
.phone-row input::placeholder{ color: var(--muted); font-weight:600; }

.bank-select-wrap{ position:relative; margin-bottom:14px; }
.bank-select-row{
  display:flex;
  align-items:center;
  gap:10px;
  background: var(--bg-deep);
  border: 1px solid var(--line);
  border-radius: 12px;
  padding: 10px 10px 10px 14px;
}
.bank-chip{
  flex:1;
  display:flex;
  align-items:center;
  gap:10px;
  min-width:0;
}
.bank-chip-icon{
  width:30px; height:30px;
  border-radius:9px;
  flex:0 0 30px;
  display:flex; align-items:center; justify-content:center;
  color:#fff;
  font-family: var(--font-display);
  font-weight:800;
  font-size:13px;
}
.bank-chip-name{
  font-size:13.5px;
  font-weight:700;
  color: var(--cream);
  white-space:nowrap;
  overflow:hidden;
  text-overflow:ellipsis;
}
.dots-btn{
  width:34px; height:34px;
  flex:0 0 34px;
  border-radius:10px;
  border:1px solid var(--line);
  background: var(--card);
  color: var(--cream);
  display:flex; align-items:center; justify-content:center;
  cursor:pointer;
}
.dots-btn svg{ width:18px; height:18px; }
.bank-picker{
  display:none;
  position:absolute;
  top:calc(100% + 6px); left:0; right:0;
  background: var(--card-raised);
  border:1px solid var(--line);
  border-radius:14px;
  padding:8px;
  z-index:35;
  box-shadow: 0 10px 28px rgba(0,0,0,0.4);
}
.bank-picker.open{ display:block; }
.bank-picker-item{
  width:100%;
  display:flex; align-items:center; gap:10px;
  background:none; border:none;
  color: var(--cream);
  font-family: var(--font-body);
  font-weight:700;
  font-size:13.5px;
  padding:10px 8px;
  border-radius:9px;
  cursor:pointer;
  text-align:left;
}
.bank-picker-item:active{ background: rgba(245,239,223,0.08); }
.bank-picker-item.selected{ background: rgba(232,163,61,0.14); }
.bank-picker-icon{
  width:28px; height:28px;
  border-radius:8px;
  flex:0 0 28px;
  display:flex; align-items:center; justify-content:center;
  color:#fff;
  font-family: var(--font-display);
  font-weight:800;
  font-size:12px;
}
.transfer-note{
  font-size:11.5px;
  color: var(--muted);
  font-weight:500;
  line-height:1.5;
  margin: 10px 2px 16px;
  text-align:center;
}

/* ===== Bottom nav ===== */
.tabbar{
  position:sticky;
  bottom:0;
  left:0; right:0;
  background: rgba(23,31,24,0.92);
  backdrop-filter: blur(10px);
  border-top: 1px solid var(--line);
  display:flex;
  padding: 8px 10px calc(10px + env(safe-area-inset-bottom));
  gap:4px;
}
.tab-btn{
  flex:1;
  background:none;
  border:none;
  display:flex;
  flex-direction:column;
  align-items:center;
  gap:4px;
  padding: 8px 4px 6px;
  border-radius: 12px;
  cursor:pointer;
  color: var(--muted);
  transition: background 0.15s, color 0.15s;
}
.tab-btn svg{ width:21px; height:21px; }
.tab-btn span{ font-size:10.5px; font-weight:700; letter-spacing:0.2px; }
.tab-btn.active{ color: var(--apricot); background: rgba(232,163,61,0.10); }

/* Toast */
.toast{
  position:fixed;
  bottom: 90px;
  left:50%;
  transform: translateX(-50%) translateY(20px);
  background: var(--card-raised);
  color: var(--cream);
  padding: 11px 18px;
  border-radius: 30px;
  font-size:12.5px;
  font-weight:700;
  border: 1px solid var(--line);
  opacity:0;
  pointer-events:none;
  transition: all 0.25s ease;
  max-width: 85%;
  text-align:center;
  z-index:50;
  box-shadow: 0 8px 24px rgba(0,0,0,0.35);
}
.toast.show{ opacity:1; transform: translateX(-50%) translateY(0); }
::-webkit-scrollbar{ width:0; height:0; }

/* Conv styles */
.conv-input-field {
  flex:1;
  background:var(--bg-deep);
  border:1px solid var(--line);
  border-radius:12px;
  padding:12px 14px;
  color:var(--cream);
  font-family:var(--font-body);
  font-size:16px;
  font-weight:700;
  outline:none;
}
.conv-input-field:read-only { color:var(--apricot); }
</style>
</head>
<body>

<div id="splash">
  <div id="splash-brand">
    <svg viewBox="0 0 24 24" fill="none" stroke="#2A2410" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z"/><path d="M3 6h18"/><path d="M16 10a4 4 0 0 1-8 0"/></svg>
  </div>
</div>

<div id="country-modal">
  <div class="country-box">
    <h2>Елді таңдаңыз</h2>
    <div class="country-list" id="countryList">
      </div>
  </div>
</div>

<div id="exit-modal">
  <div class="exit-box">
    <h2 data-i18n="exitTitle">Шығу</h2>
    <p data-i18n="exitDesc">Деректеріңізбен не істейміз?</p>
    <button class="exit-btn exit-btn-safe" id="exitSaveBtn"><span data-i18n="exitSave">Шығу — деректерді сақтау</span></button>
    <button class="exit-btn exit-btn-danger" id="exitDeleteBtn"><span data-i18n="exitDelete">Шығу — деректерді жою</span></button>
    <button class="exit-cancel" id="exitCancelBtn"><span data-i18n="cancel">Бас тарту</span></button>
  </div>
</div>

<div id="app">
  <div class="topbar">
    <div class="brand">
      <div class="brand-mark">
        <svg viewBox="0 0 24 24" fill="none" stroke="#2A2410" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z"/><path d="M3 6h18"/><path d="M16 10a4 4 0 0 1-8 0"/></svg>
      </div>
      <div class="brand-text">
        <span data-i18n="shop">дүкенге бару</span>
        <h1 data-i18n="app">Супер Көмекші</h1>
      </div>
    </div>
    <div class="topbar-right">
      <div class="header-total">
        <div class="num" id="headerTotal">0 ₸</div>
        <div class="lbl" data-i18n="total">барлығы</div>
      </div>
      <button class="settings-btn" id="settingsBtn" aria-label="Баптаулар">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 1 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 1 1-2.83-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 1 1 2.83-2.83l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 1 1 2.83 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1Z"/></svg>
      </button>
    </div>
  </div>

  <div class="page active" id="page-list">
    <div class="section-title-row">
      <div class="section-title" data-i18n="list">Тізім</div>
      <div class="share-menu-wrap">
        <button class="share-btn" id="shareBtn">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="18" cy="5" r="3"/><circle cx="6" cy="12" r="3"/><circle cx="18" cy="19" r="3"/><path d="m8.59 13.51 6.83 3.98M15.41 6.51l-6.82 3.98"/></svg>
          <span data-i18n="share">Бөлісу</span>
        </button>
        <div class="share-menu" id="shareMenu">
          <button class="sm-wa" id="shareWaBtn">
            <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2a10 10 0 0 0-8.6 15.1L2 22l4.9-1.4A10 10 0 1 0 12 2Zm0 2a8 8 0 0 1 6.9 12.1l-.3.5.9 3.3-3.3-.9-.5.3A8 8 0 1 1 12 4Zm-3.3 4.1c-.2 0-.5.1-.7.4-.2.3-.9.9-.9 2.1s.9 2.4 1 2.6c.1.2 1.8 2.7 4.3 3.8.6.3 1.1.4 1.4.5.6.2 1.2.2 1.6.1.5-.1 1.5-.6 1.7-1.2.2-.6.2-1.1.2-1.2-.1-.1-.3-.2-.5-.3l-2-1c-.3-.1-.5-.2-.7.1l-.5.7c-.1.2-.3.2-.5.1-.3-.1-1.1-.4-2.1-1.3-.8-.7-1.3-1.6-1.5-1.9-.1-.2 0-.4.1-.5l.4-.5c.1-.2.2-.3.3-.5.1-.2 0-.4 0-.5l-.9-2.1c-.2-.5-.4-.4-.6-.4h-.5Z"/></svg>
            WhatsApp
          </button>
          <button class="sm-tg" id="shareTgBtn">
            <svg viewBox="0 0 24 24" fill="currentColor"><path d="M21.8 4.4 18.3 20c-.2 1-.9 1.2-1.7.8l-4.7-3.5-2.3 2.2c-.3.3-.5.5-1 .5l.3-4.9 8.9-8c.4-.4-.1-.6-.6-.2L6 12.8l-4.7-1.5c-1-.3-1-1 .2-1.5L20.5 3c.9-.3 1.6.2 1.3 1.4Z"/></svg>
            Telegram
          </button>
          <button class="sm-copy" id="shareCopyBtn">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><rect x="9" y="9" width="12" height="12" rx="2"/><path d="M5 15H4a1 1 0 0 1-1-1V4a1 1 0 0 1 1-1h10a1 1 0 0 1 1 1v1"/></svg>
            <span data-i18n="copy">Көшіру</span>
          </button>
        </div>
      </div>
    </div>
    <div id="listContainer"></div>

    <div class="add-panel">
      <div class="add-row">
        <input type="text" id="itemNameInput" data-i18n-ph="itemNamePlaceholder" placeholder="Заттың аты" maxlength="40">
        <input type="text" inputmode="numeric" class="price-input" id="itemPriceInput" placeholder="0">
      </div>
      <button class="btn-add-full" id="addBtn">
        <svg viewBox="0 0 24 24" fill="none" stroke="#16210F" stroke-width="2.6" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg>
        <span data-i18n="add">Тізімге қосу</span>
      </button>
    </div>

    <div class="section-title-row" id="quickAddRow" style="display:none;">
      <div class="section-title" data-i18n="freq">Жиі алатын заттар</div>
    </div>
    <div class="quick-add-wrap" id="quickAddWrap"></div>
  </div>

  <div class="page" id="page-budget">
    <div class="budget-card">
      <div class="budget-set">
        <label data-i18n="budget">Бюджет</label>
        <input type="text" inputmode="numeric" id="budgetInput" placeholder="10000">
        <span style="font-size:13px;color:var(--muted);font-weight:700;" id="budgetCurrencySym">₸</span>
      </div>

      <div class="gauge-wrap">
        <div class="gauge-num" id="gaugeNum">0 ₸</div>
        <div class="gauge-sub" id="gaugeSub" data-i18n="collected">жиналды</div>
        <div class="gauge-bar"><div class="gauge-fill" id="gaugeFill" style="width:0%"></div></div>
        <div class="gauge-labels">
          <span id="gaugeLeftLabel">0 ₸</span>
          <span id="gaugeRightLabel">Бюджет: 0 ₸</span>
        </div>
      </div>
    </div>

    <div class="section-title" data-i18n="topSpend">Ең қымбат заттар</div>
    <div class="budget-card" id="topSpendCard"></div>

    <button class="checkout-btn" id="checkoutBtn">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.3" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6 9 17l-5-5"/></svg>
      <span data-i18n="checkout">Дүкеннен шықтым — сақтау</span>
    </button>
  </div>

  <div class="page" id="page-stats">
    <div class="section-title" data-i18n="statsAll">Жалпы көрсеткіштер</div>
    <div class="month-card" style="display:flex; gap:6px;">
      <div style="flex:1; text-align:center;">
        <div style="font-family:var(--font-display);font-weight:800;font-size:17px;color:var(--apricot);" id="statTotalAll">0 ₸</div>
        <div style="font-size:9.5px;color:var(--muted);font-weight:700;text-transform:uppercase;letter-spacing:0.3px;margin-top:3px;" data-i18n="total">Барлығы</div>
      </div>
      <div style="flex:1; text-align:center; border-left:1px solid var(--line); border-right:1px solid var(--line);">
        <div style="font-family:var(--font-display);font-weight:800;font-size:17px;color:var(--apricot);" id="statTripCount">0</div>
        <div style="font-size:9.5px;color:var(--muted);font-weight:700;text-transform:uppercase;letter-spacing:0.3px;margin-top:3px;" data-i18n="shop">дүкенге бару</div>
      </div>
      <div style="flex:1; text-align:center;">
        <div style="font-family:var(--font-display);font-weight:800;font-size:17px;color:var(--apricot);" id="statAvgCheck">0 ₸</div>
        <div style="font-size:9.5px;color:var(--muted);font-weight:700;text-transform:uppercase;letter-spacing:0.3px;margin-top:3px;" data-i18n="avgCheck">Орташа чек</div>
      </div>
    </div>

    <div class="section-title" data-i18n="statsMonths">Айлар бойынша шығын</div>
    <div class="month-card">
      <div class="bars" id="monthBars"></div>
    </div>

    <div class="section-title" data-i18n="statsTop">Ең көп ақша не үшін кетті</div>
    <div class="month-card" id="topAllCard"></div>
  </div>

  <div class="page" id="page-transfer">
    <div class="transfer-total-row">
      <div class="lbl" data-i18n="totalAmount">Жалпы сома</div>
      <div class="num" id="transferTotal">0 ₸</div>
    </div>

    <div class="bank-select-wrap">
      <div class="bank-select-row">
        <div class="bank-chip">
          <div class="bank-chip-icon" id="bankChipIcon">K</div>
          <div class="bank-chip-name" id="bankChipName">Kaspi.kz</div>
        </div>
        <button class="dots-btn" id="bankDotsBtn" aria-label="Банк таңдау">
          <svg viewBox="0 0 24 24" fill="currentColor"><circle cx="5" cy="12" r="2"/><circle cx="12" cy="12" r="2"/><circle cx="19" cy="12" r="2"/></svg>
        </button>
      </div>
      <div class="bank-picker" id="bankPicker"></div>
    </div>

    <button class="checkout-btn" id="transferContinueBtn" style="background:var(--apricot-dark); box-shadow:0 3px 0 #8a5c14;">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
      <span data-i18n="continue">Жалғастыру</span>
    </button>
    <div class="transfer-note" id="transferNote">Басқанда сома алмасу буферіне көшіріледі және банк қосымшасы ашылады.</div>
  </div>

  <!-- ЖАҢА КОНВЕРТЕР БЕТІ -->
  <div class="page" id="page-converter">
    <div class="section-title" data-i18n="converter" style="margin-bottom: 6px;">Валюта конвертері</div>
    <div id="convUpdatedLabel" style="font-size:11.5px; color:var(--muted); margin-bottom:16px;"></div>
    
    <!-- Бірінші валюта (Берілетін сома) -->
    <div class="bank-select-wrap" style="display:flex; align-items:stretch; gap:10px; margin-bottom:14px;">
      <input type="text" inputmode="numeric" class="conv-input-field" id="convInput1" placeholder="0">
      
      <div class="bank-select-row" style="flex:1; margin:0;" id="convSelectRow1">
        <div class="bank-chip">
          <div class="bank-chip-icon" id="convIcon1" style="background:#333; font-size:16px;">🇰🇿</div>
          <div class="bank-chip-name" id="convName1">KZT</div>
        </div>
        <button class="dots-btn" id="convDots1">
          <svg viewBox="0 0 24 24" fill="currentColor"><circle cx="5" cy="12" r="2"/><circle cx="12" cy="12" r="2"/><circle cx="19" cy="12" r="2"/></svg>
        </button>
      </div>
      <div class="bank-picker" id="convPicker1"></div>
    </div>

    <!-- Екінші валюта (Алынатын сома) -->
    <div class="bank-select-wrap" style="display:flex; align-items:stretch; gap:10px;">
      <input type="text" inputmode="numeric" class="conv-input-field" id="convInput2" placeholder="0" readonly>
      
      <div class="bank-select-row" style="flex:1; margin:0;" id="convSelectRow2">
        <div class="bank-chip">
          <div class="bank-chip-icon" id="convIcon2" style="background:#333; font-size:16px;">🇺🇿</div>
          <div class="bank-chip-name" id="convName2">UZS</div>
        </div>
        <button class="dots-btn" id="convDots2">
          <svg viewBox="0 0 24 24" fill="currentColor"><circle cx="5" cy="12" r="2"/><circle cx="12" cy="12" r="2"/><circle cx="19" cy="12" r="2"/></svg>
        </button>
      </div>
      <div class="bank-picker" id="convPicker2"></div>
    </div>
  </div>

  <div class="tabbar">
    <button class="tab-btn active" data-page="list">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z"/><path d="M16 10a4 4 0 0 1-8 0"/></svg>
      <span data-i18n="list">Тізім</span>
    </button>
    <button class="tab-btn" data-page="budget">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="9"/><path d="M12 7v5l3 3"/></svg>
      <span data-i18n="budget">Бюджет</span>
    </button>
    <button class="tab-btn" data-page="stats">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 3v18h18"/><rect x="7" y="12" width="3" height="6"/><rect x="12" y="8" width="3" height="10"/><rect x="17" y="5" width="3" height="13"/></svg>
      <span data-i18n="stats">Статистика</span>
    </button>
    <button class="tab-btn" data-page="transfer">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="5" width="20" height="14" rx="2"/><path d="M2 10h20"/><path d="M6 15h4"/></svg>
      <span data-i18n="transfer">Аударым</span>
    </button>
    <!-- ЖАҢА КОНВЕРТЕР ТҮЙМЕСІ -->
    <button class="tab-btn" data-page="converter">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 3h5v5M4 21h5v-5M16 3l-7 7M4 21l7-7M4 11V6a2 2 0 0 1 2-2h14"/><path d="M20 13v5a2 2 0 0 1-2 2H4"/></svg>
      <span data-i18n="converter">Конвертер</span>
    </button>
  </div>

  <div class="toast" id="toast"></div>
</div>

<!-- ===== Баптаулар беті ===== -->
<div class="overlay-screen" id="settings-modal">
  <div class="overlay-inner">
    <div class="overlay-topbar">
      <button class="overlay-back" id="settingsBackBtn">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.3" stroke-linecap="round" stroke-linejoin="round"><path d="M15 18l-6-6 6-6"/></svg>
      </button>
      <div class="overlay-title">Баптаулар</div>
    </div>
    <div class="overlay-body">
      <div class="settings-card">
        <div class="settings-card-title">Қауіпсіздік</div>
        <div class="settings-row">
          <div>
            <div class="settings-row-label">Қосымшаны құлыптау</div>
            <div class="settings-row-sub">Ашқан сайын құпия код сұралады</div>
          </div>
          <span class="lock-status-badge off" id="lockStatusBadge">Өшірулі</span>
        </div>
        <div id="lockTypeChooser" class="lock-type-grid">
          <button class="lock-type-btn" data-type="pin">
            <div class="lock-type-icon"><svg viewBox="0 0 24 24" fill="none" stroke="#2A2410" stroke-width="2.3" stroke-linecap="round" stroke-linejoin="round"><rect x="4" y="9" width="16" height="4" rx="1"/><circle cx="7" cy="11" r="0.6"/><circle cx="12" cy="11" r="0.6"/><circle cx="17" cy="11" r="0.6"/></svg></div>
            <div>
              <div class="lock-type-name">Сандық код (PIN)</div>
              <div class="lock-type-desc">4 таңбалы сан</div>
            </div>
          </button>
          <button class="lock-type-btn" data-type="pattern">
            <div class="lock-type-icon"><svg viewBox="0 0 24 24" fill="none" stroke="#2A2410" stroke-width="2.3" stroke-linecap="round" stroke-linejoin="round"><circle cx="5" cy="5" r="1.4"/><circle cx="12" cy="5" r="1.4"/><circle cx="19" cy="5" r="1.4"/><circle cx="5" cy="12" r="1.4"/><circle cx="12" cy="12" r="1.4"/><circle cx="19" cy="12" r="1.4"/><circle cx="5" cy="19" r="1.4"/><circle cx="12" cy="19" r="1.4"/><circle cx="19" cy="19" r="1.4"/><path d="M5 5 12 12 19 19"/></svg></div>
            <div>
              <div class="lock-type-name">Өрнек (Pattern)</div>
              <div class="lock-type-desc">Нүктелерді сызу арқылы</div>
            </div>
          </button>
          <button class="lock-type-btn" data-type="alpha">
            <div class="lock-type-icon"><svg viewBox="0 0 24 24" fill="none" stroke="#2A2410" stroke-width="2.3" stroke-linecap="round" stroke-linejoin="round"><rect x="4" y="10" width="16" height="10" rx="2"/><path d="M8 10V7a4 4 0 0 1 8 0v3"/></svg></div>
            <div>
              <div class="lock-type-name">Әріп + сан</div>
              <div class="lock-type-desc">Құпия сөз (кемінде 4 таңба)</div>
            </div>
          </button>
        </div>
        <div id="lockManageRow" style="display:none;">
          <button class="settings-plain-btn" id="lockChangeBtn">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 20h9"/><path d="M16.5 3.5a2.1 2.1 0 0 1 3 3L7 19l-4 1 1-4Z"/></svg>
            <span>Құлыпты өзгерту</span>
          </button>
          <button class="settings-plain-btn danger" id="lockDisableBtn">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="11" width="18" height="10" rx="2"/><path d="M7 11V7a5 5 0 0 1 9.9-1"/></svg>
            <span>Құлыпты өшіру</span>
          </button>
        </div>
      </div>

      <div class="settings-card">
        <div class="settings-card-title">Деректер</div>
        <button class="settings-plain-btn" id="clearListBtn">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 6h18M8 6V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2m3 0-1 14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2L4 6"/></svg>
          <span data-i18n="clearList">Тізімді тазалау</span>
        </button>
        <button class="settings-plain-btn danger" id="clearAllBtn">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 6h18M8 6V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2m3 0-1 14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2L4 6"/><path d="M10 11v6M14 11v6"/></svg>
          <span data-i18n="clearAll">Барлық деректерді өшіру</span>
        </button>
        <button class="settings-plain-btn danger" id="exitBtn">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"/><path d="M16 17l5-5-5-5"/><path d="M21 12H9"/></svg>
          <span data-i18n="exit">Шығу</span>
        </button>
      </div>
    </div>
  </div>
</div>

<!-- ===== Құлыпты орнату модалы ===== -->
<div class="overlay-screen" id="lock-setup-modal">
  <div class="overlay-inner">
    <div class="overlay-topbar">
      <button class="overlay-back" id="lockSetupBackBtn">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.3" stroke-linecap="round" stroke-linejoin="round"><path d="M15 18l-6-6 6-6"/></svg>
      </button>
      <div class="overlay-title">Құлыпты орнату</div>
    </div>
    <div class="overlay-body" id="lockSetupBody"></div>
  </div>
</div>

<!-- ===== Кіру экраны (App Lock) ===== -->
<div class="overlay-screen" id="lock-screen">
  <div class="overlay-inner">
    <div class="overlay-topbar">
      <div class="overlay-title">🔒 Супер Көмекші</div>
    </div>
    <div class="overlay-body" id="lockScreenBody"></div>
  </div>
</div>

<script>
(function(){
  'use strict';

  // ---------- Аудармалар (Dictionaries) ----------
  const translations = {
    'kk': { itemNamePlaceholder: "Заттың аты", shop: "дүкенге бару", app: "Супер Көмекші", total: "барлығы", list: "Тізім", budget: "Бюджет", stats: "Статистика", transfer: "Аударым", converter: "Конвертер", add: "Тізімге қосу", checkout: "Дүкеннен шықтым — сақтау", continue: "Жалғастыру", share: "Бөлісу", copy: "Көшіру", freq: "Жиі алатын заттар", collected: "жиналды", topSpend: "Ең қымбат заттар", statsAll: "Жалпы көрсеткіштер", avgCheck: "Орташа чек", statsMonths: "Айлар бойынша шығын", statsTop: "Ең көп ақша не үшін кетті", bill: "Есеп", totalAmount: "Жалпы сома", phoneTitle: "Аударатын адамның нөмірі", listEmpty: "Тізім бос. Затты жаз.", saveAlert: "Сақталды!", clearList: "Тізімді тазалау", clearAll: "Барлық деректерді өшіру", clearAllConfirm: "Барлық деректер (тізім, бюджет, тарих, тіл) толығымен өшіріледі. Жалғастырасыз ба?", clearedAllAlert: "Барлық деректер өшірілді", exit: "Шығу", exitTitle: "Шығу", exitDesc: "Деректеріңізбен не істейміз?", exitSave: "Шығу — деректерді сақтау", exitDelete: "Шығу — деректерді жою", cancel: "Бас тарту", clearedAlert: "Тізім тазаланды", deletedAlert: "Деректер жойылды" },
    'ru': { itemNamePlaceholder: "Название товара", shop: "поход в магазин", app: "Супер Помощник", total: "итого", list: "Список", budget: "Бюджет", stats: "Статистика", transfer: "Перевод", converter: "Конвертер", add: "Добавить в список", checkout: "Вышел из магазина — сохранить", continue: "Продолжить", share: "Поделиться", copy: "Копировать", freq: "Частые покупки", collected: "собрано", topSpend: "Самые дорогие", statsAll: "Общие показатели", avgCheck: "Средний чек", statsMonths: "Расход по месяцам", statsTop: "На что ушло больше всего", bill: "Счет", totalAmount: "Общая сумма", phoneTitle: "Номер для перевода", listEmpty: "Список пуст. Добавьте товары.", saveAlert: "Сохранено!", clearList: "Очистить список", clearAll: "Удалить все данные", clearAllConfirm: "Все данные (список, бюджет, история, язык) будут полностью удалены. Продолжить?", clearedAllAlert: "Все данные удалены", exit: "Выйти", exitTitle: "Выход", exitDesc: "Что сделать с вашими данными?", exitSave: "Выйти — сохранить данные", exitDelete: "Выйти — удалить данные", cancel: "Отмена", clearedAlert: "Список очищен", deletedAlert: "Данные удалены" },
    'uz': { itemNamePlaceholder: "Mahsulot nomi", shop: "do'konga borish", app: "Super Yordamchi", total: "jami", list: "Ro'yxat", budget: "Budjet", stats: "Statistika", transfer: "O'tkazma", converter: "Konverter", add: "Ro'yxatga qo'shish", checkout: "Do'kondan chiqdim — saqlash", continue: "Davom etish", share: "Ulashish", copy: "Nusxalash", freq: "Ko'p olinadigan", collected: "yig'ildi", topSpend: "Eng qimmat", statsAll: "Umumiy", avgCheck: "O'rtacha chek", statsMonths: "Oylar bo'yicha", statsTop: "Eng ko'p xarajat", bill: "Hisob", totalAmount: "Umumiy summa", phoneTitle: "O'tkazma raqami", listEmpty: "Ro'yxat bo'sh.", saveAlert: "Saqlandi!", clearList: "Ro'yxatni tozalash", clearAll: "Barcha ma'lumotni o'chirish", clearAllConfirm: "Barcha ma'lumotlar (ro'yxat, byudjet, tarix, til) butunlay o'chiriladi. Davom etasizmi?", clearedAllAlert: "Barcha ma'lumot o'chirildi", exit: "Chiqish", exitTitle: "Chiqish", exitDesc: "Ma'lumotlaringiz bilan nima qilamiz?", exitSave: "Chiqish — ma'lumotni saqlash", exitDelete: "Chiqish — ma'lumotni o'chirish", cancel: "Bekor qilish", clearedAlert: "Ro'yxat tozalandi", deletedAlert: "Ma'lumotlar o'chirildi" },
    'ky': { itemNamePlaceholder: "Нерсенин аты", shop: "дүкөнгө баруу", app: "Супер Жардамчы", total: "баардыгы", list: "Тизме", budget: "Бюджет", stats: "Статистика", transfer: "Котормо", converter: "Конвертер", add: "Тизмеге кошуу", checkout: "Дүкөндөн чыктым — сактоо", continue: "Улантуу", share: "Бөлүшүү", copy: "Көчүрүү", freq: "Көп алынуучу", collected: "чогултулду", topSpend: "Эң кымбат", statsAll: "Жалпы", avgCheck: "Орточо чек", statsMonths: "Айлар боюнча", statsTop: "Эң көп каражат", bill: "Эсеп", totalAmount: "Жалпы сумма", phoneTitle: "Которуу номери", listEmpty: "Тизме бош.", saveAlert: "Сакталды!", clearList: "Тизмени тазалоо", clearAll: "Бардык дайыектарды өчүрүү", clearAllConfirm: "Бардык дайыектар (тизме, бюджет, тарых, тил) толугу менен өчүрүлөт. Улантасызбы?", clearedAllAlert: "Бардык дайыектар өчүрүлдү", exit: "Чыгуу", exitTitle: "Чыгуу", exitDesc: "Дайыектарыңыз менен эмне кылабыз?", exitSave: "Чыгуу — дайыектарды сактоо", exitDelete: "Чыгуу — дайыектарды өчүрүү", cancel: "Артка", clearedAlert: "Тизме тазаланды", deletedAlert: "Дайыектар өчүрүлдү" },
    'zh': { itemNamePlaceholder: "物品名称", shop: "去商店", app: "超级助手", total: "总计", list: "列表", budget: "预算", stats: "统计", transfer: "转账", converter: "汇率换算", add: "添加到列表", checkout: "离开商店 — 保存", continue: "继续", share: "分享", copy: "复制", freq: "常买物品", collected: "已收集", topSpend: "最贵物品", statsAll: "总览", avgCheck: "平均账单", statsMonths: "按月支出", statsTop: "最大开销", bill: "账单", totalAmount: "总金额", phoneTitle: "转账号码", listEmpty: "列表为空。", saveAlert: "已保存！", clearList: "清空列表", clearAll: "删除所有数据", clearAllConfirm: "所有数据（列表、预算、历史记录、语言）将被完全删除。是否继续？", clearedAllAlert: "所有数据已删除", exit: "退出", exitTitle: "退出", exitDesc: "您的数据要如何处理？", exitSave: "退出 — 保存数据", exitDelete: "退出 — 删除数据", cancel: "取消", clearedAlert: "列表已清空", deletedAlert: "数据已删除" },
    'tr': { itemNamePlaceholder: "Ürün adı", shop: "alışverişe git", app: "Süper Yardımcı", total: "toplam", list: "Liste", budget: "Bütçe", stats: "İstatistik", transfer: "Transfer", converter: "Çevirici", add: "Listeye ekle", checkout: "Çıktım — kaydet", continue: "Devam et", share: "Paylaş", copy: "Kopyala", freq: "Sık alınanlar", collected: "toplanan", topSpend: "En pahalı", statsAll: "Genel", avgCheck: "Ortalama fiş", statsMonths: "Aylık gider", statsTop: "En çok harcanan", bill: "Hesap", totalAmount: "Toplam", phoneTitle: "Transfer numarası", listEmpty: "Liste boş.", saveAlert: "Kaydedildi!", clearList: "Listeyi temizle", clearAll: "Tüm verileri sil", clearAllConfirm: "Tüm veriler (liste, bütçe, geçmiş, dil) tamamen silinecek. Devam edilsin mi?", clearedAllAlert: "Tüm veriler silindi", exit: "Çıkış", exitTitle: "Çıkış", exitDesc: "Verilerinizle ne yapalım?", exitSave: "Çıkış — verileri kaydet", exitDelete: "Çıkış — verileri sil", cancel: "Vazgeç", clearedAlert: "Liste temizlendi", deletedAlert: "Veriler silindi" },
    'en': { itemNamePlaceholder: "Item name", shop: "go to shop", app: "Super Helper", total: "total", list: "List", budget: "Budget", stats: "Stats", transfer: "Transfer", converter: "Converter", add: "Add to list", checkout: "Left shop — save", continue: "Continue", share: "Share", copy: "Copy", freq: "Frequent items", collected: "collected", topSpend: "Top spends", statsAll: "Overall stats", avgCheck: "Avg Check", statsMonths: "Monthly spend", statsTop: "Top categories", bill: "Bill", totalAmount: "Total Amount", phoneTitle: "Transfer Number", listEmpty: "List is empty.", saveAlert: "Saved!", clearList: "Clear list", clearAll: "Delete all data", clearAllConfirm: "All data (list, budget, history, language) will be permanently deleted. Continue?", clearedAllAlert: "All data deleted", exit: "Exit", exitTitle: "Exit", exitDesc: "What should we do with your data?", exitSave: "Exit — keep data", exitDelete: "Exit — delete data", cancel: "Cancel", clearedAlert: "List cleared", deletedAlert: "Data deleted" }
  };

  // Конвертерге арналған курстар (1 USD-ге шаққандағы шамамен)
  const countriesConfig = [
    { code: 'KZ', lang: 'kk', rate: 475, name: 'Қазақстан', flag: '🇰🇿', currency: '₸', banks: [
        { name: 'Kaspi.kz', color:'#E8342A', link: 'kaspi://', url: 'https://kaspi.kz/' },
        { name: 'Halyk Bank', color:'#00A651', link: 'homebank://', url: 'https://homebank.kz/' },
        { name: 'Jusan Bank', color:'#6B2C91', link: 'jusan://', url: 'https://jusan.kz/' }
      ] },
    { code: 'RU', lang: 'ru', rate: 89, name: 'Россия', flag: '🇷🇺', currency: '₽', banks: [
        { name: 'Сбербанк', color:'#21A038', link: 'sberbankonline://', url: 'https://online.sberbank.ru/' },
        { name: 'T-Bank', color:'#FFDD2D', link: 'tinkoff://', url: 'https://www.tbank.ru/' },
        { name: 'ВТБ', color:'#00549F', link: 'vtbonline://', url: 'https://www.vtb.ru/' }
      ] },
    { code: 'UZ', lang: 'uz', rate: 12600, name: 'Oʻzbekiston', flag: '🇺🇿', currency: 'soʻm', banks: [
        { name: 'Click', color:'#0072CE', link: 'clickuz://', url: 'https://click.uz/' },
        { name: 'Payme', color:'#00CFC1', link: 'payme://', url: 'https://payme.uz/' },
        { name: 'Apelsin', color:'#FF6A00', link: 'apelsin://', url: 'https://apelsin.uz/' }
      ] },
    { code: 'KG', lang: 'ky', rate: 86, name: 'Кыргызстан', flag: '🇰🇬', currency: 'с', banks: [
        { name: 'MBank', color:'#7B2FF7', link: 'mbank://', url: 'https://mbank.kg/' },
        { name: 'Optima Bank', color:'#0090D4', link: 'optimabank://', url: 'https://optimabank.kg/' },
        { name: 'O!Money', color:'#EE3124', link: 'omoney://', url: 'https://o.kg/' }
      ] },
    { code: 'CN', lang: 'zh', rate: 7.25, name: '中国', flag: '🇨🇳', currency: '¥', banks: [
        { name: 'Alipay', color:'#1677FF', link: 'alipays://', url: 'https://www.alipay.com/' },
        { name: 'WeChat Pay', color:'#07C160', link: 'weixin://', url: 'https://pay.weixin.qq.com/' }
      ] },
    { code: 'TR', lang: 'tr', rate: 32, name: 'Türkiye', flag: '🇹🇷', currency: '₺', banks: [
        { name: 'Papara', color:'#7857FF', link: 'papara://', url: 'https://www.papara.com/' },
        { name: 'Ziraat Bankası', color:'#00713C', link: 'ziraatmobile://', url: 'https://www.ziraatbank.com.tr/' },
        { name: 'İş Bankası', color:'#003D7C', link: 'isbankasi://', url: 'https://www.isbank.com.tr/' }
      ] },
    { code: 'US', lang: 'en', rate: 1, name: 'United States', flag: '🇺🇸', currency: '$', banks: [
        { name: 'PayPal', color:'#0070BA', link: 'paypal://', url: 'https://www.paypal.com/' },
        { name: 'Venmo', color:'#3D95CE', link: 'venmo://', url: 'https://venmo.com/' },
        { name: 'Zelle', color:'#6D1ED4', link: 'zellepay://', url: 'https://www.zellepay.com/' }
      ] }
  ];

  let currentLang = 'kk';
  let currentCurrency = '₸';
  let currentBanks = countriesConfig[0].banks;
  let currentBank = currentBanks[0];

  const $ = (id) => document.getElementById(id);

  function bankInitial(name){
    return (name||'?').trim().charAt(0).toUpperCase();
  }

  function renderBankChip(){
    $('bankChipIcon').textContent = bankInitial(currentBank.name);
    $('bankChipIcon').style.background = currentBank.color;
    $('bankChipName').textContent = currentBank.name;
  }

  function renderBankPicker(){
    const picker = $('bankPicker');
    picker.innerHTML = currentBanks.map((b, i) => `
      <button class="bank-picker-item${b.name===currentBank.name ? ' selected' : ''}" data-idx="${i}">
        <div class="bank-picker-icon" style="background:${b.color}">${bankInitial(b.name)}</div>
        <span>${b.name}</span>
      </button>`).join('');
    picker.querySelectorAll('.bank-picker-item').forEach(btn=>{
      btn.addEventListener('click', ()=>{
        currentBank = currentBanks[btn.dataset.idx];
        renderBankChip();
        picker.querySelectorAll('.bank-picker-item').forEach(b=> b.classList.remove('selected'));
        btn.classList.add('selected');
        picker.classList.remove('open');
        launchBankApp(currentBank);
      });
    });
  }

  function setCountryBanks(c){
    currentBanks = c.banks;
    currentBank = c.banks[0];
    renderBankChip();
    renderBankPicker();
  }

  $('bankDotsBtn').addEventListener('click', (e)=>{
    e.stopPropagation();
    $('bankPicker').classList.toggle('open');
  });

  // ========== КОНВЕРТЕР ЛОГИКАСЫ ==========
  let convCountry1 = countriesConfig[0]; // KZT
  let convCountry2 = countriesConfig[2]; // UZS

  // ISO-4217 код сәйкестігі (open.er-api.com сұрауы үшін)
  const FX_ISO_MAP = { KZ:'KZT', RU:'RUB', UZ:'UZS', KG:'KGS', CN:'CNY', TR:'TRY', US:'USD' };

  function todayStr(){
    const d = new Date();
    return d.getFullYear()+'-'+(d.getMonth()+1)+'-'+d.getDate();
  }

  function applyRatesToCountries(rates){
    countriesConfig.forEach(c=>{
      const iso = FX_ISO_MAP[c.code];
      if(iso && rates[iso]) c.rate = rates[iso];
    });
  }

  function renderConvUpdatedLabel(dateStr, isLive){
    const el = $('convUpdatedLabel');
    if(!el) return;
    el.textContent = isLive
      ? ('Курстар нақты уақытта • жаңартылды: ' + dateStr)
      : ('Курстар offline (сақталған мән) • ' + dateStr);
  }

  async function refreshFxRates(){
    let cache = null;
    try{ cache = JSON.parse(localStorage.getItem('sk-fx-rates') || 'null'); }catch(e){}

    // Кэште бүгінгі күннің деректері бар болса, сол жеткілікті — қайта сұратпаймыз
    if(cache && cache.date === todayStr() && cache.rates){
      applyRatesToCountries(cache.rates);
      renderConvUpdatedLabel(cache.date, true);
      return;
    }

    // Интернет болмаса немесе сұрау сәтсіз болса — ескі кэш немесе кодтағы бастапқы мән қалады
    if(cache && cache.rates){
      applyRatesToCountries(cache.rates);
      renderConvUpdatedLabel(cache.date, false);
    }

    try{
      const res = await fetch('https://open.er-api.com/v6/latest/USD');
      const data = await res.json();
      if(data && data.result === 'success' && data.rates){
        applyRatesToCountries(data.rates);
        localStorage.setItem('sk-fx-rates', JSON.stringify({ date: todayStr(), rates: data.rates }));
        renderConvUpdatedLabel(todayStr(), true);
        calculateConv();
        updateConvUI();
      }
    }catch(e){
      // желі жоқ — үнсіз қалады, бұрынғы/кэштелген курс қолданыла береді
    }
  }

  function setupConverter() {
    const html = countriesConfig.map((c, i) => `
      <button class="bank-picker-item" data-idx="${i}">
        <div class="bank-picker-icon" style="background:var(--card-raised); font-size:16px;">${c.flag}</div>
        <span>${c.currency} (${c.name})</span>
      </button>`).join('');
    
    $('convPicker1').innerHTML = html;
    $('convPicker2').innerHTML = html;

    $('convPicker1').querySelectorAll('.bank-picker-item').forEach(btn => {
      btn.addEventListener('click', () => {
        convCountry1 = countriesConfig[btn.dataset.idx];
        updateConvUI();
        $('convPicker1').classList.remove('open');
        calculateConv();
      });
    });

    $('convPicker2').querySelectorAll('.bank-picker-item').forEach(btn => {
      btn.addEventListener('click', () => {
        convCountry2 = countriesConfig[btn.dataset.idx];
        updateConvUI();
        $('convPicker2').classList.remove('open');
        calculateConv();
      });
    });
  }

  function updateConvUI() {
    $('convIcon1').textContent = convCountry1.flag;
    $('convName1').textContent = convCountry1.currency;
    $('convIcon2').textContent = convCountry2.flag;
    $('convName2').textContent = convCountry2.currency;
  }

  function calculateConv() {
    let val = parseFloat($('convInput1').value.replace(/[^0-9.]/g, '')) || 0;
    if (val === 0) { $('convInput2').value = ''; return; }
    let result = (val / convCountry1.rate) * convCountry2.rate;
    
    // Бөліктерсіз немесе 2 нүктеге дейін дөңгелектеу
    if (result % 1 === 0) {
      $('convInput2').value = result;
    } else {
      $('convInput2').value = result.toFixed(2);
    }
  }

  $('convInput1').addEventListener('input', function() {
    this.value = this.value.replace(/[^0-9.]/g, '');
    calculateConv();
  });

  $('convDots1').addEventListener('click', (e) => {
    e.stopPropagation();
    $('convPicker1').classList.toggle('open');
  });
  $('convDots2').addEventListener('click', (e) => {
    e.stopPropagation();
    $('convPicker2').classList.toggle('open');
  });

  // Global click event to close dropdowns
  document.addEventListener('click', (e)=>{
    const picker = $('bankPicker');
    if(picker && picker.classList.contains('open') && !picker.contains(e.target) && e.target.id !== 'bankDotsBtn'){
      picker.classList.remove('open');
    }
    const convP1 = $('convPicker1');
    if(convP1 && convP1.classList.contains('open') && !convP1.contains(e.target) && e.target.id !== 'convDots1'){
      convP1.classList.remove('open');
    }
    const convP2 = $('convPicker2');
    if(convP2 && convP2.classList.contains('open') && !convP2.contains(e.target) && e.target.id !== 'convDots2'){
      convP2.classList.remove('open');
    }
  });
  // ==========================================

  function applyLanguage(lang) {
    const dict = translations[lang] || translations['kk'];
    document.querySelectorAll('[data-i18n]').forEach(el => {
      const key = el.getAttribute('data-i18n');
      if(dict[key]) el.textContent = dict[key];
    });
    document.querySelectorAll('[data-i18n-ph]').forEach(el => {
      const key = el.getAttribute('data-i18n-ph');
      if(dict[key]) el.placeholder = dict[key];
    });
    $('budgetCurrencySym').textContent = currentCurrency;
    renderList();
    renderBudget();
    renderStats();
    renderTransfer();
  }

  function getI18n(key) {
    return (translations[currentLang] || translations['kk'])[key] || key;
  }

  // ---------- Loader & Startup Logic ----------
  window.addEventListener('load', () => {
    const splash = $('splash');
    const countryModal = $('country-modal');
    const app = $('app');

    setTimeout(() => {
      splash.style.opacity = 0;
      setTimeout(() => {
        splash.style.display = 'none';

        function revealApp(){
          app.style.display = 'flex';
          const savedCountry = localStorage.getItem('sk-country');
          if (savedCountry) {
            const c = JSON.parse(savedCountry);
            currentLang = c.lang;
            currentCurrency = c.currency;
            setCountryBanks(c);
            applyLanguage(currentLang);
          } else {
            setupCountryList();
            countryModal.style.display = 'flex';
          }
        }

        if(lockConfig.enabled){
          showAppLockScreen(revealApp);
        } else {
          revealApp();
        }
      }, 500);
    }, 1000);
  });

  function setupCountryList() {
    const list = $('countryList');
    list.innerHTML = countriesConfig.map((c, i) => `
      <button class="country-btn" data-idx="${i}">
        <span class="flag">${c.flag}</span>
        <span class="name">${c.name}</span>
        <span class="currency">${c.currency}</span>
      </button>
    `).join('');

    list.querySelectorAll('.country-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        const c = countriesConfig[btn.dataset.idx];
        currentLang = c.lang;
        currentCurrency = c.currency;
        setCountryBanks(c);

        localStorage.setItem('sk-country', JSON.stringify(c));
        
        $('country-modal').style.display = 'none';
        applyLanguage(currentLang);
        showToast(c.name + ' таңдалды');
      });
    });
  }

  // ---------- State ----------
  let items = [];
  let budget = 0;
  let archive = [];
  let ready = false;

  async function loadAll(){
    try{ const r = localStorage.getItem('sk-items'); items = r ? JSON.parse(r) : []; }catch(e){ items = []; }
    try{ const r = localStorage.getItem('sk-budget'); budget = r ? JSON.parse(r) : 0; }catch(e){ budget = 0; }
    try{ const r = localStorage.getItem('sk-archive'); archive = r ? JSON.parse(r) : []; }catch(e){ archive = []; }
    ready = true;
  }
  async function saveItems(){ try{ localStorage.setItem('sk-items', JSON.stringify(items)); }catch(e){} }
  async function saveBudget(){ try{ localStorage.setItem('sk-budget', JSON.stringify(budget)); }catch(e){} }
  async function saveArchive(){ try{ localStorage.setItem('sk-archive', JSON.stringify(archive)); }catch(e){} }

  function fmt(n){
    n = Math.round(n || 0);
    return n.toLocaleString('ru-RU') + ' ' + currentCurrency;
  }
  function showToast(msg){
    const t = $('toast');
    t.textContent = msg;
    t.classList.add('show');
    clearTimeout(showToast._tm);
    showToast._tm = setTimeout(()=> t.classList.remove('show'), 2200);
  }

  // ---------- Tabs ----------
  document.querySelectorAll('.tab-btn').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
      document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
      btn.classList.add('active');
      $('page-'+btn.dataset.page).classList.add('active');
      if(btn.dataset.page === 'budget') renderBudget();
      if(btn.dataset.page === 'stats') renderStats();
      if(btn.dataset.page === 'transfer') renderTransfer();
    });
  });

  function currentTotal(){
    return items.reduce((s,it)=> s + ((Number(it.price)||0) * (it.count||1)), 0);
  }

  function renderList(){
    const c = $('listContainer');
    c.innerHTML = '';
    if(items.length === 0){
      c.innerHTML = `<div class="list-empty">
        <svg viewBox="0 0 24 24" fill="none" stroke="var(--muted)" stroke-width="1.6"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z"/><path d="M16 10a4 4 0 0 1-8 0"/></svg>
        <p>${getI18n('listEmpty')}</p>
      </div>`;
    } else {
      items.forEach(it=>{
        if(!it.count) it.count = 1;
        const row = document.createElement('div');
        row.className = 'tag-item' + (it.bought ? ' bought' : '');
        row.innerHTML = `
          <button class="tag-check" data-id="${it.id}">
            <svg viewBox="0 0 24 24" fill="none" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6 9 17l-5-5"/></svg>
          </button>
          <div class="tag-name">${escapeHtml(it.name)}</div>
          <div class="tag-counter">
            <input class="count-input" data-id="${it.id}" inputmode="numeric" value="${it.count}">
          </div>
          <input class="tag-price" data-id="${it.id}" inputmode="numeric" value="${it.price ? it.price : ''}" placeholder="${currentCurrency}">
          <button class="tag-del" data-id="${it.id}">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><path d="M18 6 6 18M6 6l12 12"/></svg>
          </button>
        `;
        c.appendChild(row);
      });
    }
    $('headerTotal').textContent = fmt(currentTotal());

    c.querySelectorAll('.tag-check').forEach(b=> b.addEventListener('click', ()=>{
      const it = items.find(i=>i.id===b.dataset.id);
      if(it){ it.bought = !it.bought; saveItems(); renderList(); }
    }));
    c.querySelectorAll('.count-input').forEach(inp=>{
      inp.addEventListener('change', ()=>{
        const it = items.find(i=>i.id===inp.dataset.id);
        if(it){
          let n = parseInt((inp.value||'1').replace(/[^0-9]/g,''), 10);
          if(!n || n < 1) n = 1;
          it.count = n;
          saveItems(); renderList();
        }
      });
      inp.addEventListener('focus', ()=> inp.select());
    });
    c.querySelectorAll('.tag-del').forEach(b=> b.addEventListener('click', ()=>{
      items = items.filter(i=>i.id!==b.dataset.id);
      saveItems(); renderList();
    }));
    c.querySelectorAll('.tag-price').forEach(inp=>{
      inp.addEventListener('change', ()=>{
        const it = items.find(i=>i.id===inp.dataset.id);
        if(it){
          it.price = parseFloat((inp.value||'0').replace(/[^0-9.]/g,'')) || 0;
          saveItems(); renderList();
        }
      });
    });
  }

  function escapeHtml(s){
    const d = document.createElement('div');
    d.textContent = s;
    return d.innerHTML;
  }

  function addItem(name, price){
    name = (name||'').trim();
    if(!name) return;
    items.push({ id: 'i'+Date.now(), name: name, price: price || 0, bought:false, count: 1 });
  }

  function computeFrequentItems(){
    const map = {};
    archive.forEach(e=> (e.items||[]).forEach(it=>{
      const key = (it.name||'').trim().toLowerCase();
      if(!key) return;
      const qty = it.qty || 1;
      const unit = qty > 0 ? (it.price||0) / qty : (it.price||0);
      if(!map[key]) map[key] = { name: it.name, qty: 0, unitPrice: 0 };
      map[key].qty += qty;
      map[key].unitPrice = unit;
    }));
    return Object.values(map).sort((a,b)=> b.qty - a.qty).slice(0,5);
  }

  function renderQuickAdd(){
    const freq = computeFrequentItems();
    const row = $('quickAddRow');
    const wrap = $('quickAddWrap');
    if(freq.length === 0){
      row.style.display = 'none';
      wrap.style.display = 'none';
      wrap.innerHTML = '';
      return;
    }
    row.style.display = 'flex';
    wrap.style.display = 'flex';
    wrap.innerHTML = freq.map(f=> `
      <button class="quick-chip" data-name="${escapeHtml(f.name)}" data-price="${Math.round(f.unitPrice)}">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg>
        ${escapeHtml(f.name)}
      </button>`).join('');
    wrap.querySelectorAll('.quick-chip').forEach(b=> b.addEventListener('click', ()=>{
      const name = b.dataset.name;
      const price = parseFloat(b.dataset.price) || 0;
      const existing = items.find(i=> i.name.trim().toLowerCase() === name.trim().toLowerCase());
      if(existing){ existing.count = (existing.count || 1) + 1; } 
      else { items.push({ id: 'i'+Date.now(), name: name, price: price, bought:false, count: 1 }); }
      saveItems(); renderList(); showToast(name);
    }));
  }

  $('itemNameInput').addEventListener('input', function(){
    this.value = this.value.replace(/[^A-Za-zА-Яа-яЁёІіӘәҒғҚқҢңӨөҰұҮүҺһ' -]/g, '');
  });
  $('itemPriceInput').addEventListener('input', function(){
    this.value = this.value.replace(/[^0-9]/g, '');
  });

  $('addBtn').addEventListener('click', ()=>{
    const name = $('itemNameInput').value;
    const price = parseFloat(($('itemPriceInput').value||'0').replace(/[^0-9.]/g,'')) || 0;
    if(!name.trim()) return;
    addItem(name, price);
    $('itemNameInput').value = '';
    $('itemPriceInput').value = '';
    $('itemNameInput').focus();
    saveItems(); renderList();
  });

  // Share
  function buildShareText(){
    let text = "🛒 *Тізім:*\n\n";
    items.forEach((it, idx) => {
      const check = it.bought ? "✅" : "🔲";
      const priceText = it.price ? ` - ${fmt(it.price * it.count)}` : '';
      const countText = it.count > 1 ? ` (${it.count})` : '';
      text += `${idx + 1}. ${check} ${it.name}${countText}${priceText}\n`;
    });
    text += `\n💰: ${fmt(currentTotal())}`;
    return text;
  }
  $('shareBtn').addEventListener('click', (e) => { e.stopPropagation(); $('shareMenu').classList.toggle('open'); });
  document.addEventListener('click', (e)=>{
    const menu = $('shareMenu');
    if(menu && menu.classList.contains('open') && !menu.contains(e.target) && e.target.id !== 'shareBtn'){ menu.classList.remove('open'); }
  });
  $('shareWaBtn').addEventListener('click', ()=>{ $('shareMenu').classList.remove('open'); window.open('https://wa.me/?text=' + encodeURIComponent(buildShareText()), '_blank'); });
  $('shareTgBtn').addEventListener('click', ()=>{ $('shareMenu').classList.remove('open'); window.open('https://t.me/share/url?url=&text=' + encodeURIComponent(buildShareText()), '_blank'); });
  $('shareCopyBtn').addEventListener('click', ()=>{
    $('shareMenu').classList.remove('open');
    const text = buildShareText();
    navigator.clipboard.writeText(text); showToast('📋');
  });

  // Budget
  function renderBudget(){
    $('budgetInput').value = budget ? budget : '';
    const total = currentTotal();
    $('gaugeNum').textContent = fmt(total);
    
    const pct = budget > 0 ? Math.min(100, (total/budget)*100) : (total>0 ? 100 : 0);
    const fill = $('gaugeFill');
    fill.style.width = pct + '%';
    fill.classList.toggle('over', budget>0 && total > budget);

    $('gaugeLeftLabel').textContent = fmt(total);
    if(budget > 0){
      const remain = budget - total;
      $('gaugeRightLabel').textContent = fmt(Math.abs(remain));
    } else {
      $('gaugeRightLabel').textContent = '...';
    }

    const top = [...items].filter(i=>i.price>0).sort((a,b)=> (b.price * b.count) - (a.price * a.count)).slice(0,5);
    const card = $('topSpendCard');
    if(top.length === 0){
      card.innerHTML = `<div class="empty-stats"><p>...</p></div>`;
    } else {
      card.innerHTML = top.map((it,idx)=> `
        <div class="stat-row">
          <div class="name">${idx+1}. ${escapeHtml(it.name)} ${it.count > 1 ? `×${it.count}` : ''}</div>
          <div class="val">${fmt(it.price * it.count)}</div>
        </div>`).join('');
    }
  }

  $('budgetInput').addEventListener('change', ()=>{
    budget = parseFloat(($('budgetInput').value||'0').replace(/[^0-9.]/g,'')) || 0;
    saveBudget(); renderBudget();
  });

  $('checkoutBtn').addEventListener('click', async ()=>{
    if(items.length === 0) return;
    const total = currentTotal();
    archive.push({ date: new Date().toISOString(), total: total, items: items.map(i=>({name: i.name, price: i.price * i.count, qty: i.count})) });
    await saveArchive();
    items = [];
    await saveItems();
    renderList(); renderBudget(); renderQuickAdd();
    showToast(getI18n('saveAlert'));
  });

  // Stats
  function renderStats(){
    const totalAll = archive.reduce((s,e)=> s + (e.total||0), 0);
    const tripCount = archive.length;
    const avgCheck = tripCount > 0 ? totalAll / tripCount : 0;
    $('statTotalAll').textContent = fmt(totalAll);
    $('statTripCount').textContent = tripCount;
    $('statAvgCheck').textContent = fmt(avgCheck);

    const now = new Date();
    const buckets = [];
    for(let i=5;i>=0;i--){
      const d = new Date(now.getFullYear(), now.getMonth()-i, 1);
      buckets.push({ y:d.getFullYear(), m:d.getMonth(), total:0 });
    }
    archive.forEach(e=>{
      const d = new Date(e.date);
      const b = buckets.find(b=> b.y===d.getFullYear() && b.m===d.getMonth());
      if(b) b.total += e.total;
    });
    const maxTotal = Math.max(1, ...buckets.map(b=>b.total));
    $('monthBars').innerHTML = buckets.map(b=>{
      const h = Math.max(4, Math.round((b.total/maxTotal)*100));
      return `<div class="bar-col">
        <div class="bar-fill" style="height:${h}%"></div>
      </div>`;
    }).join('');

    const map = {};
    archive.forEach(e=> e.items.forEach(it=>{
      const key = it.name.trim().toLowerCase();
      if(!key) return;
      map[key] = map[key] || { name: it.name, total:0, count:0 };
      map[key].total += (it.price||0);
      map[key].count += (it.qty||1);
    }));
    const topAll = Object.values(map).sort((a,b)=> b.total - a.total).slice(0,6);
    const card = $('topAllCard');
    if(topAll.length === 0){
      card.innerHTML = `<div class="empty-stats"><p>...</p></div>`;
    } else {
      card.innerHTML = topAll.map((it,idx)=> `
        <div class="top-item">
          <div class="top-rank">${idx+1}</div>
          <div class="name">${escapeHtml(it.name)} <span style="color:var(--muted);font-weight:500;">×${it.count}</span></div>
          <div class="val">${fmt(it.total)}</div>
        </div>`).join('');
    }
  }

  // Transfer
  function renderTransfer(){
    $('transferTotal').textContent = fmt(currentTotal());
  }

  function launchBankApp(bank){
    if(items.length === 0) return;
    const total = currentTotal();
    try{ navigator.clipboard.writeText(String(Math.round(total))); }catch(e){}

    let appOpened = false;
    const onBlur = ()=>{ appOpened = true; };
    window.addEventListener('blur', onBlur);
    window.location.href = bank.link;

    setTimeout(()=>{
      window.removeEventListener('blur', onBlur);
      if(!appOpened){ window.open(bank.url, '_blank'); }
    }, 900);
  }

  $('transferContinueBtn').addEventListener('click', ()=>{
    launchBankApp(currentBank);
  });

  // ---------- Header settings ----------
  $('settingsBtn').addEventListener('click', ()=>{
    renderLockStatus();
    $('settings-modal').classList.add('open');
  });
  $('settingsBackBtn').addEventListener('click', ()=>{
    $('settings-modal').classList.remove('open');
  });
  $('clearListBtn').addEventListener('click', async ()=>{
    items = [];
    await saveItems();
    renderList(); renderBudget(); renderQuickAdd(); renderTransfer();
    showToast(getI18n('clearedAlert'));
  });
  $('clearAllBtn').addEventListener('click', ()=>{
    if(!confirm(getI18n('clearAllConfirm'))) return;
    try{
      localStorage.removeItem('sk-items');
      localStorage.removeItem('sk-budget');
      localStorage.removeItem('sk-archive');
      localStorage.removeItem('sk-country');
      localStorage.removeItem('sk-lock');
    }catch(e){}
    location.reload();
  });
  $('exitBtn').addEventListener('click', ()=>{
    $('exit-modal').style.display = 'flex';
  });

  // ================= App Lock (PIN / Pattern / Alpha) =================
  function fallbackHash(str){
    let h = 5381;
    for(let i=0; i<str.length; i++){ h = ((h*33) ^ str.charCodeAt(i)) >>> 0; }
    return 'fb' + h.toString(16);
  }
  async function sha256Hex(str){
    // crypto.subtle only works in secure contexts (https:// or localhost).
    // On plain file:// (local testing) we fall back to a weaker hash so the feature still works.
    if(window.crypto && crypto.subtle && crypto.subtle.digest){
      try{
        const enc = new TextEncoder().encode(str);
        const buf = await crypto.subtle.digest('SHA-256', enc);
        return Array.from(new Uint8Array(buf)).map(b=> b.toString(16).padStart(2,'0')).join('');
      }catch(e){ return fallbackHash(str); }
    }
    return fallbackHash(str);
  }
  function loadLockConfig(){
    try{ const r = localStorage.getItem('sk-lock'); return r ? JSON.parse(r) : { enabled:false, type:null, hash:null }; }
    catch(e){ return { enabled:false, type:null, hash:null }; }
  }
  function saveLockConfig(cfg){
    try{ localStorage.setItem('sk-lock', JSON.stringify(cfg)); }catch(e){}
  }
  let lockConfig = loadLockConfig();

  function renderLockStatus(){
    const badge = $('lockStatusBadge');
    const chooser = $('lockTypeChooser');
    const manageRow = $('lockManageRow');
    if(lockConfig.enabled){
      const names = { pin:'PIN', pattern:'Өрнек', alpha:'Әріп+сан' };
      badge.textContent = names[lockConfig.type] + ' қосулы';
      badge.classList.remove('off'); badge.classList.add('on');
      chooser.style.display = 'none';
      manageRow.style.display = 'block';
    } else {
      badge.textContent = 'Өшірулі';
      badge.classList.remove('on'); badge.classList.add('off');
      chooser.style.display = 'flex';
      manageRow.style.display = 'none';
    }
  }

  document.querySelectorAll('#lockTypeChooser .lock-type-btn').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      openLockSetup(btn.dataset.type, 'create');
    });
  });
  $('lockChangeBtn').addEventListener('click', ()=>{
    openLockSetup(lockConfig.type, 'create');
  });
  $('lockDisableBtn').addEventListener('click', ()=>{
    openLockVerify(lockConfig.type, (ok)=>{
      if(ok){
        lockConfig = { enabled:false, type:null, hash:null };
        saveLockConfig(lockConfig);
        $('lock-setup-modal').classList.remove('open');
        renderLockStatus();
        showToast('Құлып өшірілді');
      }
    }, 'Ағымдағы құлыпты енгізіңіз');
  });
  $('lockSetupBackBtn').addEventListener('click', ()=>{
    $('lock-setup-modal').classList.remove('open');
  });

  // ---- Lock setup (create/confirm flow) ----
  function openLockSetup(type, mode){
    let firstEntry = null;
    $('lock-setup-modal').classList.add('open');
    renderLockEntry($('lockSetupBody'), type, {
      title: 'Жаңа құпияны енгізіңіз',
      sub: '',
      onComplete: (value)=>{
        if(firstEntry === null){
          firstEntry = value;
          renderLockEntry($('lockSetupBody'), type, {
            title: 'Қайталап енгізіңіз',
            sub: 'Растау үшін тағы бір рет енгізіңіз',
            onComplete: (value2)=>{
              if(value2 === firstEntry){
                sha256Hex(type+':'+value2).then(h=>{
                  lockConfig = { enabled:true, type: type, hash: h };
                  saveLockConfig(lockConfig);
                  $('lock-setup-modal').classList.remove('open');
                  renderLockStatus();
                  showToast('Құлып сақталды');
                });
              } else {
                showToast('Сәйкес келмеді, қайта көріңіз');
                firstEntry = null;
                openLockSetup(type, mode);
              }
            }
          });
        }
      }
    });
  }

  // ---- Lock verify (used to unlock app + to confirm before disabling) ----
  function openLockVerify(type, callback, subText){
    $('lock-setup-modal').classList.add('open');
    renderLockEntry($('lockSetupBody'), type, {
      title: 'Құпияны енгізіңіз',
      sub: subText || '',
      onComplete: (value)=>{
        sha256Hex(type+':'+value).then(h=>{
          const ok = h === lockConfig.hash;
          callback(ok);
          if(!ok){ showToast('Қате, қайта көріңіз'); openLockVerify(type, callback, subText); }
        });
      }
    });
  }

  // ---- Renders the correct input UI (pin / pattern / alpha) into a container ----
  function renderLockEntry(container, type, opts){
    container.innerHTML = '';
    const wrap = document.createElement('div');
    wrap.className = 'lock-entry-wrap';
    const title = document.createElement('div');
    title.className = 'lock-entry-title';
    title.textContent = opts.title;
    wrap.appendChild(title);
    if(opts.sub){
      const sub = document.createElement('div');
      sub.className = 'lock-entry-sub';
      sub.textContent = opts.sub;
      wrap.appendChild(sub);
    }
    container.appendChild(wrap);

    if(type === 'pin'){
      buildPinEntry(wrap, opts.onComplete);
    } else if(type === 'pattern'){
      buildPatternEntry(wrap, opts.onComplete);
    } else {
      buildAlphaEntry(wrap, opts.onComplete);
    }
  }

  function buildPinEntry(wrap, onComplete){
    const PIN_LEN = 4;
    let val = '';
    const dotsWrap = document.createElement('div');
    dotsWrap.className = 'pin-dots';
    for(let i=0;i<PIN_LEN;i++){
      const d = document.createElement('div'); d.className='pin-dot'; dotsWrap.appendChild(d);
    }
    wrap.appendChild(dotsWrap);
    const errEl = document.createElement('div');
    errEl.className = 'lock-entry-error';
    const pad = document.createElement('div');
    pad.className = 'pin-pad';
    const keys = ['1','2','3','4','5','6','7','8','9','','0','del'];
    keys.forEach(k=>{
      const b = document.createElement('button');
      b.type='button';
      if(k===''){ b.className='pin-key pin-empty'; }
      else if(k==='del'){
        b.className='pin-key pin-del';
        b.innerHTML = '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 4H8l-7 8 7 8h13a2 2 0 0 0 2-2V6a2 2 0 0 0-2-2Z"/><path d="M18 9l-6 6M12 9l6 6"/></svg>';
        b.addEventListener('click', ()=>{ val = val.slice(0,-1); updateDots(); });
      } else {
        b.className='pin-key'; b.textContent = k;
        b.addEventListener('click', ()=>{
          if(val.length>=PIN_LEN) return;
          val += k; updateDots();
          if(val.length===PIN_LEN){ setTimeout(()=> onComplete(val), 150); }
        });
      }
      pad.appendChild(b);
    });
    function updateDots(){
      dotsWrap.querySelectorAll('.pin-dot').forEach((d,i)=> d.classList.toggle('filled', i<val.length));
    }
    wrap.appendChild(pad);
    wrap.appendChild(errEl);
  }

  function buildPatternEntry(wrap, onComplete){
    const gridWrap = document.createElement('div');
    gridWrap.className = 'pattern-grid-wrap';
    const grid = document.createElement('div');
    grid.className = 'pattern-grid';
    const dots = [];
    for(let i=0;i<9;i++){
      const cell = document.createElement('div'); cell.className='pattern-dot-cell';
      const dot = document.createElement('div'); dot.className='pattern-dot'; dot.dataset.idx = i;
      cell.appendChild(dot); grid.appendChild(cell); dots.push(dot);
    }
    const svg = document.createElementNS('http://www.w3.org/2000/svg','svg');
    svg.setAttribute('class','pattern-svg');
    gridWrap.appendChild(grid);
    gridWrap.appendChild(svg);
    wrap.appendChild(gridWrap);
    const errEl = document.createElement('div');
    errEl.className = 'lock-entry-error';
    errEl.textContent = 'Кемінде 4 нүктені қосыңыз';
    wrap.appendChild(errEl);

    let path = [];
    let drawing = false;

    function centerOf(idx){
      const r = dots[idx].getBoundingClientRect();
      const gr = gridWrap.getBoundingClientRect();
      return { x: r.left + r.width/2 - gr.left, y: r.top + r.height/2 - gr.top };
    }
    function redrawLines(){
      svg.innerHTML = '';
      for(let i=1;i<path.length;i++){
        const a = centerOf(path[i-1]), b = centerOf(path[i]);
        const line = document.createElementNS('http://www.w3.org/2000/svg','line');
        line.setAttribute('x1',a.x); line.setAttribute('y1',a.y);
        line.setAttribute('x2',b.x); line.setAttribute('y2',b.y);
        svg.appendChild(line);
      }
    }
    function dotAtPoint(x,y){
      for(let i=0;i<dots.length;i++){
        const r = dots[i].getBoundingClientRect();
        const cx = r.left + r.width/2, cy = r.top + r.height/2;
        if(Math.hypot(x-cx, y-cy) < 24) return i;
      }
      return -1;
    }
    function addDot(idx){
      if(idx<0 || path.includes(idx)) return;
      path.push(idx);
      dots[idx].classList.add('active');
      redrawLines();
    }
    function reset(){
      path = [];
      dots.forEach(d=> d.classList.remove('active'));
      svg.innerHTML = '';
    }
    function pointFromEvent(e){
      if(e.touches && e.touches[0]) return { x:e.touches[0].clientX, y:e.touches[0].clientY };
      return { x:e.clientX, y:e.clientY };
    }
    function start(e){
      drawing = true; reset();
      const p = pointFromEvent(e);
      addDot(dotAtPoint(p.x,p.y));
    }
    function move(e){
      if(!drawing) return;
      e.preventDefault();
      const p = pointFromEvent(e);
      addDot(dotAtPoint(p.x,p.y));
    }
    function end(){
      if(!drawing) return;
      drawing = false;
      if(path.length >= 4){
        onComplete(path.join('-'));
      } else {
        errEl.classList.add('shake');
        setTimeout(()=> errEl.classList.remove('shake'), 400);
        setTimeout(reset, 300);
      }
    }
    gridWrap.addEventListener('mousedown', start);
    gridWrap.addEventListener('mousemove', move);
    window.addEventListener('mouseup', end);
    gridWrap.addEventListener('touchstart', start, {passive:true});
    gridWrap.addEventListener('touchmove', move, {passive:false});
    gridWrap.addEventListener('touchend', end);
  }

  function buildAlphaEntry(wrap, onComplete){
    const inputWrap = document.createElement('div');
    inputWrap.className = 'alpha-input-wrap';
    const input = document.createElement('input');
    input.type = 'password';
    input.className = 'alpha-input';
    input.placeholder = 'Құпия сөз (әріп + сан)';
    input.autocomplete = 'off';
    const btn = document.createElement('button');
    btn.type='button'; btn.className='alpha-submit-btn'; btn.textContent = 'Растау';
    inputWrap.appendChild(input); inputWrap.appendChild(btn);
    wrap.appendChild(inputWrap);
    const errEl = document.createElement('div');
    errEl.className = 'lock-entry-error';
    wrap.appendChild(errEl);
    function submit(){
      const v = input.value.trim();
      if(v.length < 4){
        errEl.textContent = 'Кемінде 4 таңба керек';
        errEl.parentElement.classList.add('shake');
        setTimeout(()=> errEl.parentElement.classList.remove('shake'), 400);
        return;
      }
      onComplete(v);
    }
    btn.addEventListener('click', submit);
    input.addEventListener('keydown', (e)=>{ if(e.key==='Enter') submit(); });
    setTimeout(()=> input.focus(), 200);
  }

  // ---- App startup lock screen ----
  function showAppLockScreen(onUnlocked){
    const body = $('lockScreenBody');
    body.innerHTML = '';
    renderLockEntry(body, lockConfig.type, {
      title: 'Қосымша құлыпталған',
      sub: 'Кіру үшін құпияны енгізіңіз',
      onComplete: (value)=>{
        sha256Hex(lockConfig.type+':'+value).then(h=>{
          const ok = h === lockConfig.hash;
          if(ok){
            $('lock-screen').classList.remove('open');
            onUnlocked();
          } else {
            showToast('Қате код');
            showAppLockScreen(onUnlocked);
          }
        });
      }
    });
    const forgotBtn = document.createElement('button');
    forgotBtn.type = 'button';
    forgotBtn.className = 'lock-forgot-link';
    forgotBtn.textContent = 'Құпияны ұмыттыңыз ба? Шығу';
    forgotBtn.addEventListener('click', ()=>{
      if(!confirm('Барлық деректер (тізім, бюджет, тарих, құлып) өшеді және бастапқы бетке ораласыз. Жалғастыру керек пе?')) return;
      try{
        localStorage.removeItem('sk-items');
        localStorage.removeItem('sk-budget');
        localStorage.removeItem('sk-archive');
        localStorage.removeItem('sk-country');
        localStorage.removeItem('sk-lock');
      }catch(e){}
      location.reload();
    });
    body.appendChild(forgotBtn);
    $('lock-screen').classList.add('open');
  }
  $('exitCancelBtn').addEventListener('click', ()=>{
    $('exit-modal').style.display = 'none';
  });
  $('exitSaveBtn').addEventListener('click', ()=>{
    location.reload();
  });
  $('exitDeleteBtn').addEventListener('click', ()=>{
    try{
      localStorage.removeItem('sk-items');
      localStorage.removeItem('sk-budget');
      localStorage.removeItem('sk-archive');
      localStorage.removeItem('sk-country');
      localStorage.removeItem('sk-lock');
    }catch(e){}
    location.reload();
  });

  if ('serviceWorker' in navigator) {
    window.addEventListener('load', () => {
      navigator.serviceWorker.register('sw.js').catch(()=>{});
    });
  }

  // Init
  (async function init(){
    await loadAll();
    setupConverter();
    refreshFxRates();
    renderBankChip();
    renderBankPicker();
    renderList();
    renderBudget();
    renderStats();
    renderQuickAdd();
    renderTransfer();
    updateConvUI();
  })();

})();
</script>
</body>
</html>html…]()
