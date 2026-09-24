<<<<<<< HEAD
# OpenChat
-Frontend: Next.js in frontend/(port 3000)
- Backend: FastApi in backend/ (port 8000)
- AI: Ollama at local host:11434
- Run everything: ./start.sh
- Test: cd backend && pytest



# Rules
- I am a beginner: Explain changes simply
- Never commit .env or API keys
- Run the tests after every change
=======
# OpenChat — Agent Coding Standards

## Stack

* **Frontend:** Next.js 16, React 19, TypeScript 7, Tailwind CSS 4, shadcn/ui
* **Backend:** FastAPI, Python 3.13, uv, Ruff, pytest
* **Local AI:** Ollama (`localhost:11434`), `gemma3:1b`
* **Cloud AI fallback:** OpenAI, Anthropic, Grok, or Gemini
* **Structure:** `frontend/` + `backend/`

## Architecture

* Keep frontend and backend concerns separate.
* Frontend communicates with the backend through documented HTTP APIs.
* Keep AI-provider logic inside the backend; never expose provider API keys to the frontend.
* Use a provider abstraction so local Ollama and cloud providers can be switched/fallback without changing application logic.
* Prefer local Ollama first; use configured cloud providers as fallback when local inference is unavailable or fails.
* Keep configuration and secrets in environment variables.

## Frontend

```bash
cd frontend
npm install
npm run dev
```

* Use TypeScript; avoid `any` unless unavoidable.
* Use reusable React components.
* Use shadcn/ui for UI primitives and Tailwind for styling.
* Keep API calls isolated from presentation components.
* Handle loading, error, empty, and streaming states.
* Follow Next.js App Router conventions.

## Backend

```bash
cd backend
uv sync
uv run fastapi dev
```

* Use async endpoints where appropriate.
* Keep routes thin; place business logic in services.
* Validate API input/output with Pydantic models.
* Use dependency injection for shared services.
* Never hard-code secrets, URLs, model names, or provider credentials.
* Configure the FastAPI entrypoint in `pyproject.toml` when needed.

## Dependencies

Add backend packages with:

```bash
uv add <package>
```

Development packages:

```bash
uv add --dev <package>
```

After cloning:

```bash
uv sync
```

Commit `uv.lock`. Do not manually modify the generated environment.

## AI

* Implement AI providers behind a common interface.
* Support Ollama as the local provider.
* Implement cloud providers as configurable fallbacks.
* Handle timeouts, unavailable providers, invalid responses, and rate limits.
* Never log prompts, responses, API keys, or sensitive user data unnecessarily.
* Keep model/provider configuration centralized.

## Code Quality

* **Ruff:** linting and formatting.
* **pytest:** automated tests.
* Write tests for new backend behavior and bug fixes.
* Run tests after every change:

```bash
cd backend
uv run pytest
```

* Before completing work, run lint/format checks and relevant tests.
* Keep functions small, readable, and single-purpose.
* Prefer clear names over excessive comments.

## Security

* Never commit `.env`, API keys, tokens, passwords, or credentials.
* Keep `.env` in `.gitignore`.
* Validate all external input.
* Do not expose internal errors or secrets through API responses.
* Never put AI provider secrets in frontend code.

## Agent Rules

1. Inspect existing code before changing it.
2. Follow the existing architecture and conventions.
3. Make the smallest clean change that solves the task.
4. Do not introduce unnecessary dependencies.
5. Update tests when behavior changes.
6. Run tests and linting after changes.
7. Never bypass type checking, linting, or tests just to make code pass.
8. Do not rewrite unrelated code.
9. Keep frontend/backend contracts synchronized.
10. For AI changes, preserve the provider abstraction and fallback behavior.
11. Do not commit secrets or generated environment files.

## Run

**Frontend:**

```bash
cd frontend && npm run dev
```

**Backend:**

```bash
cd backend && uv run fastapi dev
```

**Tests:**

```bash
cd backend && uv run pytest
```
>>>>>>> 8c07bb2 (:hammer: Update Agents.md)
