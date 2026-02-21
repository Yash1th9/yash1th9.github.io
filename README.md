<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>// YOUR_NAME :: Portfolio</title>
  <link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=VT323&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --bg:       #050a05;
      --surface:  #0a140a;
      --border:   #1a3a1a;
      --green:    #00ff41;
      --green2:   #00c832;
      --cyan:     #00ffe1;
      --red:      #ff2244;
      --dim:      #2a6e2a;
      --text:     #c8ffc8;
      --muted:    #527a52;
      --font-mono: 'Share Tech Mono', monospace;
      --font-display: 'Orbitron', sans-serif;
      --font-vt:  'VT323', monospace;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-mono);
      overflow-x: hidden;
      cursor: crosshair;
    }

    /* ── SCANLINES ── */
    body::before {
      content: '';
      position: fixed; inset: 0;
      background: repeating-linear-gradient(
        0deg,
        transparent,
        transparent 2px,
        rgba(0,0,0,0.15) 2px,
        rgba(0,0,0,0.15) 4px
      );
      pointer-events: none;
      z-index: 9999;
    }

    /* ── MATRIX CANVAS ── */
    #matrix-bg {
      position: fixed; top: 0; left: 0;
      width: 100%; height: 100%;
      opacity: 0.07;
      z-index: 0;
      pointer-events: none;
    }

    /* ── LAYOUT ── */
    .container { max-width: 1100px; margin: 0 auto; padding: 0 2rem; position: relative; z-index: 1; }

    /* ── NAV ── */
    nav {
      position: fixed; top: 0; left: 0; right: 0;
      background: rgba(5,10,5,0.92);
      border-bottom: 1px solid var(--border);
      backdrop-filter: blur(10px);
      z-index: 1000;
      padding: 0.8rem 2rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .nav-logo {
      font-family: var(--font-display);
      font-size: 0.9rem;
      color: var(--green);
      letter-spacing: 0.15em;
      text-decoration: none;
    }

    .nav-logo span { color: var(--cyan); }

    .nav-links {
      display: flex; gap: 1.5rem;
      list-style: none;
    }

    .nav-links a {
      font-size: 0.72rem;
      color: var(--muted);
      text-decoration: none;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      transition: color 0.2s;
      position: relative;
    }

    .nav-links a::before { content: '> '; color: var(--green); opacity: 0; transition: opacity 0.2s; }
    .nav-links a:hover { color: var(--green); }
    .nav-links a:hover::before { opacity: 1; }

    /* ── HERO ── */
    #hero {
      min-height: 100vh;
      display: flex; align-items: center;
      padding-top: 5rem;
      position: relative;
    }

    .hero-inner { position: relative; z-index: 1; }

    .hero-pre {
      font-size: 0.8rem;
      color: var(--dim);
      letter-spacing: 0.2em;
      margin-bottom: 1rem;
      animation: fadeInUp 0.6s ease both;
    }

    .hero-name {
      font-family: var(--font-display);
      font-size: clamp(2.5rem, 8vw, 5.5rem);
      font-weight: 900;
      line-height: 1;
      color: var(--green);
      text-shadow: 0 0 40px rgba(0,255,65,0.5), 0 0 80px rgba(0,255,65,0.2);
      letter-spacing: 0.05em;
      animation: fadeInUp 0.6s 0.1s ease both;
    }

    .hero-name .glitch {
      position: relative;
      display: inline-block;
    }

    .hero-name .glitch::before,
    .hero-name .glitch::after {
      content: attr(data-text);
      position: absolute; top: 0; left: 0;
      width: 100%;
    }

    .hero-name .glitch::before {
      color: var(--cyan);
      animation: glitch1 3s infinite;
      clip-path: polygon(0 0, 100% 0, 100% 33%, 0 33%);
    }

    .hero-name .glitch::after {
      color: var(--red);
      animation: glitch2 3s infinite;
      clip-path: polygon(0 67%, 100% 67%, 100% 100%, 0 100%);
    }

    @keyframes glitch1 {
      0%,94%,100% { transform: translate(0); opacity: 0; }
      95% { transform: translate(-3px, 1px); opacity: 0.8; }
      97% { transform: translate(3px, -1px); opacity: 0.8; }
      99% { transform: translate(-2px, 0); opacity: 0.8; }
    }

    @keyframes glitch2 {
      0%,94%,100% { transform: translate(0); opacity: 0; }
      95% { transform: translate(3px, -1px); opacity: 0.8; }
      97% { transform: translate(-3px, 1px); opacity: 0.8; }
      99% { transform: translate(2px, 0); opacity: 0.8; }
    }

    .hero-role {
      font-family: var(--font-vt);
      font-size: clamp(1.4rem, 4vw, 2.2rem);
      color: var(--cyan);
      margin-top: 0.5rem;
      animation: fadeInUp 0.6s 0.2s ease both;
      min-height: 2.5rem;
    }

    .cursor-blink {
      display: inline-block;
      width: 0.6em;
      height: 1.1em;
      background: var(--cyan);
      margin-left: 3px;
      vertical-align: middle;
      animation: blink 1s step-end infinite;
    }

    @keyframes blink { 50% { opacity: 0; } }

    .hero-desc {
      margin-top: 1.5rem;
      max-width: 550px;
      color: var(--muted);
      font-size: 0.88rem;
      line-height: 1.8;
      animation: fadeInUp 0.6s 0.3s ease both;
    }

    .hero-cta {
      margin-top: 2.5rem;
      display: flex; gap: 1rem; flex-wrap: wrap;
      animation: fadeInUp 0.6s 0.4s ease both;
    }

    .btn {
      display: inline-flex; align-items: center; gap: 0.4rem;
      padding: 0.7rem 1.5rem;
      font-family: var(--font-mono);
      font-size: 0.8rem;
      letter-spacing: 0.1em;
      text-decoration: none;
      text-transform: uppercase;
      border: 1px solid var(--green);
      color: var(--green);
      background: transparent;
      cursor: crosshair;
      transition: all 0.2s;
      position: relative;
      overflow: hidden;
    }

    .btn::before {
      content: '';
      position: absolute; inset: 0;
      background: var(--green);
      transform: translateX(-101%);
      transition: transform 0.25s ease;
      z-index: 0;
    }

    .btn:hover::before { transform: translateX(0); }
    .btn:hover { color: var(--bg); }
    .btn span { position: relative; z-index: 1; }

    .btn-outline {
      border-color: var(--cyan);
      color: var(--cyan);
    }

    .btn-outline::before { background: var(--cyan); }

    /* ── STATUS BAR ── */
    .status-bar {
      margin-top: 3rem;
      display: flex; gap: 2rem; flex-wrap: wrap;
      animation: fadeInUp 0.6s 0.5s ease both;
    }

    .status-item { display: flex; flex-direction: column; gap: 0.2rem; }
    .status-label { font-size: 0.65rem; color: var(--dim); letter-spacing: 0.2em; text-transform: uppercase; }
    .status-value { font-family: var(--font-display); font-size: 1.4rem; color: var(--green); }

    /* ── SECTION COMMON ── */
    section { padding: 5rem 0; position: relative; z-index: 1; }

    .section-header {
      display: flex; align-items: center; gap: 1rem;
      margin-bottom: 3rem;
    }

    .section-tag {
      font-size: 0.65rem;
      color: var(--green);
      letter-spacing: 0.25em;
      text-transform: uppercase;
      background: rgba(0,255,65,0.08);
      border: 1px solid var(--border);
      padding: 0.2rem 0.6rem;
      white-space: nowrap;
    }

    .section-title {
      font-family: var(--font-display);
      font-size: clamp(1.2rem, 3vw, 1.6rem);
      color: var(--text);
      letter-spacing: 0.08em;
    }

    .section-line {
      flex: 1;
      height: 1px;
      background: linear-gradient(90deg, var(--border), transparent);
    }

    /* ── ABOUT ── */
    .about-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 3rem;
      align-items: center;
    }

    .about-terminal {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 4px;
      overflow: hidden;
    }

    .term-bar {
      background: #0d1f0d;
      padding: 0.5rem 1rem;
      display: flex; align-items: center; gap: 0.5rem;
      border-bottom: 1px solid var(--border);
    }

    .term-dot {
      width: 10px; height: 10px; border-radius: 50%;
    }

    .term-dot.red { background: #ff5f57; }
    .term-dot.yellow { background: #febc2e; }
    .term-dot.green { background: #28c840; }

    .term-title { font-size: 0.7rem; color: var(--muted); margin-left: auto; }

    .term-body { padding: 1.5rem; font-size: 0.83rem; line-height: 1.9; }

    .term-line { margin-bottom: 0.3rem; }
    .term-prompt { color: var(--green); }
    .term-cmd { color: var(--cyan); }
    .term-out { color: var(--muted); padding-left: 1rem; }
    .term-out b { color: var(--text); }

    .about-bio {
      font-size: 0.88rem;
      line-height: 1.9;
      color: var(--muted);
    }

    .about-bio p { margin-bottom: 1rem; }
    .about-bio b { color: var(--green); }

    /* ── SKILLS ── */
    .skills-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1.5rem;
    }

    .skill-category {
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 1.5rem;
      transition: border-color 0.2s;
    }

    .skill-category:hover { border-color: var(--green); }

    .skill-cat-title {
      font-size: 0.7rem;
      color: var(--green);
      letter-spacing: 0.2em;
      text-transform: uppercase;
      margin-bottom: 1.2rem;
      padding-bottom: 0.6rem;
      border-bottom: 1px solid var(--border);
    }

    .skill-item {
      display: flex; align-items: center; justify-content: space-between;
      margin-bottom: 0.8rem;
    }

    .skill-name { font-size: 0.82rem; color: var(--text); }

    .skill-bar-wrap {
      width: 110px;
      height: 4px;
      background: var(--border);
      position: relative;
    }

    .skill-bar-fill {
      height: 100%;
      background: linear-gradient(90deg, var(--green), var(--cyan));
      box-shadow: 0 0 6px var(--green);
      transition: width 1s ease;
    }

    /* ── PROJECTS ── */
    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
      gap: 1.5rem;
    }

    .project-card {
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 1.5rem;
      position: relative;
      overflow: hidden;
      transition: border-color 0.2s, transform 0.2s;
      cursor: crosshair;
    }

    .project-card::before {
      content: '';
      position: absolute; top: 0; left: 0;
      width: 3px; height: 0;
      background: var(--green);
      transition: height 0.3s ease;
    }

    .project-card:hover { border-color: var(--green); transform: translateY(-2px); }
    .project-card:hover::before { height: 100%; }

    .project-id {
      font-size: 0.65rem;
      color: var(--dim);
      letter-spacing: 0.2em;
      margin-bottom: 0.5rem;
    }

    .project-name {
      font-family: var(--font-display);
      font-size: 0.95rem;
      color: var(--green);
      margin-bottom: 0.8rem;
      letter-spacing: 0.05em;
    }

    .project-desc {
      font-size: 0.82rem;
      color: var(--muted);
      line-height: 1.7;
      margin-bottom: 1rem;
    }

    .project-tags { display: flex; flex-wrap: wrap; gap: 0.4rem; margin-bottom: 1.2rem; }

    .tag {
      font-size: 0.65rem;
      color: var(--cyan);
      border: 1px solid rgba(0,255,225,0.3);
      padding: 0.15rem 0.5rem;
      letter-spacing: 0.1em;
    }

    .project-links { display: flex; gap: 0.8rem; }

    .project-link {
      font-size: 0.72rem;
      color: var(--muted);
      text-decoration: none;
      letter-spacing: 0.1em;
      transition: color 0.2s;
    }

    .project-link:hover { color: var(--green); }
    .project-link::before { content: '↗ '; }

    /* ── CERTS ── */
    .certs-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1.2rem;
    }

    .cert-card {
      display: flex; align-items: center; gap: 1rem;
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 1.2rem;
      transition: border-color 0.2s;
    }

    .cert-card:hover { border-color: var(--cyan); }

    .cert-icon {
      font-size: 2rem;
      flex-shrink: 0;
      filter: grayscale(0.3);
    }

    .cert-info {}
    .cert-name { font-size: 0.85rem; color: var(--text); margin-bottom: 0.2rem; }
    .cert-issuer { font-size: 0.72rem; color: var(--muted); }
    .cert-date { font-size: 0.65rem; color: var(--dim); margin-top: 0.3rem; }
    .cert-badge {
      margin-left: auto;
      font-size: 0.6rem;
      color: var(--green);
      border: 1px solid var(--green);
      padding: 0.15rem 0.4rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      white-space: nowrap;
      flex-shrink: 0;
    }

    /* ── CTF ── */
    .ctf-list { display: flex; flex-direction: column; gap: 1rem; }

    .ctf-card {
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 1.2rem 1.5rem;
      display: grid;
      grid-template-columns: auto 1fr auto;
      align-items: center;
      gap: 1.5rem;
      transition: border-color 0.2s;
      text-decoration: none;
    }

    .ctf-card:hover { border-color: var(--red); }

    .ctf-difficulty {
      font-size: 0.65rem;
      padding: 0.2rem 0.5rem;
      border: 1px solid;
      letter-spacing: 0.12em;
      text-transform: uppercase;
    }

    .ctf-difficulty.easy { color: var(--green); border-color: var(--green); }
    .ctf-difficulty.medium { color: #f0c030; border-color: #f0c030; }
    .ctf-difficulty.hard { color: var(--red); border-color: var(--red); }
    .ctf-difficulty.insane { color: #cc44ff; border-color: #cc44ff; }

    .ctf-info {}
    .ctf-name { font-size: 0.88rem; color: var(--text); margin-bottom: 0.2rem; }
    .ctf-meta { font-size: 0.7rem; color: var(--muted); }

    .ctf-platform { font-size: 0.7rem; color: var(--dim); }
    .ctf-flag {
      font-size: 0.75rem;
      color: var(--green);
      text-decoration: none;
      transition: color 0.2s;
    }
    .ctf-flag:hover { color: var(--cyan); }

    /* ── BLOG ── */
    .blog-list { display: flex; flex-direction: column; gap: 1px; border: 1px solid var(--border); }

    .blog-post {
      display: grid;
      grid-template-columns: 100px 1fr auto;
      gap: 1.5rem;
      padding: 1.2rem 1.5rem;
      align-items: center;
      background: var(--surface);
      text-decoration: none;
      border-bottom: 1px solid var(--border);
      transition: background 0.2s;
    }

    .blog-post:last-child { border-bottom: none; }
    .blog-post:hover { background: #0d1f0d; }

    .blog-date { font-size: 0.72rem; color: var(--dim); }
    .blog-title { font-size: 0.88rem; color: var(--text); }
    .blog-tag { font-size: 0.65rem; color: var(--cyan); border: 1px solid rgba(0,255,225,0.3); padding: 0.1rem 0.4rem; white-space: nowrap; }

    /* ── CONTACT ── */
    .contact-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 3rem;
    }

    .contact-links { display: flex; flex-direction: column; gap: 0.8rem; }

    .contact-link {
      display: flex; align-items: center; gap: 1rem;
      padding: 0.9rem 1.2rem;
      border: 1px solid var(--border);
      text-decoration: none;
      transition: border-color 0.2s, background 0.2s;
      background: var(--surface);
    }

    .contact-link:hover { border-color: var(--green); background: rgba(0,255,65,0.04); }

    .contact-icon { font-size: 1.1rem; width: 1.5rem; text-align: center; }
    .contact-handle { font-size: 0.82rem; color: var(--text); }
    .contact-platform { font-size: 0.65rem; color: var(--muted); display: block; }

    .contact-arrow { margin-left: auto; color: var(--green); font-size: 0.8rem; opacity: 0; transition: opacity 0.2s; }
    .contact-link:hover .contact-arrow { opacity: 1; }

    /* ── RESUME ── */
    .resume-box {
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 2rem;
      text-align: center;
    }

    .resume-box p { color: var(--muted); font-size: 0.85rem; margin-bottom: 1.5rem; line-height: 1.7; }

    /* ── FOOTER ── */
    footer {
      border-top: 1px solid var(--border);
      padding: 2rem;
      text-align: center;
      font-size: 0.72rem;
      color: var(--dim);
      position: relative; z-index: 1;
    }

    footer span { color: var(--green); }

    /* ── ANIMATIONS ── */
    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(20px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .fade-in { opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease, transform 0.6s ease; }
    .fade-in.visible { opacity: 1; transform: translateY(0); }

    /* ── DIVIDER ── */
    .divider {
      border: none;
      height: 1px;
      background: linear-gradient(90deg, transparent, var(--border), transparent);
      margin: 0;
    }

    /* ── RESPONSIVE ── */
    @media (max-width: 700px) {
      .about-grid, .contact-grid { grid-template-columns: 1fr; }
      .blog-post { grid-template-columns: 1fr; gap: 0.4rem; }
      .ctf-card { grid-template-columns: auto 1fr; }
      .nav-links { display: none; }
    }
  </style>
</head>
<body>

<!-- Matrix rain canvas -->
<canvas id="matrix-bg"></canvas>

<!-- ── NAV ── -->
<nav>
  <a class="nav-logo" href="#hero"><span>//</span> YOUR_NAME</a>
  <ul class="nav-links">
    <li><a href="#about">about</a></li>
    <li><a href="#skills">skills</a></li>
    <li><a href="#projects">projects</a></li>
    <li><a href="#certs">certs</a></li>
    <li><a href="#ctf">ctf</a></li>
    <li><a href="#blog">blog</a></li>
    <li><a href="#contact">contact</a></li>
  </ul>
</nav>

<!-- ── HERO ── -->
<section id="hero">
  <div class="container">
    <div class="hero-inner">
      <div class="hero-pre">&gt; initializing_portfolio.sh</div>
      <h1 class="hero-name">
        <span class="glitch" data-text="YOUR_NAME">YOUR_NAME</span>
      </h1>
      <div class="hero-role" id="typewriter"><span class="cursor-blink"></span></div>
      <p class="hero-desc">
        Security researcher &amp; developer operating in the digital wilderness.
        Passionate about breaking things responsibly, building secure systems,
        and documenting the journey.
      </p>
      <div class="hero-cta">
        <a class="btn" href="#projects"><span>View Projects</span></a>
        <a class="btn btn-outline" href="#contact"><span>Get In Touch</span></a>
        <a class="btn" href="resume.pdf" download><span>⬇ Resume</span></a>
      </div>
      <div class="status-bar">
        <div class="status-item">
          <span class="status-label">Projects</span>
          <span class="status-value">12</span>
        </div>
        <div class="status-item">
          <span class="status-label">Certs</span>
          <span class="status-value">05</span>
        </div>
        <div class="status-item">
          <span class="status-label">CTFs Solved</span>
          <span class="status-value">47</span>
        </div>
        <div class="status-item">
          <span class="status-label">Status</span>
          <span class="status-value" style="color:var(--cyan);font-size:0.9rem;">ONLINE</span>
        </div>
      </div>
    </div>
  </div>
</section>

<hr class="divider">

<!-- ── ABOUT ── -->
<section id="about">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">01</span>
      <h2 class="section-title">ABOUT_ME</h2>
      <div class="section-line"></div>
    </div>
    <div class="about-grid fade-in">
      <div class="about-terminal">
        <div class="term-bar">
          <span class="term-dot red"></span>
          <span class="term-dot yellow"></span>
          <span class="term-dot green"></span>
          <span class="term-title">terminal — bash</span>
        </div>
        <div class="term-body">
          <div class="term-line"><span class="term-prompt">┌──(</span><span class="term-cmd">yourname</span><span class="term-prompt">㉿kali)-[~]</span></div>
          <div class="term-line"><span class="term-prompt">└─$ </span><span class="term-cmd">whoami</span></div>
          <div class="term-out"><b>Security Researcher & Developer</b></div>
          <br>
          <div class="term-line"><span class="term-prompt">└─$ </span><span class="term-cmd">cat about.txt</span></div>
          <div class="term-out">Name    : <b>Your Full Name</b></div>
          <div class="term-out">Location: <b>Your City, Country</b></div>
          <div class="term-out">Focus   : <b>Pentesting, CTF, DevSec</b></div>
          <div class="term-out">Coffee  : <b>Black, always</b></div>
          <br>
          <div class="term-line"><span class="term-prompt">└─$ </span><span class="term-cmd">cat interests.txt</span></div>
          <div class="term-out"><b>Web Security</b> | <b>Reverse Engineering</b></div>
          <div class="term-out"><b>Network Pentesting</b> | <b>OSINT</b></div>
          <div class="term-out"><b>Malware Analysis</b> | <b>CTF Competitions</b></div>
          <br>
          <div class="term-line"><span class="term-prompt">└─$ </span><span class="term-cmd">_</span><span class="cursor-blink" style="background:var(--green)"></span></div>
        </div>
      </div>
      <div class="about-bio">
        <p>
          Hey, I'm <b>Your Name</b> — a security enthusiast and developer with a passion
          for understanding how systems work and, more importantly, how they break.
        </p>
        <p>
          I spend most of my time diving deep into <b>CTF challenges</b>, hunting bugs,
          building security tooling, and writing about what I learn along the way.
        </p>
        <p>
          Currently pursuing certifications and working toward making the digital world
          a little harder to compromise — one write-up at a time.
        </p>
        <p style="color:var(--dim);font-size:0.78rem;margin-top:1.5rem;">
          // Update this section with your actual background, goals, and story.
        </p>
      </div>
    </div>
  </div>
</section>

<hr class="divider">

<!-- ── SKILLS ── -->
<section id="skills">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">02</span>
      <h2 class="section-title">SKILLS</h2>
      <div class="section-line"></div>
    </div>
    <div class="skills-grid fade-in">

      <div class="skill-category">
        <div class="skill-cat-title">// Offensive Security</div>
        <div class="skill-item"><span class="skill-name">Web App Pentesting</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:85%"></div></div></div>
        <div class="skill-item"><span class="skill-name">Network Pentesting</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:75%"></div></div></div>
        <div class="skill-item"><span class="skill-name">Reverse Engineering</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:65%"></div></div></div>
        <div class="skill-item"><span class="skill-name">OSINT</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:80%"></div></div></div>
      </div>

      <div class="skill-category">
        <div class="skill-cat-title">// Development</div>
        <div class="skill-item"><span class="skill-name">Python</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:90%"></div></div></div>
        <div class="skill-item"><span class="skill-name">JavaScript / Node</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:70%"></div></div></div>
        <div class="skill-item"><span class="skill-name">Bash / Shell</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:85%"></div></div></div>
        <div class="skill-item"><span class="skill-name">Docker / Linux</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:80%"></div></div></div>
      </div>

      <div class="skill-category">
        <div class="skill-cat-title">// Tools & Frameworks</div>
        <div class="skill-item"><span class="skill-name">Burp Suite</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:88%"></div></div></div>
        <div class="skill-item"><span class="skill-name">Metasploit</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:72%"></div></div></div>
        <div class="skill-item"><span class="skill-name">Nmap / Wireshark</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:90%"></div></div></div>
        <div class="skill-item"><span class="skill-name">Ghidra / IDA</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:60%"></div></div></div>
      </div>

      <div class="skill-category">
        <div class="skill-cat-title">// Knowledge Areas</div>
        <div class="skill-item"><span class="skill-name">Cryptography</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:70%"></div></div></div>
        <div class="skill-item"><span class="skill-name">Malware Analysis</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:65%"></div></div></div>
        <div class="skill-item"><span class="skill-name">Cloud Security</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:60%"></div></div></div>
        <div class="skill-item"><span class="skill-name">Active Directory</span><div class="skill-bar-wrap"><div class="skill-bar-fill" style="width:75%"></div></div></div>
      </div>

    </div>
  </div>
</section>

<hr class="divider">

<!-- ── PROJECTS ── -->
<section id="projects">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">03</span>
      <h2 class="section-title">PROJECTS</h2>
      <div class="section-line"></div>
    </div>
    <div class="projects-grid fade-in">

      <div class="project-card">
        <div class="project-id">// PRJ-001</div>
        <div class="project-name">AutoRecon Framework</div>
        <p class="project-desc">Automated reconnaissance tool that chains Nmap, gobuster, and enum4linux for rapid attack surface mapping during CTFs and engagements.</p>
        <div class="project-tags">
          <span class="tag">Python</span>
          <span class="tag">Recon</span>
          <span class="tag">CLI Tool</span>
        </div>
        <div class="project-links">
          <a class="project-link" href="#">GitHub</a>
          <a class="project-link" href="#">Demo</a>
        </div>
      </div>

      <div class="project-card">
        <div class="project-id">// PRJ-002</div>
        <div class="project-name">Phishing Simulator</div>
        <p class="project-desc">Internal phishing simulation platform for security awareness training. Tracks click rates and generates detailed reports for teams.</p>
        <div class="project-tags">
          <span class="tag">Node.js</span>
          <span class="tag">Social Engineering</span>
          <span class="tag">Red Team</span>
        </div>
        <div class="project-links">
          <a class="project-link" href="#">GitHub</a>
        </div>
      </div>

      <div class="project-card">
        <div class="project-id">// PRJ-003</div>
        <div class="project-name">Log Anomaly Detector</div>
        <p class="project-desc">ML-based log parser that flags anomalous authentication events and lateral movement patterns in SIEM data.</p>
        <div class="project-tags">
          <span class="tag">Python</span>
          <span class="tag">ML</span>
          <span class="tag">Blue Team</span>
        </div>
        <div class="project-links">
          <a class="project-link" href="#">GitHub</a>
          <a class="project-link" href="#">Blog Post</a>
        </div>
      </div>

      <div class="project-card">
        <div class="project-id">// PRJ-004</div>
        <div class="project-name">Custom C2 Framework</div>
        <p class="project-desc">Lightweight command-and-control framework built for educational purposes. Demonstrates common C2 communication patterns and evasion.</p>
        <div class="project-tags">
          <span class="tag">Python</span>
          <span class="tag">C2</span>
          <span class="tag">Research</span>
        </div>
        <div class="project-links">
          <a class="project-link" href="#">GitHub</a>
        </div>
      </div>

      <div class="project-card">
        <div class="project-id">// PRJ-005</div>
        <div class="project-name">OSINT Dashboard</div>
        <p class="project-desc">Web dashboard aggregating public intelligence from Shodan, VirusTotal, and Censys into a unified threat intelligence view.</p>
        <div class="project-tags">
          <span class="tag">React</span>
          <span class="tag">APIs</span>
          <span class="tag">OSINT</span>
        </div>
        <div class="project-links">
          <a class="project-link" href="#">GitHub</a>
          <a class="project-link" href="#">Live</a>
        </div>
      </div>

      <div class="project-card">
        <div class="project-id">// PRJ-006</div>
        <div class="project-name">Add Your Project</div>
        <p class="project-desc">Replace this placeholder with your own project. Describe what it does, why you built it, and what you learned from it.</p>
        <div class="project-tags">
          <span class="tag">Your Tag</span>
          <span class="tag">Your Tag</span>
        </div>
        <div class="project-links">
          <a class="project-link" href="#">GitHub</a>
        </div>
      </div>

    </div>
  </div>
</section>

<hr class="divider">

<!-- ── CERTIFICATIONS ── -->
<section id="certs">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">04</span>
      <h2 class="section-title">CERTIFICATIONS</h2>
      <div class="section-line"></div>
    </div>
    <div class="certs-grid fade-in">

      <div class="cert-card">
        <div class="cert-icon">🛡️</div>
        <div class="cert-info">
          <div class="cert-name">Certified Ethical Hacker (CEH)</div>
          <div class="cert-issuer">EC-Council</div>
          <div class="cert-date">Issued: Jan 2024</div>
        </div>
        <span class="cert-badge">Active</span>
      </div>

      <div class="cert-card">
        <div class="cert-icon">🔐</div>
        <div class="cert-info">
          <div class="cert-name">CompTIA Security+</div>
          <div class="cert-issuer">CompTIA</div>
          <div class="cert-date">Issued: Mar 2023</div>
        </div>
        <span class="cert-badge">Active</span>
      </div>

      <div class="cert-card">
        <div class="cert-icon">🌐</div>
        <div class="cert-info">
          <div class="cert-name">eJPT — Junior Penetration Tester</div>
          <div class="cert-issuer">eLearnSecurity</div>
          <div class="cert-date">Issued: Aug 2023</div>
        </div>
        <span class="cert-badge">Active</span>
      </div>

      <div class="cert-card">
        <div class="cert-icon">☁️</div>
        <div class="cert-info">
          <div class="cert-name">AWS Solutions Architect</div>
          <div class="cert-issuer">Amazon Web Services</div>
          <div class="cert-date">Issued: Nov 2023</div>
        </div>
        <span class="cert-badge">Active</span>
      </div>

      <div class="cert-card">
        <div class="cert-icon">📜</div>
        <div class="cert-info">
          <div class="cert-name">Add Your Certification</div>
          <div class="cert-issuer">Issuing Body</div>
          <div class="cert-date">Issued: —</div>
        </div>
        <span class="cert-badge" style="border-color:var(--muted);color:var(--muted)">Pending</span>
      </div>

    </div>
  </div>
</section>

<hr class="divider">

<!-- ── CTF WRITEUPS ── -->
<section id="ctf">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">05</span>
      <h2 class="section-title">CTF_WRITEUPS</h2>
      <div class="section-line"></div>
    </div>
    <div class="ctf-list fade-in">

      <div class="ctf-card">
        <span class="ctf-difficulty hard">Hard</span>
        <div class="ctf-info">
          <div class="ctf-name">HTB — FormulaX</div>
          <div class="ctf-meta">Web · XSS → SSRF → RCE chain via Express.js template injection</div>
        </div>
        <div style="text-align:right">
          <div class="ctf-platform">HackTheBox</div>
          <a class="ctf-flag" href="#">Read Writeup ↗</a>
        </div>
      </div>

      <div class="ctf-card">
        <span class="ctf-difficulty medium">Medium</span>
        <div class="ctf-info">
          <div class="ctf-name">HTB — Keeper</div>
          <div class="ctf-meta">Linux · KeePass memory dump → root private key extraction</div>
        </div>
        <div style="text-align:right">
          <div class="ctf-platform">HackTheBox</div>
          <a class="ctf-flag" href="#">Read Writeup ↗</a>
        </div>
      </div>

      <div class="ctf-card">
        <span class="ctf-difficulty easy">Easy</span>
        <div class="ctf-info">
          <div class="ctf-name">THM — Advent of Cyber 2024</div>
          <div class="ctf-meta">Various · Log analysis, OPSEC, web exploitation, blue team tasks</div>
        </div>
        <div style="text-align:right">
          <div class="ctf-platform">TryHackMe</div>
          <a class="ctf-flag" href="#">Read Writeup ↗</a>
        </div>
      </div>

      <div class="ctf-card">
        <span class="ctf-difficulty insane">Insane</span>
        <div class="ctf-info">
          <div class="ctf-name">HTB — Ouija</div>
          <div class="ctf-meta">Linux · DNS rebinding → PHP filter exploitation → kernel privesc</div>
        </div>
        <div style="text-align:right">
          <div class="ctf-platform">HackTheBox</div>
          <a class="ctf-flag" href="#">Read Writeup ↗</a>
        </div>
      </div>

      <div class="ctf-card">
        <span class="ctf-difficulty medium">Medium</span>
        <div class="ctf-info">
          <div class="ctf-name">PicoCTF — Binary Exploitation Set</div>
          <div class="ctf-meta">Pwn · Stack overflow, format strings, ret2libc challenges</div>
        </div>
        <div style="text-align:right">
          <div class="ctf-platform">PicoCTF</div>
          <a class="ctf-flag" href="#">Read Writeup ↗</a>
        </div>
      </div>

    </div>
  </div>
</section>

<hr class="divider">

<!-- ── BLOG ── -->
<section id="blog">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">06</span>
      <h2 class="section-title">BLOG_ARTICLES</h2>
      <div class="section-line"></div>
    </div>
    <div class="blog-list fade-in">

      <a class="blog-post" href="#">
        <span class="blog-date">2025-12-18</span>
        <span class="blog-title">Exploiting SSRF to Pivot Inside AWS Metadata Service</span>
        <span class="blog-tag">Cloud</span>
      </a>

      <a class="blog-post" href="#">
        <span class="blog-date">2025-11-04</span>
        <span class="blog-title">Beginner's Guide to Active Directory Enumeration</span>
        <span class="blog-tag">Active Directory</span>
      </a>

      <a class="blog-post" href="#">
        <span class="blog-date">2025-10-21</span>
        <span class="blog-title">Breaking Down PHP Type Juggling Vulnerabilities</span>
        <span class="blog-tag">Web</span>
      </a>

      <a class="blog-post" href="#">
        <span class="blog-date">2025-09-15</span>
        <span class="blog-title">How I Set Up My Personal CTF Lab with Docker Compose</span>
        <span class="blog-tag">Lab Setup</span>
      </a>

      <a class="blog-post" href="#">
        <span class="blog-date">2025-08-30</span>
        <span class="blog-title">Writeup: Cracking KeePass in HTB Keeper</span>
        <span class="blog-tag">CTF</span>
      </a>

    </div>
  </div>
</section>

<hr class="divider">

<!-- ── CONTACT ── -->
<section id="contact">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">07</span>
      <h2 class="section-title">CONTACT</h2>
      <div class="section-line"></div>
    </div>
    <div class="contact-grid fade-in">
      <div>
        <p style="color:var(--muted);font-size:0.85rem;line-height:1.8;margin-bottom:1.5rem;">
          Open to collaborations, bug bounty teams, research projects, and good conversations about security. Reach out through any of the channels below.
        </p>
        <div class="contact-links">

          <a class="contact-link" href="https://github.com/yourusername" target="_blank">
            <span class="contact-icon">⌨</span>
            <div>
              <span class="contact-handle">yourusername</span>
              <span class="contact-platform">GitHub</span>
            </div>
            <span class="contact-arrow">→</span>
          </a>

          <a class="contact-link" href="https://linkedin.com/in/yourprofile" target="_blank">
            <span class="contact-icon">🔗</span>
            <div>
              <span class="contact-handle">yourprofile</span>
              <span class="contact-platform">LinkedIn</span>
            </div>
            <span class="contact-arrow">→</span>
          </a>

          <a class="contact-link" href="https://twitter.com/yourhandle" target="_blank">
            <span class="contact-icon">✕</span>
            <div>
              <span class="contact-handle">@yourhandle</span>
              <span class="contact-platform">X / Twitter</span>
            </div>
            <span class="contact-arrow">→</span>
          </a>

          <a class="contact-link" href="mailto:you@example.com">
            <span class="contact-icon">✉</span>
            <div>
              <span class="contact-handle">you@example.com</span>
              <span class="contact-platform">Email</span>
            </div>
            <span class="contact-arrow">→</span>
          </a>

          <a class="contact-link" href="https://app.hackthebox.com/users/yourprofile" target="_blank">
            <span class="contact-icon">⬡</span>
            <div>
              <span class="contact-handle">yourprofile</span>
              <span class="contact-platform">HackTheBox</span>
            </div>
            <span class="contact-arrow">→</span>
          </a>

          <a class="contact-link" href="https://tryhackme.com/p/yourprofile" target="_blank">
            <span class="contact-icon">🧠</span>
            <div>
              <span class="contact-handle">yourprofile</span>
              <span class="contact-platform">TryHackMe</span>
            </div>
            <span class="contact-arrow">→</span>
          </a>

        </div>
      </div>

      <!-- Resume Download Box -->
      <div class="resume-box">
        <div style="font-family:var(--font-display);font-size:1rem;color:var(--green);letter-spacing:0.1em;margin-bottom:0.5rem;">RESUME.PDF</div>
        <p>
          Download a copy of my full resume including work experience, education, certifications, and technical skills.
        </p>
        <a class="btn" href="resume.pdf" download style="display:inline-flex;margin:0 auto;">
          <span>⬇ Download Resume</span>
        </a>
        <p style="margin-top:1rem;font-size:0.72rem;color:var(--dim);">
          // Place your resume.pdf in the same folder as index.html
        </p>
      </div>
    </div>
  </div>
</section>

<!-- ── FOOTER ── -->
<footer>
  <div class="container">
    <p>// <span>YOUR_NAME</span> · Built with raw HTML &amp; CSS · Hosted on GitHub Pages</p>
    <p style="margin-top:0.4rem;">chmod 777 portfolio.sh · <span>2025</span></p>
  </div>
</footer>

<script>
// ── MATRIX RAIN ──
(function(){
  const canvas = document.getElementById('matrix-bg');
  const ctx = canvas.getContext('2d');
  let W, H, cols, drops;

  function init(){
    W = canvas.width  = window.innerWidth;
    H = canvas.height = window.innerHeight;
    cols = Math.floor(W / 16);
    drops = Array(cols).fill(0).map(() => Math.random() * -H/16);
  }

  const chars = 'アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン01ヴABCDEF0123456789<>{}[];'.split('');

  function draw(){
    ctx.fillStyle = 'rgba(5,10,5,0.05)';
    ctx.fillRect(0,0,W,H);
    ctx.fillStyle = '#00ff41';
    ctx.font = '13px Share Tech Mono';

    drops.forEach((y, i) => {
      const ch = chars[Math.floor(Math.random()*chars.length)];
      ctx.fillText(ch, i * 16, y * 16);
      if(y * 16 > H && Math.random() > 0.975) drops[i] = 0;
      drops[i] += 0.5;
    });
  }

  init();
  window.addEventListener('resize', init);
  setInterval(draw, 60);
})();

// ── TYPEWRITER ──
(function(){
  const roles = [
    'Security Researcher',
    'CTF Player',
    'Penetration Tester',
    'Bug Hunter',
    'Developer',
  ];
  const el = document.getElementById('typewriter');
  let ri = 0, ci = 0, deleting = false;

  function tick(){
    const role = roles[ri];
    if(!deleting){
      ci++;
      el.innerHTML = role.slice(0, ci) + '<span class="cursor-blink"></span>';
      if(ci === role.length){ deleting = true; setTimeout(tick, 1800); return; }
    } else {
      ci--;
      el.innerHTML = role.slice(0, ci) + '<span class="cursor-blink"></span>';
      if(ci === 0){ deleting = false; ri = (ri+1)%roles.length; }
    }
    setTimeout(tick, deleting ? 60 : 90);
  }
  tick();
})();

// ── SCROLL FADE IN ──
(function(){
  const obs = new IntersectionObserver((entries)=>{
    entries.forEach(e=>{
      if(e.isIntersecting){ e.target.classList.add('visible'); }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.fade-in').forEach(el => obs.observe(el));
})();
</script>
</body>
</html>
