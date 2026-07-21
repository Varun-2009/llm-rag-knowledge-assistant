# LLM & RAG-Based Knowledge Assistant (POC)

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI_API-412991?style=flat&logo=openai&logoColor=white)
![Vector Search](https://img.shields.io/badge/Vector_Search-7F77DD?style=flat)

A proof-of-concept AI assistant that answers domain-specific questions from structured and unstructured documents using retrieval-augmented generation (RAG). Built to explore how LLMs can be grounded in real, private data rather than relying solely on pretrained knowledge.

---

## Overview

Large language models are powerful but don't know your private documents and can hallucinate facts. This project retrieves the most relevant chunks of source material for a given question, then passes them to an LLM as context — so answers are grounded in real documents rather than the model's memory alone.

---

## Architecture

1. **Document ingestion** — source documents (PDFs, text) are loaded and split into overlapping chunks
2. **Embedding** — each chunk is converted into a vector using an embedding model
3. **Vector store** — embeddings are indexed for fast similarity search
4. **Query time** — the user's question is embedded and matched against the store to retrieve the top-k relevant chunks
5. **Prompt assembly** — retrieved context + the original query are combined into a single prompt
6. **Generation** — the LLM produces a grounded, context-aware answer

*(See the architecture diagram shared above.)*

---

## Tech Stack

- **Language:** Python
- **Orchestration:** LangChain-style workflows
- **Embeddings / Vector Search:** Vector similarity search over document chunks
- **LLM:** OpenAI API (or Hugging Face model, depending on config)
- **Evaluation:** Manual relevance scoring of retrieved chunks and responses

---

## Setup & Installation

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/llm-rag-knowledge-assistant.git
cd llm-rag-knowledge-assistant

# 2. Create a virtual environment
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Configure environment variables
cp .env.example .env
# then fill in your API keys in .env

# 5. Run the assistant
python main.py
```

---

## Environment Variables

See `.env.example` — never commit real API keys or secrets.

```
OPENAI_API_KEY=your-api-key-here
VECTOR_DB_PATH=./data/vector_store
CHUNK_SIZE=500
CHUNK_OVERLAP=50
```

---

## Sample Data

The `/sample_data` folder contains a few small, non-sensitive example documents used to demonstrate ingestion and retrieval. Swap in your own documents by placing them in `/data` and re-running the ingestion script.

---

## Results / Learnings

- Chunk size and overlap significantly affect retrieval relevance — smaller chunks improved precision but sometimes lost context
- Prompt structure (how retrieved context is framed) had a noticeable effect on answer quality
- Documented the full architecture and evaluation approach to support future productionization

---

## Screenshots / Demo

*(Add screenshots or a short GIF here showing a sample query and the assistant's response)*

---

## Author

**Varun Kumar Kandukuri**
[LinkedIn](https://www.linkedin.com/in/varun-kumar-kandukuri-3785932b9/) · [Email](mailto:kvarunkandukuri9@gmail.com)# llm-rag-knowledge-assistant
POC AI assistant using retrieval-augmented generation (RAG) to answer questions from documents
