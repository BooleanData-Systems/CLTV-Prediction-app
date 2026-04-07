# CLTV Status & Value Predictor

This application predicts Customer Lifetime Value (CLV) status and dollar value based on customer attributes such as age, income, spending behavior, credit score, and engagement metrics.

## How to Use

1. Install the app and connect a warehouse.
2. The Streamlit interface opens with two tabs: **Single Prediction** and **Batch Prediction**.

### Single Prediction
Enter customer details manually and click "Predict CLV" to get a real-time prediction with:
- CLV Status (e.g., High, Medium, Low)
- Predicted Lifetime Value in dollars
- Probability scores for each status category

### Batch Prediction (Data-Centric)
1. Go to the app **Settings** (gear icon) > **References** tab.
2. Grant SELECT access on your customer data table (`consumer_data_table` reference).
3. Optionally grant SELECT + INSERT access on a results table (`consumer_results_table` reference).
4. Return to the **Batch Prediction** tab, preview your data, and click **Run Batch Predictions**.
5. Download results as CSV or have them written to your results table.

## Required Table Schema

Your customer data table must contain the following columns:

| Column | Type | Description |
|--------|------|-------------|
| AGE | NUMBER | Customer age in years |
| INCOME | FLOAT | Annual income |
| REGION | VARCHAR | Geographic region (East, West, Central, South, North) |
| AVG_MONTHLY_SPEND | FLOAT | Average monthly spend amount |
| AVG_TRANSACTION_VALUE | FLOAT | Average value per transaction |
| CREDIT_SCORE | FLOAT | Customer credit score (300-850) |
| NUM_PRODUCTS | NUMBER | Number of products held |
| TENURE_MONTHS | FLOAT | Months as a customer |
| PREFERRED_CHANNEL | VARCHAR | Preferred channel (Online, In-Store, Mobile, Phone) |
| DISCOUNT_USAGE_RATE | FLOAT | Discount usage rate (0 to 1) |

## Results Table Schema (Optional)

If you connect a results table, it should have the following columns:

| Column | Type |
|--------|------|
| AGE | NUMBER |
| INCOME | FLOAT |
| REGION | VARCHAR |
| AVG_MONTHLY_SPEND | FLOAT |
| AVG_TRANSACTION_VALUE | FLOAT |
| CREDIT_SCORE | FLOAT |
| NUM_PRODUCTS | NUMBER |
| TENURE_MONTHS | FLOAT |
| PREFERRED_CHANNEL | VARCHAR |
| DISCOUNT_USAGE_RATE | FLOAT |
| PREDICTED_STATUS | VARCHAR |
| PREDICTED_CLV | FLOAT |
| PROB_HIGH | FLOAT |
| PROB_MEDIUM | FLOAT |
| PROB_LOW | FLOAT |

## Features

- Pre-trained classification model for CLV status prediction
- Pre-trained regression model for CLV dollar value prediction
- Single-customer prediction with real-time probability scores
- Batch prediction against consumer's own Snowflake tables
- Results written back to consumer's Snowflake table
- CSV export of prediction results
- Interactive Streamlit interface with no external dependencies

## Requirements

- A Snowflake warehouse connected to the app
- For batch mode: a customer data table matching the schema above
