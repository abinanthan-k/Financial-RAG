# ADR 001: Initial System Design & Tech Stack

## Status
Proposed (2026-04-30)

## Context
The project requires a system capable of processing dense, table-heavy financial PDFs. It must be cost-effective, maintainable by a single developer/architect, and scalable to multi-agent workflows. Previous approaches using standalone scripts lacked persistence and reliability.

## Decisions

### 1. Component Orchestration via Docker Compose
*   **Decision:** Every core component (DB, LLM, UI, Worker) will run in separate containers.
*   **Rationale:** Ensures environment parity, prevents dependency conflicts, and allows for independent scaling of the "Brain" (Ollama) vs the "Memory" (Chroma).

### 2. Data Extraction via Table-to-Markdown (Docling)
*   **Decision:** Use layout-aware extraction instead of standard OCR or raw text splitting.
*   **Rationale:** Financial data's meaning is tied to its structure. Markdown is the most efficient format for LLMs to interpret tabular relations.

### 3. Airflow for Ingestion Pipelines
*   **Decision:** Move ingestion from manual scripts to an Airflow-managed DAG.
*   **Rationale:** Provides observability, automatic retries for failed extractions, and a professional way to handle "Batch" updates of financial filings.

### 4. Local-First Inference (Ollama)
*   **Decision:** Standardize on Ollama for local LLM and Embedding serving.
*   **Rationale:** Eliminates API costs during the development of complex agentic loops and ensures data privacy for sensitive financial documents.

### 5. Persistent Standalone Vector DB (ChromaDB)
*   **Decision:** Run ChromaDB as a dedicated service rather than an in-memory library.
*   **Rationale:** Decouples the data storage from the application lifecycle, allowing for database updates without restarting the entire system.
  
### 6. APIs to extract SEC filings(US) and Annual Reports(IND)
*  **Decision:** We will prioritize direct HTM-to-Markdown conversion for SEC filings.
*  **Rationale:** Minimizes data loss for US markets while maintaining compatibility
## Consequences
*   **Pros:** High control over data privacy; professional-grade observability; zero per-token costs for local testing.
*   **Cons:** Higher initial hardware requirements (RAM/GPU); steeper learning curve for Airflow orchestration.
