<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>D10R_JURAEV // CYBERDECK TERMINAL</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;500;600;700&display=swap');

  :root {
    --cyan: #00f0ff;
    --magenta: #ff00de;
    --green: #39ff14;
    --yellow: #ffe600;
    --red: #ff003c;
    --dark-bg: #0a0a0f;
    --panel-bg: rgba(10, 10, 20, 0.85);
    --border-glow: rgba(0, 240, 255, 0.3);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--dark-bg);
    color: #e0e0e0;
    font-family: 'Rajdhani', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ANIMATED BACKGROUND */
  .bg-grid {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    background:
      linear-gradient(rgba(0,240,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,240,255,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    animation: gridScroll 20s linear infinite;
  }

  @keyframes gridScroll {
    0% { transform: translate(0, 0); }
    100% { transform: translate(40px, 40px); }
  }

  .scanline {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 1;
    pointer-events: none;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0, 240, 255, 0.015) 2px,
      rgba(0, 240, 255, 0.015) 4px
    );
  }

  .scan-beam {
    position: fixed;
    top: -100%;
    left: 0;
    width: 100%;
    height: 200px;
    background: linear-gradient(180deg, transparent, rgba(0,240,255,0.04), transparent);
    z-index: 1;
    pointer-events: none;
    animation: scanBeam 8s ease-in-out infinite;
  }

  @keyframes scanBeam {
    0% { top: -200px; }
    100% { top: 120%; }
  }

  /* FLOATING PARTICLES */
  .particles {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    overflow: hidden;
  }

  .particle {
    position: absolute;
    width: 2px;
    height: 2px;
    background: var(--cyan);
    border-radius: 50%;
    opacity: 0;
    animation: float 6s ease-in-out infinite;
  }

  @keyframes float {
    0% { opacity: 0; transform: translateY(100vh) scale(0); }
    50% { opacity: 0.8; }
    100% { opacity: 0; transform: translateY(-10vh) scale(1); }
  }

  /* MAIN CONTAINER */
  .container {
    position: relative;
    z-index: 2;
    max-width: 1400px;
    margin: 0 auto;
    padding: 20px;
  }

  /* HEADER */
  .header {
    text-align: center;
    padding: 40px 20px 30px;
    position: relative;
  }

  .header::before {
    content: '[ CYBERDECK TERMINAL v4.2.0 // SECURE CONNECTION ESTABLISHED ]';
    display: block;
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: var(--green);
    letter-spacing: 3px;
    margin-bottom: 20px;
    animation: flicker 3s infinite;
  }

  @keyframes flicker {
    0%, 100% { opacity: 1; }
    92% { opacity: 1; }
    93% { opacity: 0.3; }
    94% { opacity: 1; }
    96% { opacity: 0.5; }
    97% { opacity: 1; }
  }

  .avatar-container {
    position: relative;
    display: inline-block;
    margin-bottom: 20px;
  }

  .avatar {
    width: 140px;
    height: 140px;
    border-radius: 50%;
    border: 3px solid var(--cyan);
    box-shadow: 0 0 30px rgba(0,240,255,0.4), 0 0 60px rgba(0,240,255,0.1), inset 0 0 20px rgba(0,240,255,0.1);
    animation: avatarPulse 3s ease-in-out infinite;
    position: relative;
    z-index: 2;
  }

  @keyframes avatarPulse {
    0%, 100% { box-shadow: 0 0 30px rgba(0,240,255,0.4), 0 0 60px rgba(0,240,255,0.1); }
    50% { box-shadow: 0 0 40px rgba(0,240,255,0.6), 0 0 80px rgba(0,240,255,0.2), 0 0 120px rgba(255,0,222,0.1); }
  }

  .avatar-ring {
    position: absolute;
    top: -8px; left: -8px;
    width: 156px; height: 156px;
    border: 1px solid rgba(0,240,255,0.3);
    border-radius: 50%;
    animation: spin 10s linear infinite;
  }

  .avatar-ring::before {
    content: '';
    position: absolute;
    top: -3px; left: 50%;
    width: 6px; height: 6px;
    background: var(--cyan);
    border-radius: 50%;
    box-shadow: 0 0 10px var(--cyan);
  }

  @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

  .username {
    font-family: 'Orbitron', sans-serif;
    font-size: 2.8em;
    font-weight: 900;
    background: linear-gradient(135deg, var(--cyan), var(--magenta));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    text-shadow: none;
    letter-spacing: 4px;
    text-transform: uppercase;
  }

  .bio {
    font-family: 'Share Tech Mono', monospace;
    font-size: 14px;
    color: var(--green);
    margin-top: 8px;
    letter-spacing: 1.5px;
  }

  .status-line {
    font-family: 'Share Tech Mono', monospace;
    font-size: 12px;
    color: var(--yellow);
    margin-top: 12px;
    animation: blink 1.5s step-end infinite;
  }

  @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

  .location-bar {
    display: flex;
    justify-content: center;
    gap: 30px;
    margin-top: 15px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 12px;
    color: rgba(255,255,255,0.5);
  }

  .location-bar a {
    color: var(--cyan);
    text-decoration: none;
    transition: all 0.3s;
  }

  .location-bar a:hover {
    color: var(--magenta);
    text-shadow: 0 0 10px var(--magenta);
  }

  /* STATS GRID */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 15px;
    margin: 30px 0;
  }

  .stat-card {
    background: var(--panel-bg);
    border: 1px solid var(--border-glow);
    padding: 20px;
    text-align: center;
    position: relative;
    overflow: hidden;
    transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
  }

  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: -100%;
    width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(0,240,255,0.05), transparent);
    transition: left 0.6s;
  }

  .stat-card:hover::before { left: 100%; }

  .stat-card:hover {
    border-color: var(--cyan);
    box-shadow: 0 0 20px rgba(0,240,255,0.15), inset 0 0 20px rgba(0,240,255,0.05);
    transform: translateY(-3px);
  }

  .stat-number {
    font-family: 'Orbitron', sans-serif;
    font-size: 2.5em;
    font-weight: 900;
    color: var(--cyan);
    text-shadow: 0 0 20px rgba(0,240,255,0.5);
    line-height: 1;
  }

  .stat-card:nth-child(2) .stat-number { color: var(--magenta); text-shadow: 0 0 20px rgba(255,0,222,0.5); }
  .stat-card:nth-child(3) .stat-number { color: var(--green); text-shadow: 0 0 20px rgba(57,255,20,0.5); }
  .stat-card:nth-child(4) .stat-number { color: var(--yellow); text-shadow: 0 0 20px rgba(255,230,0,0.5); }

  .stat-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: rgba(255,255,255,0.5);
    text-transform: uppercase;
    letter-spacing: 3px;
    margin-top: 8px;
  }

  /* TECH STACK */
  .section-title {
    font-family: 'Orbitron', sans-serif;
    font-size: 1.1em;
    font-weight: 700;
    color: var(--cyan);
    letter-spacing: 4px;
    text-transform: uppercase;
    margin: 35px 0 15px;
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .section-title::before {
    content: '//';
    color: var(--magenta);
    font-family: 'Share Tech Mono', monospace;
  }

  .section-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--border-glow), transparent);
  }

  .tech-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin-bottom: 10px;
  }

  .tech-tag {
    font-family: 'Share Tech Mono', monospace;
    font-size: 12px;
    padding: 6px 16px;
    border: 1px solid;
    position: relative;
    letter-spacing: 1px;
    clip-path: polygon(8px 0, 100% 0, calc(100% - 8px) 100%, 0 100%);
    transition: all 0.3s;
    cursor: default;
  }

  .tech-tag:hover {
    transform: translateY(-2px);
  }

  .tech-tag.python { border-color: #3776ab; color: #3776ab; background: rgba(55,118,171,0.1); }
  .tech-tag.python:hover { background: rgba(55,118,171,0.25); box-shadow: 0 0 15px rgba(55,118,171,0.3); }
  .tech-tag.fastapi { border-color: #009688; color: #009688; background: rgba(0,150,136,0.1); }
  .tech-tag.fastapi:hover { background: rgba(0,150,136,0.25); box-shadow: 0 0 15px rgba(0,150,136,0.3); }
  .tech-tag.js { border-color: #f7df1e; color: #f7df1e; background: rgba(247,223,30,0.1); }
  .tech-tag.js:hover { background: rgba(247,223,30,0.2); box-shadow: 0 0 15px rgba(247,223,30,0.3); }
  .tech-tag.react { border-color: #61dafb; color: #61dafb; background: rgba(97,218,251,0.1); }
  .tech-tag.react:hover { background: rgba(97,218,251,0.2); box-shadow: 0 0 15px rgba(97,218,251,0.3); }
  .tech-tag.linux { border-color: var(--green); color: var(--green); background: rgba(57,255,20,0.08); }
  .tech-tag.linux:hover { background: rgba(57,255,20,0.2); box-shadow: 0 0 15px rgba(57,255,20,0.3); }
  .tech-tag.rpi { border-color: #c51a4a; color: #c51a4a; background: rgba(197,26,74,0.1); }
  .tech-tag.rpi:hover { background: rgba(197,26,74,0.25); box-shadow: 0 0 15px rgba(197,26,74,0.3); }
  .tech-tag.csharp { border-color: #9b4dca; color: #9b4dca; background: rgba(155,77,202,0.1); }
  .tech-tag.csharp:hover { background: rgba(155,77,202,0.25); box-shadow: 0 0 15px rgba(155,77,202,0.3); }
  .tech-tag.java { border-color: #f89820; color: #f89820; background: rgba(248,152,32,0.1); }
  .tech-tag.java:hover { background: rgba(248,152,32,0.25); box-shadow: 0 0 15px rgba(248,152,32,0.3); }
  .tech-tag.powershell { border-color: #5391FE; color: #5391FE; background: rgba(83,145,254,0.1); }
  .tech-tag.powershell:hover { background: rgba(83,145,254,0.25); box-shadow: 0 0 15px rgba(83,145,254,0.3); }

  /* REPOS */
  .repos-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
    gap: 15px;
  }

  .repo-card {
    background: var(--panel-bg);
    border: 1px solid rgba(0,240,255,0.15);
    padding: 20px;
    position: relative;
    overflow: hidden;
    transition: all 0.4s;
    cursor: pointer;
    text-decoration: none;
    display: block;
    clip-path: polygon(0 0, calc(100% - 16px) 0, 100% 16px, 100% 100%, 16px 100%, 0 calc(100% - 16px));
  }

  .repo-card::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0;
    width: 0%; height: 2px;
    background: linear-gradient(90deg, var(--cyan), var(--magenta));
    transition: width 0.4s;
  }

  .repo-card:hover::after { width: 100%; }

  .repo-card:hover {
    border-color: var(--cyan);
    box-shadow: 0 0 25px rgba(0,240,255,0.1), inset 0 0 25px rgba(0,240,255,0.03);
    transform: translateY(-4px);
  }

  .repo-card.original { border-left: 3px solid var(--cyan); }
  .repo-card.forked { border-left: 3px solid var(--magenta); }

  .repo-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 8px;
  }

  .repo-name {
    font-family: 'Orbitron', sans-serif;
    font-size: 0.95em;
    font-weight: 700;
    color: var(--cyan);
    letter-spacing: 1px;
  }

  .repo-card.forked .repo-name { color: var(--magenta); }

  .repo-badge {
    font-family: 'Share Tech Mono', monospace;
    font-size: 9px;
    padding: 2px 8px;
    border: 1px solid;
    letter-spacing: 1px;
    text-transform: uppercase;
  }

  .badge-original { border-color: var(--cyan); color: var(--cyan); }
  .badge-forked { border-color: var(--magenta); color: var(--magenta); }

  .repo-desc {
    font-size: 13px;
    color: rgba(255,255,255,0.55);
    margin-bottom: 12px;
    line-height: 1.4;
    font-family: 'Rajdhani', sans-serif;
  }

  .repo-meta {
    display: flex;
    gap: 15px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: rgba(255,255,255,0.4);
  }

  .repo-lang {
    display: flex;
    align-items: center;
    gap: 5px;
  }

  .lang-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    display: inline-block;
  }

  .lang-Python { background: #3776ab; box-shadow: 0 0 6px #3776ab; }
  .lang-PowerShell { background: #5391FE; box-shadow: 0 0 6px #5391FE; }
  .lang-C { background: #555; box-shadow: 0 0 6px #555; }
  .lang-CSharp { background: #9b4dca; box-shadow: 0 0 6px #9b4dca; }
  .lang-Java { background: #f89820; box-shadow: 0 0 6px #f89820; }
  .lang-HTML { background: #e34c26; box-shadow: 0 0 6px #e34c26; }
  .lang-Jupyter { background: #da5b0b; box-shadow: 0 0 6px #da5b0b; }

  /* LANGUAGE BREAKDOWN BAR */
  .lang-bar-container {
    margin: 20px 0;
    background: var(--panel-bg);
    border: 1px solid var(--border-glow);
    padding: 20px;
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
  }

  .lang-bar {
    height: 8px;
    display: flex;
    border-radius: 4px;
    overflow: hidden;
    margin-bottom: 12px;
    box-shadow: 0 0 10px rgba(0,240,255,0.2);
  }

  .lang-bar div {
    height: 100%;
    transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .lang-legend {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: rgba(255,255,255,0.6);
  }

  .lang-legend-item {
    display: flex;
    align-items: center;
    gap: 5px;
  }

  /* FOOTER */
  .footer {
    text-align: center;
    padding: 40px 20px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: rgba(255,255,255,0.25);
    letter-spacing: 2px;
  }

  .footer .glitch-text {
    color: var(--cyan);
    font-size: 13px;
    animation: glitch 2s infinite;
  }

  @keyframes glitch {
    0%, 100% { text-shadow: 2px 0 var(--magenta), -2px 0 var(--green); }
    25% { text-shadow: -2px 0 var(--magenta), 2px 0 var(--green); }
    50% { text-shadow: 2px 2px var(--magenta), -2px -2px var(--green); }
    75% { text-shadow: -2px 2px var(--magenta), 2px -2px var(--green); }
  }

  /* CATEGORY FILTERS */
  .filter-bar {
    display: flex;
    gap: 10px;
    margin-bottom: 15px;
    flex-wrap: wrap;
  }

  .filter-btn {
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    padding: 6px 16px;
    border: 1px solid rgba(255,255,255,0.2);
    background: transparent;
    color: rgba(255,255,255,0.5);
    cursor: pointer;
    letter-spacing: 1px;
    text-transform: uppercase;
    transition: all 0.3s;
    clip-path: polygon(6px 0, 100% 0, calc(100% - 6px) 100%, 0 100%);
  }

  .filter-btn:hover, .filter-btn.active {
    border-color: var(--cyan);
    color: var(--cyan);
    background: rgba(0,240,255,0.08);
    box-shadow: 0 0 10px rgba(0,240,255,0.2);
  }

  /* HEX DECORATION */
  .hex-decoration {
    position: fixed;
    top: 20px;
    right: 20px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    color: rgba(0,240,255,0.15);
    text-align: right;
    z-index: 1;
    pointer-events: none;
    line-height: 1.6;
  }

  /* TYPING TERMINAL */
  .terminal-box {
    background: rgba(0,0,0,0.6);
    border: 1px solid rgba(0,240,255,0.2);
    padding: 15px 20px;
    margin: 20px 0;
    font-family: 'Share Tech Mono', monospace;
    font-size: 13px;
    color: var(--green);
    position: relative;
    overflow: hidden;
  }

  .terminal-box::before {
    content: 'root@cyberdeck:~$ ';
    color: var(--cyan);
  }

  .terminal-cursor {
    display: inline-block;
    width: 8px;
    height: 14px;
    background: var(--green);
    vertical-align: text-bottom;
    animation: blink 1s step-end infinite;
  }

  /* RESPONSIVE */
  @media (max-width: 768px) {
    .stats-grid { grid-template-columns: repeat(2, 1fr); }
    .repos-grid { grid-template-columns: 1fr; }
    .username { font-size: 1.8em; }
  }

  /* NEON LINE DECORATION */
  .neon-line {
    width: 100%;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--cyan), var(--magenta), var(--cyan), transparent);
    margin: 10px 0;
    opacity: 0.4;
  }
</style>
</head>
<body>

<div class="bg-grid"></div>
<div class="scanline"></div>
<div class="scan-beam"></div>

<div class="particles" id="particles"></div>

<div class="hex-decoration" id="hexDeco"></div>

<div class="container">

  <!-- HEADER -->
  <div class="header">
    <div class="avatar-container">
      <div class="avatar-ring"></div>
      <img class="avatar" src="https://avatars.githubusercontent.com/u/62319248?v=4" alt="diorjuraev" onerror="this.src='data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><rect fill=%22%230a0a1a%22 width=%22100%22 height=%22100%22/><text x=%2250%25%22 y=%2255%25%22 font-size=%2240%22 text-anchor=%22middle%22 fill=%2200f0ff%22>DJ</text></svg>'">
    </div>
    <div class="username">DIORJURAEV</div>
    <div class="bio">Cyber Defense Specialist | AppSec Engineer | Red Team Operator</div>
    <div class="status-line">&#127919; STATUS: FOCUSING // THREAT_INTEL_APP.build()</div>
    <div class="neon-line"></div>
    <div class="location-bar">
      <span>&#128205; Williston, ND</span>
      <a href="https://www.cybersecelite.com" target="_blank">&#127760; cybersecelite.com</a>
      <a href="https://twitter.com/Cyb3rS3c3lit3" target="_blank">&#128038; @Cyb3rS3c3lit3</a>
      <a href="https://linkedin.com/in/diyorbek-juraev-" target="_blank">&#128279; LinkedIn</a>
      <a href="https://medium.com/@diorjuraev" target="_blank">&#9998; Medium</a>
    </div>
  </div>

  <!-- TERMINAL -->
  <div class="terminal-box">
    <span id="terminalText"></span><span class="terminal-cursor"></span>
  </div>

  <!-- STATS -->
  <div class="stats-grid">
    <div class="stat-card">
      <div class="stat-number" id="repoCount">0</div>
      <div class="stat-label">Repositories</div>
    </div>
    <div class="stat-card">
      <div class="stat-number" id="followerCount">0</div>
      <div class="stat-label">Followers</div>
    </div>
    <div class="stat-card">
      <div class="stat-number" id="followingCount">0</div>
      <div class="stat-label">Following</div>
    </div>
    <div class="stat-card">
      <div class="stat-number" id="starCount">0</div>
      <div class="stat-label">Stars</div>
    </div>
  </div>

  <!-- TECH STACK -->
  <div class="section-title">TECH_STACK</div>
  <div class="tech-grid">
    <div class="tech-tag python">PYTHON</div>
    <div class="tech-tag fastapi">FASTAPI</div>
    <div class="tech-tag js">JAVASCRIPT</div>
    <div class="tech-tag react">REACT</div>
    <div class="tech-tag linux">LINUX</div>
    <div class="tech-tag rpi">RASPBERRY PI</div>
    <div class="tech-tag csharp">C#</div>
    <div class="tech-tag java">JAVA</div>
    <div class="tech-tag powershell">POWERSHELL</div>
  </div>

  <!-- LANGUAGE BREAKDOWN -->
  <div class="section-title">LANG_ANALYSIS</div>
  <div class="lang-bar-container">
    <div class="lang-bar">
      <div style="width:30%;background:#5391FE"></div>
      <div style="width:25%;background:#3776ab"></div>
      <div style="width:12%;background:#f89820"></div>
      <div style="width:10%;background:#9b4dca"></div>
      <div style="width:8%;background:#555"></div>
      <div style="width:8%;background:#e34c26"></div>
      <div style="width:7%;background:#da5b0b"></div>
    </div>
    <div class="lang-legend">
      <div class="lang-legend-item"><span class="lang-dot" style="background:#5391FE;box-shadow:0 0 6px #5391FE"></span> PowerShell 30%</div>
      <div class="lang-legend-item"><span class="lang-dot" style="background:#3776ab;box-shadow:0 0 6px #3776ab"></span> Python 25%</div>
      <div class="lang-legend-item"><span class="lang-dot" style="background:#f89820;box-shadow:0 0 6px #f89820"></span> Java 12%</div>
      <div class="lang-legend-item"><span class="lang-dot" style="background:#9b4dca;box-shadow:0 0 6px #9b4dca"></span> C# 10%</div>
      <div class="lang-legend-item"><span class="lang-dot" style="background:#555;box-shadow:0 0 6px #555"></span> C 8%</div>
      <div class="lang-legend-item"><span class="lang-dot" style="background:#e34c26;box-shadow:0 0 6px #e34c26"></span> HTML 8%</div>
      <div class="lang-legend-item"><span class="lang-dot" style="background:#da5b0b;box-shadow:0 0 6px #da5b0b"></span> Jupyter 7%</div>
    </div>
  </div>

  <!-- REPOS -->
  <div class="section-title">REPOSITORIES</div>
  <div class="filter-bar">
    <button class="filter-btn active" onclick="filterRepos('all')">ALL [24]</button>
    <button class="filter-btn" onclick="filterRepos('original')">ORIGINAL [6]</button>
    <button class="filter-btn" onclick="filterRepos('forked')">FORKED [18]</button>
    <button class="filter-btn" onclick="filterRepos('security')">SECURITY</button>
  </div>

  <div class="repos-grid" id="reposGrid">

    <a class="repo-card original" href="https://github.com/diorjuraev/Testing" target="_blank" data-type="original" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">TESTING</span>
        <span class="repo-badge badge-original">SRC</span>
      </div>
      <div class="repo-desc">Testing Repository</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-Python"></span> Python</span>
        <span>Updated Feb 2025</span>
      </div>
    </a>

    <a class="repo-card original" href="https://github.com/diorjuraev/diorjuraev" target="_blank" data-type="original">
      <div class="repo-header">
        <span class="repo-name">DIORJURAEV</span>
        <span class="repo-badge badge-original">SRC</span>
      </div>
      <div class="repo-desc">Config files for my GitHub profile</div>
      <div class="repo-meta">
        <span>Updated Dec 2025</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/Flipper" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">FLIPPER</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Flipper Zero customization collection</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-C"></span> C</span>
        <span>Updated Apr 2024</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/My-Payloads" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">MY-PAYLOADS</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Payloads for Bash Bunny, Rubber Ducky, FlipperZero & OMG cable</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-PowerShell"></span> PowerShell</span>
        <span>Updated Apr 2024</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/Flipper-IRDB" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">FLIPPER-IRDB</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Infrared database for Flipper devices</div>
      <div class="repo-meta">
        <span>Updated Apr 2024</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/BadUSB-Playground" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">BADUSB-PLAYGROUND</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Flipper Zero geared BadUSB playground</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-Python"></span> Python</span>
        <span>Updated Apr 2024</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/h4cker" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">H4CKER</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Ethical hacking and security resources</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-Jupyter"></span> Jupyter</span>
        <span>Updated Dec 2023</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/badusb" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">BADUSB</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Flipper Zero BadUSB payload library</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-PowerShell"></span> PowerShell</span>
        <span>Updated Dec 2023</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/Flipper-Zero-NFC-Trolls" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">FLIPPER-ZERO-NFC-TROLLS</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Collection of helpful and troll NFC links</div>
      <div class="repo-meta">
        <span>Updated Dec 2023</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/FlipperAmiibo" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">FLIPPER-AMIIBO</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">NFC Amiibo files for Flipper</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-Python"></span> Python</span>
        <span>Updated Dec 2023</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/Flipper_Zero-BadUsb" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">FLIPPER_ZERO-BADUSB</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Advanced BadUSB scripts for Flipper Zero</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-PowerShell"></span> PowerShell</span>
        <span>Updated Dec 2023</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/Flipper-Zero-BadUSB" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">FLIPPER-ZERO-BADUSB</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">BadUSB payloads for Flipper Zero</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-PowerShell"></span> PowerShell</span>
        <span>Updated Dec 2023</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/Flipper_Zero_Badusb_hack5_payloads" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">FLIPPER_HACK5_PAYLOADS</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Modified Hack5 payloads for Flipper Zero</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-PowerShell"></span> PowerShell</span>
        <span>Updated Dec 2023</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/open-source-mac-os-apps" target="_blank" data-type="forked">
      <div class="repo-header">
        <span class="repo-name">OPEN-SOURCE-MAC-OS-APPS</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">macOS open-source applications collection</div>
      <div class="repo-meta">
        <span>Updated Nov 2023</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/wordlists" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">WORDLISTS</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Collection of wordlists for many different usages</div>
      <div class="repo-meta">
        <span>Updated Sep 2023</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/caldera" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">CALDERA</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Automated Adversary Emulation Platform</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-Python"></span> Python</span>
        <span>Updated Sep 2023</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/cybersecurity-interview-guide" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">CYBERSEC-INTERVIEW-GUIDE</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">In-depth guide for cybersecurity interviews</div>
      <div class="repo-meta">
        <span>Updated Jun 2022</span>
      </div>
    </a>

    <a class="repo-card original" href="https://github.com/diorjuraev/WebSchedulerJava" target="_blank" data-type="original">
      <div class="repo-header">
        <span class="repo-name">WEBSCHEDULERJAVA</span>
        <span class="repo-badge badge-original">SRC</span>
      </div>
      <div class="repo-desc">WebScheduler application</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-Java"></span> Java</span>
        <span>Updated Feb 2022</span>
      </div>
    </a>

    <a class="repo-card original" href="https://github.com/diorjuraev/Cyber353Project" target="_blank" data-type="original" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">CYBER353PROJECT</span>
        <span class="repo-badge badge-original">SRC</span>
      </div>
      <div class="repo-desc">Cybersecurity course project</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-CSharp"></span> C#</span>
        <span>Updated Dec 2021</span>
      </div>
    </a>

    <a class="repo-card original" href="https://github.com/diorjuraev/java-course" target="_blank" data-type="original">
      <div class="repo-header">
        <span class="repo-name">JAVA-COURSE</span>
        <span class="repo-badge badge-original">SRC</span>
      </div>
      <div class="repo-desc">An introduction to Java</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-Java"></span> Java</span>
        <span>Updated Nov 2021</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/Network-Scanner" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">NETWORK-SCANNER</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Network toolkit for scanning active IPs and open ports</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-Python"></span> Python</span>
        <span>Updated May 2021</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/Cheat-Sheets" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">CHEAT-SHEETS</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">Security reference materials</div>
      <div class="repo-meta">
        <span>Updated May 2021</span>
      </div>
    </a>

    <a class="repo-card forked" href="https://github.com/diorjuraev/mana" target="_blank" data-type="forked" data-cat="security">
      <div class="repo-header">
        <span class="repo-name">MANA</span>
        <span class="repo-badge badge-forked">FORK</span>
      </div>
      <div class="repo-desc">[DEPRECATED] MANA toolkit for WiFi rogue AP attacks and MitM</div>
      <div class="repo-meta">
        <span class="repo-lang"><span class="lang-dot lang-HTML"></span> HTML</span>
        <span>Updated Aug 2018</span>
      </div>
    </a>

  </div>

  <!-- FOOTER -->
  <div class="footer">
    <div class="neon-line" style="margin-bottom:20px"></div>
    <div class="glitch-text">DIORJURAEV // CYBERDECK</div>
    <div style="margin-top:8px">[ ENCRYPTED CHANNEL // SESSION ACTIVE // ALL SYSTEMS NOMINAL ]</div>
    <div style="margin-top:4px">github.com/diorjuraev &mdash; cybersecelite.com</div>
  </div>

</div>

<script>
  // ANIMATED COUNTERS
  function animateCount(id, target, duration = 1500) {
    const el = document.getElementById(id);
    const start = 0;
    const startTime = performance.now();
    function update(now) {
      const elapsed = now - startTime;
      const progress = Math.min(elapsed / duration, 1);
      const eased = 1 - Math.pow(1 - progress, 3);
      el.textContent = Math.round(start + (target - start) * eased);
      if (progress < 1) requestAnimationFrame(update);
    }
    requestAnimationFrame(update);
  }

  setTimeout(() => animateCount('repoCount', 24), 300);
  setTimeout(() => animateCount('followerCount', 14), 500);
  setTimeout(() => animateCount('followingCount', 62), 700);
  setTimeout(() => animateCount('starCount', 144), 900);

  // TERMINAL TYPING
  const terminalLines = [
    'nmap -sS -sV -O target.local',
    'cat /etc/shadow | hashcat -m 1800 -a 0',
    'msfconsole -q -x "use exploit/multi/handler"',
    'python3 threat_intel_app.py --mode=realtime',
    'wireshark -i eth0 -k -f "port 443"',
    'sudo airmon-ng start wlan0',
    'gobuster dir -u https://target.com -w wordlist.txt',
    'hydra -l admin -P rockyou.txt ssh://192.168.1.1',
    'volatility -f memdump.raw --profile=Win10 pslist',
  ];

  let lineIdx = 0;
  const termEl = document.getElementById('terminalText');

  function typeLine() {
    const line = terminalLines[lineIdx % terminalLines.length];
    let charIdx = 0;
    termEl.textContent = '';
    const interval = setInterval(() => {
      termEl.textContent += line[charIdx];
      charIdx++;
      if (charIdx >= line.length) {
        clearInterval(interval);
        setTimeout(() => {
          lineIdx++;
          typeLine();
        }, 2500);
      }
    }, 50);
  }
  typeLine();

  // PARTICLES
  const particlesEl = document.getElementById('particles');
  for (let i = 0; i < 30; i++) {
    const p = document.createElement('div');
    p.className = 'particle';
    p.style.left = Math.random() * 100 + '%';
    p.style.animationDelay = Math.random() * 6 + 's';
    p.style.animationDuration = (4 + Math.random() * 4) + 's';
    if (Math.random() > 0.6) p.style.background = '#ff00de';
    if (Math.random() > 0.8) p.style.background = '#39ff14';
    particlesEl.appendChild(p);
  }

  // HEX DECORATION
  const hexEl = document.getElementById('hexDeco');
  let hexLines = [];
  for (let i = 0; i < 12; i++) {
    let hex = '';
    for (let j = 0; j < 8; j++) hex += Math.floor(Math.random() * 16).toString(16);
    hexLines.push(hex.toUpperCase());
  }
  hexEl.innerHTML = hexLines.join('<br>');
  setInterval(() => {
    const idx = Math.floor(Math.random() * hexLines.length);
    let hex = '';
    for (let j = 0; j < 8; j++) hex += Math.floor(Math.random() * 16).toString(16);
    hexLines[idx] = hex.toUpperCase();
    hexEl.innerHTML = hexLines.join('<br>');
  }, 200);

  // FILTER REPOS
  function filterRepos(type) {
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    event.target.classList.add('active');
    document.querySelectorAll('.repo-card').forEach(card => {
      if (type === 'all') {
        card.style.display = '';
      } else if (type === 'security') {
        card.style.display = card.dataset.cat === 'security' ? '' : 'none';
      } else {
        card.style.display = card.dataset.type === type ? '' : 'none';
      }
    });
  }
</script>
</body>
</html>
