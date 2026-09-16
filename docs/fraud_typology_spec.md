# Fraud Typology Spec

> Written BEFORE generator code, as a design spec (not reverse-engineered from code).
> Defines the behavioral signature of each simulated fraud typology, so the data
> generator implements a documented decision rather than inventing thresholds ad hoc.

## 1. Velocity Attack

Rapid succession of transactions on the same account/card, testing how much can be extracted before detection.

- **Signature:** ≥5 transactions within a 10-minute window, on the same `card_id`
- **Amount pattern:** starts small (testing viability), escalates once early transactions succeed
- **Status pattern:** may include a few `declined` (insufficient funds hit) mixed with `approved`
- **Fields it touches:** `timestamp`, `amount`, `card_id`, `status`

## 2. Geographic Impossibility

Two transactions occur in locations no person could physically travel between in the time elapsed.

- **Signature:** two transactions on the same `account_id` where the implied travel speed exceeds ~900 km/h (commercial flight speed) — i.e., physically impossible even by fastest normal travel
- **Example:** a transaction in Montreal at 14:02, another in Vancouver at 14:15
- **Fields it touches:** `latitude`, `longitude`, `timestamp`, `account_id`

## 3. Account Takeover

A fraudster gains access to a legitimate account and its behavior suddenly, meaningfully changes.

- **Signature:** combination, not a single flag — `is_new_device = true` **+** a deviation from the account's historical pattern (e.g. average transaction amount jumps significantly, or transactions occur at unusual hours relative to that account's history, or a new city never seen for that account)
- **Why combination matters:** a new device alone is common (people get new phones) — it's new device *plus* behavioral deviation that's the real signal, a more honest way to encode this than a single boolean
- **Fields it touches:** `device_id`, `is_new_device`, `amount`, `timestamp`, `city`, historical account behavior (computed, not stored raw)

## 4. Card-Testing

Small-value transactions, rapid-fire, to check if stolen card details are still valid before a larger attempt.

- **Signature:** multiple small transactions (under a low threshold, e.g. $5) in quick succession, high proportion `declined`, often at online/card-not-present merchants, sometimes followed by one larger `approved` transaction once a valid combination is found
- **Fields it touches:** `amount`, `status`, `decline_reason`, `channel`, `timestamp`, `card_id`

## Design Notes

- **Velocity vs. card-testing overlap:** both are rapid bursts. The distinguishing factor is *amount pattern* (escalating vs. consistently tiny) and *channel* (card-testing skews online/card-not-present). This distinction should be re-validated once real synthetic data is generated — if it's too blurry in practice, that's a documented finding, not a hidden flaw.
- **Account takeover is intentionally the hardest to encode** — it depends on each account's own history rather than a fixed global rule, mirroring the fact that account-takeover detection is a genuinely harder, less-solved problem in real fraud modeling.

## Status
Approved for implementation — see Phase 1 data generator.
