# ProjectSpin 🎰

> A slot machine for developers who don't know what to build next.

ProjectSpin generates software project ideas by combining five dimensions:

```text
BUILD      → AI Agent
FOR        → Developers
THAT       → Analyzes unfamiliar repositories
WITH       → GitHub + LLM
CONSTRAINT → Local-first
```

Result:

> Build an AI Agent for Developers that analyzes unfamiliar repositories using GitHub + LLM while remaining local-first.

## MVP

* 🎰 Spin project ideas
* 🔒 Lock individual slots
* 🔄 Reroll the rest
* 💾 Save interesting ideas
* 🧩 Avoid incompatible combinations

## Stack

* React
* TypeScript
* Vite
* localStorage

No backend. No accounts. No LLM required for the MVP.

## Development

```bash
npm install
npm run dev
```

## Verify

```bash
npm test
npm run lint
npm run build
```

## Docs

See [`docs/specs/mvp.md`](docs/specs/mvp.md) for the product contract.
