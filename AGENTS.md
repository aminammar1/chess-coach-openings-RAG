# Repository Guidelines

## Project Structure & Module Organization

This repository is currently organized around one root-level notebook:

- `chess_coach_openings_rag.ipynb`: main RAG notebook for the chess openings coach.
- `.env.example`: required API key names and placeholder values.
- `.env`: local secrets file; keep it private and never commit real keys.
- `.venv/`: local Python virtual environment and Jupyter kernel files.
- `.rag_cache/`: generated at runtime for cached embeddings and retrieval artifacts.

If the project grows, place reusable Python code in `src/`, tests in `tests/`, and notebook-only experiments in clearly named `*.ipynb` files at the root or a dedicated `notebooks/` folder after team agreement.

## Build, Test, and Development Commands

Use the local virtual environment:

```bash
source .venv/bin/activate
```

Install or refresh notebook dependencies:

```bash
python -m pip install datasets huggingface_hub pandas numpy scikit-learn rank-bm25 voyageai python-dotenv requests ipywidgets tqdm joblib
```

Register the Jupyter kernel locally:

```bash
python -m ipykernel install --prefix .venv --name chess-coach-openings-rag --display-name "Chess Coach Openings RAG"
```

Validate notebook JSON:

```bash
python -m json.tool chess_coach_openings_rag.ipynb
```

## Coding Style & Naming Conventions

Use Python 3.14+ syntax where helpful, but keep notebook cells readable and linear. Prefer small functions with explicit names such as `retrieve`, `embed_query`, and `call_openrouter_chat`. Use `snake_case` for variables/functions, `UPPER_SNAKE_CASE` for configuration constants, and Markdown headings to separate notebook stages. Avoid printing API keys or full request headers.

## Testing Guidelines

There is no formal test suite yet. Before changes, run the notebook JSON validation command and at least import-check dependencies:

```bash
python -c "import datasets, pandas, numpy, sklearn, rank_bm25, voyageai"
```

For new reusable modules, add `pytest` tests under `tests/` using names like `test_retrieval.py` and `test_<behavior>()`.

## Commit & Pull Request Guidelines

No usable Git history is present in this workspace, so follow conventional, imperative commit messages: `Add RAG notebook`, `Fix OpenRouter free model filtering`, or `Document setup commands`.

Pull requests should include a short summary, changed files, setup or migration notes, and validation performed. For notebook UI changes, include screenshots or a short description of the interaction tested.

## Security & Configuration Tips

Keep provider secrets only in `.env`. Use `.env.example` for variable names: `HF_API_KEY`, `OPENROUTER_API_KEY`, and `VOYAGE_API_KEY`. Do not commit `.rag_cache/` if it contains generated embeddings from private or paid data.
