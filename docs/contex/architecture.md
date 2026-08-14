# Architecture Context

## Overview

ProjectSpin is a client-side application.

The MVP architecture should remain intentionally small.

```text
Catalog Data
     ↓
Generation Engine
     ↓
ProjectIdea
     ↓
React UI
     ↓
Local Persistence
```

The application does not require a backend for the MVP.

---

## Technology

Current intended stack:

```text
React
TypeScript
Vite
localStorage
```

Styling may use plain CSS or Tailwind depending on the implementation decision.

Animation should preferably use native CSS/browser capabilities unless a dedicated animation dependency provides clear value.

Avoid dependencies that do not materially simplify the implementation.

---

## Architectural Goals

The architecture should optimize for:

* clear responsibilities;
* deterministic business logic;
* easy testing;
* small modules;
* minimal coupling to React;
* easy modification by humans and coding agents.

The domain logic should be understandable without reading UI code.

---

## Suggested Structure

```text
src/
├── app/
│   └── App.tsx
│
├── components/
│   ├── Slot.tsx
│   ├── SlotMachine.tsx
│   ├── ChallengeCard.tsx
│   └── SavedIdeas.tsx
│
├── domain/
│   ├── project-idea.ts
│   ├── generate-idea.ts
│   └── compatibility.ts
│
├── data/
│   ├── builds.ts
│   ├── audiences.ts
│   ├── problems.ts
│   ├── technologies.ts
│   └── constraints.ts
│
├── storage/
│   └── saved-ideas.ts
│
└── styles/
```

This structure is guidance rather than a requirement to create empty files.

Only introduce a module when it has an actual responsibility.

---

## Domain Layer

`src/domain/` contains application rules that do not depend on React.

Examples:

* selecting options;
* preserving locked slots;
* evaluating compatibility;
* creating a `ProjectIdea`;
* converting selected dimensions into domain state.

Domain code must not import React.

Domain code must not access `localStorage`.

Domain code should be testable as plain TypeScript.

---

## ProjectIdea

The central domain object represents one generated project.

Conceptually:

```ts
type ProjectIdea = {
  build: SlotOption;
  audience: SlotOption;
  problem: SlotOption;
  technology: SlotOption;
  constraint: SlotOption;
};
```

A catalog option can contain metadata used by compatibility rules.

Conceptually:

```ts
type SlotOption = {
  id: string;
  label: string;
  tags: string[];
};
```

Types may evolve as requirements become clearer.

Avoid adding fields without an actual use case.

---

## Catalog Layer

`src/data/` contains the available slot options.

Catalog files contain data, not generation behavior.

Example responsibilities:

```text
builds.ts
→ available BUILD values

audiences.ts
→ available FOR values

problems.ts
→ available THAT values

technologies.ts
→ available WITH values

constraints.ts
→ available CONSTRAINT values
```

Catalogs must not depend on React components.

Catalogs should be easy to edit without changing generation code.

---

## Generation Engine

Project generation must not happen directly inside UI components.

The generation engine receives:

* current slot values;
* lock state;
* catalogs;
* randomness.

It returns a new `ProjectIdea`.

Conceptually:

```text
Current Idea
   +
Locked Slots
   +
Catalogs
   +
Random Source
      ↓
Generation Engine
      ↓
New ProjectIdea
```

Unlocked dimensions may change.

Locked dimensions must not change.

---

## Randomness

Random selection should be isolated.

Do not scatter calls to:

```ts
Math.random()
```

throughout components or domain functions.

Prefer injecting or wrapping the random source.

Conceptually:

```ts
type RandomSource = () => number;
```

Production may use:

```ts
Math.random
```

Tests may provide deterministic values.

This allows generation behavior to be tested reliably.

---

## Compatibility

Compatibility is a domain concern.

It must live outside React components.

The MVP should use lightweight rules based on metadata such as tags.

Example:

```text
AI Agent
tags: ai, backend, automation

Tool Calling
tags: ai, backend, automation
```

