<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Matias Aguirre — README</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --border: #1e1e2e;
    --accent: #7fffb2;
    --accent2: #ff6b6b;
    --accent3: #6bcbff;
    --text: #e8e8f0;
    --muted: #5a5a7a;
    --font-mono: 'Space Mono', monospace;
    --font-display: 'Syne', sans-serif;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-mono);
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    position: fixed;
    width: 10px; height: 10px;
    background: var(--accent);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    transition: width 0.2s, height 0.2s, background 0.2s;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    position: fixed;
    width: 36px; height: 36px;
    border: 1px solid var(--accent);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: all 0.12s ease;
    opacity: 0.5;
  }

  /* Grid background */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(127,255,178,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(127,255,178,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  .container {
    max-width: 860px;
    margin: 0 auto;
    padding: 60px 24px 120px;
    position: relative;
    z-index: 1;
  }

  /* ── HEADER ── */
  .header {
    border: 1px solid var(--border);
    padding: 40px;
    margin-bottom: 32px;
    position: relative;
    overflow: hidden;
    opacity: 0;
    transform: translateY(30px);
    animation: fadeUp 0.8s ease forwards 0.1s;
  }

  .header::before {
    content: '';
    position: absolute;
    top: -80px; left: -80px;
    width: 300px; height: 300px;
    background: radial-gradient(circle, rgba(127,255,178,0.08) 0%, transparent 70%);
    pointer-events: none;
  }

  .header-top {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    gap: 24px;
    flex-wrap: wrap;
  }

  .name-block h1 {
    font-family: var(--font-display);
    font-size: clamp(2.2rem, 5vw, 3.5rem);
    font-weight: 800;
    line-height: 1;
    letter-spacing: -0.02em;
    color: #fff;
  }

  .name-block h1 span {
    color: var(--accent);
  }

  .name-block .title {
    font-size: 0.75rem;
    color: var(--muted);
    margin-top: 10px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
  }

  .status-badge {
    display: flex;
    align-items: center;
    gap: 8px;
    background: rgba(127,255,178,0.06);
    border: 1px solid rgba(127,255,178,0.2);
    padding: 8px 14px;
    font-size: 0.7rem;
    letter-spacing: 0.1em;
    color: var(--accent);
    white-space: nowrap;
    margin-top: 4px;
  }

  .status-dot {
    width: 6px; height: 6px;
    background: var(--accent);
    border-radius: 50%;
    animation: pulse 2s infinite;
  }

  .bio {
    margin-top: 28px;
    font-size: 0.875rem;
    line-height: 1.8;
    color: #9090b0;
    max-width: 600px;
  }

  .bio strong {
    color: var(--text);
    font-weight: 700;
  }

  /* ── STATS ROW ── */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: 12px;
    margin-bottom: 32px;
    opacity: 0;
    transform: translateY(30px);
    animation: fadeUp 0.8s ease forwards 0.25s;
  }

  .stat-card {
    border: 1px solid var(--border);
    padding: 20px 16px;
    text-align: center;
    transition: border-color 0.3s, transform 0.3s;
    position: relative;
    overflow: hidden;
  }

  .stat-card::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 2px;
    background: var(--accent);
    transform: scaleX(0);
    transition: transform 0.3s ease;
  }

  .stat-card:hover {
    border-color: rgba(127,255,178,0.3);
    transform: translateY(-3px);
  }

  .stat-card:hover::after {
    transform: scaleX(1);
  }

  .stat-value {
    font-family: var(--font-display);
    font-size: 1.8rem;
    font-weight: 800;
    color: var(--accent);
    display: block;
    counter-reset: none;
  }

  .stat-label {
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-top: 4px;
    display: block;
  }

  /* ── SECTION ── */
  .section {
    border: 1px solid var(--border);
    margin-bottom: 20px;
    opacity: 0;
    transform: translateY(30px);
  }

  .section.visible {
    animation: fadeUp 0.7s ease forwards;
  }

  .section-header {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 14px 24px;
    border-bottom: 1px solid var(--border);
    cursor: pointer;
    user-select: none;
    transition: background 0.2s;
  }

  .section-header:hover {
    background: rgba(255,255,255,0.02);
  }

  .section-tag {
    font-size: 0.6rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--accent);
    background: rgba(127,255,178,0.08);
    padding: 3px 8px;
    border: 1px solid rgba(127,255,178,0.15);
  }

  .section-title {
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 0.95rem;
    color: var(--text);
    flex: 1;
  }

  .chevron {
    color: var(--muted);
    font-size: 0.75rem;
    transition: transform 0.3s;
  }

  .section-body {
    padding: 24px;
    display: grid;
    gap: 12px;
    overflow: hidden;
    max-height: 2000px;
    transition: max-height 0.4s ease, padding 0.3s;
  }

  .section-body.collapsed {
    max-height: 0;
    padding-top: 0;
    padding-bottom: 0;
  }

  .chevron.rotated { transform: rotate(180deg); }

  /* ── TECH STACK ── */
  .tech-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .tech-pill {
    font-size: 0.7rem;
    padding: 5px 12px;
    border: 1px solid var(--border);
    color: var(--muted);
    letter-spacing: 0.05em;
    transition: all 0.25s;
    position: relative;
    overflow: hidden;
  }

  .tech-pill::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--pill-color, var(--accent));
    opacity: 0;
    transition: opacity 0.25s;
  }

  .tech-pill:hover {
    border-color: var(--pill-color, var(--accent));
    color: var(--pill-color, var(--accent));
    transform: translateY(-2px);
  }

  /* ── PROJECT CARD ── */
  .project-card {
    border: 1px solid var(--border);
    padding: 20px;
    transition: border-color 0.3s, transform 0.3s;
    position: relative;
    overflow: hidden;
  }

  .project-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 3px;
    height: 100%;
    background: var(--accent);
    transform: scaleY(0);
    transform-origin: bottom;
    transition: transform 0.3s ease;
  }

  .project-card:hover {
    border-color: rgba(127,255,178,0.25);
    transform: translateX(4px);
  }

  .project-card:hover::before {
    transform: scaleY(1);
  }

  .project-name {
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 1rem;
    color: #fff;
    margin-bottom: 6px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .project-name .dot {
    width: 6px; height: 6px;
    background: var(--accent);
    border-radius: 50%;
    flex-shrink: 0;
  }

  .project-desc {
    font-size: 0.78rem;
    color: #7070a0;
    line-height: 1.7;
    margin-bottom: 12px;
  }

  .project-tags {
    display: flex;
    gap: 6px;
    flex-wrap: wrap;
  }

  .tag {
    font-size: 0.6rem;
    padding: 2px 8px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  .tag-green { border: 1px solid rgba(127,255,178,0.3); color: var(--accent); }
  .tag-red   { border: 1px solid rgba(255,107,107,0.3); color: var(--accent2); }
  .tag-blue  { border: 1px solid rgba(107,203,255,0.3); color: var(--accent3); }

  /* ── TERMINAL BLOCK ── */
  .terminal {
    background: #080810;
    border: 1px solid var(--border);
    padding: 20px 24px;
    font-size: 0.78rem;
    line-height: 2;
    position: relative;
  }

  .terminal::before {
    content: '● ● ●';
    position: absolute;
    top: 12px; left: 16px;
    font-size: 0.55rem;
    letter-spacing: 4px;
    color: var(--muted);
    opacity: 0.5;
  }

  .terminal-inner {
    margin-top: 12px;
  }

  .t-prompt { color: var(--accent); }
  .t-cmd    { color: var(--text); }
  .t-out    { color: var(--muted); }
  .t-highlight { color: var(--accent3); }

  .typing::after {
    content: '▌';
    animation: blink 1s step-end infinite;
  }

  /* ── CONTACT ── */
  .contact-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 10px;
  }

  .contact-item {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 14px 16px;
    border: 1px solid var(--border);
    text-decoration: none;
    color: var(--muted);
    font-size: 0.75rem;
    transition: all 0.25s;
  }

  .contact-item:hover {
    border-color: rgba(127,255,178,0.3);
    color: var(--accent);
    transform: translateY(-2px);
  }

  .contact-icon {
    font-size: 1rem;
    flex-shrink: 0;
  }

  /* ── SKILLS BAR ── */
  .skill-row {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 8px 0;
    border-bottom: 1px solid rgba(255,255,255,0.03);
  }

  .skill-name {
    font-size: 0.72rem;
    color: var(--muted);
    width: 120px;
    flex-shrink: 0;
  }

  .skill-bar-track {
    flex: 1;
    height: 3px;
    background: rgba(255,255,255,0.05);
    position: relative;
    overflow: hidden;
  }

  .skill-bar-fill {
    height: 100%;
    background: var(--accent);
    width: 0%;
    transition: width 1.2s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
  }

  .skill-bar-fill::after {
    content: '';
    position: absolute;
    right: 0; top: -2px;
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--accent);
    box-shadow: 0 0 8px var(--accent);
  }

  .skill-pct {
    font-size: 0.65rem;
    color: var(--accent);
    width: 30px;
    text-align: right;
  }

  /* ── FOOTER ── */
  .footer {
    text-align: center;
    padding-top: 48px;
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.15em;
    opacity: 0;
    animation: fadeUp 0.8s ease forwards 1s;
  }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; box-shadow: 0 0 0 0 rgba(127,255,178,0.4); }
    50% { opacity: 0.7; box-shadow: 0 0 0 6px rgba(127,255,178,0); }
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  @keyframes scanline {
    0% { transform: translateY(-100%); }
    100% { transform: translateY(100vh); }
  }

  .scanline {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(transparent, rgba(127,255,178,0.04), transparent);
    pointer-events: none;
    animation: scanline 6s linear infinite;
    z-index: 2;
  }

  /* SCROLL REVEAL */
  .reveal { opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease, transform 0.6s ease; }
  .reveal.in { opacity: 1; transform: translateY(0); }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>
