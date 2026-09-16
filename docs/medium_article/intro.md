# [Section: Intro] — Draft

**Status:** Draft v1

---

There's a LinkedIn post I keep thinking about. Someone pointed out that most data science portfolios stop at `model.fit()` — clean data, a notebook, an evaluation score, done. The part that actually makes a data scientist useful to a company — getting the model out of the notebook, into something another system or person can use, and then watching it once it's out there — barely shows up in portfolios at all.

That gap is exactly where I wanted to spend my next project.

I'm a physicist by training — my PhD was in plasma physics and nanomaterials — and I've spent the last few years moving into data science, most recently working as a data engineer embedded at a bank in Brazil. That combination taught me two things that shaped how I approached this project: physics trains you to be suspicious of a model that looks too clean, and banking taught me that a fraud model's job isn't to be interesting — it's to be trustworthy enough that someone downstream will actually act on what it says.

So instead of building another model that ends at an evaluation score, I set out to build the thing a real fraud analytics team at a bank would actually build: a transactional anomaly detection system, planned like a real project — charter, data, EDA, features, model, strategy, deployment, monitoring — and pushed all the way through to something another person could use, not just admire in a notebook.

This article is the record of that build: the decisions, the trade-offs, and the places I got it wrong before I got it right.

