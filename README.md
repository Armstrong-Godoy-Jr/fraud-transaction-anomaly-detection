# Fraud Transaction Anomaly Detection

> Portfolio project simulating an end-to-end fraud analytics workflow for debit/payment transactions, modeled on industry practice at a Canadian financial institution.

## Project Status
🚧 **Phase 0 — Project Charter** (in progress)

See [`docs/charter.md`](docs/charter.md) for scope, objectives, and success criteria.

## Overview

This project simulates the full lifecycle of a fraud detection solution as it would be built by a Fraud Analytics team at a bank: from problem framing through modeling, deployment simulation, and ongoing monitoring. It's built on synthetic transactional data designed to mimic real debit card transaction patterns, fraud typologies, and the operational constraints of a production fraud system.

## Goals

- Detect anomalous/fraudulent debit transactions using advanced analytics
- Translate model outputs into an operational mitigation strategy (thresholds, review queues, blocking rules)
- Simulate deployment of the scoring pipeline
- Build monitoring for ongoing model and strategy performance
- Document everything to production/audit standards

## Repository Structure

```
├── docs/                  # Charter, model cards, architecture decisions
├── data/
│   ├── raw/               # Synthetic raw transaction data
│   └── processed/         # Feature-engineered datasets
├── notebooks/             # Exploratory and analytical notebooks
├── src/
│   ├── features/          # Feature engineering code
│   ├── models/             # Model training/evaluation code
│   ├── pipeline/          # Scoring/inference pipeline (batch + API sim)
│   └── monitoring/        # Drift detection, performance tracking
├── dashboards/             # Analyst-facing dashboard app
├── tests/                  # Unit tests
└── .github/workflows/      # CI (lint, test)
```

## Tech Stack

- **Language:** Python (pandas, numpy, scikit-learn), PySpark-style patterns for transaction-scale processing
- **SQL:** for transactional data exploration and feature queries
- **Dashboarding:** to be determined in Phase 7
- **CI/CD:** GitHub Actions

## Roadmap

| Phase | Description | Status |
|---|---|---|
| 0 | Project Charter | 🚧 In progress |
| 1 | Data & Environment Setup | ⬜ Not started |
| 2 | Exploratory Data Analysis | ⬜ Not started |
| 3 | Feature Engineering | ⬜ Not started |
| 4 | Modeling & Theoretical Performance | ⬜ Not started |
| 5 | Detection Strategy Layer | ⬜ Not started |
| 6 | Deployment: API, Containerization & Versioning | ⬜ Not started |
| 7 | Monitoring & Dashboard | ⬜ Not started |
| 8 | Documentation & Governance | ⬜ Not started |

**Phase 6 detail:** wrap the trained model in a scoring API (FastAPI), containerize it with Docker, and version the resulting image — so the model is something another person (or system) could actually call, not just a `.pkl` file sitting in a notebook. This mirrors "déployer en production des modèles" from the target job description, and the same Dockerfile pattern would carry over to a real cloud target like Azure or IBM Cloud Pak for Data.

## Companion Article

This project is being written up as a long-form Medium article in parallel with the build — see [`docs/medium_article/`](docs/medium_article/) for the running draft. Each phase gets its section drafted right after that phase's technical work is done, so the reasoning and decisions are captured fresh rather than reconstructed at the end.

## Disclaimer

This project uses entirely synthetic data. It does not represent, reference, or use any real financial institution's proprietary data, models, or systems. It is built as an educational/portfolio simulation of industry practice.

## License

See [LICENSE](LICENSE).
