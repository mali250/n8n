
---

# README.md

## Build an AI-Powered Tech Radar Advisor — Overview

This repository documents an n8n workflow that:

* Imports a ThoughtWorks Tech Radar Google Sheet.
* Transforms the sheet rows into rag-friendly paragraph documents and stores them in a Google Doc.
* Generates vector embeddings (Google Gemini) and stores them in Pinecone for RAG.
* Synchronizes structured data into a MySQL `techradar` table for SQL-based queries.
* Exposes a `/radar-rag` webhook that routes user queries to a SQL Agent or a RAG Agent using an LLM router, with an Output Guardrail to validate responses.

---

## Quickstart (what you need)

1. An n8n instance (self-hosted, cloud, or n8n cloud).
2. Google credentials:

   * Google Sheets & Drive OAuth2 or Service Account (for Docs updates).
   * Google Gemini API key for embeddings.
3. Pinecone account & API key (or another vector store supported by LangChain).
4. MySQL database credentials (create a `techradar` table as described below).
5. LLM provider API keys for router and guardrail (Groq, Anthropic, OpenAI, Gemini, etc.).

### Recommended table schema (MySQL)

```sql
CREATE TABLE techradar (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255),
  ring VARCHAR(64),
  quadrant VARCHAR(128),
  isStrategicDirection TINYINT(1),
  isUsedByChildCompany1 TINYINT(1),
  isUsedByChildCompany2 TINYINT(1),
  isUsedByChildCompany3 TINYINT(1),
  isNew TINYINT(1),
  status VARCHAR(64),
  description TEXT,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## n8n workflow important nodes

* **Google Sheets**: Reads the Tech Radar sheet rows.
* **Code (transform)**: Formats rows into paragraph blocks (one per technology) to be inserted into a Google Doc.
* **Google Docs**: Stores transformed rag-friendly text (drives RAG ingestion).
* **Google Drive Trigger**: Watches the doc and triggers ingestion pipeline on update.
* **LangChain Doc Loader & Text Splitter**: Prepares the doc for embedding.
* **Embeddings (Google Gemini)** -> **Pinecone**: Inserts vectors.
* **MySQL nodes**: Delete & re-insert fresh rows on schedule.
* **Webhook (/radar-rag)**: Entrypoint for chat queries.
* **LLM router**: Classifies queries into SQL vs RAG.
* **Execute Workflow**: Runs the SQL or RAG sub-workflow.
* **Output Guardrail agent**: Validates/refines final response.

---

## Environment variables / credentials

Set these securely in your n8n credentials or environment:

* `GOOGLE_SHEETS_CREDENTIALS`
* `GOOGLE_DRIVE_CREDENTIALS`
* `GOOGLE_SERVICE_ACCOUNT_DOCS`
* `GOOGLE_GEMINI_API_KEY`
* `PINECONE_API_KEY`
* `MYSQL_HOST`, `MYSQL_USER`, `MYSQL_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_PORT`
* `GROQ_API_KEY` (or other LLM provider API keys)

---

## Testing & validation

1. Update the Google Sheet manually and confirm the Google Doc is updated by the Code node output.
2. Trigger the Google Drive trigger (or wait) to run the ingestion pipeline; check Pinecone index for new vectors.
3. Trigger the Cron node (or run manually) to refresh MySQL table and confirm records present.
4. POST to `/radar-rag` with `{ "chatInput": "How many items are in Adopt ring?" }` and verify:

   * Router classifies request (SQL vs RAG)
   * Appropriate sub-workflow runs
   * Output guardrail returns a concise, accurate answer

---

## Security & best-practices

* Do not commit API keys to source control. Use n8n credentials or environment variables.
* Limit webhook origins or add authentication if exposing public endpoint.
* Add rate-limiting and request validation to prevent injection or abuse.
* Monitor vector store and DB costs and set appropriate quotas.

---

## Extending the project

* Add more structured columns (owner, maturity score, last_reviewed).
* Support multi-tenant: scope MySQL queries by `organization_id` and create per-tenant vector namespaces.
* Swap Pinecone for another vector DB (e.g., Weaviate) — update LangChain vector store node accordingly.
* Add analytics dashboard (Streamlit/React) for tech radar visualizations and trends.

---
