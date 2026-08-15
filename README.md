# Bangla Social Media NLP Analytics

[![Python](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Plotly](https://img.shields.io/badge/Visualization-Plotly-3f4f75.svg)](https://plotly.com/python/)
[![NLP](https://img.shields.io/badge/NLP-Bangla-green.svg)](#)

**Bangla Social Media NLP Analytics** is a notebook-based exploratory analytics project for **Bangla social-media text**. The repository demonstrates Bangla text cleaning, rule-based sentiment labeling, exploratory data analysis, and interactive visualizations for social-media comments.

The current repository contains:

- **Facebook comment sentiment analysis and EDA**
- **YouTube analytics experiment notebook**

The Facebook workflow classifies Bangla comments into:

- **Positive**
- **Negative**
- **Neutral**

and visualizes the resulting public-sentiment patterns using Plotly and WordCloud.

---

## Key Features

- Bangla Unicode text detection
- Emoji removal
- Bangla-only text filtering
- Custom Bangla stop-word removal
- Punctuation removal
- Rule-based sentiment classification
- Positive / negative / neutral sentiment analysis
- Interactive Plotly visualizations
- Sentiment distribution analysis
- Comment-length analysis
- Positive and negative word-frequency analysis
- Bangla word-cloud generation
- Facebook comment analytics
- Separate YouTube analytics experiment notebook
- Google Colab compatible workflow

---

## Repository Structure

```text
Bangla-Social-Media-NLP-Analytics/
├── EDA_Facebook_Analytics_BN_NLP.ipynb
├── yt_analytics_dep_test.ipynb
└── README.md
```

---

## Facebook Bangla NLP Workflow

The main Facebook notebook loads a Bangla Facebook-comment sentiment dataset and performs the following workflow:

```text
Facebook Comments
       │
       ▼
Dataset Loading
       │
       ▼
Bangla Text Detection
       │
       ▼
Emoji Removal
       │
       ▼
Remove Non-Bangla Characters
       │
       ▼
Stop-word + Punctuation Removal
       │
       ▼
Cleaned Bangla Comments
       │
       ▼
Rule-Based Sentiment Analysis
 ┌─────┼─────┐
 ▼     ▼     ▼
Positive Neutral Negative
       │
       ▼
Exploratory Data Analysis
       │
       ▼
Interactive Visualizations
```

---

## Bangla Text Preprocessing

### Bangla Character Detection

The notebook checks whether text contains Bangla Unicode characters using:

```python
bangla_regex = re.compile(r'[\u0980-\u09FF]')
```

### Emoji Removal

Emojis are removed using the `emoji` package:

```python
emoji.replace_emoji(text, replace=" ")
```

### Bangla Text Cleaning

The cleaning workflow:

1. Removes emojis
2. Removes non-Bangla characters
3. Splits text into tokens
4. Removes custom Bangla stop words
5. Removes punctuation
6. Joins the remaining words

Simplified implementation:

```python
def clean_bangla_text(text):
    text = remove_emojis(text)
    text = re.sub(r"[^\u0980-\u09FF\s]", "", text)
    words = text.split()
    cleaned_words = [
        word for word in words
        if word not in stop_words
        and word not in punctuations
    ]
    return " ".join(cleaned_words)
```

---

## Sentiment Analysis

The Facebook notebook uses manually defined **positive** and **negative Bangla emotion-word dictionaries**.

The cleaned comment is classified according to the presence of sentiment-bearing words:

```python
def classify_bangla_sentiment(
    text,
    positive_emotions,
    negative_emotions
):
    words = set(text.split())

    if words & positive_emotions:
        return "positive"
    elif words & negative_emotions:
        return "negative"

    return "neutral"
```

### Sentiment Classes

```text
Positive
Negative
Neutral
```

> This is a lexicon/rule-based sentiment approach rather than a trained machine-learning or transformer classifier.

---

## Facebook Dataset

The notebook currently loads a public CSV directly from GitHub:

```python
df = pd.read_csv(
    "https://raw.githubusercontent.com/"
    "shorna99/using_ML_to_classify-B_comment-/main/"
    "FB_Comment_Sentiment%20-%20Sheet1.csv"
)
```

The processed workflow creates fields such as:

```text
Cleaned_Comment
Sentiment
Comment_Length
```

---

## Exploratory Data Analysis

The notebook contains several visual analyses.

### 1. Dataset Table

A Plotly table is used to display the loaded Facebook-comment dataset.

### 2. Sentiment Distribution

The notebook visualizes the distribution of:

```text
Positive
Negative
Neutral
```

comments using graphical summaries.

### 3. Sentiment Percentage

A donut-style visualization is used to show the relative proportion of each sentiment class.

### 4. Sunburst Visualization

The notebook creates an interactive Plotly sunburst chart:

```python
px.sunburst(
    df,
    path=["Sentiment", "Cleaned_Comment"],
    title="Sunburst Chart: Public Sentiment for Facebook Post"
)
```

### 5. Comment Length by Sentiment

Comment lengths are calculated using:

```python
df["Comment_Length"] = df["Cleaned_Comment"].apply(len)
```

A box plot is then used to compare comment lengths among sentiment groups.

### 6. Positive Word Frequency

The most frequent words from positive comments are extracted and ranked.

### 7. Negative Word Frequency

The same analysis is performed for negative comments.

The notebook displays the **top 15 positive and negative words** using Plotly bar charts.

### 8. Bangla Word Cloud

A WordCloud is generated from the cleaned Bangla comments.

Because Bangla text requires a compatible font, the original notebook references a Bangla font file through Google Drive.

---

## Example Analytics Pipeline

```text
Raw Bangla Comment
        │
        ▼
"অসাধারণ কাজ! ❤️"
        │
        ▼
Remove Emoji / Symbols
        │
        ▼
"অসাধারণ কাজ"
        │
        ▼
Stop-word Filtering
        │
        ▼
Sentiment Lexicon Matching
        │
        ▼
Positive
```

---

## YouTube Analytics

The repository also includes:

```text
yt_analytics_dep_test.ipynb
```

for a separate YouTube analytics experiment.

It is kept separate from the Facebook EDA notebook so that Facebook Bangla sentiment exploration and YouTube-oriented analysis can be developed independently.

---

## Technologies Used

- Python
- Jupyter Notebook / Google Colab
- Pandas
- Regular Expressions (`re`)
- Emoji
- Plotly
- Matplotlib
- WordCloud
- Collections / Counter

---

## Installation

Clone the repository:

```bash
git clone https://github.com/kowshir-bitto/Bangla-Social-Media-NLP-Analytics.git
cd Bangla-Social-Media-NLP-Analytics
```

Install the main dependencies:

```bash
pip install pandas plotly matplotlib wordcloud emoji jupyter
```

---

## Running the Project

Start Jupyter Notebook:

```bash
jupyter notebook
```

Then open:

```text
EDA_Facebook_Analytics_BN_NLP.ipynb
```

or:

```text
yt_analytics_dep_test.ipynb
```

You can also upload the notebooks directly to **Google Colab**.

---

## Bangla WordCloud Font

For Bangla WordCloud generation, use a Bangla-compatible `.ttf` font.

The current notebook contains a Google Drive-specific font path:

```python
font_path = "/content/drive/MyDrive/Front Bangla/SolaimanLipi_20-04-07.ttf"
```

Change this to the location of a Bangla font available in your environment.

For example:

```python
font_path = "path/to/BanglaFont.ttf"
```

---

## Important Notes

- The Facebook sentiment method is **rule-based** and depends on the coverage of the manually defined positive and negative word lists.
- A comment containing sentiment expressions not included in the lexicon may be labeled neutral.
- The project is intended primarily as an NLP analytics/EDA demonstration.
- The Facebook dataset is loaded from an external GitHub-hosted CSV.
- Some notebook paths, especially the Bangla font path, are specific to Google Colab/Google Drive and should be changed when running locally.

---

## Potential Extensions

The project can be extended with:

- Bangla BERT / BanglaBERT sentiment classification
- Transformer-based sentiment models
- Larger Bangla sentiment datasets
- YouTube Data API integration
- Facebook/YouTube analytics dashboard
- Streamlit or Dash deployment
- Topic modeling
- Emotion classification
- Toxic-comment detection
- Temporal sentiment analysis

---

## Research / Learning Applications

This repository can be useful for:

- Bangla Natural Language Processing
- Social-media sentiment analysis
- Bangla text preprocessing
- Exploratory data analysis
- Social-media analytics
- Interactive data visualization
- NLP dashboard prototyping

---

## Author

**Abu Kowshir Bitto**

- GitHub: [@kowshir-bitto](https://github.com/kowshir-bitto)
- Website: [kowshirbitto.me](http://kowshirbitto.me/)
- Google Scholar: [Abu Kowshir Bitto](https://scholar.google.com/citations?hl=en&user=AO0dWsgAAAAJ&view_op=list_works&gmla=AJ1KiT30Ms5pY2DUl6pfWl4cwjlBOwygW_3wawpWiD_769YBbLX8_0rqv4MiIf05GjDe6xY81ApN7Gy1DfwYJCZu)
