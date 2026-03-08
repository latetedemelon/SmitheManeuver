<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Smith Maneuver — Complete Visual Guide</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/mermaid/10.6.1/mermaid.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=IBM+Plex+Mono:wght@400;600&family=IBM+Plex+Sans:wght@300;400;500&display=swap" rel="stylesheet">

<style>
/* ═══════════════════════════════════════════════════
   DESIGN TOKENS — Newspaper Editorial
═══════════════════════════════════════════════════ */
:root {
  --ink:        #0e1117;
  --ink-mid:    #1c2430;
  --paper:      #f5f0e8;
  --cream:      #ede8da;
  --cream-dark: #e0dace;
  --gold:       #c9a84c;
  --gold-light: #e8c96a;
  --gold-pale:  #f5e9c4;
  --teal:       #1a6b5e;
  --teal-light: #2a9d8f;
  --rust:       #c94c1a;
  --rust-light: #e05a20;
  --slate:      #2c3e50;
  --muted:      #7a7060;
  --muted-light:#9a9080;
  --rule:       #c4bba8;
  --rule-light: #d8d0c0;

  /* chart palette that reads well on cream */
  --chart-pos:  #1a6b5e;
  --chart-neg:  #c94c1a;
  --chart-gold: #c9a84c;
  --chart-slate:#556070;
  --chart-mid:  #4a8a7e;
}

/* ═══════════════════════════════════════════════════
   RESET & BASE
═══════════════════════════════════════════════════ */
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

html { scroll-behavior: smooth; }

body {
  background: var(--paper);
  color: var(--ink);
  font-family: 'IBM Plex Sans', sans-serif;
  font-weight: 300;
  line-height: 1.65;
  font-size: 15px;
}

img { max-width: 100%; }

/* ═══════════════════════════════════════════════════
   NAV BAR
═══════════════════════════════════════════════════ */
.nav {
  background: var(--ink);
  border-bottom: 3px solid var(--gold);
  position: sticky;
  top: 0;
  z-index: 100;
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
}
.nav-inner {
  display: flex;
  align-items: center;
  gap: 0;
  padding: 0 20px;
  white-space: nowrap;
  min-width: min-content;
}
.nav-brand {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--gold);
  padding: 14px 20px 14px 0;
  border-right: 1px solid #2a2a2a;
  margin-right: 4px;
  flex-shrink: 0;
}
.nav a {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #7a6a50;
  text-decoration: none;
  padding: 14px 14px;
  display: block;
  transition: color 0.2s;
  flex-shrink: 0;
}
.nav a:hover { color: var(--gold); }

/* ═══════════════════════════════════════════════════
   MASTHEAD
═══════════════════════════════════════════════════ */
.masthead {
  background: var(--ink);
  color: var(--paper);
  padding: clamp(36px, 7vw, 72px) clamp(20px, 6vw, 80px) clamp(32px, 6vw, 60px);
  border-bottom: 4px solid var(--gold);
  position: relative;
  overflow: hidden;
}
.masthead::before {
  content: '';
  position: absolute;
  top: 0; right: 0;
  width: min(400px, 60vw); height: 100%;
  background: repeating-linear-gradient(
    45deg, transparent, transparent 18px,
    rgba(201,168,76,0.05) 18px, rgba(201,168,76,0.05) 19px
  );
  pointer-events: none;
}
.masthead-eyebrow {
  font-family: 'IBM Plex Mono', monospace;
  font-size: clamp(9px, 1.8vw, 11px);
  letter-spacing: 4px;
  text-transform: uppercase;
  color: var(--gold);
  margin-bottom: 16px;
}
.masthead h1 {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2rem, 7vw, 4.2rem);
  font-weight: 900;
  line-height: 1.05;
  letter-spacing: -0.02em;
  color: var(--paper);
  max-width: 780px;
}
.masthead h1 em { color: var(--gold); font-style: italic; }
.masthead-sub {
  margin-top: 18px;
  font-size: clamp(13px, 2.2vw, 15px);
  color: #a09880;
  max-width: 580px;
  line-height: 1.75;
}
.masthead-meta {
  display: flex;
  flex-wrap: wrap;
  gap: clamp(16px, 4vw, 40px);
  margin-top: 32px;
  padding-top: 24px;
  border-top: 1px solid #2a2a2a;
}
.meta-item { display: flex; flex-direction: column; gap: 4px; }
.meta-label {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: #4a4030;
}
.meta-value { font-size: 12px; color: #c4bba8; font-weight: 400; }

/* ═══════════════════════════════════════════════════
   STAT STRIP
═══════════════════════════════════════════════════ */
.stat-strip {
  background: var(--ink-mid);
  border-bottom: 1px solid #2a3545;
  padding: clamp(16px, 3vw, 24px) clamp(20px, 6vw, 60px);
  display: flex;
  flex-wrap: wrap;
  gap: clamp(20px, 5vw, 56px);
}
.stat-item { display: flex; flex-direction: column; gap: 4px; min-width: 80px; }
.stat-val {
  font-family: 'Playfair Display', serif;
  font-size: clamp(1.5rem, 4vw, 2.4rem);
  font-weight: 700;
  line-height: 1;
  color: var(--gold);
}
.stat-val.green { color: #2a9d8f; }
.stat-val.red   { color: var(--rust); }
.stat-val.blue  { color: #5a9aca; }
.stat-label {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #5a5040;
}

/* ═══════════════════════════════════════════════════
   PAGE BODY
═══════════════════════════════════════════════════ */
.page-body {
  max-width: 1100px;
  margin: 0 auto;
  padding: clamp(32px, 6vw, 64px) clamp(16px, 5vw, 48px) clamp(60px, 8vw, 100px);
}

/* ═══════════════════════════════════════════════════
   TABLE OF CONTENTS
═══════════════════════════════════════════════════ */
.toc {
  background: var(--ink);
  color: var(--paper);
  padding: clamp(20px, 4vw, 36px) clamp(20px, 5vw, 40px);
  margin-bottom: clamp(40px, 6vw, 64px);
}
.toc-heading {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: var(--gold);
  margin-bottom: 16px;
  display: block;
}
.toc-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 0;
}
.toc-item {
  display: flex;
  align-items: baseline;
  gap: 10px;
  padding: 7px 0;
  border-bottom: 1px dashed #2a2a2a;
  text-decoration: none;
}
.toc-item:hover .toc-text { color: var(--gold); }
.toc-num {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  color: var(--gold);
  flex-shrink: 0;
  min-width: 24px;
}
.toc-text { font-size: 12px; color: #c4bba8; font-weight: 300; transition: color 0.15s; }

/* ═══════════════════════════════════════════════════
   SECTION HEADERS
═══════════════════════════════════════════════════ */
.section-head {
  display: flex;
  align-items: center;
  gap: 16px;
  margin: clamp(48px, 7vw, 80px) 0 10px;
}
.section-head::before {
  content: '';
  flex: 0 0 36px;
  height: 2px;
  background: var(--gold);
}
.section-tag {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: 3px;
  color: var(--gold);
  text-transform: uppercase;
}
.section-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(1.4rem, 4vw, 2rem);
  font-weight: 700;
  color: var(--ink);
  margin-top: 6px;
  margin-bottom: 8px;
}
.section-desc {
  font-size: clamp(13px, 2vw, 14px);
  color: var(--muted);
  margin-bottom: 28px;
  max-width: 700px;
  line-height: 1.8;
}

/* ═══════════════════════════════════════════════════
   DIAGRAM CARDS (Mermaid)
═══════════════════════════════════════════════════ */
.diagram-card {
  background: white;
  border: 1px solid var(--rule);
  border-top: 3px solid var(--teal);
  margin-bottom: 28px;
  padding: clamp(20px, 4vw, 40px) clamp(16px, 4vw, 40px);
  box-shadow: 0 2px 12px rgba(0,0,0,0.06);
}
.diagram-card.gold-top   { border-top-color: var(--gold); }
.diagram-card.rust-top   { border-top-color: var(--rust); }

.card-eyebrow {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--teal);
  margin-bottom: 5px;
}
.diagram-card.gold-top .card-eyebrow { color: var(--gold); }
.diagram-card.rust-top .card-eyebrow { color: var(--rust); }

.card-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(1rem, 3vw, 1.3rem);
  font-weight: 700;
  color: var(--ink);
  margin-bottom: 6px;
}
.card-note {
  font-size: 13px;
  color: var(--muted);
  margin-bottom: 20px;
  padding-bottom: 18px;
  border-bottom: 1px solid var(--cream);
  line-height: 1.65;
}

.diagram-scroll {
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
  padding: 8px 0 4px;
}
.diagram-scroll .mermaid {
  display: flex;
  justify-content: center;
  min-width: 480px;
}
/* Scroll hint on mobile */
@media (max-width: 600px) {
  .diagram-scroll::after {
    content: '← scroll →';
    display: block;
    text-align: center;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    letter-spacing: 2px;
    color: var(--rule);
    margin-top: 8px;
  }
}

/* ═══════════════════════════════════════════════════
   CALLOUT BOXES
═══════════════════════════════════════════════════ */
.callout {
  background: var(--cream);
  border-left: 4px solid var(--teal);
  padding: clamp(14px, 3vw, 18px) clamp(14px, 3vw, 24px);
  margin-top: 20px;
  font-size: 13px;
  line-height: 1.75;
  color: var(--slate);
}
.callout.warn { border-left-color: var(--rust); background: #fdf0ec; }
.callout.gold  { border-left-color: var(--gold); background: var(--gold-pale); }
.callout strong { font-weight: 600; color: var(--ink); }

/* ═══════════════════════════════════════════════════
   CHART CARDS
═══════════════════════════════════════════════════ */
.chart-card {
  background: white;
  border: 1px solid var(--rule);
  border-top: 3px solid var(--teal);
  padding: clamp(18px, 4vw, 32px) clamp(16px, 4vw, 32px);
  margin-bottom: 24px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
}
.chart-card.gold-top { border-top-color: var(--gold); }
.chart-card.rust-top { border-top-color: var(--rust); }

.chart-label {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  letter-spacing: 2.5px;
  text-transform: uppercase;
  color: var(--muted-light);
  margin-bottom: 4px;
}
.chart-card h3 {
  font-family: 'Playfair Display', serif;
  font-size: clamp(1rem, 3vw, 1.2rem);
  font-weight: 700;
  color: var(--ink);
  margin-bottom: 8px;
}
.chart-note {
  font-size: 12.5px;
  color: var(--muted);
  margin-bottom: 20px;
  padding-bottom: 16px;
  border-bottom: 1px solid var(--cream);
  line-height: 1.65;
}
.chart-wrap { position: relative; width: 100%; }
.chart-wrap.tall   { height: clamp(260px, 40vw, 400px); }
.chart-wrap.medium { height: clamp(220px, 35vw, 320px); }

/* ═══════════════════════════════════════════════════
   TWO-COLUMN GRID
═══════════════════════════════════════════════════ */
.two-col {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}
@media (max-width: 700px) {
  .two-col { grid-template-columns: 1fr; }
}

/* ═══════════════════════════════════════════════════
   TOGGLE BUTTONS
═══════════════════════════════════════════════════ */
.toggle-row {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 20px;
}
.toggle-btn {
  padding: 8px 16px;
  border: 1px solid var(--rule);
  background: var(--cream);
  color: var(--muted);
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  cursor: pointer;
  transition: all 0.2s;
  -webkit-tap-highlight-color: transparent;
}
.toggle-btn.active {
  background: var(--ink);
  border-color: var(--ink);
  color: var(--gold);
}
.toggle-btn:hover:not(.active) {
  border-color: var(--gold);
  color: var(--ink);
}

/* ═══════════════════════════════════════════════════
   TABLES
═══════════════════════════════════════════════════ */
.table-scroll { overflow-x: auto; -webkit-overflow-scrolling: touch; }

.year-table { width: 100%; border-collapse: collapse; font-size: 12.5px; min-width: 480px; }
.year-table th {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--muted);
  padding: 10px 12px;
  text-align: left;
  border-bottom: 2px solid var(--cream-dark);
  background: var(--cream);
  position: sticky;
  top: 0;
}
.year-table td {
  padding: 9px 12px;
  border-bottom: 1px solid var(--cream);
  vertical-align: middle;
}
.year-table tr:last-child td { border-bottom: none; }
.year-table tr:hover td { background: var(--cream); }

