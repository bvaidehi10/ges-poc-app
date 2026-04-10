# Overview

## Summary
This application processes audio files into structured and masked data for analytics.

## Flow
1. Upload audio
2. Store in GCS
3. Transcribe using Speech-to-Text
4. Mask PII via DLP
5. Store in BigQuery
6. Visualize via Looker Studio

## Outputs

| Type | Table |
|------|------|
| Raw | call_transcripts_agent |
| Masked | call_transcripts_analytics |
