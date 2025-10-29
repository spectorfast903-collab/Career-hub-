<!doctype html>
<html lang="en" class="antialiased">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>CareerHub Ultra — Prototype</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap" rel="stylesheet">
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--glass:rgba(255,255,255,0.06);}
    .light :root{--bg:#f8fafc;--card:#ffffff;--glass:rgba(15,23,42,0.03);} 
    html{font-family:Inter,ui-sans-serif,system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial}
    /* cinematic background animation */
    .hero-gradient{
      background: radial-gradient(800px 400px at 10% 10%, rgba(99,102,241,0.12), transparent 10%),
                  radial-gradient(600px 300px at 90% 90%, rgba(139,92,246,0.10), transparent 10%);
      transition: background 600ms ease;
    }
    .glass {backdrop-filter: blur(6px); background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));}

    /* animated job cards entrance */
    .card-enter{opacity:0; transform: translateY(10px) scale(0.98);} 
    .card-enter.card-show{opacity:1; transform:none; transition: transform 420ms cubic-bezier(.2,.9,.3,1), opacity 420ms}

    /* flip effect */
    .flip-card{perspective:1200px}
    .flip-inner{transition: transform 650ms cubic-bezier(.2,.9,.3,1); transform-style:preserve-3d}
    .flip-inner.flipped{transform: rotateY(180deg)}
    .flip-front, .flip-back{backface-visibility:hidden; position:relative}
    .flip-back{transform:rotateY(180deg); position:absolute; left:0; top:0; width:100%}

    /* scan animation */
    .scanner{position:relative; overflow:hidden}
    .scanner::after{content:''; position:absolute; left:-60%; top:0; width:60%; height:100%; background:linear-gradient(90deg, transparent, rgba(99,102,241,0.14), transparent); transform:skewX(-12deg); animation:scan 2.6s linear infinite}
    @keyframes scan{0%{left:-60%}100%{left:160%}}

    /* progress ring */
    .progress-svg{transform:rotate(-90deg)}

    /* subtle floating */
    .floaty{animation:floaty 6s ease-in-out infinite}
    @keyframes floaty{0%{transform:translateY(0)}50%{transform:translateY(-6px)}100%{transform:translateY(0)}}

    /* dark/light helpers */
    .light .dark-only{display:none}
    .dark .light-only{display:none}

  </style>
