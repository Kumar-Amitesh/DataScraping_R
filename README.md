# Data Processing Report: BBC News & Reddit Dataset

## Introduction

This report outlines the end-to-end process of collecting, cleaning, and refining a dataset sourced from **BBC News articles** and **Reddit posts**. The objective is to prepare a structured, enriched dataset that serves a wide range of analytical applications including sentiment analysis, trend tracking, content classification, summarization, and misinformation detection.

## Dataset Description

The dataset aggregates information from two primary sources:

* **BBC News**: A curated collection of articles across various domains such as Politics, Business, Technology, Science, Health, Entertainment, and Sports.
* **Reddit Posts**: Discussions pulled from subreddits including `r/technology`, `r/science`, `r/worldnews`, and `r/programming`, offering diverse perspectives on trending topics.

Each entry includes:

* Headline
* Full text
* Category
* Publication timestamp (with separate date and time)
* Article/post link
* Sentiment score
* Extracted keywords
* Author information
* Summary
* Word count

All data is compiled into a consistent tabular format for ease of analysis.

## Data Collection

### BBC News Articles

Data was collected using R’s `rvest` and `httr` libraries. XPath and CSS selectors were used to extract structured content such as headlines, publication dates, and article text.

### Reddit Posts

Data was retrieved using the `RedditExtractoR` package, which combines API-based access with web scraping to gather structured metadata and post content.

## Data Wrangling Steps

To ensure the dataset is clean, relevant, and reliable, the following preprocessing steps were carried out:

1. **Handling Missing Values**

   * Empty headlines were replaced with `"Unknown"`.
   * Rows missing critical information (e.g., links or full text) were removed.

2. **Duplicate Removal**

   * String-matching techniques were applied to identify and eliminate duplicates.

3. **Standardizing Encoding**

   * All text was standardized to UTF-8 to prevent misinterpretation of special characters.

4. **Text Cleaning**

   * Removed HTML tags, special characters, extra whitespaces, and unnecessary line breaks.
   * Normalized content to improve readability and consistency.

5. **Timestamp Conversion**

   * A custom `convert_relative_time()` function was implemented to convert relative timestamps (e.g., “2 days ago”) into absolute datetime fields.

6. **Categorization**

   * Keyword-based rules were used to assign entries to predefined categories.
   * An AI-based approach using the **Gemini API** was added for dynamic categorization and summarization.
   * A fallback function `extract_article_details_r()` ensures robustness in case of API failures.

7. **Metadata Extraction**

   * Improved HTML parsing was employed to reliably extract author names and other metadata.

8. **Feature Engineering**

   * **Word Count**: Calculated for each entry to analyze content length.
   * **Sentiment Score**: Polarity scores assigned using a sentiment analysis model.
   * **Keyword Extraction**: TF-IDF was applied to identify relevant terms.

## Challenges and Solutions

* **Data Format Inconsistencies**
  Handled using string manipulation and formatting functions to maintain structural uniformity.

* **Anti-Scraping Measures**
  Managed by setting user-agent headers and introducing time delays between requests.

* **Varying Text Lengths**
  Filtered out excessively short Reddit posts to ensure only relevant content was retained.

## Potential Use Cases

This refined dataset unlocks several analytical and machine learning opportunities:

* **Sentiment Analysis**: Understand public opinion on various topics.
* **Trend Detection**: Track emerging issues and common themes across platforms.
* **News Categorization**: Train models for automatic article classification.
* **Text Summarization**: Generate concise summaries for lengthy articles.

## Summary Statistics and Visualizations

To gain insights into the dataset, the following visual tools were created:

* **News Category Distribution**: Bar chart showing the frequency of each category.
* **Sentiment Score Distribution**: Histogram visualizing polarity scores.
* **Word Frequency Analysis**: Word cloud highlighting the most common terms.

## Conclusion

This report demonstrates a comprehensive pipeline for transforming raw content from news and social media into a clean, enriched dataset. The inclusion of structured metadata, AI-powered summarization, and extensive preprocessing makes the dataset highly suitable for a variety of downstream applications. The final dataset is saved as a CSV file for ease of access and sharing.

