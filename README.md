# Microsoft Fabric: Bing News Sentiment Analysis

## 📌 Project Overview
This project demonstrates an end-to-end data analytics pipeline using **Microsoft Fabric**. It automates the extraction of news data using the **Bing Search API v7**, processes it using **Synapse Data Engineering**, performs sentiment analysis via **Synapse ML**, and visualizes the results in **Power BI**. Additionally, it sets up real-time alerts using **Data Activator** and **Microsoft Teams**.

## 🏗️ System Architecture
The solution leverages the following Microsoft Fabric components:

1.  [cite_start]**Bing Search API v7:** Acts as the data source, fetching real-time news articles and metadata[cite: 2181, 2182].
2.  **Data Factory:** Handles the ETL process (Extract, Transform, Load). [cite_start]It orchestrates pipelines to fetch data from the API and load it into the data lake[cite: 2184, 2185].
3.  [cite_start]**OneLake:** Serves as the centralized storage repository for structured and unstructured data (JSON files)[cite: 2187, 2189].
4.  [cite_start]**Synapse Data Engineering:** Uses PySpark notebooks to clean, explode, and transform raw JSON data into structured Delta tables[cite: 2191, 2452, 2699].
5.  [cite_start]**Synapse ML (Data Science):** Applies pre-built machine learning models (`AnalyzeText`) to perform sentiment analysis on news descriptions[cite: 2194, 2776].
6.  [cite_start]**Power BI:** Visualizes sentiment trends (Positive, Neutral, Negative) through interactive dashboards[cite: 2198, 2199].
7.  [cite_start]**Data Activator & Teams:** Monitors Power BI metrics in real-time and triggers alerts to Microsoft Teams when specific sentiment thresholds are met[cite: 2201, 2204].

## ⚙️ Methodology

### 1. Data Ingestion
* [cite_start]A **Data Factory pipeline** (`Bing_Data_Pipeline_TanishQ`) was created to copy news data using the Bing Search API[cite: 2268, 2295].
* [cite_start]**Source:** REST API call to `https://api.bing.microsoft.com/v7.0/search` with parameters for "latest news"[cite: 2330, 2374].
* [cite_start]**Destination:** Stored as JSON files (e.g., `Bing-Latest-News-TanishQ.json`) in the Lakehouse[cite: 2401].

### 2. Data Transformation (ETL)
* [cite_start]Raw JSON data is read into a **Spark DataFrame**[cite: 2452].
* [cite_start]The complex JSON structure (nested arrays of providers and images) is "exploded" and flattened into a readable schema[cite: 2488].
* [cite_start]Key columns extracted: `title`, `description`, `category`, `url`, `image`, `provider`, and `datePublished`[cite: 2660].
* [cite_start]The cleaned data is saved to a Delta table: `tbl_latest_news`[cite: 2698].

### 3. Sentiment Analysis
* [cite_start]**Model:** We utilized Synapse ML's `AnalyzeText` model for sentiment classification[cite: 2776].
* [cite_start]**Process:** The model analyzes the `description` column and outputs a sentiment label (Positive, Neutral, Negative)[cite: 2791].
* [cite_start]**Output:** Results are stored in a final Delta table: `tbl_sentiment_analysis`[cite: 2846].

### 4. Visualization & Alerting
* [cite_start]**Power BI:** A report connects to the sentiment table, displaying metrics like "19.15% Negative Sentiment" and "65.96% Neutral Sentiment"[cite: 2886, 2889].
* **Data Activator:** A trigger is set to monitor the "Positive Sentiment %". [cite_start]If it becomes greater than 0, an alert is automatically sent to a specified Microsoft Teams channel[cite: 2931, 2946].

## 📊 Sample Results
* [cite_start]**Negative Sentiment:** ~19% [cite: 2886]
* [cite_start]**Neutral Sentiment:** ~66% [cite: 2889]
* [cite_start]**Positive Sentiment:** ~15% [cite: 2890]

## 🚀 Getting Started
1.  **Prerequisites:** Microsoft Fabric capacity, Azure Subscription (for Bing Search API key).
2.  **Setup:** Clone this repo and import the notebooks into your Fabric workspace.
3.  [cite_start]**Config:** Update the API Key in the Data Factory pipeline connection settings[cite: 2336].

## 👤 Author
[cite_start]Tanishq Shinde [cite: 2211, 2239]
