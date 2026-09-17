# Ragger

A small Retrieval-Augmented Generation (RAG) project: chunk documents into a
Chroma vector store, retrieve relevant context for a question, and generate
an answer with a pluggable LLM provider (Anthropic, OpenAI, Google, or
Ollama).

## Setup

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
pip install -e .
copy .env.example .env
```

Fill in `.env` with the API key for whichever provider you set as
`LLM_PROVIDER`.

## Usage

Ingest documents (markdown files) into the vector store:

```bash
python -m ragger.ingest path/to/docs
```

Launch the chat UI:

```bash
python -m ragger.app
```

## Layout

- `src/ragger/` — library code: config, ingestion, vector store, LLM
  providers, RAG pipeline, Gradio app.
- `notebooks/` — exploration notebooks.
- `database/` — local Chroma persistence directory (gitignored).

## Using this as a template

This repo is meant to be forked for each new RAG project. When you fork it:

1. Set `CHROMA_COLLECTION_NAME` in `.env` to something project-specific (avoids
   collisions if you ever point two forks at the same Chroma directory).
2. Update the `name` and `description` in `pyproject.toml`.
3. Update this README's title/description.
4. Drop your own documents somewhere and point `ragger.ingest` at them —
   `database/` starts empty per fork.
5. Rename the `ragger` package (`src/ragger/` and the `ragger.*` imports) if
   the new project deserves its own name rather than staying "ragger".
