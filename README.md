<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sahil Dahale — Data Science & Machine Learning</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600;9..144,700&family=IBM+Plex+Mono:wght@400;500;600&family=IBM+Plex+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#F3F5F8;
    --surface:#FFFFFF;
    --ink:#12172A;
    --muted:#5B6472;
    --line:#DCE2E9;
    --accent:#146C5B;      /* deep teal — class A */
    --accent-soft:#DCEEE9;
    --accent2:#E8873A;     /* amber — class B */
    --accent2-soft:#FBEADA;
    --radius:14px;
    --maxw:980px;
  }
  *{box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  @media (prefers-reduced-motion: reduce){
    html{scroll-behavior:auto;}
    *{animation-duration:0.001ms !important; transition-duration:0.001ms !important;}
  }
  body{
    margin:0;
    background:var(--bg);
    color:var(--ink);
    font-family:'IBM Plex Sans', sans-serif;
    line-height:1.55;
    -webkit-font-smoothing:antialiased;
  }
  h1,h2,h3{font-family:'Fraunces', serif; font-weight:600; margin:0 0 .4em;}
  a{color:inherit;}
  .mono{font-family:'IBM Plex Mono', monospace;}

  /* Progress bar — reads like a model-accuracy meter as you scroll */
  #progress{
    position:fixed; top:0; left:0; height:3px; width:0%;
    background:linear-gradient(90deg, var(--accent), var(--accent2));
    z-index:200; transition:width .08s linear;
  }

  nav{
    position:sticky; top:0; z-index:100;
    background:rgba(243,245,248,0.88); backdrop-filter:blur(8px);
    border-bottom:1px solid var(--line);
  }
  .nav-inner{
    max-width:var(--maxw); margin:0 auto; padding:16px 24px;
    display:flex; justify-content:space-between; align-items:center;
  }
  .nav-inner .brand{font-family:'Fraunces', serif; font-weight:600; font-size:1.1rem;}
  .nav-inner .brand .dot{color:var(--accent);}
  .nav-links{display:flex; gap:22px; list-style:none; margin:0; padding:0;}
  .nav-links a{
    text-decoration:none; font-size:.9rem; color:var(--muted); font-weight:500;
    transition:color .2s;
  }
  .nav-links a:hover{color:var(--ink);}

  section{max-width:var(--maxw); margin:0 auto; padding:88px 24px;}
  .eyebrow{
    font-family:'IBM Plex Mono', monospace; font-size:.78rem; letter-spacing:.06em;
    color:var(--accent); text-transform:uppercase; margin-bottom:14px; display:block;
  }

  /* ---------- HERO ---------- */
  #hero{
    max-width:none; padding:0; position:relative; overflow:hidden;
    border-bottom:1px solid var(--line);
  }
  .hero-grid{
    max-width:var(--maxw); margin:0 auto; padding:120px 24px 60px;
    position:relative; z-index:2;
  }
  #hero-canvas{
    position:absolute; inset:0; width:100%; height:100%; z-index:1; cursor:crosshair;
  }
  .hero-tag{font-family:'IBM Plex Mono', monospace; color:var(--muted); font-size:.85rem; margin-bottom:18px;}
  #hero h1{font-size:clamp(2.4rem, 6vw, 4.2rem); line-height:1.04; max-width:11ch;}
  #hero h1 em{font-style:normal; color:var(--accent);}
  .hero-sub{max-width:46ch; color:var(--muted); font-size:1.08rem; margin:18px 0 32px;}
  .hero-actions{display:flex; gap:14px; flex-wrap:wrap; margin-bottom:56px;}
  .btn{
    display:inline-flex; align-items:center; gap:8px;
    padding:12px 22px; border-radius:999px; text-decoration:none;
    font-weight:600; font-size:.92rem; transition:transform .15s, box-shadow .15s;
    border:1px solid transparent;
  }
  .btn:hover{transform:translateY(-2px);}
  .btn-primary{background:var(--ink); color:#fff;}
  .btn-primary:hover{box-shadow:0 8px 20px rgba(18,23,42,.22);}
  .btn-ghost{background:transparent; color:var(--ink); border-color:var(--line);}
  .btn-ghost:hover{border-color:var(--ink);}
  .hero-hint{
    font-family:'IBM Plex Mono', monospace; font-size:.78rem; color:var(--muted);
    display:flex; align-items:center; gap:8px;
  }
  .hero-hint .pulse{
    width:7px; height:7px; border-radius:50%; background:var(--accent2);
    animation:pulse 1.8s infinite;
  }
  @keyframes pulse{
    0%,100%{opacity:1; transform:scale(1);}
    50%{opacity:.35; transform:scale(1.6);}
  }

  /* ---------- REVEAL ON SCROLL ---------- */
  .reveal{opacity:0; transform:translateY(28px); transition:opacity .7s ease, transform .7s ease;}
  .reveal.in-view{opacity:1; transform:translateY(0);}
  .reveal-stagger > *{opacity:0; transform:translateY(22px); transition:opacity .6s ease, transform .6s ease;}
  .reveal-stagger.in-view > *{opacity:1; transform:translateY(0);}
  .reveal-stagger.in-view > *:nth-child(1){transition-delay:.02s;}
  .reveal-stagger.in-view > *:nth-child(2){transition-delay:.08s;}
  .reveal-stagger.in-view > *:nth-child(3){transition-delay:.14s;}
  .reveal-stagger.in-view > *:nth-child(4){transition-delay:.2s;}
  .reveal-stagger.in-view > *:nth-child(5){transition-delay:.26s;}
  .reveal-stagger.in-view > *:nth-child(6){transition-delay:.32s;}
  .reveal-stagger.in-view > *:nth-child(7){transition-delay:.38s;}
  .reveal-stagger.in-view > *:nth-child(8){transition-delay:.44s;}

  p.lead{font-size:1.08rem; color:var(--muted); max-width:64ch;}

  /* ---------- EXPERIENCE ---------- */
  .timeline{border-left:2px solid var(--line); padding-left:26px; display:flex; flex-direction:column; gap:34px;}
  .t-item{position:relative;}
  .t-item::before{
    content:''; position:absolute; left:-32px; top:5px;
    width:11px; height:11px; border-radius:50%;
    background:var(--surface); border:2px solid var(--accent);
  }
  .t-role{font-weight:600; font-size:1.05rem;}
  .t-org{color:var(--accent); font-weight:600;}
  .t-time{font-family:'IBM Plex Mono', monospace; font-size:.78rem; color:var(--muted); margin-bottom:6px; display:block;}
  .t-desc{color:var(--muted); max-width:60ch;}

  /* ---------- PROJECTS ---------- */
  .proj-grid{display:grid; grid-template-columns:repeat(auto-fit, minmax(260px,1fr)); gap:18px;}
  .card{
    background:var(--surface); border:1px solid var(--line); border-radius:var(--radius);
    padding:24px; text-decoration:none; color:var(--ink);
    transition:transform .2s, box-shadow .2s, border-color .2s;
    display:flex; flex-direction:column; gap:10px;
  }
  .card:hover{transform:translateY(-4px); box-shadow:0 14px 30px rgba(18,23,42,.08); border-color:var(--accent);}
  .card .tag{
    font-family:'IBM Plex Mono', monospace; font-size:.72rem; color:var(--accent);
    background:var(--accent-soft); width:fit-content; padding:3px 9px; border-radius:6px;
  }
  .card h3{font-size:1.08rem; margin:0;}
  .card p{color:var(--muted); font-size:.92rem; margin:0;}
  .card .arrow{margin-top:auto; font-size:.85rem; color:var(--ink); font-weight:600;}
  .note{font-size:.88rem; color:var(--muted); margin-top:18px;}

  /* ---------- SKILLS ---------- */
  .chip-row{display:flex; flex-wrap:wrap; gap:10px;}
  .chip{
    font-family:'IBM Plex Mono', monospace; font-size:.82rem;
    padding:8px 14px; border-radius:8px; background:var(--surface);
    border:1px solid var(--line);
  }
  .chip.a{border-color:var(--accent); color:var(--accent);}
  .chip.b{border-color:var(--accent2); color:var(--accent2);}

  /* ---------- EDUCATION / LEADERSHIP ---------- */
  .two-col{display:grid; grid-template-columns:1fr 1fr; gap:40px;}
  @media (max-width:720px){.two-col{grid-template-columns:1fr;} .proj-grid{grid-template-columns:1fr;}}
  .block h3{font-size:1.02rem;}
  .block .meta{color:var(--muted); font-size:.88rem; margin-bottom:6px;}

  /* ---------- FOOTER / CONTACT ---------- */
  #contact{text-align:center; padding-bottom:120px;}
  #contact h2{font-size:clamp(1.9rem,4vw,2.6rem);}
  .contact-links{display:flex; gap:16px; justify-content:center; margin-top:26px; flex-wrap:wrap;}
  footer{
    text-align:center; padding:30px 24px; color:var(--muted);
    font-size:.82rem; font-family:'IBM Plex Mono', monospace;
    border-top:1px solid var(--line);
  }

  /* click-anywhere data-point ripple */
  .click-point{
    position:fixed; pointer-events:none; z-index:999;
    font-family:'IBM Plex Mono', monospace; font-size:.68rem;
    color:var(--accent); white-space:nowrap;
    transform:translate(-50%,-50%);
    animation:clickpop .85s ease-out forwards;
  }
  .click-point .dot{
    width:7px; height:7px; border-radius:50%; background:currentColor;
    display:block; margin:0 auto 3px;
  }
  @keyframes clickpop{
    0%{opacity:0; transform:translate(-50%,-50%) scale(.4);}
    15%{opacity:1; transform:translate(-50%,-50%) scale(1.15);}
    100%{opacity:0; transform:translate(-50%,-90%) scale(1);}
  }
</style>
</head>
<body>

<div id="progress"></div>

<nav>
  <div class="nav-inner">
    <div class="brand">Sahil Dahale<span class="dot">.</span></div>
    <ul class="nav-links">
      <li><a href="#about">About</a></li>
      <li><a href="#experience">Experience</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#skills">Skills</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </div>
</nav>

<!-- ================= HERO ================= -->
<section id="hero">
  <canvas id="hero-canvas"></canvas>
  <div class="hero-grid">
    <span class="hero-tag mono">Nashik, India · Open to Data Analyst / Data Science internships</span>
    <h1>Turning data into <em>decisions</em>.</h1>
    <p class="hero-sub">Final-year B.Tech student in Artificial Intelligence & Machine Learning, building classification, clustering, and NLP projects — and picking up new ML tools every internship.</p>
    <div class="hero-actions">
      <a class="btn btn-primary" href="#projects">View projects</a>
      <a class="btn btn-ghost" href="mailto:sahildahale321@gmail.com">Email me</a>
      <a class="btn btn-ghost" href="https://github.com/sahildahale01" target="_blank" rel="noopener">GitHub ↗</a>
    </div>
    <div class="hero-hint"><span class="pulse"></span> click anywhere on this canvas — each click fits a new regression line, live</div>
  </div>
</section>

<!-- ================= ABOUT ================= -->
<section id="about" class="reveal">
  <span class="eyebrow">01 · About</span>
  <h2>Final-year AI & ML student, learning by shipping.</h2>
  <p class="lead">I'm currently a Data Science Intern at Oasis Infobyte, building and evaluating classification and regression models with Scikit-learn. Across four internships I've worked on EDA, predictive modelling, NLP, and full-stack development — and outside of coursework, I lead 500+ students as Campus President at Sandip University.</p>
</section>

<!-- ================= EXPERIENCE ================= -->
<section id="experience" class="reveal">
  <span class="eyebrow">02 · Experience</span>
  <h2>Where I've worked</h2>
  <div class="timeline">
    <div class="t-item">
      <span class="t-time mono">AUG 2026 — PRESENT</span>
      <div class="t-role">Data Science Intern <span class="t-org">@ Oasis Infobyte</span></div>
      <p class="t-desc">Building and evaluating classification/regression models in Python using Scikit-learn, applying feature engineering and cross-validation to improve accuracy.</p>
    </div>
    <div class="t-item">
      <span class="t-time mono">JUL 2025 — SEP 2025</span>
      <div class="t-role">Full Stack Web Development Intern <span class="t-org">@ Mindenious</span></div>
      <p class="t-desc">Contributed front-end and back-end features to team web applications; wrote documentation and tested code.</p>
    </div>
    <div class="t-item">
      <span class="t-time mono">JUN 2025 — JUL 2025</span>
      <div class="t-role">Data Science Intern <span class="t-org">@ SaiKet Systems & HunarIntern</span></div>
      <p class="t-desc">Completed applied data science projects on real-world datasets, building predictive models and surfacing patterns for business decisions.</p>
    </div>
    <div class="t-item">
      <span class="t-time mono">2025</span>
      <div class="t-role">Data Analysis Using Python Intern <span class="t-org">@ Auspify Technologies</span></div>
      <p class="t-desc">Used Python to analyze data as part of the development team's projects; documented findings and contributed to milestone delivery.</p>
    </div>
  </div>
</section>

<!-- ================= PROJECTS ================= -->
<section id="projects" class="reveal">
  <span class="eyebrow">03 · Projects</span>
  <h2>Selected work</h2>
  <div class="proj-grid reveal-stagger">
    <a class="card" href="https://github.com/sahildahale01/AI-Resume-Screening-System" target="_blank" rel="noopener">
      <span class="tag">NLP</span>
      <h3>AI Resume Screening System</h3>
      <p>NLP pipeline in Python & Scikit-learn to parse and score resumes against job descriptions using TF-IDF.</p>
      <span class="arrow">View repo →</span>
    </a>
    <a class="card" href="https://github.com/sahildahale01/Customer-Churn-Prediction" target="_blank" rel="noopener">
      <span class="tag">Classification</span>
      <h3>Customer Churn Prediction</h3>
      <p>Classification model using Python and Pandas to predict customer churn from user behavior.</p>
      <span class="arrow">View repo →</span>
    </a>
    <a class="card" href="https://github.com/sahildahale01/Sales-Prediction-Using-Python" target="_blank" rel="noopener">
      <span class="tag">Regression</span>
      <h3>Sales Prediction</h3>
      <p>Sales prediction model built during the Oasis Infobyte Data Science internship.</p>
      <span class="arrow">View repo →</span>
    </a>
    <a class="card" href="https://github.com/sahildahale01/Car-Price-Prediction-ML" target="_blank" rel="noopener">
      <span class="tag">Regression</span>
      <h3>Car Price Prediction</h3>
      <p>Machine learning model to predict used car selling prices.</p>
      <span class="arrow">View repo →</span>
    </a>
    <a class="card" href="https://github.com/sahildahale01/OIBSIP-Iris-Flower-Classification" target="_blank" rel="noopener">
      <span class="tag">Classification</span>
      <h3>Iris Flower Classification</h3>
      <p>Classic ML classification project built during the Oasis Infobyte internship.</p>
      <span class="arrow">View repo →</span>
    </a>
    <a class="card" href="https://github.com/sahildahale01/Email-Spam-Detection-ML" target="_blank" rel="noopener">
      <span class="tag">NLP</span>
      <h3>Email Spam Detection</h3>
      <p>NLP-based spam classifier trained on email text.</p>
      <span class="arrow">View repo →</span>
    </a>
    <a class="card" href="https://github.com/sahildahale01/Unemployment-Analysis-using-Python" target="_blank" rel="noopener">
      <span class="tag">EDA</span>
      <h3>Unemployment Analysis — India</h3>
      <p>Python data analysis project exploring unemployment trends across India.</p>
      <span class="arrow">View repo →</span>
    </a>
    <a class="card" href="https://github.com/sahildahale01/Hunar-Intern" target="_blank" rel="noopener">
      <span class="tag">Applied DS</span>
      <h3>Hunar Intern — DS Tasks</h3>
      <p>Collection of applied data science tasks completed during the Hunar Intern program.</p>
      <span class="arrow">View repo →</span>
    </a>
  </div>
  <p class="note">Additional coursework: Credit Card Fraud Detection · Retail Sales Dashboard (Power BI) · Customer Segmentation (K-Means)</p>
</section>

<!-- ================= SKILLS ================= -->
<section id="skills" class="reveal">
  <span class="eyebrow">04 · Skills</span>
  <h2>Tools I reach for</h2>
  <div class="chip-row">
    <span class="chip a">Python</span>
    <span class="chip a">Pandas</span>
    <span class="chip a">NumPy</span>
    <span class="chip a">Scikit-learn</span>
    <span class="chip a">TensorFlow</span>
    <span class="chip b">SQL</span>
    <span class="chip b">Power BI</span>
    <span class="chip b">Excel / DAX</span>
    <span class="chip a">Jupyter</span>
    <span class="chip b">Git / GitHub</span>
  </div>
</section>

<!-- ================= EDUCATION + LEADERSHIP ================= -->
<section class="reveal">
  <div class="two-col">
    <div class="block">
      <span class="eyebrow">05 · Education</span>
      <h3>B.Tech, AI & Machine Learning</h3>
      <div class="meta">Sandip University, Nashik · Expected Jul 2027 · CGPA 8.0/10</div>
      <h3 style="margin-top:20px;">Class XII — PCM with CS</h3>
      <div class="meta">Nalanda Junior College · 87.5%</div>
    </div>
    <div class="block">
      <span class="eyebrow">06 · Leadership</span>
      <h3>Campus President</h3>
      <div class="meta">Sandip University, Nashik · Feb 2024 — Present</div>
      <p class="t-desc">Represent 500+ students as the point of contact between the student body and university administration.</p>
      <h3 style="margin-top:20px;">Hackathon Organizing Lead</h3>
      <div class="meta">DIPEX Official, Pune District · Feb 2025 — Present</div>
      <p class="t-desc">Handled participant registration and event logistics for the 34th DIPEX Hackathon.</p>
    </div>
  </div>
</section>

<!-- ================= CONTACT ================= -->
<section id="contact" class="reveal">
  <span class="eyebrow">07 · Contact</span>
  <h2>Let's build something with data.</h2>
  <p class="lead" style="margin:0 auto;">Open to Data Analyst / Data Science internship opportunities — reach out any time.</p>
  <div class="contact-links">
    <a class="btn btn-primary" href="mailto:sahildahale321@gmail.com">sahildahale321@gmail.com</a>
    <a class="btn btn-ghost" href="https://linkedin.com/in/sahil-dahale" target="_blank" rel="noopener">LinkedIn</a>
    <a class="btn btn-ghost" href="https://github.com/sahildahale01" target="_blank" rel="noopener">GitHub</a>
  </div>
</section>

<footer>built by Sahil Dahale · every click above just fit a new line of best fit</footer>

<script>
// ---------- scroll progress bar ----------
const progress = document.getElementById('progress');
function updateProgress(){
  const h = document.documentElement;
  const scrolled = (h.scrollTop) / (h.scrollHeight - h.clientHeight) * 100;
  progress.style.width = (isFinite(scrolled) ? scrolled : 0) + '%';
}
window.addEventListener('scroll', updateProgress);
updateProgress();

// ---------- scroll reveal ----------
const revealEls = document.querySelectorAll('.reveal, .reveal-stagger');
const io = new IntersectionObserver((entries)=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.classList.add('in-view');
      io.unobserve(e.target);
    }
  });
}, {threshold:0.15});
revealEls.forEach(el=>io.observe(el));

