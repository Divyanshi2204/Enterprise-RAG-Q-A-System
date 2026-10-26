# Enterprise RAG Q&A System

An enterprise-grade Retrieval-Augmented Generation (RAG) question answering system built for Insurellm, a fictional insurance technology company. The project ingests internal knowledge sources such as company information, product summaries, employee profiles, and contract documentation, stores them in a vector database, and answers user questions using semantic retrieval plus an LLM.

This repository contains a complete RAG workflow with:

- document ingestion and chunking
- vector embedding and semantic retrieval
- LLM-powered answer generation
- a Gradio chat interface
- evaluation utilities for retrieval and answer quality

## Project Overview

The system is designed to act as an internal knowledge assistant for Insurellm. It indexes structured and unstructured data from the `knowledge-base` folder and answers questions such as:

- What products does Insurellm offer?
- Who are the employees and leadership profiles?
- What are the key features of Healthllm or Bizllm?
- What contracts or business context exist around specific products?
- How does the company structure its operations and business model?

The architecture combines a vector database (Chroma) with OpenAI embeddings and the GPT model stack to provide grounded answers based on retrieved context.

## Features

- Semantic search over product, employee, and company documentation
- Chunked document ingestion with overlap for better retrieval coverage
- OpenAI embedding support via `text-embedding-3-large`
- RAG-based answer generation with system prompt grounding
- UI-based interaction using Gradio
- Evaluation scripts measuring retrieval quality and answer quality

## Repository Structure

```text
Enterprise-RAG-Q-A-System/
├── week5/
│   ├── app.py                         # Gradio chat application
│   ├── evaluator.py                   # Evaluation helper entry point
│   ├── implementation/
│   │   ├── answer.py                 # RAG answer generation logic
│   │   └── ingest.py                 # Knowledge ingestion and embedding pipeline
│   ├── evaluation/
│   │   ├── eval.py                   # Retrieval and answer evaluation scripts
│   │   ├── test.py                   # Test definitions for evaluation
│   │   └── tests.jsonl               # Evaluation questions and references
│   ├── knowledge-base/
│   │   ├── company/
│   │   ├── contracts/
│   │   ├── employees/
│   │   └── products/
│   └── vector_db/                    # Persisted Chroma vector database (generated after ingestion)
```

## Tech Stack

- Python
- LangChain
- ChromaDB
- OpenAI embeddings and GPT models
- Gradio
- Pydantic
- LiteLLM
- Python-dotenv

## Data Sources

The knowledge base includes:

- company overview and strategic information
- product summaries for Carllm, Homellm, Lifellm, Healthllm, Bizllm, Markellm, Claimllm, and Rellm
- employee profile documents
- contract documents across different insurance verticals

These documents are loaded, split into chunks, embedded, and stored for retrieval.

## Setup

1. Clone the repository

```bash
git clone https://github.com/Divyanshi2204/Enterprise-RAG-Q-A-System.git
cd Enterprise-RAG-Q-A-System
```

2. Create and activate a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate   # Linux/macOS
# or
.venv\Scripts\activate      # Windows
```

3. Install dependencies

```bash
pip install --upgrade pip
pip install langchain langchain-openai langchain-chroma langchain-huggingface langchain-community langchain-text-splitters gradio python-dotenv litellm pydantic
```

4. Set your OpenAI API key

Create a `.env` file in the project root with:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

## Running the Project

### 1. Ingest the knowledge base

```bash
python week5/implementation/ingest.py
```

This loads documents from `week5/knowledge-base`, splits them into chunks, embeds them, and stores them in `week5/vector_db`.

### 2. Launch the web app

```bash
python week5/app.py
```

This starts a Gradio interface where users can ask questions about Insurellm and inspect the retrieved context.

### 3. Evaluate the system

```bash
python week5/evaluation/eval.py 0
```

The evaluation script runs a specific test row from `tests.jsonl` and prints retrieval metrics and answer quality scores.

## How the RAG Pipeline Works

1. Documents are loaded from the knowledge base
2. Each document is split into chunks using `RecursiveCharacterTextSplitter`
3. Chunks are embedded using OpenAI embeddings
4. Relevant chunks are retrieved using similarity search
5. The question and retrieved context are supplied to the LLM as system/user messages
6. The model answers using grounded context from the knowledge base

## Example Use Cases

- "What is the purpose of Healthllm?"
- "How many employees does Insurellm have?"
- "Which product handles claims processing?"
- "What are the key features of Claimllm?"
- "Which contracts are tied to the reinsurance business?"

## Notes

This project is an educational enterprise RAG example and uses a fictional company dataset modeling an insurance technology business. The retrieval and answer quality are designed to support internal Q&A workflows rather than a production-ready compliance system.

## License

This project does not currently specify a repository license. If you plan to distribute or reuse it publicly, add an appropriate open-source license file.

## Acknowledgements

This project demonstrates an end-to-end Retrieval-Augmented Generation workflow using modern LLM tooling, vector databases, and domain-specific knowledge ingestion.
