# Epistemic Stance and Evidential Grounding in AI vs. Human News Discourse

Computational Corpus Analysis of Professional Journalism and Large Language Models

---

## Overview

This project investigates how AI-generated news differs from professional journalism at the discourse-pragmatic level. Using Natural Language Processing (NLP), corpus linguistics, and machine learning, it compares professional news articles with GPT-5.4-mini generated articles covering the same news topics.

Rather than relying on traditional lexical or stylistic measures, the study operationalizes discourse-theoretical concepts, specifically **epistemic stance** and **evidential grounding**, through computational feature engineering.

---

## Research Questions

1. How do AI-generated and human-written news articles differ in their use of epistemic stance markers (hedges and boosters)?

2. How do AI-generated and human-written news articles differ in their use of attribution markers?

3. Can discourse-pragmatic features reliably distinguish AI-generated from human-written news?

---

## Corpus

### Human Corpus

* 819 professional news articles
* 704,692 words
* News related to the US-Iran geopolitical conflict (February to May 2026)
* Sources:

  * BBC News
  * The Guardian
  * AP News
  * CNBC

### AI Corpus

* 819 articles
* 698,189 words
* Generated with GPT-5.4-mini through the OpenAI API
* Zero-shot generation using the corresponding human headlines

Total corpus size:

* **1,638 articles**
* **1.4 million words**

---

## Project Pipeline

```text
Professional News Sources
          │
          ▼
Web Scraping (Fundus)
          │
          ▼
Human Corpus (JSON)

          Headlines
               │
               ▼
GPT-5.4-mini (OpenAI API)
               │
               ▼
AI Corpus (JSON)
               │
               ▼
Corpus Cleaning & Normalisation
               │
               ▼
AntConc Exploration
(KWIC • Frequency • N-grams)
               │
               ▼
Feature Engineering (spaCy)
               │
               ▼
Statistical Analysis
(Mann-Whitney U)
               │
               ▼
Random Forest Classification
               │
               ▼
Visualisation & Interpretation
```

## Methodology

### 1. Human Corpus Collection

Professional news articles were collected automatically using **Fundus** from BBC News, The Guardian, AP News, and CNBC. Each article was stored in JSON format together with its headline, metadata, and source URL.

### 2. AI Corpus Generation

For every human article, the original headline was submitted to **GPT-5.4-mini** through the OpenAI API using a standardized zero-shot prompt. The model generated a hard-news article matching the target length of the corresponding human article while having no access to external news sources.

### 3. Corpus Cleaning

A Python pipeline removed boilerplate text, normalized formatting, validated article content, and prepared comparable human and AI corpora.

### 4. Exploratory Analysis

A pilot corpus was explored in AntConc using frequency lists, KWIC concordances, and N-gram analysis to identify recurring discourse patterns and guide feature selection.

### 5. Feature Engineering

A custom spaCy pipeline applied tokenization, lemmatization, POS tagging, and dependency parsing to extract:

* Hedges
* Boosters
* Attribution markers
* Passive voice (control variable)

Feature frequencies were normalized per 1,000 words.

### 6. Statistical Analysis

Feature distributions were compared using Mann-Whitney U tests. A Random Forest classifier was then trained to evaluate the predictive power of the discourse features.

## Repository Structure

```text
discourse_project/
│
├── data/
│   ├── raw/
│   ├── cleaned/
│   └── corpus_txt/
│
├── results/
│
├── scripts/
│   ├── scrape_articles.ipynb
│   ├── corpus_cleaning_pipeline.py
│   ├── feature_engineering.py
│   └── analysis.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/yourusername/discourse_project.git
cd discourse_project
```

Install the required packages:

```bash
pip install -r requirements.txt
```

Install the spaCy English model:

```bash
python -m spacy download en_core_web_sm
```

---

## Main Python Libraries

* pandas
* spaCy
* scikit-learn
* SciPy
* seaborn
* matplotlib
* Fundus
* OpenAI API
* langdetect
* Jupyter Notebook

---

## Main Findings

* AI-generated news contains substantially more hedging than professional journalism.
* Human-written news relies much more heavily on attribution markers to ground information in identifiable sources.
* Passive voice occurs at similar frequencies across both corpora, suggesting that LLMs successfully reproduce the surface syntactic conventions of hard-news writing.
* Using only discourse features, a Random Forest classifier distinguishes AI-generated from human-written articles with **89.33% accuracy**.

---

## Theoretical Framework

The project is informed by:

* Hyland (2005): Epistemic stance (hedges and boosters)
* Bednarek (2006): Evidentiality and epistemological positioning in news discourse
* Biber et al. (1999): Grammatical characteristics of news discourse

---

## Data Availability

The repository includes the corpus, processing pipeline, feature extraction scripts, statistical analysis, and visualizations for academic and demonstration purposes.

The news articles remain the property of their respective publishers.

---

## Author

**Soufiane Zekriti Drissi**

Master's Programme in Data and Discourse Studies

Technische Universität Darmstadt
