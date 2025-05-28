# 🛠️ Multi-Task Ticket Classifier & Entity Extractor

This project is a multi-task machine learning system that:
- Classifies customer support tickets into **issue types**
- Predicts the **urgency level**
- Extracts **entities** such as product names, dates, and complaint keywords from ticket text

---

## 📁 Dataset

The input Excel file (`ai_dev_assignment_tickets_complex_1000.xlsx`) includes:
- `ticket_id`
- `ticket_text`
- `issue_type` (multi-class label)
- `urgency_level` (Low, Medium, High)
- `product` (ground truth for entity extraction)

---

## ⚙️ Project Workflow

### 1. **Data Cleaning & Preprocessing**
- Handle missing values
- Normalize ticket text (lowercase, remove special characters)
- Tokenize, remove stopwords, and lemmatize

### 2. **Feature Engineering**
- TF-IDF (Bag-of-Words and bigrams)
- Ticket length and sentiment score
- Combined via `scipy.hstack`

### 3. **Multi-Task Modeling**
- **Issue Type Classifier**: `LogisticRegression`
- **Urgency Classifier**: `RandomForestClassifier` (optionally with SMOTE and `HistGradientBoostingClassifier`)

### 4. **Entity Extraction**
Rule-based extraction of:
- Products (from known product list)
- Dates (regex)
- Keywords (e.g. "broken", "late", etc.)

### 5. **Integration Function**
```python
predict_and_extract(text, issue_model, urgency_model, tfidf_vectorizer, label_enc_issue, label_enc_urgency)
```
Returns predictions and extracted entities.

### 6. **Optional Gradio UI**
Interactive interface to input ticket text and see results.

---

## ▶️ How to Run (Colab Version)

1. Open the Colab notebook: [**Colab Link Here**]
2. Select `Runtime > Run all`
3. Use the `predict_and_extract` function or launch Gradio at the bottom.

---

## 📊 Evaluation Metrics

**Issue Type Model**
- Accuracy: ~98%
- Precision, Recall, F1-score (macro): ~0.98

**Urgency Model**
- Accuracy: ~36%
- Balanced performance after SMOTE and boosting

---

## 📝 Limitations
- Urgency level is harder to predict due to vague patterns in text
- No deep learning used (only classical ML)
- Entity extraction is rule-based and may miss edge cases

---

## 🎥 Demo Video
https://drive.google.com/file/d/1o1tn02zJNJi8Tkf9gkeP3wYY4uuVfKKC/view?usp=sharing

---

## 📦 Submission Includes
- `notebook.ipynb` (Colab-ready code)
- `model_issue.pkl` and `model_urgency.pkl` 
- `README.md` 
- `demo_video.mp4` (link)

---