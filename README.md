# The Smith Maneuver — Complete Visual Guide

A single-page, self-contained **visual guide to the Smith Manoeuvre** — the
Canadian strategy that converts a non-deductible mortgage into a tax-deductible
investment loan using a readvanceable mortgage / HELOC.

The guide lives in **[`index.html`](index.html)**: a standalone page (no build
step, no dependencies beyond two CDN scripts) combining Mermaid flow diagrams,
Chart.js market-data visualisations, and an illustrative 20-year simulation.

> ⚠️ The guide is an **HTML page**, not Markdown. GitHub's README renderer
> strips the `<script>`/`<style>` it relies on, so view it as a real page:
> open `index.html` locally, or enable **GitHub Pages** for this repo to host it
> at `https://latetedemelon.github.io/SmitheManeuver/`.

## 🧮 Companion: the interactive calculator

This guide explains the strategy; its companion runs it on *your* numbers.

**→ [`heloc_projections`](https://github.com/latetedemelon/heloc_projections)** is
a month-by-month projection tool with an interactive web calculator and a Python
Excel-workbook generator, both driven by one model that's held cent-for-cent
identical by an automated test suite. The guide's masthead and the section after
the 20-year simulation link straight to it.

| | |
|---|---|
| 📖 **This repo** — *explain* the strategy | the visual guide |
| 🧮 **`heloc_projections`** — *model* the strategy | the interactive calculator + spreadsheet engine |

## What's inside the guide

| Part | Contents |
|---|---|
| **One — How It Works** | The TFSA variant plus a 6-step lifecycle of the classic maneuver (Mermaid flowcharts): setup, first draw, tax mechanics, refund recycling, the compounding loop, end-game debt conversion. |
| **Two — Market Returns & Volatility** | 50 years of MSCI World annual returns, the return distribution, ±1σ/±2σ volatility bands, the bear-market profile, and rolling 10-year CAGR. |
| **Three — 20-Year Simulation** | An illustrative year-by-year projection with base / conservative / optimistic scenarios and stylized crash years. |
| **Seven–Ten — ETF Framework & Roadmap** | A factor-strategy assessment, an AI-bubble exposure audit, TSX-listed ETF candidates, Phase 1 (TFSA) and Phase 2 (non-registered SM) model portfolios, and a 7-stage quantitative transition roadmap. |

## Viewing locally

```bash
git clone https://github.com/latetedemelon/SmitheManeuver.git
cd SmitheManeuver
python3 -m http.server 8000   # then visit http://localhost:8000/
```

(Mermaid, Chart.js, and the web fonts load from CDNs, so the first load needs
internet access.)

---

**Educational purposes only — not financial, legal, or tax advice.** The Smith
Manoeuvre is a leveraged investing strategy and can lose money. HELOC interest
is **not** deductible when the borrowed funds are contributed to a TFSA or RRSP;
only properly structured non-registered investment-loan interest may qualify
under CRA rules. Consult a fee-only financial planner and a qualified tax
professional before implementing any leveraged strategy.
