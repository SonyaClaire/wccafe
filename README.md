[cosmic-whispers.html](https://github.com/user-attachments/files/25821214/cosmic-whispers.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="theme-color" content="#0a0412">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Cosmic Whispers">
<title>Cosmic Whispers</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700&family=Crimson+Pro:ital,wght@0,300;0,400;1,300;1,400&family=Raleway:wght@300;400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/astronomy-engine/2.1.19/astronomy.browser.min.js"></script>
<style>
:root {
  --ink: #0a0412;
  --deep: #120820;
  --void: #1a0f2e;
  --veil: #241540;
  --mist: #2e1a52;
  --dust: #8b6bb1;
  --silver: #c4a8e8;
  --moon: #e8daf5;
  --star: #f5f0ff;
  --gold: #d4a843;
  --ember: #c4621a;
  --rose: #c4507a;
  --teal: #3dbcb8;
  --sage: #7ab87a;
  --radius: 16px;
  --glow: 0 0 30px rgba(196,168,232,0.15);
}

* { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }

body {
  background: var(--ink);
  color: var(--moon);
  font-family: 'Crimson Pro', Georgia, serif;
  font-size: 17px;
  min-height: 100vh;
  overflow-x: hidden;
}

/* STARFIELD */
#starfield {
  position: fixed; inset: 0; z-index: 0; pointer-events: none;
  background: radial-gradient(ellipse at 20% 20%, #1a0f3a 0%, #0a0412 60%);
  overflow: hidden;
}
.star {
  position: absolute; background: white; border-radius: 50%;
  animation: twinkle var(--dur, 3s) var(--delay, 0s) infinite ease-in-out;
}
@keyframes twinkle {
  0%,100% { opacity: var(--lo, 0.2); transform: scale(1); }
  50% { opacity: var(--hi, 0.9); transform: scale(1.3); }
}

/* NEBULA SWIRLS */
.nebula {
  position: fixed; border-radius: 50%; filter: blur(80px);
  pointer-events: none; z-index: 0; animation: drift 20s ease-in-out infinite alternate;
}
.nebula-1 { width:400px; height:300px; background:rgba(100,40,180,0.12); top:-50px; right:-100px; }
.nebula-2 { width:350px; height:350px; background:rgba(60,100,200,0.08); bottom:100px; left:-80px; animation-delay:-10s; }
.nebula-3 { width:250px; height:200px; background:rgba(180,60,120,0.07); top:40%; right:20%; animation-delay:-5s; }
@keyframes drift { 0% { transform:translate(0,0) rotate(0deg); } 100% { transform:translate(30px,20px) rotate(15deg); } }

/* LAYOUT */
#app { position:relative; z-index:1; min-height:100vh; padding-bottom:80px; }

/* TOP BAR */
#topbar {
  position: sticky; top: 0; z-index: 100;
  background: rgba(10,4,18,0.85); backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(196,168,232,0.1);
  padding: 12px 20px;
  display: flex; align-items: center; justify-content: space-between;
}
.app-title {
  font-family: 'Cinzel Decorative', serif;
  font-size: 16px; color: var(--silver);
  letter-spacing: 2px; text-shadow: 0 0 20px rgba(196,168,232,0.5);
}
.refresh-info {
  font-family: 'Raleway', sans-serif;
  font-size: 11px; color: var(--dust);
  text-align: right; line-height: 1.4;
}
.refresh-dot {
  display: inline-block; width:7px; height:7px;
  background: var(--teal); border-radius: 50%;
  margin-right: 5px; animation: pulse 2s infinite;
}
@keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:0.5;transform:scale(0.8)} }

/* NAV */
#nav {
  position: fixed; bottom: 0; left: 0; right: 0; z-index: 100;
  background: rgba(10,4,18,0.95); backdrop-filter: blur(20px);
  border-top: 1px solid rgba(196,168,232,0.1);
  display: flex; align-items: center; justify-content: space-around;
  padding: 8px 0 max(8px, env(safe-area-inset-bottom));
}
.nav-btn {
  background: none; border: none; cursor: pointer;
  display: flex; flex-direction: column; align-items: center; gap: 3px;
  padding: 6px 10px; border-radius: 12px;
  transition: all 0.2s; color: var(--dust);
  font-family: 'Raleway', sans-serif; font-size: 10px; letter-spacing: 0.5px;
  min-width: 52px;
}
.nav-btn.active { color: var(--silver); }
.nav-btn.active .nav-icon { filter: drop-shadow(0 0 6px rgba(196,168,232,0.6)); }
.nav-icon { font-size: 20px; transition: transform 0.2s; }
.nav-btn:active .nav-icon { transform: scale(0.85); }

/* PAGES */
.page { display:none; padding: 20px; max-width: 600px; margin: 0 auto; }
.page.active { display:block; animation: fadeIn 0.3s ease; }
@keyframes fadeIn { from{opacity:0;transform:translateY(8px)} to{opacity:1;transform:translateY(0)} }

/* SECTION CARDS */
.card {
  background: rgba(26,15,46,0.7);
  border: 1px solid rgba(196,168,232,0.12);
  border-radius: var(--radius);
  padding: 20px;
  margin-bottom: 16px;
  backdrop-filter: blur(10px);
  box-shadow: var(--glow);
}
.card-title {
  font-family: 'Cinzel Decorative', serif;
  font-size: 12px; letter-spacing: 3px;
  color: var(--dust); text-transform: uppercase;
  margin-bottom: 16px; display: flex; align-items: center; gap: 8px;
}
.card-title::after {
  content:''; flex:1; height:1px;
  background: linear-gradient(to right, rgba(196,168,232,0.2), transparent);
}

/* PLANET GRID */
.planet-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.planet-item {
  background: rgba(36,21,64,0.6);
  border: 1px solid rgba(196,168,232,0.08);
  border-radius: 12px; padding: 12px;
  display: flex; align-items: center; gap: 10px;
  transition: border-color 0.2s;
}
.planet-item:active { border-color: rgba(196,168,232,0.3); }
.planet-glyph { font-size: 24px; flex-shrink: 0; }
.planet-info { flex:1; min-width:0; }
.planet-name {
  font-family: 'Raleway', sans-serif; font-size: 11px;
  color: var(--dust); letter-spacing: 1px; text-transform: uppercase;
}
.planet-sign { font-size: 15px; color: var(--moon); font-weight: 300; }
.planet-deg { font-size: 12px; color: var(--dust); }
.planet-retro { font-size: 10px; color: var(--ember); letter-spacing: 1px; }

/* MOON CARD */
.moon-display { text-align: center; padding: 10px 0; }
.moon-phase-icon { font-size: 64px; line-height:1; margin-bottom: 8px; filter: drop-shadow(0 0 15px rgba(228,218,245,0.4)); }
.moon-phase-name { font-family:'Cinzel Decorative',serif; font-size:14px; color:var(--silver); margin-bottom:4px; }
.moon-illumination { font-size:13px; color:var(--dust); margin-bottom:16px; }
.moon-times { display:flex; justify-content:center; gap:30px; }
.moon-time { text-align:center; }
.moon-time-label { font-family:'Raleway',sans-serif; font-size:10px; color:var(--dust); letter-spacing:1px; text-transform:uppercase; }
.moon-time-val { font-size:18px; color:var(--moon); }

/* SABBAT / WHEEL */
.sabbat-grid { display:grid; grid-template-columns:1fr 1fr; gap:10px; }
.sabbat-card {
  background: rgba(36,21,64,0.6);
  border: 1px solid rgba(196,168,232,0.08);
  border-radius: 12px; padding: 14px;
  cursor: pointer; transition: all 0.2s;
  position: relative; overflow: hidden;
}
.sabbat-card.next-sabbat { border-color: rgba(212,168,67,0.4); background: rgba(50,35,20,0.6); }
.sabbat-card.next-sabbat::before {
  content:'NEXT'; position:absolute; top:8px; right:8px;
  font-family:'Raleway',sans-serif; font-size:9px; letter-spacing:1px;
  color:var(--gold); background:rgba(212,168,67,0.15); border-radius:4px; padding:2px 6px;
}
.sabbat-card:active { transform:scale(0.97); }
.sabbat-emoji { font-size:28px; margin-bottom:6px; }
.sabbat-name { font-family:'Cinzel Decorative',serif; font-size:11px; color:var(--silver); margin-bottom:3px; }
.sabbat-date { font-family:'Raleway',sans-serif; font-size:11px; color:var(--dust); }
.sabbat-days { font-size:12px; color:var(--gold); margin-top:4px; }