Shared tags can contribute to compatibility.

The exact scoring system should remain simple.

Do not build a complex recommendation engine unless product requirements justify it.

Important principle:

> Prefer understandable rules over clever rules.

---

## UI Layer

React components are responsible for:

* displaying slots;
* displaying lock state;
* handling interaction;
* triggering spins;
* displaying animation;
* rendering results;
* displaying saved ideas.

React components are not responsible for:

* deciding compatibility;
* selecting random catalog entries;
* defining domain rules;
* directly implementing persistence rules.

UI state may include:

```text
current idea
lock state
spin state
saved ideas
```

---

## Spin State

The application has three conceptual states:

```text
idle
spinning
result
```

During `spinning`:

* unlocked slots animate;
* locked slots remain visually stable;
* a second spin should not begin;
* final generated values should not continuously change with animation frames.

The animation is presentation.

Generation is domain behavior.

Keep those concepts separate.

A valid implementation may:

1. generate the final result;
2. start the visual animation;
3. reveal the generated result when the animation finishes.

---

## Persistence

Persistence belongs in:

```text
src/storage/
```

The MVP uses:

```text
localStorage
```

UI components should call a small storage abstraction instead of duplicating serialization logic.

Example conceptual interface:

```ts
saveIdea(idea)
loadIdeas()
removeIdea(id)
```

Storage code should handle malformed or missing persisted data safely.

A corrupted localStorage value must not crash the application.

---

## Rendered Challenge

The human-readable challenge sentence is derived from `ProjectIdea`.

The structured idea remains the source of truth.

Do not store only a sentence such as:

```text
Build an agent for developers...
```

because that loses the underlying dimensions.

Prefer:

```text
ProjectIdea
       ↓
formatter
       ↓
challenge sentence
```

This allows the UI wording to change without migrating stored ideas.

---

## Error Handling

The application should fail gracefully when possible.

Examples:

### Invalid persisted data

Ignore or reset the invalid entry rather than crashing the application.

### Empty catalog

Generation should produce an explicit failure rather than silently returning invalid data.

### No compatible candidate

The compatibility logic should have a defined fallback strategy.

It must not enter an infinite generation loop.

---

## Testing Strategy

Prioritize domain behavior.

### Domain tests

Verify:

* every generated idea contains all required dimensions;
* locked values remain unchanged;
* unlocked dimensions can be replaced;
* compatibility rules behave as expected;
* deterministic randomness produces deterministic output;
* generation cannot loop indefinitely.

### Storage tests

Verify:

* ideas can be serialized;
* ideas can be loaded;
* malformed persisted state is handled safely;
* ideas can be removed.

### UI tests

Verify user-visible behavior such as:

* Spin triggers generation;
* locking a slot preserves its value;
* saved ideas appear;
* saved ideas can be removed.

Avoid tests that depend heavily on internal component implementation.

---

## Dependency Direction

Preferred dependency direction:

```text
data ───────┐
            ↓
         domain
            ↓
           app
            ↓
       components

storage ← app/components
```

Most importantly:

```text
domain
```

must not depend on:

```text
React
browser UI
localStorage
```

This keeps the core generation system portable and testable.

---

## Change Guidelines

When modifying ProjectSpin:

1. identify the layer responsible for the behavior;
2. make the smallest coherent change;
3. avoid moving domain rules into UI components;
4. add or update tests when observable behavior changes;
5. run required verification before declaring completion.

Do not perform unrelated refactors during feature work.

---

## Verification

Before considering a change complete:

```bash
npm test
npm run lint
npm run build
```

All required commands must pass.

If one fails, the task is not complete unless the failure is clearly documented as pre-existing and unrelated.

---

## Architecture Guardrail

When deciding where new behavior belongs, use:

```text
Is it a project-generation rule?
→ domain/

Is it static project-option data?
→ data/

Is it browser persistence?
→ storage/

Is it visual or interactive behavior?
→ components/
```

If the answer is unclear, prefer keeping the domain independent from React and browser APIs.