.sim-table { width: 100%; border-collapse: collapse; font-size: 11.5px; min-width: 600px; }
.sim-table th {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 8.5px;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--muted);
  padding: 10px 10px;
  text-align: right;
  border-bottom: 2px solid var(--cream-dark);
  background: var(--cream);
  white-space: nowrap;
}
.sim-table th:first-child { text-align: left; }
.sim-table td {
  padding: 8px 10px;
  border-bottom: 1px solid var(--cream);
  text-align: right;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
}
.sim-table td:first-child {
  text-align: left;
  font-family: 'IBM Plex Sans', sans-serif;
  font-weight: 400;
  color: var(--ink);
}
.sim-table tr:last-child td {
  border-top: 2px solid var(--gold);
  font-weight: 600;
  color: var(--teal);
  background: var(--gold-pale);
  border-bottom: none;
}
.sim-table tr.crash td { background: #fff5f2; }
.sim-table tr.bull  td { background: #f2faf8; }
.sim-table tr:hover td { opacity: 0.9; }

/* pills */
.return-pill {
  display: inline-block;
  padding: 2px 8px;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 600;
  min-width: 62px;
  text-align: center;
  border-radius: 2px;
}
.pill-up   { background: rgba(26,107,94,0.1); color: var(--teal); border: 1px solid rgba(26,107,94,0.2); }
.pill-down { background: rgba(201,76,26,0.1); color: var(--rust); border: 1px solid rgba(201,76,26,0.2); }

.pos     { color: var(--teal); }
.neg     { color: var(--rust); }
.neutral { color: #8a6a10; }

.mini-bar { height: 7px; border-radius: 1px; display: inline-block; vertical-align: middle; }

/* ═══════════════════════════════════════════════════
   PAGE FOOTER
═══════════════════════════════════════════════════ */
.page-footer {
  background: var(--ink);
  border-top: 3px solid var(--gold);
  color: #5a4a30;
  padding: clamp(20px, 4vw, 32px) clamp(20px, 5vw, 60px);
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: 1px;
}
.footer-warn { color: var(--rust); opacity: 0.7; }

/* ═══════════════════════════════════════════════════
   HORIZONTAL RULE
═══════════════════════════════════════════════════ */
.chapter-rule {
  display: flex;
  align-items: center;
  gap: 16px;
  margin: clamp(48px, 7vw, 72px) 0 clamp(24px, 4vw, 40px);
}
.chapter-rule::before, .chapter-rule::after {
  content: '';
  flex: 1;
  height: 1px;
  background: var(--rule);
}
.chapter-rule-label {
  font-family: 'Playfair Display', serif;
  font-size: clamp(0.85rem, 2.5vw, 1rem);
  font-style: italic;
  color: var(--muted);
  white-space: nowrap;
  padding: 0 8px;
}

/* ── ADDITIONS FOR ETF / PORTFOLIO SECTIONS ── */
.chapter-rule-full {
  border-top: 3px solid var(--ink);
  border-bottom: 1px solid var(--ink);
  padding: 10px 0 8px;
  margin: clamp(48px,7vw,80px) 0 28px;
}
.chapter-rule-full .crl {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: var(--gold);
}
.dark-box {
  background: var(--ink); color: #ddd;
  padding: 18px 22px; margin-bottom: 22px;
  border-left: 4px solid var(--gold);
  font-size: 12.5px; line-height: 1.8;
}
.dark-box strong { color: var(--gold-light); }
.dark-box ul { padding-left: 18px; margin-top: 8px; }
.dark-box li { margin-bottom: 5px; }
.alert-box {
  background: #2a0a00; color: #f0c090;
  padding: 14px 18px; margin-bottom: 18px;
  border-left: 4px solid var(--rust);
  font-size: 12.5px; line-height: 1.75;
}
.alert-box strong { color: #ffb070; }
.fact-note {
  background: #0a1a0a; color: #a0c8a0;
  padding: 14px 18px; margin-bottom: 18px;
  border-left: 4px solid #2a9d8f;
  font-size: 12px; line-height: 1.8;
}
.fact-note strong { color: #7fba6a; }
.main-tbl { width:100%; border-collapse:collapse; font-size:11.5px; min-width:620px; }
.main-tbl thead th {
  background: var(--ink); color: var(--gold-light);
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px; letter-spacing: 1.5px; text-transform: uppercase;
  padding: 8px 10px; text-align: left; white-space: nowrap;
}
.main-tbl tbody td { padding: 8px 10px; border-bottom: 1px solid #ddd; vertical-align: middle; }
.main-tbl tbody tr:nth-child(even) td { background: #f0ebe0; }
.main-tbl tbody tr:hover td { background: #e6e0ce !important; }
.main-tbl tbody tr.win td { background: #e8f2e8 !important; border-left: 4px solid #1a4a2e; }
.main-tbl tbody tr.caution td { border-left: 4px solid var(--rust); }
.tick { font-family:'IBM Plex Mono',monospace; font-weight:700; font-size:12.5px; display:block; }
.tick-sub { font-family:'IBM Plex Mono',monospace; font-size:8.5px; color:var(--muted); display:block; }
td.g { color:#1a4a2e; font-family:'IBM Plex Mono',monospace; font-weight:600; }
td.a { color:#7a5500; font-family:'IBM Plex Mono',monospace; font-weight:600; }
td.r { color:#8b2500; font-family:'IBM Plex Mono',monospace; font-weight:600; }
td.mn { font-family:'IBM Plex Mono',monospace; font-weight:600; }
.b { display:inline-block; font-family:'IBM Plex Mono',monospace; font-size:8px;
  letter-spacing:.5px; text-transform:uppercase; padding:2px 5px; border-radius:2px;
  font-weight:700; white-space:nowrap; margin:1px 1px 0 0; }
.b-win{background:#1a4a2e;color:#fff;} .b-ok{background:#556b2f;color:#fff;}
.b-lv{background:#1a4a2e;color:#fff;} .b-q{background:#0f2a4a;color:#fff;}
.b-dg{background:#c9a84c;color:#0e1117;} .b-hd{background:#c04000;color:#fff;}
.b-warn{background:var(--rust);color:#fff;}
.port-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(205px,1fr)); gap:14px; margin-bottom:22px; }
.pcrd { background:white; border:1.5px solid #d4ccb8; box-shadow:3px 3px 0 #d4ccb8; padding:16px 18px; position:relative; overflow:hidden; }
.pcrd::before { content:''; position:absolute; top:0; left:0; width:100%; height:4px; }
.pcrd.ca::before{background:#c04000;} .pcrd.us::before{background:#0f2a4a;}
.pcrd.eafe::before{background:#1a4a2e;} .pcrd.em::before{background:#c9a84c;}
.pcrd-ticker{font-family:'Playfair Display',serif;font-size:26px;font-weight:900;line-height:1;margin-bottom:3px;}
.pcrd-sub{font-family:'IBM Plex Mono',monospace;font-size:8.5px;color:var(--muted);letter-spacing:1px;text-transform:uppercase;margin-bottom:10px;}
.pcrd-wt{font-family:'IBM Plex Mono',monospace;font-size:20px;font-weight:700;color:var(--gold);margin-bottom:8px;}
.pcrd-stats{display:grid;grid-template-columns:1fr 1fr;gap:5px;}
.pstat{display:flex;flex-direction:column;}
.pstat .lbl{font-family:'IBM Plex Mono',monospace;font-size:8px;letter-spacing:1px;text-transform:uppercase;color:var(--muted);}
.pstat .val{font-family:'IBM Plex Mono',monospace;font-weight:700;font-size:12px;}
.pstat .val.g{color:#1a4a2e;} .pstat .val.a{color:#7a5500;} .pstat .val.r{color:#8b2500;}
.port-sum{display:grid;grid-template-columns:repeat(auto-fit,minmax(120px,1fr));border:2px solid var(--ink);margin-bottom:22px;}
.ps-cell{padding:12px 14px;border-right:1px solid #d4ccb8;}
.ps-cell:last-child{border-right:none;}
.ps-lbl{font-family:'IBM Plex Mono',monospace;font-size:8.5px;letter-spacing:2px;text-transform:uppercase;color:var(--muted);margin-bottom:3px;}
.ps-val{font-family:'Playfair Display',serif;font-size:20px;font-weight:700;}
.ps-val.g{color:#1a4a2e;}
.cmp-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:22px;}
@media(max-width:600px){.cmp-grid{grid-template-columns:1fr;}}
.cmp-box{padding:16px 18px;border:1.5px solid #d4ccb8;}
.cmp-box h4{font-family:'Playfair Display',serif;font-size:15px;margin-bottom:12px;padding-bottom:7px;border-bottom:2px solid var(--ink);}
.cmp-box ul{list-style:none;padding:0;}
.cmp-box li{display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid #e8e0d0;font-size:12px;gap:8px;}
.cmp-box li span:first-child{color:var(--muted);}
.cmp-box li span:last-child{font-family:'IBM Plex Mono',monospace;font-weight:600;}
.inv-grid{display:grid;grid-template-columns:1fr 1fr;margin-bottom:24px;border:2px solid var(--ink);}
@media(max-width:600px){.inv-grid{grid-template-columns:1fr;}}
.inv-col{padding:18px 20px;}
.inv-col.old{background:#1e1e1e;color:#ccc;}
.inv-col.new{background:var(--cream-dark,#e0dace);}
.inv-col h3{font-family:'Playfair Display',serif;font-size:15px;margin-bottom:12px;padding-bottom:7px;}
.inv-col.old h3{color:#999;border-bottom:1px solid #444;}
.inv-col.new h3{color:var(--ink);border-bottom:2px solid var(--gold);}
.inv-row{display:flex;justify-content:space-between;align-items:baseline;padding:5px 0;border-bottom:1px solid rgba(255,255,255,.06);font-size:11.5px;gap:10px;}
.inv-col.new .inv-row{border-bottom-color:#e8e0d0;}
.inv-ll{color:#999;font-size:10.5px;flex-shrink:0;}
.inv-col.new .inv-ll{color:var(--muted);}
.inv-vv{font-family:'IBM Plex Mono',monospace;font-weight:600;font-size:11px;text-align:right;}
.inv-vv.g{color:#7fba6a;} .inv-vv.r{color:#e06060;}
.inv-col.new .inv-vv.g{color:#1a4a2e;} .inv-col.new .inv-vv.r{color:var(--rust);}
.wht-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(185px,1fr));border:2px solid var(--ink);margin-bottom:22px;font-size:12px;}
.wht-cell{padding:12px 14px;border-right:1px solid #d4ccb8;border-bottom:1px solid #d4ccb8;}
.wht-cell h5{font-family:'IBM Plex Mono',monospace;font-size:9.5px;letter-spacing:1px;text-transform:uppercase;color:var(--muted);margin-bottom:5px;}
.wht-amt{font-family:'Playfair Display',serif;font-size:19px;font-weight:700;margin-bottom:3px;}
.wht-note{font-size:11px;color:var(--muted);line-height:1.6;}
.crash-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(270px,1fr));gap:16px;margin-bottom:24px;}
.crash-crd{border:1.5px solid #d4ccb8;padding:18px 20px;background:white;}
.crash-crd h3{font-family:'Playfair Display',serif;font-size:17px;margin-bottom:4px;}
.crash-badge{font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:2px;text-transform:uppercase;padding:3px 8px;border-radius:2px;display:inline-block;margin-bottom:10px;}
.crash-row{display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid #eee;font-size:12px;}
.crash-row .lbl{color:var(--muted);}
.crash-row .val{font-family:'IBM Plex Mono',monospace;font-weight:600;}
.crash-row .val.r{color:var(--rust);} .crash-row .val.g{color:#1a4a2e;}
.tl-item{display:flex;gap:14px;margin-bottom:0;position:relative;}
.tl-item::before{content:'';position:absolute;left:17px;top:36px;bottom:-1px;width:2px;background:#d4ccb8;}
.tl-item:last-child::before{display:none;}
.tl-dot{width:36px;height:36px;border-radius:50%;border:2px solid var(--ink);background:var(--paper,#f5f0e8);display:flex;align-items:center;justify-content:center;flex-shrink:0;font-family:'IBM Plex Mono',monospace;font-weight:700;font-size:12px;z-index:1;}
.tl-dot.on{background:var(--ink);color:var(--gold);}
.tl-dot.off{background:white;color:var(--muted);border-color:#ccc;}
.tl-body{padding:6px 0 22px;flex:1;}
.tl-body h4{font-family:'Playfair Display',serif;font-size:15px;margin-bottom:5px;}
.tl-body p{font-size:12px;color:#2c3e50;line-height:1.7;}
.tl-trig{font-family:'IBM Plex Mono',monospace;font-size:10px;color:var(--muted);display:inline-block;margin-top:6px;padding:3px 8px;border:1px solid #ccc;}

</style>

</head>
<body>

<!-- ═══════════════════════════════════════════════════
     STICKY NAV
═══════════════════════════════════════════════════ -->

<nav class="nav" aria-label="Page sections">
  <div class="nav-inner">
    <span class="nav-brand">Smith Maneuver</span>
    <a href="#how-it-works">How It Works</a>
    <a href="#tfsa-variant">TFSA Variant</a>
    <a href="#step-by-step">Step-by-Step</a>
    <a href="#market-returns">50yr Returns</a>
    <a href="#volatility">Volatility</a>
    <a href="#simulation">20yr Simulation</a>
    <a href="#etf-framework">ETF Framework</a>
    <a href="#phase1-port">Phase 1 TFSA</a>
    <a href="#phase2-port">Phase 2 Non-Reg</a>
    <a href="#roadmap">Roadmap</a>
  </div>
</nav>

<!-- ═══════════════════════════════════════════════════
     MASTHEAD
═══════════════════════════════════════════════════ -->

<header class="masthead">
  <div class="masthead-eyebrow">Canadian Tax Strategy · Complete Visual Reference · 2026</div>
  <h1>The Smith Maneuver<br><em>Complete Guide</em></h1>
  <p class="masthead-sub">A comprehensive visual walkthrough — from the mechanics of debt conversion, through the TFSA variant, to 50 years of market return data and a realistic 20-year simulation.</p>
  <div class="masthead-meta">
    <div class="meta-item"><span class="meta-label">Diagrams</span><span class="meta-value">9 Mermaid Charts</span></div>
    <div class="meta-item"><span class="meta-label">Data Charts</span><span class="meta-value">6 Interactive</span></div>
    <div class="meta-item"><span class="meta-label">Scenarios</span><span class="meta-value">3 Projections</span></div>
    <div class="meta-item"><span class="meta-label">Jurisdiction</span><span class="meta-value">Canada · CRA Rules</span></div>
    <div class="meta-item"><span class="meta-label">Disclaimer</span><span class="meta-value">Educational Only</span></div>
  </div>
</header>

<!-- STAT STRIP -->

<div class="stat-strip">
  <div class="stat-item"><span class="stat-val green">~9.3%</span><span class="stat-label">MSCI World CAGR 1975–2024</span></div>
  <div class="stat-item"><span class="stat-val">±15%</span><span class="stat-label">Avg Annual Std Deviation</span></div>
  <div class="stat-item"><span class="stat-val red">7</span><span class="stat-label">Bear Markets Since 1970</span></div>
  <div class="stat-item"><span class="stat-val blue">85%</span><span class="stat-label">Positive Years</span></div>
  <div class="stat-item"><span class="stat-val">14mo</span><span class="stat-label">Avg Bear Duration</span></div>
</div>

<!-- ═══════════════════════════════════════════════════
     PAGE BODY
═══════════════════════════════════════════════════ -->

<div class="page-body">

  <!-- TABLE OF CONTENTS -->

  <div class="toc" role="navigation" aria-label="Table of contents">
    <span class="toc-heading">Contents</span>
    <div class="toc-grid">
      <a class="toc-item" href="#how-it-works"><span class="toc-num">A</span><span class="toc-text">TFSA Variant — Full Loop with Yearly Withdrawal</span></a>
      <a class="toc-item" href="#step1"><span class="toc-num">1</span><span class="toc-text">Classic — Setup &amp; HELOC Approval</span></a>
      <a class="toc-item" href="#step2"><span class="toc-num">2</span><span class="toc-text">Classic — First Draw &amp; Investment</span></a>
      <a class="toc-item" href="#step3"><span class="toc-num">3</span><span class="toc-text">Classic — Interest Accrual &amp; Tax Deduction</span></a>
      <a class="toc-item" href="#step4"><span class="toc-num">4</span><span class="toc-text">Classic — Refund Recycling</span></a>
      <a class="toc-item" href="#step5"><span class="toc-num">5</span><span class="toc-text">Classic — The Compounding Loop</span></a>
      <a class="toc-item" href="#step6"><span class="toc-num">6</span><span class="toc-text">Classic — End Game &amp; Debt Conversion</span></a>
      <a class="toc-item" href="#market-returns"><span class="toc-num">I</span><span class="toc-text">50-Year Annual Return History</span></a>
      <a class="toc-item" href="#volatility"><span class="toc-num">II</span><span class="toc-text">Volatility, Distribution &amp; Bear Markets</span></a>
      <a class="toc-item" href="#simulation"><span class="toc-num">III</span><span class="toc-text">20-Year Smith Maneuver Simulation</span></a>
    </div>
  </div>

  <!-- ═══════════════════════════════════
       PART ONE: FLOW DIAGRAMS
  ═══════════════════════════════════ -->

  <div class="chapter-rule"><span class="chapter-rule-label">Part One — How It Works</span></div>

  <!-- DIAGRAM A: TFSA VARIANT -->

  <div id="how-it-works">
    <div class="section-head"><span class="section-tag">Diagram A</span></div>
    <div class="section-title">TFSA Variant with Yearly Cash Withdrawal</div>
    <p class="section-desc">The TFSA variant routes the annual tax refund into a TFSA for tax-free compounding, then makes a disciplined yearly tax-free withdrawal. The HELOC must flow to a non-registered account first — this is the CRA's direct-use requirement.</p>
  </div>

  <div id="tfsa-variant" class="diagram-card gold-top">
    <div class="card-eyebrow">Strategy A · Full Loop</div>
    <div class="card-title">TFSA Variant — Complete Flow with Annual Withdrawal</div>
    <div class="card-note">The HELOC → Non-Reg → Tax Refund → TFSA chain must be preserved in this order. TFSA withdrawals restore contribution room the following January 1st, enabling a repeating annual cycle.</div>
    <div class="diagram-scroll">
      <div class="mermaid">
flowchart TD
    A([🏠 Home with Equity]) --> B[Open HELOC\nAgainst Home Equity]
    B --> C{Draw HELOC Funds\ne.g. $10,000}
    C --> D[Invest in Non-Registered\nIncome-Producing Assets\ne.g. Canadian Dividend ETFs]
    D --> E[Investment Generates\nTaxable Income / Dividends]
    E --> F[Use Income to Pay\nMortgage Principal]
    F --> G[Mortgage Principal Reduces\n→ New Home Equity Created]
    G --> H[Re-draw HELOC\nfor New Equity Amount]
    H --> D
    D --> I[HELOC Interest\nIs Tax-Deductible ✅\nCRA Direct Use Test Met]
    I --> J[File Taxes:\nDeduct HELOC Interest]
    J --> K[💰 Annual Tax Refund]
    K --> L[Contribute Tax Refund\nto TFSA\nup to Contribution Room]
    L --> M[🛡️ TFSA Invests\nTax-Free Growth]
    M --> N{Annual Year-End\nReview}
    N --> O[📅 Yearly Cash Withdrawal\nfrom TFSA — Tax-Free]
    O --> P[Use Cash For:\n• Extra Mortgage Payment\n• Living Expenses\n• Re-invest Non-Reg\n• Emergency Fund]
    P --> G
    M --> Q[TFSA Room Restored\nNext Jan 1st\nfor Withdrawn Amount]
    Q --> L
      </div>
    </div>
    <div class="callout warn">
      <strong>⚠️ CRA Rule:</strong> You cannot draw HELOC funds and deposit them directly into a TFSA. The borrowed money must flow into a non-registered, income-earning investment first. Interest deductibility is only available when the direct-use test is met. Consult a tax advisor before implementing.
    </div>
  </div>

  <!-- CLASSIC STEP-BY-STEP -->

  <div class="chapter-rule"><span class="chapter-rule-label">Classic Smith Maneuver — Step by Step</span></div>
  <div id="step-by-step">
    <div class="section-head"><span class="section-tag">Diagrams 1–6</span></div>
    <div class="section-title">The Classic Maneuver — Full Lifecycle</div>
    <p class="section-desc">Six diagrams tracing the full lifecycle from initial HELOC setup, through the monthly draw cycle, tax mechanics, refund recycling, the compounding loop, and finally the end-game debt conversion.</p>
  </div>

  <!-- STEP 1 -->

  <div id="step1" class="diagram-card">
    <div class="card-eyebrow">Step 1 · Foundation</div>
    <div class="card-title">Setup — Readvanceable Mortgage or HELOC</div>
    <div class="card-note">The strategy requires a readvanceable mortgage product where the HELOC limit automatically increases as mortgage principal is paid down. Available from most major Canadian lenders (Manulife One, Scotia STEP, BMO Homeowner ReadiLine, etc.).</div>
    <div class="diagram-scroll">
      <div class="mermaid">
flowchart LR
    A([🏠 Home\nValue: $800K\nMortgage: $400K\nEquity: $400K]) --> B[Apply for\nReadvanceable Mortgage\nor HELOC]
    B --> C[Bank Approves HELOC\nup to 80% LTV\nMax HELOC: $240K\nAvailable Now: $0]
    C --> D[✅ Ready to Begin\nSmith Maneuver\nEach mortgage payment\nunlocks new HELOC room]
      </div>
    </div>
    <div class="callout">
      <strong>80% LTV Rule:</strong> HELOC capacity = (Home Value × 80%) − Mortgage Balance. As your mortgage shrinks with each payment, the available HELOC room grows by an equal amount — this is the mechanical engine of the Smith Maneuver.
    </div>
  </div>

  <!-- STEP 2 -->

  <div id="step2" class="diagram-card">
    <div class="card-eyebrow">Step 2 · First Draw</div>
    <div class="card-title">First Draw &amp; Investment</div>
    <div class="card-note">Each mortgage payment's principal component unlocks an equivalent amount of HELOC room. That room is immediately drawn and invested in income-producing assets in a non-registered brokerage account.</div>
    <div class="diagram-scroll">
      <div class="mermaid">
flowchart TD
    A[Make Regular\nMortgage Payment\ne.g. $2,000/month\n~$500 principal] --> B[Principal Portion\nReduces Mortgage Balance\n$400,000 → $399,500]
    B --> C[HELOC Room\nOpens by Same Amount\n$500 available]
    C --> D[Draw $500\nfrom HELOC]
    D --> E[Deposit $500 into\nNon-Registered\nBrokerage Account]
    E --> F[Buy $500 of\nCanadian Dividend ETF\ne.g. XDV, VDY]
    F --> G[✅ Investment Made\nHELOC Balance: $500\nMortgage Balance: $399,500]
      </div>
    </div>
    <div class="callout">
      <strong>Net effect:</strong> Total debt is unchanged ($399,500 mortgage + $500 HELOC = $400,000), but you now own $500 in investments. The critical difference: mortgage interest is non-deductible, while the HELOC interest is deductible.
    </div>
  </div>

  <!-- STEP 3 -->

  <div id="step3" class="diagram-card rust-top">
    <div class="card-eyebrow">Step 3 · Tax Mechanics</div>
    <div class="card-title">Interest Accrues &amp; Tax Deduction</div>
    <div class="card-note">Tax deductibility of HELOC interest is the core economic advantage. CRA's "direct use" test requires meticulous record-keeping — every dollar of HELOC proceeds must be traceable to income-earning investments.</div>
    <div class="diagram-scroll">
      <div class="mermaid">
flowchart TD
    A[HELOC Balance Grows\nover the Year\ne.g. $6,000 by Year-End] --> B[HELOC Interest Accrues\ne.g. 6.5% on $6,000\n= ~$390 interest for year]
    B --> C{Is Interest\nDeductible?}
    C -->|Yes ✅| D[CRA Direct Use Test:\nBorrowed funds went\ndirectly to income-earning\nnon-reg investments]
    C -->|No ❌| E[Would fail if:\nFunds used for personal\nexpenses or TFSA directly]
    D --> F[Track ALL HELOC\nInterest Carefully\nKeep receipts and statements]
    F --> G[At Tax Time:\nReport on Schedule 4\nLine 22100 — Carrying Charges]
    G --> H[💰 Tax Deduction:\n$390 deducted from\ntaxable income\n~$175 refund at 45% MTR]
      </div>
    </div>
    <div class="callout warn">
      <strong>Record-keeping is non-negotiable.</strong> Maintain a dedicated HELOC account used solely for investments. Never commingle personal spending. CRA can audit and deny deductions if the paper trail is unclear. A spreadsheet tracking each draw, investment, and interest charge is strongly recommended.
    </div>
  </div>

  <!-- STEP 4 -->

  <div id="step4" class="diagram-card gold-top">
    <div class="card-eyebrow">Step 4 · Refund Deployment</div>
    <div class="card-title">Tax Refund Recycled into Mortgage</div>
    <div class="card-note">The annual tax refund is the "bonus accelerant" of the strategy. Applying it as a lump-sum principal payment creates more HELOC room, which funds more investments — a self-reinforcing cycle.</div>
    <div class="diagram-scroll">
      <div class="mermaid">
flowchart TD
    A[💰 Receive Tax Refund\ne.g. $1,800 Year 1\nfrom HELOC interest deduction] --> B{How to Deploy\nthe Refund?}
    B --> C[Option A ✅ Recommended:\nApply to Mortgage\nPrincipal as Lump Sum]
    B --> D[Option B:\nRe-invest in\nNon-Registered Account]
    B --> E[Option C:\nLiving expenses\n⚠️ Weakens strategy]
    C --> F[Mortgage Balance\nDrops Further\ne.g. $399,500 → $397,700]
    F --> G[New Equity Unlocked\n→ More HELOC Room]
    G --> H[Draw New HELOC Room\nand Re-invest]
    H --> I[✅ Acceleration Loop:\nEach refund speeds up\nmortgage paydown and\ngrows investment base]
      </div>
    </div>
  </div>

  <!-- STEP 5 -->

  <div id="step5" class="diagram-card">
    <div class="card-eyebrow">Step 5 · Steady State</div>
    <div class="card-title">The Compounding Loop</div>
    <div class="card-note">Once established, the strategy enters a self-sustaining loop. Monthly payments, investment income, and annual tax refunds each feed the next cycle. Over 20–25 years the compounding effect is substantial.</div>
    <div class="diagram-scroll">
      <div class="mermaid">
flowchart LR
    A([Monthly\nMortgage Payment]) --> B[Principal Portion\nOpens HELOC Room]
    B --> C[Draw HELOC\nInvest in Non-Reg]
    C --> D[Portfolio Grows\nDividends Reinvested]
    D --> E[Annual Tax Refund\nfrom Interest Deduction]
    E --> F[Lump Sum to\nMortgage Principal]
    F --> G[More Equity\n→ More HELOC Room]
    G --> C
    D --> H[Dividends and\nGrowth Compound]
    H --> I[🎯 End State:\nMortgage Paid Off\nLarge Non-Reg Portfolio\nDebt is now fully\ntax-deductible]
      </div>
    </div>
    <div class="callout">
      <strong>The key insight:</strong> You begin with $400K of non-deductible mortgage debt. Over time, you convert it dollar by dollar into deductible investment debt, while simultaneously building a portfolio. At completion, the full original mortgage amount is "good debt."
    </div>
  </div>

  <!-- STEP 6 -->

  <div id="step6" class="diagram-card gold-top">
    <div class="card-eyebrow">Step 6 · End Game</div>
    <div class="card-title">Mortgage Fully Paid — Debt Conversion Complete</div>
    <div class="card-note">After 20–25 years, the mortgage is eliminated. The entire HELOC balance — equal to the original mortgage — is now fully tax-deductible investment debt. Three strategic exit options emerge.</div>
    <div class="diagram-scroll">
      <div class="mermaid">
flowchart TD
    A([🏠 Mortgage Fully Paid\nHELOC = Original\nMortgage Amount\ne.g. $400K]) --> B[Entire HELOC Balance\nis Tax-Deductible Debt\nGood Debt Conversion\nComplete ✅]
    B --> C[Non-Reg Portfolio\nhas been growing\nfor 20-25 years]
    C --> D{Decision Point}
    D --> E[Option A: Hold Portfolio\nContinue collecting\ntax-advantaged dividends\nOffset HELOC interest]
    D --> F[Option B: Sell Portfolio\nPay off HELOC entirely\nDebt-free with\nlarge capital gain]
    D --> G[Option C: Rebalance\nPartial paydown plus keep\ncore portfolio running]
    E --> H[💰 Net Wealth:\nHome owned free and clear\nLarge investment portfolio\nAnnual carrying cost offset\nby dividends]
      </div>
    </div>
    <div class="callout">
      <strong>Outcome comparison:</strong> A homeowner who implements the Smith Maneuver vs. one who simply pays down their mortgage will typically end up with a similar net worth at payoff — but the Smith Maneuver homeowner also holds a large, liquid investment portfolio, representing significantly greater total wealth.
    </div>
  </div>

  <!-- ═══════════════════════════════════
       PART TWO: MARKET DATA
  ═══════════════════════════════════ -->

  <div class="chapter-rule"><span class="chapter-rule-label">Part Two — Market Returns &amp; Volatility</span></div>

  <!-- SECTION I: 50-YEAR RETURNS -->

  <div id="market-returns">
    <div class="section-head"><span class="section-tag">Section I</span></div>
    <div class="section-title">50 Years of Annual Returns</div>
    <p class="section-desc">Every calendar year return for the MSCI World Index from 1975–2024 — the full set of conditions a Smith Maneuver investor must be prepared to hold through. Green = positive years. Red = negative years.</p>
  </div>

  <div class="chart-card">
    <div class="chart-label">MSCI World · Annual Total Return · 1975–2024 (USD)</div>
    <h3>The Full 50-Year Return Sequence</h3>
    <div class="chart-note">The dashed gold line shows the long-run ~9.3% CAGR. Notice that negative years cluster, recoveries are sharp, and most years are positive — but the bad years can be severe. The Smith Maneuver investor never exits during these downturns.</div>
    <div class="chart-wrap tall">
      <canvas id="historicalChart"></canvas>
    </div>
    <div class="callout">
      <strong>Key insight for Smith Maneuver investors:</strong> During negative years, your HELOC and portfolio are both present. The portfolio may be down 20–40%, but the mortgage is still being paid down. Dividends continue. The interest deduction still applies. The strategy is designed to hold through cycles — not to time them.
    </div>
  </div>

  <!-- NOTABLE YEARS TABLE -->

  <div class="chart-card">
    <div class="chart-label">Notable Years · Selected Landmarks</div>
    <h3>Best, Worst &amp; Most Important Years — MSCI World</h3>
    <div class="chart-note">Key years for context. Recovery years after crashes are as important to understand as the crashes themselves — they represent the engine of long-term compounding.</div>
    <div class="table-scroll">
      <table class="year-table">
        <thead>
          <tr>
            <th>Year</th>
            <th>Return</th>
            <th>Context</th>
            <th style="width:100px">Magnitude</th>
          </tr>
        </thead>
        <tbody id="histTableBody"></tbody>
      </table>
    </div>
  </div>

  <!-- SECTION II: VOLATILITY -->

  <div id="volatility">
    <div class="section-head"><span class="section-tag">Section II</span></div>
    <div class="section-title">The Range of Expected Annual Swings</div>
    <p class="section-desc">What does "±15% standard deviation" actually mean in practice? These charts show the realistic range of outcomes in any given year, how often bad years occur, the historical bear market profile, and how time compresses volatility.</p>
  </div>

  <div class="two-col">
    <div class="chart-card">
      <div class="chart-label">Return Distribution · 50 Years</div>
      <h3>How Often Each Range Occurs</h3>
      <div class="chart-note">Frequency of annual returns in each bucket. The distribution skews right — more very large positive years than very large negative ones.</div>
      <div class="chart-wrap medium"><canvas id="distChart"></canvas></div>
    </div>
    <div class="chart-card">
      <div class="chart-label">Volatility Bands · σ = 15%</div>
      <h3>±1σ and ±2σ Around the Mean</h3>
      <div class="chart-note">In any given year, ~68% of returns fall within the ±1σ band (−5.7% to +24.3%). Only ~5% of years fall outside the ±2σ extremes.</div>
      <div class="chart-wrap medium"><canvas id="bandChart"></canvas></div>
    </div>
  </div>

  <div class="two-col">
    <div class="chart-card rust-top">
      <div class="chart-label">Bear Market Profile · 1970–2024</div>
      <h3>7 Bear Markets in 55 Years</h3>
      <div class="chart-note">Duration (bars, months) and severity (line, % decline) for each bear market. Average: 14 months, −30% decline.</div>
      <div class="chart-wrap medium"><canvas id="bearChart"></canvas></div>
    </div>
    <div class="chart-card gold-top">
      <div class="chart-label">Rolling 10-Year CAGR · 1984–2024</div>
      <h3>Time Compresses Volatility</h3>
      <div class="chart-note">The longer the holding period, the tighter the range of outcomes. This is why the Smith Maneuver's 20–25 year horizon is a feature, not a flaw.</div>
      <div class="chart-wrap medium"><canvas id="rollingChart"></canvas></div>
    </div>
  </div>

  <!-- SECTION III: SIMULATION -->

  <div class="chapter-rule"><span class="chapter-rule-label">Part Three — 20-Year Projection</span></div>

  <div id="simulation">
    <div class="section-head"><span class="section-tag">Section III</span></div>
    <div class="section-title">20-Year Smith Maneuver Simulation</div>
    <p class="section-desc">A realistic year-by-year projection using historically-calibrated returns — including crashes in years 4, 12, and 18 (one major, two moderate bear markets, consistent with historical frequency). Assumptions: $500K home · $300K mortgage · 6.5% HELOC rate · 45% marginal tax rate.</p>
  </div>

  <div class="toggle-row" role="group" aria-label="Scenario selector">
    <button class="toggle-btn active" onclick="switchScenario('base', this)">Base Case (~9.3%)</button>
    <button class="toggle-btn" onclick="switchScenario('conservative', this)">Conservative (~7%)</button>
    <button class="toggle-btn" onclick="switchScenario('optimistic', this)">Optimistic (~11%)</button>
  </div>

  <div class="chart-card">
    <div class="chart-label">Portfolio Growth · With vs. Without Smith Maneuver</div>
    <h3>Smith Maneuver Portfolio vs Standard Mortgage (No Investing)</h3>
    <div class="chart-note">Includes realistic bear market years. The gold line shows net wealth with the strategy. The dashed grey line shows equity growth without it. HELOC draws grow as mortgage principal is paid down each month.</div>
    <div class="chart-wrap tall">
      <canvas id="simChart"></canvas>
    </div>
    <div class="callout gold">
      <strong>What you're seeing:</strong> During crash years the portfolio dips — sometimes sharply. But the Smith Maneuver investor never sells. The mortgage keeps being paid down. Tax refunds still arrive. The portfolio's cost base (the HELOC) still generates deductions. Recovery years then dramatically outperform, driving long-term wealth accumulation.
    </div>
  </div>

  <div class="chart-card">
    <div class="chart-label">Year-by-Year Breakdown · Full 20-Year Table</div>
    <h3>Complete Simulation Table</h3>
    <div class="chart-note">Each row shows market return, portfolio value, HELOC balance, annual tax refund, and net wealth. 🔻 = crash year · 🚀 = strong bull year. Scroll horizontally on mobile.</div>
    <div class="table-scroll">
      <div id="simTableContainer"></div>
    </div>
    <div class="callout warn">
      <strong>⚠️ Important Disclaimer:</strong> This simulation uses historically-calibrated averages and stylized crash scenarios for illustration only. Actual returns will differ materially. This is not financial advice — consult a fee-only financial planner and qualified tax advisor before implementing the Smith Maneuver. HELOC rates, tax laws, and market returns are all variable and subject to change.
    </div>
  </div>

</div><!-- /page-body -->

<!-- FOOTER -->

<footer class="page-footer">
  <span>THE SMITH MANEUVER — COMPLETE VISUAL GUIDE · 2026</span>
  <span>Data: MSCI World 1975–2024 · PWL Capital · iShares XWD.TO · YStat.org</span>
  <span class="footer-warn">⚠️ EDUCATIONAL PURPOSES ONLY — NOT FINANCIAL OR TAX ADVICE</span>
</footer>

<!-- ═══════════════════════════════════════════════════
     SCRIPTS
═══════════════════════════════════════════════════ -->

<script>
// ── MERMAID INIT ─────────────────────────────────────────
mermaid.initialize({
  startOnLoad: true,
  theme: 'base',
  themeVariables: {
    primaryColor: '#1a6b5e',
    primaryTextColor: '#ffffff',
    primaryBorderColor: '#135248',
    lineColor: '#7a7060',
    secondaryColor: '#c9a84c',
    secondaryTextColor: '#0e1117',
    tertiaryColor: '#f5f0e8',
    tertiaryTextColor: '#0e1117',
    background: '#ffffff',
    mainBkg: '#1a6b5e',
    nodeBorder: '#135248',
    clusterBkg: '#f0ece0',
    titleColor: '#0e1117',
    edgeLabelBackground: '#f5f0e8',
    fontSize: '13px'
  },
  flowchart: { curve: 'basis', padding: 18, nodeSpacing: 44, rankSpacing: 52 }
});

// ── SHARED CHART DEFAULTS ────────────────────────────────
const paperBg = '#f5f0e8';
const chartDefaults = {
  tooltip: {
    backgroundColor: '#0e1117',
    borderColor: '#2a2a2a',
    borderWidth: 1,
    titleColor: '#f5f0e8',
    bodyColor: '#c4bba8',
    padding: 10,
  }
};
const axisStyle = {
  ticks: { color: '#9a9080', font: { family: "'IBM Plex Mono', monospace", size: 10 } },
  grid: { color: 'rgba(196,187,168,0.4)' },
  border: { color: '#c4bba8' }
};

// ── DATA ─────────────────────────────────────────────────
const historicalData = [
  {y:1975,r:35.4},{y:1976,r:12.1},{y:1977,r:-4.3},{y:1978,r:16.5},{y:1979,r:9.6},
  {y:1980,r:25.7},{y:1981,r:-4.8},{y:1982,r:9.7},{y:1983,r:22.1},{y:1984,r:4.8},
  {y:1985,r:40.7},{y:1986,r:41.9},{y:1987,r:15.2},{y:1988,r:23.3},{y:1989,r:16.6},
  {y:1990,r:-17.0},{y:1991,r:18.3},{y:1992,r:-5.2},{y:1993,r:22.5},{y:1994,r:5.6},
  {y:1995,r:20.7},{y:1996,r:13.5},{y:1997,r:15.8},{y:1998,r:24.3},{y:1999,r:24.9},
  {y:2000,r:-13.2},{y:2001,r:-16.8},{y:2002,r:-19.9},{y:2003,r:33.1},{y:2004,r:14.7},
  {y:2005,r:9.5},{y:2006,r:20.1},{y:2007,r:9.0},{y:2008,r:-40.7},{y:2009,r:29.9},
  {y:2010,r:11.8},{y:2011,r:-5.5},{y:2012,r:15.8},{y:2013,r:26.7},{y:2014,r:4.9},
  {y:2015,r:-0.9},{y:2016,r:7.5},{y:2017,r:22.4},{y:2018,r:-8.7},{y:2019,r:27.7},
  {y:2020,r:15.9},{y:2021,r:21.8},{y:2022,r:-18.1},{y:2023,r:23.8},{y:2024,r:18.7}
];

const notableYears = [
  {year:1975,r:35.4,note:"Recovery from 1973–74 oil crisis bear market",type:"up"},
  {year:1980,r:25.7,note:"Bull market resumes after stagflation era",type:"up"},
  {year:1985,r:40.7,note:"Strong bull — USD weakness, Japan boom",type:"up"},
  {year:1986,r:41.9,note:"Best year on record — Yen surge vs USD",type:"up"},
  {year:1990,r:-17.0,note:"Gulf War, S&L crisis, recession",type:"down"},
  {year:1995,r:20.7,note:"Dot-com era begins, strong US growth",type:"up"},
  {year:2000,r:-13.2,note:"Dot-com bubble begins to burst",type:"down"},
  {year:2002,r:-19.9,note:"Post-dot-com trough — 3rd consecutive down year",type:"down"},
  {year:2003,r:33.1,note:"Massive rebound from tech bust",type:"up"},
  {year:2008,r:-40.7,note:"Global Financial Crisis — worst year in 50yr data",type:"down"},
  {year:2009,r:29.9,note:"GFC recovery begins",type:"up"},
  {year:2013,r:26.7,note:"Post-GFC bull market in full swing",type:"up"},
  {year:2019,r:27.7,note:"Pre-COVID bull — Fed pivot year",type:"up"},
  {year:2022,r:-18.1,note:"Rate hike cycle — inflation shock",type:"down"},
  {year:2024,r:18.7,note:"AI-driven bull, US outperformance",type:"up"},
];

const bearMarkets = [
  {name:"1973–74 Oil",months:23,decline:-47},
  {name:"1980–82 Stag.",months:19,decline:-26},
  {name:"1987 Black Mon.",months:4,decline:-29},
  {name:"1990 Gulf War",months:9,decline:-21},
  {name:"2000–02 Dot-Com",months:31,decline:-49},
  {name:"2007–09 GFC",months:16,decline:-57},
  {name:"2022 Rate Shock",months:12,decline:-26},
];

const scenarios = {
  base: {
    label:"Base (~9.3%)",
    returns:[8.5,22.1,14.3,-18.5,11.2,27.4,9.8,15.6,-8.2,19.3,12.7,-35.0,32.1,18.4,11.0,7.5,-14.2,28.9,16.3,21.1],
    color:"#1a6b5e"
  },
  conservative: {
    label:"Conservative (~7%)",
    returns:[6.2,14.1,9.5,-18.5,7.8,18.2,6.4,10.3,-8.2,12.1,8.6,-35.0,24.5,11.8,7.2,5.1,-14.2,20.3,10.1,14.5],
    color:"#4a6a8a"
  },
  optimistic: {
    label:"Optimistic (~11%)",
    returns:[11.2,28.5,18.6,-18.5,14.8,33.2,13.1,19.8,-8.2,25.1,16.2,-35.0,41.2,24.3,14.5,10.2,-14.2,36.8,21.4,27.9],
    color:"#8a5a10"
  }
};

// ── CHART 1: HISTORICAL BAR ───────────────────────────────
new Chart(document.getElementById('historicalChart'), {
  type: 'bar',
  data: {
    labels: historicalData.map(d => d.y),
    datasets: [
      {
        label: 'Annual Return %',
        data: historicalData.map(d => d.r),
        backgroundColor: historicalData.map(d => d.r >= 0 ? 'rgba(26,107,94,0.7)' : 'rgba(201,76,26,0.7)'),
        borderColor: historicalData.map(d => d.r >= 0 ? '#1a6b5e' : '#c94c1a'),
        borderWidth: 1, borderRadius: 1,
      },
      {
        label: 'Long-run avg ~9.3%',
        data: historicalData.map(() => 9.3),
        type: 'line',
        borderColor: 'rgba(201,168,76,0.7)',
        borderWidth: 2,
        borderDash: [6,4],
        pointRadius: 0,
        fill: false,
      }
    ]
  },
  options: {
    responsive: true, maintainAspectRatio: false,
    plugins: {
      legend: { labels: { color: '#7a7060', font: { family:"'IBM Plex Mono',monospace", size:10 } } },
      tooltip: { ...chartDefaults.tooltip, callbacks: { label: ctx => ` ${ctx.parsed.y > 0 ? '+' : ''}${ctx.parsed.y.toFixed(1)}%` } }
    },
    scales: {
      x: { ...axisStyle, ticks: { ...axisStyle.ticks, maxRotation:45 } },
      y: { ...axisStyle, ticks: { ...axisStyle.ticks, callback: v => v + '%' } }
    }
  }
});

// ── CHART 2: DISTRIBUTION ────────────────────────────────
const buckets = [
  {label:'< −30%',min:-100,max:-30,c:'rgba(201,76,26,0.85)'},
  {label:'−30 to −20%',min:-30,max:-20,c:'rgba(201,76,26,0.65)'},
  {label:'−20 to −10%',min:-20,max:-10,c:'rgba(201,76,26,0.45)'},
  {label:'−10 to 0%',min:-10,max:0,c:'rgba(201,168,76,0.6)'},
  {label:'0 to 10%',min:0,max:10,c:'rgba(26,107,94,0.45)'},
  {label:'10 to 20%',min:10,max:20,c:'rgba(26,107,94,0.65)'},
  {label:'20 to 30%',min:20,max:30,c:'rgba(26,107,94,0.80)'},
  {label:'> 30%',min:30,max:100,c:'rgba(26,107,94,0.95)'},
];
new Chart(document.getElementById('distChart'), {
  type:'bar',
  data: {
    labels: buckets.map(b => b.label),
    datasets: [{ label:'Years', data: buckets.map(b => historicalData.filter(d => d.r >= b.min && d.r < b.max).length), backgroundColor: buckets.map(b => b.c), borderWidth:0, borderRadius:2 }]
  },
  options: {
    responsive:true, maintainAspectRatio:false,
    plugins: { legend:{display:false}, tooltip:{ ...chartDefaults.tooltip, callbacks:{label:ctx=>` ${ctx.parsed.y} years out of 50`} } },
    scales: {
      x: { ...axisStyle, ticks:{ ...axisStyle.ticks, maxRotation:40, font:{size:9} } },
      y: { ...axisStyle }
    }
  }
});

// ── CHART 3: VOLATILITY BANDS ────────────────────────────
const mean=9.3, sd=15.0;
new Chart(document.getElementById('bandChart'), {
  type:'bar',
  data: {
    labels:['−2σ Extreme','−1σ Bad Year','Average','＋1σ Good','＋2σ Great'],
    datasets:[{ label:'Expected Return', data:[mean-2*sd,mean-sd,mean,mean+sd,mean+2*sd], backgroundColor:['rgba(201,76,26,0.8)','rgba(201,76,26,0.5)','rgba(201,168,76,0.75)','rgba(26,107,94,0.65)','rgba(26,107,94,0.9)'], borderRadius:3 }]
  },
  options: {
    responsive:true, maintainAspectRatio:false,
    plugins: { legend:{display:false}, tooltip:{ ...chartDefaults.tooltip, callbacks:{label:ctx=>` ${ctx.parsed.y.toFixed(1)}% expected`} } },
    scales: {
      x: { ...axisStyle, ticks:{...axisStyle.ticks,font:{size:9}} },
      y: { ...axisStyle, min:-25, max:45, ticks:{...axisStyle.ticks,callback:v=>v+'%'} }
    }
  }
});

// ── CHART 4: BEAR MARKETS ────────────────────────────────
new Chart(document.getElementById('bearChart'), {
  type:'bar',
  data: {
    labels: bearMarkets.map(b=>b.name),
    datasets: [
      { label:'Decline (%)', data:bearMarkets.map(b=>b.decline), backgroundColor:'rgba(201,76,26,0.6)', borderColor:'#c94c1a', borderWidth:1, borderRadius:2, yAxisID:'y' },
      { label:'Duration (mo)', data:bearMarkets.map(b=>b.months), type:'line', borderColor:'#c9a84c', backgroundColor:'rgba(201,168,76,0.1)', borderWidth:2, pointRadius:4, pointBackgroundColor:'#c9a84c', yAxisID:'y2', fill:false }
    ]
  },
  options: {
    responsive:true, maintainAspectRatio:false,
    plugins: { legend:{labels:{color:'#7a7060',font:{family:"'IBM Plex Mono',monospace",size:9}}}, tooltip:{ ...chartDefaults.tooltip } },
    scales: {
      x: { ...axisStyle, ticks:{...axisStyle.ticks,maxRotation:30,font:{size:9}} },
      y: { ...axisStyle, position:'left', ticks:{...axisStyle.ticks,callback:v=>v+'%'} },
      y2: { ...axisStyle, position:'right', grid:{display:false}, ticks:{...axisStyle.ticks,callback:v=>v+'mo'} }
    }
  }
});

// ── CHART 5: ROLLING 10-YEAR ─────────────────────────────
const rollingYears=[], rollingVals=[];
for(let i=9;i<historicalData.length;i++){
  const slice=historicalData.slice(i-9,i+1);
  let cagr=slice.reduce((a,d)=>a*(1+d.r/100),1);
  cagr=(Math.pow(cagr,0.1)-1)*100;
  rollingYears.push(historicalData[i].y);
  rollingVals.push(+cagr.toFixed(2));
}
new Chart(document.getElementById('rollingChart'), {
  type:'line',
  data: {
    labels:rollingYears,
    datasets:[
      { label:'Rolling 10-yr CAGR', data:rollingVals, borderColor:'#1a6b5e', backgroundColor:'rgba(26,107,94,0.08)', borderWidth:2, pointRadius:2, fill:true, tension:0.3 },
      { label:'Long-run avg 9.3%', data:rollingYears.map(()=>9.3), borderColor:'rgba(201,168,76,0.6)', borderWidth:1.5, borderDash:[5,5], pointRadius:0, fill:false }
    ]
  },
  options: {
    responsive:true, maintainAspectRatio:false,
    plugins: { legend:{labels:{color:'#7a7060',font:{family:"'IBM Plex Mono',monospace",size:9}}}, tooltip:{ ...chartDefaults.tooltip, callbacks:{label:ctx=>` ${ctx.parsed.y.toFixed(1)}%`} } },
    scales: {
      x: { ...axisStyle, ticks:{...axisStyle.ticks,maxRotation:45,font:{size:9}} },
      y: { ...axisStyle, ticks:{...axisStyle.ticks,callback:v=>v+'%'} }
    }
  }
});

// ── HISTORICAL TABLE ──────────────────────────────────────
const tbody = document.getElementById('histTableBody');
notableYears.forEach(row => {
  const barW = Math.min(Math.abs(row.r)/42*100,100);
  const pillClass = row.type==='up'?'pill-up':'pill-down';
  const barColor = row.type==='up'?'#1a6b5e':'#c94c1a';
  const sign = row.r>0?'+':'';
  tbody.innerHTML += `<tr>
    <td style="font-family:'IBM Plex Mono',monospace;color:#7a7060;font-size:11px">${row.year}</td>
    <td><span class="return-pill ${pillClass}">${sign}${row.r}%</span></td>
    <td style="font-size:12px;color:#7a7060">${row.note}</td>
    <td><span class="mini-bar" style="width:${barW}%;background:${barColor};opacity:0.65"></span></td>
  </tr>`;
});

// ── SIMULATION ENGINE ─────────────────────────────────────
let simChartInst = null;

function buildSim(key) {
  const ret = scenarios[key].returns;
  let mortgage=300000, heloc=0, portfolio=0, cumRefunds=0;
  const rows=[];
  for(let i=0;i<20;i++){
    const year=2026+i, r=ret[i];
    const principal = 4800 + i*180;
    mortgage = Math.max(0, mortgage-principal);
    heloc += principal;
    portfolio = portfolio*(1+r/100)+principal;
    const interest = heloc*0.065;
    const refund = interest*0.45;
    cumRefunds += refund;
    mortgage = Math.max(0, mortgage-refund);
    const homeEquity = 500000-mortgage;
    const netWealth = homeEquity+portfolio-heloc;
    rows.push({year,r,mortgage:Math.round(mortgage),heloc:Math.round(heloc),portfolio:Math.round(portfolio),interest:Math.round(interest),refund:Math.round(refund),cumRefunds:Math.round(cumRefunds),netWealth:Math.round(netWealth),isCrash:r<-10,isBull:r>20});
  }
  return rows;
}

function fmt(n){ return '$'+Math.abs(n).toLocaleString('en-CA',{maximumFractionDigits:0}); }

function renderSim(key) {
  const rows = buildSim(key);
  const color = scenarios[key].color;

  // Destroy & rebuild chart
  const ctx = document.getElementById('simChart').getContext('2d');
  if(simChartInst) simChartInst.destroy();

  const noStrat = rows.map((_,i) => 500000 - Math.max(0,300000-(4800+i*180)*(i+1)));

  simChartInst = new Chart(ctx, {
    type:'line',
    data: {
      labels: rows.map(r=>r.year),
      datasets:[
        { label:'Portfolio Value', data:rows.map(r=>r.portfolio), borderColor:color, backgroundColor:color+'18', borderWidth:2.5, pointRadius:4, pointBackgroundColor:color, fill:true, tension:0.2 },
        { label:'HELOC Balance', data:rows.map(r=>r.heloc), borderColor:'rgba(201,76,26,0.7)', borderWidth:1.5, borderDash:[5,4], pointRadius:2, fill:false, tension:0.2 },
        { label:'Net Wealth (Strategy)', data:rows.map(r=>r.netWealth), borderColor:'#c9a84c', borderWidth:2.5, pointRadius:3, fill:false, tension:0.2 },
        { label:'Home Equity (No Strategy)', data:noStrat, borderColor:'rgba(122,112,96,0.4)', borderWidth:1.5, borderDash:[3,6], pointRadius:0, fill:false, tension:0.3 }
      ]
    },
    options: {
      responsive:true, maintainAspectRatio:false,
      plugins: {
        legend:{labels:{color:'#7a7060',font:{family:"'IBM Plex Mono',monospace",size:10},padding:16}},
        tooltip:{ ...chartDefaults.tooltip, callbacks:{label:ctx=>` ${ctx.dataset.label}: ${fmt(ctx.parsed.y)}`} }
      },
      scales: {
        x:{ ...axisStyle },
        y:{ ...axisStyle, ticks:{...axisStyle.ticks,callback:v=>'$'+(v/1000).toFixed(0)+'K'} }
      }
    }
  });

  // Table
  let html=`<table class="sim-table"><thead><tr>
    <th>Year</th><th>Return</th><th>Portfolio</th><th>HELOC Bal</th>
    <th>Interest</th><th>Tax Refund</th><th>Mortgage</th><th>Net Wealth</th>
  </tr></thead><tbody>`;

  rows.forEach(r => {
    const rc=r.r>=0?'pos':'neg';
    const cls=r.isCrash?'crash':r.isBull?'bull':'';
    const sign=r.r>0?'+':'';
    html+=`<tr class="${cls}">
      <td>${r.year}${r.isCrash?' 🔻':r.isBull?' 🚀':''}</td>
      <td class="${rc}">${sign}${r.r.toFixed(1)}%</td>
      <td class="pos">${fmt(r.portfolio)}</td>
      <td class="neg">${fmt(r.heloc)}</td>
      <td class="neutral">${fmt(r.interest)}</td>
      <td class="pos">${fmt(r.refund)}</td>
      <td>${fmt(r.mortgage)}</td>
      <td class="${r.netWealth>0?'pos':'neg'}">${fmt(r.netWealth)}</td>
    </tr>`;
  });

  const f=rows[19];
  html+=`<tr><td>Final / Total</td><td>—</td><td>${fmt(f.portfolio)}</td><td>${fmt(f.heloc)}</td>
    <td>—</td><td>${fmt(f.cumRefunds)} total</td><td>${fmt(f.mortgage)}</td><td>${fmt(f.netWealth)}</td></tr>`;
  html+='</tbody></table>';
  document.getElementById('simTableContainer').innerHTML=html;
}

function switchScenario(key, btn) {
  document.querySelectorAll('.toggle-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  renderSim(key);
}

renderSim('base');
</script>

<!-- ══════════════════════════════════════════
     ETF FRAMEWORK
══════════════════════════════════════════ -->

<div style="max-width:900px;margin:0 auto;padding:0 clamp(16px,5vw,48px);">

<div id="etf-framework" style="margin-top:60px;">
  <div class="chapter-rule-full"><span class="crl">Part Seven — ETF Universe &amp; Framework</span></div>

  <div style="display:flex;align-items:center;gap:14px;margin:0 0 8px;">
    <div style="flex:0 0 30px;height:2px;background:var(--gold);"></div>
    <span style="font-family:'IBM Plex Mono',monospace;font-size:10px;letter-spacing:3px;color:var(--gold);text-transform:uppercase;">60+ ETFs Analysed</span>
  </div>
  <h2 style="font-family:'Playfair Display',serif;font-size:clamp(1.3rem,3.5vw,1.9rem);font-weight:700;margin-bottom:8px;">ETF Selection Framework</h2>
  <p style="font-size:13px;color:var(--muted);margin-bottom:20px;max-width:700px;line-height:1.8;">TSX-listed ETFs across four sleeves (Canada, US, EAFE, EM) scored separately for TFSA Phase 1 and non-registered Phase 2. Selection criteria are nearly inverted on yield and withholding tax between the two accounts.</p>

  <div class="alert-box"><strong>⚠️ AI Bubble Warning — March 2026:</strong> Standard MSCI Quality ETFs (ZUQ, XQLT) and market-cap-weight products (XUU) carry Nvidia at 5–6.4% weight with tech at 30–34%. Our portfolios use min-vol ETFs where the MSCI optimizer structurally caps volatile AI names. ZUQ/XQLT become excellent rotation targets when Nvidia P/E falls below 30×.</div>

  <div style="background:white;border:1px solid #d4ccb8;border-top:3px solid var(--gold);padding:clamp(16px,3vw,28px);margin-bottom:20px;">
    <span style="font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:2.5px;text-transform:uppercase;color:#9a9080;">Factor Strategy Assessment</span>
    <h3 style="font-family:'Playfair Display',serif;font-size:clamp(.95rem,2.5vw,1.15rem);font-weight:700;margin:6px 0 14px;">Which Factor Strategies Suit the Smith Maneuver?</h3>
    <div class="table-scroll">
    <table class="main-tbl">
      <thead><tr><th>Factor</th><th>Phase 2 Non-Reg SM</th><th>Phase 1 TFSA</th><th>Key Characteristic</th></tr></thead>
      <tbody>
        <tr class="win"><td><span class="b b-lv">Min Volatility</span></td><td class="g">★★★★★</td><td class="g">★★★★★</td><td>MSCI optimizer caps volatile AI names. Beta 0.57–0.70. Best bubble defence. ZLB, XMU, XMI, XMM.</td></tr>
        <tr class="win"><td><span class="b b-q">Quality</span></td><td class="g">★★★★★</td><td class="g">★★★★★</td><td>High ROE, low leverage, earnings stability. Genuine income. Lower drawdowns. XDIV, FCCQ, ZUQ (post-bubble).</td></tr>
        <tr><td><span class="b b-dg">Dividend Growth</span></td><td class="g">★★★★☆</td><td class="a">★★★☆☆</td><td>Durable compounders. Low yield = TFSA-efficient. VGG has Broadcom AI issue currently.</td></tr>
        <tr><td><span class="b b-hd">High Dividend</span></td><td class="g">★★★★★</td><td class="r">★★☆☆☆</td><td>Ideal for SM income / deductibility. High yield = WHT permanently lost in TFSA.</td></tr>
        <tr class="caution"><td>Momentum</td><td class="r">★☆☆☆☆</td><td class="r">★☆☆☆☆</td><td>Worst fit: crashes harder, high turnover, tax-inefficient, ROC risk. Avoid entirely.</td></tr>
      </tbody>
    </table>
    </div>
  </div>

  <div style="background:white;border:1px solid #d4ccb8;border-top:3px solid var(--rust);padding:clamp(16px,3vw,28px);margin-bottom:20px;">
    <span style="font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:2.5px;text-transform:uppercase;color:#9a9080;">AI Bubble Audit · March 2026</span>
    <h3 style="font-family:'Playfair Display',serif;font-size:clamp(.95rem,2.5vw,1.15rem);font-weight:700;margin:6px 0 14px;">Nvidia &amp; AI Exposure by ETF</h3>
    <div class="table-scroll">
    <table class="main-tbl">
      <thead><tr><th>ETF</th><th>Tech Wt.</th><th>Nvidia</th><th>Broadcom</th><th>Risk Level</th><th>Verdict</th></tr></thead>
      <tbody>
        <tr class="caution"><td><span class="tick">XUU / ZUQ</span></td><td class="r">32–34%</td><td class="r">5.5–6.4%</td><td class="r">3–5%</td><td><span class="b b-warn">Critical</span></td><td>Avoid now. Post-bubble rotation target.</td></tr>
        <tr class="caution"><td><span class="tick">VGG</span></td><td class="a">27.8%</td><td class="g">~1%</td><td class="r">6.2%</td><td><span class="b b-warn">Moderate</span></td><td>Broadcom = AI semiconductor proxy. Post-bubble target.</td></tr>
        <tr class="win"><td><span class="tick">XMU ★</span></td><td class="g">~15%</td><td class="g">1.4%</td><td class="g">—</td><td><span class="b b-ok">Low</span></td><td>Primary US pick. JNJ/XOM/MRK lead. Structural AI cap.</td></tr>
        <tr class="win"><td><span class="tick">ZLB / XDIV ★</span></td><td class="g">~2–3%</td><td class="g">0%</td><td class="g">0%</td><td><span class="b b-win">Minimal</span></td><td>Canadian equity. Zero tech/AI. Best SM non-reg anchors.</td></tr>
        <tr class="win"><td><span class="tick">XMI / VIDY ★</span></td><td class="g">~5–12%</td><td class="g">~0.2%</td><td class="g">0%</td><td><span class="b b-ok">Low</span></td><td>EAFE. European/Japan defensive stocks dominate.</td></tr>
        <tr class="win"><td><span class="tick">XMM ★</span></td><td class="a">~20%</td><td class="g">0%</td><td class="g">0%</td><td><span class="b b-ok">Low-Mod</span></td><td>EM min-vol. TSMC/Samsung muted by optimizer. India-heavy.</td></tr>
      </tbody>
    </table>
    </div>
  </div>

  <div style="background:white;border:1px solid #d4ccb8;border-top:3px solid var(--teal);padding:clamp(16px,3vw,28px);margin-bottom:20px;">
    <span style="font-family:'IBM Plex Mono',monospace;font-size:9px;letter-spacing:2.5px;text-transform:uppercase;color:#9a9080;">All Candidates · TSX-Listed</span>
    <h3 style="font-family:'Playfair Display',serif;font-size:clamp(.95rem,2.5vw,1.15rem);font-weight:700;margin:6px 0 14px;">Key ETF Statistics</h3>
    <div class="table-scroll">
    <table class="main-tbl">
      <thead><tr><th>Ticker</th><th>Market</th><th>Strategy</th><th>MER</th><th>Yield</th><th>Beta</th><th>AUM</th><th>Best For</th></tr></thead>
      <tbody>
        <tr class="win"><td><span class="tick">ZLB</span><span class="tick-sub">BMO</span></td><td>🇨🇦 Canada</td><td><span class="b b-lv">LV</span></td><td class="g">0.40%</td><td class="mn">1.9%</td><td class="g">0.57</td><td>$2.4B</td><td>Phase 1 TFSA anchor. Best CDN beta.</td></tr>
        <tr class="win"><td><span class="tick">XDIV</span><span class="tick-sub">iShares</span></td><td>🇨🇦 Canada</td><td><span class="b b-q">Quality</span></td><td class="g">0.10%</td><td class="g">3.7%</td><td class="a">0.80</td><td>$2.2B</td><td>Both phases. Ultra-low MER, monthly eligible divs.</td></tr>
        <tr class="win"><td><span class="tick">VDY</span><span class="tick-sub">Vanguard</span></td><td>🇨🇦 Canada</td><td><span class="b b-hd">Hi Div</span></td><td class="g">0.22%</td><td class="g">3.56%</td><td class="a">0.85</td><td>$6.65B</td><td>Phase 2 non-reg anchor. Largest CDN div ETF.</td></tr>
        <tr><td><span class="tick">FCCQ</span><span class="tick-sub">Fidelity</span></td><td>🇨🇦 Canada</td><td><span class="b b-q">Quality</span></td><td class="g">0.39%</td><td class="mn">1.8%</td><td class="a">0.75</td><td>$400M</td><td>Phase 1 5th-ETF option. Quality CDN growth.</td></tr>
        <tr><td><span class="tick">XMV</span><span class="tick-sub">iShares</span></td><td>🇨🇦 Canada</td><td><span class="b b-lv">LV</span></td><td class="g">0.33%</td><td class="mn">2.2%</td><td class="g">0.68</td><td>$900M</td><td>Alt to ZLB — cheaper MER, MSCI methodology.</td></tr>
        <tr class="win"><td><span class="tick">XMU</span><span class="tick-sub">iShares</span></td><td>🇺🇸 US</td><td><span class="b b-lv">LV</span></td><td class="g">0.20%</td><td class="g">1.3%</td><td class="g">0.65</td><td>$1.8B</td><td>Phase 1 US anchor. Lowest MER, best bubble defence.</td></tr>
        <tr><td><span class="tick">VGG</span><span class="tick-sub">Vanguard</span></td><td>🇺🇸 US</td><td><span class="b b-dg">Div Gr.</span></td><td class="a">0.30%</td><td class="g">1.14%</td><td class="a">0.85</td><td>$2.33B</td><td>Post-bubble rotation. Low WHT drag in TFSA.</td></tr>
        <tr class="caution"><td><span class="tick">ZUQ</span><span class="tick-sub">BMO</span></td><td>🇺🇸 US</td><td><span class="b b-q">Quality</span></td><td class="a">0.33%</td><td class="r">0.45%</td><td class="a">0.90</td><td>$3.2B</td><td>Post-bubble target. Nvidia 6.4% now. Excellent quality screen.</td></tr>
        <tr class="win"><td><span class="tick">XMI</span><span class="tick-sub">iShares</span></td><td>🌐 EAFE</td><td><span class="b b-lv">LV</span></td><td class="a">0.33%</td><td class="a">2.64%</td><td class="g">0.63</td><td>$170M</td><td>Both phases. Lowest beta EAFE. WHT-efficient.</td></tr>
        <tr class="win"><td><span class="tick">VIDY</span><span class="tick-sub">Vanguard</span></td><td>🌐 EAFE</td><td><span class="b b-hd">Hi Div</span></td><td class="g">0.32%</td><td class="r">~4.8%</td><td class="a">0.80</td><td>$713M</td><td>Phase 2 non-reg only. WHT too costly in TFSA.</td></tr>
        <tr><td><span class="tick">ZIQ</span><span class="tick-sub">BMO</span></td><td>🌐 EAFE</td><td><span class="b b-q">Quality</span></td><td class="a">0.35%</td><td class="g">1.8%</td><td class="a">0.78</td><td>$250M</td><td>TFSA rotation target. Low WHT, quality tilt.</td></tr>
        <tr class="win"><td><span class="tick">XMM</span><span class="tick-sub">iShares</span></td><td>🌏 EM</td><td><span class="b b-lv">LV</span></td><td class="a">0.39%</td><td class="g">2.0%</td><td class="a">~0.70</td><td class="a">$96M ⚠</td><td>Both phases. Only EM LV on TSX. Watch AUM.</td></tr>
        <tr><td><span class="tick">VEE</span><span class="tick-sub">Vanguard</span></td><td>🌏 EM</td><td>Base</td><td class="g">0.25%</td><td class="a">2.5%</td><td class="mn">—</td><td>$1.9B</td><td>XMM fallback if AUM drops below $50M.</td></tr>
      </tbody>
    </table>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════
     PHASE 1 PORTFOLIO
══════════════════════════════════════════ -->

<div id="phase1-port" style="margin-top:60px;">
  <div class="chapter-rule-full"><span class="crl">Part Eight — Phase 1 TFSA Portfolio</span></div>

  <div style="display:flex;align-items:center;gap:14px;margin:0 0 8px;">
    <div style="flex:0 0 30px;height:2px;background:var(--gold);"></div>
    <span style="font-family:'IBM Plex Mono',monospace;font-size:10px;letter-spacing:3px;color:var(--gold);text-transform:uppercase;">TFSA Growth</span>
  </div>
  <h2 style="font-family:'Playfair Display',serif;font-size:clamp(1.3rem,3.5vw,1.9rem);font-weight:700;margin-bottom:8px;">Phase 1 — TFSA HELOC Growth Portfolio</h2>
  <p style="font-size:13px;color:var(--muted);margin-bottom:20px;max-width:700px;line-height:1.8;">Mandate: HELOC → TFSA. No interest deduction (accepted). Maximise tax-free compounding. Minimise WHT leakage. Prioritise bubble defence. Target: 4–5 ETFs, blended beta ~0.65, minimal Nvidia/AI exposure.</p>

  <div class="inv-grid">
    <div class="inv-col old">
      <h3>Phase 2 Non-Reg Scoring</h3>
      <div class="inv-row"><span class="inv-ll">High yield</span><span class="inv-vv g">✓ SM deductibility + dividend tax credit</span></div>
      <div class="inv-row"><span class="inv-ll">Foreign WHT</span><span class="inv-vv g">✓ Partially recovered via T1 Line 40500</span></div>
      <div class="inv-row"><span class="inv-ll">VIDY (4.8% yield)</span><span class="inv-vv g">✓ Income offsets HELOC carry cost</span></div>
      <div class="inv-row"><span class="inv-ll">XMU (1.3% yield)</span><span class="inv-vv r">✗ Insufficient for SM deductibility</span></div>
      <div class="inv-row"><span class="inv-ll">Capital gains</span><span class="inv-vv r">⚠ 50% inclusion — taxable</span></div>
    </div>
    <div class="inv-col new">
      <h3>Phase 1 TFSA Scoring</h3>
      <div class="inv-row"><span class="inv-ll">High yield</span><span class="inv-vv r">✗ Creates unnecessary distribution drag</span></div>
      <div class="inv-row"><span class="inv-ll">Foreign WHT</span><span class="inv-vv r">✗ Permanently lost — no recovery mechanism</span></div>
      <div class="inv-row"><span class="inv-ll">VIDY (4.8% yield)</span><span class="inv-vv r">✗ ~$750/yr lost per $100K in WHT</span></div>
      <div class="inv-row"><span class="inv-ll">XMU (1.3% yield)</span><span class="inv-vv g">✓ Minimal WHT leakage, max compounding</span></div>
      <div class="inv-row"><span class="inv-ll">Capital gains</span><span class="inv-vv g">✓ Tax-free forever in TFSA</span></div>
    </div>
  </div>

  <div class="port-sum">
    <div class="ps-cell"><div class="ps-lbl">Blended MER</div><div class="ps-val g">0.32%</div></div>
    <div class="ps-cell"><div class="ps-lbl">Blended Yield</div><div class="ps-val g">1.75%</div></div>
    <div class="ps-cell"><div class="ps-lbl">TFSA WHT Drag</div><div class="ps-val g">~0.57%/yr</div></div>
    <div class="ps-cell"><div class="ps-lbl">Blended Beta</div><div class="ps-val g">~0.65</div></div>
    <div class="ps-cell"><div class="ps-lbl">Nvidia Weight</div><div class="ps-val g">~0.5%</div></div>
    <div class="ps-cell"><div class="ps-lbl">Tech Weight</div><div class="ps-val g">~14%</div></div>
  </div>

  <div class="port-grid">
    <div class="pcrd ca">
      <div class="pcrd-ticker">ZLB</div>
      <div class="pcrd-sub">BMO Low Vol CDN · 🇨🇦</div>
      <div class="pcrd-wt">25%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val g">0.40%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">1.9%</span></div>
        <div class="pstat"><span class="lbl">Beta</span><span class="val g">0.57</span></div>
        <div class="pstat"><span class="lbl">WHT/TFSA</span><span class="val g">0%</span></div>
        <div class="pstat"><span class="lbl">Tech Wt.</span><span class="val g">~3%</span></div>
        <div class="pstat"><span class="lbl">Nvidia</span><span class="val g">0%</span></div>
      </div>
    </div>
    <div class="pcrd us">
      <div class="pcrd-ticker">XMU</div>
      <div class="pcrd-sub">iShares MSCI Min Vol USA · 🇺🇸</div>
      <div class="pcrd-wt">35%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val g">0.20%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">1.3%</span></div>
        <div class="pstat"><span class="lbl">Beta</span><span class="val g">0.65</span></div>
        <div class="pstat"><span class="lbl">WHT/TFSA</span><span class="val a">~0.20%/yr</span></div>
        <div class="pstat"><span class="lbl">Tech Wt.</span><span class="val g">~15%</span></div>
        <div class="pstat"><span class="lbl">Nvidia</span><span class="val g">1.4%</span></div>
      </div>
    </div>
    <div class="pcrd eafe">
      <div class="pcrd-ticker">XMI</div>
      <div class="pcrd-sub">iShares MSCI EAFE Min Vol · 🌐</div>
      <div class="pcrd-wt">25%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val a">0.33%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val a">2.64%</span></div>
        <div class="pstat"><span class="lbl">Beta</span><span class="val g">0.63</span></div>
        <div class="pstat"><span class="lbl">WHT/TFSA</span><span class="val a">~0.40%/yr</span></div>
        <div class="pstat"><span class="lbl">Tech Wt.</span><span class="val g">~12%</span></div>
        <div class="pstat"><span class="lbl">Nvidia</span><span class="val g">~0.2%</span></div>
      </div>
    </div>
    <div class="pcrd em">
      <div class="pcrd-ticker">XMM</div>
      <div class="pcrd-sub">iShares MSCI EM Min Vol · 🌏</div>
      <div class="pcrd-wt">15%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val a">0.39%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">2.0%</span></div>
        <div class="pstat"><span class="lbl">Beta (est.)</span><span class="val a">~0.70</span></div>
        <div class="pstat"><span class="lbl">WHT/TFSA</span><span class="val a">~0.38%/yr</span></div>
        <div class="pstat"><span class="lbl">AUM ⚠</span><span class="val a">$96M</span></div>
        <div class="pstat"><span class="lbl">India Wt.</span><span class="val g">~25%</span></div>
      </div>
    </div>
  </div>

  <div class="cmp-grid">
    <div class="cmp-box">
      <h4>4-ETF Core (Recommended)</h4>
      <ul>
        <li><span>ZLB — Canada Low Vol</span><span>25%</span></li>
        <li><span>XMU — US Min Vol</span><span>35%</span></li>
        <li><span>XMI — EAFE Min Vol</span><span>25%</span></li>
        <li><span>XMM — EM Min Vol</span><span>15%</span></li>
        <li><span style="font-style:italic;color:var(--muted)">Blended Beta</span><span>~0.65</span></li>
        <li><span style="font-style:italic;color:var(--muted)">Blended MER</span><span>0.32%</span></li>
      </ul>
    </div>
    <div class="cmp-box">
      <h4>5-ETF Variant (+ Quality CDN)</h4>
      <ul>
        <li><span>ZLB — Canada Low Vol</span><span>15%</span></li>
        <li><span>FCCQ — Canada Quality</span><span>10%</span></li>
        <li><span>XMU — US Min Vol</span><span>35%</span></li>
        <li><span>XMI — EAFE Min Vol</span><span>25%</span></li>
        <li><span>XMM — EM Min Vol</span><span>15%</span></li>
        <li><span style="font-style:italic;color:var(--muted)">Blended Beta</span><span>~0.66</span></li>
      </ul>
    </div>
  </div>

  <div class="wht-grid">
    <div class="wht-cell">
      <h5>VIDY — EAFE Hi Div</h5>
      <div class="wht-amt" style="color:var(--rust);">−$750/yr</div>
      <div class="wht-note">Per $100K invested. WHT permanently lost in TFSA. Non-reg only.</div>
    </div>
    <div class="wht-cell">
      <h5>XMI — EAFE Min Vol</h5>
      <div class="wht-amt" style="color:#7a5500;">−$400/yr</div>
      <div class="wht-note">Per $100K. Acceptable — low yield limits leakage. Core TFSA holding.</div>
    </div>
    <div class="wht-cell">
      <h5>XMM — EM Min Vol</h5>
      <div class="wht-amt" style="color:#7a5500;">−$380/yr</div>
      <div class="wht-note">Per $100K. Acceptable — only EM min-vol option on TSX.</div>
    </div>
    <div class="wht-cell">
      <h5>XMU — US Min Vol</h5>
      <div class="wht-amt" style="color:#1a4a2e;">−$200/yr</div>
      <div class="wht-note">Per $100K. Best US option — low yield, low leakage. TFSA-efficient.</div>
    </div>
    <div class="wht-cell">
      <h5>ZLB / XDIV</h5>
      <div class="wht-amt" style="color:#1a4a2e;">$0/yr</div>
      <div class="wht-note">Canadian equity. No withholding tax. Best TFSA efficiency.</div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════
     PHASE 2 PORTFOLIO
══════════════════════════════════════════ -->

<div id="phase2-port" style="margin-top:60px;">
  <div class="chapter-rule-full"><span class="crl">Part Nine — Phase 2 Non-Registered SM Portfolio</span></div>

  <div style="display:flex;align-items:center;gap:14px;margin:0 0 8px;">
    <div style="flex:0 0 30px;height:2px;background:var(--gold);"></div>
    <span style="font-family:'IBM Plex Mono',monospace;font-size:10px;letter-spacing:3px;color:var(--gold);text-transform:uppercase;">SM Proper</span>
  </div>
  <h2 style="font-family:'Playfair Display',serif;font-size:clamp(1.3rem,3.5vw,1.9rem);font-weight:700;margin-bottom:8px;">Phase 2 — Non-Registered Smith Maneuver</h2>
  <p style="font-size:13px;color:var(--muted);margin-bottom:20px;max-width:700px;line-height:1.8;">CRA deductibility applies. Investments must produce income. Canadian eligible dividends preferred (dividend tax credit reduces effective tax to ~22–25%). Foreign WHT now recoverable via T1 Line 40500 / T2209.</p>

  <div style="background:#fff5ec;border-left:4px solid var(--rust);padding:14px 18px;margin-bottom:18px;font-size:13px;line-height:1.75;color:#2c1a00;">
    <strong>CRA Compliance Checklist:</strong> (1) HELOC flows directly to non-registered brokerage — never to TFSA/RRSP. (2) All investments produce income (dividends, interest). (3) No ROC distributions — erodes ACB and jeopardises deductibility. (4) Dedicated HELOC account, zero personal use. (5) Annual Schedule 4 / Line 22100 with T5 slips and HELOC interest statement.
  </div>

  <div class="port-sum">
    <div class="ps-cell"><div class="ps-lbl">Blended MER</div><div class="ps-val g">0.26%</div></div>
    <div class="ps-cell"><div class="ps-lbl">Blended Yield</div><div class="ps-val g">~3.8%</div></div>
    <div class="ps-cell"><div class="ps-lbl">CDN Eligible Divs</div><div class="ps-val g">~65%</div></div>
    <div class="ps-cell"><div class="ps-lbl">SM Compliant</div><div class="ps-val g">100%</div></div>
    <div class="ps-cell"><div class="ps-lbl">ROC Risk</div><div class="ps-val g">Zero</div></div>
  </div>

  <div class="port-grid">
    <div class="pcrd ca">
      <div class="pcrd-ticker">VDY</div>
      <div class="pcrd-sub">Vanguard FTSE CDN Hi Div · 🇨🇦</div>
      <div class="pcrd-wt">40%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val g">0.22%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">3.56%</span></div>
        <div class="pstat"><span class="lbl">AUM</span><span class="val g">$6.65B</span></div>
        <div class="pstat"><span class="lbl">Div Type</span><span class="val g">Eligible ✓</span></div>
        <div class="pstat"><span class="lbl">Frequency</span><span class="val g">Monthly</span></div>
        <div class="pstat"><span class="lbl">AI Exposure</span><span class="val g">~0%</span></div>
      </div>
    </div>
    <div class="pcrd ca">
      <div class="pcrd-ticker">XDIV</div>
      <div class="pcrd-sub">iShares CDN Quality Div · 🇨🇦</div>
      <div class="pcrd-wt">25%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val g">0.10%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">3.7%</span></div>
        <div class="pstat"><span class="lbl">Holdings</span><span class="val g">~25</span></div>
        <div class="pstat"><span class="lbl">Div Type</span><span class="val g">Eligible ✓</span></div>
        <div class="pstat"><span class="lbl">Frequency</span><span class="val g">Monthly</span></div>
        <div class="pstat"><span class="lbl">AI Exposure</span><span class="val g">~2%</span></div>
      </div>
    </div>
    <div class="pcrd eafe">
      <div class="pcrd-ticker">VIDY</div>
      <div class="pcrd-sub">Vanguard Dev ex-NA Hi Div · 🌐</div>
      <div class="pcrd-wt">25%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val g">0.32%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val a">~4.8%</span></div>
        <div class="pstat"><span class="lbl">AUM</span><span class="val g">$713M</span></div>
        <div class="pstat"><span class="lbl">Holdings</span><span class="val g">642</span></div>
        <div class="pstat"><span class="lbl">WHT Recovery</span><span class="val a">~60–70%</span></div>
        <div class="pstat"><span class="lbl">Non-Reg Only</span><span class="val a">⚠ Yes</span></div>
      </div>
    </div>
    <div class="pcrd em">
      <div class="pcrd-ticker">XMM</div>
      <div class="pcrd-sub">iShares MSCI EM Min Vol · 🌏</div>
      <div class="pcrd-wt">10%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val a">0.39%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">2.0%</span></div>
        <div class="pstat"><span class="lbl">Beta</span><span class="val g">~0.70</span></div>
        <div class="pstat"><span class="lbl">AUM ⚠</span><span class="val a">$96M</span></div>
        <div class="pstat"><span class="lbl">India Wt.</span><span class="val g">~25%</span></div>
        <div class="pstat"><span class="lbl">AI Exposure</span><span class="val g">Low</span></div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════
     ROADMAP
══════════════════════════════════════════ -->

<div id="roadmap" style="margin-top:60px;">
  <div class="chapter-rule-full"><span class="crl">Part Ten — Quantitative Transition Roadmap</span></div>

  <div style="display:flex;align-items:center;gap:14px;margin:0 0 8px;">
    <div style="flex:0 0 30px;height:2px;background:var(--gold);"></div>
    <span style="font-family:'IBM Plex Mono',monospace;font-size:10px;letter-spacing:3px;color:var(--gold);text-transform:uppercase;">Forward Plan</span>
  </div>
  <h2 style="font-family:'Playfair Display',serif;font-size:clamp(1.3rem,3.5vw,1.9rem);font-weight:700;margin-bottom:8px;">Strategy Roadmap — 7 Stages</h2>
  <p style="font-size:13px;color:var(--muted);margin-bottom:28px;max-width:700px;line-height:1.8;">Each stage has a quantitative trigger — not gut-feel timing. Integrates Phase 1 TFSA growth, AI bubble rotation, Phase 2 SM, and long-term wealth extraction.</p>

  <div class="tl-item">
    <div class="tl-dot on">1</div>
    <div class="tl-body">
      <h4>Now — Phase 1 TFSA: Defensive Min-Vol</h4>
      <p>HELOC → TFSA. Portfolio: ZLB 25% + XMU 35% + XMI 25% + XMM 15%. Beta ~0.65. Nvidia ~0.5%. No SM deduction — accepted cost of TFSA compounding. Goal: fill TFSA room and survive AI correction.</p>
      <span class="tl-trig">Active while: Nvidia P/E &gt; 40× OR S&amp;P 500 tech weight &gt; 28%</span>
    </div>
  </div>
  <div class="tl-item">
    <div class="tl-dot off">2</div>
    <div class="tl-body">
      <h4>Trigger A — Rotate XMU → partial ZUQ / XQLT</h4>
      <p>When AI valuations normalise, rotate a portion of XMU into ZUQ (sector-neutral quality, 0.33% MER). ZUQ's quality screen — high ROE, low debt — outperforms in recoveries. Keep XMU as defensive core.</p>
      <span class="tl-trig">Trigger: Nvidia P/E &lt; 30× AND S&amp;P 500 tech weight &lt; 25%</span>
    </div>
  </div>
  <div class="tl-item">
    <div class="tl-dot off">3</div>
    <div class="tl-body">
      <h4>Trigger B — Add VGG (Dividend Growth) to TFSA</h4>
      <p>VGG's 1.14% yield is highly TFSA-efficient once Broadcom normalises. 10+ year dividend growth screen captures durable compounders. Low WHT drag in TFSA relative to high-yield alternatives.</p>
      <span class="tl-trig">Trigger: Broadcom AI revenue growth &lt; 20% YoY AND Broadcom P/E &lt; 25×</span>
    </div>
  </div>
  <div class="tl-item">
    <div class="tl-dot off">4</div>
    <div class="tl-body">
      <h4>Trigger C — Add ZIQ alongside XMI (EAFE Quality)</h4>
      <p>ZIQ (MSCI EAFE Quality, launched Oct 2024) at 10–12% alongside XMI at 12–15%. ZIQ captures recovery upside; XMI provides vol defence. Together they provide full-cycle EAFE coverage.</p>
      <span class="tl-trig">Trigger: ZIQ AUM &gt; $400M AND 2-year track record established</span>
    </div>
  </div>
  <div class="tl-item">
    <div class="tl-dot off">5</div>
    <div class="tl-body">
      <h4>Phase 2 — TFSA Maxed: Switch to Non-Reg SM</h4>
      <p>New HELOC deployments shift to non-registered. Criteria flip: CRA deductibility requires income. Switch to VDY 40% + XDIV 25% + VIDY 25% + XMM 10%. TFSA portfolio continues compounding — never liquidate.</p>
      <span class="tl-trig">Trigger: TFSA contribution room fully deployed</span>
    </div>
  </div>
  <div class="tl-item">
    <div class="tl-dot off">6</div>
    <div class="tl-body">
      <h4>SM Running — Annual Refund Loop</h4>
      <p>Each year: HELOC interest accrues → 45% MTR refund → lump sum to mortgage principal → more equity → more HELOC room → more investment. At $300K HELOC × 6.5%: ~$3,950 refund recycled annually.</p>
      <span class="tl-trig">Ongoing: File Schedule 4 / Line 22100 each spring with T5 slips.</span>
    </div>
  </div>
  <div class="tl-item">
    <div class="tl-dot off">7</div>
    <div class="tl-body">
      <h4>End State — Full Debt Conversion &amp; Wealth Extraction</h4>
      <p>Mortgage fully paid (~20–25 years). HELOC balance = original mortgage amount, all deductible. Three exits: (A) Hold portfolio, live on dividends. (B) Sell portfolio, pay off HELOC entirely. (C) Partial paydown, keep income core. TFSA withdrawals are tax-free forever.</p>
      <span class="tl-trig">Trigger: SM mortgage conversion &gt; 80% AND HELOC balance declining</span>
    </div>
  </div>

  <p style="font-size:11px;color:var(--muted);border-top:1px solid #ccc;padding-top:12px;margin-top:32px;line-height:1.85;">
    All ETF data March 2026. MERs from provider factsheets. Yields trailing 12-month. Beta vs MSCI World or relevant benchmark. Dot-com recovery (−47%, ~40 months) confirmed by Walter Scott Global Equity. GFC (−54–58%, 53–64 months). COVID (−34%, ~9 months) confirmed multiple sources. MSCI World 50-yr CAGR ~9.3% (1975–2024 incl. backtested pre-1986 data); actual 1986–2025 ≈ 8.9%. Annual σ ≈ 15%. Simulation: $500K home, $300K mortgage, 6.5% HELOC, 45% MTR. Not investment, tax, or legal advice. Consult a fee-only CFP and CPA before implementing any leveraged strategy. HELOC interest is not deductible when invested in a TFSA under current CRA rules.
  </p>
</div>

</div><!-- close wrapper div -->

</body>
</html>