<div class="scanline"></div>

<div class="container">

  <!-- HEADER -->
  <div class="header">
    <div class="header-top">
      <div class="name-block">
        <h1>Matias<br><span>Aguirre</span></h1>
        <p class="title">Full Stack Developer · Medellín, CO</p>
      </div>
      <div class="status-badge">
        <span class="status-dot"></span>
        Open to work
      </div>
    </div>
    <p class="bio">
      Student at <strong>RIWI</strong> building full-stack apps with <strong>Next.js 15</strong>, <strong>Prisma 7</strong> and <strong>PostgreSQL on Neon</strong>.
      Currently shipping <strong>EmbeddingAndTransformerTranslator</strong> — an AI workspace that runs transformer classification and semantic embeddings via HuggingFace Inference API, deployed on <strong>Vercel</strong>.
      Comfortable debugging Prisma v7 breaking changes at 7am.
    </p>
  </div>

  <!-- STATS -->
  <div class="stats-row">
    <div class="stat-card">
      <span class="stat-value" data-target="500">0</span>
      <span class="stat-label">Errors debugged</span>
    </div>
    <div class="stat-card">
      <span class="stat-value" data-target="3">0</span>
      <span class="stat-label">Deploys today</span>
    </div>
    <div class="stat-card">
      <span class="stat-value" data-target="7">0</span>
      <span class="stat-label">Prisma versions</span>
    </div>
    <div class="stat-card">
      <span class="stat-value" data-target="1">0</span>
      <span class="stat-label">Coffees/hr</span>
    </div>
  </div>

  <!-- TERMINAL -->
  <div class="section reveal" style="animation-delay:0.1s">
    <div class="section-header" onclick="toggle(this)">
      <span class="section-tag">SYS</span>
      <span class="section-title">whoami</span>
      <span class="chevron">▼</span>
    </div>
    <div class="section-body">
      <div class="terminal">
        <div class="terminal-inner">
          <div><span class="t-prompt">matias@riwi</span><span class="t-cmd"> ~ $ cat profile.json</span></div>
          <div class="t-out">{</div>
          <div class="t-out">&nbsp;&nbsp;<span class="t-highlight">"name"</span>: "Matias Aguirre Correa",</div>
          <div class="t-out">&nbsp;&nbsp;<span class="t-highlight">"role"</span>: "Full Stack Developer",</div>
          <div class="t-out">&nbsp;&nbsp;<span class="t-highlight">"location"</span>: "Medellín, Antioquia, CO",</div>
          <div class="t-out">&nbsp;&nbsp;<span class="t-highlight">"program"</span>: "RIWI · Cohorte 5",</div>
          <div class="t-out">&nbsp;&nbsp;<span class="t-highlight">"stack"</span>: ["Next.js", "Prisma", "PostgreSQL", "TypeScript"],</div>
          <div class="t-out">&nbsp;&nbsp;<span class="t-highlight">"currently"</span>: "Deploying to Vercel at 10am",</div>
          <div class="t-out">&nbsp;&nbsp;<span class="t-highlight">"superpower"</span>: "Doesn't give up on P1001 errors"</div>
          <div class="t-out">}</div>
          <div><span class="t-prompt">matias@riwi</span><span class="t-cmd typing"> ~ $ </span></div>
        </div>
      </div>
    </div>
  </div>

  <!-- TECH STACK -->
  <div class="section reveal" style="animation-delay:0.15s">
    <div class="section-header" onclick="toggle(this)">
      <span class="section-tag">STACK</span>
      <span class="section-title">Tech I work with</span>
      <span class="chevron">▼</span>
    </div>
    <div class="section-body">
      <p style="font-size:0.7rem;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase;margin-bottom:4px">Frontend</p>
      <div class="tech-grid">
        <span class="tech-pill" style="--pill-color:#61dafb">React</span>
        <span class="tech-pill" style="--pill-color:#000">Next.js 15</span>
        <span class="tech-pill" style="--pill-color:#3178c6">TypeScript</span>
        <span class="tech-pill" style="--pill-color:#06b6d4">Tailwind CSS</span>
        <span class="tech-pill" style="--pill-color:#e34f26">HTML5</span>
      </div>
      <p style="font-size:0.7rem;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase;margin-bottom:4px;margin-top:16px">Backend</p>
      <div class="tech-grid">
        <span class="tech-pill" style="--pill-color:#3178c6">Node.js</span>
        <span class="tech-pill" style="--pill-color:#2d3748">Prisma 7</span>
        <span class="tech-pill" style="--pill-color:#336791">PostgreSQL</span>
        <span class="tech-pill" style="--pill-color:#00e5be">Neon DB</span>
        <span class="tech-pill" style="--pill-color:#7fffb2">Zod</span>
        <span class="tech-pill" style="--pill-color:#ff6b6b">bcrypt</span>
      </div>
      <p style="font-size:0.7rem;color:var(--muted);letter-spacing:0.1em;text-transform:uppercase;margin-bottom:4px;margin-top:16px">AI / Infra</p>
      <div class="tech-grid">
        <span class="tech-pill" style="--pill-color:#ffd700">HuggingFace</span>
        <span class="tech-pill" style="--pill-color:#000">Vercel</span>
        <span class="tech-pill" style="--pill-color:#f05032">Git</span>
        <span class="tech-pill" style="--pill-color:#2088ff">GitHub</span>
        <span class="tech-pill" style="--pill-color:#007acc">VS Code</span>
      </div>
    </div>
  </div>

  <!-- SKILLS -->
  <div class="section reveal" style="animation-delay:0.2s">
    <div class="section-header" onclick="toggle(this)">
      <span class="section-tag">SKILLS</span>
      <span class="section-title">Proficiency</span>
      <span class="chevron">▼</span>
    </div>
    <div class="section-body" id="skillsBody">
      <div class="skill-row"><span class="skill-name">Next.js / React</span><div class="skill-bar-track"><div class="skill-bar-fill" data-pct="88"></div></div><span class="skill-pct">88%</span></div>
      <div class="skill-row"><span class="skill-name">TypeScript</span><div class="skill-bar-track"><div class="skill-bar-fill" data-pct="82"></div></div><span class="skill-pct">82%</span></div>
      <div class="skill-row"><span class="skill-name">Prisma / ORM</span><div class="skill-bar-track"><div class="skill-bar-fill" data-pct="78"></div></div><span class="skill-pct">78%</span></div>
      <div class="skill-row"><span class="skill-name">PostgreSQL</span><div class="skill-bar-track"><div class="skill-bar-fill" data-pct="74"></div></div><span class="skill-pct">74%</span></div>
      <div class="skill-row"><span class="skill-name">API Design</span><div class="skill-bar-track"><div class="skill-bar-fill" data-pct="80"></div></div><span class="skill-pct">80%</span></div>
      <div class="skill-row"><span class="skill-name">Auth / JWT</span><div class="skill-bar-track"><div class="skill-bar-fill" data-pct="72"></div></div><span class="skill-pct">72%</span></div>
      <div class="skill-row"><span class="skill-name">Debugging 🔥</span><div class="skill-bar-track"><div class="skill-bar-fill" data-pct="99"></div></div><span class="skill-pct">99%</span></div>
    </div>
  </div>

  <!-- PROJECTS -->
  <div class="section reveal" style="animation-delay:0.25s">
    <div class="section-header" onclick="toggle(this)">
      <span class="section-tag">WORK</span>
      <span class="section-title">Featured Projects</span>
      <span class="chevron">▼</span>
    </div>
    <div class="section-body">

      <div class="project-card">
        <div class="project-name"><span class="dot"></span>EmbeddingAndTransformerTranslator</div>
        <p class="project-desc">Full-stack AI workspace for text analysis. Authenticated users can run transformer-based sentiment classification and generate semantic embedding vectors using HuggingFace models. Built with Next.js App Router, Prisma 7, Neon PostgreSQL, and deployed on Vercel.</p>
        <div class="project-tags">
          <span class="tag tag-green">Next.js 15</span>
          <span class="tag tag-blue">Prisma 7</span>
          <span class="tag tag-blue">Neon DB</span>
          <span class="tag tag-green">HuggingFace API</span>
          <span class="tag tag-red">Vercel</span>
          <span class="tag tag-green">Auth</span>
        </div>
      </div>

    </div>
  </div>

  <!-- CONTACT -->
  <div class="section reveal" style="animation-delay:0.3s">
    <div class="section-header" onclick="toggle(this)">
      <span class="section-tag">CONTACT</span>
      <span class="section-title">Get in touch</span>
      <span class="chevron">▼</span>
    </div>
    <div class="section-body">
      <div class="contact-grid">
        <a class="contact-item" href="mailto:matiasaguirrecorrea@gmail.com">
          <span class="contact-icon">✉</span>
          <span>matiasaguirrecorrea<br>@gmail.com</span>
        </a>
        <a class="contact-item" href="https://github.com/MatiasAC110508" target="_blank">
          <span class="contact-icon">⌥</span>
          <span>github.com/<br>MatiasAC110508</span>
        </a>
        <a class="contact-item" href="#">
          <span class="contact-icon">◈</span>
          <span>Medellín,<br>Colombia 🇨🇴</span>
        </a>
      </div>
    </div>
  </div>

  <div class="footer">
    README generated — 2026 · Matias Aguirre · RIWI Cohorte 5<br>
    <span style="color:var(--accent)">↑</span> built with Next.js · Prisma · Neon · Vercel · and perseverance
  </div>

