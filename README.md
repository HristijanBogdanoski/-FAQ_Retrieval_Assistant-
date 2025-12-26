# FAQ Retrieval Assistant
## Overview
This project implements a **simple FAQ Retrieval Assistant** that takes a user query and retrieves the most relevant answers from a predefined FAQ knowledge base.

The system:
- Converts FAQ questions into embeddings
- Computes similarity between user queries and stored questions
- Returns the **Top 3 most relevant FAQs**
- Outputs the **best answer + confidence level**
- Supports **multilingual queries (English + Macedonian)**

## Dataset
The system uses a dataset of **20 FAQ pairs** covering:
- Billing
- Account
- Support
- Product
- Security
- Onboarding

Both **English and Macedonian FAQs are included**, allowing multilingual retrieval.


## Approach

### 1 Embeddings
- Model used: `paraphrase-multilingual-MiniLM-L12-v2` from SentenceTransformers
- Reason: It supports multilingual inputs and is lightweight but accurate.

We embed all FAQ questions once and store them as vectors.

---

### 2 Confidence Scoring
Similarity is mapped to confidence labels:

| Score Range | Confidence |
|------------|------------|
| ≥ 0.7      | High       |
| 0.4–0.69   | Medium     |
| < 0.4      | Low        |

---

### 3 Retrieval
For every user query:
1. Encode the query using the same sentence transformer
2. Compute cosine similarity between query embedding and FAQ embeddings
3. Sort and retrieve Top-3 most relevant FAQs
4. Optionally filter by similarity threshold
---

### 4 Test Retrieval
Test with different queries to see our Confidence levels
Quick example:
----------------------------------------------------------------------
Query: 'I forgot my password'
----------------------------------------------------------------------

:) Result 1 - High Confidence (0.819)
   Q: Како да ја ресетирам мојата лозинка?
   A: Одете на поставки → сметка → ресетирај лозинка. Ќе добиете е-пошта со инструкции...
   [Category: Account | Language: mk]

:) Result 2 - High Confidence (0.798)
   Q: How can I reset my password?
   A: Go to settings → account → reset password. You will receive an email with instru...
   [Category: Account | Language: en]

:| Result 3 - Medium Confidence (0.590)
   Q: Why can't I log into my account?
   A: Make sure your email is verified and that you are using the correct login creden...
   [Category: Account | Language: en]

  ---
  
### 5 Evaluation
System evaluated using:
- Hits@1
- Hits@3
- Mean Reciprocal Rank (MRR)

Results on test queries:
- **Hits@1:** ~66%
- **Hits@3:** **100%**
- **MRR:** ~0.83

---

### 6 Bonus Features
* Multilingual Support (EN ↔ MK)  
* Confidence Score  
* Performance Benchmarking  
Visualizations for:
- Language & category distribution
- Relevant vs irrelevant similarity separation
- Latency distribution

---

## Tools & Libraries
- Python
- pandas, numpy
- sentence-transformers
- scikit-learn
- matplotlib / seaborn

---

## How to Run
1. Install dependencies
pip install sentence-transformers pandas numpy scikit-learn matplotlib seaborn

2. After you have run the dependencies run the notebook cells in your preffered IDE. ** Recommended Jupyter Notebook or Colab **
