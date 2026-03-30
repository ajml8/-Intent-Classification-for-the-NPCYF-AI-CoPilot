# Intent-Classification-for-the-NPCYF-AI-CoPilot
Hybrid Feature-Based Intent Classifier for NPCYF AI CoPilot | LinearSVC + TF-IDF + Sentence Embeddings | IDEAS-TIH, ISI Kolkata
## 📌 Project Overview
An LLM deployed on an agriculture platform (NPCYF AI CoPilot) receives three very different types of questions:

| Intent Class    | Example                                           |
|----------------|--------------------------------------------------|
| `database_query` | "What is the average yield of wheat in Punjab?" |
| `platform_query` | "How do I reset my password?"                  |
| `general_query`  | "What is photosynthesis?"                      |

This project builds a lightweight intent classifier that reads the user's question first, labels it as one of the 3 categories, and routes it to the correct handler — preventing the LLM from wasting compute on misrouted queries.


## ✅ Results

| Metric              | Value        |
|--------------------|-------------|
| Overall Accuracy   | **98.3%**     |
| Precision          | **0.98**     |
| Recall             | **0.98**     |
| F1-Score           | **0.98**     |
| Misclassifications | **5 out of 300** |

## 🧠 Model & Approach
### Classifier
Linear regressor

```text
Input Question
      │
      ├──► TF-IDF + TruncatedSVD     →  300 features
      ├──► Sentence Embeddings        →  384 features  (all-MiniLM-L6-v2)
      └──► Text Statistics            →    5 features  (char count, word count, etc.)
                                           │
                                    ┌──────▼──────┐
                                    │  689 features │
                                    └──────┬──────┘
                                           │
                                    Logistic regression
                                           │
                              ┌────────────▼────────────┐
                              │  database_query /
  │
                              │  platform_query /        │
                              │  general_query           │
                              └─────────────────────────┘
```

## Why Logistic Regression

Logistic Regression was chosen as the final classifier because it handles multi-class problems natively through the softmax formulation used by the lbfgs solver, is computationally efficient on the 689-feature input, and produces interpretable probability scores for each class. With three well-separated intent classes in a high-dimensional feature space, Logistic Regression achieves strong performance without the risk of overfitting that more complex models can introduce.

## 📁 Repository Structure

```text
📁 Hybrid-Feature-Based-Intent-Classification/
│
├── 📓 model_training.ipynb          ← Complete training pipeline
│
├── 📊 finaldataset.xlsx         ← Full labelled dataset (3,840 questions)
├── 📊 test_dataset_30.xlsx             ← Test set (300 questions, 100 per class)
│
├── 📄 final12.docx        ← Full technical report
├── 📊 finalpptgm.pptx  ← Project presentation slides
│
└── 📋 README.md                     ← You are here!
```
⚠️ Model File (PKL): The trained model intent_classifier11.pkl (95MB) exceeds GitHub's 25MB limit

📥 Download it here → [Google drive ](https://drive.google.com/file/d/1hk-aGWH5RFlWxUqb2Sq_HUqGmrNSnHWz/view?usp=drive_link)


## 📊 Dataset

| Property        | Value                                      |
|----------------|--------------------------------------------|
| Total Questions | 3,857                                      |
| Classes         | 3 (database, platform, general)             |
| Test Set Size   | 300 (100 per class)                         |
| Format          | XLSX                                       |
| Source          | Manually curated for NPCYF AI CoPilot       |

## 🚀 How to Run

```bash
git clone https://github.com/ajml8/-IntentClassification-for-the-NPCYF-AI-CoPilot.git
cd Intent-Classification-for-the-NPCYF-AI-CoPilot
```
## 2. Install Dependencies
```bash
pip install scikit-learn sentence-transformers pandas numpy openpyxl
```
## 3. Download the Model
Download intent_classifier11.pkl from the  [Google drive ](https://drive.google.com/file/d/1hk-aGWH5RFlWxUqb2Sq_HUqGmrNSnHWz/view?usp=drive_link) and place it in the project folder
## 4. Run Training (Optional)
Open and run intent_classifier.ipynb in Jupyter Notebook

## 🛠️ Tech Stack

| Tool                | Purpose                                   |
|---------------------|-------------------------------------------|
| Python 3.x          | Core language                             |
| scikit-learn        | LinearSVC, TF-IDF, Pipeline               |
| sentence-transformers | all-MiniLM-L6-v2 embeddings             |
| pandas / numpy      | Data handling                             |
| Jupyter Notebook    | Development environment                   |
| pickle              | Model serialisation                       |

## 🏛️ About the Organisation
This project was built during an internship at:

*IDEAS-TIH* — Institute of Data Engineering, Analytics and Science Foundation
Indian Statistical Institute (ISI), Kolkata
## 👨‍💻 Author
Muhammed Ajmal mc
## Licence
This project was developed as part of an internship at IDEAS-TIH, ISI Kolkata. All rights reserved.
