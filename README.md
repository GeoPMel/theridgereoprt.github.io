<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Ridge Report — New England Trail Weather</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Mono:wght@300;400;500&family=Crimson+Pro:ital,wght@0,300;0,400;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --forest: #1a2e1a;
    --moss: #3d5c2e;
    --sage: #7a9e5f;
    --stone: #c4b89a;
    --fog: #e8e4dc;
    --sky: #a8c4d4;
    --peak: #f5f0e8;
    --bark: #5c3d1e;
    --accent: #d4541a;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background-color: var(--forest);
    color: var(--fog);
    font-family: 'Crimson Pro', serif;
    font-size: 18px;
    line-height: 1.6;
    overflow-x: hidden;
  }

  /* ── HEADER ── */
  header {
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    overflow: hidden;
    padding: 2rem;
  }

  .hero-bg {
    position: absolute;
    inset: 0;
    background:
      radial-gradient(ellipse at 20% 50%, rgba(61,92,46,0.4) 0%, transparent 60%),
      radial-gradient(ellipse at 80% 20%, rgba(168,196,212,0.15) 0%, transparent 50%),
      radial-gradient(ellipse at 60% 80%, rgba(92,61,30,0.3) 0%, transparent 50%),
      linear-gradient(170deg, #0d1a0d 0%, #1a2e1a 40%, #2a3d22 100%);
  }

  .mountains {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 45%;
  }

  .mountains svg { width: 100%; height: 100%; }

  .grain {
    position: absolute;
    inset: 0;
    opacity: 0.035;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
    background-size: 200px 200px;
    pointer-events: none;
  }

  .hero-content {
    position: relative;
    z-index: 2;
    max-width: 800px;
    animation: fadeUp 1.2s ease both;
  }

  .eyebrow {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--sage);
    margin-bottom: 1.5rem;
    opacity: 0;
    animation: fadeUp 1s ease 0.2s both;
  }

  h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(3rem, 9vw, 7.5rem);
    font-weight: 900;
    line-height: 0.9;
    letter-spacing: -0.02em;
    color: var(--peak);
    margin-bottom: 0.3em;
    opacity: 0;
    animation: fadeUp 1s ease 0.4s both;
  }

  h1 em { font-style: italic; color: var(--stone); }

  .tagline {
    font-size: clamp(1rem, 2.5vw, 1.35rem);
    color: var(--stone);
    font-weight: 300;
    font-style: italic;
    max-width: 500px;
    margin: 1.5rem auto 2.5rem;
    opacity: 0;
    animation: fadeUp 1s ease 0.6s both;
  }

  .hero-cta {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 1s ease 0.8s both;
  }

  .btn {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    text-decoration: none;
    padding: 0.85rem 2rem;
    border-radius: 2px;
    transition: all 0.3s ease;
    cursor: pointer;
    border: none;
  }

  .btn-primary { background: var(--accent); color: var(--peak); }
  .btn-primary:hover { background: #e86030; transform: translateY(-2px); box-shadow: 0 8px 24px rgba(212,84,26,0.4); }
  .btn-outline { background: transparent; color: var(--fog); border: 1px solid rgba(196,184,154,0.4); }
  .btn-outline:hover { border-color: var(--stone); color: var(--stone); transform: translateY(-2px); }

  .scroll-hint {
    position: absolute;
    bottom: 2rem;
    left: 50%;
    transform: translateX(-50%);
    z-index: 2;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    opacity: 0;
    animation: fadeUp 1s ease 1.2s both;
  }

  .scroll-hint span {
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: rgba(196,184,154,0.5);
  }

  .scroll-line {
    width: 1px;
    height: 48px;
    background: linear-gradient(to bottom, rgba(196,184,154,0.5), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }

  /* ── NAV ── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    padding: 1.5rem 3rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: linear-gradient(to bottom, rgba(10,20,10,0.8), transparent);
    backdrop-filter: blur(4px);
  }

  .nav-brand {
    font-family: 'Playfair Display', serif;
    font-size: 1.1rem;
    font-weight: 700;
    color: var(--peak);
    text-decoration: none;
    letter-spacing: 0.03em;
  }

  .nav-links { display: flex; gap: 2rem; list-style: none; }

  .nav-links a {
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--stone);
    text-decoration: none;
    transition: color 0.2s;
  }

  .nav-links a:hover { color: var(--peak); }

  /* ── SECTIONS ── */
  section {
    padding: 6rem 2rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--sage);
    margin-bottom: 1rem;
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: rgba(122,158,95,0.3);
  }

  h2 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 5vw, 3.5rem);
    font-weight: 700;
    line-height: 1.1;
    color: var(--peak);
    margin-bottom: 1.5rem;
  }

  h2 em { color: var(--stone); font-style: italic; }

  /* ── WEATHER GRID ── */
  .weather-section {
    background: rgba(255,255,255,0.03);
    border-top: 1px solid rgba(196,184,154,0.1);
    border-bottom: 1px solid rgba(196,184,154,0.1);
    padding: 5rem 2rem;
  }

  .weather-inner { max-width: 1200px; margin: 0 auto; }

  .region-tabs {
    display: flex;
    gap: 0.5rem;
    flex-wrap: wrap;
    margin-bottom: 2.5rem;
  }

  .tab {
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.5rem 1.2rem;
    border-radius: 2px;
    border: 1px solid rgba(196,184,154,0.2);
    background: transparent;
    color: var(--stone);
    cursor: pointer;
    transition: all 0.2s;
  }

  .tab.active, .tab:hover {
    background: var(--moss);
    border-color: var(--sage);
    color: var(--peak);
  }

  .trail-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1.5rem;
  }

  .trail-card {
    background: rgba(26,46,26,0.8);
    border: 1px solid rgba(196,184,154,0.12);
    border-radius: 4px;
    padding: 1.5rem;
    transition: all 0.3s ease;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }

  .trail-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: var(--sage);
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.3s ease;
  }

  .trail-card:hover {
    border-color: rgba(196,184,154,0.3);
    transform: translateY(-4px);
    box-shadow: 0 16px 40px rgba(0,0,0,0.4);
  }

  .trail-card:hover::before { transform: scaleX(1); }

  .trail-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.2rem;
    font-weight: 700;
    color: var(--peak);
    margin-bottom: 0.25rem;
  }

  .trail-region {
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--sage);
    margin-bottom: 1.2rem;
  }

  .weather-display {
    display: flex;
    align-items: flex-end;
    gap: 1rem;
    margin-bottom: 1rem;
  }

  .temp-big {
    font-family: 'Playfair Display', serif;
    font-size: 3rem;
    font-weight: 400;
    color: var(--peak);
    line-height: 1;
  }

  .weather-meta {
    flex: 1;
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    color: var(--stone);
    line-height: 1.8;
  }

  .conditions-badge {
    display: inline-block;
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.3rem 0.8rem;
    border-radius: 2px;
    margin-bottom: 0.75rem;
  }

  .badge-good { background: rgba(122,158,95,0.2); color: var(--sage); border: 1px solid rgba(122,158,95,0.3); }
  .badge-caution { background: rgba(212,84,26,0.15); color: #e8904a; border: 1px solid rgba(212,84,26,0.3); }
  .badge-poor { background: rgba(100,100,120,0.2); color: #aaa; border: 1px solid rgba(150,150,170,0.3); }

  .forecast-row {
    display: flex;
    gap: 0.5rem;
    margin-top: 1rem;
    padding-top: 1rem;
    border-top: 1px solid rgba(196,184,154,0.1);
  }

  .forecast-day {
    flex: 1;
    text-align: center;
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    color: var(--stone);
  }

  .forecast-day .f-temp { font-size: 0.85rem; color: var(--fog); display: block; margin-top: 0.25rem; }
  .forecast-day .f-icon { font-size: 1rem; display: block; margin: 0.2rem 0; }

  /* ── TRAIL GUIDES ── */
  .guides-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
    gap: 2rem;
    margin-top: 3rem;
  }

  .guide-card {
    border: 1px solid rgba(196,184,154,0.12);
    border-radius: 4px;
    overflow: hidden;
    transition: all 0.3s ease;
  }

  .guide-card:hover {
    border-color: rgba(196,184,154,0.3);
    transform: translateY(-4px);
    box-shadow: 0 16px 40px rgba(0,0,0,0.4);
  }

  /* Topo map embed */
  .topo-map {
    width: 100%;
    height: 200px;
    border: none;
    display: block;
    filter: brightness(0.85) saturate(0.9);
    transition: filter 0.3s ease;
  }

  .guide-card:hover .topo-map {
    filter: brightness(0.95) saturate(1);
  }

  .topo-label {
    background: rgba(10,20,10,0.85);
    padding: 0.3rem 0.75rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .topo-label span {
    font-family: 'DM Mono', monospace;
    font-size: 0.55rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: rgba(196,184,154,0.5);
  }

  .topo-label a {
    font-family: 'DM Mono', monospace;
    font-size: 0.55rem;
    letter-spacing: 0.08em;
    color: var(--sage);
    text-decoration: none;
    opacity: 0.7;
    transition: opacity 0.2s;
  }

  .topo-label a:hover { opacity: 1; }

  .guide-difficulty {
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    padding: 0.3rem 0.7rem;
    color: var(--fog);
  }

  .guide-body {
    padding: 1.5rem;
    background: rgba(26,46,26,0.9);
  }

  .guide-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.3rem;
    font-weight: 700;
    color: var(--peak);
    margin-bottom: 0.5rem;
  }

  .guide-stats {
    display: flex;
    gap: 1.5rem;
    flex-wrap: wrap;
    margin-bottom: 1rem;
    font-family: 'DM Mono', monospace;
    font-size: 0.62rem;
    color: var(--sage);
    letter-spacing: 0.05em;
  }

  .guide-excerpt {
    font-size: 0.9rem;
    color: var(--stone);
    line-height: 1.7;
    font-style: italic;
  }

  /* ── GEAR SECTION ── */
  .gear-section {
    background: linear-gradient(135deg, rgba(61,92,46,0.15) 0%, transparent 60%);
    border-top: 1px solid rgba(196,184,154,0.1);
    padding: 5rem 2rem;
  }

  .gear-inner { max-width: 1200px; margin: 0 auto; }

  .gear-disclaimer {
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.08em;
    color: rgba(196,184,154,0.4);
    margin-bottom: 2rem;
    font-style: italic;
  }

  .gear-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
    gap: 1.5rem;
    margin-top: 2.5rem;
  }

  .gear-card {
    background: rgba(26,46,26,0.6);
    border: 1px solid rgba(196,184,154,0.1);
    border-radius: 4px;
    padding: 1.5rem;
    text-align: center;
    transition: all 0.3s ease;
    text-decoration: none;
    display: block;
    color: inherit;
  }

  .gear-card:hover {
    border-color: rgba(122,158,95,0.4);
    transform: translateY(-3px);
    box-shadow: 0 12px 32px rgba(0,0,0,0.35);
  }

  .gear-icon { font-size: 2.5rem; display: block; margin-bottom: 0.75rem; }
  .gear-name { font-family: 'Playfair Display', serif; font-size: 1rem; font-weight: 700; color: var(--peak); margin-bottom: 0.4rem; }

  .gear-desc {
    font-size: 0.82rem;
    color: var(--stone);
    font-style: italic;
    line-height: 1.5;
    margin-bottom: 1rem;
  }

  .gear-link {
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--sage);
    border-bottom: 1px solid rgba(122,158,95,0.3);
    padding-bottom: 0.1rem;
    transition: color 0.2s, border-color 0.2s;
  }

  .gear-card:hover .gear-link { color: var(--accent); border-color: rgba(212,84,26,0.5); }

  /* ── SEASONAL TIPS ── */
  .tips-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-top: 3rem;
  }

  .tip-card {
    padding: 2rem;
    border-radius: 4px;
    border: 1px solid rgba(196,184,154,0.1);
    position: relative;
    overflow: hidden;
  }

  .tip-season {
    font-family: 'Playfair Display', serif;
    font-size: 1.4rem;
    font-weight: 900;
    color: var(--peak);
    margin-bottom: 1rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .tip-list { list-style: none; font-size: 0.88rem; color: var(--stone); line-height: 2; }
  .tip-list li::before { content: '—'; color: var(--sage); margin-right: 0.5rem; }

  .spring-card { background: rgba(61,92,46,0.15); }
  .summer-card { background: rgba(168,196,212,0.08); }
  .fall-card   { background: rgba(212,84,26,0.08); }
  .winter-card { background: rgba(196,184,154,0.05); }

  /* ── FOOTER ── */
  footer {
    background: rgba(0,0,0,0.4);
    border-top: 1px solid rgba(196,184,154,0.1);
    padding: 3rem 2rem;
    text-align: center;
  }

  .footer-brand { font-family: 'Playfair Display', serif; font-size: 1.8rem; font-weight: 900; color: var(--peak); margin-bottom: 0.5rem; }
  .footer-tagline { font-family: 'Crimson Pro', serif; font-style: italic; color: var(--stone); margin-bottom: 2rem; }

  .footer-links {
    display: flex;
    justify-content: center;
    gap: 2rem;
    flex-wrap: wrap;
    margin-bottom: 2rem;
    list-style: none;
  }

  .footer-links a {
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--stone);
    text-decoration: none;
    transition: color 0.2s;
  }

  .footer-links a:hover { color: var(--sage); }

  .footer-note {
    font-family: 'DM Mono', monospace;
    font-size: 0.58rem;
    letter-spacing: 0.08em;
    color: rgba(196,184,154,0.3);
    max-width: 600px;
    margin: 0 auto;
    line-height: 1.8;
  }

  .divider { border: none; border-top: 1px solid rgba(196,184,154,0.08); margin: 0; }

  /* ── LIVE BADGE ── */
  .live-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--sage);
    padding: 0.3rem 0.75rem;
    border: 1px solid rgba(122,158,95,0.3);
    border-radius: 2px;
    margin-bottom: 2rem;
  }

  .live-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--sage);
    animation: pulse 2s ease-in-out infinite;
  }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  @keyframes scrollPulse {
    0%, 100% { opacity: 0.5; transform: scaleY(1); }
    50%       { opacity: 1;   transform: scaleY(1.2); }
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50%       { opacity: 0.4; transform: scale(0.8); }
  }

  @media (max-width: 768px) {
    nav { padding: 1rem 1.5rem; }
    .nav-links { display: none; }
    section { padding: 4rem 1.25rem; }
    .guides-grid { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <a href="#" class="nav-brand">The Ridge Report</a>
  <ul class="nav-links">
    <li><a href="#weather">Weather</a></li>
    <li><a href="#trails">Trails</a></li>
    <li><a href="#seasonal">Seasonal</a></li>
    <li><a href="#gear">Gear</a></li>
  </ul>
</nav>

<!-- HERO -->
<header>
  <div class="hero-bg"></div>
  <div class="grain"></div>
  <div class="mountains">
    <svg viewBox="0 0 1440 400" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
      <defs>
        <linearGradient id="mtGrad" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0%" stop-color="#2a3d22" stop-opacity="0.9"/>
          <stop offset="100%" stop-color="#1a2e1a" stop-opacity="1"/>
        </linearGradient>
      </defs>
      <path d="M0 400 L0 280 L120 200 L240 260 L380 140 L520 220 L640 100 L760 180 L880 120 L1000 200 L1120 130 L1240 190 L1360 160 L1440 180 L1440 400 Z" fill="rgba(30,50,25,0.5)"/>
      <path d="M0 400 L0 320 L100 280 L200 340 L340 240 L440 300 L560 180 L680 260 L800 200 L920 280 L1040 210 L1160 290 L1300 230 L1440 260 L1440 400 Z" fill="url(#mtGrad)"/>
      <path d="M0 400 L0 360 L60 350 L80 370 L120 345 L150 365 L200 348 L240 360 L280 344 L320 358 L380 342 L420 355 L480 338 L530 352 L600 335 L660 348 L730 330 L790 344 L860 326 L920 340 L990 322 L1060 336 L1140 318 L1220 332 L1300 316 L1380 328 L1440 320 L1440 400 Z" fill="rgba(20,35,18,0.8)"/>
      <g fill="#0d1a0d" opacity="0.9">
        <polygon points="60,360 50,380 70,380"/><polygon points="60,355 48,370 72,370"/>
        <polygon points="150,355 138,375 162,375"/><polygon points="150,349 136,365 164,365"/>
        <polygon points="280,349 268,369 292,369"/><polygon points="420,352 408,372 432,372"/>
        <polygon points="530,349 518,369 542,369"/><polygon points="660,345 648,365 672,365"/>
        <polygon points="790,341 778,361 802,361"/><polygon points="920,337 908,357 932,357"/>
        <polygon points="1060,333 1048,353 1072,353"/><polygon points="1220,329 1208,349 1232,349"/>
        <polygon points="1380,325 1368,345 1392,345"/>
      </g>
    </svg>
  </div>
  <div class="hero-content">
    <p class="eyebrow">New England Trail Weather &amp; Guides</p>
    <h1>The Ridge<br><em>Report</em></h1>
    <p class="tagline">Forecasts, trail conditions, and seasonal wisdom for the peaks of New England.</p>
    <div class="hero-cta">
      <a href="#weather" class="btn btn-primary">Check Forecasts</a>
      <a href="#trails" class="btn btn-outline">Browse Trails</a>
    </div>
  </div>
  <div class="scroll-hint">
    <div class="scroll-line"></div>
    <span>Scroll</span>
  </div>
</header>

<!-- WEATHER SECTION -->
<div class="weather-section" id="weather">
  <div class="weather-inner">
    <p class="section-label">Live Conditions</p>
    <div style="display:flex; align-items:center; justify-content:space-between; flex-wrap:wrap; gap:1rem; margin-bottom:2rem;">
      <h2 style="margin:0;">Trail <em>Weather</em></h2>
      <div class="live-badge"><div class="live-dot"></div> Updated hourly</div>
    </div>

    <div class="region-tabs" id="regionTabs">
      <button class="tab active" onclick="filterRegion('all', this)">All Regions</button>
      <button class="tab" onclick="filterRegion('white-mountains', this)">White Mountains</button>
      <button class="tab" onclick="filterRegion('green-mountains', this)">Green Mountains</button>
      <button class="tab" onclick="filterRegion('maine', this)">Maine Highlands</button>
      <button class="tab" onclick="filterRegion('berkshires', this)">Berkshires</button>
      <button class="tab" onclick="filterRegion('connecticut', this)">Connecticut</button>
    </div>

    <div class="trail-grid" id="trailGrid"></div>
  </div>
</div>

<hr class="divider">

<!-- TRAIL GUIDES -->
<section id="trails">
  <p class="section-label">Featured Trails</p>
  <h2>Know Before<br>You <em>Go</em></h2>
  <p style="color:var(--stone); font-style:italic; max-width:560px;">In-depth guides to New England's most beloved peaks — difficulty, distance, elevation, and what to expect each season.</p>

  <div class="guides-grid">

    <!-- Mt. Washington -->
    <div class="guide-card">
      <iframe class="topo-map"
        src="https://www.opentopomap.org/#map=13/44.2706/-71.3033"
        title="Topographic map of Mt. Washington, NH"
        loading="lazy" referrerpolicy="no-referrer"></iframe>
      <div class="topo-label">
        <span>OpenTopoMap</span>
        <a href="https://www.opentopomap.org/#map=13/44.2706/-71.3033" target="_blank" rel="noopener">Open full map ↗</a>
      </div>
      <div class="guide-body">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:0.5rem;">
          <h3 class="guide-title" style="margin:0;">Mt. Washington</h3>
          <span class="guide-difficulty" style="font-family:'DM Mono',monospace; font-size:0.6rem; letter-spacing:0.1em; text-transform:uppercase; color:#e8904a; padding:0;">Strenuous</span>
        </div>
        <div class="guide-stats">
          <span>NH &middot; Presidential Range</span>
          <span>&uarr; 4,258 ft gain</span>
          <span>8.4 mi round trip</span>
        </div>
        <p class="guide-excerpt">Home to some of the world's most extreme weather. The Tuckerman Ravine Trail rewards the prepared with unmatched summit views — but demands respect in every season. Wind speeds can exceed 100 mph; always check the Mount Washington Observatory forecast before heading up.</p>
      </div>
    </div>

    <!-- Mt. Katahdin -->
    <div class="guide-card">
      <iframe class="topo-map"
        src="https://www.opentopomap.org/#map=13/45.9044/-68.9213"
        title="Topographic map of Mt. Katahdin, ME"
        loading="lazy" referrerpolicy="no-referrer"></iframe>
      <div class="topo-label">
        <span>OpenTopoMap</span>
        <a href="https://www.opentopomap.org/#map=13/45.9044/-68.9213" target="_blank" rel="noopener">Open full map ↗</a>
      </div>
      <div class="guide-body">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:0.5rem;">
          <h3 class="guide-title" style="margin:0;">Mt. Katahdin</h3>
          <span style="font-family:'DM Mono',monospace; font-size:0.6rem; letter-spacing:0.1em; text-transform:uppercase; color:#e8904a;">Strenuous</span>
        </div>
        <div class="guide-stats">
          <span>ME &middot; Baxter State Park</span>
          <span>&uarr; 4,267 ft gain</span>
          <span>10.4 mi round trip</span>
        </div>
        <p class="guide-excerpt">The northern terminus of the Appalachian Trail. The Knife Edge ridge traverse is legendary — a narrow, exposed scramble with sheer drops on both sides. Approach only in clear, dry conditions, and be aware that Baxter State Park enforces strict trailhead quotas.</p>
      </div>
    </div>

    <!-- Camel's Hump -->
    <div class="guide-card">
      <iframe class="topo-map"
        src="https://www.opentopomap.org/#map=13/44.3192/-72.8849"
        title="Topographic map of Camel's Hump, VT"
        loading="lazy" referrerpolicy="no-referrer"></iframe>
      <div class="topo-label">
        <span>OpenTopoMap</span>
        <a href="https://www.opentopomap.org/#map=13/44.3192/-72.8849" target="_blank" rel="noopener">Open full map ↗</a>
      </div>
      <div class="guide-body">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:0.5rem;">
          <h3 class="guide-title" style="margin:0;">Camel's Hump</h3>
          <span style="font-family:'DM Mono',monospace; font-size:0.6rem; letter-spacing:0.1em; text-transform:uppercase; color:var(--sage);">Moderate</span>
        </div>
        <div class="guide-stats">
          <span>VT &middot; Green Mountains</span>
          <span>&uarr; 2,559 ft gain</span>
          <span>6.4 mi round trip</span>
        </div>
        <p class="guide-excerpt">Vermont's most iconic silhouette on the horizon. The Burrows Trail winds through pristine boreal forest before opening onto a rocky, exposed alpine summit with sweeping 360-degree views. Stay on marked rocks above treeline to protect fragile arctic vegetation.</p>
      </div>
    </div>

    <!-- Franconia Ridge -->
    <div class="guide-card">
      <iframe class="topo-map"
        src="https://www.opentopomap.org/#map=13/44.1599/-71.6445"
        title="Topographic map of Franconia Ridge, NH"
        loading="lazy" referrerpolicy="no-referrer"></iframe>
      <div class="topo-label">
        <span>OpenTopoMap</span>
        <a href="https://www.opentopomap.org/#map=13/44.1599/-71.6445" target="_blank" rel="noopener">Open full map ↗</a>
      </div>
      <div class="guide-body">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:0.5rem;">
          <h3 class="guide-title" style="margin:0;">Franconia Ridge</h3>
          <span style="font-family:'DM Mono',monospace; font-size:0.6rem; letter-spacing:0.1em; text-transform:uppercase; color:var(--sage);">Moderate</span>
        </div>
        <div class="guide-stats">
          <span>NH &middot; Franconia Notch</span>
          <span>&uarr; 3,900 ft gain</span>
          <span>8.9 mi loop</span>
        </div>
        <p class="guide-excerpt">Widely considered the finest ridge walk in the Northeast. The loop over Little Haystack, Lincoln, and Lafayette offers over two miles of above-treeline travel with spectacular views in every direction. The Falling Waters Trail descent passes three beautiful waterfalls.</p>
      </div>
    </div>

    <!-- Mt. Monadnock -->
    <div class="guide-card">
      <iframe class="topo-map"
        src="https://www.opentopomap.org/#map=14/42.8606/-72.1072"
        title="Topographic map of Mt. Monadnock, NH"
        loading="lazy" referrerpolicy="no-referrer"></iframe>
      <div class="topo-label">
        <span>OpenTopoMap</span>
        <a href="https://www.opentopomap.org/#map=14/42.8606/-72.1072" target="_blank" rel="noopener">Open full map ↗</a>
      </div>
      <div class="guide-body">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:0.5rem;">
          <h3 class="guide-title" style="margin:0;">Mt. Monadnock</h3>
          <span style="font-family:'DM Mono',monospace; font-size:0.6rem; letter-spacing:0.1em; text-transform:uppercase; color:var(--sage);">Moderate</span>
        </div>
        <div class="guide-stats">
          <span>NH &middot; Monadnock Region</span>
          <span>&uarr; 1,800 ft gain</span>
          <span>4.2 mi round trip</span>
        </div>
        <p class="guide-excerpt">One of the most-climbed mountains in the world, and a perfect introduction to New England alpine hiking. The White Dot Trail is direct and rewarding — the broad, rocky summit offers views into five states on a clear day and is especially spectacular during fall foliage.</p>
      </div>
    </div>

    <!-- Mt. Mansfield -->
    <div class="guide-card">
      <iframe class="topo-map"
        src="https://www.opentopomap.org/#map=13/44.5437/-72.8143"
        title="Topographic map of Mt. Mansfield, VT"
        loading="lazy" referrerpolicy="no-referrer"></iframe>
      <div class="topo-label">
        <span>OpenTopoMap</span>
        <a href="https://www.opentopomap.org/#map=13/44.5437/-72.8143" target="_blank" rel="noopener">Open full map ↗</a>
      </div>
      <div class="guide-body">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:0.5rem;">
          <h3 class="guide-title" style="margin:0;">Mt. Mansfield</h3>
          <span style="font-family:'DM Mono',monospace; font-size:0.6rem; letter-spacing:0.1em; text-transform:uppercase; color:#e8904a;">Strenuous</span>
        </div>
        <div class="guide-stats">
          <span>VT &middot; Green Mountains</span>
          <span>&uarr; 2,700 ft gain</span>
          <span>7.1 mi round trip</span>
        </div>
        <p class="guide-excerpt">Vermont's highest peak, with a summit ridge shaped like a human profile when viewed from the east. The Long Trail traverses a rare and delicate alpine zone — step only on bare rock above treeline. Ice can persist on north-facing slopes well into May.</p>
      </div>
    </div>

  </div>
</section>

<hr class="divider">

<!-- SEASONAL TIPS -->
<section id="seasonal">
  <p class="section-label">Planning Guides</p>
  <h2>Every Season<br>Has Its <em>Rules</em></h2>
  <p style="color:var(--stone); font-style:italic; max-width:560px;">New England weather is notoriously unpredictable. Here's what to know before heading out in each season.</p>

  <div class="tips-grid">
    <div class="tip-card spring-card">
      <div class="tip-season">🌿 Spring</div>
      <ul class="tip-list">
        <li>Mud season closes many trails April through May</li>
        <li>Ice lingers at elevation well into May</li>
        <li>Microspikes recommended above 3,000 ft</li>
        <li>Stream crossings run high — plan your route carefully</li>
        <li>Check AMC and state park trail status before every trip</li>
      </ul>
    </div>
    <div class="tip-card summer-card">
      <div class="tip-season">☀️ Summer</div>
      <ul class="tip-list">
        <li>Start early — afternoon thunderstorms build quickly</li>
        <li>High humidity makes climbs feel significantly harder</li>
        <li>Trailhead parking fills fast — arrive before 8 AM on weekends</li>
        <li>Blackflies peak in June, mosquitoes through July</li>
        <li>Sunscreen is essential on exposed ridges and summits</li>
      </ul>
    </div>
    <div class="tip-card fall-card">
      <div class="tip-season">🍂 Fall</div>
      <ul class="tip-list">
        <li>Best visibility of the year for summit views</li>
        <li>Foliage peaks late September in NH and VT, mid-October in MA and CT</li>
        <li>Frost and ice arrive at summits by early October</li>
        <li>Trailheads fill fast on peak foliage weekends — arrive very early</li>
        <li>Daylight shortens rapidly — always carry a headlamp</li>
      </ul>
    </div>
    <div class="tip-card winter-card">
      <div class="tip-season">❄️ Winter</div>
      <ul class="tip-list">
        <li>Four-season gear is required — no exceptions above treeline</li>
        <li>Crampons and ice axe essential above treeline</li>
        <li>Mt. Washington averages wind gusts over 110 mph in winter</li>
        <li>File a trip plan with someone before every outing</li>
        <li>Prior winter hiking experience is strongly recommended</li>
      </ul>
    </div>
  </div>
</section>

<!-- GEAR SECTION -->
<div class="gear-section" id="gear">
  <div class="gear-inner">
    <p class="section-label">Essential Kit</p>
    <h2 style="color:var(--peak); font-family:'Playfair Display',serif; font-size:clamp(2rem,5vw,3.5rem); margin-bottom:0.5rem;">Gear We <em style="color:var(--stone); font-style:italic;">Trust</em></h2>
    <p class="gear-disclaimer">* Affiliate links — we may earn a small commission at no extra cost to you. We only recommend gear we would bring on the trail ourselves.</p>

    <div class="gear-grid">

      <a href="https://www.rei.com/c/hiking-boots" target="_blank" rel="noopener" class="gear-card">
        <span class="gear-icon">🥾</span>
        <div class="gear-name">Trail Footwear</div>
        <p class="gear-desc">Waterproof boots built for New England's rocky, rooted terrain.</p>
        <span class="gear-link">Shop at REI →</span>
      </a>

      <a href="https://www.rei.com/c/trekking-poles" target="_blank" rel="noopener" class="gear-card">
        <span class="gear-icon">🗻</span>
        <div class="gear-name">Trekking Poles</div>
        <p class="gear-desc">Essential for steep descents and river crossings. Carbon or aluminum.</p>
        <span class="gear-link">Shop at REI →</span>
      </a>

      <a href="https://www.rei.com/c/rain-jackets" target="_blank" rel="noopener" class="gear-card">
        <span class="gear-icon">🧥</span>
        <div class="gear-name">Rain Shells</div>
        <p class="gear-desc">Gore-Tex and equivalent waterproof membranes. Assume the weather will change.</p>
        <span class="gear-link">Shop at REI →</span>
      </a>

      <a href="https://www.rei.com/c/headlamps" target="_blank" rel="noopener" class="gear-card">
        <span class="gear-icon">🔦</span>
        <div class="gear-name">Headlamps</div>
        <p class="gear-desc">Always carry one. Alpine starts and late descents demand reliable light.</p>
        <span class="gear-link">Shop at REI →</span>
      </a>

      <a href="https://www.rei.com/c/microspikes-crampons" target="_blank" rel="noopener" class="gear-card">
        <span class="gear-icon">⛏️</span>
        <div class="gear-name">Microspikes</div>
        <p class="gear-desc">Required spring and fall above 3,000 ft. Kahtoola MICROspikes are the New England standard.</p>
        <span class="gear-link">Shop at REI →</span>
      </a>

      <a href="https://www.rei.com/c/navigation" target="_blank" rel="noopener" class="gear-card">
        <span class="gear-icon">🧭</span>
        <div class="gear-name">Navigation</div>
        <p class="gear-desc">GPS watch or dedicated device. Always carry a paper topo map as backup.</p>
        <span class="gear-link">Shop at REI →</span>
      </a>

      <a href="https://www.rei.com/c/water-filters-purifiers" target="_blank" rel="noopener" class="gear-card">
        <span class="gear-icon">💧</span>
        <div class="gear-name">Water Filtration</div>
        <p class="gear-desc">Sawyer Squeeze or Katadyn BeFree — lightweight, reliable, and trail-tested.</p>
        <span class="gear-link">Shop at REI →</span>
      </a>

      <a href="https://www.rei.com/c/sleeping-bags" target="_blank" rel="noopener" class="gear-card">
        <span class="gear-icon">🏕️</span>
        <div class="gear-name">Shelter &amp; Sleep</div>
        <p class="gear-desc">For hut-to-hut trips and wilderness overnights on the Long Trail or Appalachian Trail.</p>
        <span class="gear-link">Shop at REI →</span>
      </a>

    </div>
  </div>
</div>

<!-- FOOTER -->
<footer>
  <div class="footer-brand">The Ridge Report</div>
  <p class="footer-tagline">New England trail weather, guides, and gear — for hikers who take it seriously.</p>
  <ul class="footer-links">
    <li><a href="#weather">Weather</a></li>
    <li><a href="#trails">Trail Guides</a></li>
    <li><a href="#seasonal">Seasonal Tips</a></li>
    <li><a href="#gear">Gear</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Privacy</a></li>
  </ul>
  <p class="footer-note">
    Weather data sourced from NOAA National Weather Service. Conditions change rapidly in mountain environments — always verify forecasts within hours of departure and carry appropriate safety gear. The Ridge Report is an informational resource and is not responsible for decisions made in the field.<br><br>
    Topographic maps provided by OpenTopoMap, &copy; OpenStreetMap contributors.<br><br>
    &copy; 2025 The Ridge Report &middot; Affiliate links help support this site at no cost to you.
  </p>
</footer>

<script>
const trails = [
  { name:"Mt. Washington",      region:"white-mountains", regionLabel:"White Mountains, NH",    temp:28, condition:"Icy &amp; Windy",   badge:"caution", wind:"52 mph", humidity:"78%", forecast:[{day:"Thu",icon:"🌨️",temp:"24°"},{day:"Fri",icon:"🌥️",temp:"31°"},{day:"Sat",icon:"⛅",temp:"38°"},{day:"Sun",icon:"☀️",temp:"42°"}] },
  { name:"Franconia Ridge",     region:"white-mountains", regionLabel:"White Mountains, NH",    temp:34, condition:"Partly Cloudy",    badge:"good",    wind:"18 mph", humidity:"62%", forecast:[{day:"Thu",icon:"🌥️",temp:"32°"},{day:"Fri",icon:"⛅",temp:"40°"},{day:"Sat",icon:"☀️",temp:"46°"},{day:"Sun",icon:"☀️",temp:"49°"}] },
  { name:"Camel's Hump",        region:"green-mountains", regionLabel:"Green Mountains, VT",    temp:36, condition:"Clear",            badge:"good",    wind:"12 mph", humidity:"55%", forecast:[{day:"Thu",icon:"☀️",temp:"38°"},{day:"Fri",icon:"☀️",temp:"44°"},{day:"Sat",icon:"⛅",temp:"47°"},{day:"Sun",icon:"🌧️",temp:"41°"}] },
  { name:"Mt. Mansfield",       region:"green-mountains", regionLabel:"Green Mountains, VT",    temp:31, condition:"Overcast",         badge:"caution", wind:"28 mph", humidity:"82%", forecast:[{day:"Thu",icon:"🌥️",temp:"33°"},{day:"Fri",icon:"⛅",temp:"39°"},{day:"Sat",icon:"⛅",temp:"43°"},{day:"Sun",icon:"🌧️",temp:"38°"}] },
  { name:"Mt. Katahdin",        region:"maine",           regionLabel:"Baxter State Park, ME",  temp:29, condition:"Snow Possible",   badge:"caution", wind:"22 mph", humidity:"75%", forecast:[{day:"Thu",icon:"🌨️",temp:"27°"},{day:"Fri",icon:"🌥️",temp:"33°"},{day:"Sat",icon:"⛅",temp:"38°"},{day:"Sun",icon:"☀️",temp:"41°"}] },
  { name:"Cadillac Mountain",   region:"maine",           regionLabel:"Acadia NP, ME",          temp:42, condition:"Sunny &amp; Clear", badge:"good",   wind:"9 mph",  humidity:"48%", forecast:[{day:"Thu",icon:"☀️",temp:"45°"},{day:"Fri",icon:"☀️",temp:"50°"},{day:"Sat",icon:"⛅",temp:"52°"},{day:"Sun",icon:"🌧️",temp:"44°"}] },
  { name:"Mt. Greylock",        region:"berkshires",      regionLabel:"Berkshires, MA",         temp:38, condition:"Mostly Clear",    badge:"good",    wind:"11 mph", humidity:"53%", forecast:[{day:"Thu",icon:"☀️",temp:"41°"},{day:"Fri",icon:"☀️",temp:"47°"},{day:"Sat",icon:"⛅",temp:"50°"},{day:"Sun",icon:"🌥️",temp:"45°"}] },
  { name:"Bear Mountain",       region:"connecticut",     regionLabel:"Litchfield Hills, CT",   temp:44, condition:"Clear",            badge:"good",    wind:"7 mph",  humidity:"50%", forecast:[{day:"Thu",icon:"☀️",temp:"47°"},{day:"Fri",icon:"☀️",temp:"53°"},{day:"Sat",icon:"⛅",temp:"55°"},{day:"Sun",icon:"🌧️",temp:"47°"}] },
];

function badgeLabel(b) {
  return b === 'good' ? 'Good Conditions' : b === 'caution' ? 'Use Caution' : 'Poor Conditions';
}

function renderCards(filter) {
  const grid = document.getElementById('trailGrid');
  const list = filter === 'all' ? trails : trails.filter(t => t.region === filter);
  grid.innerHTML = list.map(t => `
    <div class="trail-card" data-region="${t.region}">
      <div class="trail-name">${t.name}</div>
      <div class="trail-region">${t.regionLabel}</div>
      <span class="conditions-badge badge-${t.badge}">${badgeLabel(t.badge)}</span>
      <div class="weather-display">
        <div class="temp-big">${t.temp}&deg;</div>
        <div class="weather-meta">
          ${t.condition}<br>
          Wind: ${t.wind}<br>
          Humidity: ${t.humidity}
        </div>
      </div>
      <div class="forecast-row">
        ${t.forecast.map(f => `
          <div class="forecast-day">
            ${f.day}
            <span class="f-icon">${f.icon}</span>
            <span class="f-temp">${f.temp}</span>
          </div>
        `).join('')}
      </div>
    </div>
  `).join('');
}

function filterRegion(region, btn) {
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  btn.classList.add('active');
  renderCards(region);
}

renderCards('all');

document.querySelectorAll('a[href^="#"]').forEach(a => {
  a.addEventListener('click', e => {
    const target = document.querySelector(a.getAttribute('href'));
    if (target) { e.preventDefault(); target.scrollIntoView({ behavior:'smooth', block:'start' }); }
  });
});
</script>
</body>
</html>
