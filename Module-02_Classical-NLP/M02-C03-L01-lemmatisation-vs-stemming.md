# Chapter 3 — Lemmatization vs. Stemming

> **Module 2 · Classical NLP** · Estimated Duration: 35 minutes

---

## 🎯 Learning Objectives

1. Distinguish between stemming (rule-based suffix stripping) and lemmatization (dictionary-based morphological analysis).
2. Implement Porter Stemmer and Snowball Stemmer from NLTK.
3. Implement WordNet Lemmatiser with POS-tag awareness.
4. Choose the right normalization strategy for different NLP tasks.

---

## 📚 Core Concepts

### 3.1 — Stemming vs. Lemmatization Comparison

```mermaid
flowchart TD
    A[Input Word] --> B{Method}
    B -->|Stemming| C[Rule-Based Suffix Stripping]
    B -->|Lemmatization| D[Dictionary Lookup + POS]
    C --> E["'running' → 'run'"]
    C --> F["'studies' → 'studi' ⚠️"]
    D --> G["'running' → 'run'"]
    D --> H["'studies' → 'study' ✅"]

    style C fill:#f97316,stroke:#ea580c,color:#fff
    style D fill:#22c55e,stroke:#16a34a,color:#fff
    style F fill:#ef4444,stroke:#dc2626,color:#fff
    style H fill:#22c55e,stroke:#16a34a,color:#fff
```

```python
import nltk  # Import NLTK for stemming and lemmatization tools
from nltk.stem import PorterStemmer, SnowballStemmer  # Import stemmers
from nltk.stem import WordNetLemmatizer  # Import the WordNet-based lemmatiser
from loguru import logger  # Import loguru for DEBUG execution tracing

nltk.download("wordnet", quiet=True)  # Download WordNet data for the lemmatiser

logger.debug("Starting M02-C03 — Lemmatization vs. Stemming")  # Log chapter entry

words: list[str] = ["running", "studies", "better", "geese", "was", "are"]  # Test words with varied morphology

# --- Porter Stemmer ---
porter: PorterStemmer = PorterStemmer()  # Instantiate the classic Porter stemmer
stems_porter: list[str] = [porter.stem(w) for w in words]  # Apply stemming to each word
logger.debug(f"Porter stems: {list(zip(words, stems_porter))}")  # Log input-output pairs

# --- WordNet Lemmatiser ---
lemmatiser: WordNetLemmatizer = WordNetLemmatizer()  # Instantiate the WordNet lemmatiser
lemmas: list[str] = [lemmatiser.lemmatize(w, pos="v") for w in words]  # Lemmatise as verbs
logger.debug(f"WordNet lemmas (verb): {list(zip(words, lemmas))}")  # Log input-output pairs
```

### 3.2 — When to Use Each

```mermaid
flowchart LR
    subgraph "Use Stemming"
        A1[Search Engines]
        A2[Information Retrieval]
        A3[Speed-Critical Pipelines]
    end
    subgraph "Use Lemmatization"
        B1[Text Classification]
        B2[Sentiment Analysis]
        B3[Named Entity Recognition]
    end

    style A1 fill:#fbbf24,stroke:#d97706,color:#000
    style B1 fill:#34d399,stroke:#059669,color:#000
```

---

## 🧪 Exercises

1. **Exercise 3.1** — Compare Porter and Snowball stemmers on 20 irregular English verbs.
2. **Exercise 3.2** — Implement a POS-aware lemmatiser that automatically detects the correct POS tag.
3. **Exercise 3.3** — Measure vocabulary size after stemming vs. lemmatization on a 10,000-document corpus.

---

## 🔑 Key Takeaways

- **Stemming** is fast but aggressive — it may produce non-words (e.g., "studi").
- **Lemmatization** produces valid dictionary forms but requires POS-tag information for accuracy.
- Choose based on your task: **stemming for IR/search**, **lemmatization for classification/NLU**.

---

[← Previous Chapter](M02-C02-L01-stopwords-noise-reduction.md) · [Module Index](MODULE.md) · [Next Chapter →](M02-C04-L01-n-grams-contextual-windows.md)
