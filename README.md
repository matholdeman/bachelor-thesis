## INFLUENCE OF GEOPOLITICAL POSITION ON NEWS MEDIA NARRATIVES

Bachelor's thesis, BSc Cognitive Science & Artificial Intelligence, Tilburg University (2026)
**Author:** Anne Mathilde Oldeman
**Committee:** dr. Noortje Venhuizen, dr. Parto Shahroudi

## OVERVIEW

This project investigates whether a country's geopolitical position shapes how its news media frame the same global event. Using the 2025–26 Greenland crisis as a case study, it combines topic modeling and sentiment analysis to compare news coverage across four regional groups:

- Greenland & Denmark — directly threatened stakeholder
- Affected Europe — tariff-threatened countries(NL, FR, SE, NO, FI, DE, UK)
- USA — opposing party in the crisis
- Other — unaffiliated regions (Canada, India, Australia)

The dataset consists of 1,674 articles collected from 47 English-language outlets, scraped between January 2025 and February 2026.

## RESEARCH QUESTIONS

1. Which themes dominate the framing of the crisis across regions?
2. How does emotional tone differ between regions?
3. To what extent do unaffiliated regions align with or diverge from stakeholder narratives?

## METHODOLOGY

**Data Collection:**
- Article URLs retrieved via the `GNews` Python library and `googlenewsdecoder`
- Full text extracted with `newspaper3k`
- 3-stage verification pipeline (deduplication, keyword filtering, extraction) to reduce noise
- Stratified down-sampling to balance regional group sizes

**Topic Modeling:**
- Preprocessing with spaCy (`en_core_web_sm`): tokenization, stopword removal, lemmatization
- Latent Dirichlet Allocation (LDA) via `gensim`, with optimal *k* selected using coherence and perplexity scores
- Principal Component Analysis (PCA) to visualize topic distributions and compare thematic overlap across regions

**Sentiment Analysis:**
- Baseline: VADER (lexicon-based)
- Advanced: RoBERTa (`siebert/sentiment-roberta-large-english`), applied with a chunking strategy to handle the 512-token limit
- Statistical comparison via Kruskal-Wallis and pairwise Mann-Whitney U tests with Bonferroni correction
- Pearson correlation between VADER and RoBERTa scores to assess model agreement

## KEY FINDINGS

- Greenland & Denmark's coverage consistently centers on sovereignty and security, distinct from other regions' more dispersed thematic scope.
- VADER found little sentiment variation across regions and skewed positive throughout — consistent with its known limitations on formal, non-social-media text.
- RoBERTa revealed sharper, statistically significant regional differences: USA coverage was most negative, Affected Europe most positive, while Greenland & Denmark and Other were statistically indistinguishable — suggesting proximity to the crisis alone doesn't predict tone.

## REPOSITORY STRUCTURE

```
├── datascraper.ipynb         # scrapes article URLs (GNews) and extracts full text (newspaper3k)
├── MASTER_SAMPLED.csv        # cleaned, stratified-downsampled dataset (1,674 articles, 4 regions)
├── master_preprocess.csv     # preprocessed text for topic modeling (stopwords removed, lemmatized)
├── topicmodeling.ipynb       # LDA topic modeling + PCA on regional topic distributions
├── sentimentanalysis.ipynb   # VADER + RoBERTa sentiment scoring and statistical testing
└── bachelor_thesis.pdf       # full written thesis
```

**Pipeline Order:** `datascraper.ipynb` → `master_preprocess.csv` → `topicmodeling.ipynb` and `sentimentanalysis.ipynb` (the latter two both run on `MASTER_SAMPLED.csv`, with `topicmodeling.ipynb` using the further-preprocessed `master_preprocess.csv` for LDA)

## ACKNOWLEDGMENTS

Thank you to my supervisor, dr. Noortje Venhuizen, for guidance throughout this project. A generative language model (Claude, Anthropic) was used to assist with code development; Grammarly was used for spell-checking.
