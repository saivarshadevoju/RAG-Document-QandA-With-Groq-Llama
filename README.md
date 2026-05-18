# RAG Document Q&A with Groq and Llama

A simple Streamlit app that uses Retrieval-Augmented Generation (RAG) to answer questions from your PDF research papers.

It combines:
- OpenAI embeddings for vectorization
- FAISS for vector search
- Groq-hosted Llama model for grounded answers

## Features

- Loads PDF documents from the `research_papers/` directory
- Splits documents into chunks for retrieval
- Builds a FAISS vector index from document embeddings
- Retrieves relevant chunks and answers with Groq Llama
- Displays retrieved context in the Streamlit UI

## Tech Stack

- Streamlit
- LangChain (`0.1.x` compatible setup)
- `langchain-groq`
- `langchain-openai`
- `langchain-community`
- `faiss-cpu`
- `python-dotenv`

## Project Structure

```text
RAG_Document/
├── app.py
├── requirements.txt
├── .env
└── research_papers/
```

## Setup

1. Clone the repository and enter the project directory.

```bash
git clone https://github.com/yourusername/your-repo-name.git
cd your-repo-name
```

2. Create/activate your Python environment (recommended).

```bash
conda create -n rag-doc python=3.11 -y
conda activate rag-doc
```

3. Install dependencies.

```bash
pip install -r requirements.txt
```

4. Create a `.env` file in the project root.

```env
OPENAI_API_KEY=your_openai_api_key
GROQ_API_KEY=your_groq_api_key
```

5. Add PDFs to `research_papers/`.

## Run

```bash
streamlit run app.py
```

## How to Use

1. Click **Document Embedding** to load PDFs and build the FAISS index.
2. Enter your question in the text box.
3. View the generated answer and the retrieved document chunks.

## Current App Behavior Notes

- The app currently loads only the first 50 documents/chunks source subset (`docs[:50]`) for faster indexing.
- Chunking is configured as:
  - `chunk_size=1000`
  - `chunk_overlap=200`

## Troubleshooting

- **`ModuleNotFoundError: langchain.chains`**
  - This is usually a version mismatch. Current `requirements.txt` pins a compatible LangChain stack.

- **`ImportError: Could not import faiss`**
  - Install `faiss-cpu` (already included in `requirements.txt`).

- **Running in wrong environment**
  - Ensure your shell is using the same env where dependencies were installed:

```bash
which python
pip list | grep -E "langchain|faiss|streamlit"
```
