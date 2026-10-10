# Contributing

## Workflow

1. Create a branch from `main`: `git checkout -b feature/short-name`.
2. Make a focused change. One purpose per branch.
3. Run the quality checks (below). All must pass.
4. Commit with a short, imperative message, for example `Fix model fallback note`.
5. Open a pull request describing what changed, why, and how you tested it.

## Quality checks

```bash
cd assistant-app/api && uv run ruff check . && uv run ruff format --check . && uv run pytest
cd assistant-app/agent && uv run pytest
cd assistant-app/web && npm run typecheck && npm run build
```

## Rules

### Security
- Never commit `.env`, `.env.local`, API keys, tokens or LiveKit secrets. Only `.env.example` is tracked.
- Treat all user input, uploaded files and model output as untrusted.
- Keep upload limits and type checks in place for photos and Library files.

### Backend (Python)
- Python 3.13, dependencies managed with `uv`. Commit `uv.lock` changes.
- Format and lint with ruff. No unformatted code.
- New behaviour needs a pytest test. Tests must run offline (use the fake providers and fixtures).
- Provider order is local Ollama first, then `CLOUD_PRIORITY`. Keep that behaviour.

### Frontend (TypeScript)
- Must pass `npm run typecheck` and `npm run build`.
- Use the existing shadcn/ui components and Tailwind classes; keep light and dark themes working.
- Read the Next.js docs in `node_modules/next/dist/docs/` before using APIs you are unsure of (see `assistant-app/web/AGENTS.md`).

### Configuration and docs
- Every new setting goes into the matching `.env.example` with a comment.
- Update the README command tables when you add or change a command.
- Keep the architecture diagram (`assistant-app/docs/architecture.svg`) in sync with structural changes.

### Commits and pull requests
- Short imperative subject line, under 72 characters.
- Do not commit logs, build output, `node_modules` or virtual environments (already git-ignored).
- Do not rewrite shared history on `main`.
