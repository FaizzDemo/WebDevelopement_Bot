# Web Development Tutor AI (RAG)

A beginner-friendly Streamlit chatbot that retrieves relevant passages from the supplied Markdown web-development knowledge base and uses OpenRouter to generate grounded answers. The app displays source filenames and retrieved excerpts for transparency.

## Features
- Loads every `.md` file in `knowledge_base/` automatically.
- Retrieval-augmented generation (RAG) with embeddings and cosine similarity.
- Shows source excerpts used for each answer.
- Supports English and Roman Urdu responses.
- Covers HTML, CSS, JavaScript, responsive design, accessibility, frontend development, backend development, web APIs, and Bootstrap.
- Keeps API credentials in a local `.env` file (excluded from Git).

## Requirements
- Python 3.10 or newer
- An OpenRouter API key
- An OpenRouter chat model and an embeddings-compatible model enabled for your account

## Windows setup (PowerShell)

1. Extract the ZIP and open the `cybersecurity_rag_chatbot` folder in VS Code (the existing folder name is preserved).
2. Open **Terminal → New Terminal**.
3. Create and activate a virtual environment:

   ```powershell
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

   If PowerShell blocks activation, for this terminal session only run:

   ```powershell
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
   .\.venv\Scripts\Activate.ps1
   ```

4. Install packages:

   ```powershell
   python -m pip install -r requirements.txt
   ```

5. Create your local `.env` file from the example:

   ```powershell
   Copy-Item .env.example .env
   ```

6. Open `.env` and add your own OpenRouter API key. Keep the key private and do not upload `.env` to GitHub.
7. Start the chatbot:

   ```powershell
   streamlit run app.py
   ```

8. Open the local URL Streamlit prints, usually `http://localhost:8501`.

## Knowledge files

The `knowledge_base/` folder contains the seven web-development Markdown files provided for this project. The app automatically loads all `.md` files in this folder and builds embeddings on startup. If you replace or update knowledge files, stop Streamlit with `Ctrl+C` and restart it. Embedding creation uses your configured API and may incur API usage costs.

## Troubleshooting
- **Missing API key:** confirm `.env` exists next to `app.py` and the key is valid.
- **Embedding model error:** use an embeddings-compatible model available to your OpenRouter account, such as `openai/text-embedding-3-small` if available.
- **Knowledge file not loaded:** ensure the `.md` file is directly inside `knowledge_base/`.
- **API errors/costs:** embeddings are created at startup and question embeddings are requested during retrieval. Check your OpenRouter usage and model access.

## Accuracy note
The Markdown knowledge base is the primary source for grounded answers. The model can still make mistakes, so test code in a safe development environment and verify important implementation details.
