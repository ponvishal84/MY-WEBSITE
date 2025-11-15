# MY-WEBSITE<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>SmartStudy AI – Personalized Study Planner</title>
  <meta name="description" content="SmartStudy AI — create a personalized study plan. Responsive, mobile-friendly demo with dark mode and chat UI." />

  <!-- FAVICON (replace 'favicon.png' with your file in repo root) -->
  <link rel="icon" href="favicon.png" type="image/png" />

  <!-- GOOGLE FONT -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg: #eef1f7;
      --card: #ffffff;
      --text: #1f2a44;
      --muted: #667085;
      --accent: #4a6cf7;
      --accent-2: #6f86ff;
      --glass: rgba(255,255,255,0.6);
      --radius: 12px;
    }

    [data-theme="dark"]{
      --bg: #0f1724;
      --card: #0b1220;
      --text: #e6eef8;
      --muted: #a3b0c4;
      --accent: #7e9bff;
      --accent-2: #6b7bff;
      --glass: rgba(255,255,255,0.03);
    }

    *{box-sizing:border-box}
    html,body{height:100%;margin:0;font-family:"Inter",system-ui,Segoe UI,Roboto,Arial,sans-serif;background:var(--bg);color:var(--text);-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;}
    a{color:inherit;text-decoration:none}
    header.site-header{
      position:sticky;top:0;z-index:40;
      backdrop-filter: blur(6px);
      background: linear-gradient(180deg, rgba(255,255,255,0.4), rgba(255,255,255,0.15));
      border-bottom:1px solid rgba(0,0,0,0.04);
    }
    [data-theme="dark"] header.site-header{
      background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      border-bottom:1px solid rgba(255,255,255,0.03);
    }

    .nav-container{
      max-width:1100px;margin:0 auto;display:flex;align-items:center;justify-content:space-between;padding:12px 20px;
    }

    /* Logo */
    .logo{
      display:flex;align-items:center;gap:12px;
    }
    .logo svg{width:38px;height:38px;flex:0 0 38px;border-radius:8px;}
    .site-title{font-weight:700;font-size:18px;line-height:1;color:var(--text)}
    .site-sub{font-size:12px;color:var(--muted);margin-top:-2px}

    /* Nav */
    nav.primary{display:flex;gap:18px;align-items:center}
    nav.primary a{padding:8px 10px;border-radius:8px;font-weight:600;color:var(--muted);transition:0.18s}
    nav.primary a:hover{color:var(--accent);background:linear-gradient(90deg, rgba(74,108,247,0.06), rgba(111,134,255,0.03));}

    .cta-btn{background:linear-gradient(90deg,var(--accent),var(--accent-2));color:white;padding:8px 14px;border-radius:10px;font-weight:700;border:none;cursor:pointer}
    .icon-btn{background:transparent;border:1px solid rgba(0,0,0,0.06);padding:8px;border-radius:10px;cursor:pointer;}

    /* Mobile menu button */
    .menu-toggle{display:none;padding:8px;border-radius:8px;border:0;background:transparent}

    /* Hero */
    .hero{
      max-width:1100px;margin:34px auto 18px;padding:28px;display:grid;grid-template-columns:1fr 380px;gap:28px;align-items:start;
    }
    .card{
      background:var(--card);border-radius:var(--radius);padding:22px;box-shadow:0 6px 20px rgba(17,24,39,0.04); border:1px solid rgba(0,0,0,0.03);
    }
    [data-theme="dark"] .card{box-shadow:0 6px 18px rgba(2,6,23,0.6);border:1px solid rgba(255,255,255,0.03)}

    h1{margin:0;font-size:28px}
    p.lead{margin:12px 0 18px;color:var(--muted);font-weight:500}

    /* Form */
    label{display:block;font-weight:700;margin-bottom:6px;color:var(--text)}
    input, textarea, select{width:100%;padding:12px;border-radius:10px;border:1px solid rgba(16,24,40,0.06);font-size:15px;background:transparent;color:var(--text)}
    input:focus,textarea:focus,select:focus{outline:none;box-shadow:0 6px 20px rgba(74,108,247,0.12);border-color:var(--accent)}
    textarea{min-height:84px;resize:vertical}
    .btn-primary{display:inline-block;background:linear-gradient(90deg,var(--accent),var(--accent-2));color:white;padding:12px 16px;border-radius:10px;border:0;font-weight:700;cursor:pointer}
    .muted{color:var(--muted);font-size:13px}

    /* Output */
    .output{
      margin-top:16px;padding:14px;border-radius:10px;background:linear-gradient(180deg, rgba(74,108,247,0.06), rgba(111,134,255,0.03));
      white-space:pre-line;font-weight:600;border:1px solid rgba(74,108,247,0.08);
    }

    /* Cards list */
    .cards{display:grid;grid-template-columns:repeat(2,1fr);gap:14px}
    .project-card{padding:14px;border-radius:10px;background:linear-gradient(180deg, rgba(0,0,0,0.01), rgba(0,0,0,0.02));border:1px solid rgba(0,0,0,0.03);}

    /* Footer */
    footer{max-width:1100px;margin:34px auto;padding:18px 22px;color:var(--muted);display:flex;justify-content:space-between;align-items:center}
    .socials a{margin-left:12px;color:var(--muted);font-weight:700}

    /* Floating Chat */
    .chat-float{
      position:fixed;right:18px;bottom:18px;z-index:60;
      width:340px;max-width:calc(100% - 36px);border-radius:14px;overflow:hidden;
      box-shadow:0 20px 40px rgba(2,6,23,0.2);
    }
    .chat-header{display:flex;align-items:center;gap:10px;padding:12px 14px;background:linear-gradient(90deg,var(--accent),var(--accent-2));color:white}
    .chat-body{background:var(--card);padding:12px;height:220px;overflow:auto}
    .chat-input{display:flex;gap:8px;padding:12px;background:var(--card);border-top:1px solid rgba(0,0,0,0.04)}
    .chat-input input{flex:1;padding:10px;border-radius:10px;border:1px solid rgba(0,0,0,0.06)}
    .chat-mini{display:none}

    /* Animations */
    .animate-fade{animation:fadeInUp .6s ease both}
    @keyframes fadeInUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}

    /* Responsive */
    @media (max-width:980px){
      .hero{grid-template-columns:1fr 320px}
      .cards{grid-template-columns:1fr}
    }
    @media (max-width:760px){
      nav.primary{display:none}
      .menu-toggle{display:block}
      .hero{grid-template-columns:1fr;gap:16px;padding:18px;margin:18px auto}
      .chat-float{right:12px;left:12px;width:auto}
      .chat-mini{display:block;position:fixed;right:18px;bottom:18px;z-index:70}
      .chat-float{display:none}
    }

    /* Mobile slide menu */
    .mobile-menu{
      display:none;position:fixed;left:0;top:0;width:100%;height:100%;background:rgba(2,6,23,0.45);z-index:80;
    }
    .mobile-menu .panel{background:var(--card);width:280px;height:100%;padding:20px}
    .mobile-menu a{display:block;padding:12px 8px;border-radius:8px;margin-bottom:8px;color:var(--text)}
    .mobile-menu .close{margin-bottom:10px}

    /* small touches */
    .muted-small{font-size:13px;color:var(--muted)}
  </style>