// ---------- click-anywhere data point ripple ----------
document.addEventListener('click', function(e){
  const el = document.createElement('div');
  el.className = 'click-point';
  const x = (Math.random()*4-2).toFixed(1);
  const y = (Math.random()*4-2).toFixed(1);
  el.innerHTML = '<span class="dot"></span>(' + x + ', ' + y + ')';
  el.style.left = e.clientX + 'px';
  el.style.top = e.clientY + 'px';
  document.body.appendChild(el);
  setTimeout(()=>el.remove(), 900);
});

// ---------- hero canvas: click to fit a live regression line ----------
const canvas = document.getElementById('hero-canvas');
const ctx = canvas.getContext('2d');
let points = [];
let animT = 0;
let animLine = null, targetLine = null;

function resizeCanvas(){
  const hero = document.getElementById('hero');
  canvas.width = hero.clientWidth;
  canvas.height = hero.clientHeight;
  seedPoints();
}
function seedPoints(){
  points = [];
  const n = 14;
  for(let i=0;i<n;i++){
    points.push({
      x: Math.random()*canvas.width,
      y: canvas.height*0.35 + Math.random()*canvas.height*0.5,
      c: Math.random() > 0.5 ? 'a' : 'b',
      seeded:true
    });
  }
  fitLine();
}
function fitLine(){
  if(points.length < 2){ targetLine = null; return; }
  const n = points.length;
  let sx=0, sy=0, sxy=0, sxx=0;
  points.forEach(p=>{ sx+=p.x; sy+=p.y; sxy+=p.x*p.y; sxx+=p.x*p.x; });
  const denom = (n*sxx - sx*sx) || 1;
  const m = (n*sxy - sx*sy) / denom;
  const b = (sy - m*sx) / n;
  targetLine = {m, b};
  if(!animLine) animLine = {...targetLine};
}
function draw(){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  // faint grid
  ctx.strokeStyle = 'rgba(18,23,42,0.045)';
  ctx.lineWidth = 1;
  const gap = 48;
  for(let x=0;x<canvas.width;x+=gap){ ctx.beginPath(); ctx.moveTo(x,0); ctx.lineTo(x,canvas.height); ctx.stroke(); }
  for(let y=0;y<canvas.height;y+=gap){ ctx.beginPath(); ctx.moveTo(0,y); ctx.lineTo(canvas.width,y); ctx.stroke(); }

  // animate line toward target
  if(targetLine){
    if(!animLine) animLine = {...targetLine};
    animLine.m += (targetLine.m - animLine.m)*0.08;
    animLine.b += (targetLine.b - animLine.b)*0.08;
    ctx.strokeStyle = '#146C5B';
    ctx.lineWidth = 2.5;
    ctx.beginPath();
    ctx.moveTo(0, animLine.m*0 + animLine.b);
    ctx.lineTo(canvas.width, animLine.m*canvas.width + animLine.b);
    ctx.stroke();
  }

  // points
  points.forEach(p=>{
    ctx.beginPath();
    ctx.arc(p.x, p.y, 5, 0, Math.PI*2);
    ctx.fillStyle = p.c === 'a' ? 'rgba(20,108,91,0.55)' : 'rgba(232,135,58,0.6)';
    ctx.fill();
  });

  requestAnimationFrame(draw);
}
canvas.addEventListener('click', (e)=>{
  const rect = canvas.getBoundingClientRect();
  points.push({
    x: e.clientX - rect.left,
    y: e.clientY - rect.top,
    c: Math.random() > 0.5 ? 'a' : 'b'
  });
  if(points.length > 40) points.shift();
  fitLine();
});
window.addEventListener('resize', resizeCanvas);
resizeCanvas();
draw();
</script>

</body>
</html>
