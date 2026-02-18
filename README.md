# Semantic Similarity Engine for Persian Legal Entities

This repository features a hybrid NLP system designed to detect similarities between proposed company names and existing legal entities. Built to handle the specific challenges of the Persian language, the system identifies potential registration conflicts by combining **Semantic Embeddings (Sentence Transformers)** with custom **Rule-Based Logic**.

## ⚖️ The Problem
In many jurisdictions, a new company name cannot be registered if it is "confusingly similar" to an existing one. This project automates that verification process by enforcing several legal rules:
1. **Exact Matches:** Rejecting identical strings.
2. **Subset Detection:** Identifying if a new name is a subset or superset of an existing one.
3. **Permutation Analysis:** Detecting reordered words (e.g., "Tech Solutions" vs "Solutions Tech").
4. **Morphological Variations:** Handling singular/plural forms and root word derivatives (e.g., "Merchant" vs "Merchandise").
5. **Semantic Similarity:** Detecting names that are conceptually too close using vector distance.

## 🚀 Key Technical Features
* **Transformer-Based Embeddings:** Utilizes `sentence-transformers` to map company names into a high-dimensional vector space, allowing for similarity detection beyond simple keyword matching.
* **Custom Lemmatization Pipeline:** Implements a specialized root-word dictionary (built from `dataset_sample.csv`) to normalize Persian words to their lemmas before comparison.
* **Dadmatools Integration:** Uses `dadmatools` for sophisticated Persian text normalization (standardizing characters, removing half-spaces, etc.).
* **Fuzzy String Matching:** Incorporates Levenshtein distance to catch minor typographical variations and "confusingly similar" spellings.
* **GPU-Accelerated Inference:** Optimized to process thousands of existing records efficiently using CUDA.

## 🛠️ Tech Stack
* **Models:** Sentence-Transformers (BERT-based)
* **NLP Tools:** Dadmatools, Hazm (for Persian normalization)
* **Data Science:** Pandas, NumPy, Scikit-learn
* **Logic:** Python-Levenshtein

## 📐 Implementation Logic
The system processes a candidate name through a multi-stage pipeline:
1.  **Normalization:** Standardizing Persian character sets.
2.  **Lemmatization:** Mapping words to their roots (e.g., matching "صنعت" and "صنعتی").
3.  **Heuristic Checks:** Running fast rules for subsets, exact matches, and permutations.
4.  **Vector Search:** Using cosine similarity on embeddings to find the "Top K" most similar existing names.
5.  **Final Decision:** A weighted score combining semantic distance and edit distance determines the final "Accept" or "Reject" status.

## 📁 Repository Structure
* `Detecting similarity between company names.ipynb`: The core engine and experimental results.
* `dataset_sample.csv`: The morphological mapping dataset for Persian roots and derivatives.
* `data_sample.csv`: A sample database of existing registered company names.
* `requirements.txt`: Environment dependencies.

## ⚙️ How to Use
1.  **Clone the repo:**
    ```bash
    git clone [https://github.com/mahdisdg/Semantic-Company-Name-Verification.git](https://github.com/mahdisdg/Semantic-Company-Name-Verification.git)
    ```
2.  **Install dependencies:**
    ```bash
    pip install dadmatools sentence-transformers pandas python-Levenshtein
    ```
3.  **Run the Engine:**
    Load your database of existing names into the notebook and test candidate names against the `SimilarityChecker` class.
