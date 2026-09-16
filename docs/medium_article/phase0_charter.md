# [Section: Phase 0 — The Charter] — Draft

**Status:** Draft v1

---

## Starting with a charter, not a notebook

Most tutorials start with `import pandas as pd`. Real projects start with a document nobody outside the team ever sees: a charter that forces you to answer, in writing, what problem you're actually solving and how you'll know if you solved it — before you touch a single dataset.

I wrote one for this project, the way a fraud analytics team at a bank would write one before greenlighting any modeling work. It forced a few decisions I want to walk through, because the reasoning mattered more than the document itself.

## Debit fraud, not credit card fraud — on purpose

If you've built a fraud detection portfolio project before, there's a good chance you used the classic Kaggle credit card fraud dataset — PCA-anonymized transactions, a handful of features nobody can interpret, and a well-worn tutorial path everyone follows the same way.

I deliberately didn't go that route. Debit card and payment fraud is a different problem: different typologies (account takeover, e-transfer fraud, point-of-sale card-testing), different data (you actually get real fields — merchant, geography, channel — instead of anonymized components), and different stakes, since debit fraud hits a member's actual funds directly rather than a credit line. It's also, frankly, a less crowded portfolio path — which matters if the goal is to stand out, not just to demonstrate you can call `.fit()`.

## Synthetic data, built to be messy on purpose

I made an early decision that I think is the most important one in this whole project: build the data myself (with my friend Claude), and make it messy in a *specific, defensible* way — not just clean and simple, and not just randomly corrupted either.

Real fraud data comes with missing fields, inconsistent formats, and broken joins between systems. Most portfolio projects skip straight past that reality because a clean CSV is easier to demo. But cleaning genuinely messy data — and reasoning about *why* it's messy — is a real and underrated part of the job. So I built a two-layer data generator: a clean ground-truth layer with labeled fraud cases, then a second layer that deliberately degrades it the way production banking data actually looks.

The detail I'm most proud of in this design: some of that messiness isn't random. A documented subset of it is quietly correlated with the fraud labels — synthetic or stolen identities tend to have incomplete account profiles, for instance — because in real fraud data, missingness itself is sometimes a signal, not just noise to clean away. Getting that balance right, so the project stays solvable but still realistic, was worth the extra planning time.

## The idea I didn't expect to learn: shadow mode

One decision I made in the charter that I think is worth calling out on its own: before this model would ever be trusted to make real decisions, it has to run in **shadow mode** — scoring live transactions, logging what it *would* decide, without actually acting on any of it.

The reasoning is subtle but important: a backtest only tells you how a model performs on historical data that its own decisions never touched. The moment a model starts actually blocking transactions, it changes the data it sees next — fraud patterns shift in response, and the model's own success quietly reshapes what "normal" looks like going forward. Shadow mode is how real teams bridge that gap before trusting a model with real decisions.

It's a small paragraph in the charter. But it's the kind of distinction that separates "my model has 95% precision" from "my model has 95% precision *and I know that number will hold up once it's actually making decisions*".

<!-- TODO: consider adding a small diagram or table summarizing the schema decisions -->
