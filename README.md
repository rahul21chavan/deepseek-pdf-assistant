# PDF Question-Answering Assistant

A Streamlit prototype for asking questions about an uploaded PDF. It extracts PDF text, splits it into overlapping chunks, indexes the chunks in an in-memory vector store, retrieves relevant passages, and uses a local Ollama model to generate a concise answer.

## Features

- Upload a single PDF through the Streamlit interface
- Extract PDF pages with PDFPlumber
- Split extracted text into 1,000-character chunks with 200-character overlap
- Create embeddings and store chunks in an in-memory vector store
- Retrieve relevant chunks with similarity search
- Generate answers with the local `deepseek-r1:14b` Ollama model

## Tech stack

- Python
- Streamlit
- LangChain
- PDFPlumber
- Ollama embeddings and LLM
- In-memory vector store

## Prerequisites

1. Python 3.10 or newer (recommended).
2. [Ollama](https://ollama.com/) installed and running.
3. Pull the model used by the application:

   ```bash
   ollama pull deepseek-r1:14b
   ```

## Run locally

1. Clone the repository:

   ```bash
   git clone https://github.com/rahul21chavan/deepseek-pdf-assistant.git
   cd deepseek-pdf-assistant
   ```

2. Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   ```

   macOS/Linux:

   ```bash
   source .venv/bin/activate
   ```

   Windows PowerShell:

   ```powershell
   .venv\\Scripts\\Activate.ps1
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Start the application:

   ```bash
   streamlit run app.py
   ```

## Current implementation notes

- The vector store is in memory, so indexed documents are not persisted between application restarts.
- The app processes the uploaded PDF during the upload interaction; it is a prototype rather than a production multi-user service.
- The current file-path construction in `app.py` should be corrected before relying on uploads: `pdfs_directory` is set to a filename-like string and then concatenated with the uploaded filename. Use a dedicated directory (for example, `./uploaded_pdfs/`) and path-joining utilities.
- Add file-size limits, error handling, per-session isolation, and cleanup of uploaded files before deploying with real users.

## Security and responsible use

Do not upload confidential or personally identifiable documents to an untrusted deployment. Review generated answers against the source PDF; retrieval-based responses can still be incomplete or incorrect.
