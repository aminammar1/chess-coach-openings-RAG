# Chess Coach Openings RAG

A Jupyter notebook project for a chess opening coach powered by retrieval augmented generation.

The notebook searches and loads chess opening data, builds local retrieval indexes, retrieves relevant opening records, and asks ai models to answer with plain-text coaching advice. The UI includes a session-only chatbot, so chat history stays only in the active notebook kernel and disappears when the session is cleared or restarted.

## Main File

- `chess_coach_openings_rag.ipynb`: full notebook pipeline, from dataset loading to retrieval, answer generation, and chatbot UI.

## What It Does

- Loads chess opening records, preferring `Lichess/chess-openings`.
- Builds local TF-IDF vector search, BM25 search, and chess keyword search.
- Merges results with reciprocal rank fusion.
- Generates plain-text coaching answers with concrete move orders, ECO codes, plans, risks, and beginner recommendations.
- Shows retrieved sources in a styled table.
- Provides a chess-themed notebook chatbot.

## Setup

Create a `.env` file based on `.env.example` with:

```bash
HF_API_KEY=your_huggingface_key
OPENROUTER_API_KEY=your_openrouter_key
```

Use the local environment and run the notebook cells in order:

```bash
source .venv/bin/activate
python -m json.tool chess_coach_openings_rag.ipynb
```

Generated retrieval artifacts are cached in `.rag_cache/`.