/* MODAL */
#modal-overlay {
  display:none; position:fixed; inset:0; z-index:200;
  background:rgba(5,2,12,0.85); backdrop-filter:blur(6px);
  align-items:flex-end; justify-content:center;
}
#modal-overlay.open { display:flex; animation:fadeIn 0.2s ease; }
#modal {
  background: var(--void);
  border: 1px solid rgba(196,168,232,0.15);
  border-radius: 24px 24px 0 0;
  padding: 24px 24px max(24px, env(safe-area-inset-bottom));
  width: 100%; max-width: 600px;
  max-height: 85vh; overflow-y: auto;
  animation: slideUp 0.3s ease;
}
@keyframes slideUp { from{transform:translateY(100%)} to{transform:translateY(0)} }
.modal-close {
  float:right; background:rgba(196,168,232,0.1); border:none;
  color:var(--dust); font-size:20px; border-radius:50%;
  width:32px; height:32px; cursor:pointer; line-height:32px; text-align:center;
}
.modal-title { font-family:'Cinzel Decorative',serif; font-size:16px; color:var(--silver); margin-bottom:4px; }
.modal-subtitle { font-size:13px; color:var(--dust); margin-bottom:20px; }
.modal-body { font-size:15px; color:var(--moon); line-height:1.8; }
.modal-section { margin-bottom:16px; }
.modal-section h4 { font-family:'Raleway',sans-serif; font-size:11px; letter-spacing:2px; color:var(--dust); text-transform:uppercase; margin-bottom:6px; }
.modal-section p { color:var(--moon); }
.tag-row { display:flex; flex-wrap:wrap; gap:6px; margin-top:6px; }
.tag {
  background:rgba(196,168,232,0.1); border:1px solid rgba(196,168,232,0.15);
  border-radius:20px; padding:4px 12px;
  font-family:'Raleway',sans-serif; font-size:12px; color:var(--silver);
}

/* RESEARCH PAGE */
.date-input-row { display:flex; gap:10px; margin-bottom:16px; flex-wrap:wrap; }
.field-group { flex:1; min-width:140px; }
.field-label { font-family:'Raleway',sans-serif; font-size:11px; color:var(--dust); letter-spacing:1px; text-transform:uppercase; margin-bottom:6px; display:block; }
.field-input {
  width:100%; background:rgba(36,21,64,0.8);
  border:1px solid rgba(196,168,232,0.15); border-radius:10px;
  color:var(--moon); font-family:'Crimson Pro',serif; font-size:16px;
  padding:10px 14px; outline:none;
  transition: border-color 0.2s;
}
.field-input:focus { border-color:rgba(196,168,232,0.4); }
.btn-primary {
  background: linear-gradient(135deg, rgba(100,50,180,0.4), rgba(60,90,200,0.3));
  border: 1px solid rgba(196,168,232,0.25);
  border-radius: 12px; color: var(--moon);
  font-family:'Raleway',sans-serif; font-size:13px; letter-spacing:2px;
  padding: 12px 24px; cursor:pointer; width:100%;
  transition: all 0.2s; text-transform:uppercase;
}
.btn-primary:active { transform:scale(0.97); }
.btn-copy {
  background: rgba(61,188,184,0.15);
  border: 1px solid rgba(61,188,184,0.3);
  border-radius: 10px; color: var(--teal);
  font-family:'Raleway',sans-serif; font-size:12px; letter-spacing:1px;
  padding: 10px 20px; cursor:pointer; width:100%;
  transition: all 0.2s; margin-top:12px; text-transform:uppercase;
}
.btn-copy:active { transform:scale(0.97); }
.research-result { margin-top:16px; }
.result-row { display:flex; justify-content:space-between; padding:8px 0; border-bottom:1px solid rgba(196,168,232,0.06); }
.result-label { color:var(--dust); font-size:14px; }
.result-val { color:var(--moon); font-size:14px; text-align:right; }

/* JOURNAL */
.journal-entry-form { margin-bottom:20px; }
textarea.field-input { min-height:120px; resize:vertical; }
.journal-entries { display:flex; flex-direction:column; gap:12px; }
.journal-entry {
  background:rgba(36,21,64,0.5);
  border:1px solid rgba(196,168,232,0.08);
  border-radius:12px; padding:16px;
}
.journal-entry-date { font-family:'Raleway',sans-serif; font-size:11px; color:var(--dust); margin-bottom:8px; }
.journal-entry-text { font-size:15px; color:var(--moon); line-height:1.7; }
.journal-entry-moon { font-size:12px; color:var(--silver); margin-top:8px; }

/* HOROSCOPE */
.sign-grid { display:grid; grid-template-columns:repeat(4,1fr); gap:8px; margin-bottom:16px; }
.sign-btn {
  background:rgba(36,21,64,0.6); border:1px solid rgba(196,168,232,0.08);
  border-radius:12px; padding:10px 6px; cursor:pointer;
  text-align:center; transition:all 0.2s; color:var(--moon);
  font-family:'Crimson Pro',serif;
}
.sign-btn.selected { border-color:rgba(196,168,232,0.4); background:rgba(60,40,100,0.6); }
.sign-btn:active { transform:scale(0.93); }
.sign-glyph { font-size:22px; display:block; margin-bottom:3px; }
.sign-name { font-size:11px; color:var(--dust); font-family:'Raleway',sans-serif; }
.reading-box {
  background:rgba(26,15,46,0.8);
  border:1px solid rgba(196,168,232,0.1);
  border-radius:12px; padding:16px;
  font-size:15px; color:var(--moon); line-height:1.8;
  min-height:80px;
}
.loading-text { color:var(--dust); font-style:italic; text-align:center; padding:20px; }

/* STATUS BADGE */
.status-badge {
  display:inline-flex; align-items:center; gap:6px;
  background:rgba(61,188,184,0.1); border:1px solid rgba(61,188,184,0.2);
  border-radius:20px; padding:4px 12px;
  font-family:'Raleway',sans-serif; font-size:11px; color:var(--teal); letter-spacing:1px;
}

/* HEMISPHERE TOGGLE */
.hemi-toggle {
  display:flex; background:rgba(36,21,64,0.6);
  border:1px solid rgba(196,168,232,0.1); border-radius:10px;
  overflow:hidden; margin-bottom:16px;
}
.hemi-btn {
  flex:1; background:none; border:none; cursor:pointer;
  padding:9px; font-family:'Raleway',sans-serif; font-size:12px;
  color:var(--dust); transition:all 0.2s; letter-spacing:1px;
}
.hemi-btn.active { background:rgba(196,168,232,0.12); color:var(--silver); }

/* TOAST */
#toast {
  position:fixed; bottom:100px; left:50%; transform:translateX(-50%) translateY(20px);
  background:rgba(61,188,184,0.9); color:#fff; border-radius:20px;
  padding:10px 24px; font-family:'Raleway',sans-serif; font-size:13px;
  z-index:300; opacity:0; transition:all 0.3s; pointer-events:none; white-space:nowrap;
}
#toast.show { opacity:1; transform:translateX(-50%) translateY(0); }

/* DIVIDER */
.divider { height:1px; background:linear-gradient(to right,transparent,rgba(196,168,232,0.15),transparent); margin:16px 0; }

/* ZODIAC SIGNS PAGE */
.zodiac-full-grid { display:grid; grid-template-columns:1fr 1fr; gap:10px; }
.zodiac-card {
  background:rgba(36,21,64,0.6); border:1px solid rgba(196,168,232,0.08);
  border-radius:12px; padding:14px; cursor:pointer; transition:all 0.2s;
}
.zodiac-card:active { transform:scale(0.96); border-color:rgba(196,168,232,0.3); }
.zodiac-glyph { font-size:28px; display:block; margin-bottom:6px; }
.zodiac-name { font-family:'Cinzel Decorative',serif; font-size:11px; color:var(--silver); margin-bottom:3px; }
.zodiac-dates { font-family:'Raleway',sans-serif; font-size:11px; color:var(--dust); }
.zodiac-element { font-size:11px; color:var(--gold); margin-top:4px; }

