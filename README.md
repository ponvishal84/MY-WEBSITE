# MY-WEBSITE<!DOCTYPE html><!DOCTYPE html><!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>SmartStudy AI — Futuristic Edition (Full)</title>
<meta name="description" content="SmartStudy AI — futuristic study planner with voice assistant, animated background, dark mode, saving plans, and a premium UI for project submission." />
<meta name="theme-color" content="#050816" />

<!-- Fonts & Icons -->
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

<style>
  :root{
    --bg-dark:#050816;
    --bg-light:#f5f7fb;
    --card-dark: rgba(255,255,255,0.06);
    --card-light: rgba(255,255,255,0.9);
    --accent:#00c3ff;
    --accent-2:#7c4dff;
    --glass-border: rgba(255,255,255,0.08);
    --text-light:#eaf2ff;
    --text-dark:#111827;
  }
  /* Basic resets */
  *{box-sizing:border-box}
  html,body{height:100%;margin:0;font-family:"Poppins",system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial;}
  body{background: radial-gradient(1200px 800px at 10% 10%, rgba(0,135,255,0.06), transparent), radial-gradient(900px 700px at 90% 90%, rgba(124,77,255,0.04), transparent); color:var(--text-light); min-height:100vh; overflow:hidden;}
  /* Theme toggling */
  body.light{
    background: linear-gradient(180deg,#f7fbff,#eef6ff);
    color:var(--text-dark);
  }

  /* Canvas background full screen */
  #bg-canvas{position:fixed;inset:0;z-index:0;width:100%;height:100%;display:block}

  /* Splash screen */
  .splash {
    position:fixed;inset:0;z-index:40;display:flex;align-items:center;justify-content:center;
    background:linear-gradient(180deg, rgba(2,6,23,0.95), rgba(2,6,23,0.88));
    color:white;flex-direction:column;gap:18px;backdrop-filter: blur(6px);
  }
  .splash .logo {
    width:110px;height:110px;border-radius:22px;
    background:linear-gradient(135deg,var(--accent),var(--accent-2));
    display:flex;align-items:center;justify-content:center;font-weight:800;font-size:34px;box-shadow:0 10px 40px rgba(0,0,0,0.5);
  }
  .splash h1{margin:0;font-size:20px;letter-spacing:0.6px}
  .progress {
    width:320px;max-width:80%;height:8px;background:rgba(255,255,255,0.08);border-radius:999px;overflow:hidden;
  }
  .progress > i {display:block;height:100%;width:0;background:linear-gradient(90deg,var(--accent),var(--accent-2));border-radius:999px;transition:width 300ms linear}

  /* Top header */
  header {
    position:relative;z-index:10;display:flex;align-items:center;gap:12px;padding:14px 18px;
    justify-content:space-between;
    width:100%;
    max-width:1200px;margin:20px auto 0;
  }

  .brand {
    display:flex;gap:12px;align-items:center;
  }
  .brand .mark{
    width:44px;height:44px;border-radius:10px;
    background:linear-gradient(135deg,var(--accent),var(--accent-2));
    display:flex;align-items:center;justify-content:center;font-weight:800;font-size:18px;color:#021226;box-shadow:0 10px 30px rgba(0,195,255,0.12);
  }
  .brand .title{display:flex;flex-direction:column;line-height:1}
  .brand .title .main{font-weight:700;font-size:16px}
  .brand .title .sub{font-size:12px;opacity:0.8;margin-top:2px}

  /* Controls */
  .controls {display:flex;gap:12px;align-items:center}
  .icon-btn{
    display:inline-flex;align-items:center;justify-content:center;border-radius:10px;padding:8px;cursor:pointer;
    background:rgba(255,255,255,0.02);border:1px solid rgba(255,255,255,0.03);backdrop-filter: blur(6px);
  }
  .icon-btn:active{transform:scale(0.98)}
  .icon-btn svg{width:20px;height:20px}

  /* Main layout: center card and side actions for larger screens */
  .wrap{position:relative;z-index:5;display:flex;gap:22px;align-items:flex-start;justify-content:center;padding:24px;max-width:1200px;margin:18px auto}
  .left {
    width:100%;max-width:760px;
    border-radius:18px;
    padding:28px;
    background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.02));
    border:1px solid var(--glass-border);
    backdrop-filter: blur(10px);
    box-shadow:0 10px 40px rgba(0,0,0,0.4);
  }

  /* Small right panel */
  .right {
    width:320px;min-height:200px;border-radius:14px;padding:18px;
    background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    border:1px solid var(--glass-border);backdrop-filter: blur(8px);
  }

  /* Heading and hero */
  .hero {
    display:flex;align-items:center;gap:16px;margin-bottom:18px;
  }
  .hero h2{margin:0;font-size:22px;color:inherit}
  .hero p{margin:0;opacity:0.85;font-size:13px}

  /* form controls */
  label{display:block;font-weight:600;margin-top:12px;font-size:13px;opacity:0.95}
  input, select, textarea{
    width:100%;padding:12px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);background:rgba(0,0,0,0.12);color:inherit;font-size:15px;margin-top:8px;
  }
  body.light input, body.light textarea {background:white;border:1px solid #e7eefc;color:var(--text-dark)}
  textarea{min-height:90px;resize:vertical}

  /* buttons */
  .primary {
    margin-top:18px;padding:14px;border-radius:12px;display:inline-flex;align-items:center;gap:10px;justify-content:center;width:100%;
    background:linear-gradient(90deg,var(--accent),var(--accent-2));color:#021226;font-weight:700;border:none;cursor:pointer;box-shadow:0 10px 30px rgba(0,195,255,0.11);
  }
  .ghost{
    margin-top:12px;padding:10px;border-radius:10px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:inherit;cursor:pointer;width:100%;
  }

  /* outputs */
  .output {
    margin-top:18px;padding:14px;border-radius:10px;background:linear-gradient(180deg,rgba(0,195,255,0.06),rgba(124,77,255,0.03));
    border-left:4px solid var(--accent);white-space:pre-line;font-weight:600;
  }

  /* saved list */
  .saved-list{display:flex;flex-direction:column;gap:10px;margin-top:8px}
  .saved-item{padding:10px;border-radius:10px;background:rgba(0,0,0,0.06);display:flex;justify-content:space-between;align-items:center}
  .saved-item small{opacity:0.85}

  /* footer small */
  footer{position:relative;z-index:6;text-align:center;opacity:0.7;margin:18px auto;color:var(--text-light);font-size:13px}

  /* responsive */
  @media (max-width:980px){
    .wrap{flex-direction:column;padding:12px}
    .right{width:100%;max-width:600px}
  }
  @media (max-width:520px){
    header{padding:10px 12px}
    .brand .title .main{font-size:14px}
  }

  /* small helper styles for toggles */
  .switch {display:inline-flex;align-items:center;gap:8px}
  .switch input{display:none}
  .switch .knob{width:44px;height:26px;background:rgba(255,255,255,0.06);border-radius:999px;padding:4px;display:inline-flex;align-items:center}
  .switch .dot{width:18px;height:18px;border-radius:50%;background:white}
  body.light .switch .knob{background:#e6eefc}
  body.light .switch .dot{background:var(--accent)}
</style>
</head>
<body>

<!-- BACKGROUND CANVAS -->
<canvas id="bg-canvas" aria-hidden="true"></canvas>

<!-- SPLASH LOADER -->
<div class="splash" id="splash" role="status" aria-live="polite">
  <div class="logo" aria-hidden="true">SS</div>
  <h1>SmartStudy AI</h1>
  <div class="progress" aria-hidden="true"><i id="progress-bar"></i></div>
  <small style="opacity:0.8">Initializing futuristic UI...</small>
</div>

<!-- Top header -->
<header>
  <div class="brand" aria-hidden="false">
    <div class="mark">SS</div>
    <div class="title"><div class="main">SmartStudy AI</div><div class="sub">Futuristic Study Planner</div></div>
  </div>

  <div class="controls" role="toolbar" aria-label="App controls">
    <div class="switch" title="Toggle theme" id="theme-toggle" role="button" tabindex="0" aria-pressed="false" aria-label="Toggle dark or light theme">
      <div class="knob"><div class="dot" id="theme-dot"></div></div>
    </div>

    <button class="icon-btn" id="voice-btn" title="Voice input" aria-label="Use voice to input subjects">
      <span class="material-icons" style="color:var(--accent)">mic</span>
    </button>

    <button class="icon-btn" id="tts-btn" title="Read plan aloud" aria-label="Read plan aloud">
      <span class="material-icons" style="color:var(--accent-2)">volume_up</span>
    </button>
  </div>
</header>

<!-- Main content -->
<main class="wrap" role="main">

  <!-- left: planner -->
  <section class="left" id="page-planner" aria-labelledby="planner-title">
    <div class="hero" >
      <div>
        <h2 id="planner-title">Futuristic Study Planner</h2>
        <p>Use voice or type subjects, select hours and difficulty. Save plans locally for later.</p>
      </div>
    </div>

    <label for="subjects">Enter your subjects (comma separated)</label>
    <textarea id="subjects" placeholder="Math, Physics, English" aria-label="Subjects"></textarea>

    <label for="hours">Hours available per day</label>
    <input id="hours" type="number" min="0.5" step="0.5" placeholder="Example: 4" aria-label="Hours available per day">

    <label for="difficulty">Difficulty level</label>
    <select id="difficulty" aria-label="Difficulty level">
      <option value="easy">Easy</option>
      <option value="medium" selected>Medium</option>
      <option value="hard">Hard</option>
    </select>

    <button class="primary" id="generate-btn" aria-pressed="false">
      <span class="material-icons" style="color:#021226">auto_awesome</span>
      Generate Futuristic Plan
    </button>

    <div id="output" class="output" role="region" aria-live="polite">Your futuristic study plan will appear here.</div>

    <div style="display:flex;gap:12px;margin-top:14px">
      <button class="ghost" id="save-btn" title="Save plan">Save Plan</button>
      <button class="ghost" id="clear-btn" title="Clear fields">Clear</button>
    </div>
  </section>

  <!-- right: saved plans and navigation -->
  <aside class="right" aria-labelledby="saved-title">
    <h3 id="saved-title" style="margin:0 0 8px 0">Saved Plans</h3>
    <div class="saved-list" id="saved-list" aria-live="polite">
      <!-- saved plans inserted here -->
    </div>

    <hr style="margin:14px 0;border:none;border-top:1px solid rgba(255,255,255,0.03)">

    <div style="display:flex;gap:8px;flex-direction:column">
      <button class="ghost" id="view-about">About</button>
      <button class="ghost" id="view-planner">Planner</button>
      <button class="ghost" id="view-saved">Saved</button>
    </div>
  </aside>
</main>

<footer aria-hidden="false">Made with ♥ — SmartStudy AI • Save plans locally • Works offline after load (cached)</footer>

<!-- SOUND EFFECTS are created with WebAudio; no external files needed -->

<script>
/* -------------------------
   Initialization & splash
   ------------------------- */
const splash = document.getElementById('splash');
const progressBar = document.getElementById('progress-bar');

let prog = 0;
const progInterval = setInterval(()=> {
  prog += Math.random()*18;
  if (prog > 100) prog = 100;
  progressBar.style.width = prog + "%";
  if (prog >= 100) {
    clearInterval(progInterval);
    setTimeout(()=> {
      splash.style.transition = "opacity 400ms ease, transform 400ms ease";
      splash.style.opacity = 0;
      splash.style.transform = "translateY(-8px)";
      setTimeout(()=> splash.remove(), 500);
    }, 450);
  }
}, 220);

/* -------------------------
   Background particles (lightweight 3D-like)
   ------------------------- */

const canvas = document.getElementById('bg-canvas');
const ctx = canvas.getContext('2d');
let W, H, particles=[];

function resize() {
  W = canvas.width = innerWidth;
  H = canvas.height = innerHeight;
}
window.addEventListener('resize', resize, {passive:true});
resize();

function rnd(min,max){return Math.random()*(max-min)+min}

class P {
  constructor(){
    // simulate depth with z between 0.2..1.6
    this.z = rnd(0.25,1.6);
    this.x = rnd(0,W);
    this.y = rnd(0,H);
    this.vx = rnd(-0.2,0.2)/this.z;
    this.vy = rnd(-0.05,0.15)/this.z;
    this.r = rnd(0.6,2.3)* (1/this.z);
    this.hue = rnd(180,220);
  }
  step(){
    this.x += this.vx;
    this.y += this.vy;
    if (this.x < -20) this.x = W + 20;
    if (this.x > W + 20) this.x = -20;
    if (this.y > H + 20) this.y = -20;
  }
  draw(){
    ctx.beginPath();
    const alpha = Math.min(0.9,0.12*this.z + 0.02);
    ctx.fillStyle = `hsla(${this.hue},90%,65%,${alpha})`;
    ctx.shadowBlur = 12 * (1/this.z);
    ctx.shadowColor = `hsla(${this.hue},90%,60%,0.9)`;
    ctx.arc(this.x, this.y, this.r, 0, Math.PI*2);
    ctx.fill();
  }
}

function initParticles(n=140){
  particles = [];
  for(let i=0;i<n;i++) particles.push(new P());
}
initParticles(Math.floor((innerWidth+innerHeight)/20));

let mouse = {x:W/2,y:H/2};
window.addEventListener('mousemove', e=> {mouse.x=e.clientX;mouse.y=e.clientY});

function frame(){
  ctx.clearRect(0,0,W,H);
  // subtle gradient
  const g = ctx.createLinearGradient(0,0,W,H);
  g.addColorStop(0,'rgba(2,6,23,0.02)');
  g.addColorStop(1,'rgba(2,6,23,0.06)');
  ctx.fillStyle = g;
  ctx.fillRect(0,0,W,H);

  // parallax: offset particles slightly towards/away from mouse
  const cx = mouse.x - W/2, cy = mouse.y - H/2;
  for(const p of particles){
    // small attraction/repel to mouse for life
    p.x += (cx * 0.00002) * p.z;
    p.y += (cy * 0.00002) * p.z;
    p.step();
    p.draw();
  }
  requestAnimationFrame(frame);
}
frame();

/* -------------------------
   UI behavior, voice, TTS, audio cues, storage
   ------------------------- */

const subjectsEl = document.getElementById('subjects');
const hoursEl = document.getElementById('hours');
const difficultyEl = document.getElementById('difficulty');
const generateBtn = document.getElementById('generate-btn');
const outputEl = document.getElementById('output');
const saveBtn = document.getElementById('save-btn');
const clearBtn = document.getElementById('clear-btn');
const savedList = document.getElementById('saved-list');

const themeToggle = document.getElementById('theme-toggle');
const themeDot = document.getElementById('theme-dot');
const voiceBtn = document.getElementById('voice-btn');
const ttsBtn = document.getElementById('tts-btn');

let synth = window.speechSynthesis;
let recognition = null;
let isRecording = false;
// speech recognition setup (chrome prefix)
if ('webkitSpeechRecognition' in window || 'SpeechRecognition' in window) {
  const SR = window.SpeechRecognition || webkitSpeechRecognition;
  recognition = new SR();
  recognition.lang = navigator.language || 'en-US';
  recognition.interimResults = false;
}

/* tiny audio cue generator using WebAudio */
const AudioCtx = window.AudioContext||window.webkitAudioContext;
const audioCtx = AudioCtx ? new AudioCtx() : null;
function beep(freq=440, dur=0.12, vol=0.08){
  if (!audioCtx) return;
  const o = audioCtx.createOscillator();
  const g = audioCtx.createGain();
  o.type = 'sine'; o.frequency.value = freq;
  g.gain.value = vol;
  o.connect(g); g.connect(audioCtx.destination);
  o.start();
  setTimeout(()=>{ o.stop(); }, dur*1000);
}

/* toast-like subtle feedback (console fallback) */
function toast(text){
  // small console fallback
  console.log("Toast:", text);
  // beep for tactile feedback
  beep(520,0.08,0.03);
}

/* Generate plan logic */
function generatePlan() {
  beep(880,0.06,0.045);
  const raw = subjectsEl.value || '';
  const subjects = raw.split(',').map(s=>s.trim()).filter(Boolean);
  const hours = parseFloat(hoursEl.value) || 0;
  const diff = difficultyEl.value || 'medium';
  if (subjects.length === 0 || !hours) {
    outputEl.innerText = '⚠️ Please provide subjects and hours.';
    toast('Please fill in fields');
    return;
  }
  const multiplier = diff === 'easy' ? 0.85 : diff === 'hard' ? 1.2 : 1.0;
  const perSub = (hours / subjects.length) * multiplier;
  let plan = `⚡ Futuristic Study Plan\n\n`;
  subjects.forEach(s => plan += `• ${s}: ${perSub.toFixed(1)} hrs/day\n`);
  plan += `\nGenerated: ${new Date().toLocaleString()}`;
  outputEl.innerText = plan;
  toast('Plan generated');
}

/* Save plan to localStorage */
function savePlan() {
  const title = prompt('Give this plan a name (e.g., "Exam Prep - May")', `Plan ${new Date().toLocaleString()}`);
  if (!title) return;
  const plan = outputEl.innerText;
  if (!plan || plan.startsWith('⚠')) { alert('Generate a plan first.'); return; }
  const items = JSON.parse(localStorage.getItem('ss_plans')||'[]');
  items.push({id:Date.now(),title,plan, created:Date.now()});
  localStorage.setItem('ss_plans', JSON.stringify(items));
  renderSaved();
  toast('Plan saved');
}

/* Render saved plans */
function renderSaved(){
  const items = JSON.parse(localStorage.getItem('ss_plans')||'[]');
  savedList.innerHTML = '';
  if (!items.length) {
    savedList.innerHTML = '<small style="opacity:0.7">No saved plans yet. Save your first plan!</small>';
    return;
  }
  items.slice().reverse().forEach(it=>{
    const el = document.createElement('div'); el.className='saved-item';
    el.innerHTML = `<div><strong>${escapeHtml(it.title)}</strong><br><small>${new Date(it.created).toLocaleString()}</small></div>
      <div style="display:flex;gap:8px">
        <button class="ghost" data-id="${it.id}" data-action="load">Load</button>
        <button class="ghost" data-id="${it.id}" data-action="delete">Delete</button>
      </div>`;
    savedList.appendChild(el);
  });
}

/* Helpers: escapeHtml */
function escapeHtml(s){ return s.replace(/[&<>"']/g, c=>({ '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }

/* load plan */
function loadPlan(id){
  const items = JSON.parse(localStorage.getItem('ss_plans')||'[]');
  const it = items.find(x=>x.id==id);
  if (!it) return;
  outputEl.innerText = it.plan;
  toast('Plan loaded');
}

/* delete plan */
function deletePlan(id){
  if (!confirm('Delete this saved plan?')) return;
  const items = JSON.parse(localStorage.getItem('ss_plans')||'[]');
  const remaining = items.filter(x=>x.id!=id);
  localStorage.setItem('ss_plans', JSON.stringify(remaining));
  renderSaved();
  toast('Plan deleted');
}

/* clear fields */
clearBtn.addEventListener('click', ()=>{
  subjectsEl.value=''; hoursEl.value=''; difficultyEl.value='medium'; outputEl.innerText='Your futuristic study plan will appear here.'; beep(660,0.05,0.03);
});

/* click handlers */
generateBtn.addEventListener('click', generatePlan);
saveBtn.addEventListener('click', savePlan);

/* delegated clicks for saved list */
savedList.addEventListener('click', (ev)=>{
  const btn = ev.target.closest('button');
  if (!btn) return;
  const id = btn.dataset.id;
  const act = btn.dataset.action;
  if (act==='load') loadPlan(id);
  if (act==='delete') deletePlan(id);
});

/* keyboard accessible theme toggle */
themeToggle.addEventListener('click', toggleTheme);
themeToggle.addEventListener('keypress', (e)=>{ if (e.key==='Enter'||e.key===' ') toggleTheme(); });

/* Theme toggling with persistence */
function applyTheme(theme){
  if (theme === 'light') {
    document.body.classList.add('light');
    localStorage.setItem('ss_theme','light');
    themeToggle.setAttribute('aria-pressed','true');
  } else {
    document.body.classList.remove('light');
    localStorage.setItem('ss_theme','dark');
    themeToggle.setAttribute('aria-pressed','false');
  }
}
function toggleTheme(){
  const cur = localStorage.getItem('ss_theme') || 'dark';
  applyTheme(cur==='dark' ? 'light' : 'dark');
  beep(520,0.06,0.03);
}
applyTheme(localStorage.getItem('ss_theme') || 'dark');

/* Voice recognition: populate subjects textarea with recognition result */
if (recognition) {
  recognition.onstart = ()=> { isRecording=true; voiceBtn.classList.add('active'); voiceBtn.title='Listening... (click to stop)'; toast('Voice started'); }
  recognition.onend = ()=> { isRecording=false; voiceBtn.classList.remove('active'); voiceBtn.title='Voice input'; toast('Voice ended'); }
  recognition.onresult = (e)=> {
    const t = Array.from(e.results).map(r=>r[0].transcript).join(' ');
    // append recognized text into subjects
    subjectsEl.value = subjectsEl.value ? subjectsEl.value + ', ' + t : t;
  };
  recognition.onerror = (e)=> {
    console.warn('Speech recognition error', e);
    alert('Voice recognition error or not allowed. Try granting mic permission or use the manual input.');
  }
}

/* voice button toggles recognition */
voiceBtn.addEventListener('click', ()=>{
  if (!recognition) { alert('Speech recognition not supported in this browser.'); return; }
  if (!isRecording) {
    try { recognition.start(); } catch(e){ console.warn(e); }
  } else {
    recognition.stop();
  }
});

/* TTS: read the output */
ttsBtn.addEventListener('click', ()=>{
  const text = outputEl.innerText || '';
  if (!('speechSynthesis' in window)) { alert('Text-to-speech not supported'); return; }
  if (!text || text.startsWith('⚠')) { alert('Generate a plan to read it aloud'); return; }
  const ut = new SpeechSynthesisUtterance(text.replace(/\n/g,'. '));
  ut.lang = navigator.language || 'en-US';
  ut.rate = 1;
  synth.cancel();
  synth.speak(ut);
  beep(440,0.06,0.03);
});

/* Navigation simple SPA (hash) */
document.getElementById('view-about').addEventListener('click', ()=> showAbout());
document.getElementById('view-planner').addEventListener('click', ()=> showPlanner());
document.getElementById('view-saved').addEventListener('click', ()=> showSaved());

function showAbout(){
  // simple overlay modal or alert for this single-file demo
  alert('SmartStudy AI — Futuristic Edition\\n\\nThis demo includes:\\n• Voice input & TTS\\n• Animated background\\n• Save/load plans locally\\n• Light/Dark mode\\n• Sound effects\\n• Mobile-friendly UI\\n\\nGood luck with your project submission!');
}
function showPlanner(){ window.scrollTo({top:0,behavior:'smooth'}); }
function showSaved(){ window.scrollTo({top:0,behavior:'smooth'}); }

/* Keyboard hint for accessibility */
document.addEventListener('keydown',(e)=>{
  if (e.key === 'g' && (e.ctrlKey || e.metaKey)) { e.preventDefault(); generatePlan(); }
});

/* render on load */
renderSaved();

/* small portability: load previously saved inputs */
subjectsEl.value = localStorage.getItem('ss_last_subjects') || '';
hoursEl.value = localStorage.getItem('ss_last_hours') || '';
difficultyEl.value = localStorage.getItem('ss_last_diff') || 'medium';

/* save last inputs as user types (auto-save) */
['input','change'].forEach(evt=>{
  subjectsEl.addEventListener(evt, ()=> localStorage.setItem('ss_last_subjects', subjectsEl.value));
  hoursEl.addEventListener(evt, ()=> localStorage.setItem('ss_last_hours', hoursEl.value));
  difficultyEl.addEventListener(evt, ()=> localStorage.setItem('ss_last_diff', difficultyEl.value));
});

/* PWA-like quick manifest (not fully PWA but gives meta for add-to-home) */
(function addMeta(){
  const meta = document.createElement('link');
  meta.rel='manifest';
  // not providing manifest file here; if you want, add a manifest.json to repo and update href
  // meta.href='/manifest.json';
  document.head.appendChild(meta);
})();

/* make sure audio context is resumed on first user interaction in some mobile browsers */
['click','touchstart'].forEach(ev=>window.addEventListener(ev, ()=>{ if (audioCtx && audioCtx.state === 'suspended') audioCtx.resume(); }, {once:true}));

</script>
</body>
</html>
