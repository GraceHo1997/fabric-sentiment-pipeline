### 📊 Bing News Sentiment Analysis Pipeline (Microsoft Fabric)

An end-to-end data engineering and analytics pipeline built in Microsoft Fabric to ingest real-time news from the Bing API, transform JSON into Delta tables, perform sentiment analysis using SynapseML, and trigger automated alerts in Microsoft Teams when positive sentiment exceeds a defined threshold.

#### Project Objective
Build a fully automated pipeline that:
- Ingests daily news data from Bing News API
- Stores raw JSON in OneLake (Bronze layer)
- Transforms and cleans data into structured Delta tables
- Performs sentiment analysis on news descriptions
- Publishes metrics to Power BI
- Sends Teams alert when Positive Sentiment % > 30%

#### Architecture Overview
<img width="1048" height="563" alt="image" src="https://github.com/user-attachments/assets/59fb53f6-2db0-438d-b59c-c207c9e51247" />
