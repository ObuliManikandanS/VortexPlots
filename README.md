# Vortexplots

Interactive Tamil Nadu Property estimation platform with locality-based ₹/sq ft benchmarks, ML prediction, budget analysis, comparison dashboard, and PDF report export.

# VortexPlots

Tamil Nadu property research workspace. This is a working implementation with explicit data and deployment limits, not a completed statewide valuation service.

## Available in this version

- Responsive district explorer with Leaflet / OpenStreetMap and 38 district reference polygons.
- 185 selected search localities, district / locality routes and a five-property-type estimator.
- Strict separation of asking, transaction, guideline and user-scenario prices.
- Area conversion (sq ft, sq m, cent, acre, ground).
- Carpet / built-up / super built-up analysis, loading factor, space efficiency and true usable cost.
- Public A4 PDF generation with selectable rupee text, formulas, dataset status, page numbers and district map snapshots for location/property reports.
- Netlify Identity sign-up, login, recovery and protected records integration.
- Account portfolio and report snapshot APIs, report filters and owner-scoped deletion.
- Data coverage and source registry views.
- Observation ingestion with raw-record preservation, normalization, duplicate removal, provenance/date validation and atomic replacement.
- Offline Python training workflow: median, ridge and random forest comparisons, district holdout, future holdout, evaluation registry. Training does not deploy a model.

## Current evidence

Dataset version: tn-2026-09-20.4. Accepted price observations: **0**. Model version and evaluation metrics: **unavailable**. No verified transaction, guideline or asking prices are shipped. Manual rates are unverified user scenarios. An unknown value remains null, never zero or an invented district average.

38 district names are checked against https://igod.gov.in/sg/TN/E042/organizations. Boundary source, MIT license and limitations are in public/maps/. Polygons contain mixed source vintages through 2022 and are simplified for visualization. They are not certified current or cadastral boundaries. Localities are a selected directory, not an official exhaustive village, ward, municipality or taluk register. Exact locality coordinates and historical prices are not populated.

## Run and deploy

Node 22+; pnpm (lockfile included).

    pnpm install
    pnpm build:netlify
    npx netlify-cli login
    npx netlify-cli link
    npx netlify-cli deploy --build --prod

Choose the intended Netlify project when linking. Do not overwrite another project. New-project creation and Identity activation require the account owner to complete setup. Identity does not work in local Netlify development. Enable it in the project's Identity settings, then test email confirmation, password recovery and two separate accounts in a deployed environment. Netlify Blobs provides owner-scoped JSON storage. Secrets belong in runtime settings, never in source.

The existing .openai project binding was not modified. That prior Sites project returned “not found” in this session. The Netlify delivery archive excludes Sites-specific runtime metadata; this archive is for the Netlify target.

## Verification performed

- Next.js production build and TypeScript check.
- Six automated valuation / conversion / invalid-input tests.
- Browser render of district map and area calculator, including an invalid area hierarchy.
- PDF renderer sample generated and both A4 pages visually inspected, including rupee glyphs and district geometry.
- 38 unique polygons matched to the 38 directory district names.

The final production build must pass before publishing. Netlify production smoke testing, cross-user authorization, email delivery, mobile-device testing and storage persistence tests remain blocked until deployment and Identity activation.

## Known incomplete requirements

- Verified statewide prices and full administrative/locality coverage; dated historical series.
- Current official boundaries, exact locality points, taluk overlays and supported price heatmaps.
- A trained and evaluated production ML model, calibrated uncertainty and inference service.
- Relational database integration (the current private store is Netlify Blobs; old D1 migrations are legacy).
- Background ingestion scheduling, saved-search alerts and operational monitoring.
- Full authenticated draft autosave and offline synchronization.
- Portfolio space-efficiency aggregation and charted price distributions.
- Tamil-language names/fonts and verified property-type comparisons.

## Training

Install scripts/requirements-training.txt in a Python environment. Start with data/training-template.csv and legally reusable, reviewed observations. Run scripts/train.py with the input CSV. The workflow deliberately blocks insufficient datasets and never substitutes synthetic examples for market observations. Its artifacts are evaluation-only and require separate review before production integration.
