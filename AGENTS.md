# Agent Instructions

## Product

ProjectSpin generates software project ideas using five combinable slots:

Build → For → That → With → Constraint.

Before modifying product behavior, read:

- `docs/specs/mvp.md`
- `docs/context/product.md`
- `docs/context/architecture.md`

## Architecture

Generation logic belongs in `src/domain/`.

Catalog data belongs in `src/data/`.

React components must not implement generation rules.

Persistence belongs in `src/storage/`.

Keep domain logic independent from React and browser APIs whenever possible.

## MVP Constraints

Do not add:

- backend
- authentication
- database
- LLM dependencies
- cloud services

unless an active spec explicitly requires them.

## Verification

Before completing any change, run:

```bash
npm run check
```
