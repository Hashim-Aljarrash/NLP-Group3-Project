# Short Review Sentiment: TF-IDF vs Sentence-BERT

**Course:** ARTI 404 | **Section:** 9MA1 | **Group:** 3 | **Instructor:** Dr. Mohammed Mosuily
College of Computer Science & Information Technology, Imam Abdulrahman Bin Faisal University

**Team**

| Name | Student ID |
|---|---|
| Hashim Aljarrash (Team Leader) | 2230000215 |
| Mohammed Alammari | 2230003182 |
| Ahmad Muhanna | 2230006180 |

## About the project

This project is Option 2 (Review Sentiment Analysis) of the NLP course project. The notebook takes a short English review and returns **Positive** or **Negative**, with a confidence score.

**Experimental question:** Which method classifies short reviews more reliably: TF-IDF with logistic regression, or pretrained Sentence-BERT embeddings with logistic regression?

A review is called *short* if it has 6 words or fewer.

## Data

UCI Sentiment Labelled Sentences (Kotzias et al., 2015): 3,000 sentences from Amazon, IMDB and Yelp, 1,500 Positive and 1,500 Negative.
Source: https://archive.ics.uci.edu/dataset/331

The notebook downloads the data automatically, so no data files are stored in this repository.

The data is split 70/15/15 into training (2,100), development (451) and test (449) sets, stratified by label, with seed 42. Duplicate reviews are kept in the same split.

## Methods

| Method | Text representation | Classifier |
|---|---|---|
| 1. Traditional | TF-IDF (scikit-learn) | Logistic regression |
| 2. Pretrained | Sentence-BERT embeddings (`all-MiniLM-L6-v2`, sentence-transformers) | Logistic regression |

Settings (n-gram range and C) were chosen on the development set. Both methods are compared once on the same test reviews.

## Results (test set)

| Subset | Reviews | Method | Accuracy | Macro F1 |
|---|---|---|---|---|
| All test reviews | 449 | TF-IDF + LR | 0.8441 | 0.8440 |
| | | Sentence-BERT + LR | 0.9131 | 0.9131 |
| Short (6 words or fewer) | 130 | TF-IDF + LR | 0.8923 | 0.8907 |
| | | Sentence-BERT + LR | 0.9231 | 0.9226 |
| Longer (more than 6 words) | 319 | TF-IDF + LR | 0.8245 | 0.8234 |
| | | Sentence-BERT + LR | 0.9091 | 0.9087 |

Sentence-BERT scored higher in every group. On short reviews the gap is small (4 reviews out of 130), so it should be read with care. See the report for the full analysis.

## Repository contents

| Folder | Contents |
|---|---|
| `0_proposal` | Project proposal |
| `1_code` | Notebook (`Group3_Sentiment_Notebook.ipynb`) |
| `2_report` | Project report |
| `3_appendix` | Team appendix |
| `4_powerpoint` | Presentation slides |

## How to run

The notebook was developed in **Jupyter inside Visual Studio Code**, with Python 3.9 or newer.

1. Install Python and the VS Code **Python** and **Jupyter** extensions.
2. Open the `1_code` folder in VS Code.
3. Open `Group3_Sentiment_Notebook.ipynb`, select your Python kernel, and click **Run All**.
4. The first code cell installs the packages automatically (numpy, pandas, scikit-learn, sentence-transformers), so no separate install step is needed.
5. The first run needs internet. It downloads the dataset (small) and the Sentence-BERT model (about 90 MB).

The notebook creates `data/` and `results/` folders next to itself. Results are saved to `results/` as CSV files.

If the first cell installs new packages, restart the kernel and run all cells again.

## Notebook sections

1. Setup
2. Data
3. Method 1: TF-IDF + Logistic Regression
4. Method 2: Sentence-BERT + Logistic Regression
5. Results
6. Error analysis
7. Our own examples
8. Try it
9. Sources

## Trying a new review

Go to Section 8 (**Try it**). Edit the `my_review` text in the last code cell and run it. The trained models predict without retraining, and an empty input shows a helpful message instead of an error.

```
Review: "The food was not good"
  TF-IDF + LR -> Negative (0.96)
  SBERT + LR  -> Negative (0.88)
```

## Libraries

numpy, pandas, scikit-learn, sentence-transformers.

## References

- N. Reimers and I. Gurevych, "Sentence-BERT: Sentence embeddings using Siamese BERT-networks," EMNLP-IJCNLP, 2019.
- D. Kotzias, M. Denil, N. de Freitas, and P. Smyth, "From group to individual labels using deep features," KDD, 2015.
