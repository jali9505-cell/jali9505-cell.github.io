<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Twenty8Productions — Creative & Technical Design Studio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500;600&family=Familjen+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --white: #ffffff;
  --off-white: #f0f7ff;
  --paper: #ddeeff;
  --ink: #1a2340;
  --ink-light: #2e3d60;
  --gray: #5a6a8a;
  --gray-light: #a0b0cc;
  --punch1: #ff5a1f;
  --punch2: #2563ff;
  --punch3: #00d4a0;
  --punch4: #ffc000;
  --font-display: 'DM Serif Display', serif;
  --font-ui: 'Familjen Grotesk', sans-serif;
  --font-body: 'DM Sans', sans-serif;
  --nav-h: 72px;
  --ease: cubic-bezier(0.22, 1, 0.36, 1);
}
html { scroll-behavior: smooth; }
body {
  background: var(--white);
  color: var(--ink);
  font-family: var(--font-body);
  font-weight: 400;
  line-height: 1.6;
  overflow-x: hidden;
  cursor: none;
}

/* CURSOR */
.cursor { position:fixed; width:10px; height:10px; background:var(–punch1); border-radius:50%; pointer-events:none; z-index:9999; transform:translate(-50%,-50%); transition:width .3s var(–ease),height .3s var(–ease),background .3s; mix-blend-mode:multiply; }
.cursor-ring { position:fixed; width:40px; height:40px; border:1.5px solid rgba(255,77,28,.35); border-radius:50%; pointer-events:none; z-index:9998; transform:translate(-50%,-50%); transition:width .4s var(–ease),height .4s var(–ease),border-color .3s; }
body:has(a:hover) .cursor,body:has(button:hover) .cursor { width:18px; height:18px; }
body:has(a:hover) .cursor-ring,body:has(button:hover) .cursor-ring { width:60px; height:60px; border-color:var(–punch1); }