</head>
<body class="min-h-screen bg-gradient-to-b from-gray-50 to-white light hero-gradient dark:bg-gradient-to-b dark:from-[#071020] dark:to-[#041025] dark text-slate-100">
  <div class="max-w-6xl mx-auto p-6">
    <!-- Nav -->
    <nav class="flex items-center justify-between mb-6">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-indigo-500 to-violet-500 flex items-center justify-center text-white font-extrabold">CH</div>
        <div>
          <div class="text-lg font-semibold">CareerHub</div>
          <div class="text-xs text-slate-400 light-only dark:text-slate-300">Ultra Prototype</div>
        </div>
      </div>

      <div class="flex items-center gap-3">
        <button id="themeToggle" class="px-3 py-2 rounded-md glass border border-transparent hover:scale-105 transition">Toggle Dark</button>
        <button id="studentBtn" class="px-3 py-2 rounded-md bg-indigo-600 hover:bg-indigo-700">For Students</button>
        <button id="recruiterBtn" class="px-3 py-2 rounded-md bg-white text-indigo-600 dark:bg-transparent dark:border dark:border-slate-700 dark:text-slate-200">For Recruiters</button>
      </div>
    </nav>

    <!-- Hero -->
    <header class="grid grid-cols-1 md:grid-cols-3 gap-6 items-center mb-8">
      <div class="md:col-span-2">
        <h1 class="text-4xl md:text-5xl font-extrabold leading-tight mb-4">Empowering Your Career <span class="text-transparent bg-clip-text bg-gradient-to-r from-indigo-400 to-violet-400">through intelligent AI</span></h1>
        <p class="text-slate-400 mb-6 max-w-xl">Resume insights, semantic job matching, and recruiter tools — fast, beautiful, and built for outcomes. This prototype focuses on the cinematic experience and front-end interactions; AI hookups are ready-to-plug.</p>
        <div class="flex gap-3">
          <a href="#dashboard" class="px-5 py-3 rounded-lg bg-indigo-600 hover:bg-indigo-700 shadow-lg">Explore Dashboard</a>
          <a href="#features" class="px-5 py-3 rounded-lg border border-slate-200 dark:border-slate-700">Learn More</a>
        </div>
      </div>

      <div class="glass rounded-2xl p-4 shadow-2xl relative overflow-hidden floaty hidden md:block" style="min-height:220px;">
        <div class="absolute inset-0 -z-10 opacity-30" style="background:linear-gradient(90deg, rgba(99,102,241,0.12), rgba(139,92,246,0.08)); filter: blur(40px)"></div>
        <div class="flex flex-col gap-4">
          <div class="flex items-center justify-between">
            <div>
              <div class="text-xs text-slate-300">Resume Score</div>
              <div class="text-2xl font-semibold">78 <span class="text-sm text-slate-400">/100</span></div>
            </div>
            <div class="w-20 h-20">
              <!-- progress ring -->
              <svg class="progress-svg" width="80" height="80" viewBox="0 0 36 36">
                <defs>
                  <linearGradient id="g1" x1="0%" y1="0%" x2="100%" y2="0%">
                    <stop offset="0%" stop-color="#6366f1" />
                    <stop offset="100%" stop-color="#8b5cf6" />
                  </linearGradient>
                </defs>
                <g fill="none" stroke-linecap="round">
                  <path d="M18 2.0845a15.9155 15.9155 0 1 1 0 31.831" stroke="rgba(255,255,255,0.06)" stroke-width="3"></path>
                  <path id="p1" d="M18 2.0845a15.9155 15.9155 0 1 1 0 31.831" stroke="url(#g1)" stroke-width="3" stroke-dasharray="78,100"></path>
                </g>
              </svg>
            </div>
          </div>
          <div class="text-xs text-slate-300">Top suggestions</div>
          <ul class="text-sm text-slate-200 list-disc ml-5">
            <li>Highlight 1–2 projects with metrics</li>
            <li>Add GitHub / portfolio links</li>
            <li>Use clear skill sections for ATS parsing</li>
          </ul>
        </div>
      </div>
    </header>

    <!-- Dashboard -->
    <section id="dashboard" class="grid grid-cols-1 lg:grid-cols-3 gap-6">
      <!-- Left: Job feed -->
      <div class="lg:col-span-2">
        <div class="flex items-center justify-between mb-4">
          <h2 class="text-xl font-semibold">Recommended Jobs</h2>
          <div class="flex items-center gap-2">
            <input id="search" placeholder="Search jobs, skills, company" class="px-3 py-2 rounded-lg border bg-transparent w-72" />
            <select id="loc" class="px-3 py-2 rounded-lg border bg-transparent">
              <option value="any">Any location</option>
              <option>Remote</option>
              <option>Bengaluru</option>
              <option>New York</option>
            </select>
          </div>
        </div>

        <div id="jobsGrid" class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <!-- cards go here -->
        </div>
      </div>

      <!-- Right: Resume analyzer + career coach -->
      <aside class="glass rounded-2xl p-4 shadow-lg">
        <div class="flex items-center justify-between mb-3">
          <h3 class="font-semibold">AI Resume Analyzer</h3>
          <div class="text-xs text-slate-400">Prototype</div>
        </div>

        <div class="scanner rounded-lg p-3 bg-white/5 dark:bg-white/2">
          <input id="resumeFile" type="file" accept=".pdf,.txt,.doc,.docx" class="block w-full mb-3 text-sm" />
          <div class="flex items-center gap-3">
            <button id="analyze" class="px-3 py-2 rounded-md bg-indigo-600 hover:bg-indigo-700">Analyze</button>
            <div id="scanProgress" class="flex items-center gap-2 text-sm text-slate-300"> <svg width="18" height="18" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10" stroke="rgba(255,255,255,0.08)" stroke-width="2" fill="none"></circle></svg> <span>Ready to scan</span></div>
          </div>

          <div id="analysisCard" class="mt-4 hidden bg-white/3 rounded-lg p-3">
            <div class="flex items-center justify-between">
              <div>
                <div class="text-xs text-slate-300">Overall Score</div>
                <div id="scoreLarge" class="text-3xl font-bold">--</div>
              </div>
              <div id="miniSuggestions" class="text-sm text-slate-200 text-right"></div>
            </div>
            <div class="mt-3">
              <div class="text-xs text-slate-400 mb-1">ATS compatibility</div>
              <div class="w-full bg-slate-800/40 rounded-full h-2 overflow-hidden">
                <div id="atsBar" class="h-2 rounded-full" style="width:0%; background:linear-gradient(90deg,#6366f1,#8b5cf6)"></div>
              </div>
            </div>
          </div>
        </div>

        <hr class="my-4 border-slate-700/40" />

        <div>
          <h4 class="font-semibold mb-2">Career Coach</h4>
          <div class="text-sm text-slate-300 mb-2">Ask quick career questions (AI-ready chat UI placeholder):</div>
          <input id="coachQ" placeholder="How do I break into data science?" class="w-full px-3 py-2 rounded-lg border bg-transparent mb-2" />
          <button id="askCoach" class="w-full px-3 py-2 rounded-md border border-indigo-600">Ask</button>
          <div id="coachResp" class="mt-3 text-sm text-slate-200"></div>
        </div>
      </aside>
    </section>

    <!-- Recruiter modal (hidden) -->
    <div id="recruiterModal" class="fixed inset-0 z-40 hidden items-center justify-center bg-black/40">
      <div class="w-full max-w-2xl p-6 bg-white dark:bg-[#071021] rounded-2xl glass shadow-2xl">
        <div class="flex items-center justify-between mb-4">
          <h3 class="font-semibold">Post a Job</h3>
          <button id="closeRecruiter" class="px-2 py-1 rounded-md">Close</button>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
          <input id="jobTitle" placeholder="Job title" class="px-3 py-2 rounded-lg border bg-transparent" />
          <input id="jobCompany" placeholder="Company" class="px-3 py-2 rounded-lg border bg-transparent" />
          <input id="jobLoc" placeholder="Location" class="px-3 py-2 rounded-lg border bg-transparent" />
          <input id="jobSkills" placeholder="Skills (comma separated)" class="px-3 py-2 rounded-lg border bg-transparent" />
        </div>
        <textarea id="jobDesc" placeholder="Short description" class="w-full mt-3 px-3 py-2 rounded-lg border bg-transparent"></textarea>
        <div class="mt-4 flex justify-end gap-2">
          <button id="postJob" class="px-4 py-2 rounded-md bg-green-600">Post</button>
        </div>
      </div>
    </div>

    <footer class="text-center text-xs text-slate-400 mt-8">Prototype — Front-end cinematic experience. Backend & AI integrations are next.</footer>

    <!-- Hidden: Image prompts & shot descriptions for demo video -->
    <template id="imagePrompts">
      <!--
      1) Hero shot: "Wide frame: a glass-like dashboard on a laptop; soft indigo-violet gradient in background; subtle particle glow; camera dolly-in to the Resume Score card."
      2) Resume upload: "Close-up on hand dragging a PDF onto an upload area; neon-blue scanning line passes; split-screen shows live score animating up."
      3) Job reveal: "Over-the-shoulder screen recording: search typed -> cards stagger in with flip animation; each card shows match % in a circular meter."
      4) Recruiter analytics: "Smooth pan across charts as bars draw from left; numbers count up; voiceover: 'Find top talent faster.'" 
      5) Outro: "Slow zoom out from dashboard; CareerHub logo fades; tagline 'Built for the Future of Work' types in." 
      -->
    </template>

  </div>

  <script>
    // state
    let dark = true;
    document.documentElement.classList.add('dark');

    const sampleJobs = [
      {id:1, title:'Frontend Engineer (Intern)', company:'BrightTech', loc:'Remote', skills:['react','javascript'], score:82, desc:'Build polished UI components and prototypes.'},
      {id:2, title:'Data Science Intern', company:'Insight Labs', loc:'Bengaluru', skills:['python','ml'], score:76, desc:'Work on models and real datasets.'},
      {id:3, title:'Backend Engineer', company:'ScaleX', loc:'New York', skills:['node','sql'], score:69, desc:'Design scalable APIs and systems.'},
      {id:4, title:'Product Designer', company:'Morph Studio', loc:'Remote', skills:['figma','ux'], score:71, desc:'Design delightful user experiences.'}
    ];

    const jobsGrid = document.getElementById('jobsGrid');
    const search = document.getElementById('search');
    const loc = document.getElementById('loc');

    function createJobCard(j){
      const wrapper = document.createElement('div');
      wrapper.className = 'card-enter';
      wrapper.innerHTML = `
        <div class="flip-card bg-white/5 dark:bg-white/2 rounded-xl p-4 shadow-lg relative overflow-hidden" style="min-height:140px">
          <div class="flip-inner" data-id="${j.id}">
            <div class="flip-front">
              <div class="flex items-start justify-between">
                <div>
                  <div class="text-sm text-slate-300">${j.company} • ${j.loc}</div>
                  <div class="text-lg font-semibold">${j.title}</div>
                </div>
                <div class="text-right">
                  <div class="text-xs text-slate-400">Match</div>
                  <div class="text-2xl font-bold">${j.score}%</div>
                </div>
              </div>
              <p class="mt-3 text-sm text-slate-300">${j.desc}</p>
            </div>
            <div class="flip-back p-2 bg-gradient-to-r from-indigo-600 to-violet-600 rounded-xl text-white">
              <div class="text-sm">Top matched skills</div>
              <div class="mt-2 font-semibold">${j.skills.join(', ')}</div>
              <div class="mt-3 flex gap-2">
                <button class="applyBtn px-3 py-1 rounded bg-white text-indigo-700">Apply</button>
                <button class="viewBtn px-3 py-1 rounded border border-white/30">View</button>
              </div>
            </div>
          </div>
        </div>
      `;

      // flip interaction on hover
      wrapper.querySelector('.flip-card').addEventListener('mouseenter', () => {
        wrapper.querySelector('.flip-inner').classList.add('flipped');
      });
      wrapper.querySelector('.flip-card').addEventListener('mouseleave', () => {
        wrapper.querySelector('.flip-inner').classList.remove('flipped');
      });

      return wrapper;
    }

    function renderJobs(){
      jobsGrid.innerHTML = '';
      const q = search.value.toLowerCase();
      const l = loc.value;
      const filtered = sampleJobs.filter(j => ( (q==='' || (j.title + ' ' + j.company + ' ' + j.skills.join(' ')).toLowerCase().includes(q)) && (l==='any' || j.loc===l) ));
      filtered.forEach((j, i) => {
        const card = createJobCard(j);
        jobsGrid.appendChild(card);
        // staggered entrance
        setTimeout(()=>{ card.classList.add('card-show'); }, 80 * i);
      });
    }
    search.addEventListener('input', renderJobs);
    loc.addEventListener('change', renderJobs);
    document.addEventListener('DOMContentLoaded', renderJobs);

    // Theme toggle
    const themeToggle = document.getElementById('themeToggle');
    themeToggle.addEventListener('click', () => {
      dark = !dark;
      document.documentElement.classList.toggle('dark', dark);
      document.body.classList.toggle('light', !dark);
      themeToggle.textContent = dark ? 'Dark mode' : 'Light mode';
    });

    // Recruiter modal
    document.getElementById('recruiterBtn').addEventListener('click', ()=>{
      document.getElementById('recruiterModal').classList.remove('hidden');
      document.getElementById('recruiterModal').classList.add('flex');
    });
    document.getElementById('closeRecruiter').addEventListener('click', ()=>{
      document.getElementById('recruiterModal').classList.add('hidden');
      document.getElementById('recruiterModal').classList.remove('flex');
    });
    document.getElementById('postJob').addEventListener('click', ()=>{
      const title = document.getElementById('jobTitle').value || 'Untitled Role';
      const company = document.getElementById('jobCompany').value || 'Company';
      const l = document.getElementById('jobLoc').value || 'Remote';
      const skills = (document.getElementById('jobSkills').value || '').split(',').map(s=>s.trim()).filter(Boolean);
      const desc = document.getElementById('jobDesc').value || '';
      const newJob = {id:sampleJobs.length+1, title, company, loc: l, skills, score: Math.floor(60 + Math.random()*30), desc};
      sampleJobs.unshift(newJob);
      renderJobs();
      document.getElementById('recruiterModal').classList.add('hidden');
      document.getElementById('recruiterModal').classList.remove('flex');
    });

    // Simple resume analyzer prototype
    document.getElementById('analyze').addEventListener('click', ()=>{
      const file = document.getElementById('resumeFile').files[0];
      const analysisCard = document.getElementById('analysisCard');
      const scoreLarge = document.getElementById('scoreLarge');
      const atsBar = document.getElementById('atsBar');
      const miniSuggestions = document.getElementById('miniSuggestions');
      const scanProgress = document.getElementById('scanProgress');

      if(!file){ alert('Please choose a resume file first (PDF/TXT).'); return; }
      scanProgress.querySelector('span').textContent = 'Scanning...';
      scanProgress.classList.add('text-indigo-300');

      // fake async animation (client-only demo)
      let progress = 0;
      const interval = setInterval(()=>{
        progress += Math.floor(8 + Math.random()*18);
        if(progress >= 100) progress = 100;
        atsBar.style.width = (40 + Math.floor(progress*0.6)) + '%';
        scoreLarge.textContent = progress;
        if(progress >= 100){
          clearInterval(interval);
          analysisCard.classList.remove('hidden');
          scanProgress.querySelector('span').textContent = 'Complete';
          scanProgress.classList.remove('text-indigo-300');
          miniSuggestions.innerHTML = 'Add more project metrics & portfolio links.';
        }
      }, 420);
    });

    // Career coach placeholder
    document.getElementById('askCoach').addEventListener('click', ()=>{
      const q = document.getElementById('coachQ').value || 'How do I get an internship?';
      const resp = document.getElementById('coachResp');
      resp.textContent = 'Analyzing…';
      setTimeout(()=>{
        resp.innerHTML = '<strong>Tip:</strong> Build a 1–2 week project with measurable results (e.g., reduced latency by 30%). Highlight it in the top of your resume and link to GitHub.';
      }, 800 + Math.random()*400);
    });

    // small UX touches: apply button
    document.addEventListener('click', (e)=>{
      if(e.target.classList.contains('applyBtn')){
        e.target.textContent = 'Applied ✓';
        e.target.disabled = true;
        e.target.classList.add('opacity-70');
      }
      if(e.target.classList.contains('viewBtn')){
        alert('Open job detail (demo)');
      }
    });

  </script>
</body>
</html>
