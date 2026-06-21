# AI201 Project 3 — TakeMeter

## Overview

TakeMeter is a text classification project that identifies different discussion styles within One Piece Reddit communities.

The classifier categorizes comments into one of three labels:

- Analysis
- Opinion
- Reaction

The goal is to determine whether a comment is primarily reasoning-based, expresses a personal judgment, or reflects an emotional response.

---

## Community

Data was collected from One Piece discussion communities, including:

- r/OnePiece
- r/shounenfolk
- r/OnePiecePowerScaling

These communities contain a mixture of character analysis, arc discussions, powerscaling debates, personal rankings, and reactions to new chapters and episodes.

---

## Labels

### Analysis

Comments that use reasoning, evidence, comparisons, or explanations to support a claim.

Example:

> "Fishman Island demonstrates the cycle of hatred through Hody Jones."

### Opinion

Comments that express personal preferences, rankings, or subjective judgments.

Example:

> "Fishman Island is the worst arc."

### Reaction

Comments that primarily express an emotional response.

Example:

> "That chapter blew my mind."

---

## Dataset

Total examples: 201

Label distribution:

| Label    | Count |
| -------- | ----- |
| Analysis | 74    |
| Opinion  | 74    |
| Reaction | 53    |

Dataset files:

- `labeled_dataset.csv` – original labeled dataset with notes
- `anime_classifier.csv` – cleaned dataset used for training

---

## Model

Model used:

- DistilBERT (`distilbert-base-uncased`)

Training approach:

- Label encoding
- 80/20 train-test split
- Fine-tuning using Hugging Face Transformers
- Evaluation using Accuracy, Precision, Recall, and F1 Score

---

## Results

| Metric    | Score  |
| --------- | ------ |
| Accuracy  | 92.68% |
| Precision | 92.74% |
| Recall    | 92.68% |
| F1 Score  | 92.63% |

### Confusion Matrix Analysis

The model achieved perfect classification on Analysis examples within the test set.

Most classification errors occurred between Opinion and Reaction comments, which is expected because both categories frequently contain subjective or emotional language.

The classifier demonstrated strong separation between analytical discussion and other discussion styles.

---

## Files

```text
ai201-project3-takemeter/
│
├── planning.md
├── README.md
├── evaluation_results.json
├── confusion_matrix.png
│
└── data/
    ├── labeled_dataset.csv
    └── anime_classifier.csv
```

---

## Conclusion

The fine-tuned DistilBERT classifier achieved over 92% accuracy and F1 score on the test set. The results indicate that discussion styles within One Piece communities can be reliably classified into Analysis, Opinion, and Reaction categories using a relatively small manually labeled dataset.
