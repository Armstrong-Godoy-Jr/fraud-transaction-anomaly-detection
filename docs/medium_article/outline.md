# Medium Article — Outline & Tracker

**Working title:** _TBD (revisit after Phase 4 once the model's "story" is clear)_
**Format:** Single long-form article
**Status:** Not started

## Purpose

Document the full build of this fraud detection project as a portfolio narrative — not a tutorial, but a "here's how a fraud analytics data scientist actually works" story. Written for two audiences at once: hiring managers skimming for signal, and other DS-transition folks who want the real workflow, not just `model.fit()`.

## Section-by-section plan

Each section is drafted in its own file in this folder right after the corresponding phase wraps, then assembled into the final article at the end.

| Section | Maps to | File | Status |
|---|---|---|---|
| Hook / why this project | Intro | `intro.md` | 🚧 Draft v1 |
| The business problem | Phase 0 | `phase0_charter.md` | 🚧 Draft v1 |
| Setting up like a real team would | Phase 1 | `phase1_setup.md` | ⬜ |
| What the data actually shows | Phase 2 | `phase2_eda.md` | ⬜ |
| Finding signal: feature engineering | Phase 3 | `phase3_features.md` | ⬜ |
| Building and evaluating the model | Phase 4 | `phase4_modeling.md` | ⬜ |
| From score to decision: the strategy layer | Phase 5 | `phase5_strategy.md` | ⬜ |
| Getting it out of the notebook: API + Docker | Phase 6 | `phase6_deployment.md` | ⬜ |
| Keeping it honest: monitoring | Phase 7 | `phase7_monitoring.md` | ⬜ |
| What I'd do differently / lessons | Closing | `closing.md` | ⬜ |

## Notes on tone/content per section (fill in as we go)

- Capture **decisions and trade-offs**, not just what we built (e.g. why cost-sensitive evaluation over plain F1, why this threshold and not another)
- Include 1–2 concrete artifacts per section where useful (a chart, a code snippet, a table) — pull directly from what we build in the repo, don't fabricate numbers
- Flag anywhere we hit a "real" production concern (class imbalance, latency, drift) so the article reads as lived experience, not a course recap
- Keep synthetic-data disclaimer consistent with the repo's README

## Assembly checklist (do at the end)

- [ ] All section files drafted
- [ ] Consistent voice/tense pass
- [ ] Add real screenshots/plots exported from the repo
- [ ] Cross-link to the GitHub repo
- [ ] Final title + subtitle
- [ ] Publish, then link back into the repo README
