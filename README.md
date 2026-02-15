# Risk Radar — Detecting Unfair Contract Terms with NLP

## Overview
**Risk Radar** is a natural language processing project exploring whether machine learning can help identify potentially unfair contract terms under Australian Consumer Law.

Contracts are widely used but rarely read in full. Assessing whether a clause is unfair typically requires legal expertise and manual review, which does not scale across large volumes of consumer agreements. This project investigates whether models can assist by automatically flagging clauses that warrant legal attention.

The goal is not to replace legal judgement, but to prioritise review and make risk more visible.

---

## The Problem
- Terms & Conditions average ~8,500 words
- Consumers rarely read them fully
- Regulators cannot manually review every agreement
- Manual legal review takes significant time per contract

This creates a gap where problematic clauses may go unnoticed unless challenged.

---

## Data

### Training Data — European Consumer Law
- **CLAUDETTE dataset (~11,800 clauses)**
- Labelled as *fair* or *potentially unfair*
- Significant class imbalance

### Australian Dataset (Custom Built)
Derived from:
- Federal Court unfair contract term decisions
- ACCC enforcement actions and undertakings
- ACCC guidance material

To improve learning, historical unfair clauses were paired with later compliant versions to teach the model what changed and why.

---

## Methodology

### Step 1 — Benchmarking
Compared multiple modelling approaches:

| Tier | Approach | Purpose |
|----|----|----|
| Baseline | TF-IDF + SVM | Keyword & phrase detection |
| Semantic | RoBERTa embeddings | Contextual meaning |
| Legal Domain | Legal-BERT | Legal language understanding |
| Ensemble | Combined model | Risk-focused detection |

### Step 2 — Cross-Jurisdiction Testing
Models trained on EU law were tested on Australian law to evaluate transferability.

### Step 3 — Local Adaptation
Few-shot fine-tuning performed using the Australian dataset.

---

## Key Results

| Scenario | F1 Score | Recall (Unfair) |
|-------|------|------|
| Zero-shot (EU → AU) | 0.00 | 0% |
| After fine-tuning | ~0.60 | ~65% |

- Clause analysis reduced from ~20 minutes manual review to under 1 second
- Ensemble model produced the most stable performance

---

## Key Insight
The main limitation was not language differences but legal context.  
Models trained on one jurisdiction did not generalise until exposed to local regulatory reasoning.

---

## Tech Stack
- Python
- PyTorch
- HuggingFace Transformers
- Scikit-learn
- NLP / Transfer Learning
- Jupyter / Google Colab

---

## Project Structure
```
notebooks/        model training & evaluation
data/             processed datasets
models/           trained model outputs
app/              prototype interface
```

---

## Future Work
- Move from clause-level to full-document analysis
- Classify types of unfairness (termination, indemnity, unilateral variation)
- Continuous updating with new regulatory decisions
- Evaluate deployment for regulatory or compliance workflows

---

## Disclaimer
This tool does not provide legal advice.  
It is designed to assist review by highlighting clauses that may require legal assessment.
