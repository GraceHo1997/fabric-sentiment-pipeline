### 📊 Bing News Sentiment Analysis Pipeline (Microsoft Fabric)

An end-to-end data engineering and analytics pipeline built in Microsoft Fabric to ingest daily news from the Bing API, transform JSON into Delta tables, perform sentiment analysis using SynapseML, and trigger automated alerts in Microsoft Teams.

#### Project Objective
This project demonstrates how to design and implement a production-style analytics pipeline that:
- Ingests latest news data from Bing News API
- Stores raw JSON in OneLake (Bronze layer)
- Transforms data into curated Delta tables
- Performs sentiment classification (Positive / Negative / Neutral)
- Visualizes results in Power BI
- Sends automated Teams alert when Positive Sentiment % > 30%
The pipeline runs daily at 8:00 AM using Microsoft Fabric Data Factory.

#### Architecture Overview
<img width="1048" height="563" alt="image" src="https://github.com/user-attachments/assets/59fb53f6-2db0-438d-b59c-c207c9e51247" />
Bing News API 
-> Data Factory Pipeline (Daily @ 8:00 AM)
-> OneLake (Bronze - Raw JSON)
-> Synapse Data Engineering Notebook
-> Silver Delta Table (Cleaned Data)
-> Synapse Data Science (Sentiment Model)
-> Gold Delta Table (Enriched Data)
-> Power BI Semantic Model
-> Data Activator → Microsoft Teams Alert

#### Technology Stack
| Layer | Tool |
|-------|------|
| Orchestration | Microsoft Fabric Data Factory |
| Storage | OneLake (Lakehouse) |
| Processing | Synapse Data Engineering |
| Machine Learning | Synapse Data Science + SynapseML |
| Modeling | SQL MERGE (SCD Type 1) |
| Visualization | Power BI |
| Alerting |  Microsoft Teams |

#### Data Pipeline Details

1️⃣ Data Ingestion (Bing API → OneLake)
- REST API connection to Bing News API
- Parameterized pipeline (API key, keyword, date filter)
- Scheduled trigger (runs daily at 8:00 AM)
- Raw JSON stored in OneLake (Bronze layer)
This establishes the foundation for downstream analytics.

2️⃣ Data Transformation (JSON → Delta)
- Using Synapse Data Engineering (Spark notebook):
- Load raw JSON into Spark DataFrame
- Flatten nested fields
- Clean and standardize columns
- Remove duplicates
- Handle null values
- Write structured data into Delta table (Silver layer)

3️⃣ Incremental Load Strategy
- Implemented Slowly Changing Dimension (SCD) Type 1 logic.
- SCD Type 1 Characteristics
- Overwrites existing records
- No historical tracking
- Maintains latest state only

Ensures:
- Idempotent daily loads
- No duplicate records
- Efficient incremental updates

4️⃣ Sentiment Analysis (SynapseML)

Using Synapse Data Science, we apply a pre-built sentiment model on the description column.

The model classifies each article as:
- Positive
- Negative
- Neutral
Enriched data is stored in a Gold Delta table for reporting.

5️⃣ Data Modeling & Reporting (Power BI)

Power BI connects directly to the Fabric Lakehouse.

Dashboard Includes:
- Sentiment % KPI
- News detailed information
- Count by sentiment

6️⃣ Automated Alerting (Data Activator → Teams)

- Alert is configured with the condition:
  Positive Sentiment % > 0.30
- When triggered:
  A Microsoft Teams notification is automatically sent.
This enables proactive monitoring and real-time business awareness.

🧪 End-to-End Pipeline Testing

The full pipeline was tested from ingestion to dashboard update to ensure:
- Data integrity
- Accurate transformation logic
- Correct incremental load behavior
- Dashboard auto-refresh
- Alert functionality

This validates the reliability and performance of the pipeline.

#### Key Engineering Highlights
- End-to-end automated data pipeline
- REST API ingestion
- JSON parsing and schema flattening
- Delta Lake implementation
- SQL MERGE incremental logic
- SCD Type 1 modeling
- ML inference integration
- Event-driven Teams alerting
- Production-style medallion architecture

#### This project was inspired by learning materials from:

Mr. K Talks Tech

– – – Support the creator – – –

Please Subscribe: https://www.youtube.com/@mr.ktalkstech
