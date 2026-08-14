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

## Design

Before modifying UI, layout, animation, or interaction behavior, read:

- `docs/context/design.md`

Preserve the established visual direction:

Minimalism × Neobrutalism.

Do not introduce visual patterns that conflict with the design context unless an active spec explicitly requires them.

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