/* SCROLLBAR */
::-webkit-scrollbar { width:4px; }
::-webkit-scrollbar-track { background:transparent; }
::-webkit-scrollbar-thumb { background:rgba(196,168,232,0.2); border-radius:2px; }
</style>
</head>
<body>

<div id="starfield"></div>
<div class="nebula nebula-1"></div>
<div class="nebula nebula-2"></div>
<div class="nebula nebula-3"></div>

<div id="app">
  <!-- TOP BAR -->
  <div id="topbar">
    <div class="app-title">✦ Cosmic Whispers</div>
    <div class="refresh-info">
      <span class="refresh-dot"></span>
      <span id="refresh-label">Loading…</span><br>
      <span id="next-refresh-label" style="opacity:0.6"></span>
    </div>
  </div>

  <!-- PAGES -->
  <div id="page-dashboard" class="page active">
    <div class="card">
      <div class="card-title">🌙 Moon</div>
      <div class="moon-display">
        <div class="moon-phase-icon" id="moon-icon">🌑</div>
        <div class="moon-phase-name" id="moon-name">Loading…</div>
        <div class="moon-illumination" id="moon-illum"></div>
        <div class="moon-times">
          <div class="moon-time">
            <div class="moon-time-label">Moonrise</div>
            <div class="moon-time-val" id="moonrise">—</div>
          </div>
          <div class="moon-time">
            <div class="moon-time-label">Sign</div>
            <div class="moon-time-val" id="moon-sign-dash">—</div>
          </div>
          <div class="moon-time">
            <div class="moon-time-label">Moonset</div>
            <div class="moon-time-val" id="moonset">—</div>
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-title">☿ Planets</div>
      <div class="planet-grid" id="planet-grid">
        <div class="loading-text" style="grid-column:span 2">Calculating positions…</div>
      </div>
    </div>

    <div class="card">
      <div class="card-title">🔭 Next Sign Changes</div>
      <div id="sign-changes" style="font-size:14px;color:var(--dust);font-style:italic">Calculating…</div>
    </div>
  </div>

  <div id="page-wheel" class="page">
    <div class="card">
      <div class="card-title">☸ Wheel of the Year</div>
      <div class="hemi-toggle">
        <button class="hemi-btn active" id="hemi-n" onclick="setHemi('N')">🌿 Northern</button>
        <button class="hemi-btn" id="hemi-s" onclick="setHemi('S')">🌊 Southern</button>
      </div>
      <div class="sabbat-grid" id="sabbat-grid">
        <div class="loading-text" style="grid-column:span 2">Loading sabbats…</div>
      </div>
    </div>
  </div>

  <div id="page-horoscope" class="page">
    <div class="card">
      <div class="card-title">♈ Zodiac Signs</div>
      <div class="zodiac-full-grid" id="zodiac-grid"></div>
    </div>
  </div>

  <div id="page-research" class="page">
    <div class="card">
      <div class="card-title">🔭 Astro Research Chart</div>
      <div style="margin-bottom:12px">
        <span class="status-badge">⚗️ Cross-check with astro.com</span>
      </div>
      <div class="date-input-row">
        <div class="field-group">
          <label class="field-label">Date</label>
          <input type="date" class="field-input" id="research-date">
        </div>
        <div class="field-group">
          <label class="field-label">Time (optional)</label>
          <input type="time" class="field-input" id="research-time" value="12:00">
        </div>
      </div>
      <button class="btn-primary" onclick="runResearch()">✦ Cast Chart</button>
      <div id="research-result" class="research-result" style="display:none">
        <div class="divider"></div>
        <div id="research-rows"></div>
        <div class="divider"></div>
        <div id="research-reading" class="reading-box" style="margin-top:0"></div>
        <button class="btn-copy" onclick="copyResearch()">📋 Copy to Book of Shadows</button>
      </div>
    </div>
  </div>

  <div id="page-journal" class="page">
    <div class="card">
      <div class="card-title">📖 Book of Shadows</div>
      <div class="journal-entry-form">
        <div class="field-group" style="margin-bottom:10px">
          <label class="field-label">Title / Intention</label>
          <input type="text" class="field-input" id="journal-title" placeholder="Tonight's working…">
        </div>
        <div class="field-group" style="margin-bottom:10px">
          <label class="field-label">Entry</label>
          <textarea class="field-input" id="journal-text" placeholder="Write your observations, spells, dreams…"></textarea>
        </div>
        <button class="btn-primary" onclick="saveEntry()">✦ Save Entry</button>
      </div>
      <div class="divider"></div>
      <div class="journal-entries" id="journal-entries">
        <div style="color:var(--dust);font-style:italic;text-align:center;padding:20px">Your entries will appear here…</div>
      </div>
    </div>
  </div>
</div>

<!-- NAV -->
<nav id="nav">
  <button class="nav-btn active" onclick="showPage('dashboard',this)">
    <span class="nav-icon">🌌</span>Sky
  </button>
  <button class="nav-btn" onclick="showPage('wheel',this)">
    <span class="nav-icon">☸</span>Wheel
  </button>
  <button class="nav-btn" onclick="showPage('horoscope',this)">
    <span class="nav-icon">♈</span>Signs
  </button>
  <button class="nav-btn" onclick="showPage('research',this)">
    <span class="nav-icon">🔭</span>Research
  </button>
  <button class="nav-btn" onclick="showPage('journal',this)">
    <span class="nav-icon">📖</span>Shadows
  </button>
</nav>

<!-- MODAL -->
<div id="modal-overlay" onclick="closeModal(event)">
  <div id="modal">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <div id="modal-content"></div>
  </div>
</div>

<!-- TOAST -->
<div id="toast"></div>

<script>
// ─── STARFIELD ───────────────────────────────────────────────────────────────
(function(){
  const sf = document.getElementById('starfield');
  for(let i=0;i<180;i++){
    const s=document.createElement('div'); s.className='star';
    const sz=Math.random()*2.5+0.5;
    s.style.cssText=`
      width:${sz}px;height:${sz}px;
      left:${Math.random()*100}%;top:${Math.random()*100}%;
      --lo:${(Math.random()*0.3+0.05).toFixed(2)};
      --hi:${(Math.random()*0.6+0.4).toFixed(2)};
      --dur:${(Math.random()*4+2).toFixed(1)}s;
      --delay:-${(Math.random()*6).toFixed(1)}s;
    `;
    sf.appendChild(s);
  }
})();

// ─── DATA ─────────────────────────────────────────────────────────────────────
const PLANETS = [
  { name:'Sun',    glyph:'☉', body:'Sun'     },
  { name:'Moon',   glyph:'☽', body:'Moon'    },
  { name:'Mercury',glyph:'☿', body:'Mercury' },
  { name:'Venus',  glyph:'♀', body:'Venus'   },
  { name:'Mars',   glyph:'♂', body:'Mars'    },
  { name:'Jupiter',glyph:'♃', body:'Jupiter' },
  { name:'Saturn', glyph:'♄', body:'Saturn'  },
  { name:'Uranus', glyph:'⛢', body:'Uranus'  },
  { name:'Neptune',glyph:'♆', body:'Neptune' },
  { name:'Pluto',  glyph:'♇', body:'Pluto'   },
];

const SIGNS = [
  {name:'Aries',    glyph:'♈',start:0  },
  {name:'Taurus',   glyph:'♉',start:30 },
  {name:'Gemini',   glyph:'♊',start:60 },
  {name:'Cancer',   glyph:'♋',start:90 },
  {name:'Leo',      glyph:'♌',start:120},
  {name:'Virgo',    glyph:'♍',start:150},
  {name:'Libra',    glyph:'♎',start:180},
  {name:'Scorpio',  glyph:'♏',start:210},
  {name:'Sagittarius',glyph:'♐',start:240},
  {name:'Capricorn',glyph:'♑',start:270},
  {name:'Aquarius', glyph:'♒',start:300},
  {name:'Pisces',   glyph:'♓',start:330},
];

