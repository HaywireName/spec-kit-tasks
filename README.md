# spec-kit-tasks

A simple task management CLI to add, list (color-coded), and complete tasks stored locally in `.tasks.json`.

## Requirements
- Python 3.14+
- Optional: [uv](https://docs.astral.sh/uv/) for fast installs and runs

## Quickstart

Using uv (recommended):

1. Install dependencies
   - `uv sync`
2. Run commands
   - `uv run python main.py add "Write report"`
   - `uv run python main.py add "Prepare slides" --deadline 2099-01-02`
   - `uv run python main.py list`
   - `uv run python main.py list --json`
   - `uv run python main.py complete 1`

Without uv:

1. Create a venv and install dependencies
   - `python -m venv .venv && . .venv/bin/activate`
   - `pip install -r <(python - <<'PY'\nimport tomllib, sys; print('\n'.join(tomllib.load(open('pyproject.toml','rb'))['project']['dependencies']))\nPY
)`
2. Run commands
   - `python main.py add "Write report"`
   - `python main.py list`

## Notes
- Storage file: `.tasks.json` in the current working directory
- Colors: red (overdue), yellow (due ≤ 3 days), white (others/no deadline); applied only when stdout is a TTY
- JSON output: `list --json` emits an array of objects with fields `id`, `description`, `deadline|null`, `created_at`, `relative`, `urgency`

## Exit Codes
- 0: success
- 2: validation error (e.g., invalid date)
- 3: not found (e.g., completing unknown id)
