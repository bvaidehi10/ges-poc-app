# Diagrams

## Architecture
```mermaid
flowchart LR
A[Streamlit] --> B[GCS]
B --> C[Speech-to-Text]
C --> D[DLP]
D --> E[BigQuery]
E --> F[Looker Studio]