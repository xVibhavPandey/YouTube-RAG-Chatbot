# YouTube Video RAG Chatbot (Learning Project)

A lightweight Retrieval-Augmented Generation (RAG) prototype built strictly for **educational and learning purposes** using Jupyter Notebooks (`.ipynb`). **No UI or web application framework** (like Streamlit or Gradio) has been implemented; all interactions occur directly within the notebook cell outputs.

---

## 🛠️ Tech Stack & Libraries Used
- **Environment:** Jupyter Notebook (`making.ipynb`)
- **API & LLM Client:** `langchain-huggingface`, `huggingface_hub` (TinyLlama model via LangChain integration)
- **Data Ingestion:** `youtube-transcript-api`
- **Text Processing & Chunking:** `langchain-text-splitters` (`RecursiveCharacterTextSplitter`)
- **Embeddings & Vector Store:** `sentence-transformers` (`all-MiniLM-L6-v2`), `faiss-cpu`

---

## 🔄 RAG Workflow Diagram

```text
[ YouTube Video URL ]
         │
         ▼
[ youtube-transcript-api ] ──► Extracts Full Video Transcript (Raw Text)
                                       │
                                       ▼
                       [ RecursiveCharacterTextSplitter ]
                                       │
                                       ▼
                       [ FAISS Vector Store + Embeddings ]
                               (all-MiniLM-L6-v2)
                                       │
                                       ▼
                     [ User Question / Prompt Query ]
                                       │
                                       ▼
                     [ Vector Similarity Search (k=4) ] ──► Retrieves Context Chunks
                                       │
                                       ▼
                     [ LangChain PromptTemplate Constructor ]
                                       │
                                       ▼
                 [ HuggingFaceEndpoint / ChatHuggingFace LLM ]
                        (TinyLlama-1.1B-Chat-v1.0)
                                       │
                                       ▼
                   [ Jupyter Notebook Cell Output Display ]
```

---

## 🚀 Step-by-Step Execution Flow

```text
[1. Setup Environment]
   ├── Set HF_TOKEN environment variable
   └── Install dependencies via pip

[2. Data Extraction]
   └── Fetch transcript using YouTube Video ID (e.g., "Gfr50f6ZBvo")

[3. Text Splitting]
   └── Break raw text into manageable chunks (chunk_size=1000, overlap=200)

[4. Vectorization]
   ├── Generate local embeddings using HuggingFaceEmbeddings
   └── Index and store chunks inside FAISS vector store

[5. Retrieval & Generation]
   ├── Query the vector store to fetch relevant context documents
   ├── Format final prompt template with context + question
   └── Invoke model and print output in notebook cell
