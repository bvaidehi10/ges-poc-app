## 4. Repository Structure

```
ges-poc-app/
├── app.py                          # Streamlit UI and pipeline orchestration
├── requirements.txt                # Python dependencies
├── PROJECT_WORKFLOW_DOCUMENTATION.md
└── services/
    ├── config.py                   # Project ID, bucket name, table names, constants
    ├── auth.py                     # Google access token helper (ADC / service account)
    ├── http_utils.py               # Retry-enabled HTTP session (urllib3 + requests)
    ├── gcs_service.py              # Cloud Storage: upload, list, download
    ├── speech_service.py           # Speech-to-Text: submit job, poll operation
    ├── dlp_service.py              # DLP: mask sensitive fields in transcript
    ├── bigquery_service.py         # BigQuery: ensure tables exist, insert rows
    └── parsers.py                  # Transcript parsing, email normalisation, entity extraction
```

**Design rationale:** The UI layer (`app.py`) is fully decoupled from cloud integrations. Each GCP service has a dedicated module. Retry/network logic is centralised in `http_utils.py`, making the codebase straightforward to explain, extend, and test independently.