const ZODIAC_DATA = [
  {name:'Aries',    glyph:'♈',dates:'Mar 21–Apr 19',element:'🔥 Fire · Cardinal',   ruler:'Mars',    mod:'Cardinal',traits:'Bold, pioneering, energetic',body:'Head & face',   polarity:'Yang',description:'The first sign of the zodiac, Aries embodies the raw energy of new beginnings. Ruled by Mars, Aries souls are courageous, direct, and fiercely independent. They charge forward fearlessly, igniting inspiration wherever they go.',keywords:['Action','Courage','Initiative','Passion'],crystals:['Carnelian','Red Jasper','Bloodstone'],herbs:['Nettle','Ginger','Garlic'],colors:['Red','Orange','White'],deity:'Mars / Ares'},
  {name:'Taurus',   glyph:'♉',dates:'Apr 20–May 20',element:'🌍 Earth · Fixed',     ruler:'Venus',   mod:'Fixed',  traits:'Loyal, patient, sensual',   body:'Throat & neck', polarity:'Yin', description:'Taurus is the sign of enduring beauty and earthly pleasures. Ruled by Venus, Taurus souls are patient, devoted, and deeply connected to the material world. They build slowly but create things that last forever.',keywords:['Stability','Abundance','Sensuality','Loyalty'],crystals:['Rose Quartz','Emerald','Malachite'],herbs:['Thyme','Sage','Mint'],colors:['Green','Pink','Earth tones'],deity:'Venus / Aphrodite'},
  {name:'Gemini',   glyph:'♊',dates:'May 21–Jun 20',element:'💨 Air · Mutable',     ruler:'Mercury', mod:'Mutable',traits:'Curious, witty, adaptable', body:'Hands & lungs',  polarity:'Yang',description:'Gemini is the sign of the cosmic twins — duality, curiosity, and the eternal search for knowledge. Ruled by Mercury, Gemini souls are quick-minded, communicative, and endlessly fascinating.',keywords:['Curiosity','Communication','Duality','Wit'],crystals:['Citrine','Agate','Tiger Eye'],herbs:['Lavender','Dill','Fennel'],colors:['Yellow','Silver','Light blue'],deity:'Mercury / Hermes'},
  {name:'Cancer',   glyph:'♋',dates:'Jun 21–Jul 22',element:'💧 Water · Cardinal',  ruler:'Moon',    mod:'Cardinal',traits:'Nurturing, intuitive, protective',body:'Chest & stomach',polarity:'Yin',description:'Cancer is the sign of home, memory, and emotional depth. Ruled by the Moon, Cancer souls are fiercely protective, deeply intuitive, and gifted with emotional intelligence that borders on psychic.',keywords:['Nurturing','Intuition','Home','Emotions'],crystals:['Moonstone','Pearl','Selenite'],herbs:['Chamomile','Jasmine','Rose'],colors:['Silver','White','Sea green'],deity:'Selene / Diana'},
  {name:'Leo',      glyph:'♌',dates:'Jul 23–Aug 22',element:'🔥 Fire · Fixed',      ruler:'Sun',     mod:'Fixed',  traits:'Radiant, generous, dramatic',body:'Heart & spine',  polarity:'Yang',description:'Leo is the sign of the solar sovereign — radiant, generous, and born to shine. Ruled by the Sun itself, Leo souls carry an inner light that warms everyone around them. They lead with heart.',keywords:['Radiance','Creativity','Leadership','Joy'],crystals:['Sunstone','Citrine','Gold Tiger Eye'],herbs:['Sunflower','Bay Laurel','Marigold'],colors:['Gold','Orange','Royal purple'],deity:'Sol / Apollo'},
  {name:'Virgo',    glyph:'♍',dates:'Aug 23–Sep 22',element:'🌍 Earth · Mutable',   ruler:'Mercury', mod:'Mutable',traits:'Analytical, healing, precise',body:'Digestive system',polarity:'Yin',description:'Virgo is the sign of sacred service and the healer\'s art. Ruled by Mercury, Virgo souls are meticulous, analytical, and deeply devoted to making the world function with grace and precision.',keywords:['Service','Analysis','Healing','Purity'],crystals:['Moss Agate','Peridot','Amazonite'],herbs:['Echinacea','Valerian','Skullcap'],colors:['Green','Navy','Earth brown'],deity:'Demeter / Ceres'},
  {name:'Libra',    glyph:'♎',dates:'Sep 23–Oct 22',element:'💨 Air · Cardinal',    ruler:'Venus',   mod:'Cardinal',traits:'Harmonious, just, refined',  body:'Kidneys & lower back',polarity:'Yang',description:'Libra is the sign of balance, beauty, and sacred partnership. Ruled by Venus, Libra souls are gifted diplomats who weave harmony wherever there is discord. They seek the divine in human connection.',keywords:['Balance','Justice','Beauty','Partnership'],crystals:['Opal','Lapis Lazuli','Kunzite'],herbs:['Spearmint','Violet','Yarrow'],colors:['Pink','Ivory','Pale blue'],deity:'Themis / Astraea'},
  {name:'Scorpio',  glyph:'♏',dates:'Oct 23–Nov 21',element:'💧 Water · Fixed',     ruler:'Pluto',   mod:'Fixed',  traits:'Intense, perceptive, transformative',body:'Reproductive organs',polarity:'Yin',description:'Scorpio is the sign of death, rebirth, and the deepest mysteries. Co-ruled by Mars and Pluto, Scorpio souls dive into shadow without fear, transforming darkness into wisdom and power.',keywords:['Transformation','Mystery','Power','Depth'],crystals:['Obsidian','Black Tourmaline','Garnet'],herbs:['Wormwood','Mugwort','Myrrh'],colors:['Black','Deep red','Crimson'],deity:'Hekate / Persephone'},
  {name:'Sagittarius',glyph:'♐',dates:'Nov 22–Dec 21',element:'🔥 Fire · Mutable',  ruler:'Jupiter', mod:'Mutable',traits:'Adventurous, philosophical, free',body:'Hips & thighs', polarity:'Yang',description:'Sagittarius is the sign of the archer — always aiming at distant horizons. Ruled by Jupiter, Sagittarius souls are eternal seekers of truth, wisdom, and freedom. Philosophy and adventure are their sacred paths.',keywords:['Freedom','Philosophy','Adventure','Truth'],crystals:['Turquoise','Sodalite','Amethyst'],herbs:['Sage','Anise','Hyssop'],colors:['Purple','Royal blue','Gold'],deity:'Zeus / Jupiter'},
  {name:'Capricorn',glyph:'♑',dates:'Dec 22–Jan 19',element:'🌍 Earth · Cardinal',  ruler:'Saturn',  mod:'Cardinal',traits:'Ambitious, disciplined, wise',body:'Knees & bones',  polarity:'Yin', description:'Capricorn is the sign of the elder, the mountain-climber, and the keeper of time. Ruled by Saturn, Capricorn souls understand that true mastery is built slowly, with patience and discipline.',keywords:['Ambition','Discipline','Mastery','Legacy'],crystals:['Jet','Garnet','Black Onyx'],herbs:['Comfrey','Solomon\'s Seal','Bistort'],colors:['Black','Dark green','Charcoal'],deity:'Kronos / Saturn'},
  {name:'Aquarius', glyph:'♒',dates:'Jan 20–Feb 18',element:'💨 Air · Fixed',       ruler:'Uranus',  mod:'Fixed',  traits:'Visionary, humanitarian, unconventional',body:'Ankles & circulation',polarity:'Yang',description:'Aquarius is the sign of the water-bearer — paradoxically an air sign — carrying the waters of collective consciousness. Ruled by Uranus, Aquarius souls are visionaries, revolutionaries, and servants of humanity.',keywords:['Humanity','Innovation','Freedom','Vision'],crystals:['Aquamarine','Labradorite','Amethyst'],herbs:['Frankincense','Star Anise','Clove'],colors:['Electric blue','Silver','Violet'],deity:'Prometheus / Uranus'},
  {name:'Pisces',   glyph:'♓',dates:'Feb 19–Mar 20',element:'💧 Water · Mutable',   ruler:'Neptune', mod:'Mutable',traits:'Empathic, mystical, dreaming',body:'Feet & lymphatic',polarity:'Yin', description:'Pisces is the sign of dissolution, dreams, and divine mystery. Ruled by Neptune, Pisces souls move between worlds with ease — empaths, mystics, and artists who feel the unity beneath all apparent separation.',keywords:['Compassion','Dreams','Mysticism','Surrender'],crystals:['Amethyst','Aquamarine','Fluorite'],herbs:['Lotus','Mugwort','Blue Lotus'],colors:['Sea green','Lavender','White'],deity:'Poseidon / Neptune'},
];

