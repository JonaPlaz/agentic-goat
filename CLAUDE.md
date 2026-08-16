# agentic-goat

All-time ranking of the greatest players who played in the NBA. Two halves separated by a strict boundary: LLM agents collect and explain, deterministic Python computes.

The project is self-hosted: users run it themselves and bring their own model credentials. There is no hosted service.

## Architecture

- `agents/` — Python code that calls an LLM. Researches sources, normalizes them into inputs for the computation, writes the explanations of its results.
- `deterministic/` — pure Python. Consumes the collected data, produces the ranking.
- `.claude/` — development tooling only. Never part of what a user runs.
- Each folder has its own `README.md`: update it when the folder's role changes.

## Agents / deterministic boundary

- An agent never decides a rank, a score, or a weight. It supplies sourced data and prose.
- `deterministic/` contains no LLM call, no API key, no network access to a model.
- Every piece of data entering the computation carries its source (URL or dataset identifier).
- Same input, same output: no clock, no unseeded randomness, no non-deterministic iteration order in `deterministic/`.

## Model providers

- The project is model-agnostic by design. Anthropic is the first provider, not the only one.
- No provider SDK is imported outside the adapter layer that isolates it. Everything else talks to an internal interface.
- Provider and model are configuration, never hardcoded at a call site.
- That adapter layer does not exist yet. Ask before introducing one.

## Python

- Type hints required on every public function.
- Comments and docstrings in English.
- Every computation function has a unit test. No test, no merge.

### Tooling — to be completed

Python version, package manager, test runner, and linter are not chosen yet. Replace this section with the exact commands (install, test, lint) at the first Python code commit. Do not invent a command while this section is a TODO: ask.

## Agents

- One agent = one responsibility.
- An agent producing data for the computation returns structured JSON, not prose.
- An agent writing an explanation cites the data it explains and introduces no figure absent from the computation output.

## Git

- Commit format: `type: subject`, in English, imperative mood.
- Types in use: `feat`, `fix`, `docs`, `chore`.
- Example: `chore: scaffold agents and deterministic directories`.
- One PR, one thing.
