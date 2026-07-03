# A Layout-Aware, Multimodal Retrieval-Augmented Generation System for Technical Manuals

This project is a hybrid retrieval-augmented generation (RAG) system for querying equipment manuals in PDF form. It combines dense vector search using Qdrant, lexical BM25 retrieval, and Cohere reranking to answer natural-language questions grounded in manual content — including text, embedded images, and tabular specifications (torque values, part numbers, error codes) extracted and stored separately for precise lookup. Built with FastAPI and LlamaIndex, it supports incremental document ingestion, cached parsing, and environment-specific LLM backends (Groq for dev, self-hosted vLLM for production).

## Project Structure

```
root/
├── config/                  # System-level parameters
│   ├── llm.yaml             # LLM settings (temperature, models, tokens)
│   └── retriever.yaml       # Retrieval settings (top-k, similarity thresholds)
├── data/                    # Knowledge base and assets
│   ├── raw/                 # Original source documents (PDFs, docs, raw text)
│   ├── processed/           # Cleaned and chunked docs ready for embedding
│   └── vectordb/            # Persisted vector indexes or databases
├── app/                     # Core RAG logic and endpoints
│   ├── __init__.py
│   ├── main.py              # FastAPI or primary orchestration entry point
│   ├── ingest.py            # Document processing pipeline (loading and chunking)
│   ├── retriever.py         # Vector similarity search and reranking
│   ├── generator.py         # Prompt formatting and LLM integration
│   └── utils.py             # Helper functions
```

## Getting Started

1. Install uv
```
pip install uv
```

2. Copy .env.example to .env file and add API Keys
```
sp .env.example .env
```

3. Run local Qdrant server
```
docker compose up qdrant -d
```

4. Install dependencies
```
cd ./src
uv sync
```

5. Run app.py
```
uv run uvicorn app.main:app --reload
```

6. Run frontend
```
cd ./ui
npm i
npm run dev
```
