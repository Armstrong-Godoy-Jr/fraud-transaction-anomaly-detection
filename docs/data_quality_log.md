# Data Quality Log — Injection Spec

> Written BEFORE data generation, as a design spec (not an after-the-fact log).
> Purpose: document every deliberate data quality issue injected into the "realism layer,"
> whether it's informative (tied to fraud) or pure noise, and why — so EDA/modeling
> decisions can later be checked against this ground truth.

## Legend
- **Informative**: correlated with `is_fraud` / `fraud_typology` — mirrors real-world signal hidden in data quality
- **Noise**: unrelated to fraud — mirrors ordinary system/operational messiness

## Injected Issues by Field

### accounts

| Field | Issue | Type | Rationale |
|---|---|---|---|
| `income_bracket` | Missing (~15% overall) | **Informative** (higher missing rate on fraudulent accounts) | Synthetic/stolen identities often have incomplete profile data at account opening |
| `employment_status` | Missing (~15% overall) | **Informative** (same accounts as above) | Same rationale — bundled with income to avoid two independent "tells" |
| `province` | Occasional inconsistent casing/abbreviation (`QC` vs `Quebec` vs `québec`) | Noise | Realistic multi-system data entry inconsistency |

### merchants

| Field | Issue | Type | Rationale |
|---|---|---|---|
| `merchant_name` | Inconsistent casing, accents dropped/kept inconsistently | Noise | Realistic encoding/entry inconsistency, especially for French names |
| `merchant_risk_tier` | Missing for ~5% of merchants | **Informative** (new/unverified merchants disproportionately missing this) | Mirrors real onboarding lag for new merchants — also disproportionately used in card-testing fraud |

### transactions

| Field | Issue | Type | Rationale |
|---|---|---|---|
| `merchant_id` | ~2% reference a merchant_id not present in `merchants` | Noise | Simulates join/system-sync lag between processor and internal merchant table |
| `device_id` | Missing for older/in-branch-opened accounts | Noise | Not every channel historically captured device data |
| `timestamp` | Mixed date formats across a simulated "system migration" date | Noise | Realistic schema drift over time |
| `amount` | Occasional currency format inconsistency (`$45.00` / `45,00` / `45.0`) | Noise | Multi-source formatting inconsistency |
| `amount` | Rare negative values (~0.1%) | Noise | Simulates reversal/refund logging errors |
| `city` | Inconsistent casing/accents/abbreviations | Noise | Same as merchant_name rationale |
| `decline_reason` | Missing when status ≠ declined (expected/structural, not an "issue") | N/A | Structural null, not injected messiness |

## Explicitly NOT degraded
- `is_fraud`, `fraud_typology` — ground truth, kept clean for validation
- `transaction_id`, `account_id` (as a value, not as a reference) — primary keys stay valid

## Summary
- **Informative issues**: 3 (income/employment missingness, merchant risk tier missingness) — all deliberately subtle, not deterministic flags
- **Noise issues**: 7 — realistic operational messiness unrelated to fraud
