## Search and Ranking Systems

Staff Engineer @ BloomReach — Oct 2013 to Mar 2018  
**Location:** Bengaluru, India

**Patents and Blog**
  - [US20180060936A1: Search Ranking System](https://patents.google.com/patent/US20180060936A1)  
  - [US20160350395A1: Synonym Generation](https://patents.google.com/patent/US20160350395A1)
- Blog: [Synonym Generation](https://dev.to/bloomreach/discovery-synonym-generation-at-bloomreach-ob5)


**Overview**  
Led the design and implementation of an **automated synonym generation** pipeline for BloomReach Discovery, processing **100 million+ product descriptions** and **30 million+ queries** weekly to extract high-quality synonym pairs for e-commerce search.
As deep learning started emerging, designed deep NNs to match user queries with document text & images.


E-commerce search faces messy, short queries (“nj devils tees”), shifting language (“jorts”), and ambiguity (“frozen” the temperature vs. *Frozen* the movie). Synonyms aren’t just dictionary swaps; they’re a controlled expansion of user intent.

**Goal.** Bridge query–catalog mismatch without flooding results. Boost recall while preserving precision and rank quality.

**Synonym Types.**

* **Variants:** spelling/lemma/plural (“adapter ↔ adaptor”, “shoe ↔ shoes”).
* **Equivalents:** true alternates (“graph paper ↔ grid paper”).
* **Hierarchy:** hypernym/hyponym (“desktop pc ↔ computers”).
* **Backstops:** closely related substitutes when inventory is thin (“paper plates ↔ plastic plates”).

**Data Scale.** Weekly mining over ~100M product descriptions, billions of web lines, and ~30M queries to capture new vocabulary, trends, and seasonality.

**Pipeline (Mining, not per-query).**

* **Candidate extraction:** phrase pairs from catalog, crawl, and logs.
* **Representations:**

  * Context windows / embeddings (“a word by the company it keeps”).
  * Behavioral signals: clicked/viewed/bought product distributions after a query.
  * Document vectors: TF-IDF-weighted phrase contexts.
  * Session neighbors: queries issued together or sequentially.
* **Similarity scoring:**

  * Symmetric measures (e.g., Jensen–Shannon divergence on click dists) for equivalence.
  * Asymmetric measures for hypernym/hyponym directionality.
  * Heuristics (edit distance, morphology) to nudge borderline cases.
* **Decisioning:**

  * Phrase-specific thresholds (relative to known baselines like “shoe↔shoes”).
  * Supervised model over multi-score features to grade and type pairs.
  * Guardrails so low-confidence expansions don’t bubble to the top after sorts (price/popularity).

**Application.**

* Build a typed synonym graph (variant/equivalent/hierarchy/related) with confidence scores.
* Apply class-specific rules at query time to expand cautiously.
* Refresh weekly to reflect new products, slang, and events.

**Outcomes.**

* Higher findability and better long-tail recall with minimal precision loss.
* Resilient to language drift; fewer manual thesaurus edits.
* Honest note: Like any ML system, it has “good and bad days,” so monitoring and iteration matter.

![synonyms.png](assets/synonyms.png)