const SABBATS_N = [
  {name:'Yule',        emoji:'🌑',date:'Dec 21',doy:355,desc:'The Winter Solstice — the longest night of the year. The Sun King is reborn from the Goddess, and we celebrate the return of the light.',traditions:['Wassailing','Yule log burning','Mistletoe & holly decoration','Gift giving','Caroling'],magic:'Rebirth, new beginnings, light returning, inner reflection',herbs:['Holly','Mistletoe','Pine','Frankincense','Cinnamon'],crystals:['Clear Quartz','Ruby','Garnet'],colors:['Red','Green','Gold','White'],deities:['The Oak King','Sun God','Great Mother']},
  {name:'Imbolc',      emoji:'🕯️',date:'Feb 2', doy:33, desc:'The first stirring of spring. Sacred to Brigid — goddess of fire, healing, and poetry. Candles are lit to honour the lengthening days.',traditions:['Brigid cross weaving','Candle lighting','Snow scrying','Seed blessing'],magic:'Purification, new beginnings, inspiration, healing',herbs:['Snowdrop','Rosemary','Basil','Angelica'],crystals:['Amethyst','Garnet','Moonstone'],colors:['White','Silver','Red'],deities:['Brigid','Cailleach']},
  {name:'Ostara',      emoji:'🌸',date:'Mar 21',doy:80, desc:'The Spring Equinox — perfect balance of day and night. The Goddess awakens and the Earth blooms. A time of fertility, renewal, and possibility.',traditions:['Egg decorating','Seed planting','Bonfires at dawn','Flower crowns'],magic:'Balance, fertility, growth, new beginnings',herbs:['Violet','Jasmine','Rose','Clover'],crystals:['Rose Quartz','Moss Agate','Amazonite'],colors:['Pastel pink','Yellow','Green','Lavender'],deities:['Ostara / Eostre','The Green Man']},
  {name:'Beltane',     emoji:'🔥',date:'May 1', doy:121,desc:'The great fire festival celebrating the height of spring. The union of the God and Goddess. Fire, fertility, and the wild dance of life.',traditions:['Maypole dancing','Jumping bonfires','Flower garlands','Handfasting'],magic:'Passion, fertility, creativity, union, abundance',herbs:['Hawthorn','Rose','Lilac','Elderflower'],crystals:['Garnet','Rose Quartz','Carnelian'],colors:['Red','White','Green','Gold'],deities:['Cernunnos','Flora','Bel']},
  {name:'Litha',       emoji:'☀️',date:'Jun 21',doy:172,desc:'The Summer Solstice — the longest day. The Sun King is at his peak power before beginning his descent. A time of fullness, magic, and gratitude.',traditions:['Midsummer bonfires','Herb gathering','Fairy offerings','Fire wheels'],magic:'Abundance, strength, power, love, protection',herbs:['St. John\'s Wort','Lavender','Chamomile','Mugwort'],crystals:['Citrine','Sunstone','Topaz'],colors:['Gold','Orange','Yellow','Red'],deities:['Sun God','Oak King & Holly King']},
  {name:'Lammas',      emoji:'🌾',date:'Aug 1', doy:213,desc:'Lammas / Lughnasadh — the first harvest. We give thanks for the grain and the first fruits. The God begins to wane; his energy enters the harvest.',traditions:['Bread baking','Corn dollies','Harvest offerings','Competitions'],magic:'Gratitude, abundance, sacrifice, transformation',herbs:['Wheat','Corn','Gorse','Sunflower'],crystals:['Peridot','Citrine','Gold Tiger Eye'],colors:['Gold','Yellow','Orange','Brown'],deities:['Lugh','Demeter']},
  {name:'Mabon',       emoji:'🍂',date:'Sep 21',doy:264,desc:'The Autumn Equinox — the second harvest and a time of balance. We give thanks and prepare for the dark half of the year.',traditions:['Harvest feasts','Apple gathering','Ancestor altars','Wine making'],magic:'Gratitude, balance, release, preparation',herbs:['Apple','Sage','Rosemary','Hops'],crystals:['Amber','Carnelian','Tiger Eye'],colors:['Orange','Red','Brown','Gold'],deities:['Persephone','Mabon ap Modron']},
  {name:'Samhain',     emoji:'🕸️',date:'Oct 31',doy:304,desc:'The most sacred sabbat — the Witches\' New Year. The veil between worlds is thinnest. We honour our ancestors and embrace the divine dark.',traditions:['Ancestor altars','Dumb supper','Divination','Jack-o-lanterns','Bone reading'],magic:'Divination, ancestral connection, release, endings',herbs:['Mugwort','Wormwood','Blackthorn','Deadly Nightshade'],crystals:['Obsidian','Black Tourmaline','Smoky Quartz'],colors:['Black','Orange','Deep purple'],deities:['Hekate','The Morrigan','Cernunnos','Anubis']},
];

const SABBAT_OFFSETS_S = { // Southern Hemisphere dates (6 months offset)
  'Yule':'Jun 21','Imbolc':'Aug 1','Ostara':'Sep 21','Beltane':'Nov 1',
  'Litha':'Dec 21','Lammas':'Feb 2','Mabon':'Mar 21','Samhain':'Apr 30',
};

// ─── STATE ───────────────────────────────────────────────────────────────────
let hemisphere = 'N';
let lastCalculated = null;
let cachedData = null;
let nextRefreshTime = null;
let journals = JSON.parse(localStorage.getItem('cw_journal') || '[]');

// ─── ASTRONOMY ───────────────────────────────────────────────────────────────
function getLongitude(body, date) {
  try {
    const ecl = Astronomy.SunPosition(date); // fallback
    if (body === 'Sun') return Astronomy.SunPosition(date).elon;
    const eq = Astronomy.Equator(body, date, null, false, true);
    const eclPos = Astronomy.Ecliptic(eq.vec);
    return ((eclPos.elon % 360) + 360) % 360;
  } catch(e) {
    return null;
  }
}

function getSunLongitude(date) {
  try { return Astronomy.SunPosition(date).elon; } catch(e) { return null; }
}

function getMoonLongitude(date) {
  try {
    const eq = Astronomy.Equator('Moon', date, null, false, true);
    const ecl = Astronomy.Ecliptic(eq.vec);
    return ((ecl.elon % 360) + 360) % 360;
  } catch(e) { return null; }
}

function getPlanetLongitude(body, date) {
  try {
    const eq = Astronomy.Equator(body, date, null, false, true);
    const ecl = Astronomy.Ecliptic(eq.vec);
    return ((ecl.elon % 360) + 360) % 360;
  } catch(e) { return null; }
}

function lonToSign(lon) {
  if (lon === null) return {name:'Unknown', glyph:'?', deg:0};
  const norm = ((lon % 360) + 360) % 360;
  const idx = Math.floor(norm / 30);
  const deg = norm - idx * 30;
  return { ...SIGNS[idx], deg: deg.toFixed(1) };
}

function getMoonPhase(date) {
  try {
    const angle = Astronomy.MoonPhase(date);
    const illumination = (1 - Math.cos(angle * Math.PI / 180)) / 2 * 100;
    let phase, icon;
    if (angle < 22.5)          { phase='New Moon';          icon='🌑'; }
    else if (angle < 67.5)     { phase='Waxing Crescent';   icon='🌒'; }
    else if (angle < 112.5)    { phase='First Quarter';     icon='🌓'; }
    else if (angle < 157.5)    { phase='Waxing Gibbous';    icon='🌔'; }
    else if (angle < 202.5)    { phase='Full Moon';         icon='🌕'; }
    else if (angle < 247.5)    { phase='Waning Gibbous';    icon='🌖'; }
    else if (angle < 292.5)    { phase='Last Quarter';      icon='🌗'; }
    else if (angle < 337.5)    { phase='Waning Crescent';   icon='🌘'; }
    else                        { phase='New Moon';          icon='🌑'; }
    return { phase, icon, illumination: illumination.toFixed(0) };
  } catch(e) { return { phase:'Unknown', icon:'🌙', illumination:0 }; }
}

