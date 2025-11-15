<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>SmartStudy AI — Personalized Study Planner</title>
  <meta name="description" content="SmartStudy AI generates a personalized daily study plan. Enter subjects, choose hours and difficulty — get a balanced schedule instantly." />
  <meta name="theme-color" content="#0F62FE" />

  <!-- Open Graph (when shared on social) -->
  <meta property="og:title" content="SmartStudy AI — Personalized Study Planner" />
  <meta property="og:description" content="Generate a custom, balanced study plan in seconds. Mobile-friendly, accessible, and ready to save your plans." />
  <meta property="og:type" content="website" />

  <!-- Google Fonts & Material Icons -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

  <style>
    :root{
      --md-blue: #0F62FE;
      --md-surface: #ffffff;
      --bg: #f4f6fb;
      --text: #102a43;
      --muted: #637381;
      --card-radius: 12px;
      --shadow-sm: 0 6px 18px rgba(16,42,67,0.08);
      --shadow-md: 0 10px 30px rgba(16,42,67,0.10);
    }

    /* Light / Dark */
    html[data-theme="dark"] {
      --md-surface: #0b1220;
      --bg: linear-gradient(180deg,#071022,#020511);
      --text: #e6f0ff;
      --muted: #9fb2d1;
      --shadow-sm: 0 8px 30px rgba(2,8,23,0.6);
      --shadow-md: 0 20px 40px rgba(2,8,23,0.7);
    }

    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: "Inter", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background: var(--bg);
      color:var(--text);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      line-height:1.45;
      padding: 24px;
    }

    /* Top bar */
    .topbar{
      max-width:1200px;margin:0 auto 20px;display:flex;align-items:center;justify-content:space-between;gap:12px;
    }
    .brand{display:flex;align-items:center;gap:12px}
    .brand .badge{
      width:54px;height:54px;border-radius:12px;background:linear-gradient(135deg,var(--md-blue),#5f7cff);display:flex;align-items:center;justify-content:center;color:white;font-weight:700;font-size:20px;box-shadow:var(--shadow-sm);
    }
    .brand .title{font-weight:700;font-size:18px}
    .top-actions{display:flex;gap:8px;align-items:center}

    .icon-btn{
      background:var(--md-surface);border-radius:10px;padding:10px;display:inline-flex;align-items:center;gap:8px;border:1px solid rgba(16,42,67,0.06);box-shadow:var(--shadow-sm);cursor:pointer;
    }
    .icon-btn:active{transform:translateY(1px)}
    .icon-btn .material-icons{color:var(--md-blue)}

    /* Layout */
    .layout{max-width:1100px;margin:0 auto;display:grid;grid-template-columns:1fr 340px;gap:24px;align-items:start}
    @media (max-width:980px){ .layout{grid-template-columns:1fr; padding:0 12px} }

    /* Main card */
    .card{
      background:var(--md-surface);
      border-radius:var(--card-radius);
      padding:26px;
      box-shadow:var(--shadow-md);
      border:1px solid rgba(16,42,67,0.04);
    }
    h1{margin:0 0 6px;font-size:20px}
    p.lead{margin:0 0 18px;color:var(--muted);font-size:14px}

    /* form */
    label{display:block;font-weight:600;margin-top:12px;font-size:13px;color:var(--muted)}
    input,select,textarea{
      width:100%;padding:12px;border-radius:10px;border:1px solid rgba(16,42,67,0.06);margin-top:8px;font-size:15px;background:transparent;color:inherit;
    }
    textarea{min-height:100px;resize:vertical}
    input[type="number"]::-webkit-outer-spin-button,input[type="number"]::-webkit-inner-spin-button{appearance:none;margin:0}

    .controls-row{display:flex;gap:12px;margin-top:14px}
    .btn{
      display:inline-flex;align-items:center;justify-content:center;gap:10px;padding:12px 16px;border-radius:10px;border:none;cursor:pointer;
      font-weight:700;font-size:15px;
    }
    .btn.primary{background:var(--md-blue);color:white;box-shadow:0 8px 28px rgba(15,98,254,0.18);flex:1}
    .btn.ghost{background:transparent;border:1px solid rgba(16,42,67,0.06);flex:1}

    .output{
      margin-top:18px;padding:14px;border-radius:10px;background:linear-gradient(180deg, rgba(15,98,254,0.06), rgba(95,124,255,0.02));font-weight:600;white-space:pre-line;
    }

    /* Right panel */
    .panel h3{margin:0 0 8px}
    .saved-list{margin-top:12px;display:flex;flex-direction:column;gap:10px}
    .saved{background:linear-gradient(180deg, rgba(16,42,67,0.02), rgba(16,42,67,0.01));padding:10px;border-radius:10px;display:flex;justify-content:space-between;align-items:center}
    .saved small{color:var(--muted);font-size:12px}

    /* footer */
    footer{max-width:1100px;margin:24px auto 0;font-size:13px;color:var(--muted);text-align:center}

    /* small animations */
    .fade-in{animation:fadeIn .45s ease both}
    @keyframes fadeIn{from{opacity:0;transform:translateY(6px)} to{opacity:1;transform:none}}

    /* accessible focus */
    [tabindex]:focus, button:focus, input:focus, textarea:focus {outline:3px solid rgba(15,98,254,0.12);outline-offset:2px}

  </style>
</head>
<body>

  <div class="topbar fade-in" role="banner">
    <div class="brand" aria-label="SmartStudy brand">
      <div class="badge" aria-hidden="true">SS</div>
      <div>
        <div class="title">SmartStudy AI</div>
        <div style="font-size:12px;color:var(--muted)">Personalized Study Planner</div>
      </div>
    </div>

    <div class="top-actions" role="toolbar" aria-label="Top actions">
      <button class="icon-btn" id="themeToggle" title="Toggle theme (light/dark)" aria-pressed="false">
        <span class="material-icons">light_mode</span>
      </button>
      <button class="icon-btn" id="voiceBtn" title="Voice input for subjects" aria-pressed="false">
        <span class="material-icons">mic</span>
      </button>
      <button class="icon-btn" id="ttsBtn" title="Read plan aloud" aria-pressed="false">
        <span class="material-icons">volume_up</span>
      </button>
    </div>
  </div>

  <main class="layout" role="main">
    <!-- Main planner -->
    <section class="card fade-in" aria-labelledby="plannerTitle">
      <h1 id="plannerTitle">Create your personalized study plan</h1>
      <p class="lead">Enter your subjects (comma separated), how many hours per day you can study, and the difficulty level. SmartStudy AI will evenly allocate your time.</p>

      <label for="subjects">Subjects</label>
      <textarea id="subjects" placeholder="e.g., Math, Physics, English" aria-label="Subjects"></textarea>

      <div style="display:grid;grid-template-columns:1fr 160px;gap:12px;align-items:end;">
        <div>
          <label for="hours">Hours per day</label>
          <input id="hours" type="number" min="0.5" step="0.5" placeholder="e.g., 4" aria-label="Hours per day" />
        </div>
        <div>
          <label for="difficulty">Difficulty</label>
          <select id="difficulty" aria-label="Difficulty">
            <option value="easy">Easy</option>
            <option value="medium" selected>Medium</option>
            <option value="hard">Hard</option>
          </select>
        </div>
      </div>

      <div class="controls-row">
        <button class="btn primary" id="generateBtn" aria-pressed="false">
          <span class="material-icons">auto_awesome</span>
          Generate Plan
        </button>
        <button class="btn ghost" id="saveBtn" title="Save plan">Save</button>
      </div>

      <div id="output" class="output" role="status" aria-live="polite">Your plan will appear here after you generate it.</div>

      <div style="display:flex;gap:12px;margin-top:12px">
        <button class="btn ghost" id="clearBtn">Clear</button>
        <button class="btn ghost" id="downloadBtn">Download</button>
      </div>
    </section>

    <!-- Right panel: saved plans + about -->
    <aside class="panel card fade-in" aria-labelledby="savedTitle">
      <h3 id="savedTitle">Saved Plans</h3>
      <div id="savedList" class="saved-list" aria-live="polite"></div>

      <hr style="margin:14px 0;border:none;border-top:1px solid rgba(16,42,67,0.04)" />

      <h3>About</h3>
      <p style="margin:6px 0 0;color:var(--muted);font-size:13px">SmartStudy AI is a client-side educational tool to quickly create balanced study schedules. Saves plans locally in your browser.</p>
    </aside>
  </main>

  <footer>© <span id="year"></span> SmartStudy AI — Built for project submission • Works offline after loading</footer>

<script>
  // --- Utilities & UI hookup ---
  const subjectsEl = document.getElementById('subjects');
  const hoursEl = document.getElementById('hours');
  const difficultyEl = document.getElementById('difficulty');
  const generateBtn = document.getElementById('generateBtn');
  const saveBtn = document.getElementById('saveBtn');
  const clearBtn = document.getElementById('clearBtn');
  const downloadBtn = document.getElementById('downloadBtn');
  const outputEl = document.getElementById('output');
  const savedList = document.getElementById('savedList');
  const themeToggle = document.getElementById('themeToggle');
  const voiceBtn = document.getElementById('voiceBtn');
  const ttsBtn = document.getElementById('ttsBtn');

  // Accessibility: set current year
  document.getElementById('year').innerText = new Date().getFullYear();

  // Initial load from localStorage (auto-fill last input)
  subjectsEl.value = localStorage.getItem('ss_last_subjects') || '';
  hoursEl.value = localStorage.getItem('ss_last_hours') || '';
  difficultyEl.value = localStorage.getItem('ss_last_diff') || 'medium';

  // Save last inputs as user types (helps user)
  subjectsEl.addEventListener('input', ()=> localStorage.setItem('ss_last_subjects', subjectsEl.value));
  hoursEl.addEventListener('input', ()=> localStorage.setItem('ss_last_hours', hoursEl.value));
  difficultyEl.addEventListener('change', ()=> localStorage.setItem('ss_last_diff', difficultyEl.value));

  // Generate plan
  function generatePlan(){
    const raw = (subjectsEl.value || '').trim();
    const subjects = raw.split(',').map(s=>s.trim()).filter(Boolean);
    const hours = parseFloat(hoursEl.value);
    const difficulty = difficultyEl.value || 'medium';

    if (!subjects.length || !hours || hours <= 0) {
      outputEl.innerText = '⚠️ Please enter at least one subject and a positive number of hours.';
      return;
    }

    const multiplier = difficulty === 'easy' ? 0.85 : difficulty === 'hard' ? 1.2 : 1.0;
    const perSubject = (hours / subjects.length) * multiplier;

    let plan = 'Your Personalized Study Plan\n\n';
    subjects.forEach(s => plan += `• ${s}: ${perSubject.toFixed(1)} hours/day\n`);
    plan += `\n(Generated: ${new Date().toLocaleString()})`;

    outputEl.innerText = plan;
  }

  generateBtn.addEventListener('click', generatePlan);

  // Save plan to localStorage
  function savePlan(){
    const planText = outputEl.innerText || '';
    if (!planText || planText.startsWith('⚠️')) { alert('Generate a plan before saving.'); return; }
    const title = prompt('Name this plan:', 'My Study Plan');
    if (!title) return;
    const items = JSON.parse(localStorage.getItem('ss_saved') || '[]');
    items.push({id:Date.now(),title,plan:planText,created:Date.now()});
    localStorage.setItem('ss_saved', JSON.stringify(items));
    renderSaved();
  }
  saveBtn.addEventListener('click', savePlan);

  // Render saved plans
  function renderSaved(){
    const items = JSON.parse(localStorage.getItem('ss_saved') || '[]').slice().reverse();
    savedList.innerHTML = '';
    if (!items.length) {
      savedList.innerHTML = '<div style="color:var(--muted);font-size:13px">No saved plans — generate and save a plan.</div>';
      return;
    }
    items.forEach(it => {
      const el = document.createElement('div');
      el.className = 'saved';
      el.innerHTML = `<div>
                        <div style="font-weight:700">${escapeHtml(it.title)}</div>
                        <small>${new Date(it.created).toLocaleString()}</small>
                      </div>
                      <div style="display:flex;gap:8px">
                        <button class="btn ghost" data-id="${it.id}" data-action="load">Load</button>
                        <button class="btn ghost" data-id="${it.id}" data-action="delete">Delete</button>
                      </div>`;
      savedList.appendChild(el);
    });
  }

  // Delegated click
  savedList.addEventListener('click', (e) => {
    const b = e.target.closest('button');
    if (!b) return;
    const id = b.dataset.id;
    const action = b.dataset.action;
    const items = JSON.parse(localStorage.getItem('ss_saved') || '[]');
    const idx = items.findIndex(x => String(x.id) === String(id));
    if (action === 'load' && idx > -1) {
      outputEl.innerText = items[idx].plan;
      window.scrollTo({top:0,behavior:'smooth'});
    }
    if (action === 'delete' && idx > -1) {
      if (!confirm('Delete this saved plan?')) return;
      items.splice(idx,1);
      localStorage.setItem('ss_saved', JSON.stringify(items));
      renderSaved();
    }
  });

  // Clear inputs
  clearBtn.addEventListener('click', ()=> {
    subjectsEl.value=''; hoursEl.value=''; difficultyEl.value='medium'; outputEl.innerText='Your plan will appear here after you generate it.';
    localStorage.removeItem('ss_last_subjects'); localStorage.removeItem('ss_last_hours'); localStorage.removeItem('ss_last_diff');
  });

  // Download plan as text file
  downloadBtn.addEventListener('click', ()=> {
    const text = outputEl.innerText || '';
    if (!text || text.startsWith('⚠️')) { alert('Generate a plan to download it.'); return; }
    const blob = new Blob([text], {type:'text/plain'});
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a'); a.href = url; a.download = 'study-plan.txt'; a.click();
    URL.revokeObjectURL(url);
  });

  // Simple TTS read
  ttsBtn.addEventListener('click', ()=> {
    const text = outputEl.innerText || '';
    if (!text || text.startsWith('⚠️')) { alert('Generate a plan to read it aloud.'); return; }
    if (!('speechSynthesis' in window)) { alert('Text-to-speech not supported in this browser.'); return; }
    const ut = new SpeechSynthesisUtterance(text.replace(/\n/g,'. '));
    ut.lang = navigator.language || 'en-US';
    speechSynthesis.cancel(); speechSynthesis.speak(ut);
  });

  // Voice input (simple recognition) — works best in Chromium browsers
  let recognition = null;
  try {
    const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
    if (SR) {
      recognition = new SR();
      recognition.lang = navigator.language || 'en-US';
      recognition.interimResults = false;
      recognition.onresult = (e)=> {
        const transcript = Array.from(e.results).map(r=>r[0].transcript).join(' ');
        subjectsEl.value = subjectsEl.value ? subjectsEl.value + ', ' + transcript : transcript;
        localStorage.setItem('ss_last_subjects', subjectsEl.value);
      };
      recognition.onerror = ()=> alert('Voice input error or permission denied. You can type subjects manually.');
    }
  } catch(e){ recognition = null; }

  voiceBtn.addEventListener('click', ()=> {
    if (!recognition) { alert('Voice input is not supported in this browser. Use Chrome on desktop or Android for best results.'); return; }
    try {
      recognition.start();
    } catch(e){ /* ignore start error */ }
  });

  // Theme toggle (persist)
  const savedTheme = localStorage.getItem('ss_theme') || 'dark';
  setTheme(savedTheme);
  themeToggle.addEventListener('click', ()=> {
    const current = document.documentElement.getAttribute('data-theme') || 'dark';
    const next = current === 'dark' ? 'light' : 'dark';
    setTheme(next);
    localStorage.setItem('ss_theme', next);
  });
  function setTheme(t){
    if (t === 'light') document.documentElement.setAttribute('data-theme','light');
    else document.documentElement.removeAttribute('data-theme');
  }

  // Small keyboard shortcut: Ctrl/Cmd + G to generate
  document.addEventListener('keydown', (e)=> {
    if ((e.ctrlKey || e.metaKey) && e.key.toLowerCase() === 'g') { e.preventDefault(); generatePlan(); }
  });

  // render saved on load
  renderSaved();

  // make sure focusable for keyboard users
  generateBtn.setAttribute('tabindex', '0');
  saveBtn.setAttribute('tabindex', '0');

  // Helper
  function escapeHtml(s){ return String(s).replace(/[&<>"']/g,c=>({ '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }

  // Inform user if custom domain steps are pending (optional)
  // (You can remove this snippet; left for clarity)
  (function maybeShowDomainHint(){
    // no-op placeholder; keep for future guidance
  })();

</script>
</body>
</html>
