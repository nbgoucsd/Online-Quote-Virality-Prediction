# Online-Quote-Virality-Prediction
# NLP Quote Frequency Prediction

An NLP project exploring whether textual features can be used to predict whether a quote belongs to the highest-frequency group in a large collection of online news quotes.

## Overview

This project uses the **Stanford Memetracker quote dataset** to analyze patterns in frequently repeated quotes and build models that predict whether a quote falls into the highest-frequency group.

The project includes exploratory data analysis, text preprocessing, feature engineering, and comparisons between Bag-of-Words and TF-IDF representations.

## Dataset

The project uses the Stanford Memetracker dataset, which contains quotes extracted from online news and other web sources.

Each document is organized by:

* URL
* Timestamp
* Quote content
* Hyperlinks

The dataset file used in the project is approximately **2.5 GB** compressed. For processing, the analysis reads the dataset and uses the first **20,000 documents** to construct the working dataset.

After normalization, the dataset contains **121,528 unique quotes**.

## Defining High-Frequency Quotes

Quote frequency was calculated by counting how many times each normalized quote appeared in the dataset.

Rather than using a median threshold, the project defines a quote as part of the high-frequency group when its frequency is at or above the **90th percentile** of quote frequency.

This produced:

* **13,271 high-frequency quotes**
* **108,257 other quotes**

## Exploratory Data Analysis

Several characteristics of the quotes were explored:

### Quote Frequency

The frequency distribution shows how often quotes appear throughout the dataset.

### Quote Length

Quote length was compared between high-frequency and other quotes based on the number of words.

### Type-Token Ratio

Type-token ratio (TTR) was used to examine word variety within quotes.

> **TTR = unique words / total words**

These analyses helped investigate whether quote frequency was associated with characteristics such as length and lexical diversity.

## Modeling

The quotes were split into:

* **80% training data**
* **20% test data**
* `random_state = 42`

Three text representations were compared:

### Bag-of-Words — Unigrams

Individual words were used as features. The vocabulary was limited to the **1,000 most frequent unigrams** in the training data.

### Bag-of-Words — Bigrams

Two-word sequences were used as features, again using the **1,000 most frequent bigrams**.

### TF-IDF

TF-IDF features were constructed from the unigram vocabulary. Term frequency was represented as binary presence, with inverse document frequency calculated from the training data.

Each representation was used with a **Ridge regression model** to predict the binary high-frequency label.

## Results

Models were evaluated using **Mean Squared Error (MSE)**.

| Model                   |   Test MSE |
| ----------------------- | ---------: |
| Bag-of-Words (Unigrams) |     0.1000 |
| Bag-of-Words (Bigrams)  |     0.0997 |
| TF-IDF (Unigrams)       | **0.0986** |

The TF-IDF representation produced the lowest test MSE among the three approaches tested.

## Key Takeaways

* The project explored relationships between quote frequency and textual characteristics.
* Unigram, bigram, and TF-IDF representations were compared for predicting high-frequency quotes.
* TF-IDF achieved the lowest test MSE among the evaluated representations.
* The project provided experience with large-scale text preprocessing, exploratory analysis, feature engineering, and NLP model evaluation.

## Tools & Technologies

**Python · Pandas · NumPy · Scikit-learn · Matplotlib · NLP · TF-IDF · Bag-of-Words · Ridge Regression**

## Project Materials

* **Jupyter Notebook:** `CSE158_Assignment_2.ipynb`
* **Project Presentation:** https://youtu.be/BoE1nUrqGXE?si=Ab-0zyg8Td0unJYS
* **Dataset:** Stanford Memetracker

## Limitations

The high-frequency label is based on quote frequency within the dataset and should not be interpreted as a general measure of social-media virality or popularity.

Additionally, model performance was evaluated using MSE. Other classification metrics such as precision, recall, F1 score, and ROC-AUC could provide additional insight into classification performance.
