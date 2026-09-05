# SURGE

**Turn regulatory deadlines into executable operations.**

SURGE is an operations command center built for the Razorpay AI Buildathon 2026 (Open Track). It answers a specific problem: when a fintech has to re-verify (re-KYC) a large batch of merchants before a hard regulatory deadline, and only has a small field workforce to do it, how do you decide who gets visited first, how you allocate agents, and whether you'll actually make the deadline?

The demo scenario: **500 merchants** need re-verification, **12 field agents** are available, and there are **9 days** left before the compliance deadline (15 Sep 2026). SURGE turns that into a prioritized, capacity-aware operational plan — and lets you see the impact of every lever (headcount, routing, document quality, repeat visits) before you commit to it.

> All data in this build is **synthetic/simulated**, seeded for a reproducible demo. Nothing here is real Razorpay merchant or operational data.

## What it does

SURGE is organized as one continuous story, not a pile of disconnected screens:

| Screen | Question it answers |
|---|---|
| Command Center | What needs attention right now? |
| AI Priority | Who should we handle first? |
| Field Operations | How should we allocate our workforce? |
| Live Map | Where should agents go? |
| Document Copilot | Can we prevent a failed visit before it happens? |
| What-If Simulator | What happens if capacity or conditions change? |
| Merchant Intelligence, Compliant-Path Intelligence, Analytics, Alerts | Secondary/deep-dive screens, tucked under "More" |

Each screen exists to support one decision, not to show off data.

### Core capabilities

- **Deterministic priority scoring** — every merchant gets an explainable priority score from revenue exposure, deadline pressure, prior contact attempts, and document readiness. A live **Priority Focus** slider re-weights the score between "Deadline Urgency" and "Business Impact" and re-ranks the list in real time (with a smooth FLIP re-order animation, not a jarring re-render).
- **Capacity-constrained optimization engine** — a real day-by-day simulation of what a field workforce can clear under different routing strategies, document-quality assistance, and compliant-path offload, not a hardcoded number. Baseline vs. optimized plans are computed from the same model.
- **What-If Simulator** — three live controls (Field Agents 2–20, Days Remaining 1–15, Repeat Visit Rate 0–30%) that recompute projected completion, critical backlog, required agents, and deadline status on every change.
- **Document Copilot** — real client-side computer vision (Canvas 2D pixel analysis: Laplacian edge-variance for blur, luminance averaging for exposure) flags bad document captures *before* an agent leaves for a failed visit. A secondary fuzzy name-matching tool (Levenshtein distance) checks identity-field consistency.
- **Compliant-Path Intelligence** — a rule-based eligibility engine modeled on RBI-style light-KYC criteria (turnover and document-readiness thresholds), so eligible merchants can be offloaded to a remote path instead of consuming field-agent capacity.
- **Live Map** — an SVG operational map of regional hubs, agent positions, and merchant clusters, with routes that visibly recalculate when a plan is optimized.
- **Native SVG analytics** — four focused charts (baseline vs. SURGE completion, agent utilization, critical-backlog trend, zone performance), hand-rolled in inline SVG with **zero external chart-library dependency**, so they always render, including fully offline.
- **Cinematic intro** — a short, project-specific animated sequence (merchants → agents → deadline → backlog → SURGE analyzing → prioritizing → optimizing → plan) built in Canvas/SVG/CSS, with a "Skip Intro" and "Enter Surge" control, and a full `prefers-reduced-motion` fallback.
- **Ambient background** — a subtle, always-on network visualization (merchant/agent nodes, flowing routes, verification pulses) that runs behind every screen once you're in the app, using the same zone geography as the Live Map, and adapts slightly per screen (e.g. stronger route activity on Live Map, agent-movement emphasis on Field Operations).

## Architecture

SURGE is intentionally a **single self-contained HTML file** — `index.html` — with no build step, no server, and no external runtime dependencies beyond Google Fonts. This was a deliberate choice for a hackathon MVP: every "AI" or optimization feature is either a genuine deterministic algorithm or genuine client-side computer vision running in the browser, not a mocked API call, so the whole thing is inspectable in one file and has nothing that can fail from a missing backend or a flaky third-party API during a live demo.

- **Frontend**: vanilla JavaScript SPA, hash-based client-side routing, no framework.
- **"Backend"**: none — by design. All computation (priority scoring, capacity simulation, document analysis, fuzzy matching) runs client-side in real time.
- **Data**: a seeded pseudo-random generator (`mulberry32`) produces a deterministic, reproducible synthetic dataset (500 merchants, 12 agents, 6 regional zones across South/West India) every time the page loads — the same seed, so the demo scenario is stable and repeatable.
- **Styling**: CSS custom properties with full light/dark theming (`prefers-color-scheme` + manual override), responsive layout including a mobile slide-in navigation drawer.
- **Fonts**: Inter (UI), Big Shoulders Display (intro/logo only), IBM Plex Mono (data/IDs) — loaded from Google Fonts.

### File structure

```
SURGE/
├── index.html              # the entire application
├── docs/
│   └── research/            # problem-selection research that led to the SURGE concept
└── README.md
```

## How to run it

No install, no build, no dependencies to fetch.

**Option 1 — just open it:**
Double-click `index.html`, or open it directly in a browser (`file://` works, since there are no server-side calls).

**Option 2 — serve it locally (recommended, avoids any browser `file://` restrictions):**
```bash
git clone https://github.com/sharaniv166/SURGE.git
cd SURGE
python3 -m http.server 8000
# then open http://localhost:8000
```
Any static file server works equally well (`npx serve`, `php -S`, etc.) — there is nothing to configure, no environment variables, and no API keys required.

## Current limitations

Being upfront about what this build is and isn't:

- **No backend or database.** This is a client-side simulation of the operational logic a real SURGE product would run against live merchant/case data through a backend and database. The algorithms (priority scoring, capacity simulation, compliant-path rules) are real and would carry over directly to a production backend; what's missing is persistence, auth, and real data ingestion.
- **No live Razorpay API integration.** The scenario is entirely synthetic and seeded for demo reproducibility — it does not read from or write to any real Razorpay system.
- **Single-session only.** There is no account system or saved state across sessions; every page load regenerates the same seeded dataset.
- **Document analysis is quality-focused, not identity-verification-grade.** The Canvas CV checks (blur, exposure) and fuzzy name matching are real, working client-side signal-processing, but they are not a substitute for a production KYC/OCR pipeline.

## Credits

Built for the Razorpay AI Buildathon 2026, Open Track. See `docs/research/` for the problem-space research that led to the merchant re-KYC compliance-deadline problem this project addresses.
