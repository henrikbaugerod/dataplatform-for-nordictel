## NordicTel synthetic telecom operations dataset

#### What this is
- Fully synthetic CSV dataset for Databricks / lakehouse pipeline demos.
- Business domain: telecom customer, network, billing, and support operations.
- Time span: mostly 2025 H1 for transactional data, with daily tower KPI history across all of 2025.
- Designed for bronze / silver / gold pipelines, CDC ingestion, event joins, and churn modeling.

#### Scale
- Total CSV files: 48
- Total rows across all CSV files: 2,888,293
- Total on-disk CSV size: 336.76 MB

#### Suggested Databricks pipeline ideas
##### Bronze
   - Auto Loader over raw/usage, raw/billing, raw/support, raw/network, raw/cdc.
   - Keep file metadata and ingestion timestamps.
##### Silver
   - Deduplicate by natural keys.
   - Build SCD2 customer profile history from customer_contact_cdc_2025H1.csv.
   - Build subscription lifecycle history from subscription_status_events_2025H1.csv.
   - Standardize currencies, timestamps, and data-quality rules.
##### Gold
   - Monthly revenue by country / region / service family.
   - Tower reliability and outage impact scorecards.
   - Support SLA and CSAT dashboards.
   - Roaming and usage mix analysis.
   - Churn feature table joined to subscription_churn_target_2025-06-30.csv.

#### Folder map
- raw/master: static dimensions and latest snapshots.
- raw/cdc: change data capture style tables.
- raw/usage: partition-like monthly event drops for voice, data, and SMS.
- raw/billing: monthly invoices and payments.
- raw/support: monthly ticket extracts.
- raw/network: outage events and daily tower KPIs.
- raw/analytics: optional ML target table.
- schema: manifest, table dictionary, and join relationships.

#### Notes
- No real customer data is included.
- Keys are internally consistent across files.
- Files are plain CSV with headers and no compression so they are easy to ingest into Databricks, DBFS, or Unity Catalog volumes.
