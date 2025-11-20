# GenAI Analytical SQL Engine (Gemini & PostgreSQL)

This project demonstrates a GenAI-powered SQL engine using Gemini LLM (2.5 Flash model) to automate analytical queries and reporting, reducing report generation time via natural language prompts.


##  Key Features and Architecture

* **Natural Language to SQL:** Gemini generates production-ready, multi-table PostgreSQL queries from simple English prompts.
* **Multi-Table Reasoning:** The LLM handles complex JOINs and aggregations across the 4-table college inventory schema.
* **Automated Reporting:** Raw SQL results are fed back to Gemini to generate a concise, human-readable analytical report, eliminating manual data interpretation.
* **Secure Infrastructure:** PostgreSQL database with secure environment variable handling (using `.env`).

## Demonstration

**Example Prompt:** Show all assets in the 'Architecture' department that are currently marked 'Maintenance'. Include the asset name and the room location.

**Resulting Analytical Report**

![Gemini Generated Analytical Report Summary](https://private-user-images.githubusercontent.com/51848469/510343835-9d5051b9-a9f7-46c4-8e9e-276de110b606.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjM2NjY1NTUsIm5iZiI6MTc2MzY2NjI1NSwicGF0aCI6Ii81MTg0ODQ2OS81MTAzNDM4MzUtOWQ1MDUxYjktYTlmNy00NmM0LThlOWUtMjc2ZGUxMTBiNjA2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTExMjAlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMTIwVDE5MTczNVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWM3MmY4MzViYmUwNWNlMmZiZDFhMzI4Yzk3MmUxN2M4NTc0M2E1NGZmYWFkNzdlZDdiNzU2YjM0OGNlNzZmZGQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.Q00aOGZAFZEcv1IHjaU-BdpWWFWwqq7JY6gYx6_KZMI)

**Generated PostgreSQL Query**

```sql
SELECT
  a.asset_name,
  di.room_location
FROM assets AS a
JOIN dept_inventory AS di
  ON a.asset_id = di.asset_id
JOIN departments AS d
  ON di.dept_id = d.dept_id
WHERE
  d.dept_name = 'Architecture' AND di.status = 'Maintenance'
