# Microsoft Fabric: Bing News Sentiment Analysis

## 📌 Project Overview
This project demonstrates an end-to-end data analytics pipeline using **Microsoft Fabric**. It automates the extraction of news data using the **Bing Search API v7**, processes it using **Synapse Data Engineering**, performs sentiment analysis via **Synapse ML**, and visualizes the results in **Power BI**. Additionally, it sets up real-time alerts using **Data Activator** and **Microsoft Teams**.

## 🏗️ System Architecture
The solution leverages the following Microsoft Fabric components:

1.  **Bing Search API v7:** Acts as the data source, fetching real-time news articles and metadata.
2.  **Data Factory:** Handles the ETL process (Extract, Transform, Load).It orchestrates pipelines to fetch data from the API and load it into the data lake.
3.  **OneLake:** Serves as the centralized storage repository for structured and unstructured data (JSON files).
4.  **Synapse Data Engineering:** Uses PySpark notebooks to clean, explode, and transform raw JSON data into structured Delta tables.
5.  **Synapse ML (Data Science):** Applies pre-built machine learning models (`AnalyzeText`) to perform sentiment analysis on news descriptions.
6.  **Power BI:** Visualizes sentiment trends (Positive, Neutral, Negative) through interactive dashboards.
7.  **Data Activator & Teams:** Monitors Power BI metrics in real-time and triggers alerts to Microsoft Teams when specific sentiment thresholds are met.

## ⚙️ Methodology

### 1. Data Ingestion
* A **Data Factory pipeline** (`Bing_Data_Pipeline_TanishQ`) was created to copy news data using the Bing Search API.
* **Source:** REST API call to `https://api.bing.microsoft.com/v7.0/search` with parameters for "latest news".
* **Destination:** Stored as JSON files (e.g., `Bing-Latest-News-TanishQ.json`) in the Lakehouse.

### 2. Data Transformation (ETL)
* Raw JSON data is read into a **Spark DataFrame**.
* The complex JSON structure (nested arrays of providers and images) is "exploded" and flattened into a readable schema.
* Key columns extracted: `title`, `description`, `category`, `url`, `image`, `provider`, and `datePublished`.
* The cleaned data is saved to a Delta table: `tbl_latest_news`.

### 3. Sentiment Analysis
* **Model:** We utilized Synapse ML's `AnalyzeText` model for sentiment classification.
* **Process:** The model analyzes the `description` column and outputs a sentiment label (Positive, Neutral, Negative).
* **Output:** Results are stored in a final Delta table: `tbl_sentiment_analysis`.

### 4. Visualization & Alerting
* **Power BI:** A report connects to the sentiment table, displaying metrics like "19.15% Negative Sentiment" and "65.96% Neutral Sentiment".
* **Data Activator:** A trigger is set to monitor the "Positive Sentiment %". [cite_start]If it becomes greater than 0, an alert is automatically sent to a specified Microsoft Teams channel.

## 📊 Sample Results
* **Negative Sentiment:** ~19% 
* **Neutral Sentiment:** ~66% 
* **Positive Sentiment:** ~15% 

## 🚀 Getting Started
1.  **Prerequisites:** Microsoft Fabric capacity, Azure Subscription (for Bing Search API key).
2.  **Setup:** Clone this repo and import the notebooks into your Fabric workspace.
3.  **Config:** Update the API Key in the Data Factory pipeline connection settings.

## 👤 Author
Tanishk Nanasaheb Shinde
