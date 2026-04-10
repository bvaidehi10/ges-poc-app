# GES Audio Processing POC

<div class="hero-card">
  <div class="hero-badge">Google Cloud • Streamlit • Analytics</div>
  <h1>GES Audio Processing POC</h1>
  <p>
    Technical documentation for a Streamlit-based application deployed on Google Cloud Run
    that processes audio files through transcription, masking, structured persistence, and analytics.
  </p>
</div>

## Purpose

This documentation describes the end-to-end workflow, code structure, cloud services, deployment model, and operational considerations for the GES Audio Processing POC repository.

The solution processes uploaded audio files using the following pipeline:

> **Streamlit UI → Google Cloud Storage → Speech-to-Text → DLP masking → BigQuery → Looker Studio**

## Audience

This documentation is intended for:

- Engineering managers
- Technical leads
- Developers onboarding to the project
- Cloud engineers supporting deployment
- Analysts consuming BigQuery and Looker Studio outputs

## Solution Summary

The application accepts an audio file, stores it in Cloud Storage, sends it for batch transcription, processes the transcript text, masks selected personally identifiable information, and persists the results into BigQuery for downstream reporting.

## Current Default Configuration

| Item | Value |
|---|---|
| Repository | `bvaidehi10/ges-poc-app` |
| Application entry point | `app.py` |
| Default project | `ges-poc-490514` |
| Default bucket | `ges-poc-capgemini-001` |
| Default dataset | `ges_demo` |
| Agent table | `call_transcripts_agent` |
| Analytics table | `call_transcripts_analytics` |
| Speech location | `global` |

## Documentation Map

| Section | Description |
|---|---|
| Overview | High-level solution description and business purpose |
| Architecture | Component-level design and runtime workflow |
| Codebase | Repository structure and module responsibilities |
| Infrastructure | GCP services, bucket/table layout, and IAM expectations |
| Deployment | Cloud Run deployment and GitHub Pages publishing |
| Authentication | Local and runtime authentication patterns |
| Troubleshooting | Common failure modes and resolutions |
| Diagrams | Mermaid-based architectural and delivery visuals |

## Notable Implementation Notes

!!! info "Important implementation note"
    The current codebase masks **phone numbers** and **email addresses** through DLP.  
    Customer name extraction exists in parser logic, but name masking is not currently implemented in the DLP request.

## Success Criteria of the POC

The solution is considered operationally successful when the following conditions are met:

- audio upload completes successfully
- transcript JSON is generated in Cloud Storage
- transcript text can be parsed
- masked transcript is created through DLP
- agent and analytics rows are inserted into BigQuery
- Looker Studio can query the analytics dataset without exposing raw PII