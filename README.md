# PowerBI-Ecommerce-GA4-Event_Analysis
Presents overall structure and steps in creating a power bi dashboard for event analysis, using publicly available dataset on BigQuery covering user engagement, session behavior and purchase conversion for an Ecommerce Platform.

**[View the interactive report →](#)** *(link once published)*

![Engagement Overview](images/engagement_overview.png)

## What this project demonstrates

- Extracting and flattening nested GA4 event data directly from BigQuery 
  using SQL, including array unnesting for event parameters and 
  ecommerce items
- Designing a star schema from raw event-level data with no native 
  session or user tables in the source
- Building surrogate keys for dimensions (device, traffic, geo) that 
  have no natural identifiers in the source data
- Writing DAX measures for session-level analysis, cohort behavior 
  (new vs. returning users), and multi-step funnel conversion
- Diagnosing and resolving real data modeling issues along the way, 
  documented in [methodology.md](docs/methodology.md)

## Data source

GA4 sample export, Google Merchandise Store (public BigQuery dataset)
`bigquery-public-data.ga4_obfuscated_sample_ecommerce` | Nov 2020 – Jan 2021

## Report pages

1. **User Engagement** — daily/weekly active users, session duration, 
   bounce and return patterns, engagement by weekday vs. weekend
2. **Revenue Analysis** — purchase funnel (session and item level), 
   revenue by category, revenue scatter by item price and quantity

## Repository structure

| Folder | Contents |
|---|---|
| `sql/` | BigQuery extraction queries, one per table, in build order |
| `sql/exploratory/` | Diagnostic queries that informed modeling decisions |
| `dax/` | Power BI measures, grouped by theme |
| `docs/` | Data model, data dictionary, and methodology notes |
| `images/` | Report screenshots and the model diagram |

## Tech stack

BigQuery (SQL) → Power Query (M) → Power BI (DAX)

## Data model

Star schema with two fact tables at different grains:

- **FACT_Event** — one row per event
- **Fact_Item** — one row per item per event (from GA4's repeated `items` array)

Supporting dimensions: **Sessions**, **Users**, **Device**, **Traffic**, 
**Geo**, **Date_Table**. Full breakdown in [data_model.md](docs/data_model.md).
