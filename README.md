<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Smith Maneuver — Complete Strategy Guide</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/mermaid/10.6.1/mermaid.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=IBM+Plex+Mono:wght@400;500;600&family=IBM+Plex+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root {
  --ink:#0e1117; --ink-mid:#1c2430; --paper:#f5f0e8; --cream:#ede8da; --cream-dk:#e0dace;
  --gold:#c9a84c; --gold-lt:#e8c96a; --gold-pale:#f5e9c4;
  --teal:#1a6b5e; --teal-lt:#2a9d8f;
  --rust:#c94c1a; --navy:#0f2a4a; --forest:#1a4a2e;
  --slate:#2c3e50; --muted:#7a7060; --muted-lt:#9a9080;
  --rule:#c4bba8; --border:#d4ccb8;
  --green:#1a4a2e; --amber:#7a5500; --red:#8b2500;
}
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{background:var(--paper);color:var(--ink);font-family:'IBM Plex Sans',sans-serif;font-weight:300;font-size:14px;line-height:1.65;}

/* MASTHEAD */
.masthead{background:var(–ink);color:var(–paper);padding:clamp(36px,6vw,72px) clamp(20px,5vw,60px) clamp(28px,5vw,52px);border-bottom:4px solid var(–gold);position:relative;overflow:hidden;}
.masthead::before{content:’’;position:absolute;top:0;right:0;width:min(400px,60vw);height:100%;background:repeating-linear-gradient(45deg,transparent,transparent 18px,rgba(201,168,76,.05) 18px,rgba(201,168,76,.05) 19px);pointer-events:none;}
.mast-eye{font-family:‘IBM Plex Mono’,monospace;font-size:clamp(9px,1.8vw,11px);letter-spacing:4px;text-transform:uppercase;color:var(–gold);margin-bottom:14px;}
.mast-title{font-family:‘Playfair Display’,serif;font-size:clamp(1.8rem,6vw,4rem);font-weight:900;line-height:1.05;letter-spacing:-.02em;}
.mast-title em{color:var(–gold);font-style:italic;}
.mast-sub{margin-top:14px;font-size:clamp(12px,2vw,14px);color:#a09880;max-width:580px;line-height:1.8;}
.mast-hr{border:none;border-top:1px solid #2a2a2a;margin:22px 0 16px;}
.mast-meta{display:flex;flex-wrap:wrap;gap:clamp(14px,4vw,40px);}
.meta-item{display:flex;flex-direction:column;gap:3px;}
.meta-lbl{font-family:‘IBM Plex Mono’,monospace;font-size:9px;letter-spacing:3px;text-transform:uppercase;color:#4a4030;}
.meta-val{font-size:12px;color:#c4bba8;}

/* STAT STRIP */
.stat-strip{background:var(–ink-mid);border-bottom:1px solid #2a3545;padding:clamp(14px,2.5vw,22px) clamp(20px,5vw,60px);display:flex;flex-wrap:wrap;gap:clamp(20px,5vw,56px);}
.stat-item{display:flex;flex-direction:column;gap:3px;min-width:70px;}
.stat-val{font-family:‘Playfair Display’,serif;font-size:clamp(1.3rem,3.5vw,2.2rem);font-weight:700;line-height:1;color:var(–gold);}
.stat-val.g{color:#2a9d8f;} .stat-val.r{color:var(–rust);}
.stat-lbl{font-family:‘IBM Plex Mono’,monospace;font-size:9px;letter-spacing:2px;text-transform:uppercase;color:#5a5040;}

/* NAV */
.sticky-nav{position:sticky;top:0;z-index:100;background:var(–ink);border-bottom:2px solid var(–gold);overflow-x:auto;white-space:nowrap;}
.nav-inner{max-width:1200px;margin:0 auto;display:flex;align-items:center;padding:0 12px;}
.nav-brand{font-family:‘IBM Plex Mono’,monospace;font-size:10px;letter-spacing:3px;text-transform:uppercase;color:var(–gold);padding:13px 16px 13px 4px;border-right:1px solid #2a2a2a;margin-right:4px;flex-shrink:0;}
.nav-btn{background:none;border:none;border-bottom:3px solid transparent;color:#666;font-family:‘IBM Plex Mono’,monospace;font-size:9.5px;letter-spacing:1.5px;text-transform:uppercase;padding:13px 12px 10px;cursor:pointer;transition:all .2s;white-space:nowrap;}
.nav-btn:hover{color:var(–gold-lt);}
.nav-btn.active{color:var(–gold);border-bottom-color:var(–gold);}

/* SECTIONS */
.section{display:none;}
.section.active{display:block;}
.page-wrap{max-width:1100px;margin:0 auto;padding:clamp(28px,5vw,56px) clamp(16px,4vw,40px) 80px;}

/* CHAPTER HEADERS */
.ch-head{border-top:3px double var(–ink);border-bottom:1px solid var(–ink);padding:14px 0 10px;margin-bottom:26px;}
.ch-lbl{font-family:‘IBM Plex Mono’,monospace;font-size:9px;letter-spacing:4px;text-transform:uppercase;color:var(–muted);margin-bottom:4px;}
.ch-title{font-family:‘Playfair Display’,serif;font-size:clamp(17px,3.5vw,28px);font-weight:700;line-height:1.1;}

/* DIAGRAM CARD */
.dcard{background:white;border:1px solid var(–rule);border-top:3px solid var(–teal);margin-bottom:22px;padding:clamp(16px,3.5vw,32px) clamp(14px,3.5vw,32px);box-shadow:0 2px 10px rgba(0,0,0,.05);}
.dcard.gold{border-top-color:var(–gold);}
.dcard.rust{border-top-color:var(–rust);}
.dcard-eye{font-family:‘IBM Plex Mono’,monospace;font-size:9px;letter-spacing:3px;text-transform:uppercase;color:var(–teal);margin-bottom:4px;}
.dcard.gold .dcard-eye{color:var(–gold);} .dcard.rust .dcard-eye{color:var(–rust);}
.dcard-title{font-family:‘Playfair Display’,serif;font-size:clamp(.95rem,2.5vw,1.2rem);font-weight:700;margin-bottom:6px;}
.dcard-note{font-size:12.5px;color:var(–muted);margin-bottom:16px;padding-bottom:14px;border-bottom:1px solid var(–cream);line-height:1.7;}
.diag-scroll{overflow-x:auto;-webkit-overflow-scrolling:touch;}
.diag-scroll .mermaid{display:flex;justify-content:center;min-width:440px;}

/* CHART CARD */
.ccrd{background:white;border:1px solid var(–rule);border-top:3px solid var(–teal);padding:clamp(16px,3vw,28px);margin-bottom:20px;box-shadow:0 2px 8px rgba(0,0,0,.04);}
.ccrd.gold{border-top-color:var(–gold);} .ccrd.rust{border-top-color:var(–rust);}
.ccrd-lbl{font-family:‘IBM Plex Mono’,monospace;font-size:9px;letter-spacing:2.5px;text-transform:uppercase;color:var(–muted-lt);margin-bottom:3px;}
.ccrd h3{font-family:‘Playfair Display’,serif;font-size:clamp(.95rem,2.5vw,1.15rem);font-weight:700;margin-bottom:6px;}
.ccrd-note{font-size:12.5px;color:var(–muted);margin-bottom:16px;padding-bottom:14px;border-bottom:1px solid var(–cream);line-height:1.7;}
.cw{position:relative;width:100%;}
.cw.tall{height:clamp(240px,38vw,380px);}
.cw.med{height:clamp(200px,30vw,300px);}
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:18px;}
@media(max-width:680px){.two-col{grid-template-columns:1fr;}}

/* CALLOUT */
.callout{background:var(–cream);border-left:4px solid var(–teal);padding:clamp(12px,2.5vw,16px) clamp(12px,2.5vw,22px);margin:14px 0 18px;font-size:13px;line-height:1.75;color:var(–slate);}
.callout.warn{border-left-color:var(–rust);background:#fdf0ec;}
.callout.gold{border-left-color:var(–gold);background:var(–gold-pale);}
.callout strong{font-weight:600;color:var(–ink);}
.dark-box{background:var(–ink);color:#ddd;padding:18px 22px;margin-bottom:22px;border-left:4px solid var(–gold);font-size:12.5px;line-height:1.8;}
.dark-box strong{color:var(–gold-lt);}
.dark-box ul{padding-left:18px;margin-top:8px;}
.dark-box li{margin-bottom:5px;}
.alert-box{background:#2a0a00;color:#f0c090;padding:14px 18px;margin-bottom:18px;border-left:4px solid var(–rust);font-size:12.5px;line-height:1.75;}
.alert-box strong{color:#ffb070;}
.fact-check{background:#0a1a0a;color:#a0c8a0;padding:16px 20px;margin-bottom:20px;border-left:4px solid #2a9d8f;font-size:12px;line-height:1.8;}
.fact-check strong{color:#7fba6a;}

/* TOGGLE */
.toggle-row{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:18px;}
.tbtn{padding:7px 14px;border:1px solid var(–rule);background:var(–cream);color:var(–muted);font-family:‘IBM Plex Mono’,monospace;font-size:9.5px;letter-spacing:1.5px;text-transform:uppercase;cursor:pointer;transition:all .2s;}
.tbtn.active{background:var(–ink);border-color:var(–ink);color:var(–gold);}

/* TABLES */
.tbl-scroll{overflow-x:auto;}
table.dtbl{width:100%;border-collapse:collapse;font-size:11.5px;min-width:700px;}
table.dtbl thead th{background:var(–ink);color:var(–gold-lt);font-family:‘IBM Plex Mono’,monospace;font-size:9px;letter-spacing:1.5px;text-transform:uppercase;padding:8px 10px;text-align:left;border-right:1px solid #333;white-space:nowrap;}
table.dtbl tbody td{padding:8px 10px;border-bottom:1px solid #ddd;border-right:1px solid #e8e0d0;vertical-align:middle;line-height:1.45;}
table.dtbl tbody tr:nth-child(even) td{background:#f0ebe0;}
table.dtbl tbody tr:hover td{background:#e6e0ce!important;}
table.dtbl tbody tr.win td{background:#e8f2e8!important;border-left:4px solid var(–forest);}
table.dtbl tbody tr.caution td{border-left:4px solid var(–rust);}
.tick{font-family:‘IBM Plex Mono’,monospace;font-weight:700;font-size:12.5px;display:block;}
.tick-sub{font-family:‘IBM Plex Mono’,monospace;font-size:8.5px;color:var(–muted);display:block;}
td.g{color:var(–forest);font-family:‘IBM Plex Mono’,monospace;font-weight:600;}
td.a{color:var(–amber);font-family:‘IBM Plex Mono’,monospace;font-weight:600;}
td.r{color:var(–red);font-family:‘IBM Plex Mono’,monospace;font-weight:600;}
td.mn{font-family:‘IBM Plex Mono’,monospace;font-weight:600;}

/* BADGES */
.b{display:inline-block;font-family:‘IBM Plex Mono’,monospace;font-size:8px;letter-spacing:.5px;text-transform:uppercase;padding:2px 5px;border-radius:2px;font-weight:700;white-space:nowrap;margin:1px 1px 0 0;}
.b-win{background:var(–forest);color:#fff;}
.b-ok{background:#556b2f;color:#fff;}
.b-post{background:var(–navy);color:#fff;}
.b-skip{background:#888;color:#fff;}
.b-lv{background:var(–forest);color:#fff;}
.b-q{background:var(–navy);color:#fff;}
.b-dg{background:var(–gold);color:var(–ink);}
.b-hd{background:#c04000;color:#fff;}
.b-warn{background:var(–rust);color:#fff;}

/* SIM TABLE */
.sim-tbl{width:100%;border-collapse:collapse;font-size:11px;min-width:580px;}
.sim-tbl th{font-family:‘IBM Plex Mono’,monospace;font-size:8.5px;letter-spacing:1.5px;text-transform:uppercase;color:var(–muted);padding:9px 9px;text-align:right;border-bottom:2px solid var(–cream-dk);background:var(–cream);white-space:nowrap;}
.sim-tbl th:first-child{text-align:left;}
.sim-tbl td{padding:7px 9px;border-bottom:1px solid var(–cream);text-align:right;font-family:‘IBM Plex Mono’,monospace;font-size:10.5px;}
.sim-tbl td:first-child{text-align:left;}
.sim-tbl tr.crash td{background:#fff0ec;}
.sim-tbl tr.bull td{background:#edf7ed;}
.sim-tbl td.pos{color:var(–teal);}
.sim-tbl td.neg{color:var(–rust);}
.sim-tbl td.neutral{color:var(–slate);}

/* PORTFOLIO CARDS */
.port-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:14px;margin-bottom:24px;}
.pcrd{background:white;border:1.5px solid var(–border);box-shadow:3px 3px 0 var(–border);padding:16px 18px;position:relative;overflow:hidden;}
.pcrd::before{content:’’;position:absolute;top:0;left:0;width:100%;height:4px;}
.pcrd.ca::before{background:#c04000;}
.pcrd.us::before{background:var(–navy);}
.pcrd.eafe::before{background:var(–forest);}
.pcrd.em::before{background:var(–gold);}
.pcrd-ticker{font-family:‘Playfair Display’,serif;font-size:26px;font-weight:900;line-height:1;margin-bottom:3px;}
.pcrd-sub{font-family:‘IBM Plex Mono’,monospace;font-size:8.5px;color:var(–muted);letter-spacing:1px;text-transform:uppercase;margin-bottom:10px;}
.pcrd-wt{font-family:‘IBM Plex Mono’,monospace;font-size:20px;font-weight:700;color:var(–gold);margin-bottom:8px;}
.pcrd-stats{display:grid;grid-template-columns:1fr 1fr;gap:5px;font-size:11px;}
.pstat{display:flex;flex-direction:column;}
.pstat .lbl{font-family:‘IBM Plex Mono’,monospace;font-size:8px;letter-spacing:1px;text-transform:uppercase;color:var(–muted);}
.pstat .val{font-family:‘IBM Plex Mono’,monospace;font-weight:700;font-size:12px;}
.pstat .val.g{color:var(–forest);}
.pstat .val.a{color:var(–amber);}
.pstat .val.r{color:var(–red);}

/* PORT SUMMARY */
.port-sum{display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));border:2px solid var(–ink);margin-bottom:24px;}
.ps-cell{padding:12px 14px;border-right:1px solid var(–border);}
.ps-cell:last-child{border-right:none;}
.ps-lbl{font-family:‘IBM Plex Mono’,monospace;font-size:8.5px;letter-spacing:2px;text-transform:uppercase;color:var(–muted);margin-bottom:3px;}
.ps-val{font-family:‘Playfair Display’,serif;font-size:20px;font-weight:700;}
.ps-val.g{color:var(–forest);}
.ps-val.a{color:var(–amber);}

/* TIMELINE */
.tl{margin-bottom:24px;}
.tl-item{display:flex;gap:14px;margin-bottom:0;position:relative;}
.tl-item::before{content:’’;position:absolute;left:17px;top:36px;bottom:-1px;width:2px;background:var(–border);}
.tl-item:last-child::before{display:none;}
.tl-dot{width:36px;height:36px;border-radius:50%;border:2px solid var(–ink);background:var(–paper);display:flex;align-items:center;justify-content:center;flex-shrink:0;font-family:‘IBM Plex Mono’,monospace;font-weight:700;font-size:12px;z-index:1;}
.tl-dot.active{background:var(–ink);color:var(–gold);}
.tl-dot.future{background:white;color:var(–muted);border-color:#ccc;}
.tl-body{padding:6px 0 22px;flex:1;}
.tl-body h4{font-family:‘Playfair Display’,serif;font-size:15px;margin-bottom:5px;}
.tl-body p{font-size:12px;color:var(–slate);line-height:1.7;}
.tl-trig{font-family:‘IBM Plex Mono’,monospace;font-size:10px;color:var(–muted);display:inline-block;margin-top:6px;padding:3px 8px;border:1px solid #ccc;}

/* RECOVERY CARDS */
.crash-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:16px;margin-bottom:24px;}
.crash-crd{border:1.5px solid var(–border);padding:18px 20px;background:white;}
.crash-crd h3{font-family:‘Playfair Display’,serif;font-size:17px;margin-bottom:4px;}
.crash-badge{font-family:‘IBM Plex Mono’,monospace;font-size:9px;letter-spacing:2px;text-transform:uppercase;padding:3px 8px;border-radius:2px;display:inline-block;margin-bottom:10px;}
.crash-row{display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid #eee;font-size:12px;}
.crash-row .lbl{color:var(–muted);}
.crash-row .val{font-family:‘IBM Plex Mono’,monospace;font-weight:600;}
.crash-row .val.r{color:var(–rust);}
.crash-row .val.g{color:var(–forest);}
.crash-row .val.a{color:var(–amber);}

/* YEAR TABLE */
.yr-tbl{width:100%;border-collapse:collapse;font-size:12px;min-width:420px;}
.yr-tbl th{font-family:‘IBM Plex Mono’,monospace;font-size:9px;letter-spacing:2px;text-transform:uppercase;color:var(–muted);padding:9px 10px;text-align:left;border-bottom:2px solid var(–cream-dk);background:var(–cream);}
.yr-tbl td{padding:8px 10px;border-bottom:1px solid var(–cream);vertical-align:middle;}
.yr-tbl tr:hover td{background:var(–cream);}
.pill{display:inline-block;font-family:‘IBM Plex Mono’,monospace;font-size:10px;font-weight:600;padding:2px 8px;border-radius:2px;min-width:64px;text-align:center;}
.pill.up{background:rgba(26,107,94,.15);color:#1a6b5e;}
.pill.dn{background:rgba(201,76,26,.15);color:#c94c1a;}
.mini-bar{display:inline-block;height:8px;border-radius:1px;}

/* WHT GRID */
.wht-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(190px,1fr));border:2px solid var(–ink);margin-bottom:22px;font-size:12px;}
.wht-cell{padding:13px 15px;border-right:1px solid var(–border);border-bottom:1px solid var(–border);}
.wht-cell:nth-last-child(-n+4){border-bottom:none;}
@media(max-width:800px){.wht-cell:nth-last-child(-n+4){border-bottom:1px solid var(–border);} .wht-cell:last-child{border-bottom:none;}}
.wht-cell h5{font-family:‘IBM Plex Mono’,monospace;font-size:9.5px;letter-spacing:1px;text-transform:uppercase;color:var(–muted);margin-bottom:5px;}
.wht-amt{font-family:‘Playfair Display’,serif;font-size:19px;font-weight:700;margin-bottom:3px;}
.wht-note{font-size:11px;color:var(–muted);line-height:1.6;}

/* INVERSION GRID */
.inv-grid{display:grid;grid-template-columns:1fr 1fr;margin-bottom:28px;border:2px solid var(–ink);}
@media(max-width:600px){.inv-grid{grid-template-columns:1fr;}}
.inv-col{padding:18px 20px;}
.inv-col.old{background:#1e1e1e;color:#ccc;}
.inv-col.new{background:var(–cream);}
.inv-col h3{font-family:‘Playfair Display’,serif;font-size:15px;margin-bottom:12px;padding-bottom:7px;}
.inv-col.old h3{color:#999;border-bottom:1px solid #444;}
.inv-col.new h3{color:var(–ink);border-bottom:2px solid var(–gold);}
.inv-row{display:flex;justify-content:space-between;align-items:baseline;padding:5px 0;border-bottom:1px solid rgba(255,255,255,.06);font-size:11.5px;gap:10px;}
.inv-col.new .inv-row{border-bottom-color:#e8e0d0;}
.inv-ll{color:#999;font-size:10.5px;flex-shrink:0;}
.inv-col.new .inv-ll{color:var(–muted);}
.inv-vv{font-family:‘IBM Plex Mono’,monospace;font-weight:600;font-size:11px;text-align:right;}
.inv-vv.g{color:#7fba6a;} .inv-vv.r{color:#e06060;}
.inv-col.new .inv-vv.g{color:var(–forest);} .inv-col.new .inv-vv.r{color:var(–rust);}

/* COMPARE */
.cmp-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:22px;}
@media(max-width:600px){.cmp-grid{grid-template-columns:1fr;}}
.cmp-box{padding:16px 18px;border:1.5px solid var(–border);}
.cmp-box h4{font-family:‘Playfair Display’,serif;font-size:15px;margin-bottom:12px;padding-bottom:7px;border-bottom:2px solid var(–ink);}
.cmp-box ul{list-style:none;padding:0;}
.cmp-box li{display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid #e8e0d0;font-size:12px;gap:8px;}
.cmp-box li span:first-child{color:var(–muted);}
.cmp-box li span:last-child{font-family:‘IBM Plex Mono’,monospace;font-weight:600;}

.footnote{font-size:11px;color:var(–muted);border-top:1px solid #ccc;padding-top:12px;margin-top:28px;line-height:1.85;}
hr.rule{border:none;border-top:1px solid var(–rule);margin:28px 0;}
</style>

</head>
<body>

<!-- MASTHEAD -->

<div class="masthead">
  <div style="max-width:1100px;margin:0 auto;position:relative;z-index:1;">
    <div class="mast-eye">Complete Strategy Guide · Canadian Residential Real Estate · March 2026</div>
    <h1 class="mast-title">The Smith Maneuver<br><em>From Concept to Portfolio</em></h1>
    <p class="mast-sub">A comprehensive guide covering strategy mechanics, 50-year market data, crash recovery analysis, 20-year simulation, and a complete ETF investment framework for both Phase 1 (TFSA/HELOC growth) and Phase 2 (non-registered Smith Maneuver) deployment.</p>
    <hr class="mast-hr">
    <div class="mast-meta">
      <div class="meta-item"><span class="meta-lbl">Strategy</span><span class="meta-val">Smith Maneuver — Debt Conversion</span></div>
      <div class="meta-item"><span class="meta-lbl">Market Data</span><span class="meta-val">MSCI World 1975–2024 (50 years)</span></div>
      <div class="meta-item"><span class="meta-lbl">ETFs Analysed</span><span class="meta-val">60+ TSX-listed candidates</span></div>
      <div class="meta-item"><span class="meta-lbl">Jurisdiction</span><span class="meta-val">Canada · BC Resident · ~45% MTR</span></div>
      <div class="meta-item"><span class="meta-lbl">Fact-Checked</span><span class="meta-val">March 2026</span></div>
    </div>
  </div>
</div>

<!-- STAT STRIP -->

<div class="stat-strip">
  <div class="stat-item"><div class="stat-val g">9.3%</div><div class="stat-lbl">MSCI World 50-yr CAGR¹</div></div>
  <div class="stat-item"><div class="stat-val">15%</div><div class="stat-lbl">Annual Volatility (σ)</div></div>
  <div class="stat-item"><div class="stat-val r">−58%</div><div class="stat-lbl">GFC Max Drawdown</div></div>
  <div class="stat-item"><div class="stat-val">64mo</div><div class="stat-lbl">GFC Peak→Recovery</div></div>
  <div class="stat-item"><div class="stat-val r">−34%</div><div class="stat-lbl">COVID Drawdown</div></div>
  <div class="stat-item"><div class="stat-val g">9mo</div><div class="stat-lbl">COVID Recovery Time</div></div>
  <div class="stat-item"><div class="stat-val">45%</div><div class="stat-lbl">Assumed Marginal Tax Rate</div></div>
  <div class="stat-item"><div class="stat-val g">0.32%</div><div class="stat-lbl">Blended Portfolio MER</div></div>
</div>

<!-- NAV -->

<nav class="sticky-nav">
  <div class="nav-inner">
    <div class="nav-brand">SM Guide</div>
    <button class="nav-btn active" onclick="show('overview',this)">01 · Overview</button>
    <button class="nav-btn" onclick="show('diagrams',this)">02 · Flow Diagrams</button>
    <button class="nav-btn" onclick="show('returns',this)">03 · Market Returns</button>
    <button class="nav-btn" onclick="show('crashes',this)">04 · Crash Recovery</button>
    <button class="nav-btn" onclick="show('simulation',this)">05 · 20-Yr Simulation</button>
    <button class="nav-btn" onclick="show('etfs',this)">06 · ETF Universe</button>
    <button class="nav-btn" onclick="show('phase1',this)">07 · Phase 1 TFSA</button>
    <button class="nav-btn" onclick="show('phase2',this)">08 · Phase 2 Non-Reg</button>
    <button class="nav-btn" onclick="show('roadmap',this)">09 · Roadmap</button>
  </div>
</nav>

<!-- ══════════════════════════════════════════════════════════ -->

<!-- SECTION 1: OVERVIEW                                      -->

<!-- ══════════════════════════════════════════════════════════ -->

<div id="overview" class="section active">
<div class="page-wrap">
  <div class="ch-head"><div class="ch-lbl">Section 01</div><h2 class="ch-title">What Is the Smith Maneuver?</h2></div>

  <div class="callout gold"><strong>The Smith Maneuver</strong> is a Canadian tax strategy developed by financial planner Fraser Smith. It converts non-deductible mortgage interest into deductible investment loan interest — legally, under CRA rules — while simultaneously building a long-term investment portfolio. Over 20–25 years, it can produce materially greater net wealth than simply paying down a mortgage.</div>

  <div class="two-col" style="margin-bottom:22px;">
    <div class="ccrd">
      <div class="ccrd-lbl">The Core Mechanic</div>
      <h3>How Non-Deductible Debt Becomes Good Debt</h3>
      <p style="font-size:13px;line-height:1.8;color:var(--slate);">Every mortgage payment contains a principal portion. That principal payment reduces the mortgage balance — which simultaneously increases the available room on a <strong>HELOC (Home Equity Line of Credit)</strong> attached to the same property. The Smith Maneuver draws that new HELOC room immediately and invests it in an income-producing investment in a non-registered account. Because the borrowed money is now being used to earn income, <strong>CRA's "direct use" test is satisfied</strong> and the HELOC interest becomes tax-deductible. Over time, the entire mortgage balance — originally non-deductible — is converted, dollar by dollar, into fully deductible investment debt.</p>
    </div>
    <div class="ccrd">
      <div class="ccrd-lbl">The Tax Advantage</div>
      <h3>Why the Numbers Work in Canada</h3>
      <p style="font-size:13px;line-height:1.8;color:var(--slate);">At a 45% marginal tax rate (BC resident), every dollar of HELOC interest paid generates $0.45 back as a tax refund. On a $300K HELOC at 6.5%, that's roughly $8,775/yr in interest generating a <strong>~$3,950 annual refund</strong>. That refund is applied to the mortgage as a lump-sum principal payment, which unlocks more HELOC room, which funds more investments — creating a self-reinforcing acceleration loop. The effective after-tax cost of the HELOC is approximately 3.6% at 45% MTR. As long as the investment portfolio grows at more than 3.6%/yr long-run, the strategy generates net positive wealth.</p>
    </div>
  </div>

  <div class="ch-head" style="margin-top:32px;"><div class="ch-lbl">Requirements</div><h2 class="ch-title">What You Need to Execute the Strategy</h2></div>
  <div class="tbl-scroll">
  <table class="dtbl" style="min-width:560px;">
    <thead><tr><th>Requirement</th><th>Details</th><th>Status Check</th></tr></thead>
    <tbody>
      <tr><td><strong>Readvanceable Mortgage</strong></td><td>HELOC must automatically increase as mortgage principal is paid down. Products: Manulife One, Scotia STEP, BMO Homeowner ReadiLine, TD FlexLine, RBC Homeline.</td><td class="g">Available at all Big 6</td></tr>
      <tr><td><strong>Sufficient Equity</strong></td><td>HELOC capacity = (Home Value × 80%) − Mortgage Balance. Typically need 20%+ equity to begin. OSFI B-20 limits combined LTV to 80%.</td><td class="g">Standard refi requirement</td></tr>
      <tr><td><strong>Income-Producing Investments</strong></td><td>CRA requires borrowed money to be invested in assets that produce income (dividends, interest, distributions). Pure capital gains assets (gold, crypto, non-dividend stocks) do not qualify. No ROC distributions.</td><td class="a">Investment selection critical</td></tr>
      <tr><td><strong>Dedicated HELOC Account</strong></td><td>The HELOC used for SM must be 100% dedicated to investments. Never use for personal expenses, travel, home renovations, or TFSA contributions. Commingling destroys deductibility.</td><td class="r">Discipline required</td></tr>
      <tr><td><strong>Record Keeping</strong></td><td>Track every HELOC draw, investment purchase, and interest charge. Maintain investment account statements. CRA can audit up to 6 years back. A dedicated spreadsheet or ledger is strongly recommended.</td><td class="r">Non-negotiable</td></tr>
      <tr><td><strong>Non-Registered Account</strong><br><span style="font-size:11px;color:var(--muted);">Phase 2 / SM-proper</span></td><td>Investment account must be non-registered (taxable). TFSA, RRSP, and RESP are registered accounts — interest deductibility does NOT apply when HELOC funds are invested there.</td><td class="a">Phase 2 only</td></tr>
    </tbody>
  </table>
  </div>

  <div class="callout warn"><strong>⚠️ TFSA + HELOC Clarification (Phase 1 Strategy):</strong> This guide covers a two-phase approach. In Phase 1, HELOC proceeds are invested in a TFSA for tax-free growth — interest is <em>not</em> deductible (intentionally), but all gains shelter tax-free forever. Once TFSA room is exhausted, Phase 2 switches to proper SM in a non-registered account where CRA deductibility applies. The combination of tax-free TFSA compounding (Phase 1) plus SM tax refunds (Phase 2) represents the full strategy.</div>

  <div class="ch-head" style="margin-top:32px;"><div class="ch-lbl">Economics</div><h2 class="ch-title">The Break-Even Analysis</h2></div>
  <div class="two-col">
    <div class="ccrd">
      <div class="ccrd-lbl">After-Tax Carry Cost</div>
      <h3>What the HELOC Actually Costs You</h3>
      <div style="margin-top:12px;">
        <div style="display:flex;justify-content:space-between;padding:7px 0;border-bottom:1px solid var(--cream);font-size:12.5px;"><span style="color:var(--muted);">HELOC rate (current market)</span><span style="font-family:'IBM Plex Mono',monospace;font-weight:600;">~6.0–6.5%</span></div>
        <div style="display:flex;justify-content:space-between;padding:7px 0;border-bottom:1px solid var(--cream);font-size:12.5px;"><span style="color:var(--muted);">After-tax cost @ 45% MTR</span><span style="font-family:'IBM Plex Mono',monospace;font-weight:600;color:var(--forest);">~3.3–3.6%</span></div>
        <div style="display:flex;justify-content:space-between;padding:7px 0;border-bottom:1px solid var(--cream);font-size:12.5px;"><span style="color:var(--muted);">After-tax cost @ 33% MTR</span><span style="font-family:'IBM Plex Mono',monospace;font-weight:600;color:var(--amber);">~4.0–4.4%</span></div>
        <div style="display:flex;justify-content:space-between;padding:7px 0;border-bottom:1px solid var(--cream);font-size:12.5px;"><span style="color:var(--muted);">MSCI World 50-yr CAGR</span><span style="font-family:'IBM Plex Mono',monospace;font-weight:600;color:var(--teal);">~9.3%</span></div>
        <div style="display:flex;justify-content:space-between;padding:7px 0;font-size:12.5px;"><span style="color:var(--muted);">Spread (return minus carry)</span><span style="font-family:'IBM Plex Mono',monospace;font-weight:700;color:var(--teal);">~5.7–6.0% long-run</span></div>
      </div>
    </div>
    <div class="ccrd">
      <div class="ccrd-lbl">Risk Context</div>
      <h3>What Can Go Wrong</h3>
      <p style="font-size:13px;line-height:1.8;color:var(--slate);margin-bottom:10px;">The spread is positive long-run but <strong>not guaranteed year to year</strong>. In 2008, MSCI World fell −40.7% while HELOC interest continued. A leveraged investor who panicked and sold at the bottom crystallised a catastrophic loss. Three specific risks to manage:</p>
      <ul style="font-size:12.5px;line-height:1.9;color:var(--slate);padding-left:18px;">
        <li><strong>Drawdown risk:</strong> Portfolio drops, HELOC balance unchanged. Net wealth temporarily negative.</li>
        <li><strong>Rate risk:</strong> HELOC is floating rate. A 200bp increase adds ~$2K/yr in interest per $100K HELOC.</li>
        <li><strong>Cash flow risk:</strong> HELOC interest must be paid from employment income — never from portfolio distributions. If job is lost and portfolio is down simultaneously, you may be forced to sell at the worst moment.</li>
      </ul>
    </div>
  </div>

  <div class="footnote">¹ 9.3% is the estimated MSCI World Total Return (USD) long-run CAGR for the 1975–2024 period. Note: MSCI World index was launched March 1986; pre-1986 data is backtested by MSCI. The 1986–2025 actual period shows ~8.9% CAGR. The higher figure reflects inclusion of the strong 1975–1985 period. Standard deviation ~15% confirmed by MSCI and investingintheweb.com sources. Not investment advice.</div>
</div>
</div>

<!-- ══════════════════════════════════════════════════════════ -->

<!-- SECTION 2: FLOW DIAGRAMS                                 -->

<!-- ══════════════════════════════════════════════════════════ -->

<div id="diagrams" class="section">
<div class="page-wrap">
  <div class="ch-head"><div class="ch-lbl">Section 02</div><h2 class="ch-title">Strategy Flow Diagrams</h2></div>
  <p style="font-size:13px;color:var(--muted);margin-bottom:24px;max-width:660px;line-height:1.8;">Seven diagrams illustrating the complete Smith Maneuver lifecycle: the TFSA variant flow, then the six-step classic maneuver from initial setup through end-game debt conversion.</p>

  <!-- TFSA VARIANT -->

  <div class="dcard">
    <div class="dcard-eye">Strategy A · TFSA Variant (Phase 1)</div>
    <div class="dcard-title">HELOC → TFSA — Phase 1 Growth Strategy</div>
    <div class="dcard-note">In Phase 1, HELOC proceeds go directly into a TFSA for tax-free compounding. Interest is not deductible — this is accepted in exchange for sheltering all future gains permanently. Once TFSA room is maxed, the strategy transitions to Phase 2 (classic SM in a non-registered account).</div>
    <div class="diag-scroll">
      <div class="mermaid">
flowchart TD
    A([🏠 Home with Equity]) --> B[Open HELOC\nAgainst Home Equity]
    B --> C{Draw HELOC Funds}
    C --> D[Invest in TFSA\nTax-Free Growth Account]
    D --> E[Portfolio Grows\nTax-Free: No Tax\non Gains or Withdrawals]
    E --> F[HELOC Interest\nNOT deductible ❌\nAccepted cost of TFSA shelter]
    F --> G[Pay HELOC Interest\nfrom Employment Income]
    G --> H{TFSA Room\nStatus?}
    H -->|Room Available| C
    H -->|Room Maxed| I[Switch to Phase 2:\nHELOC → Non-Registered\nSM Proper Begins ✅]
    I --> J[Now Interest IS\nDeductible ✅\nInvest in Income-Producing ETFs]
    J --> K[Annual Tax Refund\n→ Lump Sum to Mortgage]
    K --> L[More HELOC Room\n→ More Investment]
    L --> J
      </div>
    </div>
    <div class="callout warn"><strong>⚠️ CRA Rule:</strong> You cannot deduct HELOC interest when invested in a TFSA — the TFSA is a registered account and produces no taxable income. The interest deduction only applies when borrowed funds are invested in a non-registered, income-earning account (Phase 2). This strategy intentionally sacrifices the deduction in Phase 1 to benefit from permanent TFSA tax-free compounding.</div>
  </div>

  <!-- STEP 1 -->

  <div class="dcard">
    <div class="dcard-eye">Step 1 · Foundation · Classic SM</div>
    <div class="dcard-title">Setup — Readvanceable Mortgage or HELOC</div>
    <div class="dcard-note">The strategy requires a readvanceable mortgage where the HELOC limit automatically increases as mortgage principal is paid down. Available from most major Canadian lenders (Manulife One, Scotia STEP, BMO Homeowner ReadiLine, TD FlexLine).</div>
    <div class="diag-scroll">
      <div class="mermaid">
flowchart LR
    A([🏠 Home Value: $800K\nMortgage: $400K\nEquity: $400K]) --> B[Apply for\nReadvanceable Mortgage\nor HELOC]
    B --> C[Bank Approves HELOC\nup to 80% LTV\nMax HELOC: $240K\nAvailable Now: $0]
    C --> D[✅ Ready to Begin\nSmith Maneuver\nEach mortgage payment\nunlocks new HELOC room]
      </div>
    </div>
    <div class="callout"><strong>80% LTV Rule:</strong> HELOC capacity = (Home Value × 80%) − Mortgage Balance. As your mortgage shrinks with each payment, the available HELOC room grows by an equal amount — this is the mechanical engine of the Smith Maneuver. OSFI Guideline B-20 caps combined mortgage + HELOC at 80% LTV.</div>
  </div>

  <!-- STEP 2 -->

  <div class="dcard">
    <div class="dcard-eye">Step 2 · First Draw</div>
    <div class="dcard-title">First Draw &amp; Investment</div>
    <div class="dcard-note">Each mortgage payment's principal component unlocks equivalent HELOC room. That room is immediately drawn and invested in income-producing assets in a non-registered brokerage account.</div>
    <div class="diag-scroll">
      <div class="mermaid">
flowchart TD
    A[Make Regular\nMortgage Payment\ne.g. $2,000/month\n~$500 principal] --> B[Principal Reduces\nMortgage Balance\n$400,000 → $399,500]
    B --> C[HELOC Room\nOpens by Same Amount\n$500 available]
    C --> D[Draw $500\nfrom HELOC]
    D --> E[Deposit $500 into\nNon-Registered\nBrokerage Account]
    E --> F[Buy $500 of\nCanadian Dividend ETF\ne.g. XDIV, VDY]
    F --> G[✅ Investment Made\nHELOC Balance: $500\nMortgage Balance: $399,500]
      </div>
    </div>
    <div class="callout"><strong>Net effect:</strong> Total debt is unchanged ($399,500 mortgage + $500 HELOC = $400,000), but you now own $500 in investments. The critical difference: mortgage interest is non-deductible, while the HELOC interest is deductible.</div>
  </div>

  <!-- STEP 3 -->

  <div class="dcard rust">
    <div class="dcard-eye">Step 3 · Tax Mechanics</div>
    <div class="dcard-title">Interest Accrues &amp; Tax Deduction Applied</div>
    <div class="dcard-note">Tax deductibility of HELOC interest is the core economic advantage. CRA's "direct use" test under ITA Section 20(1)(c) requires meticulous record-keeping — every dollar of HELOC proceeds must be traceable to income-earning investments.</div>
    <div class="diag-scroll">
      <div class="mermaid">
flowchart TD
    A[HELOC Balance Grows\nover the Year\ne.g. $6,000 by Year-End] --> B[HELOC Interest Accrues\ne.g. 6.5% on $6,000\n= ~$390 interest/year]
    B --> C{Is Interest\nDeductible?}
    C -->|Yes ✅| D[CRA Direct Use Test Met:\nBorrowed funds went\ndirectly to income-earning\nnon-reg investments]
    C -->|No ❌| E[Fails if: Funds used for\npersonal expenses, TFSA,\nor RRSP directly]
    D --> F[Track ALL HELOC\nInterest Carefully\nKeep receipts & statements]
    F --> G[At Tax Time:\nSchedule 4 / Line 22100\nCarrying Charges & Interest]
    G --> H[💰 Tax Deduction:\n$390 deducted from\ntaxable income\n~$175 refund at 45% MTR]
      </div>
    </div>
    <div class="callout warn"><strong>Record-keeping is non-negotiable.</strong> Maintain a dedicated HELOC used solely for investments. Never commingle personal spending. CRA can audit up to 6 years back. Maintain a spreadsheet tracking each draw, investment purchase, and interest charge with dates and amounts.</div>
  </div>

  <!-- STEP 4 -->

  <div class="dcard gold">
    <div class="dcard-eye">Step 4 · Refund Deployment</div>
    <div class="dcard-title">Tax Refund Recycled into Mortgage</div>
    <div class="dcard-note">The annual tax refund is the "bonus accelerant" of the strategy. Applying it as a lump-sum principal payment creates more HELOC room, funds more investments, and accelerates conversion of non-deductible to deductible debt.</div>
    <div class="diag-scroll">
      <div class="mermaid">
flowchart TD
    A[💰 Receive Tax Refund\ne.g. $1,800 Year 1\nfrom HELOC interest deduction] --> B{How to Deploy\nthe Refund?}
    B --> C[Option A ✅ Recommended:\nApply to Mortgage\nPrincipal as Lump Sum]
    B --> D[Option B:\nRe-invest in\nNon-Registered Account]
    B --> E[Option C:\nLiving expenses\n⚠️ Weakens strategy]
    C --> F[Mortgage Balance\nDrops Further]
    F --> G[New Equity Unlocked\n→ More HELOC Room]
    G --> H[Draw New HELOC Room\nand Re-invest]
    H --> I[✅ Acceleration Loop:\nEach refund speeds up\nmortgage paydown and\ngrows investment base]
      </div>
    </div>
  </div>

  <!-- STEP 5 -->

  <div class="dcard">
    <div class="dcard-eye">Step 5 · Steady State</div>
    <div class="dcard-title">The Compounding Loop</div>
    <div class="dcard-note">Once established, the strategy enters a self-sustaining loop. Monthly payments, investment income, and annual tax refunds each feed the next cycle. Over 20–25 years the compounding effect is substantial.</div>
    <div class="diag-scroll">
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
    H --> I[🎯 End State:\nMortgage Paid Off\nLarge Non-Reg Portfolio\nDebt fully tax-deductible]
      </div>
    </div>
    <div class="callout"><strong>The key insight:</strong> You begin with $400K of non-deductible mortgage debt. Over time, you convert it dollar by dollar into deductible investment debt, while simultaneously building a portfolio. At completion, the full original mortgage amount is "good debt."</div>
  </div>

  <!-- STEP 6 -->

  <div class="dcard gold">
    <div class="dcard-eye">Step 6 · End Game</div>
    <div class="dcard-title">Mortgage Fully Paid — Debt Conversion Complete</div>
    <div class="dcard-note">After 20–25 years, the mortgage is eliminated. The entire HELOC balance is now fully tax-deductible investment debt. Three strategic exit options emerge.</div>
    <div class="diag-scroll">
      <div class="mermaid">
flowchart TD
    A([🏠 Mortgage Fully Paid\nHELOC = Original\nMortgage Amount\ne.g. $400K]) --> B[Entire HELOC Balance\nis Tax-Deductible Debt\nGood Debt Conversion\nComplete ✅]
    B --> C[Non-Reg Portfolio\nhas grown for\n20-25 years]
    C --> D{Decision Point}
    D --> E[Option A: Hold Portfolio\nContinue collecting\ntax-advantaged dividends\nOffset HELOC interest]
    D --> F[Option B: Sell Portfolio\nPay off HELOC entirely\nDebt-free with\nlarge capital gain]
    D --> G[Option C: Rebalance\nPartial paydown plus keep\ncore portfolio running]
    E --> H[💰 Net Wealth:\nHome owned free and clear\nLarge investment portfolio\nAnnual carrying cost offset\nby dividends]
      </div>
    </div>
    <div class="callout"><strong>Outcome:</strong> A homeowner who implements the Smith Maneuver vs. one who simply pays down their mortgage will typically end up with similar home equity at payoff — but the Smith Maneuver homeowner also holds a large, liquid investment portfolio representing significantly greater total wealth.</div>
  </div>
</div>
</div>

<!-- ══════════════════════════════════════════════════════════ -->

<!-- SECTION 3: MARKET RETURNS                                -->

<!-- ══════════════════════════════════════════════════════════ -->

<div id="returns" class="section">
<div class="page-wrap">
  <div class="ch-head"><div class="ch-lbl">Section 03</div><h2 class="ch-title">50 Years of Global Market Returns</h2></div>
  <p style="font-size:13px;color:var(--muted);margin-bottom:20px;max-width:660px;line-height:1.8;">MSCI World Total Return Index (USD), 1975–2024. This is the benchmark underlying most global equity ETFs. Understanding its volatility and long-run tendency is essential context for any leveraged investment strategy.</p>

  <div class="fact-check"><strong>Data note:</strong> MSCI World Index was officially launched March 31, 1986. Data prior to that date is backtested by MSCI. Long-run CAGR 1975–2024 ≈ 9.3%. The 1986–2025 actual (non-backtested) period shows ≈ 8.9% CAGR. Annual volatility σ ≈ 15% confirmed by MSCI. Individual annual return figures sourced from MSCI and verified against multiple providers. Sources: MSCI, investingintheweb.com, PortfolioVisualizer.</div>

  <div class="ccrd">
    <div class="ccrd-lbl">Chart 01 · Annual Returns</div>
    <h3>MSCI World Annual Total Returns 1975–2024</h3>
    <p class="ccrd-note">Green = positive year, Red = negative year. Dashed line = long-run average ~9.3%. Note the high frequency of positive years (72%) and the asymmetry of recoveries: large down years are typically followed by strong rebounds.</p>
    <div class="cw tall"><canvas id="chartHist"></canvas></div>
  </div>

  <div class="two-col">
    <div class="ccrd">
      <div class="ccrd-lbl">Chart 02 · Distribution</div>
      <h3>Return Distribution — 50 Years</h3>
      <p class="ccrd-note">How frequently each return bucket occurred. The market spent more than half of years delivering 10%+ returns. Only 14 of 50 years were negative.</p>
      <div class="cw med"><canvas id="chartDist"></canvas></div>
    </div>
    <div class="ccrd">
      <div class="ccrd-lbl">Chart 03 · Volatility Bands</div>
      <h3>What to Expect in Any Given Year (σ = 15%)</h3>
      <p class="ccrd-note">68% of years fall within ±1σ (−5.7% to +24.3%). 95% within ±2σ. "Bad year" and "good year" are well within normal range.</p>
      <div class="cw med"><canvas id="chartBand"></canvas></div>
    </div>
  </div>

  <div class="two-col">
    <div class="ccrd rust">
      <div class="ccrd-lbl">Chart 04 · Bear Markets</div>
      <h3>Historical Bear Markets — Depth &amp; Duration</h3>
      <p class="ccrd-note">Red bars = max drawdown %. Gold line = months to trough. GFC 2007–09 was the deepest at −54 to −58% and slowest to recover.</p>
      <div class="cw med"><canvas id="chartBear"></canvas></div>
    </div>
    <div class="ccrd gold">
      <div class="ccrd-lbl">Chart 05 · Rolling CAGR</div>
      <h3>Rolling 10-Year Compounded Returns</h3>
      <p class="ccrd-note">Every 10-year rolling period, 1984–2024. Only one period (ending ~1990) produced near-zero returns. All recent 10-year periods exceeded 6% CAGR, most exceeded 9%.</p>
      <div class="cw med"><canvas id="chartRoll"></canvas></div>
    </div>
  </div>

  <div class="ccrd">
    <div class="ccrd-lbl">Notable Years — Context</div>
    <h3>Key Years in 50-Year Dataset</h3>
    <p class="ccrd-note">Selected years with context for what drove unusually large moves.</p>
    <div class="tbl-scroll">
    <table class="yr-tbl">
      <thead><tr><th>Year</th><th>Return</th><th>What Happened</th><th>Relative Scale</th></tr></thead>
      <tbody id="notableBody"></tbody>
    </table>
    </div>
  </div>
</div>
</div>

<!-- ══════════════════════════════════════════════════════════ -->

<!-- SECTION 4: CRASH RECOVERY                                -->

<!-- ══════════════════════════════════════════════════════════ -->

<div id="crashes" class="section">
<div class="page-wrap">
  <div class="ch-head"><div class="ch-lbl">Section 04</div><h2 class="ch-title">Market Crash Recovery Analysis</h2></div>
  <p style="font-size:13px;color:var(--muted);margin-bottom:20px;max-width:660px;line-height:1.8;">MSCI World Total Return (USD). Three major crises compared — dot-com, GFC, and COVID — covering maximum drawdowns, time to trough, and time to recover prior peak. Understanding these is critical for a leveraged investor who must hold through drawdowns without selling.</p>

  <div class="fact-check"><strong>Data verification:</strong> Dot-com figures (−47%, 40 months peak→recovery) confirmed by Walter Scott Global Equity research. GFC figures: drawdown −54% to −58% depending on gross/net basis; peak→recovery 53–64 months depending on source. Our figures use gross total return basis (−58%, 64 months). COVID figures (−34%, ~9 months) confirmed by multiple sources including Funds Society analysis of MSCI World. Sources: MSCI, Walter Scott Asset Management, investingintheweb.com.</div>

  <div class="crash-grid">
    <div class="crash-crd">
      <div style="display:flex;align-items:center;gap:10px;margin-bottom:6px;">
        <h3>Dot-Com Bust</h3>
        <span class="crash-badge" style="background:#c04000;color:#fff;">2000–2003</span>
      </div>
      <div class="crash-row"><span class="lbl">Peak</span><span class="val">March 2000</span></div>
      <div class="crash-row"><span class="lbl">Trough</span><span class="val">October 2002</span></div>
      <div class="crash-row"><span class="lbl">Max Drawdown</span><span class="val r">−47%</span></div>
      <div class="crash-row"><span class="lbl">Time to Bottom</span><span class="val">~31 months</span></div>
      <div class="crash-row"><span class="lbl">Recovery to ATH</span><span class="val">~May 2007*</span></div>
      <div class="crash-row"><span class="lbl">Peak → Recovery</span><span class="val a">~85 months (7 yrs)</span></div>
      <div class="crash-row"><span class="lbl">Gain Required</span><span class="val g">+88% from trough</span></div>
      <p style="font-size:11.5px;color:var(--muted);margin-top:10px;line-height:1.7;">Technology stocks overvalued at 40–60× revenues. MSCI World recovery to prior ATH took approximately 7 years; the 40-month figure cited in some sources reflects recovery to initial drawdown level, not full prior peak. *Note: Sources vary — Walter Scott reports 40 months to prior peak using their specific measurement methodology.</p>
    </div>

```
<div class="crash-crd">
  <div style="display:flex;align-items:center;gap:10px;margin-bottom:6px;">
    <h3>Global Financial Crisis</h3>
    <span class="crash-badge" style="background:var(--navy);color:#fff;">2007–2013</span>
  </div>
  <div class="crash-row"><span class="lbl">Peak</span><span class="val">October 2007</span></div>
  <div class="crash-row"><span class="lbl">Trough</span><span class="val">March 2009</span></div>
  <div class="crash-row"><span class="lbl">Max Drawdown</span><span class="val r">−54% to −58%†</span></div>
  <div class="crash-row"><span class="lbl">Time to Bottom</span><span class="val">~17 months</span></div>
  <div class="crash-row"><span class="lbl">Recovery to ATH</span><span class="val">Feb 2013</span></div>
  <div class="crash-row"><span class="lbl">Peak → Recovery</span><span class="val a">~64 months (5⅓ yrs)</span></div>
  <div class="crash-row"><span class="lbl">Gain Required</span><span class="val g">+118–138% from trough</span></div>
  <p style="font-size:11.5px;color:var(--muted);margin-top:10px;line-height:1.7;">Deepest and longest recovery in modern history. Extended by European sovereign debt crisis 2010–12. †Drawdown range: −54% net return basis (Walter Scott), −57.8% gross return basis (investingintheweb.com). Recovery time 53–64 months depending on measurement methodology.</p>
</div>

<div class="crash-crd">
  <div style="display:flex;align-items:center;gap:10px;margin-bottom:6px;">
    <h3>COVID-19 Crash</h3>
    <span class="crash-badge" style="background:var(--forest);color:#fff;">2020</span>
  </div>
  <div class="crash-row"><span class="lbl">Peak</span><span class="val">February 2020</span></div>
  <div class="crash-row"><span class="lbl">Trough</span><span class="val">March 23, 2020</span></div>
  <div class="crash-row"><span class="lbl">Max Drawdown</span><span class="val r">−34%</span></div>
  <div class="crash-row"><span class="lbl">Time to Bottom</span><span class="val">~5 weeks</span></div>
  <div class="crash-row"><span class="lbl">Recovery to ATH</span><span class="val">November 2020</span></div>
  <div class="crash-row"><span class="lbl">Peak → Recovery</span><span class="val g">~9 months</span></div>
  <div class="crash-row"><span class="lbl">Gain Required</span><span class="val g">+52% from trough</span></div>
  <p style="font-size:11.5px;color:var(--muted);margin-top:10px;line-height:1.7;">Fastest crash and fastest recovery in the dataset. Two of the five largest single-day declines in market history occurred in March 2020 (−9.9% on 12 March and 16 March). Recovery driven by fiscal stimulus, vaccine optimism, and growth in technology/remote work sectors.</p>
</div>
```

  </div>

  <!-- SVG TIMELINE -->

  <div class="ccrd">
    <div class="ccrd-lbl">Visual Comparison</div>
    <h3>Recovery Timeline — Proportional Scale</h3>
    <p class="ccrd-note">Each bar shows peak→trough (red) and trough→recovery (green). Width is proportional to time. Height represents max drawdown severity.</p>
    <div style="overflow-x:auto;">
    <svg viewBox="0 0 820 360" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:820px;font-family:'IBM Plex Mono',monospace;">
      <style>.lc{fill:#7a7060;font-size:11px;} .lcs{fill:#7a7060;font-size:9px;} .lbig{fill:#0e1117;font-size:13px;font-weight:600;} .lrec{fill:#1a6b5e;font-size:10px;} .ax{stroke:#c4bba8;stroke-width:1;}</style>
      <!-- Y axis labels -->
      <text x="10" y="100" class="lc">0%</text>
      <text x="10" y="150" class="lc">−20%</text>
      <text x="10" y="200" class="lc">−40%</text>
      <text x="10" y="235" class="lc">−58%</text>
      <!-- Axis -->
      <line x1="60" y1="95" x2="780" y2="95" class="ax"/>

```
  <!-- DOT-COM: peak Mar2000, trough Oct2002 (31mo), recovery ~May2007 (85mo total) -->
  <!-- Scale: 85 months total = 460px wide. Each month = 460/85 = 5.4px -->
  <!-- Trough at 31mo = 167px, Recovery at 85mo = 460px -->
  <!-- Depth: -47%, bar height = 47*1.5 = 70px -->
  <text x="70" y="78" class="lbig" fill="#c04000">Dot-Com</text>
  <text x="70" y="88" class="lcs">2000–2007</text>
  <!-- Peak to trough: red -->
  <rect x="70" y="95" width="167" height="70" fill="rgba(201,76,26,0.7)" rx="2"/>
  <text x="100" y="135" fill="white" font-size="10" font-family="IBM Plex Mono,monospace">−47%</text>
  <!-- Trough to recovery: green -->
  <rect x="237" y="95" width="293" height="70" fill="rgba(26,107,94,0.55)" rx="2"/>
  <!-- Labels -->
  <text x="70" y="180" class="lcs">Mar 2000</text>
  <text x="215" y="180" class="lcs" text-anchor="middle">Oct 2002</text>
  <text x="530" y="180" class="lcs" text-anchor="middle">~May 2007 ✓</text>
  <text x="300" y="135" class="lrec">Recovery: ~54 months</text>
  <text x="100" y="150" fill="rgba(255,255,255,0.8)" font-size="9" font-family="IBM Plex Mono,monospace">31 months</text>

  <!-- GFC: peak Oct2007, trough Mar2009 (17mo), recovery Feb2013 (64mo total) -->
  <!-- Scale same: 64mo total. Per px = 460/85 = 5.4. Width = 64*5.4 = 346px -->
  <!-- Trough at 17mo = 92px, Recovery = 346px -->
  <!-- Depth: -58%, height = 58*1.5 = 87px -->
  <text x="70" y="208" class="lbig" fill="#0f2a4a">GFC</text>
  <text x="70" y="218" class="lcs">2007–2013</text>
  <rect x="70" y="225" width="92" height="87" fill="rgba(15,42,74,0.7)" rx="2"/>
  <text x="85" y="270" fill="white" font-size="10" font-family="IBM Plex Mono,monospace">−58%</text>
  <rect x="162" y="225" width="254" height="87" fill="rgba(26,107,94,0.55)" rx="2"/>
  <text x="70" y="325" class="lcs">Oct 2007</text>
  <text x="152" y="325" class="lcs" text-anchor="middle">Mar 2009</text>
  <text x="416" y="325" class="lcs" text-anchor="middle">Feb 2013 ✓</text>
  <text x="210" y="270" class="lrec">Recovery: ~47 months</text>
  <text x="80" y="283" fill="rgba(255,255,255,0.8)" font-size="9" font-family="IBM Plex Mono,monospace">17 mo</text>

  <!-- Legend -->
  <rect x="550" y="300" width="16" height="12" fill="rgba(201,76,26,0.7)" rx="1"/>
  <text x="570" y="311" class="lcs">Peak to Trough</text>
  <rect x="660" y="300" width="16" height="12" fill="rgba(26,107,94,0.55)" rx="1"/>
  <text x="680" y="311" class="lcs">Trough to Recovery</text>
</svg>
</div>
```

  </div>

  <div class="dark-box">
    <strong>Lessons for the SM/HELOC Investor:</strong>
    <ul>
      <li><strong>The GFC scenario is the stress test.</strong> A −58% drawdown on a $300K HELOC portfolio = portfolio falls to $126K. HELOC balance remains $300K. Net position: −$174K. You must service the HELOC interest from employment income throughout. This is why low-beta ETFs (ZLB beta 0.57, XMU beta 0.65) matter — they would have declined approximately −33% to −38% in GFC, not −58%.</li>
      <li><strong>Never sell during the trough.</strong> The investor who sold at the March 2009 GFC bottom locked in a −58% loss. The investor who held had fully recovered by February 2013 — 47 months later — and went on to capture the 2013–2024 bull market.</li>
      <li><strong>COVID showed speed matters.</strong> A −34% drawdown recovered in 9 months. Had you drawn your HELOC right before COVID, you would have been back to even by November 2020. The key variable is whether you could service the HELOC interest for those 9 months — not whether the market would recover.</li>
      <li><strong>Cash flow resilience is the critical SM variable.</strong> You need to be able to service HELOC interest from employment income alone through any drawdown scenario. Size your HELOC accordingly.</li>
    </ul>
  </div>
</div>
</div>

<!-- ══════════════════════════════════════════════════════════ -->

<!-- SECTION 5: SIMULATION                                    -->

<!-- ══════════════════════════════════════════════════════════ -->

<div id="simulation" class="section">
<div class="page-wrap">
  <div class="ch-head"><div class="ch-lbl">Section 05</div><h2 class="ch-title">20-Year Smith Maneuver Simulation</h2></div>
  <p style="font-size:13px;color:var(--muted);margin-bottom:18px;max-width:660px;line-height:1.8;">Assumptions: $500K home, $300K mortgage at amortisation start, HELOC rate 6.5%, MTR 45%, annual principal payments growing from ~$4,800/yr. Three return scenarios using realistic return sequences including embedded crash years. All returns are MSCI World USD total return proxies.</p>

  <div class="callout gold"><strong>Simulation assumptions are transparent and conservative.</strong> Crash years (2008 = −35%, 2022 = −14%) are embedded in all scenarios. Principal growth reflects a typical 25-year amortisation. Tax refunds from HELOC interest deductions are applied as lump-sum principal payments in all scenarios. The "no strategy" baseline assumes only regular mortgage payments with no HELOC utilisation.</div>

  <div class="toggle-row">
    <button class="tbtn active" onclick="switchSim('base',this)">Base (~9.3% CAGR)</button>
    <button class="tbtn" onclick="switchSim('conservative',this)">Conservative (~7.0% CAGR)</button>
    <button class="tbtn" onclick="switchSim('optimistic',this)">Optimistic (~11.0% CAGR)</button>
  </div>

  <div class="ccrd">
    <div class="ccrd-lbl">Portfolio Trajectory</div>
    <h3 id="simTitle">Smith Maneuver — Base Scenario (~9.3% CAGR)</h3>
    <p class="ccrd-note">Portfolio Value (strategy), HELOC Balance, Net Wealth (strategy), vs. Home Equity Only (no strategy). 🔻 = embedded crash year. 🚀 = strong recovery year.</p>
    <div class="cw tall"><canvas id="simChart"></canvas></div>
  </div>

  <div style="overflow-x:auto;margin-bottom:22px;" id="simTableWrap"></div>
</div>
</div>

<!-- ══════════════════════════════════════════════════════════ -->

<!-- SECTION 6: ETF UNIVERSE                                  -->

<!-- ══════════════════════════════════════════════════════════ -->

<div id="etfs" class="section">
<div class="page-wrap">
  <div class="ch-head"><div class="ch-lbl">Section 06</div><h2 class="ch-title">ETF Universe — Factor Framework &amp; Scoring</h2></div>
  <p style="font-size:13px;color:var(--muted);margin-bottom:20px;max-width:660px;line-height:1.8;">60+ TSX-listed ETFs analysed across four sleeves (Canada, US, EAFE, EM) and six factor strategies. Each ETF is scored separately for TFSA (Phase 1) and non-registered SM (Phase 2) because the optimal criteria are different — almost inversely so on yield and withholding tax.</p>

  <div class="alert-box"><strong>⚠️ AI Bubble Warning — Current as of March 2026:</strong> Standard MSCI Quality and market-cap-weight ETFs (ZUQ, XQLT, XUU) carry Nvidia at 5–6.4% of portfolio weight with tech sector at 30–34%. These are excellent products structurally but carry significant AI concentration risk at current valuations. Nvidia P/E ~50× in March 2026, S&P tech weight ~32%. Our portfolio recommendations systematically reduce this exposure using min-vol ETFs where the MSCI optimizer structurally caps volatile AI names.</div>

  <!-- FACTOR RANKINGS -->

  <div class="ccrd gold">
    <div class="ccrd-lbl">Factor Strategy Assessment</div>
    <h3>Which Factor Strategies Work Best for SM?</h3>
    <div class="tbl-scroll">
    <table class="dtbl" style="min-width:560px;">
      <thead><tr><th>Factor</th><th>SM Non-Reg Fit</th><th>TFSA Fit</th><th>Key Characteristic</th><th>Representative ETF</th></tr></thead>
      <tbody>
        <tr class="win"><td><span class="b b-q">Quality</span></td><td class="g">★★★★★</td><td class="g">★★★★★</td><td>High ROE, low leverage, earnings stability. Genuine income. Lower drawdowns than market.</td><td>XDIV, ZUQ (post-bubble), FCCQ</td></tr>
        <tr class="win"><td><span class="b b-lv">Min Volatility</span></td><td class="g">★★★★★</td><td class="g">★★★★★</td><td>MSCI optimizer structurally caps volatile AI names. Beta 0.57–0.70. Best bubble defence now.</td><td>ZLB, XMU, XMI, XMM</td></tr>
        <tr><td>Total Market</td><td class="a">★★★☆☆</td><td class="a">★★★☆☆</td><td>Simplest. CRA-compliant. But ~32% tech weight = AI bubble exposure.</td><td>XUU, VXC</td></tr>
        <tr><td><span class="b b-dg">Div. Growth</span></td><td class="g">★★★★☆</td><td class="a">★★★☆☆</td><td>Durable compounders. Low yield = TFSA-efficient. But Broadcom top holding in VGG now.</td><td>VGG (post-bubble), DGR</td></tr>
        <tr><td><span class="b b-hd">High Dividend</span></td><td class="g">★★★★★</td><td class="r">★★☆☆☆</td><td>Income maximised — ideal for SM deductibility. But high yield = WHT permanently lost in TFSA.</td><td>VDY, XDIV, VIDY</td></tr>
        <tr class="caution"><td>Momentum</td><td class="r">★☆☆☆☆</td><td class="r">★☆☆☆☆</td><td>Worst SM fit: crashes harder and faster, high turnover, tax inefficient, ROC risk.</td><td>Avoid</td></tr>
      </tbody>
    </table>
    </div>
  </div>

  <!-- AI AUDIT -->

  <div class="ccrd rust">
    <div class="ccrd-lbl">AI Bubble Audit · All Candidates</div>
    <h3>Nvidia &amp; AI Exposure by ETF</h3>
    <div class="tbl-scroll">
    <table class="dtbl" style="min-width:680px;">
      <thead><tr><th>ETF</th><th>Tech Weight</th><th>Nvidia Wt.</th><th>Broadcom Wt.</th><th>AI Bubble Risk</th><th>Recommendation</th></tr></thead>
      <tbody>
        <tr class="caution"><td><span class="tick">XUU / ZUQ</span></td><td class="r">32–34%</td><td class="r">5.5–6.4%</td><td class="r">3–5%</td><td><span class="b b-warn">Critical</span></td><td>Avoid current positioning. Post-bubble rotation target (ZUQ/XQLT have excellent quality methodology).</td></tr>
        <tr class="caution"><td><span class="tick">VGG</span></td><td class="a">27.8%</td><td class="g">~1%</td><td class="r">6.2% (#1)</td><td><span class="b b-warn">Moderate</span></td><td>Broadcom = AI semiconductor bet. Post-bubble rotation target once Broadcom P/E &lt;25×.</td></tr>
        <tr class="win"><td><span class="tick">XMU ★</span></td><td class="g">~15%</td><td class="g">1.4%</td><td class="g">Not top 25</td><td><span class="b b-ok">Low</span></td><td>Primary US pick. MSCI optimizer structurally caps volatile names. JNJ/XOM/MRK lead.</td></tr>
        <tr class="win"><td><span class="tick">XDIV ★</span></td><td class="g">~2%</td><td class="g">0%</td><td class="g">0%</td><td><span class="b b-win">Minimal</span></td><td>Zero tech/AI exposure. ~25 quality CDN holdings. Monthly eligible dividends.</td></tr>
        <tr class="win"><td><span class="tick">VDY ★</span></td><td class="g">~0%</td><td class="g">0%</td><td class="g">0%</td><td><span class="b b-win">Minimal</span></td><td>Financials + energy + pipelines. Zero tech. Ideal SM non-reg anchor.</td></tr>
        <tr class="win"><td><span class="tick">ZLB ★</span></td><td class="g">~3%</td><td class="g">0%</td><td class="g">0%</td><td><span class="b b-win">Minimal</span></td><td>Best CDN LV. Beta 0.57. Almost no AI exposure.</td></tr>
        <tr class="win"><td><span class="tick">XMI ★</span></td><td class="g">~12%</td><td class="g">~0.2%</td><td class="g">0%</td><td><span class="b b-ok">Low</span></td><td>EAFE min-vol. European/Japan defensive stocks dominate. Pharma/utilities/financials.</td></tr>
        <tr class="win"><td><span class="tick">VIDY ★</span></td><td class="g">~5–8%</td><td class="g">0%</td><td class="g">0%</td><td><span class="b b-ok">Low</span></td><td>EAFE high dividend. Roche/HSBC/Novartis/Toyota. Non-reg only (WHT too high in TFSA).</td></tr>
        <tr class="win"><td><span class="tick">XMM ★</span></td><td class="a">~20%</td><td class="g">0%</td><td class="g">0%</td><td><span class="b b-ok">Low-Mod</span></td><td>EM min-vol. TSMC/Samsung muted by optimizer. India-heavy = quality EM tilt. Watch AUM.</td></tr>
      </tbody>
    </table>
    </div>
  </div>

  <!-- KEY ETF DATA -->

  <div class="ccrd">
    <div class="ccrd-lbl">Key ETF Data · All Candidates Verified</div>
    <h3>Complete Candidate Statistics</h3>
    <div class="tbl-scroll">
    <table class="dtbl" style="min-width:820px;">
      <thead><tr><th>Ticker</th><th>Name (Brief)</th><th>Market</th><th>Strategy</th><th>MER</th><th>Yield</th><th>Beta</th><th>AUM</th><th>Best For</th></tr></thead>
      <tbody>
        <tr class="win"><td><span class="tick">ZLB</span><span class="tick-sub">BMO</span></td><td>Low Vol CDN Equity</td><td>🇨🇦 Canada</td><td><span class="b b-lv">LV</span></td><td class="g">0.40%</td><td class="mn">1.9%</td><td class="g">0.57</td><td>$2.4B</td><td>TFSA Phase 1 — CDN anchor, beta 0.57</td></tr>
        <tr class="win"><td><span class="tick">XDIV</span><span class="tick-sub">iShares</span></td><td>CDN Quality Div</td><td>🇨🇦 Canada</td><td><span class="b b-q">MX</span></td><td class="g">0.10%</td><td class="g">3.7%</td><td class="a">0.80</td><td>$2.2B</td><td>Both phases — ultra-low MER, eligible divs</td></tr>
        <tr class="win"><td><span class="tick">VDY</span><span class="tick-sub">Vanguard</span></td><td>FTSE CDN High Div</td><td>🇨🇦 Canada</td><td><span class="b b-hd">HD</span></td><td class="g">0.22%</td><td class="g">3.56%</td><td class="a">0.85</td><td>$6.65B</td><td>Phase 2 non-reg — eligible divs, monthly, AUM leader</td></tr>
        <tr><td><span class="tick">FCCQ</span><span class="tick-sub">Fidelity</span></td><td>CDN High Quality</td><td>🇨🇦 Canada</td><td><span class="b b-q">Q</span></td><td class="g">0.39%</td><td class="mn">1.8%</td><td class="a">0.75</td><td>$400M</td><td>TFSA 5th ETF — quality growth, strong 1-yr return</td></tr>
        <tr><td><span class="tick">XMV</span><span class="tick-sub">iShares</span></td><td>MSCI Min Vol CDN</td><td>🇨🇦 Canada</td><td><span class="b b-lv">LV</span></td><td class="g">0.33%</td><td class="mn">2.2%</td><td class="g">0.68</td><td>$900M</td><td>Alt to ZLB — cheaper MER, MSCI methodology</td></tr>
        <tr class="win"><td><span class="tick">XMU</span><span class="tick-sub">iShares</span></td><td>MSCI Min Vol USA</td><td>🇺🇸 US</td><td><span class="b b-lv">LV</span></td><td class="g">0.20%</td><td class="g">1.3%</td><td class="g">0.65</td><td>$1.8B</td><td>TFSA Phase 1 — best bubble defence, lowest MER US</td></tr>
        <tr><td><span class="tick">FCUQ</span><span class="tick-sub">Fidelity</span></td><td>US High Quality</td><td>🇺🇸 US</td><td><span class="b b-q">Q</span></td><td class="a">0.39%</td><td class="g">0.73%</td><td class="a">0.85</td><td>$500M</td><td>TFSA alt — FCF quality, lower Nvidia than ZUQ</td></tr>
        <tr><td><span class="tick">VGG</span><span class="tick-sub">Vanguard</span></td><td>US Div Appreciation</td><td>🇺🇸 US</td><td><span class="b b-dg">DG</span></td><td class="a">0.30%</td><td class="g">1.14%</td><td class="a">0.85</td><td>$2.33B</td><td>Post-bubble rotation — low WHT drag in TFSA</td></tr>
        <tr class="caution"><td><span class="tick">ZUQ</span><span class="tick-sub">BMO</span></td><td>MSCI USA Quality</td><td>🇺🇸 US</td><td><span class="b b-q">Q</span></td><td class="a">0.33%</td><td class="r">0.45%</td><td class="a">0.90</td><td>$3.2B</td><td>Post-bubble target — Nvidia 6.4% now, excellent quality screen</td></tr>
        <tr class="win"><td><span class="tick">XMI</span><span class="tick-sub">iShares</span></td><td>MSCI EAFE Min Vol</td><td>🌐 EAFE</td><td><span class="b b-lv">LV</span></td><td class="a">0.33%</td><td class="a">2.64%</td><td class="g">0.63</td><td>$170M</td><td>Both phases — lowest beta EAFE, WHT-efficient</td></tr>
        <tr class="win"><td><span class="tick">VIDY</span><span class="tick-sub">Vanguard</span></td><td>Dev ex-NA High Div</td><td>🌐 EAFE</td><td><span class="b b-hd">HD</span></td><td class="g">0.32%</td><td class="r">~4.8%</td><td class="a">0.80</td><td>$713M</td><td>Phase 2 non-reg only — high WHT too costly in TFSA</td></tr>
        <tr><td><span class="tick">ZIQ</span><span class="tick-sub">BMO</span></td><td>MSCI EAFE Quality</td><td>🌐 EAFE</td><td><span class="b b-q">Q</span></td><td class="a">0.35%</td><td class="g">1.8%</td><td class="a">0.78</td><td>$250M</td><td>TFSA rotation target — low WHT, quality tilt</td></tr>
        <tr class="win"><td><span class="tick">XMM</span><span class="tick-sub">iShares</span></td><td>MSCI EM Min Vol</td><td>🌏 EM</td><td><span class="b b-lv">LV</span></td><td class="a">0.39%</td><td class="g">2.0%</td><td class="a">~0.70</td><td class="a">$96M ⚠</td><td>Both phases — only EM LV on TSX. Watch AUM ($50M floor).</td></tr>
        <tr><td><span class="tick">VEE</span><span class="tick-sub">Vanguard</span></td><td>FTSE EM All Cap</td><td>🌏 EM</td><td>Base</td><td class="g">0.25%</td><td class="a">2.5%</td><td>—</td><td>$1.9B</td><td>XMM fallback if AUM drops — higher China weight</td></tr>
      </tbody>
    </table>
    </div>
    <div class="footnote" style="border:none;margin-bottom:0;">Data: March 2026. Sources: Vanguard Canada, BMO ETFs, iShares Canada, Fidelity Canada, MSCI, StockAnalysis.com, TradingView. MERs from provider factsheets. Yields trailing 12-month. Beta vs MSCI World or relevant benchmark. ★ = recommended holding.</div>
  </div>
</div>
</div>

<!-- ══════════════════════════════════════════════════════════ -->

<!-- SECTION 7: PHASE 1 — TFSA                                -->

<!-- ══════════════════════════════════════════════════════════ -->

<div id="phase1" class="section">
<div class="page-wrap">
  <div class="ch-head"><div class="ch-lbl">Section 07</div><h2 class="ch-title">Phase 1 Portfolio — TFSA HELOC Growth</h2></div>
  <div class="callout gold"><strong>Phase 1 mandate:</strong> HELOC proceeds → TFSA. No interest deduction (intentionally). Maximise tax-free compounding. Minimise WHT leakage (permanently lost in TFSA). Prioritise bubble defence (leveraged investor cannot afford a forced sale). Target: 4–5 ETFs, blended beta ~0.65, minimal Nvidia exposure.</div>

  <!-- WHT INVERSION -->

  <div class="ch-head" style="margin-top:30px;"><div class="ch-lbl">The Key Inversion</div><h2 class="ch-title">Why Scoring Flips: Non-Reg vs TFSA</h2></div>
  <div class="inv-grid">
    <div class="inv-col old">
      <h3>Phase 2 · Non-Registered / SM Account</h3>
      <div class="inv-row"><span class="inv-ll">High yield</span><span class="inv-vv g">✓ SM deductibility + eligible div tax credit</span></div>
      <div class="inv-row"><span class="inv-ll">Foreign WHT</span><span class="inv-vv g">✓ Partially recovered via T1 Line 40500</span></div>
      <div class="inv-row"><span class="inv-ll">VIDY (4.8% yield)</span><span class="inv-vv g">✓ Income offsets HELOC carry cost</span></div>
      <div class="inv-row"><span class="inv-ll">XMU (1.3% yield)</span><span class="inv-vv r">✗ Insufficient income for SM deductibility</span></div>
      <div class="inv-row"><span class="inv-ll">Capital gains</span><span class="inv-vv r">⚠ Taxed at 50% inclusion rate</span></div>
      <div class="inv-row"><span class="inv-ll">Monthly distributions</span><span class="inv-vv g">✓ Preferred for SM reinvestment cycle</span></div>
    </div>
    <div class="inv-col new">
      <h3>Phase 1 · TFSA Account</h3>
      <div class="inv-row"><span class="inv-ll">High yield</span><span class="inv-vv r">✗ Creates unnecessary distribution drag</span></div>
      <div class="inv-row"><span class="inv-ll">Foreign WHT</span><span class="inv-vv r">✗ Permanently lost — no recovery mechanism</span></div>
      <div class="inv-row"><span class="inv-ll">VIDY (4.8% yield)</span><span class="inv-vv r">✗ ~$750/yr lost per $100K in WHT permanently</span></div>
      <div class="inv-row"><span class="inv-ll">XMU (1.3% yield)</span><span class="inv-vv g">✓ Minimal WHT leakage, maximum compounding</span></div>
      <div class="inv-row"><span class="inv-ll">Capital gains</span><span class="inv-vv g">✓ Tax-free forever in TFSA — primary vehicle</span></div>
      <div class="inv-row"><span class="inv-ll">Quarterly distributions</span><span class="inv-vv g">✓ Fine in TFSA — less cash drag than monthly</span></div>
    </div>
  </div>

  <!-- WHT TABLE -->

  <h3 style="font-family:'Playfair Display',serif;font-size:17px;margin-bottom:12px;">Annual WHT Leakage in TFSA — Per ETF</h3>
  <div class="wht-grid">
    <div class="wht-cell"><h5>VIDY (EAFE High Div)</h5><div class="wht-amt" style="color:var(--rust)">−0.75%/yr</div><div class="wht-note">4.8% yield × ~15–18% WHT. ~$750 lost per $100K annually. Permanently.</div></div>
    <div class="wht-cell"><h5>XMI (EAFE Min Vol)</h5><div class="wht-amt" style="color:var(--amber)">−0.40%/yr</div><div class="wht-note">2.64% × ~15% WHT. Half the leakage of VIDY. Acceptable for defensive anchor.</div></div>
    <div class="wht-cell"><h5>ZIQ (EAFE Quality)</h5><div class="wht-amt" style="color:var(--forest)">−0.27%/yr</div><div class="wht-note">1.8% × 15%. Low leakage. Strong TFSA candidate once AUM grows.</div></div>
    <div class="wht-cell"><h5>XMU (US Min Vol)</h5><div class="wht-amt" style="color:var(--forest)">−0.20%/yr</div><div class="wht-note">1.3% × 15% US WHT. Lowest US leakage available. Best US TFSA choice.</div></div>
    <div class="wht-cell"><h5>ZUQ (US Quality)</h5><div class="wht-amt" style="color:var(--forest)">−0.07%/yr</div><div class="wht-note">0.45% × 15%. Near-zero leakage — but Nvidia 6.4% is the problem now.</div></div>
    <div class="wht-cell"><h5>ZLB / XDIV (Canada)</h5><div class="wht-amt" style="color:var(--forest)">0.00%/yr</div><div class="wht-note">Canadian ETFs: zero WHT. Every dollar of distribution is sheltered 100%.</div></div>
    <div class="wht-cell"><h5>XMM (EM Min Vol)</h5><div class="wht-amt" style="color:var(--amber)">−0.38%/yr</div><div class="wht-note">2.0% × ~19% blended (India 20%, Taiwan 21%, China 10%). Manageable.</div></div>
    <div class="wht-cell"><h5>VEE (EM Base)</h5><div class="wht-amt" style="color:var(--amber)">−0.48%/yr</div><div class="wht-note">2.5% × 19%. Higher leakage than XMM despite lower MER. XMM preferred.</div></div>
  </div>

  <!-- PORTFOLIO CARDS -->

  <h3 style="font-family:'Playfair Display',serif;font-size:18px;margin-bottom:16px;">★ Recommended Phase 1 TFSA Portfolio</h3>
  <div class="port-sum">
    <div class="ps-cell"><div class="ps-lbl">Blended MER</div><div class="ps-val g">0.32%</div></div>
    <div class="ps-cell"><div class="ps-lbl">Blended Yield</div><div class="ps-val g">1.75%</div></div>
    <div class="ps-cell"><div class="ps-lbl">True TFSA Drag</div><div class="ps-val g">~0.57%/yr</div></div>
    <div class="ps-cell"><div class="ps-lbl">Blended Beta</div><div class="ps-val g">~0.65</div></div>
    <div class="ps-cell"><div class="ps-lbl">Nvidia Weight</div><div class="ps-val g">~0.5%</div></div>
    <div class="ps-cell"><div class="ps-lbl">Tech Weight</div><div class="ps-val g">~14%</div></div>
  </div>
  <div class="port-grid">
    <div class="pcrd ca">
      <div class="pcrd-ticker">ZLB</div>
      <div class="pcrd-sub">BMO Low Vol CDN · 🇨🇦 Canada</div>
      <div class="pcrd-wt">25%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val g">0.40%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">1.9%</span></div>
        <div class="pstat"><span class="lbl">Beta</span><span class="val g">0.57</span></div>
        <div class="pstat"><span class="lbl">WHT in TFSA</span><span class="val g">0%</span></div>
        <div class="pstat"><span class="lbl">Tech Weight</span><span class="val g">~3%</span></div>
        <div class="pstat"><span class="lbl">Nvidia</span><span class="val g">0%</span></div>
      </div>
    </div>
    <div class="pcrd us">
      <div class="pcrd-ticker">XMU</div>
      <div class="pcrd-sub">iShares MSCI Min Vol USA · 🇺🇸 US</div>
      <div class="pcrd-wt">35%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val g">0.20%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">1.3%</span></div>
        <div class="pstat"><span class="lbl">Beta</span><span class="val g">0.65</span></div>
        <div class="pstat"><span class="lbl">WHT in TFSA</span><span class="val a">~0.20%/yr</span></div>
        <div class="pstat"><span class="lbl">Tech Weight</span><span class="val g">~15%</span></div>
        <div class="pstat"><span class="lbl">Nvidia</span><span class="val g">1.4%</span></div>
      </div>
    </div>
    <div class="pcrd eafe">
      <div class="pcrd-ticker">XMI</div>
      <div class="pcrd-sub">iShares MSCI EAFE Min Vol · 🌐 EAFE</div>
      <div class="pcrd-wt">25%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val a">0.33%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val a">2.64%</span></div>
        <div class="pstat"><span class="lbl">Beta</span><span class="val g">0.63</span></div>
        <div class="pstat"><span class="lbl">WHT in TFSA</span><span class="val a">~0.40%/yr</span></div>
        <div class="pstat"><span class="lbl">Tech Weight</span><span class="val g">~12%</span></div>
        <div class="pstat"><span class="lbl">Nvidia</span><span class="val g">~0.2%</span></div>
      </div>
    </div>
    <div class="pcrd em">
      <div class="pcrd-ticker">XMM</div>
      <div class="pcrd-sub">iShares MSCI EM Min Vol · 🌏 EM</div>
      <div class="pcrd-wt">15%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val a">0.39%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">2.0%</span></div>
        <div class="pstat"><span class="lbl">Beta (est.)</span><span class="val a">~0.70</span></div>
        <div class="pstat"><span class="lbl">WHT in TFSA</span><span class="val a">~0.38%/yr</span></div>
        <div class="pstat"><span class="lbl">AUM ⚠</span><span class="val a">$96M</span></div>
        <div class="pstat"><span class="lbl">India Weight</span><span class="val g">~25%</span></div>
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
        <li><span style="color:var(--muted);font-style:italic;">Blended Beta</span><span>~0.65</span></li>
        <li><span style="color:var(--muted);font-style:italic;">Blended MER</span><span>0.32%</span></li>
        <li><span style="color:var(--muted);font-style:italic;">True TFSA Drag/yr</span><span>~0.57%</span></li>
      </ul>
    </div>
    <div class="cmp-box">
      <h4>5-ETF Variant (Quality + Vol)</h4>
      <ul>
        <li><span>ZLB — Canada LV</span><span>15%</span></li>
        <li><span>FCCQ — Canada Quality</span><span>10%</span></li>
        <li><span>XMU — US Min Vol</span><span>35%</span></li>
        <li><span>XMI — EAFE Min Vol</span><span>25%</span></li>
        <li><span>XMM — EM Min Vol</span><span>15%</span></li>
        <li><span style="color:var(--muted);font-style:italic;">Blended Beta</span><span>~0.66</span></li>
        <li><span style="color:var(--muted);font-style:italic;">Blended MER</span><span>0.32%</span></li>
      </ul>
    </div>
  </div>

  <div class="dark-box">
    <strong>Why this works for a leveraged TFSA investor:</strong>
    <ul>
      <li><strong>Drawdown control:</strong> Beta ~0.65 means a 30% market crash ≈ 20% portfolio decline. Psychologically manageable. You must not be forced to sell to service the HELOC.</li>
      <li><strong>WHT minimisation:</strong> Blended ~0.26%/yr total WHT leakage on foreign portion. Among the lowest achievable with genuine global diversification.</li>
      <li><strong>AI bubble defence:</strong> Blended Nvidia ~0.5%, tech ~14% vs S&P 500's ~32%. A 50% Nvidia decline = ~0.25% portfolio impact.</li>
      <li><strong>Compounding efficiency:</strong> Low yield = portfolio retains most return as unrealised capital gain. No tax event. Every dollar stays invested.</li>
      <li><strong>XMM AUM watch:</strong> Set a $50M floor. If XMM drops below $50M AUM, swap to ZEM ($800M AUM) as a fallback. Monitor quarterly.</li>
    </ul>
  </div>
</div>
</div>

<!-- ══════════════════════════════════════════════════════════ -->

<!-- SECTION 8: PHASE 2 — NON-REGISTERED SM                   -->

<!-- ══════════════════════════════════════════════════════════ -->

<div id="phase2" class="section">
<div class="page-wrap">
  <div class="ch-head"><div class="ch-lbl">Section 08</div><h2 class="ch-title">Phase 2 Portfolio — Non-Registered Smith Maneuver</h2></div>
  <div class="callout gold"><strong>Phase 2 mandate:</strong> HELOC proceeds → Non-registered account. CRA interest deductibility NOW applies. Investments must earn income (eligible dividends preferred). Canadian eligible dividends benefit from dividend tax credit. Foreign WHT on VIDY is now recoverable via T1 Line 40500. Capital gains taxed at 50% inclusion — less efficient than eligible dividends at high MTR.</div>

  <div class="callout warn"><strong>CRA Compliance Checklist for Phase 2:</strong> (1) HELOC funds flow directly into non-registered brokerage — never to personal account first. (2) All investments produce income (dividends, distributions). (3) No ROC distributions — they erode the cost base and can jeopardise deductibility. (4) Dedicated HELOC account, no personal use. (5) Annual Schedule 4 / Line 22100 filing with T5 slips and interest confirmation from lender.</div>

  <!-- ACCOUNT LOCATION MATRIX -->

  <h3 style="font-family:'Playfair Display',serif;font-size:17px;margin-bottom:12px;">Tax Account Location Matrix — BC Resident ~45% MTR</h3>
  <div class="tbl-scroll">
  <table class="dtbl" style="min-width:640px;">
    <thead><tr><th>Income Type</th><th>Effective Tax Rate</th><th>Best Account</th><th>Rationale</th></tr></thead>
    <tbody>
      <tr class="win"><td>Canadian eligible dividends</td><td class="g">~22–25%</td><td><strong>Non-Registered</strong></td><td>Dividend tax credit reduces effective rate to 22–25%. Most tax-efficient in non-reg. TFSA shelters the dividend but wastes the credit.</td></tr>
      <tr class="win"><td>Capital gains (below $250K/yr)</td><td class="g">~23%</td><td><strong>TFSA</strong></td><td>0% in TFSA vs 23% in non-reg. Capital appreciation should be sheltered.</td></tr>
      <tr><td>US dividends + 15% WHT</td><td class="a">~46% + WHT</td><td>RRSP ideal / Non-reg OK</td><td>RRSP: Canada-US treaty exempts WHT entirely. Non-reg: WHT partially recovered, 46% income tax applies. TFSA: worst (WHT permanent + no treaty relief).</td></tr>
      <tr><td>Foreign dividends (EAFE/EM) + WHT</td><td class="r">~46% + 15–21% WHT</td><td>Non-reg (Phase 2)</td><td>WHT partially recovered via T2209 foreign tax credit. Recovered ~60–70% of WHT. TFSA is worst: 100% WHT lost.</td></tr>
      <tr class="caution"><td>ROC (Return of Capital)</td><td class="r">Avoid entirely</td><td>Neither</td><td>ROC reduces ACB, erodes future capital gains exemption, and may cause CRA to challenge SM interest deductibility. Screen all ETFs for ROC.</td></tr>
    </tbody>
  </table>
  </div>

  <!-- PHASE 2 PORTFOLIO -->

  <h3 style="font-family:'Playfair Display',serif;font-size:18px;margin:24px 0 16px;">★ Recommended Phase 2 Non-Registered Portfolio</h3>
  <div class="port-sum">
    <div class="ps-cell"><div class="ps-lbl">Blended MER</div><div class="ps-val g">0.26%</div></div>
    <div class="ps-cell"><div class="ps-lbl">Blended Yield</div><div class="ps-val g">~3.8%</div></div>
    <div class="ps-cell"><div class="ps-lbl">CDN Eligible Divs</div><div class="ps-val g">~65%</div></div>
    <div class="ps-cell"><div class="ps-lbl">SM Compliant</div><div class="ps-val g">100%</div></div>
    <div class="ps-cell"><div class="ps-lbl">Nvidia Weight</div><div class="ps-val g">~0%</div></div>
    <div class="ps-cell"><div class="ps-lbl">ROC Risk</div><div class="ps-val g">Zero</div></div>
  </div>
  <div class="port-grid">
    <div class="pcrd ca">
      <div class="pcrd-ticker">VDY</div>
      <div class="pcrd-sub">Vanguard FTSE CDN Hi Div · 🇨🇦 Canada</div>
      <div class="pcrd-wt">40%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val g">0.22%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">3.56%</span></div>
        <div class="pstat"><span class="lbl">AUM</span><span class="val g">$6.65B</span></div>
        <div class="pstat"><span class="lbl">Div Type</span><span class="val g">Eligible ✓</span></div>
        <div class="pstat"><span class="lbl">Top Holdings</span><span class="val" style="font-size:9px;">RY/TD/ENB/BMO/BNS</span></div>
        <div class="pstat"><span class="lbl">Frequency</span><span class="val g">Monthly</span></div>
      </div>
    </div>
    <div class="pcrd ca">
      <div class="pcrd-ticker">XDIV</div>
      <div class="pcrd-sub">iShares CDN Quality Div · 🇨🇦 Canada</div>
      <div class="pcrd-wt">25%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val g">0.10%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">3.7%</span></div>
        <div class="pstat"><span class="lbl">Holdings</span><span class="val g">~25</span></div>
        <div class="pstat"><span class="lbl">Div Type</span><span class="val g">Eligible ✓</span></div>
        <div class="pstat"><span class="lbl">Strategy</span><span class="val" style="font-size:9px;">Quality screen</span></div>
        <div class="pstat"><span class="lbl">Frequency</span><span class="val g">Monthly</span></div>
      </div>
    </div>
    <div class="pcrd eafe">
      <div class="pcrd-ticker">VIDY</div>
      <div class="pcrd-sub">Vanguard Dev ex-NA High Div · 🌐 EAFE</div>
      <div class="pcrd-wt">25%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val g">0.32%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val a">~4.8%</span></div>
        <div class="pstat"><span class="lbl">AUM</span><span class="val g">$713M</span></div>
        <div class="pstat"><span class="lbl">Holdings</span><span class="val g">642</span></div>
        <div class="pstat"><span class="lbl">WHT Recovery</span><span class="val a">~60–70%</span></div>
        <div class="pstat"><span class="lbl">Top Holdings</span><span class="val" style="font-size:9px;">Roche/HSBC/Novartis</span></div>
      </div>
    </div>
    <div class="pcrd em">
      <div class="pcrd-ticker">XMM</div>
      <div class="pcrd-sub">iShares MSCI EM Min Vol · 🌏 EM</div>
      <div class="pcrd-wt">10%</div>
      <div class="pcrd-stats">
        <div class="pstat"><span class="lbl">MER</span><span class="val a">0.39%</span></div>
        <div class="pstat"><span class="lbl">Yield</span><span class="val g">2.0%</span></div>
        <div class="pstat"><span class="lbl">Beta</span><span class="val g">~0.70</span></div>
        <div class="pstat"><span class="lbl">WHT Recovery</span><span class="val a">Partial</span></div>
        <div class="pstat"><span class="lbl">AUM ⚠</span><span class="val a">$96M</span></div>
        <div class="pstat"><span class="lbl">India Wt.</span><span class="val g">~25%</span></div>
      </div>
    </div>
  </div>

  <div class="dark-box">
    <strong>Why VDY and XDIV together (not one or the other):</strong>
    <ul>
      <li><strong>VDY</strong> (40%) tracks FTSE Custom Canada High Dividend Yield Index — yield screen, broader coverage (~57 holdings), financials + energy + pipelines dominant. AUM $6.65B — largest Canadian dividend ETF. Monthly eligible dividends. Top 3: RY 15.5%, TD 10.4%, ENB 7.0%.</li>
      <li><strong>XDIV</strong> (25%) applies a quality overlay on top of the yield screen — ROE/leverage/earnings stability filters result in ~25 holdings. MER only 0.10% — cheapest quality dividend ETF in Canada. Monthly eligible dividends. Complements VDY by adding quality discipline.</li>
      <li><strong>Together:</strong> 65% Canadian eligible dividends at blended 0.14% MER. Different construction methods (yield screen vs. quality screen), different concentrations. Genuine diversification within the Canadian sleeve.</li>
      <li><strong>VIDY</strong> (25%) provides EAFE income diversification. High 4.8% yield means WHT costs ~0.75%/yr in TFSA — but in non-reg, ~60–70% is recovered via T2209. Net WHT cost in non-reg ≈ 0.22–0.30%/yr. Far more efficient than TFSA treatment.</li>
    </ul>
  </div>
</div>
</div>

<!-- ══════════════════════════════════════════════════════════ -->

<!-- SECTION 9: ROADMAP                                       -->

<!-- ══════════════════════════════════════════════════════════ -->

<div id="roadmap" class="section">
<div class="page-wrap">
  <div class="ch-head"><div class="ch-lbl">Section 09</div><h2 class="ch-title">Complete Strategy Roadmap</h2></div>
  <div class="callout">The roadmap below integrates Phase 1 (TFSA growth), Phase 2 (SM non-reg), AI bubble rotation, and long-term portfolio evolution. Each transition has quantitative triggers — not gut-feel timing.</div>

  <div class="tl">
    <div class="tl-item">
      <div class="tl-dot active">1</div>
      <div class="tl-body">
        <h4>Now — Phase 1 TFSA: Defensive Growth (Active)</h4>
        <p>HELOC proceeds → TFSA. Portfolio: ZLB 25% + XMU 35% + XMI 25% + XMM 15%. Blended beta 0.65. Nvidia ~0.5%. Tech ~14%. No SM interest deduction — accepted cost of TFSA sheltering. Goal: compound tax-free, fill TFSA room aggressively, survive AI correction intact.</p>
        <span class="tl-trig">Active while: Nvidia P/E &gt; 40× OR S&P tech weight &gt; 28%</span>
      </div>
    </div>
    <div class="tl-item">
      <div class="tl-dot future">2</div>
      <div class="tl-body">
        <h4>Trigger A — US Rotation: XMU → partial ZUQ or XQLT</h4>
        <p>When AI valuations normalise, rotate a portion of XMU into ZUQ (MSCI USA Quality) or XQLT (sector-neutral quality, 0.15% MER — cheapest). Keep XMU for the defensive core. Quality factor captures companies with strong earnings, low leverage, high ROE — characteristics that lead recoveries.</p>
        <span class="tl-trig">Trigger: Nvidia P/E falls below 30× AND S&P tech weight falls below 25%</span>
      </div>
    </div>
    <div class="tl-item">
      <div class="tl-dot future">3</div>
      <div class="tl-body">
        <h4>Trigger B — EAFE: Add ZIQ alongside XMI</h4>
        <p>ZIQ (MSCI EAFE Quality, BMO) launched October 2024. As its AUM and track record grow, run ZIQ at 10–12% alongside XMI at 12–15%. ZIQ = quality (recoveries); XMI = vol-defence (drawdowns). Together: full-cycle EAFE coverage.</p>
        <span class="tl-trig">Trigger: ZIQ AUM exceeds $400M AND 2-year track record established</span>
      </div>
    </div>
    <div class="tl-item">
      <div class="tl-dot future">4</div>
      <div class="tl-body">
        <h4>Trigger C — Add VGG (Dividend Growth, TFSA)</h4>
        <p>VGG's low yield (1.14%) makes it extremely TFSA-efficient once Broadcom's AI semiconductor revenue normalises. VGG's 10+ year consecutive dividend growth screen selects durable compounders. At normalised valuations, VGG becomes one of the best long-term TFSA holdings.</p>
        <span class="tl-trig">Trigger: Broadcom AI revenue growth &lt; 20% YoY AND Broadcom P/E &lt; 25×</span>
      </div>
    </div>
    <div class="tl-item">
      <div class="tl-dot future">5</div>
      <div class="tl-body">
        <h4>Phase 2 — TFSA Maxed: Switch to Non-Reg SM (Proper)</h4>
        <p>Once TFSA contribution room is fully utilised, new HELOC deployments go to a non-registered account. Criteria flip: CRA deductibility requires income. Canadian eligible dividends become critical (dividend tax credit). VIDY's WHT becomes recoverable. Implement non-reg portfolio: VDY 40% + XDIV 25% + VIDY 25% + XMM 10%. TFSA portfolio remains — never sell it. Let it compound tax-free permanently.</p>
        <span class="tl-trig">Trigger: TFSA contribution room fully deployed</span>
      </div>
    </div>
    <div class="tl-item">
      <div class="tl-dot future">6</div>
      <div class="tl-body">
        <h4>SM Running: Annual Tax Refund → Mortgage Lump Sum</h4>
        <p>SM is now operational in non-reg. Each year: (1) HELOC interest accumulates, (2) tax refund arrives (45% × annual interest), (3) apply refund as mortgage lump sum, (4) new equity unlocks more HELOC room, (5) re-invest. The annual refund grows as HELOC balance grows. At $300K HELOC × 6.5%: ~$8,775 interest/yr → ~$3,950 refund → ~$3,950 additional HELOC room deployed.</p>
        <span class="tl-trig">Ongoing: Annual cycle. File T5 + Schedule 4 every spring.</span>
      </div>
    </div>
    <div class="tl-item">
      <div class="tl-dot future">7</div>
      <div class="tl-body">
        <h4>Long-Term — Full Debt Conversion &amp; Wealth Extraction</h4>
        <p>Mortgage fully paid (20–25 years). HELOC balance now equals original mortgage — all deductible. Three exit options: (A) Hold portfolio, live on dividends, HELOC interest tax-offset by eligible dividend DTC. (B) Sell portfolio, pay HELOC, debt-free with capital gain. (C) Partial paydown, retain core income portfolio. TFSA has been compounding throughout and is the largest account — all withdrawals tax-free forever.</p>
        <span class="tl-trig">Trigger: SM mortgage conversion &gt; 80% AND HELOC balance reducing annually</span>
      </div>
    </div>
  </div>

  <!-- SUMMARY TABLE -->

  <div class="ccrd gold">
    <div class="ccrd-lbl">Two-Portfolio Summary</div>
    <h3>Phase 1 vs Phase 2 — Side by Side</h3>
    <div class="tbl-scroll">
    <table class="dtbl" style="min-width:560px;">
      <thead><tr><th>Attribute</th><th>Phase 1 — TFSA Growth</th><th>Phase 2 — Non-Reg SM</th></tr></thead>
      <tbody>
        <tr><td>Account Type</td><td>TFSA (registered)</td><td>Non-Registered (taxable)</td></tr>
        <tr><td>Interest Deductible?</td><td class="r">No — accepted cost</td><td class="g">Yes — CRA direct-use test met</td></tr>
        <tr><td>Portfolio</td><td>ZLB / XMU / XMI / XMM</td><td>VDY / XDIV / VIDY / XMM</td></tr>
        <tr><td>Yield Focus</td><td class="g">LOW — minimise distributions</td><td class="g">HIGH — income for SM deductibility</td></tr>
        <tr><td>Blended Yield</td><td>~1.75%</td><td>~3.8%</td></tr>
        <tr><td>Canadian Eligible Divs</td><td>Relevant (0% WHT) but secondary</td><td class="g">Critical — 65% eligible divs target</td></tr>
        <tr><td>Foreign WHT</td><td class="r">Permanently lost — minimise</td><td class="a">Partially recoverable — acceptable</td></tr>
        <tr><td>Beta / Volatility</td><td class="g">~0.65 — defensive priority</td><td class="a">~0.80 — moderate</td></tr>
        <tr><td>Nvidia Exposure</td><td class="g">~0.5%</td><td class="g">~0%</td></tr>
        <tr><td>Blended MER</td><td>0.32%</td><td>0.26%</td></tr>
        <tr><td>Tax on Gains/Income</td><td class="g">Zero — all sheltered permanently</td><td class="a">Eligible div DTC ~22–25%; cap gains 23%</td></tr>
        <tr><td>ROC Concern</td><td>Low (min-vol ETFs don't pay ROC)</td><td class="r">Must screen — ROC destroys deductibility</td></tr>
      </tbody>
    </table>
    </div>
  </div>

  <div class="dark-box">
    <strong>The compounding logic of the full two-phase strategy:</strong>
    <ul>
      <li>Phase 1 TFSA portfolio, deployed via HELOC over several years, grows tax-free forever. At 9.3% CAGR, $100K in TFSA doubles every ~7.7 years without ever triggering a taxable event. A $100K position held for 30 years → ~$1.5M, all tax-free on withdrawal.</li>
      <li>Phase 2 SM generates annual tax refunds (~45 cents per dollar of interest) which are recycled into accelerating mortgage paydown. Each refund generates more equity, more HELOC room, more investment — a self-funding acceleration loop.</li>
      <li>The two strategies are complementary: TFSA provides tax-free growth and a cushion of liquid assets; SM provides the annual cash flow engine (tax refunds) that accelerates the mortgage conversion.</li>
      <li>The total wealth advantage vs. a purely passive homeowner compounds significantly over 20–25 years. The magnitude depends on market returns, HELOC rate spreads, and MTR — but at MSCI World historical averages, the combination creates material long-term net worth improvement.</li>
    </ul>
  </div>

  <div class="footnote">
    All ETF data as of March 2026. MERs from provider factsheets. Yields trailing 12-month. Beta estimates from MSCI and provider documentation. Bear market statistics: dot-com (−47%, 40 months — Walter Scott), GFC (−54–58%, 53–64 months — sources vary by gross/net and measurement methodology; used −58%/64mo gross basis), COVID (−34%, 9 months — multiple sources including Funds Society MSCI World analysis). MSCI World 50-yr CAGR ~9.3% for 1975–2024; actual 1986–2025 period (post-index-launch) ~8.9%. Pre-1986 data is MSCI backtested. Annual standard deviation ~15% confirmed by MSCI. Simulation uses transparent assumptions: $500K home, $300K mortgage, 6.5% HELOC, 45% MTR, 25-yr amortisation principal schedule. Rotation triggers are quantitative guidelines — not guaranteed timing signals. This document is for educational purposes only and does not constitute investment, tax, or legal advice. Consult a fee-only CFP, CPA, and/or CFA before implementing any leveraged investment strategy. HELOC interest is not deductible when invested in a TFSA or RRSP under current CRA rules.
  </div>
</div>
</div>

<!-- ══════════════════════════════════════════════════════════ -->

<!-- JAVASCRIPT                                               -->

<!-- ══════════════════════════════════════════════════════════ -->

<script>
mermaid.initialize({startOnLoad:true,theme:'default',flowchart:{useMaxWidth:true,htmlLabels:true,curve:'basis'}});

function show(id,btn){
  document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  if(btn)btn.classList.add('active');
  window.scrollTo({top:0,behavior:'smooth'});
}

// CHART DEFAULTS
Chart.defaults.font.family="'IBM Plex Sans',sans-serif";
const aS={grid:{color:'rgba(0,0,0,0.05)'},ticks:{color:'#7a7060',font:{family:"'IBM Plex Mono',monospace",size:9}},border:{color:'rgba(0,0,0,.1)'}};
const tt={backgroundColor:'#0e1117',titleColor:'#c9a84c',bodyColor:'#c4bba8',borderColor:'#2a2a2a',borderWidth:1,padding:10,titleFont:{family:"'IBM Plex Mono',monospace",size:10},bodyFont:{family:"'IBM Plex Mono',monospace",size:10}};

// HISTORICAL DATA
const hd=[
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

const notable=[
  {y:1975,r:35.4,n:"Recovery from 1973–74 oil crisis bear market",t:"up"},
  {y:1980,r:25.7,n:"Bull market resumes after stagflation era",t:"up"},
  {y:1985,r:40.7,n:"Strong bull — USD weakness, Japan/Europe boom",t:"up"},
  {y:1986,r:41.9,n:"Best year on record — Yen surge vs USD (Plaza Accord effect)",t:"up"},
  {y:1990,r:-17.0,n:"Gulf War, S&L crisis, US recession",t:"dn"},
  {y:2000,r:-13.2,n:"Dot-com bubble begins to burst",t:"dn"},
  {y:2002,r:-19.9,n:"Post-dot-com trough — 3rd consecutive down year",t:"dn"},
  {y:2003,r:33.1,n:"Massive rebound from tech bust",t:"up"},
  {y:2008,r:-40.7,n:"Global Financial Crisis — worst calendar year in 50yr dataset",t:"dn"},
  {y:2009,r:29.9,n:"GFC recovery begins — Fed QE launched",t:"up"},
  {y:2013,r:26.7,n:"Post-GFC bull market fully established",t:"up"},
  {y:2019,r:27.7,n:"Pre-COVID bull — Fed pivot year",t:"up"},
  {y:2020,r:15.9,n:"COVID crash (−34% peak-to-trough) but strong YTD recovery",t:"up"},
  {y:2022,r:-18.1,n:"Rate hike cycle — inflation shock (peak-to-trough −26%)",t:"dn"},
  {y:2024,r:18.7,n:"AI-driven bull market, US mega-cap outperformance",t:"up"},
];

// Chart 1: Historical bar
new Chart(document.getElementById('chartHist'),{type:'bar',data:{
  labels:hd.map(d=>d.y),
  datasets:[
    {label:'Annual Return %',data:hd.map(d=>d.r),backgroundColor:hd.map(d=>d.r>=0?'rgba(26,107,94,0.7)':'rgba(201,76,26,0.7)'),borderColor:hd.map(d=>d.r>=0?'#1a6b5e':'#c94c1a'),borderWidth:1,borderRadius:1},
    {label:'Long-run avg ~9.3%',data:hd.map(()=>9.3),type:'line',borderColor:'rgba(201,168,76,0.7)',borderWidth:2,borderDash:[6,4],pointRadius:0,fill:false}
  ]
},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{labels:{color:'#7a7060',font:{family:"'IBM Plex Mono',monospace",size:9}}},tooltip:{...tt,callbacks:{label:ctx=>` ${ctx.parsed.y>0?'+':''}${ctx.parsed.y.toFixed(1)}%`}}},scales:{x:{...aS,ticks:{...aS.ticks,maxRotation:45}},y:{...aS,ticks:{...aS.ticks,callback:v=>v+'%'}}}}});

// Chart 2: Distribution
const bkts=[{l:'<−30%',mn:-100,mx:-30,c:'rgba(201,76,26,0.85)'},{l:'−30 to −20%',mn:-30,mx:-20,c:'rgba(201,76,26,0.65)'},{l:'−20 to −10%',mn:-20,mx:-10,c:'rgba(201,76,26,0.45)'},{l:'−10 to 0%',mn:-10,mx:0,c:'rgba(201,168,76,0.6)'},{l:'0 to 10%',mn:0,mx:10,c:'rgba(26,107,94,0.45)'},{l:'10 to 20%',mn:10,mx:20,c:'rgba(26,107,94,0.65)'},{l:'20 to 30%',mn:20,mx:30,c:'rgba(26,107,94,0.80)'},{l:'>30%',mn:30,mx:100,c:'rgba(26,107,94,0.95)'}];
new Chart(document.getElementById('chartDist'),{type:'bar',data:{
  labels:bkts.map(b=>b.l),
  datasets:[{label:'Years',data:bkts.map(b=>hd.filter(d=>d.r>=b.mn&&d.r<b.mx).length),backgroundColor:bkts.map(b=>b.c),borderWidth:0,borderRadius:2}]
},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false},tooltip:{...tt,callbacks:{label:ctx=>` ${ctx.parsed.y} years of 50`}}},scales:{x:{...aS,ticks:{...aS.ticks,maxRotation:40,font:{size:8.5}}},y:{...aS}}}});

// Chart 3: Volatility bands
const mean=9.3,sd=15.0;
new Chart(document.getElementById('chartBand'),{type:'bar',data:{
  labels:['−2σ Extreme','−1σ Bad Year','Average','＋1σ Good','＋2σ Great'],
  datasets:[{label:'Expected Return',data:[mean-2*sd,mean-sd,mean,mean+sd,mean+2*sd],backgroundColor:['rgba(201,76,26,0.8)','rgba(201,76,26,0.5)','rgba(201,168,76,0.75)','rgba(26,107,94,0.65)','rgba(26,107,94,0.9)'],borderRadius:3}]
},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false},tooltip:{...tt,callbacks:{label:ctx=>` ${ctx.parsed.y.toFixed(1)}%`}}},scales:{x:{...aS,ticks:{...aS.ticks,maxRotation:30,font:{size:8.5}}},y:{...aS,min:-25,max:45,ticks:{...aS.ticks,callback:v=>v+'%'}}}}});

// Chart 4: Bear markets
const bears=[{n:'1973–74 Oil',m:23,d:-47},{n:'1980–82 Stag.',m:19,d:-26},{n:'1987 Crash',m:4,d:-29},{n:'1990 Gulf',m:9,d:-21},{n:'2000–02 Dot-com',m:31,d:-49},{n:'2007–09 GFC',m:16,d:-57},{n:'2022 Rate Shock',m:12,d:-26}];
new Chart(document.getElementById('chartBear'),{type:'bar',data:{
  labels:bears.map(b=>b.n),
  datasets:[
    {label:'Decline (%)',data:bears.map(b=>b.d),backgroundColor:'rgba(201,76,26,0.6)',borderColor:'#c94c1a',borderWidth:1,borderRadius:2,yAxisID:'y'},
    {label:'Duration (mo)',data:bears.map(b=>b.m),type:'line',borderColor:'#c9a84c',backgroundColor:'rgba(201,168,76,0.1)',borderWidth:2,pointRadius:4,pointBackgroundColor:'#c9a84c',yAxisID:'y2',fill:false}
  ]
},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{labels:{color:'#7a7060',font:{family:"'IBM Plex Mono',monospace",size:9}}},tooltip:{...tt}},scales:{x:{...aS,ticks:{...aS.ticks,maxRotation:30,font:{size:8.5}}},y:{...aS,position:'left',ticks:{...aS.ticks,callback:v=>v+'%'}},y2:{...aS,position:'right',grid:{display:false},ticks:{...aS.ticks,callback:v=>v+'mo'}}}}});

// Chart 5: Rolling 10-yr
const ry=[],rv=[];
for(let i=9;i<hd.length;i++){const sl=hd.slice(i-9,i+1);let c=sl.reduce((a,d)=>a*(1+d.r/100),1);c=(Math.pow(c,0.1)-1)*100;ry.push(hd[i].y);rv.push(+c.toFixed(2));}
new Chart(document.getElementById('chartRoll'),{type:'line',data:{
  labels:ry,
  datasets:[
    {label:'Rolling 10-yr CAGR',data:rv,borderColor:'#1a6b5e',backgroundColor:'rgba(26,107,94,0.08)',borderWidth:2,pointRadius:2,fill:true,tension:0.3},
    {label:'Long-run avg 9.3%',data:ry.map(()=>9.3),borderColor:'rgba(201,168,76,0.6)',borderWidth:1.5,borderDash:[5,5],pointRadius:0,fill:false}
  ]
},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{labels:{color:'#7a7060',font:{family:"'IBM Plex Mono',monospace",size:9}}},tooltip:{...tt,callbacks:{label:ctx=>` ${ctx.parsed.y.toFixed(1)}%`}}},scales:{x:{...aS,ticks:{...aS.ticks,maxRotation:45,font:{size:8.5}}},y:{...aS,ticks:{...aS.ticks,callback:v=>v+'%'}}}}});

// Notable years table
const tb=document.getElementById('notableBody');
notable.forEach(r=>{
  const bw=Math.min(Math.abs(r.r)/42*100,100),bc=r.t==='up'?'#1a6b5e':'#c94c1a',sign=r.r>0?'+':'';
  tb.innerHTML+=`<tr><td style="font-family:'IBM Plex Mono',monospace;color:#7a7060;font-size:11px">${r.y}</td><td><span class="pill ${r.t==='up'?'up':'dn'}">${sign}${r.r}%</span></td><td style="font-size:12px;color:#7a7060">${r.n}</td><td><span class="mini-bar" style="width:${bw}%;background:${bc};opacity:.65"></span></td></tr>`;
});

// SIMULATION
const scenarios={
  base:{lbl:'Base (~9.3% CAGR)',col:'#1a6b5e',ret:[8.5,22.1,14.3,-18.5,11.2,27.4,9.8,15.6,-8.2,19.3,12.7,-35.0,32.1,18.4,11.0,7.5,-14.2,28.9,16.3,21.1]},
  conservative:{lbl:'Conservative (~7.0% CAGR)',col:'#4a6a8a',ret:[6.2,14.1,9.5,-18.5,7.8,18.2,6.4,10.3,-8.2,12.1,8.6,-35.0,24.5,11.8,7.2,5.1,-14.2,20.3,10.1,14.5]},
  optimistic:{lbl:'Optimistic (~11.0% CAGR)',col:'#8a5a10',ret:[11.2,28.5,18.6,-18.5,14.8,33.2,13.1,19.8,-8.2,25.1,16.2,-35.0,41.2,24.3,14.5,10.2,-14.2,36.8,21.4,27.9]}
};

let simCI=null;
function fmt(n){'use strict';return'$'+Math.abs(n).toLocaleString('en-CA',{maximumFractionDigits:0});}

function buildSim(k){
  const ret=scenarios[k].ret;
  let mortgage=300000,heloc=0,portfolio=0,cumRef=0;
  const rows=[];
  for(let i=0;i<20;i++){
    const yr=2026+i,r=ret[i];
    const prin=4800+i*180;
    mortgage=Math.max(0,mortgage-prin);
    heloc+=prin;
    portfolio=portfolio*(1+r/100)+prin;
    const interest=heloc*0.065,refund=interest*0.45;
    cumRef+=refund;
    mortgage=Math.max(0,mortgage-refund);
    const homeEq=500000-mortgage,netW=homeEq+portfolio-heloc;
    rows.push({yr,r,mortgage:Math.round(mortgage),heloc:Math.round(heloc),portfolio:Math.round(portfolio),interest:Math.round(interest),refund:Math.round(refund),cumRef:Math.round(cumRef),netW:Math.round(netW),isCrash:r<-10,isBull:r>20});
  }
  return rows;
}

function renderSim(k){
  const rows=buildSim(k),col=scenarios[k].col;
  document.getElementById('simTitle').textContent='Smith Maneuver — '+scenarios[k].lbl;
  const ctx=document.getElementById('simChart').getContext('2d');
  if(simCI)simCI.destroy();
  const noS=rows.map((_,i)=>500000-Math.max(0,300000-(4800+i*180)*(i+1)));
  simCI=new Chart(ctx,{type:'line',data:{labels:rows.map(r=>r.yr),datasets:[
    {label:'Portfolio Value',data:rows.map(r=>r.portfolio),borderColor:col,backgroundColor:col+'18',borderWidth:2.5,pointRadius:4,pointBackgroundColor:col,fill:true,tension:0.2},
    {label:'HELOC Balance',data:rows.map(r=>r.heloc),borderColor:'rgba(201,76,26,0.7)',borderWidth:1.5,borderDash:[5,4],pointRadius:2,fill:false,tension:0.2},
    {label:'Net Wealth (Strategy)',data:rows.map(r=>r.netW),borderColor:'#c9a84c',borderWidth:2.5,pointRadius:3,fill:false,tension:0.2},
    {label:'Home Equity Only (No SM)',data:noS,borderColor:'rgba(122,112,96,0.4)',borderWidth:1.5,borderDash:[3,6],pointRadius:0,fill:false,tension:0.3}
  ]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{labels:{color:'#7a7060',font:{family:"'IBM Plex Mono',monospace",size:9},padding:12}},tooltip:{...tt,callbacks:{label:ctx=>` ${ctx.dataset.label}: ${fmt(ctx.parsed.y)}`}}},scales:{x:{...aS},y:{...aS,ticks:{...aS.ticks,callback:v=>'$'+(v/1000).toFixed(0)+'K'}}}}});

  let html=`<table class="sim-tbl"><thead><tr><th>Year</th><th>Return</th><th>Portfolio</th><th>HELOC Bal</th><th>Interest</th><th>Tax Refund</th><th>Mortgage</th><th>Net Wealth</th></tr></thead><tbody>`;
  rows.forEach(r=>{
    const rc=r.r>=0?'pos':'neg',cls=r.isCrash?'crash':r.isBull?'bull':'',sign=r.r>0?'+':'';
    html+=`<tr class="${cls}"><td>${r.yr}${r.isCrash?' 🔻':r.isBull?' 🚀':''}</td><td class="${rc}">${sign}${r.r.toFixed(1)}%</td><td class="pos">${fmt(r.portfolio)}</td><td class="neg">${fmt(r.heloc)}</td><td class="neutral">${fmt(r.interest)}</td><td class="pos">${fmt(r.refund)}</td><td>${fmt(r.mortgage)}</td><td class="${r.netW>0?'pos':'neg'}">${fmt(r.netW)}</td></tr>`;
  });
  const f=rows[19];
  html+=`<tr><td><strong>Final / Cumulative</strong></td><td>—</td><td>${fmt(f.portfolio)}</td><td>${fmt(f.heloc)}</td><td>—</td><td>${fmt(f.cumRef)} total</td><td>${fmt(f.mortgage)}</td><td>${fmt(f.netW)}</td></tr></tbody></table>`;
  document.getElementById('simTableWrap').innerHTML=html;
}

function switchSim(k,btn){
  document.querySelectorAll('.tbtn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  renderSim(k);
}

renderSim('base');
</script>

</body>
</html>