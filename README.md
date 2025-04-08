
# 🔒 Phishing URL Detection using Machine Learning

## 🧠 Motivation

The increasing use of the internet for day-to-day activities has led to a surge in cyber threats like phishing and malware. Malicious URLs are a key vector in such attacks. This project aims to detect these harmful URLs using machine learning by extracting insightful features from them and training classification models for accurate detection.

---

## 📂 Data Description

- **Shape:** `450,176 rows × 4 columns`
- **Columns:**
  - `url`: The URL to be classified
  - `label`: Benign or Malicious
  - `result`: 0 for Benign, 1 for Malicious
  - `Unnamed`: Dropped during cleaning

---

## 🧹 Methodology

### 🔸 Data Cleaning
- Dropped unnamed column and invalid URLs using a custom `is_valid_url` function.
- Resulting dataset shape: `450,172 × 3`

### 🔸 Feature Extraction
Extracted 18 features to help classify URLs, grouped as:
- **Length-Based (4):** `url_length`, `hostname_length`, `path_length`, `fd_length`
- **Count-Based (12):** `count-`, `count@`, `count?`, `count%`, `count.`, `count=`, `count-http`, `count-https`, `count-www`, `count-digits`, `count-letters`, `count_dir`
- **Binary (2):** `use_of_ip`, `short_url`

Final shape: `450,172 × 21`

### 🔸 Data Preprocessing
- **Oversampling:** SMOTE to balance class distribution → `691,476 records`
- **Train-Test Split:** 80/20
- **Feature Scaling:** `StandardScaler` for normalization

---

## 📊 Exploratory Data Analysis (EDA)

Key findings:
- `count-https` and `count-www` are negatively correlated with being malicious
- `count-http` positively correlates with maliciousness
- Longer URLs often have longer paths
- Malicious URLs are more evenly distributed in length
- Characters like `@`, `?`, `%` are rare
- Malicious URLs often use IPs and shorter paths

---

## 🤖 ML Models Trained

### 1. Logistic Regression
- Sigmoid activation function
- Optimized using log-loss
- Default parameters

### 2. K-Nearest Neighbors (KNN)
- `k = 5`
- Euclidean distance
- Non-parametric

### 3. Support Vector Machine (SVM)
- Linear kernel
- Avoided RBF due to computational load

### 4. Decision Tree
- `max_depth = 5`

---

## 📈 Model Performance

| Model                  | Test Accuracy | Train Accuracy | F1-Score (Benign) | F1-Score (Malicious) |
|------------------------|---------------|----------------|-------------------|-----------------------|
| Logistic Regression    | 99.68%        | 99.68%         | 0.99678           | 0.99677               |
| K-Nearest Neighbors    | **99.75%**    | **99.79%**     | **0.99747**       | **0.99746**           |
| Support Vector Machine | 99.68%        | 99.68%         | 0.99677           | 0.99676               |
| Decision Tree          | 99.71%        | 99.73%         | 0.99715           | 0.99714               |

---

## ✅ Conclusion and Future Scope

All models performed exceptionally well, with **KNN** leading slightly in performance. The success of this approach highlights the effectiveness of structured feature extraction in identifying phishing threats.

### 🔮 Next Steps:
- Deploy best model in a real-time detection system using Flask or similar.
- Explore ensemble and deep learning methods for further improvements.
- Continuously update dataset to adapt to evolving threats.

---

## 📚 References

- [Python URL Parsing Docs](https://docs.python.org/3/library/urllib.parse.html)  
- [Scikit-learn Documentation](https://scikit-learn.org/stable/)