function getMoonTimes(date, lat, lon) {
  try {
    const observer = new Astronomy.Observer(lat, lon, 0);
    const rise = Astronomy.SearchRiseSet('Moon', observer, +1, date, 1);
    const set  = Astronomy.SearchRiseSet('Moon', observer, -1, date, 1);
    const fmt = d => d ? new Date(d.date).toLocaleTimeString([],{hour:'2-digit',minute:'2-digit'}) : '—';
    return { rise: fmt(rise), set: fmt(set) };
  } catch(e) { return { rise:'—', set:'—' }; }
}

function isRetrograde(body, date) {
  try {
    if (body === 'Sun' || body === 'Moon') return false;
    const d1 = new Date(date.getTime() - 86400000);
    const d2 = new Date(date.getTime() + 86400000);
    const l1 = getPlanetLongitude(body, d1);
    const l2 = getPlanetLongitude(body, d2);
    if (l1 === null || l2 === null) return false;
    let diff = l2 - l1;
    if (diff > 180) diff -= 360;
    if (diff < -180) diff += 360;
    return diff < 0;
  } catch(e) { return false; }
}

// ─── REFRESH LOGIC ───────────────────────────────────────────────────────────
function shouldRefresh() {
  if (!lastCalculated) return true;
  const now = Date.now();
  const fourHours = 4 * 60 * 60 * 1000;
  if (now - lastCalculated > fourHours) return true;
  // Check if any planet has changed sign
  if (cachedData) {
    const current = calcPlanetSigns(new Date());
    for (const p of PLANETS) {
      const old = cachedData.signs[p.name];
      const cur = current[p.name];
      if (old && cur && old.name !== cur.name) return true;
    }
  }
  return false;
}

function calcPlanetSigns(date) {
  const signs = {};
  for (const p of PLANETS) {
    let lon;
    if (p.body === 'Sun')  lon = getSunLongitude(date);
    else if (p.body === 'Moon') lon = getMoonLongitude(date);
    else lon = getPlanetLongitude(p.body, date);
    signs[p.name] = lonToSign(lon);
    signs[p.name].retro = isRetrograde(p.body, date);
  }
  return signs;
}

function computeData(date, lat, lon) {
  const signs = calcPlanetSigns(date);
  const moon  = getMoonPhase(date);
  const moonTimes = (lat && lon) ? getMoonTimes(date, lat, lon) : { rise:'Enable location', set:'for live times' };
  return { signs, moon, moonTimes };
}

// ─── RENDER ──────────────────────────────────────────────────────────────────
function renderDashboard(data) {
  // Moon
  document.getElementById('moon-icon').textContent  = data.moon.icon;
  document.getElementById('moon-name').textContent  = data.moon.phase;
  document.getElementById('moon-illum').textContent = `${data.moon.illumination}% illuminated`;
  document.getElementById('moonrise').textContent   = data.moonTimes.rise;
  document.getElementById('moonset').textContent    = data.moonTimes.set;
  document.getElementById('moon-sign-dash').textContent = data.signs['Moon']?.glyph + ' ' + data.signs['Moon']?.name || '—';

  // Planets (exclude Moon from grid since it's in moon card)
  const grid = document.getElementById('planet-grid');
  grid.innerHTML = '';
  for (const p of PLANETS) {
    if (p.name === 'Moon') continue;
    const s = data.signs[p.name];
    if (!s) continue;
    const el = document.createElement('div');
    el.className = 'planet-item';
    el.innerHTML = `
      <div class="planet-glyph">${p.glyph}</div>
      <div class="planet-info">
        <div class="planet-name">${p.name}</div>
        <div class="planet-sign">${s.glyph} ${s.name}</div>
        <div class="planet-deg">${s.deg}°${s.retro ? ' <span class="planet-retro">℞ RX</span>' : ''}</div>
      </div>
    `;
    grid.appendChild(el);
  }

  // Sign changes preview
  renderNextSignChanges(data.signs);

  // Timestamps
  const now = new Date();
  lastCalculated = now.getTime();
  document.getElementById('refresh-label').textContent = 'Updated ' + now.toLocaleTimeString([],{hour:'2-digit',minute:'2-digit'});
  nextRefreshTime = new Date(lastCalculated + 4*60*60*1000);
  document.getElementById('next-refresh-label').textContent = 'Next check: ' + nextRefreshTime.toLocaleTimeString([],{hour:'2-digit',minute:'2-digit'});
}

function renderNextSignChanges(signs) {
  const container = document.getElementById('sign-changes');
  const lines = [];
  const now = new Date();
  for (const p of ['Sun','Moon','Mercury','Venus','Mars']) {
    const s = signs[p];
    if (!s) continue;
    const degLeft = 30 - parseFloat(s.deg);
    const bodyLabel = PLANETS.find(x=>x.name===p).glyph + ' ' + p;
    lines.push(`<div class="result-row"><div class="result-label">${bodyLabel} in ${s.glyph} ${s.name}</div><div class="result-val">${degLeft.toFixed(1)}° remaining</div></div>`);
  }
  container.innerHTML = lines.join('') || '<div style="color:var(--dust)">Calculating…</div>';
}

// ─── SABBATS ─────────────────────────────────────────────────────────────────
function setHemi(h) {
  hemisphere = h;
  document.getElementById('hemi-n').classList.toggle('active', h==='N');
  document.getElementById('hemi-s').classList.toggle('active', h==='S');
  renderSabbats();
}

function getSabbatDate(s) {
  const dateStr = hemisphere === 'S' ? SABBAT_OFFSETS_S[s.name] : s.date;
  const now = new Date();
  const year = now.getFullYear();
  const parts = dateStr.split(' ');
  const months = {Jan:0,Feb:1,Mar:2,Apr:3,May:4,Jun:5,Jul:6,Aug:7,Sep:8,Oct:9,Nov:10,Dec:11};
  const m = months[parts[0]];
  const d = parseInt(parts[1]);
  let dt = new Date(year, m, d);
  if (dt < now) dt = new Date(year+1, m, d);
  return dt;
}

function renderSabbats() {
  const grid = document.getElementById('sabbat-grid');
  const now = new Date();
  // Find next sabbat
  let nearest = null, nearestDiff = Infinity;
  for (const s of SABBATS_N) {
    const dt = getSabbatDate(s);
    const diff = dt - now;
    if (diff >= 0 && diff < nearestDiff) { nearest = s.name; nearestDiff = diff; }
  }
  grid.innerHTML = SABBATS_N.map(s => {
    const dt = getSabbatDate(s);
    const diff = Math.ceil((dt - now) / 86400000);
    const dStr = diff === 0 ? 'Today!' : diff === 1 ? 'Tomorrow' : `In ${diff} days`;
    const dateStr = hemisphere === 'S' ? SABBAT_OFFSETS_S[s.name] : s.date;
    const isNext = s.name === nearest;
    return `<div class="sabbat-card ${isNext?'next-sabbat':''}" onclick="showSabbat('${s.name}')">
      <div class="sabbat-emoji">${s.emoji}</div>
      <div class="sabbat-name">${s.name}</div>
      <div class="sabbat-date">${dateStr}</div>
      <div class="sabbat-days">${dStr}</div>
    </div>`;
  }).join('');
}

