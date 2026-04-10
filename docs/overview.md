# Overview

## Executive Summary

The GES Audio Processing POC is a cloud-based processing pipeline that transforms uploaded audio recordings into structured transcript data for operational review and analytics consumption.

The application is implemented as a Streamlit front end and is designed to run on Google Cloud Run. Processing relies on managed Google Cloud services rather than locally hosted inference or custom infrastructure.

## Business Objective

The primary objective of the solution is to demonstrate a practical pipeline for:

- ingesting customer or service-call audio
- converting speech to text
- masking sensitive content for downstream use
- storing processed outputs in an analytics-ready format
- enabling dashboarding and review through BigQuery and Looker Studio

## End-to-End Workflow

### Step 1: User upload

A user uploads a supported audio file from the Streamlit interface.

Supported input formats currently include:

- `.wav`
- `.mp3`
- `.flac`

### Step 2: Raw storage

The uploaded file is stored in Google Cloud Storage under the configured raw audio prefix.

### Step 3: Batch transcription

A batch transcription request is submitted to Google Speech-to-Text v2 using the uploaded object URI.

### Step 4: Transcript retrieval

The transcription result is written by Speech-to-Text into Cloud Storage as structured JSON and then downloaded by the application.

### Step 5: Transcript parsing

The application extracts transcript text from the JSON response and derives structured values such as:

- probable customer name
- phone number
- email address

### Step 6: DLP masking

The transcript text is submitted to Cloud DLP for redaction of supported info types.

### Step 7: BigQuery persistence

Two records are written:

| Record Type | Purpose |
|---|---|
| Agent row | Operational review with raw transcript and extracted fields |
| Analytics row | Masked transcript for reporting and dashboarding |

### Step 8: Reporting

Looker Studio is used as a downstream reporting layer that can read from the analytics table in BigQuery.

## Functional Scope

### Included in current implementation

- audio upload
- Cloud Storage integration
- Speech-to-Text batch request
- operation polling
- transcript JSON retrieval
- transcript normalization
- regex-based field extraction
- DLP masking for selected data types
- BigQuery table creation support
- BigQuery inserts

### Not included in current implementation

- Terraform or IaC
- direct Looker Studio automation
- multi-language transcription configuration
- name masking in DLP
- advanced audit logging
- production observability dashboards

## Solution Characteristics

### Strengths

- straightforward service-oriented code structure
- practical use of managed GCP services
- clean separation between raw and masked analytics outputs
- suitable for demonstrations, POC validation, and incremental hardening

### Constraints

- Streamlit is appropriate for POC workflows, not high-scale transactional workloads
- parser extraction is heuristic and regex-driven
- privacy coverage is currently limited to configured DLP types
- deployment assets are partially external to the repository at present