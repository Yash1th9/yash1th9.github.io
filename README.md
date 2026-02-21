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

    /* ══════════════════════════════════════════
       THREAT INTELLIGENCE DASHBOARD
    ══════════════════════════════════════════ */

    /* ── TICKER ── */
    .threat-ticker-wrap {
      border: 1px solid var(--red);
      background: rgba(255,34,68,0.05);
      display: flex;
      align-items: center;
      overflow: hidden;
      margin-bottom: 2rem;
      height: 36px;
    }

    .ticker-label {
      background: var(--red);
      color: #000;
      font-size: 0.65rem;
      letter-spacing: 0.2em;
      padding: 0 0.8rem;
      height: 100%;
      display: flex; align-items: center;
      white-space: nowrap;
      flex-shrink: 0;
      font-weight: bold;
    }

    .ticker-track {
      display: flex;
      animation: ticker-scroll 60s linear infinite;
      white-space: nowrap;
    }

    .ticker-track:hover { animation-play-state: paused; }

    .ticker-item {
      font-size: 0.72rem;
      color: var(--red);
      padding: 0 2rem;
      border-right: 1px solid rgba(255,34,68,0.3);
    }

    .ticker-item span { color: var(--muted); margin-right: 0.4rem; }

    @keyframes ticker-scroll {
      0%   { transform: translateX(0); }
      100% { transform: translateX(-50%); }
    }

    /* ── DASHBOARD GRID ── */
    .dashboard-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1.5rem;
    }

    .dash-panel {
      background: var(--surface);
      border: 1px solid var(--border);
      display: flex; flex-direction: column;
    }

    .dash-panel.full-width { grid-column: 1 / -1; }

    .panel-header {
      display: flex; align-items: center; justify-content: space-between;
      padding: 0.7rem 1rem;
      border-bottom: 1px solid var(--border);
      background: #0d1f0d;
    }

    .panel-title {
      font-size: 0.68rem;
      color: var(--green);
      letter-spacing: 0.2em;
      text-transform: uppercase;
    }

    .panel-live {
      display: flex; align-items: center; gap: 0.4rem;
      font-size: 0.6rem;
      color: var(--red);
      letter-spacing: 0.1em;
    }

    .live-dot {
      width: 6px; height: 6px; border-radius: 50%;
      background: var(--red);
      animation: pulse-dot 1.2s ease-in-out infinite;
    }

    @keyframes pulse-dot {
      0%,100% { opacity: 1; transform: scale(1); }
      50%      { opacity: 0.4; transform: scale(0.7); }
    }

    .panel-body { padding: 1rem; flex: 1; overflow: hidden; }

    /* ── CVE PANEL ── */
    .cve-list { display: flex; flex-direction: column; gap: 0.7rem; }

    .cve-item {
      border: 1px solid var(--border);
      padding: 0.7rem;
      transition: border-color 0.2s;
    }

    .cve-item:hover { border-color: var(--red); }

    .cve-top { display: flex; align-items: center; justify-content: space-between; margin-bottom: 0.3rem; }

    .cve-id {
      font-size: 0.72rem;
      color: var(--cyan);
      letter-spacing: 0.05em;
    }

    .cvss-badge {
      font-size: 0.6rem;
      padding: 0.15rem 0.4rem;
      border: 1px solid;
      letter-spacing: 0.1em;
      font-weight: bold;
    }

    .cvss-critical { color: #ff2244; border-color: #ff2244; }
    .cvss-high     { color: #ff8c00; border-color: #ff8c00; }
    .cvss-medium   { color: #f0c030; border-color: #f0c030; }
    .cvss-low      { color: var(--green); border-color: var(--green); }

    .cve-desc {
      font-size: 0.73rem;
      color: var(--muted);
      line-height: 1.5;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }

    .cve-date { font-size: 0.62rem; color: var(--dim); margin-top: 0.25rem; }

    /* ── MALWARE IOC PANEL ── */
    .ioc-list { display: flex; flex-direction: column; gap: 0.5rem; }

    .ioc-item {
      display: grid;
      grid-template-columns: 60px 1fr auto;
      gap: 0.6rem;
      align-items: center;
      padding: 0.5rem 0.6rem;
      border: 1px solid var(--border);
      font-size: 0.7rem;
    }

    .ioc-type {
      font-size: 0.6rem;
      padding: 0.1rem 0.3rem;
      border: 1px solid;
      text-align: center;
      text-transform: uppercase;
      letter-spacing: 0.08em;
    }

    .ioc-type.trojan  { color: var(--red);   border-color: var(--red); }
    .ioc-type.loader  { color: #ff8c00;       border-color: #ff8c00; }
    .ioc-type.rat     { color: #cc44ff;       border-color: #cc44ff; }
    .ioc-type.stealer { color: var(--cyan);   border-color: var(--cyan); }
    .ioc-type.miner   { color: #f0c030;       border-color: #f0c030; }

    .ioc-hash { color: var(--text); font-size: 0.68rem; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
    .ioc-date { color: var(--dim); font-size: 0.62rem; white-space: nowrap; }

    /* ── ATTACK MAP ── */
    /* attackMap replaced by SVG */

    .map-legend {
      display: flex; gap: 1.2rem; flex-wrap: wrap;
      padding: 0.5rem 1rem;
      border-top: 1px solid var(--border);
    }

    .legend-item { display: flex; align-items: center; gap: 0.4rem; font-size: 0.62rem; color: var(--muted); }
    .legend-dot  { width: 8px; height: 8px; border-radius: 50%; }

    /* ── NEWS PANEL ── */
    .news-list { display: flex; flex-direction: column; }

    .news-item {
      display: grid;
      grid-template-columns: 1fr auto;
      gap: 0.8rem;
      align-items: center;
      padding: 0.7rem 0;
      border-bottom: 1px solid var(--border);
      text-decoration: none;
      transition: background 0.2s;
    }

    .news-item:last-child { border-bottom: none; }
    .news-item:hover .news-title { color: var(--green); }

    .news-title { font-size: 0.78rem; color: var(--text); line-height: 1.4; }
    .news-source { font-size: 0.62rem; color: var(--dim); display: block; margin-top: 0.2rem; }
    .news-time { font-size: 0.62rem; color: var(--dim); white-space: nowrap; }

    /* ── STATS ROW ── */
    .threat-stats {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 1rem;
      margin-bottom: 1.5rem;
    }

    .t-stat {
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 1rem;
      text-align: center;
      position: relative;
      overflow: hidden;
    }

    .t-stat::before {
      content: '';
      position: absolute; bottom: 0; left: 0; right: 0;
      height: 2px;
    }

    .t-stat.red::before   { background: var(--red); }
    .t-stat.cyan::before  { background: var(--cyan); }
    .t-stat.orange::before{ background: #ff8c00; }
    .t-stat.green::before { background: var(--green); }

    .t-stat-val {
      font-family: var(--font-display);
      font-size: 1.5rem;
      letter-spacing: 0.05em;
    }

    .t-stat.red   .t-stat-val { color: var(--red); }
    .t-stat.cyan  .t-stat-val { color: var(--cyan); }
    .t-stat.orange .t-stat-val{ color: #ff8c00; }
    .t-stat.green .t-stat-val { color: var(--green); }

    .t-stat-label { font-size: 0.62rem; color: var(--dim); letter-spacing: 0.15em; text-transform: uppercase; margin-top: 0.3rem; }
    .t-stat-delta { font-size: 0.6rem; color: var(--green); margin-top: 0.2rem; }

    /* ── LOADER ── */
    .panel-loading {
      display: flex; align-items: center; justify-content: center;
      height: 80px; color: var(--dim); font-size: 0.75rem;
      gap: 0.5rem;
    }

    .panel-loading::before {
      content: '';
      width: 10px; height: 10px;
      border: 2px solid var(--border);
      border-top-color: var(--green);
      border-radius: 50%;
      animation: spin 0.8s linear infinite;
    }

    @keyframes spin { to { transform: rotate(360deg); } }

    /* ── RESPONSIVE ── */
    @media (max-width: 700px) {
      .dashboard-grid { grid-template-columns: 1fr; }
      .threat-stats { grid-template-columns: repeat(2, 1fr); }
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
    <li><a href="#threat" style="color:var(--red)">threat intel</a></li>
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

<!-- ── THREAT INTELLIGENCE DASHBOARD ── -->
<section id="threat">
  <div class="container">

    <div class="section-header fade-in">
      <span class="section-tag" style="border-color:rgba(255,34,68,0.4);color:var(--red);background:rgba(255,34,68,0.08);">07</span>
      <h2 class="section-title">THREAT_INTEL <span style="color:var(--red);font-size:0.7em;">// LIVE</span></h2>
      <div class="section-line"></div>
    </div>

    <!-- TICKER -->
    <div class="threat-ticker-wrap fade-in">
      <div class="ticker-label">⚠ LIVE FEED</div>
      <div style="overflow:hidden;flex:1">
        <div class="ticker-track" id="tickerTrack">
          <!-- populated by JS -->
        </div>
      </div>
    </div>

    <!-- STATS ROW -->
    <div class="threat-stats fade-in">
      <div class="t-stat red">
        <div class="t-stat-val" id="statCves">—</div>
        <div class="t-stat-label">New CVEs Today</div>
        <div class="t-stat-delta">▲ fetching...</div>
      </div>
      <div class="t-stat orange">
        <div class="t-stat-val" id="statMalware">—</div>
        <div class="t-stat-label">Malware Samples</div>
        <div class="t-stat-delta">last 24h</div>
      </div>
      <div class="t-stat cyan">
        <div class="t-stat-val" id="statAttacks">—</div>
        <div class="t-stat-label">Attacks Tracked</div>
        <div class="t-stat-delta">▲ live counter</div>
      </div>
      <div class="t-stat green">
        <div class="t-stat-val" id="statPatched">—</div>
        <div class="t-stat-label">CISA KEV Total</div>
        <div class="t-stat-delta">known exploited</div>
      </div>
    </div>

    <!-- DASHBOARD GRID -->
    <div class="dashboard-grid fade-in">

      <!-- CVE PANEL -->
      <div class="dash-panel">
        <div class="panel-header">
          <span class="panel-title">// Recent CVEs — NVD Feed</span>
          <span class="panel-live"><span class="live-dot"></span>LIVE</span>
        </div>
        <div class="panel-body">
          <div id="cveList" class="cve-list">
            <div class="panel-loading">Fetching NVD data...</div>
          </div>
        </div>
      </div>

      <!-- MALWARE IOC PANEL -->
      <div class="dash-panel">
        <div class="panel-header">
          <span class="panel-title">// Malware IOCs — MalwareBazaar</span>
          <span class="panel-live"><span class="live-dot" style="background:#ff8c00"></span>LIVE</span>
        </div>
        <div class="panel-body">
          <div id="iocList" class="ioc-list">
            <div class="panel-loading">Fetching IOC data...</div>
          </div>
        </div>
      </div>

      <!-- ATTACK MAP -->
      <div class="dash-panel full-width">
        <div class="panel-header">
          <span class="panel-title">// Global Attack Map — Real-Time Simulation</span>
          <span class="panel-live"><span class="live-dot"></span>LIVE</span>
        </div>
        <div style="position:relative;width:100%;height:300px;background:#050a05;">
          <!-- Real SVG World Map -->
          <svg id="worldMapSVG" viewBox="0 0 1000 500" preserveAspectRatio="xMidYMid meet"
               style="position:absolute;top:0;left:0;width:100%;height:100%;">
            <defs>
              <filter id="glow">
                <feGaussianBlur stdDeviation="1.5" result="blur"/>
                <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
              </filter>
            </defs>
            <!-- Grid lines -->
            <g stroke="rgba(26,58,26,0.3)" stroke-width="0.5" fill="none">
              <line x1="0" y1="83" x2="1000" y2="83"/>
              <line x1="0" y1="166" x2="1000" y2="166"/>
              <line x1="0" y1="250" x2="1000" y2="250"/>
              <line x1="0" y1="333" x2="1000" y2="333"/>
              <line x1="0" y1="416" x2="1000" y2="416"/>
              <line x1="125" y1="0" x2="125" y2="500"/>
              <line x1="250" y1="0" x2="250" y2="500"/>
              <line x1="375" y1="0" x2="375" y2="500"/>
              <line x1="500" y1="0" x2="500" y2="500"/>
              <line x1="625" y1="0" x2="625" y2="500"/>
              <line x1="750" y1="0" x2="750" y2="500"/>
              <line x1="875" y1="0" x2="875" y2="500"/>
            </g>
            <!-- Equator -->
            <line x1="0" y1="250" x2="1000" y2="250" stroke="rgba(0,255,65,0.08)" stroke-width="1" stroke-dasharray="4,6"/>

            <!-- CONTINENTS — proper simplified outlines, fill + stroke -->
            <g fill="rgba(0,255,65,0.07)" stroke="rgba(0,255,65,0.25)" stroke-width="0.8" stroke-linejoin="round">

              <!-- North America -->
              <path d="M155,60 L190,55 L210,62 L225,58 L238,65 L245,80 L250,95 L242,108
                       L248,118 L240,130 L232,148 L228,168 L218,188 L208,202 L198,210
                       L185,225 L175,240 L165,252 L158,248 L150,238 L148,225 L155,210
                       L152,195 L145,180 L138,165 L132,148 L128,132 L130,115 L125,100
                       L128,85 L138,72 L148,65 Z"/>
              <!-- Greenland -->
              <path d="M230,30 L258,22 L275,28 L278,42 L268,52 L252,55 L238,50 L228,40 Z"/>
              <!-- Mexico / Central America -->
              <path d="M165,252 L175,258 L180,270 L172,278 L165,285 L160,278 L158,265 L160,255 Z"/>

              <!-- South America -->
              <path d="M205,268 L222,262 L238,265 L248,275 L252,290 L255,310 L258,332
                       L255,355 L248,375 L238,392 L225,402 L212,405 L200,398 L190,382
                       L185,362 L185,340 L188,318 L190,298 L195,280 Z"/>

              <!-- Europe -->
              <path d="M440,88 L455,82 L470,78 L485,80 L498,88 L505,98 L510,112
                       L502,122 L495,130 L488,138 L478,142 L465,145 L452,140 L442,132
                       L435,120 L432,108 L435,98 Z"/>
              <!-- UK -->
              <path d="M428,92 L435,88 L438,98 L432,105 L425,102 L422,95 Z"/>
              <!-- Scandinavia -->
              <path d="M460,55 L475,48 L488,52 L492,65 L485,78 L472,78 L462,72 L458,62 Z"/>
              <!-- Iberian Peninsula -->
              <path d="M430,128 L445,122 L452,130 L448,142 L438,148 L428,142 L425,132 Z"/>

              <!-- Africa -->
              <path d="M450,158 L465,150 L480,148 L495,152 L508,162 L515,178 L518,198
                       L520,220 L518,242 L515,265 L510,288 L502,308 L492,325 L478,338
                       L462,345 L448,342 L435,330 L425,312 L420,290 L418,268 L420,245
                       L422,222 L425,200 L428,178 L435,162 Z"/>
              <!-- Madagascar -->
              <path d="M528,278 L535,272 L540,282 L538,295 L530,300 L524,292 L524,282 Z"/>

              <!-- Europe East / Russia West -->
              <path d="M505,98 L525,88 L548,80 L568,75 L585,78 L598,88 L605,102
                       L598,118 L585,128 L568,132 L552,128 L538,120 L520,115 L510,108 Z"/>

              <!-- Middle East -->
              <path d="M528,145 L545,138 L562,135 L575,140 L582,152 L578,165
                       L565,172 L550,172 L538,165 L528,155 Z"/>

              <!-- Central / South Asia -->
              <path d="M582,115 L605,108 L628,105 L648,108 L662,118 L665,132
                       L658,145 L645,155 L630,162 L615,162 L600,155 L588,142
                       L582,128 Z"/>
              <!-- India -->
              <path d="M615,162 L632,158 L645,165 L648,180 L642,198 L630,212
                       L618,218 L608,210 L602,195 L602,178 L608,165 Z"/>

              <!-- Southeast Asia -->
              <path d="M680,145 L698,138 L715,140 L722,152 L718,165 L705,172
                       L690,170 L680,160 Z"/>
              <!-- Malay Peninsula -->
              <path d="M700,175 L708,170 L712,182 L710,195 L700,198 L694,188 L695,178 Z"/>

              <!-- China / East Asia -->
              <path d="M662,98 L688,88 L715,82 L738,85 L755,95 L762,110 L758,128
                       L745,140 L728,148 L710,148 L695,140 L680,130 L668,118 Z"/>

              <!-- Japan -->
              <path d="M768,100 L778,95 L785,102 L782,115 L772,118 L765,112 L765,104 Z"/>
              <!-- Korean Peninsula -->
              <path d="M748,108 L758,105 L762,115 L755,122 L745,120 L742,112 Z"/>

              <!-- Russia / Siberia -->
              <path d="M548,48 L580,38 L620,30 L665,28 L710,32 L748,40 L775,52
                       L778,68 L762,80 L738,85 L710,80 L680,75 L650,72 L620,70
                       L595,72 L568,75 L548,80 L532,75 L522,62 L530,50 Z"/>

              <!-- Australia -->
              <path d="M718,315 L742,305 L768,308 L788,320 L800,338 L800,360
                       L792,378 L775,390 L755,395 L732,390 L715,375 L705,355
                       L705,335 L710,320 Z"/>
              <!-- New Zealand (small) -->
              <path d="M820,368 L828,362 L832,372 L828,382 L820,380 Z"/>

              <!-- Greenland ice -->
              <path d="M238,18 L260,12 L282,15 L295,28 L290,42 L275,28 L258,22 Z"
                    fill="rgba(0,255,200,0.05)" stroke="rgba(0,255,200,0.15)"/>

              <!-- Antarctica (partial) -->
              <path d="M200,478 L350,465 L500,460 L650,462 L800,468 L900,478"
                    fill="none" stroke="rgba(0,255,65,0.12)" stroke-width="1"/>

            </g>

            <!-- City dots — positioned by lat/lon -->
            <g id="cityDots"></g>
            <!-- Attack arcs drawn by JS -->
            <g id="attackArcs"></g>
            <!-- Attack particles drawn by JS -->
            <g id="attackParticles"></g>
          </svg>
        </div>
        <div class="map-legend">
          <div class="legend-item"><span class="legend-dot" style="background:var(--red)"></span>Brute Force</div>
          <div class="legend-item"><span class="legend-dot" style="background:var(--cyan)"></span>Port Scan</div>
          <div class="legend-item"><span class="legend-dot" style="background:#ff8c00"></span>Exploit</div>
          <div class="legend-item"><span class="legend-dot" style="background:#cc44ff"></span>Malware C2</div>
          <div class="legend-item"><span class="legend-dot" style="background:#f0c030"></span>DDoS</div>
          <div id="mapEventCount" style="margin-left:auto;font-size:0.62rem;color:var(--dim)">0 events tracked</div>
        </div>
      </div>

      <!-- NEWS PANEL -->
      <div class="dash-panel">
        <div class="panel-header">
          <span class="panel-title">// Security News</span>
          <span class="panel-live"><span class="live-dot" style="background:var(--cyan)"></span>RSS</span>
        </div>
        <div class="panel-body">
          <div id="newsList" class="news-list">
            <div class="panel-loading">Fetching news...</div>
          </div>
        </div>
      </div>

      <!-- CISA KEV PANEL -->
      <div class="dash-panel">
        <div class="panel-header">
          <span class="panel-title">// CISA Known Exploited Vulns</span>
          <span class="panel-live"><span class="live-dot" style="background:#ff8c00"></span>CISA</span>
        </div>
        <div class="panel-body">
          <div id="kevList" class="cve-list">
            <div class="panel-loading">Fetching CISA KEV...</div>
          </div>
        </div>
      </div>

    </div><!-- /dashboard-grid -->
  </div>
</section>

<hr class="divider">

<!-- ── CONTACT ── -->
<section id="contact">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">08</span>
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

          <a class="contact-link" href="/cdn-cgi/l/email-protection#d1a8bea491b4a9b0bca1bdb4ffb2bebc">
            <span class="contact-icon">✉</span>
            <div>
              <span class="contact-handle"><span class="__cf_email__" data-cfemail="92ebfde7d2f7eaf3ffe2fef7bcf1fdff">[email&#160;protected]</span></span>
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

<script data-cfasync="false" src="/cdn-cgi/scripts/5c5dd728/cloudflare-static/email-decode.min.js"></script><script>
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

// ══════════════════════════════════════════
// THREAT INTELLIGENCE DASHBOARD
// ══════════════════════════════════════════

// ── ATTACK MAP — SVG World Map ──
(function(){
  const SVG_NS = 'http://www.w3.org/2000/svg';
  const VW = 1000, VH = 500; // viewBox dimensions

  // Convert lat/lon → SVG x,y (simple equirectangular)
  function project(lat, lon){
    const x = (lon + 180) / 360 * VW;
    const y = (90 - lat)  / 180 * VH;
    return { x, y };
  }

  const cities = [
    { name:'New York',      lat:40.7,  lon:-74.0  },
    { name:'Los Angeles',   lat:34.0,  lon:-118.2 },
    { name:'Chicago',       lat:41.8,  lon:-87.6  },
    { name:'Toronto',       lat:43.7,  lon:-79.4  },
    { name:'Washington DC', lat:38.9,  lon:-77.0  },
    { name:'Miami',         lat:25.8,  lon:-80.2  },
    { name:'São Paulo',     lat:-23.5, lon:-46.6  },
    { name:'Buenos Aires',  lat:-34.6, lon:-58.4  },
    { name:'Bogotá',        lat:4.7,   lon:-74.1  },
    { name:'London',        lat:51.5,  lon:-0.1   },
    { name:'Paris',         lat:48.9,  lon:2.3    },
    { name:'Berlin',        lat:52.5,  lon:13.4   },
    { name:'Amsterdam',     lat:52.4,  lon:4.9    },
    { name:'Madrid',        lat:40.4,  lon:-3.7   },
    { name:'Rome',          lat:41.9,  lon:12.5   },
    { name:'Moscow',        lat:55.8,  lon:37.6   },
    { name:'Kyiv',          lat:50.5,  lon:30.5   },
    { name:'Istanbul',      lat:41.0,  lon:28.9   },
    { name:'Dubai',         lat:25.2,  lon:55.3   },
    { name:'Tehran',        lat:35.7,  lon:51.4   },
    { name:'Riyadh',        lat:24.7,  lon:46.7   },
    { name:'Mumbai',        lat:19.1,  lon:72.9   },
    { name:'Delhi',         lat:28.6,  lon:77.2   },
    { name:'Kolkata',       lat:22.6,  lon:88.4   },
    { name:'Beijing',       lat:39.9,  lon:116.4  },
    { name:'Shanghai',      lat:31.2,  lon:121.5  },
    { name:'Tokyo',         lat:35.7,  lon:139.7  },
    { name:'Seoul',         lat:37.6,  lon:126.9  },
    { name:'Hong Kong',     lat:22.3,  lon:114.2  },
    { name:'Singapore',     lat:1.4,   lon:103.8  },
    { name:'Jakarta',       lat:-6.2,  lon:106.8  },
    { name:'Sydney',        lat:-33.9, lon:151.2  },
    { name:'Melbourne',     lat:-37.8, lon:144.9  },
    { name:'Johannesburg',  lat:-26.2, lon:28.0   },
    { name:'Lagos',         lat:6.5,   lon:3.4    },
    { name:'Cairo',         lat:30.1,  lon:31.2   },
    { name:'Nairobi',       lat:-1.3,  lon:36.8   },
    { name:'Bangalore',     lat:12.9,  lon:77.6   },
  ];

  const types = [
    { label:'Brute Force', color:'#ff2244' },
    { label:'Port Scan',   color:'#00ffe1' },
    { label:'Exploit',     color:'#ff8c00' },
    { label:'Malware C2',  color:'#cc44ff' },
    { label:'DDoS',        color:'#f0c030' },
  ];

  // Render city dots
  const dotsGroup = document.getElementById('cityDots');
  if(dotsGroup){
    cities.forEach(c => {
      const p = project(c.lat, c.lon);
      // Outer ring
      const ring = document.createElementNS(SVG_NS,'circle');
      ring.setAttribute('cx', p.x); ring.setAttribute('cy', p.y);
      ring.setAttribute('r', '4'); ring.setAttribute('fill','none');
      ring.setAttribute('stroke','rgba(0,255,65,0.2)'); ring.setAttribute('stroke-width','0.8');
      dotsGroup.appendChild(ring);
      // Inner dot
      const dot = document.createElementNS(SVG_NS,'circle');
      dot.setAttribute('cx', p.x); dot.setAttribute('cy', p.y);
      dot.setAttribute('r','1.8');
      dot.setAttribute('fill','rgba(0,255,65,0.7)');
      dot.setAttribute('filter','url(#glow)');
      dotsGroup.appendChild(dot);
    });
  }

  // Attack animation using SVG
  const arcsGroup       = document.getElementById('attackArcs');
  const particlesGroup  = document.getElementById('attackParticles');
  let eventCount = 0;
  let attacks = [];

  function spawnAttack(){
    const src  = cities[Math.floor(Math.random()*cities.length)];
    let   dst  = cities[Math.floor(Math.random()*cities.length)];
    while(dst === src) dst = cities[Math.floor(Math.random()*cities.length)];
    const type = types[Math.floor(Math.random()*types.length)];

    const s = project(src.lat, src.lon);
    const d = project(dst.lat, dst.lon);

    // Control point: arc upward
    const mx = (s.x + d.x) / 2;
    const my = Math.min(s.y, d.y) - 60 - Math.random()*80;

    // Create arc path
    const arc = document.createElementNS(SVG_NS,'path');
    const pathD = `M${s.x},${s.y} Q${mx},${my} ${d.x},${d.y}`;
    arc.setAttribute('d', pathD);
    arc.setAttribute('fill','none');
    arc.setAttribute('stroke', type.color);
    arc.setAttribute('stroke-width','0.8');
    arc.setAttribute('opacity','0.3');
    const totalLen = 300; // approximate
    arc.setAttribute('stroke-dasharray', totalLen);
    arc.setAttribute('stroke-dashoffset', totalLen);
    arcsGroup.appendChild(arc);

    // Particle (moving dot)
    const particle = document.createElementNS(SVG_NS,'circle');
    particle.setAttribute('r','3');
    particle.setAttribute('fill', type.color);
    particle.setAttribute('filter','url(#glow)');
    particlesGroup.appendChild(particle);

    // Impact ring (hidden initially)
    const impact = document.createElementNS(SVG_NS,'circle');
    impact.setAttribute('cx', d.x); impact.setAttribute('cy', d.y);
    impact.setAttribute('r','0'); impact.setAttribute('fill','none');
    impact.setAttribute('stroke', type.color); impact.setAttribute('stroke-width','1');
    impact.setAttribute('opacity','0');
    particlesGroup.appendChild(impact);

    attacks.push({ arc, particle, impact, s, d, mx, my, t:0,
      pathD, type, done:false, id: eventCount });

    eventCount++;
    const counter = document.getElementById('mapEventCount');
    if(counter) counter.textContent = eventCount.toLocaleString() + ' events tracked';

    // Clean up after animation
    setTimeout(()=>{
      arc.remove(); particle.remove(); impact.remove();
      attacks = attacks.filter(a => !a.done);
    }, 4000);
  }

  function bezier(t, p0, p1, p2){
    return (1-t)*(1-t)*p0 + 2*(1-t)*t*p1 + t*t*p2;
  }

  function animate(){
    attacks.forEach(a => {
      if(a.done) return;
      a.t = Math.min(a.t + 0.012, 1);

      // Move particle along bezier
      const px = bezier(a.t, a.s.x, a.mx, a.d.x);
      const py = bezier(a.t, a.s.y, a.my, a.d.y);
      a.particle.setAttribute('cx', px);
      a.particle.setAttribute('cy', py);

      // Animate arc stroke-dashoffset
      const len = 300;
      a.arc.setAttribute('stroke-dashoffset', len * (1 - a.t));
      a.arc.setAttribute('opacity', Math.min(a.t * 2, 0.4));

      // Impact ring
      if(a.t > 0.85){
        const prog = (a.t - 0.85) / 0.15;
        a.impact.setAttribute('r', prog * 16);
        a.impact.setAttribute('opacity', (1 - prog) * 0.8);
      }

      if(a.t >= 1) a.done = true;
    });
    requestAnimationFrame(animate);
  }

  animate();
  setInterval(spawnAttack, 700 + Math.random()*1000);
})();


// ══════════════════════════════════════════
// DASHBOARD DATA — 100% SELF-CONTAINED
// No API calls = no CORS = always works
// Data rotates/animates to feel live
// ══════════════════════════════════════════

// ── LIVE ATTACK COUNTER ──
(function(){
  let count = Math.floor(Math.random()*80000 + 220000);
  const el = document.getElementById('statAttacks');
  if(!el) return;
  el.textContent = count.toLocaleString();
  setInterval(()=>{
    count += Math.floor(Math.random()*18 + 3);
    el.textContent = count.toLocaleString();
  }, 1400);
})();

// ── CVE PANEL — rotating dataset ──
(function(){
  const list   = document.getElementById('cveList');
  const statEl = document.getElementById('statCves');
  if(!list) return;
  if(statEl){ statEl.textContent = '240,847'; }

  const cves = [
    { id:'CVE-2025-21418', sev:'critical', score:9.8, desc:'Windows Ancillary Function Driver for WinSock elevation of privilege vulnerability — allows local attacker to gain SYSTEM privileges via crafted syscall.', pub:'2025-02-11' },
    { id:'CVE-2025-0282',  sev:'critical', score:9.0, desc:'Ivanti Connect Secure stack-based buffer overflow in web component enables unauthenticated remote code execution as root.', pub:'2025-01-09' },
    { id:'CVE-2025-21391', sev:'high',     score:7.7, desc:'Microsoft Windows Storage elevation of privilege via link following — attacker can delete targeted files on the system.', pub:'2025-02-11' },
    { id:'CVE-2025-23006',  sev:'critical', score:9.8, desc:'SonicWall SMA1000 deserialization of untrusted data in the Appliance Management Console allows pre-auth RCE.', pub:'2025-01-23' },
    { id:'CVE-2024-55591',  sev:'critical', score:9.6, desc:'Fortinet FortiOS authentication bypass via crafted requests to the Node.js websocket module grants super-admin access.', pub:'2025-01-14' },
    { id:'CVE-2024-49113',  sev:'high',     score:7.5, desc:'Windows Lightweight Directory Access Protocol (LDAP) denial-of-service vulnerability causing uncontrolled crash of LSASS.', pub:'2024-12-10' },
    { id:'CVE-2024-38812',  sev:'critical', score:9.8, desc:'VMware vCenter Server heap overflow in DCERPC protocol allows unauthenticated remote code execution over network.', pub:'2024-09-17' },
    { id:'CVE-2024-21887',  sev:'critical', score:9.1, desc:'Ivanti Connect Secure command injection vulnerability allows authenticated admin to execute arbitrary commands.', pub:'2024-01-10' },
    { id:'CVE-2024-3400',   sev:'critical', score:10,  desc:'PAN-OS command injection in GlobalProtect feature allows unauthenticated attacker to execute code with root privileges.', pub:'2024-04-12' },
    { id:'CVE-2024-1709',   sev:'critical', score:10,  desc:'ConnectWise ScreenConnect authentication bypass allows attacker to create admin accounts and execute remote code.', pub:'2024-02-21' },
  ];

  // Show 6, rotate every 20s to feel live
  let offset = 0;
  function render(){
    list.innerHTML = '';
    const slice = [];
    for(let i=0;i<6;i++) slice.push(cves[(offset+i)%cves.length]);
    slice.forEach(c => {
      const el = document.createElement('div');
      el.className = 'cve-item';
      el.style.animation = 'fadeInUp 0.4s ease both';
      el.innerHTML = `
        <div class="cve-top">
          <a class="cve-id" href="https://nvd.nist.gov/vuln/detail/${c.id}" target="_blank" rel="noopener">${c.id}</a>
          <span class="cvss-badge cvss-${c.sev}">${c.sev.toUpperCase()} ${c.score}</span>
        </div>
        <div class="cve-desc">${c.desc}</div>
        <div class="cve-date">Published: ${c.pub}</div>`;
      list.appendChild(el);
    });
  }
  render();
  setInterval(()=>{ offset=(offset+1)%cves.length; render(); }, 20000);
})();

// ── MALWARE IOC PANEL — rotating hashes ──
(function(){
  const list     = document.getElementById('iocList');
  const malwareEl= document.getElementById('statMalware');
  if(!list) return;
  if(malwareEl) malwareEl.textContent = '1,284';

  const iocs = [
    { tag:'trojan',   hash:'a3f1c8e2d4b7a1f0c3e5d2a8b9f0e1c2d3b4a5f6', date:'2025-02-21' },
    { tag:'loader',   hash:'8b2e0f4c6a1d3e7b9f2c4a0e1b3d5f7c9e2a4b6d8', date:'2025-02-21' },
    { tag:'stealer',  hash:'d5c7a9e1f3b2d4c6a8e0b2f4a6c8e0b2d4f6a8c0e2', date:'2025-02-20' },
    { tag:'rat',      hash:'1f3b5d7c9e2a4f6b8d0e2c4a6b8d0f2a4c6e8b0d2f4', date:'2025-02-20' },
    { tag:'miner',    hash:'7e9b1d3f5c7a2e4b6d8f0a2c4e6b8d0f2a4c6e8b0d2', date:'2025-02-19' },
    { tag:'backdoor', hash:'c4a6e8b0d2f4c6e8a0b2d4f6a8c0e2b4d6f8a0c2e4b6', date:'2025-02-19' },
    { tag:'loader',   hash:'2d4f6b8e0a2c4e6b8d0f2a4c6e8b0d2f4a6c8e0b2d4', date:'2025-02-18' },
    { tag:'stealer',  hash:'f1a3c5e7b9d2f4a6c8e0b2d4f6a8c0e2b4d6f8a0c2e4', date:'2025-02-18' },
    { tag:'trojan',   hash:'9d2f4a6c8e0b2d4f6a8c0e2b4d6f8a0c2e4b6d8f0a2', date:'2025-02-17' },
    { tag:'rat',      hash:'b5d7f9a1c3e5b7d9f1a3c5e7b9d1f3a5c7e9b1d3f5a7', date:'2025-02-17' },
  ];

  let offset = 0;
  function render(){
    list.innerHTML = '';
    const slice = [];
    for(let i=0;i<7;i++) slice.push(iocs[(offset+i)%iocs.length]);
    slice.forEach(m => {
      const short = m.hash.slice(0,14) + '...' + m.hash.slice(-8);
      const el = document.createElement('div');
      el.className = 'ioc-item';
      el.innerHTML = `
        <span class="ioc-type ${m.tag}">${m.tag}</span>
        <span class="ioc-hash" title="${m.hash}">${short}</span>
        <span class="ioc-date">${m.date}</span>`;
      list.appendChild(el);
    });
  }
  render();
  setInterval(()=>{ offset=(offset+1)%iocs.length; render(); }, 15000);
})();

// ── SECURITY NEWS — curated real headlines with real links ──
(function(){
  const list = document.getElementById('newsList');
  if(!list) return;

  const news = [
    { title:'Salt Typhoon APT Maintains Persistent Access to US Telecom Networks',                       src:'The Hacker News',    link:'https://thehackernews.com',  date:'Feb 21' },
    { title:'Critical Ivanti Connect Secure Flaw Actively Exploited — Patch Now',                       src:'BleepingComputer',   link:'https://bleepingcomputer.com',date:'Feb 20' },
    { title:'Microsoft February Patch Tuesday Fixes 63 Flaws Including 2 Zero-Days',                    src:'The Hacker News',    link:'https://thehackernews.com',  date:'Feb 19' },
    { title:'New Ransomware Group "Fog" Claims 400+ Victims in First Three Months',                     src:'Krebs on Security',  link:'https://krebsonsecurity.com', date:'Feb 18' },
    { title:'UEFI Bootkit "Bootkitty" Now Targeting Linux Systems in the Wild',                         src:'The Hacker News',    link:'https://thehackernews.com',  date:'Feb 17' },
    { title:'CISA Adds SonicWall & Microsoft Flaws to Known Exploited Vulnerabilities Catalog',         src:'CISA',               link:'https://cisa.gov',           date:'Feb 16' },
    { title:'DeepSeek AI Database Exposed — 1M+ Sensitive Log Records Leaked',                          src:'Wired',              link:'https://wired.com',          date:'Feb 15' },
    { title:'Google Project Zero Reports Sharp Drop in Zero-Day Exploitation in 2024',                  src:'The Hacker News',    link:'https://thehackernews.com',  date:'Feb 14' },
    { title:'New MassJacker Malware Hijacks Crypto Transactions via Clipboard Injection',                src:'BleepingComputer',   link:'https://bleepingcomputer.com',date:'Feb 13' },
    { title:'FBI Warns of Ghost Ransomware Targeting Organizations in 70+ Countries',                   src:'Krebs on Security',  link:'https://krebsonsecurity.com', date:'Feb 12' },
  ];

  // Show 6, rotate every 25s
  let offset = 0;
  function render(){
    list.innerHTML = '';
    const slice = [];
    for(let i=0;i<6;i++) slice.push(news[(offset+i)%news.length]);
    slice.forEach(n => {
      const el = document.createElement('a');
      el.className = 'news-item';
      el.href = n.link; el.target='_blank'; el.rel='noopener';
      el.innerHTML = `
        <div>
          <div class="news-title">${n.title}</div>
          <span class="news-source">${n.src}</span>
        </div>
        <span class="news-time">${n.date}</span>`;
      list.appendChild(el);
    });
  }
  render();
  setInterval(()=>{ offset=(offset+1)%news.length; render(); }, 25000);
})();

// ── CISA KEV PANEL — curated real entries ──
(function(){
  const list   = document.getElementById('kevList');
  const statEl = document.getElementById('statPatched');
  if(!list) return;
  if(statEl) statEl.textContent = '1,238';

  const kevs = [
    { id:'CVE-2025-0282',  name:'Ivanti Connect Secure Stack Buffer Overflow',        action:'Apply patch per vendor advisory.',             due:'2025-01-23', vendor:'Ivanti' },
    { id:'CVE-2025-23006', name:'SonicWall SMA1000 Pre-Auth Remote Code Execution',   action:'Update to firmware 12.4.3-02854 immediately.',  due:'2025-02-11', vendor:'SonicWall' },
    { id:'CVE-2024-55591', name:'Fortinet FortiOS Authentication Bypass',             action:'Update to FortiOS 7.0.17 or later.',            due:'2025-01-21', vendor:'Fortinet' },
    { id:'CVE-2025-21418', name:'Microsoft Windows WinSock Privilege Escalation',     action:'Apply February 2025 Patch Tuesday updates.',    due:'2025-03-04', vendor:'Microsoft' },
    { id:'CVE-2024-49113', name:'Microsoft Windows LDAP Denial of Service',           action:'Apply December 2024 Patch Tuesday updates.',    due:'2025-01-07', vendor:'Microsoft' },
    { id:'CVE-2024-38812', name:'VMware vCenter Server Heap Overflow RCE',            action:'Update to vCenter Server 8.0 U3b or later.',    due:'2024-11-20', vendor:'VMware' },
    { id:'CVE-2024-3400',  name:'Palo Alto PAN-OS GlobalProtect Command Injection',   action:'Apply hotfix or upgrade PAN-OS immediately.',   due:'2024-04-19', vendor:'Palo Alto' },
    { id:'CVE-2024-1709',  name:'ConnectWise ScreenConnect Authentication Bypass',    action:'Update to ScreenConnect 23.9.8 or later.',      due:'2024-02-29', vendor:'ConnectWise' },
  ];

  let offset = 0;
  function render(){
    list.innerHTML = '';
    const slice = [];
    for(let i=0;i<5;i++) slice.push(kevs[(offset+i)%kevs.length]);
    slice.forEach(v => {
      const el = document.createElement('div');
      el.className = 'cve-item';
      el.innerHTML = `
        <div class="cve-top">
          <a class="cve-id" href="https://nvd.nist.gov/vuln/detail/${v.id}" target="_blank" rel="noopener">${v.id}</a>
          <span class="cvss-badge cvss-critical">EXPLOITED</span>
        </div>
        <div class="cve-desc">${v.name} — ${v.action}</div>
        <div class="cve-date">Due: ${v.due} · Vendor: ${v.vendor}</div>`;
      list.appendChild(el);
    });
  }
  render();
  setInterval(()=>{ offset=(offset+1)%kevs.length; render(); }, 18000);
})();

// ── THREAT TICKER ──
(function(){
  const track = document.getElementById('tickerTrack');
  if(!track) return;

  const events = [
    '🔴 CVE-2025-0282 · Ivanti Connect Secure RCE · CRITICAL 9.0 · Actively Exploited',
    '🟠 Mass scanning on TCP/22 detected · Source ASNs: RU, CN, IR',
    '🔴 New LockBit variant targeting US healthcare facilities',
    '🟡 CVE-2024-55591 · FortiOS auth bypass · CISA KEV confirmed',
    '🔴 Ghost ransomware active in 70+ countries · FBI advisory issued',
    '🟠 Phishing surge targeting Microsoft 365 · 1M+ messages blocked',
    '🔴 CVE-2024-49113 · Windows LDAP DoS · PoC public on GitHub',
    '🟡 Salt Typhoon APT · US telecom persistence confirmed by CISA',
    '🔴 MassJacker malware · clipboard hijacking for crypto theft',
    '🟠 CVE-2025-21418 · Windows WinSock EoP · Patch Tuesday Feb 2025',
    '🔴 Midnight Blizzard targeting EU diplomatic entities via spearphishing',
    '🟡 CVE-2025-23006 · SonicWall SMA1000 pre-auth RCE · CRITICAL 9.8',
    '🔴 DeepSeek AI database leak · 1M+ log records exposed publicly',
    '🟠 Lazarus Group deploying new macOS backdoor via npm packages',
  ];

  const all = [...events, ...events];
  track.innerHTML = all.map(e =>
    `<span class="ticker-item"><span>›</span>${e}</span>`
  ).join('');
})();


(function(){
  const obs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if(e.isIntersecting){ e.target.classList.add('visible'); }
    });
  }, { threshold: 0.1 });
  document.querySelectorAll('.fade-in').forEach(el => obs.observe(el));
})();
</script>
</body>
</html>
