# Agent Instructions

## Product

ProjectSpin generates software project ideas using five combinable slots:

Build → For → That → With → Constraint.

Read `docs/specs/mvp.md` before modifying product behavior.

## Architecture

Generation logic belongs in `src/domain/`.

Catalog data belongs in `src/data/`.

React components must not implement generation rules.

Persistence belongs in `src/storage/`.

## MVP Constraints

Do not add:

- backend
- authentication
- database
- LLM dependencies
- cloud services

unless a spec explicitly requires them.

## Verification

Before completing a change, run:

npm test
npm run lint
npm run build

Do not report a task complete if any required verification fails.

## Change Discipline

Prefer the smallest change that satisfies the active spec.

Do not perform unrelated refactors.

Update tests whenever observable behavior changes.