</div>

<script>
// Cursor
const cursor = document.getElementById('cursor');
const ring = document.getElementById('cursorRing');
let mx = 0, my = 0, rx = 0, ry = 0;

document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.left = mx + 'px';
  cursor.style.top  = my + 'px';
});

function animRing() {
  rx += (mx - rx) * 0.12;
  ry += (my - ry) * 0.12;
  ring.style.left = rx + 'px';
  ring.style.top  = ry + 'px';
  requestAnimationFrame(animRing);
}
animRing();

document.querySelectorAll('a, button, .section-header, .stat-card, .project-card, .tech-pill').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.width = '18px'; cursor.style.height = '18px';
    cursor.style.background = '#ff6b6b';
  });
  el.addEventListener('mouseleave', () => {
    cursor.style.width = '10px'; cursor.style.height = '10px';
    cursor.style.background = 'var(--accent)';
  });
});

// Toggle sections
function toggle(header) {
  const body = header.nextElementSibling;
  const chevron = header.querySelector('.chevron');
  body.classList.toggle('collapsed');
  chevron.classList.toggle('rotated');
  // Animate skill bars when opened
  if (!body.classList.contains('collapsed')) {
    body.querySelectorAll('.skill-bar-fill').forEach(bar => {
      bar.style.width = bar.dataset.pct + '%';
    });
  }
}

// Counter animation
function animateCounters() {
  document.querySelectorAll('[data-target]').forEach(el => {
    const target = +el.dataset.target;
    let current = 0;
    const step = target / 40;
    const timer = setInterval(() => {
      current = Math.min(current + step, target);
      el.textContent = Math.floor(current);
      if (current >= target) clearInterval(timer);
    }, 30);
  });
}

// Scroll reveal
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('in');
      // Trigger skill bars if visible
      e.target.querySelectorAll('.skill-bar-fill').forEach(bar => {
        setTimeout(() => bar.style.width = bar.dataset.pct + '%', 300);
      });
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

// Start counters after short delay
setTimeout(animateCounters, 600);
</script>
</body>
</html>