function showSabbat(name) {
  const s = SABBATS_N.find(x=>x.name===name);
  if (!s) return;
  const dateStr = hemisphere === 'S' ? SABBAT_OFFSETS_S[s.name] : s.date;
  const hemiNote = hemisphere === 'S' ? `<div style="background:rgba(61,188,184,0.1);border:1px solid rgba(61,188,184,0.2);border-radius:8px;padding:10px;margin-bottom:16px;font-size:13px;color:var(--teal)">🌊 Southern Hemisphere: ${dateStr} — seasons are reversed, so this sabbat falls 6 months from the Northern date.</div>` : '';
  document.getElementById('modal-content').innerHTML = `
    <div style="font-size:36px;margin-bottom:8px">${s.emoji}</div>
    <div class="modal-title">${s.name}</div>
    <div class="modal-subtitle">${dateStr} ${hemisphere==='S'?'(Southern)':'(Northern)'} · Wheel of the Year</div>
    ${hemiNote}
    <div class="modal-body">
      <div class="modal-section"><p>${s.desc}</p></div>
      <div class="modal-section"><h4>Traditions</h4><p>${s.traditions.join(' · ')}</p></div>
      <div class="modal-section"><h4>Magical Focus</h4><p>${s.magic}</p></div>
      <div class="modal-section"><h4>Sacred Herbs</h4><div class="tag-row">${s.herbs.map(h=>`<span class="tag">🌿 ${h}</span>`).join('')}</div></div>
      <div class="modal-section"><h4>Crystals</h4><div class="tag-row">${s.crystals.map(c=>`<span class="tag">💎 ${c}</span>`).join('')}</div></div>
      <div class="modal-section"><h4>Colors</h4><div class="tag-row">${s.colors.map(c=>`<span class="tag">${c}</span>`).join('')}</div></div>
      <div class="modal-section"><h4>Associated Deities</h4><div class="tag-row">${s.deities.map(d=>`<span class="tag">✦ ${d}</span>`).join('')}</div></div>
    </div>
    <button class="btn-copy" onclick="copySabbat('${s.name}')">📋 Copy to Book of Shadows</button>
  `;
  document.getElementById('modal-overlay').classList.add('open');
}

function copySabbat(name) {
  const s = SABBATS_N.find(x=>x.name===name);
  const dateStr = hemisphere === 'S' ? SABBAT_OFFSETS_S[s.name] : s.date;
  const text = `✦ ${s.name} — ${dateStr}\n\n${s.desc}\n\nTraditions: ${s.traditions.join(', ')}\nMagical Focus: ${s.magic}\nHerbs: ${s.herbs.join(', ')}\nCrystals: ${s.crystals.join(', ')}\nColors: ${s.colors.join(', ')}\nDeities: ${s.deities.join(', ')}\n\n— Copied from Cosmic Whispers`;
  navigator.clipboard.writeText(text).then(() => showToast('Copied to clipboard! ✦'));
}

// ─── ZODIAC ──────────────────────────────────────────────────────────────────
function renderZodiac() {
  const grid = document.getElementById('zodiac-grid');
  grid.innerHTML = ZODIAC_DATA.map(z => `
    <div class="zodiac-card" onclick="showZodiac('${z.name}')">
      <span class="zodiac-glyph">${z.glyph}</span>
      <div class="zodiac-name">${z.name}</div>
      <div class="zodiac-dates">${z.dates}</div>
      <div class="zodiac-element">${z.element}</div>
    </div>
  `).join('');
}

function showZodiac(name) {
  const z = ZODIAC_DATA.find(x=>x.name===name);
  if (!z) return;
  document.getElementById('modal-content').innerHTML = `
    <div style="font-size:40px;margin-bottom:8px">${z.glyph}</div>
    <div class="modal-title">${z.name}</div>
    <div class="modal-subtitle">${z.dates} · Ruled by ${z.ruler}</div>
    <div class="modal-body">
      <div class="modal-section"><p>${z.description}</p></div>
      <div class="modal-section"><h4>Keywords</h4><div class="tag-row">${z.keywords.map(k=>`<span class="tag">${k}</span>`).join('')}</div></div>
      <div class="modal-section"><h4>Element & Modality</h4><p>${z.element} · ${z.mod} · ${z.polarity} polarity</p></div>
      <div class="modal-section"><h4>Body Rulership</h4><p>${z.body}</p></div>
      <div class="modal-section"><h4>Sacred Crystals</h4><div class="tag-row">${z.crystals.map(c=>`<span class="tag">💎 ${c}</span>`).join('')}</div></div>
      <div class="modal-section"><h4>Sacred Herbs</h4><div class="tag-row">${z.herbs.map(h=>`<span class="tag">🌿 ${h}</span>`).join('')}</div></div>
      <div class="modal-section"><h4>Colors</h4><div class="tag-row">${z.colors.map(c=>`<span class="tag">${c}</span>`).join('')}</div></div>
      <div class="modal-section"><h4>Associated Deity</h4><p>${z.deity}</p></div>
      <div class="modal-section"><h4>Core Traits</h4><p>${z.traits}</p></div>
    </div>
    <button class="btn-copy" onclick="copyZodiac('${z.name}')">📋 Copy to Book of Shadows</button>
  `;
  document.getElementById('modal-overlay').classList.add('open');
}

function copyZodiac(name) {
  const z = ZODIAC_DATA.find(x=>x.name===name);
  const text = `✦ ${z.glyph} ${z.name} — ${z.dates}\nRuler: ${z.ruler} · ${z.element} · ${z.mod}\n\n${z.description}\n\nKeywords: ${z.keywords.join(', ')}\nCrystals: ${z.crystals.join(', ')}\nHerbs: ${z.herbs.join(', ')}\nColors: ${z.colors.join(', ')}\nBody: ${z.body}\nDeity: ${z.deity}\n\n— Copied from Cosmic Whispers`;
  navigator.clipboard.writeText(text).then(() => showToast('Copied to clipboard! ✦'));
}

// ─── RESEARCH ────────────────────────────────────────────────────────────────
function runResearch() {
  const dateVal = document.getElementById('research-date').value;
  const timeVal = document.getElementById('research-time').value || '12:00';
  if (!dateVal) { showToast('Please choose a date first'); return; }

  const [y,mo,d] = dateVal.split('-').map(Number);
  const [h,mi] = timeVal.split(':').map(Number);
  const date = new Date(y, mo-1, d, h, mi, 0);

  const signs = calcPlanetSigns(date);
  const moon = getMoonPhase(date);
  const sunSign = signs['Sun'];
  const moonSign = signs['Moon'];

  // Numerology
  const numLife = [y,mo,d].join('').split('').reduce((a,b)=>a+parseInt(b),0);
  const numReduced = n => { while(n>9&&n!==11&&n!==22&&n!==33) n=[...String(n)].reduce((a,b)=>a+parseInt(b),0); return n; };
  const lifeNum = numReduced(numLife);

  // Build rows
  const rows = [
    ['Date & Time', date.toLocaleString([], {dateStyle:'long', timeStyle:'short'})],
    ['Sun Sign', `${sunSign.glyph} ${sunSign.name} ${sunSign.deg}°`],
    ['Moon Sign', `${moonSign.glyph} ${moonSign.name} ${moonSign.deg}°`],
    ['Moon Phase', `${moon.icon} ${moon.phase} (${moon.illumination}% lit)`],
    ...PLANETS.filter(p=>p.name!=='Sun'&&p.name!=='Moon').map(p => {
      const s = signs[p.name];
      return [p.glyph+' '+p.name, s ? `${s.glyph} ${s.name} ${s.deg}°${s.retro?' ℞':''}` : '—'];
    }),
    ['Life Number', lifeNum],
  ];

  document.getElementById('research-rows').innerHTML = rows.map(([l,v])=>`<div class="result-row"><div class="result-label">${l}</div><div class="result-val">${v}</div></div>`).join('');

  // Generate reading
  const retros = PLANETS.filter(p=>signs[p.name]?.retro).map(p=>p.name);
  const reading = generateReading(date, sunSign, moonSign, moon, signs, retros, lifeNum);
  document.getElementById('research-reading').textContent = reading;
  document.getElementById('research-result').style.display = 'block';
}

