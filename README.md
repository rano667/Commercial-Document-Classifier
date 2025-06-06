### 📄 Commercial Document Classifier (Lightweight Rule-Based Engine)

This project trains a lightweight classifier to determine whether a document is **Commercial** or **Non-Commercial**, using a small labeled dataset of text extracted from OCR.

---

### 🔍 How It Works

1. **Training**:
   - Input data: CSV with document text and binary labels (`1 = Commercial`, `0 = Non-Commercial`)
   - Preprocessing: Lowercasing, punctuation & number removal
   - Vectorization: `TfidfVectorizer` with top 50 keywords
   - Model: `DecisionTreeClassifier` (depth-limited)
   - Auto-generates: A pure `if-else` Python function based on decision tree rules

2. **Production**:
   - Takes OCR-extracted text as input
   - Transforms text using the trained `TfidfVectorizer`
   - Applies the generated `if-else` rule to classify

---

### ⚙️ Project Structure

```
📁 your-project/
├── Commercial Doc Classification data.csv   # Input dataset
├── train_and_export.py                      # Model training & rule generation
├── commercial_rule.py                       # Auto-generated rule (pure Python if-else)
├── predict_from_ocr.py                      # Runtime classifier using OCR text
└── tfidf_vectorizer.joblib                  # Saved vectorizer
```

---

### 🏁 Getting Started

```bash
# 1. Train the model and generate rule
python train_and_export.py

# 2. Run prediction on new OCR text
python predict_from_ocr.py
```

---

### 🧠 Example Rule Output (`commercial_rule.py`)

```python
def is_commercial_doc(features):
    if features['port'] <= 0.13:
        return 0  # Non-Commercial
    if features['port'] > 0.13:
        return 1  # Commercial
```

---

### ✅ Why This Approach?

- ⚡ Fast & lightweight (no ML library needed in production)
- 🔍 Transparent logic (easy to debug and explain)
- 🧩 Can be integrated into any Python backend
