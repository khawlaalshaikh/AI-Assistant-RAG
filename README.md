# AI Assistant — Retrieval-Augmented Generation (RAG)

An interactive AI assistant that allows users to upload documents and ask questions about their content using **Retrieval-Augmented Generation (RAG)**. The system combines semantic embeddings, vector search, and Large Language Models (LLMs) to retrieve relevant information and generate context-aware responses.

## Overview

This project implements an end-to-end RAG pipeline that connects user-provided documents with an LLM. Instead of relying only on the knowledge stored in the language model, the assistant first retrieves relevant information from the uploaded documents and then uses that context to generate the response.

The application is designed to work with **multiple document/file formats** and provides an interactive **Streamlit** interface for document upload and conversational question answering.

## Architecture

The system follows the following workflow:

```text
User Uploads Documents
        ↓
Document Processing
        ↓
Text Extraction & Chunking
        ↓
BGE Semantic Embeddings
        ↓
FAISS Vector Database
        ↓
User Query
        ↓
Query Embedding
        ↓
Similarity Search
        ↓
Relevant Context Retrieval
        ↓
LLM via OpenRouter
        ↓
Generated Answer
        ↓
Streamlit Interface
```

## Key Components

### 1. Document Processing

Uploaded documents are processed and divided into smaller text chunks. Chunking allows the system to retrieve focused and relevant sections instead of passing an entire document to the language model.

The project uses a recursive text-splitting strategy with:

* **Chunk size:** 800
* **Chunk overlap:** 200

### 2. Semantic Embeddings

Each document chunk is converted into a numerical vector using:

**BAAI/bge-small-en-v1.5**

These embeddings represent the semantic meaning of the text and allow the system to search for information based on meaning rather than exact keyword matching.

### 3. Vector Search

The generated embeddings are stored in a **FAISS** vector index.

FAISS enables efficient similarity search between:

* the user's question
* the document embeddings

The most relevant document chunks are retrieved and provided as context to the LLM.

### 4. Retrieval-Augmented Generation

The retrieved context is combined with the user's question and passed to an LLM.

This allows the assistant to generate answers grounded in the content of the uploaded documents rather than relying exclusively on the model's pretrained knowledge.

### 5. LLM Integration

The project uses **OpenRouter** to connect the RAG pipeline with an LLM.

The assistant maintains conversational history, allowing users to ask follow-up questions within the same conversation.

### 6. Streamlit Application

The complete pipeline is integrated into a **Streamlit** web application.

The interface allows users to:

* Upload documents
* Ask questions using natural language
* Maintain conversational context
* Receive AI-generated answers based on retrieved document content

## Evaluation

The retrieval component was evaluated using semantic similarity between retrieved information and the expected relevant content.

**Average Semantic Similarity: 0.796**

This indicates a strong level of semantic alignment between the retrieved information and the evaluated reference content.

## Technologies

* **Python**
* **Streamlit**
* **LangChain**
* **FAISS**
* **Sentence Transformers**
* **BAAI/bge-small-en-v1.5**
* **OpenRouter**
* **Large Language Models (LLMs)**

## Project Structure

```text
AI-Assistant-RAG/
│
├── app/
│   └── ...
│
├── data/
│   └── ...
│
├── notebooks/
│   └── ...
│
├── requirements.txt
├── README.md
└── ...
```

> The exact structure may vary depending on the final organization of the project files.

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/AI-Assistant-RAG.git
cd AI-Assistant-RAG
```

Create a virtual environment:

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

## Environment Variables

Create a `.env` file and add your OpenRouter API key:

```env
OPENROUTER_API_KEY=your_api_key_here
```

Do not commit your API key or `.env` file to GitHub.

Add the following to `.gitignore`:

```text
.env
venv/
__pycache__/
```

## Running the Application

Start the Streamlit application with:

```bash
streamlit run app.py
```

The application will open in your browser and provide the interface for uploading documents and interacting with the AI assistant.

## Future Improvements

* Support for additional document and multimedia formats
* Improved retrieval and document ranking
* Hybrid keyword + semantic retrieval
* Reranking of retrieved chunks
* Conversation-aware retrieval
* Source citations for generated answers
* Evaluation using additional RAG-specific metrics

## Author

**Khawla Al-Shaikh**

AI & Machine Learning | Deep Learning | NLP | LLMs | RAG
