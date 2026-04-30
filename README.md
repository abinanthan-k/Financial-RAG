# Project Alpha-Agent: Financial Intelligence & Forensic Analysis

## 1. Overview
Alpha-Agent is a production-grade AI system designed for high-stakes financial analysis. The system specializes in ingesting complex financial documents (such as SEC 10-K and 10-Q filings), performing layout-aware data extraction, and providing a reasoning engine for forensic accounting and investment research.

## 2. Core Objectives
*   **High-Fidelity Retrieval:** Extract and index financial data with structural integrity, ensuring tables and financial statements are preserved.
*   **Forensic Reasoning:** Identify "red flags," revenue recognition patterns, and sentiment shifts in management discussion.
*   **Local-First & Open-Source:** Ensure data privacy and cost-efficiency by utilizing local LLMs and open-source orchestration.
*   **Architectural Scalability:** Transition from a robust RAG foundation to a Multi-Agent system capable of autonomous research.

## 3. High-Level Architecture
The system is built as a microservice-oriented platform using Docker Compose:
*   **Ingestion Engine:** Orchestrated by **Apache Airflow**, utilizing **Docling** for Table-to-Markdown conversion.
*   **Vector Memory:** **ChromaDB** running in client-server mode for persistent semantic storage.
*   **Inference Engine:** **Ollama** serving local models (Llama 3 / Mistral / Nomic-Embed).
*   **Serving Layer:** **FastAPI** providing an asynchronous interface for the end-user or downstream agents.



## 4. Key Features
*   **Layout-Aware RAG:** Preserves document hierarchy and tabular data.
*   **Metadata Filtering:** Enhances retrieval precision by tagging data with Ticker, Year, and Document Section.
*   **Agentic Roadmap:** Future integration of LangGraph for Supervisor-Worker orchestration.
