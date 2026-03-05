# Chapter 4 — Pre-trained Models & HuggingFace

> **Module 3 · Transformers & Summarization** · Estimated Duration: 50 minutes

---

## 🎯 Learning Objectives

1. Navigate the HuggingFace Model Hub and select models for specific NLP tasks.
2. Load pre-trained models and tokenisers using `AutoModel` and `AutoTokenizer`.
3. Perform inference with a loaded model (tokenise → encode → decode).
4. Understand model cards, licensing, and ethical considerations.

---

## 📚 Core Concepts

### 4.1 — The HuggingFace Ecosystem

```mermaid
flowchart TD
    A[HuggingFace Hub] --> B[Models]
    A --> C[Datasets]
    A --> D[Tokenisers]
    B --> E["AutoModel.from_pretrained()"]
    D --> F["AutoTokenizer.from_pretrained()"]
    E --> G[Inference / Fine-Tuning]
    F --> G

    style A fill:#fbbf24,stroke:#d97706,color:#000
    style G fill:#22c55e,stroke:#16a34a,color:#fff
```

```python
from transformers import AutoTokenizer, AutoModel  # Import HuggingFace auto classes
from loguru import logger  # Import loguru for DEBUG tracing

logger.debug("Starting M03-C04 — Pre-trained Models & HuggingFace")

model_name: str = "bert-base-uncased"  # Specify the pre-trained model identifier
logger.debug(f"Loading model: {model_name}")

tokeniser = AutoTokenizer.from_pretrained(model_name)  # Load the associated tokeniser
model = AutoModel.from_pretrained(model_name)  # Load the pre-trained model weights
logger.debug(f"Tokeniser vocab size: {tokeniser.vocab_size}")
logger.debug(f"Model parameters: {sum(p.numel() for p in model.parameters()):,}")

text: str = "Natural language processing is fascinating."
inputs = tokeniser(text, return_tensors="pt")  # Tokenise and convert to PyTorch tensors
logger.debug(f"Input IDs: {inputs['input_ids'].tolist()}")
logger.debug(f"Attention mask: {inputs['attention_mask'].tolist()}")
```

### 4.2 — Model Selection Guide

```mermaid
flowchart LR
    A{Task?} -->|Classification| B[BERT / RoBERTa]
    A -->|Generation| C[GPT-2 / Llama]
    A -->|Summarization| D[BART / T5]
    A -->|Translation| E[MarianMT / NLLB]

    style B fill:#60a5fa,stroke:#2563eb,color:#fff
    style C fill:#c084fc,stroke:#7c3aed,color:#fff
    style D fill:#34d399,stroke:#059669,color:#000
    style E fill:#fbbf24,stroke:#d97706,color:#000
```

---

## 🧪 Exercises

1. **Exercise 4.1** — Load `distilbert-base-uncased` and compare its parameter count to `bert-base-uncased`.
2. **Exercise 4.2** — Tokenise 10 sentences and log the token-to-word ratio for each.
3. **Exercise 4.3** — Read a model card on Hub and summarise its training data and limitations.

---

## 🔑 Key Takeaways

- `AutoModel` and `AutoTokenizer` detect the correct architecture automatically from the model name.
- Always check the **model card** for training data, intended use, and known limitations.
- DistilBERT offers **40% fewer parameters** with ~97% of BERT's performance — ideal for prototyping.

---

[← Previous Chapter](M03-C03-L01-context-window-architecture.md) · [Module Index](MODULE.md) · [Next Chapter →](M03-C05-L01-text-classification-transformers.md)
