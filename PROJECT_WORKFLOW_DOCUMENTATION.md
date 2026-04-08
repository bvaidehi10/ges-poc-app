# Technical Workflow Documentation

## 1) Architecture Overview
This project follows a modular layered design to separate concerns and enhance maintainability. Each layer interacts with adjacent layers while encapsulating its functionalities.

## 2) Workflow Steps
The audio processing workflow consists of the following 12 steps:
1. Audio upload
2. Audio processing
3. Transcription
4. Data parsing
5. DLP (Data Loss Prevention) checks
6. BigQuery insertion
7. Error handling
8. Logging
9. Notifications
10. Data validation
11. Report generation
12. Archival

## 3) Service Module Descriptions
- **Config:** Handles configuration settings and environment variables.
- **Auth:** Manages user authentication using Google Cloud services.
- **HTTP Utils:** A set of utility functions for handling HTTP requests and responses.
- **GCS Service:** Interacts with Google Cloud Storage for file uploads and retrievals.
- **Speech Service:** Processes audio files for transcription.
- **DLP Service:** Implements data loss prevention checks to protect sensitive information.
- **BigQuery Service:** Manages data insertion and querying in BigQuery.
- **Parsers:** Responsible for interpreting and structuring the data post-transcription.

## 4) Authentication Flow
We utilize Google Application Default Credentials for seamless authentication to Google Cloud services.

## 5) Network Resilience and Retry Strategy
Adopts an exponential backoff strategy for handling network failures to ensure resilience.

## 6) Configuration and Environment Variables Reference
| Variable Name            | Description                          |
|-------------------------|--------------------------------------|
| PROJECT_ID              | Google Cloud project ID              |
| GCS_BUCKET              | Google Cloud Storage bucket name     |
| GOOGLE_APPLICATION_CREDENTIALS | Path to the service account key |

## 7) Data Flow Diagrams and Process Flows
[Insert diagrams here]  
*Include visual representations of the data flow and processes.*

## 8) Dependencies and Setup Instructions
- Ensure the following libraries are installed:
  - google-cloud-storage
  - google-cloud-bigquery
  - google-auth

To set up:
1. Clone the repository.
2. Install dependencies using `pip install -r requirements.txt`.
3. Configure the environment variables as described above.

## 9) Error Handling and Debugging Approaches
Implement logging at various stages to capture errors and facilitate debugging. Use structured error messages to identify issues promptly.

## 10) Running Instructions
To run the application, use the following command:
```bash
python main.py
```

## 11) BigQuery Table Schemas
- **Audio Data Schema:**  
  - `audio_id`: STRING  
  - `user_id`: STRING  
  - `transcription`: STRING  

## 12) Design Decisions and Key Rationale
- Chose a microservices architecture for scalability and maintenance.
- Adopted cloud services for managing infrastructure and reducing overhead.

## 13) Troubleshooting Guide
- Check application logs for error messages.  
- Verify environment variable configurations.

## 14) Looker Studio Integration Instructions
- Connect Looker Studio to the BigQuery dataset used for reporting.
- Use the provided dashboard templates for visualization.

## 15) Future Enhancement Suggestions
- Explore adding support for additional audio formats.
- Consider implementing a user-friendly frontend for managing audio uploads and analyses.

---

This document is a living document and will be regularly updated as the project evolves.