</head>

<body>
  <!-- Add data-theme="dark" to body to toggle dark mode -->
  <script>
    // Initialize theme from localStorage or system preference
    (function(){
      const saved = localStorage.getItem('theme');
      const prefersDark = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;
      const theme = saved || (prefersDark ? 'dark' : 'light');
      if(theme === 'dark') document.documentElement.setAttribute('data-theme','dark');
      else document.documentElement.removeAttribute('data-theme');
    })();
  </script>

  <header class="site-header">
    <div class="nav-container">
      <div style="display:flex;align-items:center;gap:12px">
        <div class="logo">
          <!-- Inline SVG logo: replace path or the whole SVG with your logo file if you prefer -->
          <svg viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="SmartStudy logo">
            <defs>
              <linearGradient id="g" x1="0" x2="1">
                <stop offset="0" stop-color="#4a6cf7"/>
                <stop offset="1" stop-color="#6f86ff"/>
              </linearGradient>
            </defs>
            <rect width="64" height="64" rx="12" fill="url(#g)"/>
            <path d="M20 42c6-8 12-8 18 0" fill="none" stroke="#fff" stroke-width="3" stroke-linecap="round"/>
            <circle cx="32" cy="24" r="7" fill="rgba(255,255,255,0.12)"/>
          </svg>

          <div>
            <div class="site-title">SmartStudy AI</div>
            <div class="site-sub">Personalized Study Planner</div>
          </div>
        </div>
      </div>

      <nav class="primary" aria-label="Primary navigation">
        <a href="#home">Home</a>
        <a href="#projects">Projects</a>
        <a href="#about">About</a>
        <a href="#contact">Contact</a>
        <button class="cta-btn" onclick="scrollToSection('contact')">Get Plan</button>
      </nav>

      <div style="display:flex;align-items:center;gap:8px">
        <button title="Toggle dark mode" id="themeToggle" class="icon-btn" onclick="toggleTheme()">🌓</button>
        <button class="menu-toggle" aria-label="Open menu" onclick="openMobileMenu()">☰</button>
      </div>
    </div>
  </header>

  <!-- Mobile menu -->
  <div id="mobileMenu" class="mobile-menu" style="display:none" onclick="closeMobileMenu()">
    <div class="panel" onclick="event.stopPropagation()">
      <button class="close" onclick="closeMobileMenu()">Close ✕</button>
      <a href="#home" onclick="closeMobileMenu()">Home</a>
      <a href="#projects" onclick="closeMobileMenu()">Projects</a>
      <a href="#about" onclick="closeMobileMenu()">About</a>
      <a href="#contact" onclick="closeMobileMenu()">Contact</a>
      <hr/>
      <div style="margin-top:12px">
        <button class="cta-btn" style="width:100%" onclick="scrollToSection('contact'); closeMobileMenu()">Get Plan</button>
      </div>
    </div>
  </div>

  <!-- HERO / MAIN -->
  <main id="home" class="hero" role="main">
    <section class="card animate-fade" aria-labelledby="heroTitle">
      <h1 id="heroTitle">SmartStudy AI — Create a Personalized Study Plan</h1>
      <p class="lead">Enter your subjects, choose available hours and difficulty. SmartStudy AI helps you split your time with a clear daily plan.</p>

      <!-- Form -->
      <div style="margin-top:10px">
        <label for="subjects">Subjects (comma separated)</label>
        <textarea id="subjects" placeholder="Example: Math, Physics, English"></textarea>

        <div style="display:grid;grid-template-columns:1fr 140px;gap:12px;">
          <div>
            <label for="hours">Hours per day</label>
            <input id="hours" type="number" min="0" step="0.5" placeholder="4" />
          </div>
          <div>
            <label for="difficulty">Difficulty</label>
            <select id="difficulty">
              <option value="easy">Easy</option>
              <option value="medium" selected>Medium</option>
              <option value="hard">Hard</option>
            </select>
          </div>
        </div>

        <div style="display:flex;gap:10px;margin-top:10px;align-items:center">
          <button class="btn-primary" onclick="generatePlan()">Generate Plan</button>
          <button class="icon-btn" title="Clear fields" onclick="clearForm()">⟲</button>
          <div class="muted-small" style="margin-left:auto">Tip: use commas to separate multiple subjects</div>
        </div>

        <div id="output" class="output muted" aria-live="polite" style="min-height:48px;margin-top:12px">Your plan will appear here...</div>
      </div>
    </section>

    <!-- Right column: Projects / Quick tips -->
    <aside>
      <div class="card animate-fade" style="margin-bottom:14px">
        <h3 style="margin:0 0 8px">Quick Tips</h3>
        <ul class="muted" style="margin:0;padding-left:18px">
          <li>Break sessions into 25–50 min blocks</li>
          <li>Prioritize harder subjects earlier</li>
          <li>Review older material weekly</li>
        </ul>
      </div>

      <div class="card animate-fade">
        <h3 style="margin:0 0 8px">Saved Plans</h3>
        <p class="muted">You can implement localStorage saving later. This demo keeps it simple.</p>
        <div style="display:flex;gap:8px;margin-top:10px">
          <button class="icon-btn">Load</button>
          <button class="icon-btn">Save</button>
        </div>
      </div>
    </aside>
  </main>

  <!-- Projects Section -->
  <section id="projects" style="max-width:1100px;margin:8px auto;padding:18px">
    <div class="card animate-fade">
      <h2 style="margin-top:0">Projects & Examples</h2>
      <p class="muted">Example study plans generated from this tool.</p>

      <div class="cards" style="margin-top:12px">
        <div class="project-card">
          <strong>Exam Prep — 6 hours/day</strong>
          <p class="muted">Math • Physics • Chemistry</p>
          <p style="margin:8px 0 0">Suggested: Math 2.0 hrs / Physics 2.0 hrs / Chemistry 2.0 hrs</p>
        </div>

        <div class="project-card">
          <strong>Weekly Revision — 3 hours/day</strong>
          <p class="muted">English • Biology</p>
          <p style="margin:8px 0 0">Suggested: English 1.5 hrs / Biology 1.5 hrs</p>
        </div>
      </div>
    </div>
  </section>

  <!-- About -->
  <section id="about" style="max-width:1100px;margin:8px auto;padding:18px">
    <div class="card animate-fade">
      <h2 style="margin-top:0">About SmartStudy AI</h2>
      <p class="muted">SmartStudy AI is a simple demo to help students plan study time. This page demonstrates UI features — dark mode, animations, responsive layout, and a chat-like interface that you can later connect to an AI backend.</p>
      <p class="muted">Want help wiring this to a real AI (OpenAI / local model)? I can provide the code to connect the chatbox and generate plans server-side.</p>
    </div>
  </section>

  <!-- Contact -->
  <section id="contact" style="max-width:1100px;margin:8px auto;padding:18px 18px 72px">
    <div class="card animate-fade">
      <h2 style="margin-top:0">Contact / Get Help</h2>
      <p class="muted">Want customization, custom domain setup, or AI connection? Send a message below.</p>

      <div style="display:grid;grid-template-columns:1fr 320px;gap:18px">
        <div>
          <label for="name">Your name</label>
          <input id="name" placeholder="Your name" />

          <label for="email">Email</label>
          <input id="email" placeholder="you@example.com" />

          <label for="message">Message</label>
          <textarea id="message" placeholder="I want help integrating AI..."></textarea>

          <div style="margin-top:12px;display:flex;gap:10px">
            <button class="btn-primary" onclick="sendContact()">Send Message</button>
            <div class="muted-small" style="align-self:center">We'll reply to your email.</div>
          </div>
        </div>

        <aside class="card" style="height:100%;">
          <h3 style="margin-top:0">Need a custom plan?</h3>
          <p class="muted">If you'd like I can connect this UI to an AI engine to make smarter, adaptive study plans — e.g., spaced repetition, past-performance weighting, and calendar exports.</p>
        </aside>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <div class="muted-small">© <span id="year"></span> SmartStudy AI — Built by you</div>
    <div class="socials">
      <!-- Replace with your real links -->
      <a href="https://github.com/ponvishal84" target="_blank" rel="noreferrer">GitHub</a>
      <a href="https://www.linkedin.com/" target="_blank" rel="noreferrer">LinkedIn</a>
      <a href="mailto:you@example.com">Email</a>
    </div>
  </footer>

  <!-- FLOATING CHAT (desktop) -->
  <div class="chat-float" id="chatFloat" role="dialog" aria-label="Chat">
    <div class="chat-header">
      <div style="display:flex;align-items:center;gap:10px">
        <div style="width:36px;height:36px;border-radius:8px;background:rgba(255,255,255,0.12);display:flex;align-items:center;justify-content:center;font-weight:700">AI</div>
        <div>
          <div style="font-weight:700">SmartStudy Chat</div>
          <div style="font-size:12px;opacity:0.9">Ask for study tips or generate a plan</div>
        </div>
      </div>
      <div style="margin-left:auto">
        <button onclick="toggleChat()" class="icon-btn" title="Minimize chat">━</button>
      </div>
    </div>
    <div class="chat-body" id="chatBody">
      <div class="muted" style="font-size:13px">This is a UI demo. To make it functional, wire `sendChat()` to your AI backend (OpenAI, etc.).</div>
      <div id="chatMessages" style="margin-top:10px"></div>
    </div>

    <div class="chat-input">
      <input id="chatInput" placeholder="Ask: e.g., 'Make a 2-hour math plan'" onkeydown="if(event.key==='Enter') sendChat()"/>
      <button class="cta-btn" onclick="sendChat()">Send</button>
    </div>
  </div>

  <!-- mini chat button for mobile -->
  <button class="chat-mini cta-btn" id="chatMini" onclick="openMiniChat()" style="display:none">Chat</button>

  <script>
    // Small helpers
    document.getElementById('year').innerText = new Date().getFullYear();

    function scrollToSection(id){
      document.getElementById(id).scrollIntoView({behavior:'smooth',block:'start'});
    }

    // Theme toggle
    function toggleTheme(){
      const isDark = document.documentElement.getAttribute('data-theme') === 'dark';
      if(isDark){
        document.documentElement.removeAttribute('data-theme');
        localStorage.setItem('theme','light');
      } else {
        document.documentElement.setAttribute('data-theme','dark');
        localStorage.setItem('theme','dark');
      }
    }

    // Mobile menu
    function openMobileMenu(){document.getElementById('mobileMenu').style.display='block'}
    function closeMobileMenu(){document.getElementById('mobileMenu').style.display='none'}

    // Chat window behavior
    let chatOpen = true;
    function toggleChat(){
      const el = document.getElementById('chatFloat');
      chatOpen = !chatOpen;
      el.style.display = chatOpen ? 'block' : 'none';
      document.getElementById('chatMini').style.display = chatOpen ? 'none' : 'block';
    }
    function openMiniChat(){ document.getElementById('chatFloat').style.display='block'; document.getElementById('chatMini').style.display='none'; chatOpen=true; }

    // Clear form
    function clearForm(){
      document.getElementById('subjects').value='';
      document.getElementById('hours').value='';
      document.getElementById('difficulty').value='medium';
      document.getElementById('output').innerText='Your plan will appear here...';
    }

    // Main plan generator (improved)
    function generatePlan(){
      const raw = document.getElementById('subjects').value;
      const subjects = raw.split(',').map(s=>s.trim()).filter(Boolean);
      const hours = parseFloat(document.getElementById('hours').value);
      const difficulty = document.getElementById('difficulty').value;

      if(subjects.length === 0 || !hours || hours <= 0){
        document.getElementById('output').innerText = "⚠️ Please enter at least one subject and a valid number of hours.";
        return;
      }

      const difficultyMultiplier = (difficulty === 'easy') ? 0.85 : (difficulty === 'medium') ? 1.0 : 1.2;
      const base = (hours / subjects.length) * difficultyMultiplier;

      // small weighting — give slightly more time to first subjects (example)
      let planText = `📌 Personalized Study Plan — ${hours} hr/day — ${difficulty}\n\n`;
      subjects.forEach((sub, idx)=>{
        // weight: first subject +10% per position up to 20%
        const weight = 1 + Math.max(0, 0.08 * Math.max(0, (subjects.length - idx - 1)));
        const t = base * weight;
        planText += `• ${sub}: ${t.toFixed(1)} hours/day\n`;
      });

      document.getElementById('output').innerText = planText;
      // Optionally show animated toast or save to localStorage...
    }

    // Contact send (UI only)
    function sendContact(){
      const name = document.getElementById('name').value || 'Anonymous';
      const email = document.getElementById('email').value || '';
      const message = document.getElementById('message').value || '';
      alert(`Thanks ${name}! (This demo doesn't send email). You wrote: "${message.slice(0,120)}" — add backend to submit.`);
    }

    // Chat UI handlers (UI only)
    function sendChat(){
      const input = document.getElementById('chatInput');
      const msg = input.value.trim();
      if(!msg) return;
      appendChat('You', msg);
      input.value = '';

      // Simulated AI response (replace with fetch to your backend)
      appendChat('AI', 'Thinking...');
      setTimeout(()=>{
        // replace with real suggestion logic
        const aiResp = generateSimpleResponse(msg);
        // replace last AI 'Thinking...' with real content
        const chatMessages = document.getElementById('chatMessages');
        // remove the last AI 'Thinking...' node
        const nodes = chatMessages.querySelectorAll('.msg');
        if(nodes.length){
          for(let i=nodes.length-1;i>=0;i--){
            if(nodes[i].dataset.sender === 'AI' && nodes[i].dataset.status==='pending'){
              nodes[i].querySelector('.bubble').innerText = aiResp;
              nodes[i].dataset.status = 'done';
              break;
            }
          }
        } else {
          appendChat('AI', aiResp);
        }
      }, 800);
    }

    function appendChat(sender, text){
      const chatMessages = document.getElementById('chatMessages');
      const div = document.createElement('div');
      div.className = 'msg';
      div.dataset.sender = sender;
      div.dataset.status = (sender==='AI' ? 'pending' : 'done');
      div.style.marginBottom = '8px';
      div.innerHTML = `<div style="font-size:12px;color:var(--muted);margin-bottom:4px">${sender}</div><div class="bubble" style="padding:8px 10px;border-radius:8px;background:${sender==='AI' ? 'linear-gradient(90deg,var(--accent),var(--accent-2))' : 'var(--card)'};color:${sender==='AI' ? '#fff' : 'var(--text)'};max-width:85%">${text}</div>`;
      chatMessages.appendChild(div);
      chatMessages.scrollTop = chatMessages.scrollHeight;
    }

    function generateSimpleResponse(msg){
      // VERY simple canned responses for demo. Replace with AI call.
      msg = msg.toLowerCase();
      if(msg.includes('plan') || msg.includes('study')){
        return "Try splitting time equally, prioritize harder subjects earlier. Example: start with 45–60 min focused sessions, then quick reviews.";
      } else if(msg.includes('math')){
        return "Math tip: practice problems for 50 mins, then 10 mins review. Use spaced repetition for formulas.";
      } else if(msg.includes('hours')){
        return "Tell me how many hours per day you have and your subjects, I'll suggest a split.";
      } else {
        return "Nice question — connect this UI to an AI backend (OpenAI/others). I can provide that code if you'd like.";
      }
    }

    // Accessibility: enable keyboard escape to close mobile menu
    document.addEventListener('keydown', e=>{ if(e.key==='Escape') closeMobileMenu(); });
  </script>
</body>
</html>
