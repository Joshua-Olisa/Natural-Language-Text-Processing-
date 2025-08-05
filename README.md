# NLT Analysis: Airline Review NLP Pipeline

This repository contains a Jupyter Notebook (`NLT Analysis.ipynb`) in which we scrape, clean, analyze, and model text data from airline reviews. The goal is to demonstrate end-to-end NLP techniques—culminating in sentiment analysis and topic modeling—to generate actionable insights.

## Table of Contents
1. [Task 1: Web Scraping & Data Collection](#task-1)
2. [Data Cleaning](#data-cleaning)
3. [Loading & Inspecting Data](#loading--inspecting-data)
4. [Word Cloud Analysis](#word-cloud-analysis)
5. [Text Preprocessing](#text-preprocessing)
   - Tokenization  
   - Stopword Removal  
   - Lemmatization  
6. [Word Frequency Analysis](#word-frequency-analysis)
7. [Topic Modeling](#topic-modeling)
   - Coherence Evaluation  
   - LDA Fitting  
   - Topic Labeling
8. [Sentiment Analysis](#sentiment-analysis)
9. [Linking Sentiment to Topics](#linking-sentiment-to-topics)

---

## Task 1: Web Scraping & Data Collection

- **Objective:** Gather passenger reviews for British Airways from AirlineQuality.com.  
- **Steps:**
  1. Sent HTTP requests to the main airline reviews page.  
  2. Parsed the HTML to extract links to individual review pages.  
  3. Iterated through review URLs, scraped review text and metadata (date, rating).  
  4. Consolidated results into a pandas DataFrame and exported it as `BA_reviews.csv`.

---

## Data Cleaning

- **Objective:** Ensure the raw CSV is free of artifacts before analysis.  
- **Steps:**
  1. Opened `BA_reviews.csv` in Excel (per notebook note) to manually remove empty rows and fix encoding issues.  
  2. Saved the cleaned file back to `BA_reviews_clean.csv`.

---

## Loading & Inspecting Data

- **Objective:** Bring the cleaned data into Python and perform initial sanity checks.  
- **Steps:**
  1. Used `pandas.read_csv()` to load `BA_reviews_clean.csv`.  
  2. Inspected `DataFrame.info()` and `DataFrame.head()` to verify column types and null counts.

---

## Word Cloud Analysis

- **Objective:** Visualize the most common words across all reviews.  
- **Steps:**
  1. Installed the `wordcloud` package.  
  2. Preprocessed the text: removed special characters, converted to lowercase.  
  3. Generated and displayed a word cloud of the top 200 tokens.

---

## Text Preprocessing

### Tokenization

- **Objective:** Break each review into individual words.  
- **Steps:**
  1. Imported `TreebankWordTokenizer` from NLTK.  
  2. Applied it to each review to produce lists of tokens.

### Stopword Removal

- **Objective:** Remove common words that carry little semantic weight.  
- **Steps:**
  1. Downloaded NLTK’s English stopword list.  
  2. Filtered out tokens present in `stopwords.words('english')`.

### Lemmatization

- **Objective:** Reduce tokens to their dictionary form.  
- **Steps:**
  1. Initialized NLTK’s `WordNetLemmatizer`.  
  2. Applied it to each token, preserving part-of-speech tags where possible.

---

## Word Frequency Analysis

- **Objective:** Identify the top 20 most frequent lemmatized words.  
- **Steps:**
  1. Flattened the list of all tokens and counted occurrences with `collections.Counter`.  
  2. Plotted a bar chart of the top 20 words using Matplotlib.

## Topic Modeling

- **Objective:** Discover latent themes in the review corpus.  
- **Steps:**
  1. Prepared the token lists from preprocessing (no further cleaning).  
  2. Created a Gensim dictionary and corpus.  
  3. Computed coherence scores for topic counts 2 through 10.  
  4. Selected **7 topics** based on the highest coherence.  
  5. Fitted LDA to the corpus and extracted the top 10 keywords per topic.

---

### Topic Labeling

- **Objective:** Assign human-readable labels to each topic.  
- **Steps:**
  1. Reviewed keyword lists for each of the 7 topics.  
  2. Chose descriptive labels (e.g., *Customer Service*, *Delays*, *Seating*, etc.).  
  3. Merged labels back into the review DataFrame for context.

---

---

## Sentiment Analysis

- **Objective:** Gauge the overall tone of each review.  
- **Steps:**
  1. Chose VADER from NLTK’s `SentimentIntensityAnalyzer` for its nuance with longer texts.  
  2. Calculated `compound` sentiment scores for each review.  
  3. Classified reviews as Positive (≥ 0.05), Negative (≤ –0.05), or Neutral (otherwise).  
  4. Visualized sentiment distribution with Seaborn and explored correlation with review length.

---

## Linking Sentiment to Topics

- **Objective:** Provide qualitative insights on how topics align with sentiment.  
- **Approach:**
  - Not a formal statistical join, but logical inference:
    - Topics heavy in complaints (e.g., *Delays*, *Customer Service*) map to negative sentiment.
    - Topics about comfort (“food,” “seating”) tend toward positive sentiment.
  - Summarized overlaps and highlighted areas for the client’s attention.

---

> **Next Steps:**  
> - Automate the entire ETL to run on new incoming reviews.

---

*End of README*  
