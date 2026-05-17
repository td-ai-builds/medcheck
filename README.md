# MedCheck — Drug Interaction Checker

> Check drug-drug interactions in seconds. Powered by the US National Library of Medicine.

## The problem

Patients and healthcare professionals regularly need to check whether two medications are safe to take together. Existing tools either bury the answer in dense clinical text, require a login, or serve the information inside apps that aren't quick to access. There's no simple, fast, open tool that returns a clear interaction summary with a severity level.

## What it does

Enter two drug names → MedCheck resolves them against the RxNorm database, queries the NLM RxNav interaction API, and returns a plain-English summary of any known interactions — severity-coded (Major / Moderate / Minor) and sourced by database (DrugBank, ONCHigh, NDF-RT). A direct link to Drugs.com lets users read the full clinical detail if needed.

## Live demo

[https://td-ai-builds.github.io/medcheck](https://td-ai-builds.github.io/medcheck)

## PM notes

- **Hypothesis:** A fast, no-login interaction checker with a clear severity signal will be more useful to time-pressed users than navigating a full pharmacy reference site.
- **What I cut from scope:** Multi-drug checks (3+), allergy/food interaction lookups, patient-facing dosing advice, saved history, and any backend. Week 1 is a single HTML file — the trust comes from using official NLM data, not from engineering complexity.
- **Known limitations:** RxNav only surfaces interactions that have been formally documented in its source databases. Absence of a result does not mean an interaction is safe — always confirm with a pharmacist. The app uses generic drug names; brand names (e.g. "Coumadin" for warfarin) may not resolve correctly.
- **What I'd do differently:** I'd test with 5–10 real drug pairs against a pharmacist's reference before shipping, to validate that the RxNav data matches what practitioners expect to see. I did the API research first; clinical validation should have been parallel.

## How to run it locally

1. Clone this repo
2. Open `index.html` in any browser
3. No server, no dependencies, no API key required

## Stack

- **Frontend:** HTML + CSS + vanilla JS (single file, no framework)
- **Data:** [NLM RxNorm API](https://rxnav.nlm.nih.gov/RxNormAPIs.html) (name → RxCUI resolution) + [NLM RxNav Interaction API](https://rxnav.nlm.nih.gov/InteractionAPIs.html) (interaction lookup)
- **Hosting:** GitHub Pages
- **Built with:** Claude Code

## Data sources

All interaction data is drawn from the US National Library of Medicine's RxNav service, which aggregates from:
- **DrugBank** — comprehensive drug interaction database
- **ONCHigh** — ONC high-priority drug-drug interactions
- **NDF-RT** — National Drug File Reference Terminology

No data is scraped. All API calls are made directly from the browser to public NLM endpoints.
