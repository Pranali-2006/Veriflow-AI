<div align="center">

# VeriFlow AI

**Intelligent document verification & application readiness checker**

Built for **HACK-VERSE 2026** · Problem Statement 1 · **Team ByteForce**

[![Live demo](https://img.shields.io/badge/Live_demo-online-2563EB?style=flat-square)](https://pranali-2006.github.io/Veriflow-AI/)
[![License: MIT](https://img.shields.io/badge/License-MIT-0E9F6E?style=flat-square)](LICENSE)
[![Built with](https://img.shields.io/badge/Built_with-Vanilla_JS-D97706?style=flat-square)](#tech-stack)
[![No backend](https://img.shields.io/badge/Backend-none_required-7C3AED?style=flat-square)](#privacy)

[**Open the live demo →**](https://pranali-2006.github.io/Veriflow-AI/)

</div>

---

## The problem

Every loan file, KYC pack and insurance claim arrives as a pile of scanned documents. Someone has
to open each one, check it is the right document, check the name matches the form, check the
address proof is recent enough, check nothing has been submitted twice — and then decide whether
the application can move forward. It is slow, it is inconsistent between reviewers, and the
applicant usually finds out something was missing days later.

## What VeriFlow AI does

VeriFlow AI takes the documents for one application and answers three questions in a few seconds:

1. **Is anything missing?** Against a configurable requirement list, not a hardcoded one.
2. **Is what's here usable?** Quality, legibility, expiry, name match, duplicates, cross-document consistency.
3. **How close is this file to ready?** One weighted readiness score, with every point traced back
   to the rule that added or removed it.

Then it tells the reviewer what to fix first, and — this is the part judges tend to ask about —
shows what the score *would* be after each fix, before anyone does the work.

## Features

| | |
|---|---|
| **Readiness score** | Weighted across the required document set, not a flat count |
| **8-stage pipeline** | Intake → security gate → classification → extraction → quality → rules → cross-check → scoring |
| **What-if simulator** | Toggle each issue as "fixed" and watch the projected score move |
| **Written AI insight** | Assembled from the actual results, not a canned paragraph |
| **Cross-document consistency** | Compares the same field across documents instead of checking each alone |
| **Risk breakdown** | 0–100, every point attributed to a named rule |
| **Security centre** | SHA-256 fingerprints, file-type gate, size limits, privacy mode |
| **Audit log** | Every action in the session, exportable |
| **Reports** | CSV export and a print-ready view |
| **Configurable rules** | Quality threshold, name-similarity threshold, address-proof age — all live-editable |
| **Trilingual UI** | English, हिंदी, मराठी |
| **Light & dark** | Follows the toggle, remembered per device |

## What is genuinely computed vs. simulated

Judges ask this, so it is stated up front rather than buried:

**Really computed in the browser**

- Name matching — part-by-part string distance against the application record
- Duplicate detection — filename and field-signature comparison
- Readiness — weighted across the live requirement set
- Risk score — every rule reads the thresholds from the Settings page
- File fingerprints — SHA-256 via the Web Crypto API

**Labelled simulation**

- The OCR / extraction stage. The app never claims a real model is running, the stage is badged in
  the UI, and every extracted field stays editable so the rest of the pipeline works on real input.

## Privacy

Documents are read inside the browser tab. Nothing is uploaded, there is no server, no API key and
no network call. Applications, requirements, issues, audit entries, language and theme live in
`localStorage` on the device. Of a document, only the filename, size and verification outcome are
kept — never the contents.

## Tech stack

- **HTML, CSS, vanilla JavaScript** — no framework, no build step, no dependencies
- **Web Crypto API** for SHA-256 fingerprints
- **`localStorage`** for persistence
- **Three files** — markup, styles and logic kept separate; no bundler, nothing to compile

## Run it locally

Clone and open — that is the whole setup.

```bash
git clone https://github.com/Pranali-2006/Veriflow-AI.git
cd veriflow-ai
```

Then serve the folder — with separate CSS and JS files a local server is the reliable way to open it:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Double-clicking `index.html` usually works too, but some browsers restrict `file://` pages.

## Deploy

Hosted on GitHub Pages from the `main` branch root. Any static host works — Netlify, Vercel,
Cloudflare Pages — because there is nothing to build.

## Try it in 30 seconds

1. Open the live demo.
2. Pick a scenario from the dropdown on the dashboard.
3. Press **Run full AI demo** and watch the pipeline.
4. Open **Verification → What-if simulator** and toggle an issue to see the projected score.

## Project structure

```
veriflow-ai/
├── index.html      # markup — layout, pages, dialogs
├── style.css       # design tokens, components, light/dark, responsive, print
├── script.js       # state, verification engine, rules, scoring, i18n
├── README.md
├── LICENSE
├── .gitignore
└── .nojekyll       # tells GitHub Pages to serve the files as-is
```

`script.js` is organised top-down: config and `TEAM` first, then state and storage, then the
verification pipeline, then rendering, then event wiring and `initApp()` at the bottom.

## Team ByteForce

| Member | Role | GitHub |
|---|---|---|
| Pranali Dhodi | Team lead · Frontend & AI logic | [@Pranali-2006](https://github.com/Pranali-2006) |
| Prachi Giri | Developer | _add handle_ |
| Tejas Savale | Developer | _add handle_ |

## License

[MIT](LICENSE) © 2026 Team ByteForce