/* NAV */
nav { position:fixed; top:0; left:0; right:0; height:var(–nav-h); display:flex; align-items:center; justify-content:space-between; padding:0 40px; z-index:1000; background:rgba(255,255,255,.95); backdrop-filter:blur(12px); border-bottom:1.5px solid var(–paper); box-shadow:0 1px 24px rgba(37,99,255,.06); }
.nav-logo { font-family:var(–font-ui); font-size:17px; font-weight:700; color:var(–ink); text-decoration:none; display:flex; align-items:center; gap:0; }
.nav-logo .num { display:inline-flex; align-items:center; justify-content:center; width:28px; height:28px; background:var(–punch1); color:#fff; font-size:14px; font-weight:700; border-radius:4px; margin:0 2px; transition:background .3s; }
.nav-logo:hover .num { background:var(–punch2); }
.nav-links { display:flex; align-items:center; gap:36px; list-style:none; }
.nav-links a { font-family:var(–font-ui); font-size:13px; font-weight:500; color:var(–gray); text-decoration:none; transition:color .2s; }
.nav-links a:hover { color:var(–ink); }
.nav-cta { font-family:var(–font-ui); font-size:13px; font-weight:600; color:#fff !important; background:var(–ink); padding:10px 22px; border-radius:100px; text-decoration:none !important; transition:background .3s,transform .2s !important; }
.nav-cta:hover { background:var(–punch1) !important; transform:translateY(-1px); }
.hamburger { display:none; flex-direction:column; gap:5px; background:none; border:none; cursor:none; padding:4px; }
.hamburger span { display:block; width:24px; height:1.5px; background:var(–ink); transition:all .3s; }

/* PAGE SYSTEM */
.page { display:none; }
.page.active { display:block; }

/* MOBILE NAV */
.mobile-nav { display:none; position:fixed; inset:0; background:var(–white); z-index:999; flex-direction:column; align-items:flex-start; justify-content:center; padding:60px 40px; gap:8px; border-left:4px solid var(–punch1); }
.mobile-nav.open { display:flex; }
.mobile-nav a { font-family:var(–font-display); font-size:48px; color:var(–ink); text-decoration:none; transition:color .2s; line-height:1.2; }
.mobile-nav a:hover { color:var(–punch1); }
.mobile-close { position:absolute; top:24px; right:32px; background:none; border:none; font-size:28px; cursor:none; color:var(–ink); }

/* REVEAL */
.reveal { opacity:0; transform:translateY(20px); transition:opacity .7s var(–ease),transform .7s var(–ease); }
.reveal.visible { opacity:1; transform:none; }
.reveal-d1 { transition-delay:.08s; }
.reveal-d2 { transition-delay:.16s; }
.reveal-d3 { transition-delay:.24s; }
.reveal-d4 { transition-delay:.32s; }

/* BUTTONS */
.btn { display:inline-flex; align-items:center; gap:10px; font-family:var(–font-ui); font-size:13px; font-weight:600; letter-spacing:0.02em; padding:13px 28px; border-radius:100px; text-decoration:none; cursor:none; border:none; transition:transform .25s var(–ease),background .25s; }
.btn:hover { transform:translateY(-2px); }
.btn-dark { background:var(–ink); color:#fff; }
.btn-dark:hover { background:var(–punch1); }.btn-outline { background:transparent; color:var(–ink); border:1.5px solid var(–ink); }
.btn-outline:hover { background:var(–ink); color:#fff; }
.btn-punch { background:#fff; color:var(–punch2); }
.btn-punch:hover { background:var(–punch4); color:var(–ink); }
.btn-arrow::after { content:‘→’; font-size:16px; }

/* LABEL */
.label { font-family:var(–font-ui); font-size:11px; font-weight:600; letter-spacing:0.12em; text-transform:uppercase; color:var(–gray); display:inline-flex; align-items:center; gap:10px; }
.label::before { content:’’; display:block; width:20px; height:1.5px; background:currentColor; }

/* TICKER */
.ticker-row { background:linear-gradient(90deg,var(–punch2),#5b21b6); overflow:hidden; padding:14px 0; white-space:nowrap; }
.ticker-inner { display:inline-flex; animation:ticker 30s linear infinite; }
.ticker-item { font-family:var(–font-ui); font-size:12px; font-weight:600; letter-spacing:0.1em; text-transform:uppercase; color:var(–white); padding:0 32px; display:flex; align-items:center; gap:32px; }
.ticker-item::after { content:‘✦’; color:var(–punch1); }
@keyframes ticker { from{transform:translateX(0)} to{transform:translateX(-50%)} }

/* ══ HOME HERO ══ */
.hero { min-height:100vh; padding:calc(var(–nav-h) + 60px) 40px 80px; display:grid; grid-template-columns:1fr 1fr; gap:0 48px; align-items:start; background:linear-gradient(160deg, #eef6ff 0%, #ffffff 50%, #fff4ee 100%); }
.hero-left { display:flex; flex-direction:column; }
.hero-eyebrow { font-family:var(–font-ui); font-size:11px; font-weight:600; letter-spacing:0.14em; text-transform:uppercase; color:var(–punch1); margin-bottom:24px; display:flex; align-items:center; gap:10px; opacity:0; animation:fadeUp .6s var(–ease) .2s forwards; }
.hero-eyebrow::before { content:’’; display:block; width:20px; height:1.5px; background:var(–punch1); }
.hero-h1 { font-family:var(–font-display); font-size:clamp(52px,6.5vw,96px); line-height:1.0; letter-spacing:-0.025em; color:var(–ink); margin-bottom:36px; opacity:0; animation:fadeUp .8s var(–ease) .35s forwards; }
.hero-h1 em { font-style:italic; color:var(–punch2); }
.underline-red { position:relative; display:inline-block; }
.underline-red::after { content:’’; position:absolute; left:0; bottom:4px; width:100%; height:4px; background:var(–punch1); border-radius:2px; }
.hero-body { font-size:17px; line-height:1.65; color:var(–gray); max-width:440px; margin-bottom:40px; opacity:0; animation:fadeUp .7s var(–ease) .55s forwards; }
.hero-actions { display:flex; gap:14px; flex-wrap:wrap; opacity:0; animation:fadeUp .7s var(–ease) .7s forwards; }
.hero-media { display:grid; grid-template-columns:1fr 1fr; grid-template-rows:260px 200px; gap:12px; opacity:0; animation:fadeUp .9s var(–ease) .4s forwards; }
.hm-card { border-radius:16px; overflow:hidden; position:relative; }
.hm-card:nth-child(1) { grid-row:span 2; }
.hm-inner { position:absolute; inset:0; display:flex; flex-direction:column; justify-content:flex-end; padding:20px; }
.hm-tag { font-family:var(–font-ui); font-size:10px; font-weight:600; letter-spacing:0.1em; text-transform:uppercase; background:rgba(255,255,255,.9); color:var(–ink); padding:5px 10px; border-radius:100px; display:inline-block; backdrop-filter:blur(4px); }

/* project mock visuals */
.proj-elara { background:linear-gradient(135deg,#1e3a8a,#2563ff); display:flex; align-items:center; justify-content:center; }
.proj-meridian { background:#f0ede6; display:flex; align-items:center; justify-content:center; }
.proj-vance { background:#fff9f0; display:flex; align-items:center; justify-content:center; flex-direction:column; gap:8px; }
.proj-vance-logo { width:72px; height:72px; border-radius:50%; background:var(–punch4); display:flex; align-items:center; justify-content:center; font-family:var(–font-display); font-size:30px; color:var(–ink); font-style:italic; }
.bottle { width:28px; border-radius:14px 14px 4px 4px; background:linear-gradient(180deg,#1a2a1a,#0a1a0a); border:1px solid rgba(255,255,255,.1); position:relative; }
.bottle::before { content:’’; position:absolute; top:-14px; left:50%; transform:translateX(-50%); width:10px; height:16px; background:rgba(255,255,255,.1); border-radius:3px 3px 0 0; }

/* ══ INTRO STRIP ══ */
.intro-strip { padding:100px 40px; display:grid; grid-template-columns:1fr 1.4fr; gap:80px; align-items:center; border-top:1.5px solid var(–paper); }
.intro-number { font-family:var(–font-display); font-size:clamp(100px,15vw,180px); line-height:1; color:var(–paper); letter-spacing:-0.04em; user-select:none; }
.intro-right h2 { font-family:var(–font-display); font-size:clamp(34px,4vw,52px); line-height:1.1; letter-spacing:-0.02em; color:var(–ink); margin-bottom:20px; }
.intro-right h2 em { font-style:italic; color:var(–punch2); }
.intro-right p { font-size:16px; line-height:1.75; color:var(–gray); margin-bottom:16px; }
.pill-row { display:flex; gap:10px; flex-wrap:wrap; margin-top:28px; }
.pill { font-family:var(–font-ui); font-size:12px; font-weight:600; letter-spacing:0.05em; padding:8px 18px; border-radius:100px; border:1.5px solid var(–ink); color:var(–ink); }
.pill.active { background:var(–ink); color:var(–white); }

/* ══ WORK MOSAIC ══ */
.work-section { padding:0 40px 100px; }
.section-head { display:flex; justify-content:space-between; align-items:flex-end; margin-bottom:48px; }
.section-head h2 { font-family:var(–font-display); font-size:clamp(36px,4.5vw,60px); letter-spacing:-0.02em; line-height:1.05; }
.section-head h2 em { font-style:italic; color:var(–punch1); }
.work-mosaic { display:grid; grid-template-columns:repeat(12,1fr); grid-auto-rows:80px; gap:12px; }
.wm { border-radius:16px; overflow:hidden; position:relative; }
.wm-a { grid-column:span 5; grid-row:span 5; }
.wm-b { grid-column:span 7; grid-row:span 3; }
.wm-c { grid-column:span 4; grid-row:span 2; }
.wm-d { grid-column:span 3; grid-row:span 2; }
.wm-e { grid-column:span 4; grid-row:span 3; }
.wm-f { grid-column:span 4; grid-row:span 3; }
.wm-g { grid-column:span 4; grid-row:span 3; }
.wm-bg { position:absolute; inset:0; transition:transform .6s var(–ease); }
.wm:hover .wm-bg { transform:scale(1.04); }
.wm-caption { position:absolute; bottom:0; left:0; right:0; padding:20px 22px; background:linear-gradient(to top,rgba(10,10,10,.75),transparent); transform:translateY(6px); opacity:0; transition:all .4s var(–ease); }
.wm:hover .wm-caption { transform:none; opacity:1; }
.wm-caption-cat { font-family:var(–font-ui); font-size:10px; font-weight:600; letter-spacing:0.12em; text-transform:uppercase; color:rgba(255,255,255,.7); margin-bottom:3px; }
.wm-caption-title { font-family:var(–font-display); font-size:20px; color:#fff; }
.wb1 { background:linear-gradient(135deg,#1e3a8a,#2563ff); display:flex; align-items:center; justify-content:center; }
.wb2 { background:linear-gradient(135deg,#f0f7ff,#dbeafe); display:flex; align-items:center; justify-content:center; }
.wb3 { background:linear-gradient(135deg,#fffbeb,#fef3c7); display:flex; align-items:center; justify-content:center; }
.wb4 { background:linear-gradient(135deg,#1e1b4b,#312e81); display:flex; align-items:center; justify-content:center; }
.wb5 { background:linear-gradient(135deg,#ecfdf5,#d1fae5); display:flex; align-items:center; justify-content:center; }
.wb6 { background:linear-gradient(135deg,#fff7ed,#ffedd5); display:flex; align-items:center; justify-content:center; }
.wb7 { background:linear-gradient(135deg,#faf5ff,#ede9fe); display:flex; align-items:center; justify-content:center; }

/* ══ SERVICES SPLIT ══ */
.services-split { display:grid; grid-template-columns:1fr 1fr; border-top:1.5px solid var(–paper); }
.svc-col { padding:80px 56px; }
.svc-col:first-child { border-right:1.5px solid var(–paper); }
.svc-num { font-family:var(–font-ui); font-size:11px; font-weight:600; letter-spacing:0.14em; text-transform:uppercase; color:var(–gray-light); margin-bottom:8px; }
.svc-col-title { font-family:var(–font-display); font-size:clamp(32px,3.5vw,48px); letter-spacing:-0.02em; line-height:1.05; margin-bottom:18px; }
.svc-col-title em { font-style:italic; }
.svc-col:first-child .svc-col-title em { color:var(–punch1); }
.svc-col:last-child .svc-col-title em { color:var(–punch2); }
.svc-col p { font-size:15px; color:var(–gray); line-height:1.75; margin-bottom:36px; }
.svc-list { list-style:none; }
.svc-list li { font-family:var(–font-ui); font-size:14px; font-weight:500; color:var(–ink-light); padding:14px 0; border-bottom:1px solid var(–paper); display:flex; align-items:center; justify-content:space-between; transition:color .2s; cursor:default; }
.svc-list li:hover { color:var(–ink); }
.svc-list li .arrow { color:var(–gray-light); font-size:12px; transition:transform .3s; }
.svc-list li:hover .arrow { transform:translateX(4px); color:var(–punch1); }
.svc-visual { margin-top:40px; height:220px; border-radius:16px; overflow:hidden; position:relative; display:flex; align-items:center; justify-content:center; }

/* ══ CTA BAND ══ */
.cta-band { background:linear-gradient(135deg,#2563ff 0%,#1a40c8 100%); padding:100px 40px; display:grid; grid-template-columns:1fr auto; gap:40px; align-items:center; }
.cta-band h2 { font-family:var(–font-display); font-size:clamp(36px,5vw,72px); letter-spacing:-0.025em; line-height:1.0; color:#fff; }
.cta-band h2 em { font-style:italic; color:var(–punch4); }
.cta-band-right { display:flex; flex-direction:column; align-items:flex-end; gap:16px; }
.cta-band-right p { font-size:15px; color:rgba(255,255,255,.75); text-align:right; max-width:280px; }

/* ══ FOOTER ══ */
footer { background:var(–off-white); border-top:1.5px solid var(–paper); padding:64px 40px 36px; }
.footer-top { display:grid; grid-template-columns:1.8fr 1fr 1fr 1fr; gap:48px; margin-bottom:56px; }
.footer-brand-name { font-family:var(–font-ui); font-size:16px; font-weight:700; color:var(–ink); margin-bottom:12px; display:flex; align-items:center; gap:3px; }
.footer-brand-name .num { display:inline-flex; align-items:center; justify-content:center; width:22px; height:22px; background:var(–punch1); color:#fff; font-size:11px; font-weight:700; border-radius:3px; }
.footer-brand p { font-size:14px; color:var(–gray); line-height:1.65; max-width:240px; }
.footer-col h5 { font-family:var(–font-ui); font-size:11px; font-weight:600; letter-spacing:0.12em; text-transform:uppercase; color:var(–gray-light); margin-bottom:18px; }
.footer-col ul { list-style:none; }
.footer-col ul li { margin-bottom:10px; }
.footer-col ul a,.footer-col p { font-size:14px; color:var(–gray); text-decoration:none; transition:color .2s; }
.footer-col ul a:hover { color:var(–ink); }
.footer-bottom { display:flex; justify-content:space-between; align-items:center; padding-top:28px; border-top:1px solid var(–paper); }
.footer-bottom p { font-size:12px; color:var(–gray-light); }
.footer-legal { display:flex; gap:20px; }
.footer-legal a { font-size:12px; color:var(–gray-light); text-decoration:none; transition:color .2s; }
.footer-legal a:hover { color:var(–gray); }

/* ══ PAGE HERO ══ */
.page-hero { padding:calc(var(–nav-h)+70px) 40px 60px; border-bottom:1.5px solid var(–paper); position:relative; overflow:hidden; background:linear-gradient(160deg,#eef6ff 0%,#ffffff 60%,#fff4ee 100%); }
.page-hero-bg-num { position:absolute; right:-20px; top:50%; transform:translateY(-50%); font-family:var(–font-display); font-size:280px; line-height:1; color:var(–paper); pointer-events:none; letter-spacing:-0.05em; user-select:none; }
.page-hero h1 { font-family:var(–font-display); font-size:clamp(56px,8vw,108px); letter-spacing:-0.03em; line-height:.95; position:relative; z-index:1; margin-bottom:20px; }
.page-hero h1 em { font-style:italic; }
.page-hero p { font-size:17px; color:var(–gray); max-width:520px; line-height:1.7; position:relative; z-index:1; }

/* ══ SERVICES PAGE ══ */
.services-page-section { padding:80px 40px; border-bottom:1.5px solid var(–paper); }
.services-page-section.alt { background:var(–off-white); }.sp-grid { display:grid; grid-template-columns:repeat(3,1fr); gap:16px; margin-top:48px; }
.sp-card { background:var(–white); border-radius:20px; padding:40px 32px; border:1.5px solid var(–paper); transition:border-color .3s,transform .3s var(–ease),box-shadow .3s; }
.sp-card:hover { border-color:var(–punch1); transform:translateY(-4px); box-shadow:0 16px 48px rgba(255,90,31,.1); }
.services-page-section.alt .sp-card:hover { border-color:var(–punch2); box-shadow:0 16px 48px rgba(37,99,255,.1); }
.sp-card-num { font-family:var(–font-ui); font-size:11px; font-weight:600; letter-spacing:0.12em; color:var(–gray-light); margin-bottom:20px; }
.sp-icon { width:48px; height:48px; border-radius:12px; display:flex; align-items:center; justify-content:center; margin-bottom:20px; font-size:22px; }
.sp-icon-orange { background:rgba(255,77,28,.1); }
.sp-icon-blue { background:rgba(26,86,255,.1); }
.sp-card h3 { font-family:var(–font-display); font-size:26px; letter-spacing:-0.01em; color:var(–ink); margin-bottom:12px; }
.sp-card p { font-size:14px; color:var(–gray); line-height:1.7; margin-bottom:24px; }
.sp-features { list-style:none; }
.sp-features li { font-family:var(–font-ui); font-size:13px; font-weight:500; color:var(–ink-light); padding:9px 0; border-bottom:1px solid var(–off-white); display:flex; align-items:center; gap:10px; }
.sp-features li::before { content:’—’; color:var(–punch1); font-size:10px; }
.services-page-section.alt .sp-features li::before { color:var(–punch2); }

/* ══ PORTFOLIO PAGE ══ */
.portfolio-page { padding:60px 40px 100px; }
.filter-row { display:flex; gap:8px; margin-bottom:48px; flex-wrap:wrap; }
.filt { font-family:var(–font-ui); font-size:12px; font-weight:600; letter-spacing:0.05em; padding:9px 20px; border-radius:100px; background:none; border:1.5px solid var(–paper); color:var(–gray); cursor:none; transition:all .25s; }
.filt:hover,.filt.active { background:var(–ink); color:var(–white); border-color:var(–ink); }
.pf-grid { display:grid; grid-template-columns:repeat(3,1fr); gap:16px; }
.pf-tile { border-radius:20px; overflow:hidden; aspect-ratio:4/3; position:relative; cursor:none; }
.pf-tile-bg { position:absolute; inset:0; transition:transform .6s var(–ease); display:flex; align-items:center; justify-content:center; }
.pf-tile:hover .pf-tile-bg { transform:scale(1.04); }
.pf-tile-overlay { position:absolute; inset:0; border-radius:20px; background:rgba(17,16,16,0); transition:background .4s; display:flex; flex-direction:column; justify-content:flex-end; padding:24px; }
.pf-tile:hover .pf-tile-overlay { background:rgba(17,16,16,.72); }
.pf-tile-info { opacity:0; transform:translateY(10px); transition:all .4s var(–ease); }
.pf-tile:hover .pf-tile-info { opacity:1; transform:none; }
.pf-tile-cat { font-family:var(–font-ui); font-size:10px; font-weight:600; letter-spacing:0.12em; text-transform:uppercase; color:var(–punch1); margin-bottom:4px; }
.pf-tile-name { font-family:var(–font-display); font-size:22px; color:#fff; }
.pf-tile-desc { font-size:13px; color:rgba(255,255,255,.7); margin-top:4px; }
.ptb1{background:linear-gradient(135deg,#1e3a8a,#2563ff);}
.ptb2{background:linear-gradient(135deg,#f0f7ff,#dbeafe);}
.ptb3{background:linear-gradient(135deg,#fffbeb,#fef3c7);}
.ptb4{background:linear-gradient(135deg,#1e1b4b,#312e81);}
.ptb5{background:linear-gradient(135deg,#ecfdf5,#d1fae5);}
.ptb6{background:linear-gradient(135deg,#fff7ed,#ffedd5);}
.ptb7{background:linear-gradient(135deg,#faf5ff,#ede9fe);}
.ptb8{background:linear-gradient(135deg,#f0fdf4,#dcfce7);}
.ptb9{background:linear-gradient(135deg,#fffbeb,#fef9c3);}

/* ══ ABOUT PAGE ══ */
.about-intro { padding:80px 40px; display:grid; grid-template-columns:1fr 1fr; gap:80px; align-items:start; border-bottom:1.5px solid var(–paper); }
.about-intro h2 { font-family:var(–font-display); font-size:clamp(36px,4.5vw,60px); letter-spacing:-0.025em; line-height:1.0; margin-bottom:24px; }
.about-intro h2 em { font-style:italic; color:var(–punch1); }
.about-intro p { font-size:16px; color:var(–gray); line-height:1.8; margin-bottom:16px; }
.stats-row { display:grid; grid-template-columns:repeat(4,1fr); border-top:1.5px solid var(–paper); border-bottom:1.5px solid var(–paper); }
.stat-cell { padding:56px 40px; text-align:center; border-right:1.5px solid var(–paper); }
.stat-cell:last-child { border-right:none; }
.stat-big { font-family:var(–font-display); font-size:clamp(52px,5vw,72px); line-height:1; letter-spacing:-0.03em; color:var(–ink); display:block; margin-bottom:8px; }
.stat-big span { color:var(–punch1); }
.stat-label { font-family:var(–font-ui); font-size:12px; font-weight:600; letter-spacing:0.1em; text-transform:uppercase; color:var(–gray); }
.values-section { padding:80px 40px; background:var(–off-white); }.values-grid { display:grid; grid-template-columns:repeat(4,1fr); gap:16px; margin-top:48px; }
.val-card { background:var(–white); border-radius:20px; padding:36px 28px; transition:transform .3s var(–ease),box-shadow .3s; }
.val-card:hover { transform:translateY(-6px); box-shadow:0 20px 48px rgba(0,0,0,.07); }
.val-emoji { font-size:32px; margin-bottom:16px; display:block; }
.val-card h4 { font-family:var(–font-display); font-size:22px; margin-bottom:10px; }
.val-card p { font-size:13px; color:var(–gray); line-height:1.65; }
.disciplines-section { padding:80px 40px; display:grid; grid-template-columns:1fr 1fr; gap:24px; border-bottom:1.5px solid var(–paper); }
.disc-card { border-radius:24px; padding:48px 40px; }
.disc-card.creative { background:linear-gradient(135deg,#fff4ee,#ffe8d6); }
.disc-card.technical { background:linear-gradient(135deg,#eef4ff,#dbeafe); }
.disc-card h3 { font-family:var(–font-display); font-size:clamp(28px,3vw,40px); letter-spacing:-0.02em; line-height:1.05; margin-bottom:16px; }
.disc-card p { font-size:15px; color:var(–gray); line-height:1.75; }

/* ══ CONTACT PAGE ══ */
.contact-grid { display:grid; grid-template-columns:1fr 1.2fr; gap:0; border-top:1.5px solid var(–paper); }
.contact-info-panel { padding:80px 56px; border-right:1.5px solid var(–paper); }
.contact-info-panel h2 { font-family:var(–font-display); font-size:clamp(36px,4.5vw,60px); letter-spacing:-0.025em; line-height:1.0; margin-bottom:20px; }
.contact-info-panel h2 em { font-style:italic; color:var(–punch1); }
.contact-info-panel>p { font-size:16px; color:var(–gray); line-height:1.75; margin-bottom:48px; }
.contact-detail { display:flex; gap:16px; padding:20px 0; border-bottom:1px solid var(–paper); align-items:flex-start; }
.cd-dot { width:36px; height:36px; border-radius:50%; background:var(–off-white); display:flex; align-items:center; justify-content:center; flex-shrink:0; font-size:15px; }
.cd-text label { font-family:var(–font-ui); font-size:10px; font-weight:600; letter-spacing:0.12em; text-transform:uppercase; color:var(–gray-light); display:block; margin-bottom:3px; }
.cd-text p { font-size:15px; color:var(–ink); font-weight:500; }
.contact-form-panel { padding:80px 56px; background:var(–off-white); }.form-title { font-family:var(–font-ui); font-size:11px; font-weight:600; letter-spacing:0.14em; text-transform:uppercase; color:var(–gray-light); margin-bottom:36px; }
.form-row { display:grid; grid-template-columns:1fr 1fr; gap:14px; }
.form-group { margin-bottom:16px; }
.form-group label { font-family:var(–font-ui); font-size:11px; font-weight:600; letter-spacing:0.1em; text-transform:uppercase; color:var(–gray); display:block; margin-bottom:7px; }
.form-group input,.form-group select,.form-group textarea { width:100%; background:var(–white); border:1.5px solid var(–paper); color:var(–ink); font-family:var(–font-body); font-size:15px; padding:13px 16px; outline:none; border-radius:10px; transition:border-color .25s; -webkit-appearance:none; cursor:none; }
.form-group input:focus,.form-group select:focus,.form-group textarea:focus { border-color:var(–punch1); }
.form-group textarea { resize:none; height:120px; }
.form-group select option { background:var(–white); }
.form-submit { width:100%; background:var(–ink); color:#fff; font-family:var(–font-ui); font-size:14px; font-weight:600; letter-spacing:0.05em; padding:16px; border-radius:100px; border:none; cursor:none; transition:background .3s; margin-top:8px; }
.form-submit:hover { background:var(–punch1); }

@keyframes fadeUp { from{opacity:0;transform:translateY(24px)} to{opacity:1;transform:none} }
@keyframes fadeIn { from{opacity:0} to{opacity:1} }

/* ══ RESPONSIVE ══ */
@media(max-width:1024px){
.hero{grid-template-columns:1fr;}
.hero-right{display:none;}
.intro-strip{grid-template-columns:1fr;gap:24px;}
.intro-number{font-size:80px;}
.services-split{grid-template-columns:1fr;}
.svc-col:first-child{border-right:none;border-bottom:1.5px solid var(–paper);}
.sp-grid{grid-template-columns:1fr 1fr;}
.pf-grid{grid-template-columns:1fr 1fr;}
.values-grid{grid-template-columns:1fr 1fr;}
.stats-row{grid-template-columns:1fr 1fr;}
.stat-cell{border-bottom:1.5px solid var(–paper);}
.about-intro{grid-template-columns:1fr;gap:40px;}
.disciplines-section{grid-template-columns:1fr;}
.contact-grid{grid-template-columns:1fr;}
.contact-info-panel{border-right:none;border-bottom:1.5px solid var(–paper);}
.footer-top{grid-template-columns:1fr 1fr;gap:40px;}
.cta-band{grid-template-columns:1fr;}
.cta-band-right{align-items:flex-start;}
.cta-band-right p{text-align:left;}
}
@media(max-width:768px){
nav{padding:0 20px;}
.nav-links{display:none;}
.hamburger{display:flex;}
.hero{padding:calc(var(–nav-h)+40px) 20px 60px;}
.ticker-row{display:none;}
.intro-strip,.work-section,.services-split,.about-intro,.disciplines-section,.values-section{padding-left:20px;padding-right:20px;}
.sp-grid,.pf-grid{grid-template-columns:1fr;}
.values-grid{grid-template-columns:1fr;}
.stats-row{grid-template-columns:1fr 1fr;}
.page-hero{padding-left:20px;padding-right:20px;}
.contact-info-panel,.contact-form-panel{padding:60px 20px;}
.portfolio-page{padding:40px 20px 80px;}
.services-page-section{padding:60px 20px;}
.footer-top,footer{padding-left:20px;padding-right:20px;}
.cta-band{padding:60px 20px;}
.work-mosaic{display:grid;grid-template-columns:1fr 1fr;grid-auto-rows:180px;}
.wm-a,.wm-b,.wm-c,.wm-d,.wm-e,.wm-f,.wm-g{grid-column:span 1;grid-row:span 1;}
body{cursor:auto;}
.cursor,.cursor-ring{display:none;}
}
</style>

</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<nav id="mainNav">
  <a href="#" class="nav-logo" onclick="showPage('home')">Twenty<span class="num">8</span>Productions</a>
  <ul class="nav-links">
    <li><a href="#" onclick="showPage('home')">Home</a></li>
    <li><a href="#" onclick="showPage('services')">Services</a></li>
    <li><a href="#" onclick="showPage('portfolio')">Work</a></li>
    <li><a href="#" onclick="showPage('about')">About</a></li>
    <li><a href="#" class="nav-cta" onclick="showPage('contact')">Get a Quote</a></li>
  </ul>
  <button class="hamburger" id="hamburger"><span></span><span></span><span></span></button>
</nav>

<div class="mobile-nav" id="mobileNav">
  <button class="mobile-close" id="mobileClose">✕</button>
  <a href="#" onclick="showPage('home');closeMobileNav()">Home</a>
  <a href="#" onclick="showPage('services');closeMobileNav()">Services</a>
  <a href="#" onclick="showPage('portfolio');closeMobileNav()">Work</a>
  <a href="#" onclick="showPage('about');closeMobileNav()">About</a>
  <a href="#" onclick="showPage('contact');closeMobileNav()">Contact</a>
</div>

<!-- ═══════ HOME ═══════ -->

<div class="page active" id="page-home">
  <section class="hero">
    <div class="hero-left">
      <p class="hero-eyebrow">Multidisciplinary Studio — Est. 2012</p>
      <h1 class="hero-h1">Creative.<br><em>Technical.</em><br><span class="underline-red">One Studio.</span></h1>
      <p class="hero-body">Brand design that stops you in your tracks. Construction documents that build with confidence. Twenty8Productions does both — at the same uncommon standard.</p>
      <div class="hero-actions">
        <a href="#" class="btn btn-dark btn-arrow" onclick="showPage('portfolio')">See Our Work</a>
        <a href="#" class="btn btn-outline" onclick="showPage('contact')">Start a Project</a>
      </div>
    </div>
    <div class="hero-right">
      <div class="hero-media">
        <div class="hm-card proj-elara">
          <svg width="90" height="200" viewBox="0 0 90 200" fill="none" style="position:relative;z-index:1">
            <rect x="20" y="15" width="50" height="160" rx="6" fill="rgba(255,255,255,.06)" stroke="rgba(255,255,255,.2)" stroke-width="1.2"/>
            <rect x="30" y="5" width="30" height="18" rx="2" fill="rgba(255,255,255,.08)" stroke="rgba(255,255,255,.15)" stroke-width="1"/>
            <rect x="24" y="55" width="42" height="50" rx="2" fill="rgba(26,86,255,.2)" stroke="rgba(26,86,255,.5)" stroke-width="0.8"/>
            <text x="45" y="85" fill="rgba(255,255,255,.6)" font-size="13" text-anchor="middle" font-family="Georgia,serif" font-style="italic">Elara</text>
            <circle cx="45" cy="148" r="14" stroke="rgba(255,255,255,.1)" stroke-width="0.8"/>
          </svg>
          <div class="hm-inner"><span class="hm-tag">Packaging · Elara Spirits</span></div>
        </div>
        <div class="hm-card proj-meridian" style="background:#eef6ff">
          <svg width="160" height="100" viewBox="0 0 160 100" fill="none" style="position:relative;z-index:1;opacity:.5">
            <line x1="10" y1="50" x2="150" y2="50" stroke="#111" stroke-width="1.5"/>
            <line x1="10" y1="25" x2="60" y2="25" stroke="#111" stroke-width="1.2"/>
            <line x1="60" y1="25" x2="60" y2="75" stroke="#111" stroke-width="1.2"/>
            <line x1="60" y1="75" x2="110" y2="75" stroke="#111" stroke-width="1.2"/>
            <circle cx="35" cy="50" r="8" fill="none" stroke="#ff4d1c" stroke-width="1.5"/>
            <circle cx="85" cy="50" r="8" fill="none" stroke="#ff4d1c" stroke-width="1.5"/>
            <rect x="52" y="17" width="16" height="16" fill="none" stroke="#1a56ff" stroke-width="1"/>
          </svg>
          <div class="hm-inner"><span class="hm-tag">MEP · Meridian Tower</span></div>
        </div>
        <div class="hm-card proj-vance" style="background:#fffbeb">
          <div class="proj-vance-logo">V</div>
          <div class="hm-inner" style="justify-content:flex-end;"><span class="hm-tag">Brand · Vance & Co.</span></div>
        </div>
      </div>
    </div>
  </section>

  <div class="ticker-row">
    <div class="ticker-inner">
      <span class="ticker-item">Packaging Design</span><span class="ticker-item">Label Design</span><span class="ticker-item">Brand Identity</span><span class="ticker-item">Plumbing Systems</span><span class="ticker-item">MEP Coordination</span><span class="ticker-item">Construction Docs</span>
      <span class="ticker-item">Packaging Design</span><span class="ticker-item">Label Design</span><span class="ticker-item">Brand Identity</span><span class="ticker-item">Plumbing Systems</span><span class="ticker-item">MEP Coordination</span><span class="ticker-item">Construction Docs</span>
    </div>
  </div>

  <section class="intro-strip">
    <div class="intro-number reveal">28</div>
    <div class="intro-right reveal reveal-d1">
      <div class="label" style="margin-bottom:20px;">Our Studio</div>
      <h2>Where a <em>brand identity</em> and a pipe isometric get the same obsessive treatment.</h2>
      <p style="margin-top:16px;">We built Twenty8Productions because great design should be rigorous and great engineering should be clear. We're the rare studio that lives at that intersection.</p>
      <div class="pill-row">
        <span class="pill active">Creative Design</span>
        <span class="pill">Brand Identity</span>
        <span class="pill">Plumbing Systems</span>
        <span class="pill">MEP Engineering</span>
      </div>
    </div>
  </section>

  <section class="work-section">
    <div class="section-head reveal">
      <div><div class="label" style="margin-bottom:12px;">Selected Work</div><h2>What we've<br><em>built.</em></h2></div>
      <a href="#" class="btn btn-outline" onclick="showPage('portfolio')">Full Portfolio →</a>
    </div>
    <div class="work-mosaic reveal reveal-d1">
      <div class="wm wm-a"><div class="wm-bg wb1">
        <svg width="90" height="200" viewBox="0 0 90 200" fill="none"><rect x="20" y="15" width="50" height="160" rx="6" fill="rgba(255,255,255,.06)" stroke="rgba(255,255,255,.2)" stroke-width="1.2"/><rect x="30" y="5" width="30" height="18" rx="2" fill="rgba(255,255,255,.08)" stroke="rgba(255,255,255,.15)" stroke-width="1"/><rect x="24" y="55" width="42" height="48" rx="2" fill="rgba(26,86,255,.18)" stroke="rgba(26,86,255,.4)" stroke-width="0.8"/><text x="45" y="82" fill="rgba(255,255,255,.55)" font-size="12" text-anchor="middle" font-family="Georgia,serif" font-style="italic">Elara</text><circle cx="45" cy="148" r="14" stroke="rgba(255,255,255,.1)" stroke-width="0.8"/></svg>
      </div><div class="wm-caption"><div class="wm-caption-cat">Packaging Design</div><div class="wm-caption-title">Elara Spirits</div></div></div>

```
  <div class="wm wm-b"><div class="wm-bg wb2">
    <svg width="300" height="140" viewBox="0 0 300 140" fill="none"><line x1="20" y1="70" x2="280" y2="70" stroke="#111" stroke-width="1.5" opacity=".25"/><line x1="20" y1="40" x2="100" y2="40" stroke="#111" stroke-width="1.2" opacity=".25"/><line x1="100" y1="40" x2="100" y2="100" stroke="#111" stroke-width="1.2" opacity=".25"/><line x1="100" y1="100" x2="200" y2="100" stroke="#111" stroke-width="1.2" opacity=".25"/><line x1="200" y1="100" x2="200" y2="50" stroke="#111" stroke-width="1.2" opacity=".25"/><line x1="200" y1="50" x2="280" y2="50" stroke="#111" stroke-width="1.2" opacity=".25"/><circle cx="60" cy="70" r="9" fill="none" stroke="#ff4d1c" stroke-width="1.5" opacity=".7"/><circle cx="150" cy="70" r="9" fill="none" stroke="#ff4d1c" stroke-width="1.5" opacity=".7"/><circle cx="240" cy="70" r="9" fill="none" stroke="#ff4d1c" stroke-width="1.5" opacity=".7"/><rect x="90" y="32" width="20" height="16" fill="none" stroke="#1a56ff" stroke-width="1" opacity=".6"/><text x="150" y="128" fill="#6b6b6b" font-size="9" text-anchor="middle" font-family="monospace" letter-spacing="2" opacity=".5">PLUMBING ISOMETRIC — MERIDIAN</text></svg>
  </div><div class="wm-caption"><div class="wm-caption-cat">MEP Engineering</div><div class="wm-caption-title">Meridian Tower</div></div></div>

  <div class="wm wm-c"><div class="wm-bg wb3">
    <svg width="100" height="100" viewBox="0 0 100 100" fill="none"><circle cx="50" cy="50" r="38" fill="#f5c800" opacity=".2"/><circle cx="50" cy="50" r="24" fill="none" stroke="#111" stroke-width="1.5" opacity=".4"/><text x="50" y="58" fill="#111" font-size="24" text-anchor="middle" font-family="Georgia,serif" font-style="italic" opacity=".7">V</text></svg>
  </div><div class="wm-caption"><div class="wm-caption-cat">Brand Identity</div><div class="wm-caption-title">Vance & Co.</div></div></div>

  <div class="wm wm-d"><div class="wm-bg wb4">
    <div style="display:flex;align-items:center;justify-content:center;gap:10px;width:100%;height:100%"><div class="bottle" style="height:100px;"></div><div class="bottle" style="height:80px;"></div><div class="bottle" style="height:90px;"></div></div>
  </div><div class="wm-caption"><div class="wm-caption-cat">Label Design</div><div class="wm-caption-title">Nocturne Wines</div></div></div>

  <div class="wm wm-e"><div class="wm-bg wb5">
    <svg width="160" height="120" viewBox="0 0 160 120" fill="none"><rect x="10" y="10" width="140" height="100" fill="none" stroke="#00c48c" stroke-width="1" opacity=".3"/><rect x="18" y="18" width="40" height="84" fill="rgba(0,196,140,.12)" stroke="#00c48c" stroke-width="1" opacity=".6"/><rect x="64" y="40" width="32" height="62" fill="rgba(0,196,140,.08)" stroke="#00c48c" stroke-width="1" opacity=".6"/><rect x="102" y="52" width="40" height="50" fill="rgba(0,196,140,.08)" stroke="#00c48c" stroke-width="1" opacity=".6"/><text x="80" y="116" fill="#00c48c" font-size="7" text-anchor="middle" font-family="monospace" letter-spacing="1" opacity=".7">HARLOW RESIDENCES</text></svg>
  </div><div class="wm-caption"><div class="wm-caption-cat">Construction Docs</div><div class="wm-caption-title">Harlow Residences</div></div></div>

  <div class="wm wm-f"><div class="wm-bg wb6">
    <svg width="120" height="100" viewBox="0 0 120 100" fill="none"><rect x="10" y="15" width="44" height="70" rx="3" fill="rgba(255,77,28,.1)" stroke="#ff4d1c" stroke-width="1.2" opacity=".7"/><rect x="63" y="15" width="47" height="32" rx="3" fill="rgba(255,77,28,.07)" stroke="#ff4d1c" stroke-width="1" opacity=".7"/><rect x="63" y="53" width="47" height="32" rx="3" fill="rgba(255,77,28,.07)" stroke="#ff4d1c" stroke-width="1" opacity=".7"/><text x="32" y="56" fill="#ff4d1c" font-size="20" text-anchor="middle" font-family="Georgia,serif" font-style="italic" opacity=".8">Kv</text></svg>
  </div><div class="wm-caption"><div class="wm-caption-cat">Packaging Design</div><div class="wm-caption-title">Kova Skincare</div></div></div>

  <div class="wm wm-g"><div class="wm-bg wb7">
    <svg width="120" height="100" viewBox="0 0 120 100" fill="none"><polygon points="60,10 110,80 10,80" fill="rgba(100,60,220,.1)" stroke="#6438cc" stroke-width="1.5" opacity=".7"/><polygon points="60,28 92,72 28,72" fill="rgba(100,60,220,.06)" stroke="#6438cc" stroke-width="0.8" opacity=".7"/><circle cx="60" cy="55" r="10" fill="rgba(100,60,220,.15)" stroke="#6438cc" stroke-width="0.8" opacity=".7"/><text x="60" y="94" fill="#6b6b6b" font-size="8" text-anchor="middle" font-family="monospace" letter-spacing="2" opacity=".6">APEX COLLECTIVE</text></svg>
  </div><div class="wm-caption"><div class="wm-caption-cat">Brand Identity</div><div class="wm-caption-title">Apex Collective</div></div></div>
</div>
```

  </section>

  <div class="services-split">
    <div class="svc-col reveal">
      <p class="svc-num">01</p>
      <h2 class="svc-col-title">Creative<br><em>Design</em></h2>
      <p>Visual work built to resonate — on shelves, in hands, and in memory.</p>
      <ul class="svc-list">
        <li>Packaging Design <span class="arrow">→</span></li>
        <li>Label Design <span class="arrow">→</span></li>
        <li>Brand Identity <span class="arrow">→</span></li>
        <li>Creative Direction <span class="arrow">→</span></li>
        <li>Art Direction <span class="arrow">→</span></li>
      </ul>
      <div class="svc-visual" style="background:linear-gradient(135deg,#fff7ed,#ffedd5)">
        <svg width="200" height="140" viewBox="0 0 200 140" fill="none"><rect x="40" y="10" width="50" height="120" rx="4" fill="rgba(255,77,28,.1)" stroke="#ff4d1c" stroke-width="1.2"/><rect x="50" y="22" width="30" height="36" rx="2" fill="rgba(255,77,28,.15)" stroke="#ff4d1c" stroke-width="0.8"/><rect x="100" y="30" width="60" height="80" rx="4" fill="rgba(255,77,28,.07)" stroke="#ff4d1c" stroke-width="1"/><circle cx="130" cy="90" r="20" fill="none" stroke="#ff4d1c" stroke-width="0.8"/><text x="65" y="47" fill="#ff4d1c" font-size="12" text-anchor="middle" font-family="Georgia,serif" font-style="italic">28</text></svg>
      </div>
    </div>
    <div class="svc-col reveal reveal-d2">
      <p class="svc-num">02</p>
      <h2 class="svc-col-title">Technical<br><em>Engineering</em></h2>
      <p>Construction documents, plumbing systems, and MEP coordination that get the job done right.</p>
      <ul class="svc-list">
        <li>Plumbing System Design <span class="arrow">→</span></li>
        <li>MEP Coordination <span class="arrow">→</span></li>
        <li>Construction Documents <span class="arrow">→</span></li>
        <li>Technical Drawings <span class="arrow">→</span></li>
        <li>Engineering Support <span class="arrow">→</span></li>
      </ul>
      <div class="svc-visual" style="background:linear-gradient(135deg,#eef6ff,#dbeafe)">
        <svg width="220" height="140" viewBox="0 0 220 140" fill="none"><line x1="20" y1="70" x2="200" y2="70" stroke="#1a56ff" stroke-width="1.5" opacity=".35"/><line x1="20" y1="40" x2="80" y2="40" stroke="#1a56ff" stroke-width="1.2" opacity=".35"/><line x1="80" y1="40" x2="80" y2="100" stroke="#1a56ff" stroke-width="1.2" opacity=".35"/><line x1="80" y1="100" x2="140" y2="100" stroke="#1a56ff" stroke-width="1.2" opacity=".35"/><line x1="140" y1="100" x2="140" y2="55" stroke="#1a56ff" stroke-width="1.2" opacity=".35"/><line x1="140" y1="55" x2="200" y2="55" stroke="#1a56ff" stroke-width="1.2" opacity=".35"/><circle cx="50" cy="70" r="8" fill="rgba(26,86,255,.15)" stroke="#1a56ff" stroke-width="1.5"/><circle cx="110" cy="70" r="8" fill="rgba(26,86,255,.15)" stroke="#1a56ff" stroke-width="1.5"/><circle cx="170" cy="70" r="8" fill="rgba(26,86,255,.15)" stroke="#1a56ff" stroke-width="1.5"/><rect x="72" y="32" width="16" height="16" fill="rgba(26,86,255,.1)" stroke="#1a56ff" stroke-width="1"/></svg>
      </div>
    </div>
  </div>

  <section class="cta-band reveal"><h2>Ready to build<br>something <em>great?</em></h2><div class="cta-band-right"><p>Tell us what you're working on. We respond within 24 hours.</p><a href="#" class="btn btn-punch btn-arrow" onclick="showPage('contact')">Start a conversation</a></div></section>

  <footer><div class="footer-top"><div class="footer-brand"><div class="footer-brand-name">Twenty<span class="num">8</span>Productions</div><p>A multidisciplinary studio at the intersection of creative brand design and technical construction engineering.</p></div><div class="footer-col"><h5>Services</h5><ul><li><a href="#" onclick="showPage('services')">Packaging Design</a></li><li><a href="#" onclick="showPage('services')">Label Design</a></li><li><a href="#" onclick="showPage('services')">Brand Identity</a></li><li><a href="#" onclick="showPage('services')">Plumbing Design</a></li><li><a href="#" onclick="showPage('services')">Construction Docs</a></li></ul></div><div class="footer-col"><h5>Studio</h5><ul><li><a href="#" onclick="showPage('about')">About</a></li><li><a href="#" onclick="showPage('portfolio')">Portfolio</a></li><li><a href="#" onclick="showPage('contact')">Contact</a></li></ul></div><div class="footer-col"><h5>Contact</h5><p style="margin-bottom:8px">hello@twenty8productions.com</p><p style="margin-bottom:8px">+1 (800) 280-0028</p><p>Los Angeles, CA</p></div></div><div class="footer-bottom"><p>© 2026 Twenty8Productions. All rights reserved.</p><div class="footer-legal"><a href="#">Privacy</a><a href="#">Terms</a></div></div></footer>
</div>

<!-- ═══════ SERVICES ═══════ -->

<div class="page" id="page-services">
  <section class="page-hero"><div class="page-hero-bg-num">02</div><div class="label" style="margin-bottom:20px;color:var(--punch1)">What We Offer</div><h1>Our <em style="color:var(--punch1)">Services</em></h1><p>Two disciplines. The same high standard. Whether it's a label or a load-bearing calculation — we don't cut corners.</p></section>

  <section class="services-page-section">
    <div class="reveal"><div class="label" style="color:var(--punch1);margin-bottom:32px">01 — Creative Design</div><h2 style="font-family:var(--font-display);font-size:clamp(36px,4vw,56px);letter-spacing:-0.02em;line-height:1.05">Brand &amp; <em style="font-style:italic;color:var(--punch1)">Creative Work</em></h2></div>
    <div class="sp-grid">
      <div class="sp-card reveal"><div class="sp-card-num">01</div><div class="sp-icon sp-icon-orange">📦</div><h3>Packaging Design</h3><p>Structural and surface packaging that earns its place on the shelf — designed for impact, feasibility, and brand alignment.</p><ul class="sp-features"><li>Structural packaging development</li><li>Graphic surface design</li><li>Dieline creation</li><li>Print-ready files</li><li>Material specification</li></ul></div>
      <div class="sp-card reveal reveal-d1"><div class="sp-card-num">02</div><div class="sp-icon sp-icon-orange">🏷</div><h3>Label Design</h3><p>Labels that tell a story. Designed for wine, spirits, beauty, food, and industrial applications — compliant and beautiful.</p><ul class="sp-features"><li>Custom illustration</li><li>Regulatory compliance</li><li>Foil & emboss specs</li><li>Multi-SKU label systems</li><li>Print vendor coordination</li></ul></div>
      <div class="sp-card reveal reveal-d2"><div class="sp-card-num">03</div><div class="sp-icon sp-icon-orange">◎</div><h3>Brand Identity</h3><p>Complete visual identity systems — logo, typography, color, and guidelines that keep it all cohesive at scale.</p><ul class="sp-features"><li>Logo & wordmark design</li><li>Visual identity systems</li><li>Brand guidelines</li><li>Stationery & collateral</li><li>Digital asset creation</li></ul></div>
    </div>
  </section>

  <section class="services-page-section alt">
    <div class="reveal"><div class="label" style="color:var(--punch2);margin-bottom:32px">02 — Technical Design</div><h2 style="font-family:var(--font-display);font-size:clamp(36px,4vw,56px);letter-spacing:-0.02em;line-height:1.05">Construction &amp; <em style="font-style:italic;color:var(--punch2)">Engineering</em></h2></div>
    <div class="sp-grid">
      <div class="sp-card reveal"><div class="sp-card-num">01</div><div class="sp-icon sp-icon-blue">🔧</div><h3>Plumbing Systems</h3><p>Full plumbing design — domestic water, sanitary drainage, storm water — for residential, commercial, and mixed-use projects.</p><ul class="sp-features"><li>Domestic water supply design</li><li>Sanitary & drainage systems</li><li>Storm water management</li><li>Fixture scheduling</li><li>Code compliance review</li></ul></div>
      <div class="sp-card reveal reveal-d1"><div class="sp-card-num">02</div><div class="sp-icon sp-icon-blue">📐</div><h3>Construction Documents</h3><p>Complete CD packages that communicate to contractors and pass permitting. Clear, organized, and built for the field.</p><ul class="sp-features"><li>Full CD-set production</li><li>Permit-ready drawings</li><li>Detail sections</li><li>Specification writing</li><li>RFI & submittal support</li></ul></div>
      <div class="sp-card reveal reveal-d2"><div class="sp-card-num">03</div><div class="sp-icon sp-icon-blue">⬡</div><h3>MEP Coordination</h3><p>Mechanical, electrical, and plumbing coordination that catches conflicts before they hit the job site.</p><ul class="sp-features"><li>BIM / 3D coordination</li><li>Clash detection & resolution</li><li>Architect collaboration</li><li>Structural interface design</li><li>Site visit support</li></ul></div>
    </div>
  </section>

  <section class="cta-band reveal"><h2>Have a project<br>in <em>mind?</em></h2><div class="cta-band-right"><p>Creative or technical — we want to hear about it.</p><a href="#" class="btn btn-punch btn-arrow" onclick="showPage('contact')">Request a quote</a></div></section>
  <footer><div class="footer-top"><div class="footer-brand"><div class="footer-brand-name">Twenty<span class="num">8</span>Productions</div><p>Creative brand design and technical construction engineering under one roof.</p></div><div class="footer-col"><h5>Navigate</h5><ul><li><a href="#" onclick="showPage('home')">Home</a></li><li><a href="#" onclick="showPage('portfolio')">Work</a></li><li><a href="#" onclick="showPage('about')">About</a></li><li><a href="#" onclick="showPage('contact')">Contact</a></li></ul></div><div class="footer-col"><h5>Contact</h5><p style="margin-bottom:8px">hello@twenty8productions.com</p><p>Los Angeles, CA</p></div><div class="footer-col"></div></div><div class="footer-bottom"><p>© 2026 Twenty8Productions.</p><div class="footer-legal"><a href="#">Privacy</a><a href="#">Terms</a></div></div></footer>
</div>

<!-- ═══════ PORTFOLIO ═══════ -->

<div class="page" id="page-portfolio">
  <section class="page-hero"><div class="page-hero-bg-num">03</div><div class="label" style="margin-bottom:20px;color:var(--punch1)">Selected Projects</div><h1>Our <em style="color:var(--punch1)">Work</em></h1><p>Brand design that lives on shelves. Construction documents that live in walls. All made with the same care.</p></section>

  <section class="portfolio-page">
    <div class="filter-row reveal">
      <button class="filt active" onclick="filterPF('all',this)">All Work</button>
      <button class="filt" onclick="filterPF('creative',this)">Creative Design</button>
      <button class="filt" onclick="filterPF('technical',this)">Technical / Engineering</button>
    </div>
    <div class="pf-grid reveal reveal-d1" id="pfGrid">
      <div class="pf-tile" data-cat="creative"><div class="pf-tile-bg ptb1"><svg width="90" height="200" viewBox="0 0 90 200" fill="none"><rect x="20" y="15" width="50" height="160" rx="6" fill="rgba(255,255,255,.06)" stroke="rgba(255,255,255,.2)" stroke-width="1.2"/><rect x="24" y="55" width="42" height="50" rx="2" fill="rgba(26,86,255,.2)" stroke="rgba(26,86,255,.5)" stroke-width="0.8"/><text x="45" y="84" fill="rgba(255,255,255,.6)" font-size="13" text-anchor="middle" font-family="Georgia,serif" font-style="italic">Elara</text><circle cx="45" cy="148" r="14" stroke="rgba(255,255,255,.1)" stroke-width="0.8"/></svg></div><div class="pf-tile-overlay"><div class="pf-tile-info"><p class="pf-tile-cat">Packaging Design</p><p class="pf-tile-name">Elara Spirits</p><p class="pf-tile-desc">Premium gin packaging system</p></div></div></div>

```
  <div class="pf-tile" data-cat="technical"><div class="pf-tile-bg ptb2"><svg width="280" height="180" viewBox="0 0 280 180" fill="none"><line x1="20" y1="90" x2="260" y2="90" stroke="#111" stroke-width="1.5" opacity=".25"/><line x1="20" y1="55" x2="100" y2="55" stroke="#111" stroke-width="1.2" opacity=".25"/><line x1="100" y1="55" x2="100" y2="125" stroke="#111" stroke-width="1.2" opacity=".25"/><line x1="100" y1="125" x2="180" y2="125" stroke="#111" stroke-width="1.2" opacity=".25"/><circle cx="60" cy="90" r="10" fill="none" stroke="#ff4d1c" stroke-width="1.5" opacity=".7"/><circle cx="140" cy="90" r="10" fill="none" stroke="#ff4d1c" stroke-width="1.5" opacity=".7"/><rect x="90" y="45" width="20" height="20" fill="none" stroke="#1a56ff" stroke-width="1" opacity=".6"/><text x="140" y="168" fill="#6b6b6b" font-size="8" text-anchor="middle" font-family="monospace" letter-spacing="2" opacity=".5">MERIDIAN — ISOMETRIC</text></svg></div><div class="pf-tile-overlay"><div class="pf-tile-info"><p class="pf-tile-cat">MEP Engineering</p><p class="pf-tile-name">Meridian Tower</p><p class="pf-tile-desc">38-floor commercial plumbing system</p></div></div></div>

  <div class="pf-tile" data-cat="creative"><div class="pf-tile-bg ptb3"><svg width="120" height="120" viewBox="0 0 120 120" fill="none"><circle cx="60" cy="60" r="44" fill="#f5c800" opacity=".2"/><circle cx="60" cy="60" r="28" fill="none" stroke="#111" stroke-width="1.5" opacity=".4"/><text x="60" y="69" fill="#111" font-size="30" text-anchor="middle" font-family="Georgia,serif" font-style="italic" opacity=".7">V</text></svg></div><div class="pf-tile-overlay"><div class="pf-tile-info"><p class="pf-tile-cat">Brand Identity</p><p class="pf-tile-name">Vance & Co.</p><p class="pf-tile-desc">Boutique law firm brand system</p></div></div></div>

  <div class="pf-tile" data-cat="technical"><div class="pf-tile-bg ptb5"><svg width="200" height="140" viewBox="0 0 200 140" fill="none"><rect x="15" y="15" width="170" height="110" fill="none" stroke="#00c48c" stroke-width="1" opacity=".3"/><rect x="22" y="22" width="50" height="96" fill="rgba(0,196,140,.12)" stroke="#00c48c" stroke-width="1" opacity=".6"/><rect x="78" y="44" width="40" height="74" fill="rgba(0,196,140,.08)" stroke="#00c48c" stroke-width="1" opacity=".6"/><rect x="124" y="58" width="52" height="60" fill="rgba(0,196,140,.08)" stroke="#00c48c" stroke-width="1" opacity=".6"/><text x="100" y="132" fill="#00c48c" font-size="7" text-anchor="middle" font-family="monospace" letter-spacing="1" opacity=".7">HARLOW RESIDENCES</text></svg></div><div class="pf-tile-overlay"><div class="pf-tile-info"><p class="pf-tile-cat">Construction Documents</p><p class="pf-tile-name">Harlow Residences</p><p class="pf-tile-desc">240-unit residential CD package</p></div></div></div>

  <div class="pf-tile" data-cat="creative"><div class="pf-tile-bg ptb4"><div style="display:flex;align-items:center;justify-content:center;gap:12px;width:100%;height:100%"><div class="bottle" style="height:110px;"></div><div class="bottle" style="height:90px;"></div><div class="bottle" style="height:100px;"></div></div></div><div class="pf-tile-overlay"><div class="pf-tile-info"><p class="pf-tile-cat">Label Design</p><p class="pf-tile-name">Nocturne Wines</p><p class="pf-tile-desc">6-varietal label collection</p></div></div></div>

  <div class="pf-tile" data-cat="technical"><div class="pf-tile-bg ptb7"><svg width="180" height="140" viewBox="0 0 180 140" fill="none"><line x1="20" y1="70" x2="160" y2="70" stroke="#6438cc" stroke-width="1.5" opacity=".3"/><line x1="20" y1="40" x2="70" y2="40" stroke="#6438cc" stroke-width="1.2" opacity=".3"/><line x1="70" y1="40" x2="70" y2="100" stroke="#6438cc" stroke-width="1.2" opacity=".3"/><line x1="70" y1="100" x2="130" y2="100" stroke="#6438cc" stroke-width="1.2" opacity=".3"/><circle cx="45" cy="70" r="9" fill="rgba(100,56,204,.15)" stroke="#6438cc" stroke-width="1.5" opacity=".7"/><circle cx="100" cy="70" r="9" fill="rgba(100,56,204,.15)" stroke="#6438cc" stroke-width="1.5" opacity=".7"/><rect x="62" y="30" width="16" height="20" fill="rgba(100,56,204,.1)" stroke="#6438cc" stroke-width="1" opacity=".6"/><text x="90" y="130" fill="#6438cc" font-size="7" text-anchor="middle" font-family="monospace" letter-spacing="1" opacity=".6">CIVIC CENTER COMPLEX</text></svg></div><div class="pf-tile-overlay"><div class="pf-tile-info"><p class="pf-tile-cat">MEP Coordination</p><p class="pf-tile-name">Civic Center Complex</p><p class="pf-tile-desc">Multi-building BIM coordination</p></div></div></div>

  <div class="pf-tile" data-cat="creative"><div class="pf-tile-bg ptb6"><svg width="130" height="110" viewBox="0 0 130 110" fill="none"><rect x="10" y="10" width="48" height="90" rx="4" fill="rgba(255,77,28,.1)" stroke="#ff4d1c" stroke-width="1.2" opacity=".7"/><rect x="70" y="10" width="52" height="42" rx="4" fill="rgba(255,77,28,.07)" stroke="#ff4d1c" stroke-width="1" opacity=".7"/><rect x="70" y="58" width="52" height="42" rx="4" fill="rgba(255,77,28,.07)" stroke="#ff4d1c" stroke-width="1" opacity=".7"/><text x="34" y="61" fill="#ff4d1c" font-size="24" text-anchor="middle" font-family="Georgia,serif" font-style="italic" opacity=".8">Kv</text></svg></div><div class="pf-tile-overlay"><div class="pf-tile-info"><p class="pf-tile-cat">Packaging Design</p><p class="pf-tile-name">Kova Skincare</p><p class="pf-tile-desc">Full product line packaging</p></div></div></div>

  <div class="pf-tile" data-cat="technical"><div class="pf-tile-bg ptb8"><svg width="180" height="140" viewBox="0 0 180 140" fill="none"><line x1="15" y1="70" x2="60" y2="70" stroke="#00c48c" stroke-width="1.5" opacity=".5"/><line x1="60" y1="70" x2="60" y2="35" stroke="#00c48c" stroke-width="1.5" opacity=".5"/><line x1="60" y1="35" x2="120" y2="35" stroke="#00c48c" stroke-width="1.5" opacity=".5"/><line x1="120" y1="35" x2="120" y2="100" stroke="#00c48c" stroke-width="1.5" opacity=".5"/><line x1="120" y1="100" x2="165" y2="100" stroke="#00c48c" stroke-width="1.5" opacity=".5"/><circle cx="38" cy="70" r="9" fill="rgba(0,196,140,.15)" stroke="#00c48c" stroke-width="1.5" opacity=".7"/><circle cx="90" cy="35" r="9" fill="rgba(0,196,140,.15)" stroke="#00c48c" stroke-width="1.5" opacity=".7"/><circle cx="143" cy="100" r="9" fill="rgba(0,196,140,.15)" stroke="#00c48c" stroke-width="1.5" opacity=".7"/><text x="90" y="130" fill="#00c48c" font-size="7" text-anchor="middle" font-family="monospace" letter-spacing="1" opacity=".7">EASTSIDE MEDICAL CENTER</text></svg></div><div class="pf-tile-overlay"><div class="pf-tile-info"><p class="pf-tile-cat">Plumbing Design</p><p class="pf-tile-name">Eastside Medical Center</p><p class="pf-tile-desc">Healthcare-grade systems</p></div></div></div>

  <div class="pf-tile" data-cat="creative"><div class="pf-tile-bg ptb9"><svg width="120" height="120" viewBox="0 0 120 120" fill="none"><polygon points="60,10 110,90 10,90" fill="rgba(245,200,0,.15)" stroke="#f5c800" stroke-width="1.5" opacity=".7"/><polygon points="60,26 92,80 28,80" fill="rgba(245,200,0,.08)" stroke="#f5c800" stroke-width="0.8" opacity=".7"/><circle cx="60" cy="62" r="10" fill="rgba(245,200,0,.2)" stroke="#f5c800" stroke-width="0.8" opacity=".7"/><text x="60" y="110" fill="#6b6b6b" font-size="8" text-anchor="middle" font-family="monospace" letter-spacing="2" opacity=".6">APEX COLLECTIVE</text></svg></div><div class="pf-tile-overlay"><div class="pf-tile-info"><p class="pf-tile-cat">Brand Identity</p><p class="pf-tile-name">Apex Collective</p><p class="pf-tile-desc">Creative agency visual identity</p></div></div></div>
</div>
```

  </section>

  <section class="cta-band reveal"><h2>Your project<br>could be <em>next.</em></h2><div class="cta-band-right"><p>We take on select projects. Tell us what you're building.</p><a href="#" class="btn btn-punch btn-arrow" onclick="showPage('contact')">Get in touch</a></div></section>
  <footer><div class="footer-top"><div class="footer-brand"><div class="footer-brand-name">Twenty<span class="num">8</span>Productions</div><p>Creative brand design and technical construction engineering.</p></div><div class="footer-col"><h5>Navigate</h5><ul><li><a href="#" onclick="showPage('home')">Home</a></li><li><a href="#" onclick="showPage('services')">Services</a></li><li><a href="#" onclick="showPage('about')">About</a></li><li><a href="#" onclick="showPage('contact')">Contact</a></li></ul></div><div class="footer-col"><h5>Contact</h5><p style="margin-bottom:8px">hello@twenty8productions.com</p><p>Los Angeles, CA</p></div><div class="footer-col"></div></div><div class="footer-bottom"><p>© 2026 Twenty8Productions.</p><div class="footer-legal"><a href="#">Privacy</a><a href="#">Terms</a></div></div></footer>
</div>

<!-- ═══════ ABOUT ═══════ -->

<div class="page" id="page-about">
  <section class="page-hero"><div class="page-hero-bg-num">04</div><div class="label" style="margin-bottom:20px;color:var(--punch1)">Our Studio</div><h1>Built for<br><em style="color:var(--punch1)">both.</em></h1><p>We didn't set out to build two separate studios. We set out to build one exceptional one that does something nobody else was doing.</p></section>

  <section class="about-intro">
    <div class="reveal"><div class="label" style="margin-bottom:20px">Who We Are</div><h2>Engineering meets <em>creative vision.</em></h2><a href="#" class="btn btn-dark btn-arrow" style="margin-top:32px" onclick="showPage('contact')">Work with us</a></div>
    <div class="reveal reveal-d2"><p>Twenty8Productions was founded on a single conviction: the highest standard of design thinking should apply equally to a product label and a plumbing isometric. The disciplines are different. The commitment is identical.</p><p>Our studio brings together graphic designers, brand strategists, licensed engineers, and CAD drafters — all under one roof, sharing the same values, holding every deliverable to the same demanding standard.</p><p>Over twelve years, we've built a reputation for work that doesn't just look right or function correctly. It excels at both.</p></div>
  </section>

  <div class="stats-row">
    <div class="stat-cell reveal"><span class="stat-big">12<span>+</span></span><span class="stat-label">Years in Business</span></div>
    <div class="stat-cell reveal reveal-d1"><span class="stat-big">200<span>+</span></span><span class="stat-label">Projects Completed</span></div>
    <div class="stat-cell reveal reveal-d2"><span class="stat-big">48<span>+</span></span><span class="stat-label">Brand Identities</span></div>
    <div class="stat-cell reveal reveal-d3"><span class="stat-big">30<span>M+</span></span><span class="stat-label">Sq. Ft. Engineered</span></div>
  </div>

  <section class="values-section">
    <div class="label reveal" style="margin-bottom:20px">What We Stand For</div>
    <h2 class="reveal reveal-d1" style="font-family:var(--font-display);font-size:clamp(36px,4.5vw,56px);letter-spacing:-0.02em">The principles <em style="font-style:italic;color:var(--punch1)">we live by.</em></h2>
    <div class="values-grid">
      <div class="val-card reveal"><span class="val-emoji">⬟</span><h4>Precision</h4><p>Every millimeter in a CAD file and every pixel in a design matters. We get it right the first time.</p></div>
      <div class="val-card reveal reveal-d1"><span class="val-emoji">◎</span><h4>Craft</h4><p>We take pride in the quality of our work — because a half-measure isn't in our vocabulary.</p></div>
      <div class="val-card reveal reveal-d2"><span class="val-emoji">◈</span><h4>Integrity</h4><p>We tell clients the truth, deliver what we promise, and flag problems early. Trust is our most valuable asset.</p></div>
      <div class="val-card reveal reveal-d3"><span class="val-emoji">△</span><h4>Elevation</h4><p>Our goal is not to meet the brief — it's to exceed what the brief imagined was possible.</p></div>
    </div>
  </section>

  <section class="disciplines-section">
    <div class="disc-card creative reveal"><div class="label" style="color:var(--punch1);margin-bottom:20px">Creative Studio</div><h3>Brand & <em style="font-style:italic;color:var(--punch1)">Design</em></h3><p>Senior brand designers, packaging specialists, illustrators, and print production experts working across food & beverage, beauty, spirits, and consumer goods.</p><p style="margin-top:16px">We design for real-world application: shelf presence, production feasibility, and brand consistency at scale.</p></div>
    <div class="disc-card technical reveal reveal-d2"><div class="label" style="color:var(--punch2);margin-bottom:20px">Engineering Division</div><h3>Technical & <em style="font-style:italic;color:var(--punch2)">Construction</em></h3><p>Licensed engineers, CAD specialists, and construction document coordinators with experience from single-family homes to large-scale civic developments.</p><p style="margin-top:16px">We bring a designer's eye to technical documentation — clear, organized, and built to communicate efficiently with every construction team member.</p></div>
  </section>

  <section class="cta-band reveal"><h2>Let's build<br>something <em>together.</em></h2><div class="cta-band-right"><p>Tell us about your project — creative, technical, or both.</p><a href="#" class="btn btn-punch btn-arrow" onclick="showPage('contact')">Work with us</a></div></section>
  <footer><div class="footer-top"><div class="footer-brand"><div class="footer-brand-name">Twenty<span class="num">8</span>Productions</div><p>Creative brand design and technical construction engineering under one roof.</p></div><div class="footer-col"><h5>Navigate</h5><ul><li><a href="#" onclick="showPage('home')">Home</a></li><li><a href="#" onclick="showPage('services')">Services</a></li><li><a href="#" onclick="showPage('portfolio')">Work</a></li><li><a href="#" onclick="showPage('contact')">Contact</a></li></ul></div><div class="footer-col"><h5>Contact</h5><p style="margin-bottom:8px">hello@twenty8productions.com</p><p>Los Angeles, CA</p></div><div class="footer-col"></div></div><div class="footer-bottom"><p>© 2026 Twenty8Productions.</p><div class="footer-legal"><a href="#">Privacy</a><a href="#">Terms</a></div></div></footer>
</div>

<!-- ═══════ CONTACT ═══════ -->

<div class="page" id="page-contact">
  <section class="page-hero"><div class="page-hero-bg-num">05</div><div class="label" style="margin-bottom:20px;color:var(--punch1)">Get in Touch</div><h1>Let's start<br>a <em style="color:var(--punch1)">conversation.</em></h1><p>A label. A plumbing isometric. A full rebrand. Whatever it is — we'd love to hear about it.</p></section>

  <div class="contact-grid">
    <div class="contact-info-panel reveal">
      <div class="label" style="margin-bottom:20px">Contact Info</div>
      <h2>We'd love<br>to hear about<br>your <em>project.</em></h2>
      <p>Reach out with a quick description of what you're working on and we'll follow up within 24 hours.</p>
      <div class="contact-detail"><div class="cd-dot">✉</div><div class="cd-text"><label>Email</label><p>hello@twenty8productions.com</p></div></div>
      <div class="contact-detail"><div class="cd-dot">📞</div><div class="cd-text"><label>Phone</label><p>+1 (800) 280-0028</p></div></div>
      <div class="contact-detail"><div class="cd-dot">📍</div><div class="cd-text"><label>Location</label><p>Los Angeles, California</p></div></div>
      <div class="contact-detail"><div class="cd-dot">🕐</div><div class="cd-text"><label>Hours</label><p>Mon – Fri, 9AM – 6PM PST</p></div></div>
    </div>
    <div class="contact-form-panel reveal reveal-d2">
      <p class="form-title">Send a message</p>
      <div class="form-row"><div class="form-group"><label>First Name</label><input type="text" placeholder="John"></div><div class="form-group"><label>Last Name</label><input type="text" placeholder="Smith"></div></div>
      <div class="form-group"><label>Email</label><input type="email" placeholder="john@company.com"></div>
      <div class="form-group"><label>Company</label><input type="text" placeholder="Your company name"></div>
      <div class="form-group"><label>Service Needed</label><select><option value="">Select a service...</option><optgroup label="Creative Design"><option>Packaging Design</option><option>Label Design</option><option>Brand Identity</option></optgroup><optgroup label="Technical / Engineering"><option>Plumbing System Design</option><option>Construction Documents</option><option>MEP Coordination</option></optgroup><option>Multiple Services</option><option>Not sure — let's talk</option></select></div>
      <div class="form-group"><label>Budget Range</label><select><option value="">Select range...</option><option>Under $5,000</option><option>$5,000 – $15,000</option><option>$15,000 – $50,000</option><option>$50,000 – $150,000</option><option>$150,000+</option></select></div>
      <div class="form-group"><label>Tell Us About Your Project</label><textarea placeholder="Brief description, timeline, any specific requirements..."></textarea></div>
      <button class="form-submit" onclick="handleSubmit(this)">Send Message →</button>
    </div>
  </div>

  <footer><div class="footer-top"><div class="footer-brand"><div class="footer-brand-name">Twenty<span class="num">8</span>Productions</div><p>Creative brand design and technical construction engineering under one roof.</p></div><div class="footer-col"><h5>Navigate</h5><ul><li><a href="#" onclick="showPage('home')">Home</a></li><li><a href="#" onclick="showPage('services')">Services</a></li><li><a href="#" onclick="showPage('portfolio')">Work</a></li><li><a href="#" onclick="showPage('about')">About</a></li></ul></div><div class="footer-col"><h5>Contact</h5><p style="margin-bottom:8px">hello@twenty8productions.com</p><p style="margin-bottom:8px">+1 (800) 280-0028</p><p>Los Angeles, CA</p></div><div class="footer-col"></div></div><div class="footer-bottom"><p>© 2026 Twenty8Productions.</p><div class="footer-legal"><a href="#">Privacy</a><a href="#">Terms</a></div></div></footer>
</div>

<script>
const cursor=document.getElementById('cursor'),ring=document.getElementById('cursorRing');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;cursor.style.left=mx+'px';cursor.style.top=my+'px';});
(function animRing(){rx+=(mx-rx)*.12;ry+=(my-ry)*.12;ring.style.left=rx+'px';ring.style.top=ry+'px';requestAnimationFrame(animRing);})();
function showPage(id){document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));document.getElementById('page-'+id).classList.add('active');window.scrollTo({top:0,behavior:'instant'});setTimeout(initReveal,80);}
document.getElementById('hamburger').addEventListener('click',()=>document.getElementById('mobileNav').classList.add('open'));
document.getElementById('mobileClose').addEventListener('click',closeMobileNav);
function closeMobileNav(){document.getElementById('mobileNav').classList.remove('open');}
function initReveal(){const els=document.querySelectorAll('.page.active .reveal');const obs=new IntersectionObserver(entries=>{entries.forEach(e=>{if(e.isIntersecting)e.target.classList.add('visible');});},{threshold:.08,rootMargin:'0px 0px -32px 0px'});els.forEach(el=>{el.classList.remove('visible');obs.observe(el);});}
window.addEventListener('load',()=>setTimeout(initReveal,100));
function filterPF(cat,btn){document.querySelectorAll('.filt').forEach(b=>b.classList.remove('active'));btn.classList.add('active');document.querySelectorAll('.pf-tile').forEach(tile=>{const show=cat==='all'||tile.dataset.cat===cat;tile.style.display=show?'':'none';if(show){tile.style.opacity='0';tile.style.transform='translateY(12px)';setTimeout(()=>{tile.style.transition='opacity .4s,transform .4s';tile.style.opacity='1';tile.style.transform='none';},40);}});}
function handleSubmit(btn){btn.textContent='Message Sent ✓';btn.style.background='var(--punch3)';setTimeout(()=>{btn.textContent='Send Message →';btn.style.background='';},4000);}
document.querySelectorAll('a[href="#"]').forEach(a=>a.addEventListener('click',e=>e.preventDefault()));
</script>

</body>
</html>