function generateReading(date, sun, moon, moonPhase, signs, retros, lifeNum) {
  const mercury = signs['Mercury'];
  const venus   = signs['Venus'];
  const mars    = signs['Mars'];
  const elements = { Aries:'fire',Taurus:'earth',Gemini:'air',Cancer:'water',Leo:'fire',Virgo:'earth',Libra:'air',Scorpio:'water',Sagittarius:'fire',Capricorn:'earth',Aquarius:'air',Pisces:'water' };
  const sunEl = elements[sun.name] || 'mixed';
  const moonEl = elements[moon.name] || 'mixed';

  let r = `On ${date.toLocaleDateString([],{dateStyle:'long'})}, the cosmos weaves a distinct tapestry. `;
  r += `The Sun moves through ${sun.glyph} ${sun.name}, radiating ${sunEl} energy and illuminating themes of ${sun.name === 'Aries' ? 'courage and new beginnings' : sun.name === 'Taurus' ? 'beauty, patience, and earthly abundance' : sun.name === 'Gemini' ? 'curiosity and communication' : sun.name === 'Cancer' ? 'home, nurturing, and emotional depth' : sun.name === 'Leo' ? 'creativity, radiance, and joy' : sun.name === 'Virgo' ? 'service, healing, and discernment' : sun.name === 'Libra' ? 'balance, beauty, and relationships' : sun.name === 'Scorpio' ? 'transformation, mystery, and depth' : sun.name === 'Sagittarius' ? 'freedom, philosophy, and adventure' : sun.name === 'Capricorn' ? 'ambition, discipline, and legacy' : sun.name === 'Aquarius' ? 'vision, community, and innovation' : 'dreams, compassion, and surrender'}. `;
  r += `The Moon in ${moonPhase.icon} ${moonPhase.phase} (${moonPhase.illumination}% illuminated) through ${moon.name} ${moonEl === sunEl ? 'echoes and amplifies this elemental theme' : 'creates a dynamic interplay between ' + sunEl + ' and ' + moonEl + ' energies'}. `;
  if (mercury) r += `Mercury in ${mercury.glyph} ${mercury.name}${mercury.retro ? ' (retrograde — review before committing, double-check communications)' : ' favours clear and direct expression'}. `;
  if (venus) r += `Venus in ${venus.glyph} ${venus.name} colours matters of love and creativity with ${venus.name} qualities. `;
  if (mars) r += `Mars in ${mars.glyph} ${mars.name} fuels action and desire. `;
  if (retros.length > 0) r += `\n\nPlanets in retrograde: ${retros.join(', ')} — these are periods to reflect, revise, and revisit rather than forge ahead recklessly. `;
  r += `\n\nNumerologically, the life path vibration ${lifeNum} carries the energy of ${lifeNum===1?'leadership and independence':lifeNum===2?'partnership and balance':lifeNum===3?'creativity and expression':lifeNum===4?'structure and hard work':lifeNum===5?'freedom and change':lifeNum===6?'love and responsibility':lifeNum===7?'wisdom and spiritual depth':lifeNum===8?'power and manifestation':lifeNum===9?'completion and compassion':lifeNum===11?'illumination and spiritual sensitivity (master number)':lifeNum===22?'master builder energy':lifeNum===33?'master teacher energy':'sacred numerological energy'}.`;
  r += '\n\n✦ Always verify planetary positions at astro.com for precision chart work.';
  return r;
}

function copyResearch() {
  const dateVal = document.getElementById('research-date').value;
  const rows = document.getElementById('research-rows').querySelectorAll('.result-row');
  const reading = document.getElementById('research-reading').textContent;
  let text = `✦ Astrological Research Chart\n${dateVal}\n\n`;
  rows.forEach(r => {
    const label = r.querySelector('.result-label').textContent;
    const val   = r.querySelector('.result-val').textContent;
    text += `${label}: ${val}\n`;
  });
  text += `\n— Reading —\n${reading}\n\n— Copied from Cosmic Whispers`;
  navigator.clipboard.writeText(text).then(() => showToast('Copied to clipboard! ✦'));
}

// ─── JOURNAL ─────────────────────────────────────────────────────────────────
function saveEntry() {
  const title = document.getElementById('journal-title').value.trim();
  const text  = document.getElementById('journal-text').value.trim();
  if (!text) { showToast('Write something first…'); return; }

  const now = new Date();
  const moonInfo = cachedData ? `${cachedData.moon.icon} ${cachedData.moon.phase} · ${cachedData.signs?.['Moon']?.name || ''}` : '';
  const entry = { id: Date.now(), date: now.toISOString(), title, text, moon: moonInfo };
  journals.unshift(entry);
  localStorage.setItem('cw_journal', JSON.stringify(journals));
  document.getElementById('journal-title').value = '';
  document.getElementById('journal-text').value = '';
  renderJournal();
  showToast('Entry saved to your Book of Shadows ✦');
}

function renderJournal() {
  const container = document.getElementById('journal-entries');
  if (journals.length === 0) {
    container.innerHTML = '<div style="color:var(--dust);font-style:italic;text-align:center;padding:20px">Your entries will appear here…</div>';
    return;
  }
  container.innerHTML = journals.map(e => `
    <div class="journal-entry">
      <div class="journal-entry-date">${new Date(e.date).toLocaleDateString([],{dateStyle:'full'})}</div>
      ${e.title ? `<div style="font-family:Cinzel Decorative,serif;font-size:13px;color:var(--silver);margin-bottom:6px">${e.title}</div>` : ''}
      <div class="journal-entry-text">${e.text}</div>
      ${e.moon ? `<div class="journal-entry-moon">${e.moon}</div>` : ''}
      <div style="display:flex;gap:8px;margin-top:10px">
        <button class="btn-copy" style="flex:1;margin-top:0" onclick="copyEntry(${e.id})">📋 Copy</button>
        <button class="btn-copy" style="flex:1;margin-top:0;background:rgba(180,80,80,0.1);border-color:rgba(180,80,80,0.3);color:#c46060" onclick="deleteEntry(${e.id})">🗑 Delete</button>
      </div>
    </div>
  `).join('');
}

function copyEntry(id) {
  const e = journals.find(x=>x.id===id);
  if (!e) return;
  const text = `✦ Book of Shadows Entry\n${new Date(e.date).toLocaleDateString([],{dateStyle:'full'})}\n${e.title ? e.title+'\n' : ''}\n${e.text}${e.moon ? '\n\nMoon: '+e.moon : ''}\n\n— Cosmic Whispers`;
  navigator.clipboard.writeText(text).then(() => showToast('Copied to clipboard! ✦'));
}

function deleteEntry(id) {
  journals = journals.filter(x=>x.id!==id);
  localStorage.setItem('cw_journal', JSON.stringify(journals));
  renderJournal();
}

// ─── MODAL ───────────────────────────────────────────────────────────────────
function closeModal(e) {
  if (!e || e.target === document.getElementById('modal-overlay')) {
    document.getElementById('modal-overlay').classList.remove('open');
  }
}

// ─── NAVIGATION ──────────────────────────────────────────────────────────────
function showPage(name, btn) {
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-'+name).classList.add('active');
  if (btn) btn.classList.add('active');
}

// ─── TOAST ───────────────────────────────────────────────────────────────────
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'), 2500);
}

// ─── INIT ────────────────────────────────────────────────────────────────────
function init() {
  // Set research date default
  const today = new Date();
  const yyyy = today.getFullYear();
  const mm   = String(today.getMonth()+1).padStart(2,'0');
  const dd   = String(today.getDate()).padStart(2,'0');
  document.getElementById('research-date').value = `${yyyy}-${mm}-${dd}`;

  renderZodiac();
  renderSabbats();
  renderJournal();

  // Try geolocation for moon times
  const doCalc = (lat, lon) => {
    if (!shouldRefresh()) {
      renderDashboard(cachedData);
      return;
    }
    const data = computeData(new Date(), lat, lon);
    cachedData = data;
    renderDashboard(data);
  };

  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(
      pos => doCalc(pos.coords.latitude, pos.coords.longitude),
      ()  => doCalc(null, null)
    );
  } else {
    doCalc(null, null);
  }

  // Auto-check every 10 minutes for sign changes
  setInterval(() => {
    if (shouldRefresh()) {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          pos => { const d = computeData(new Date(), pos.coords.latitude, pos.coords.longitude); cachedData=d; renderDashboard(d); },
          () => { const d = computeData(new Date(), null, null); cachedData=d; renderDashboard(d); }
        );
      } else {
        const d = computeData(new Date(), null, null);
        cachedData = d; renderDashboard(d);
      }
    }
  }, 10 * 60 * 1000);
}

window.addEventListener('load', init);
</script>
</head>
</html>
