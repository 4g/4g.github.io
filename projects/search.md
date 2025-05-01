## Search and Ranking Systems - 2015
- Automated synonym generation, spell-correction, and query understanding.  
- Patents:  
  - [US20180060936A1: Search Ranking System](https://patents.google.com/patent/US20180060936A1)  
  - [US20160350395A1: Synonym Generation](https://patents.google.com/patent/US20160350395A1)
- Designed deep NNs to match user queries with document text & images.


### Synonym Generation System

![Synonym Generation Pipeline](<INSERT_IMAGE_URL_1>)  
![Similarity Scoring Diagram](<INSERT_IMAGE_URL_2>)

**Role & Timeline**  
Staff Engineer @ BloomReach — Oct 2013 to Mar 2018  
**Location:** Bengaluru, India

**Overview**  
Led the design and implementation of an **automated synonym generation** pipeline for BloomReach Discovery, processing **100 million+ product descriptions** and **30 million+ queries** weekly to extract high-quality synonym pairs for e-commerce search :contentReference[oaicite:0]{index=0}.

**Key Features**  
- **Data Mining & Representation:**  
  - Extract candidate phrase pairs from product catalog text, Web crawl, and search logs.  
  - Build contextual embeddings via co-occurrence contexts, click-through distributions, document-vector averages, and session proximity. :contentReference[oaicite:1]{index=1}  
- **Similarity Metrics & Filtering:**  
  - Combine symmetric (JS divergence) and asymmetric (hyponym/hypernym) measures, augmented by edit-distance heuristics.  
  - Apply phrase-specific thresholds (e.g. ensuring D(P, Q) < D(P, P′) where P′ is a known variant) to filter high-confidence pairs.  
  - Train a supervised classifier on multi-score feature vectors to rank and grade synonyms.  
- **Continuous Learning:** Weekly batch updates to capture evolving language, new trends, and seasonal shifts in user queries.

**Patents**  
- **US20180060936A1:** Search Ranking System—contextual term weighting and nonessential term filtering :contentReference[oaicite:3]{index=3}  
- **US20160350395A1:** Synonym Generation & Identification—vector-based candidate filtering & similarity modules :contentReference[oaicite:4]{index=4}  

**Resources**  
- Blog: [Discovery | Synonym Generation at Bloomreach](https://dev.to/bloomreach/discovery-synonym-generation-at-bloomreach-ob5)
