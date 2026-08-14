# ProjectSpin — MVP Product Spec

## 1. Product

**ProjectSpin** is a project idea generator for developers.

It uses a slot-machine interaction to combine several dimensions into a coherent project challenge.

The product should answer one question:

> What should I build next?

## 2. Goal

Help developers quickly discover interesting software project ideas without requiring them to manually brainstorm from scratch.

The MVP should make generating ideas:

* fast;
* playful;
* repeatable;
* controllable;
* useful enough to produce something someone could actually build.

## 3. Core Concept

Every project idea consists of five slots:

```text
BUILD       → what is being built
FOR         → who it is for
THAT        → what problem it solves
WITH        → technology or technique
CONSTRAINT  → engineering restriction
```

Example:

```text
BUILD
AI Agent

FOR
Developers

THAT
Analyzes unfamiliar repositories

WITH
GitHub + LLM

CONSTRAINT
Local-first
```

Generated challenge:

> Build an AI Agent for Developers that analyzes unfamiliar repositories using GitHub + LLM while remaining local-first.

## 4. MVP Features

### Spin

The user can press `Spin`.

All unlocked slots animate and receive a new value.

### Lock

Every slot has a lock control.

When locked:

* its value does not change;
* subsequent spins only affect unlocked slots.

Example:

```text
BUILD       AI Agent               🔒
FOR         Developers             🔒
THAT        Reviews pull requests
WITH        GitHub API
CONSTRAINT  Human-in-the-loop
```

The user can keep `AI Agent` and `Developers` while rerolling everything else.

### Generated Challenge

After every completed spin, the application displays a readable sentence describing the generated project.

### Save Idea

The user can save a generated combination.

Saved ideas persist locally in the browser.

No user account is required.

### Spin Again

The user can generate another combination immediately.

## 5. Slots

### Build

Examples:

* AI Agent
* CLI Tool
* Developer Tool
* API
* Dashboard
* Automation
* RAG Application
* MCP Server
* Browser Extension
* Monitoring Tool

### For

Examples:

* Developers
* Students
* Small Businesses
* Recruiters
* Content Creators
* Support Teams
* Data Teams
* AI Engineers
* Open Source Maintainers

### That

Examples:

* analyzes unfamiliar repositories;
* detects recurring problems;
* automates repetitive workflows;
* monitors external changes;
* summarizes complex information;
* organizes knowledge;
* reviews code changes;
* evaluates LLM outputs;
* detects anomalies;
* generates structured reports.

### With

Examples:

* LLM tool calling
* RAG
* GitHub API
* local LLMs
* embeddings
* WebSockets
* background jobs
* structured outputs
* MCP
* semantic search

### Constraint

Examples:

* local-first;
* offline-capable;
* no database;
* human-in-the-loop;
* under $5/month;
* privacy-first;
* real-time;
* must include automated evals;
* must expose an API;
* must work from the terminal.

## 6. Compatibility

Pure randomness should not be allowed to create obviously meaningless combinations.

Each catalog item can include metadata.

Example conceptual model:

```ts
type SlotOption = {
  id: string;
  label: string;
  tags: string[];
};
```

Possible tags:

```text
ai
backend
frontend
devtools
data
realtime
local
automation
```

Generation logic should prefer combinations sharing compatible tags.

The compatibility system should remain intentionally simple in the MVP.

Do not introduce an AI model purely to validate combinations.

## 7. Generation Engine

Randomness must live outside UI components.

Conceptually:

```text
catalogs
   ↓
compatibility filter
   ↓
random selector
   ↓
ProjectIdea
   ↓
UI
```

The random generator should support dependency injection of its RNG so generation can be tested deterministically.

Example domain object:

```ts
type ProjectIdea = {
  build: SlotOption;
  audience: SlotOption;
  problem: SlotOption;
  technology: SlotOption;
  constraint: SlotOption;
};
```

## 8. UI State

The application has three relevant states:

```text
idle
 ↓
spinning
 ↓
result
```

While spinning:

* unlocked slots animate;
* locked slots remain static;
* another spin cannot start.

When the animation finishes:

* final values are committed;
* the generated challenge appears.

## 9. Visual Direction

Default direction:

**Minimal developer-tool UI with slot-machine behavior.**

Not a literal casino interface.

Characteristics:

* dark or neutral interface;
* large typography;
* generous spacing;
* subtle borders;
* smooth vertical slot animation;
* monospace used selectively;
* minimal visual noise.

The interaction should feel playful without making the application look like a gambling product.

## 10. Architecture

MVP is a client-side application.

Recommended stack:

```text
React
TypeScript
Vite
CSS/Tailwind
localStorage
```

Animation can use either:

```text
CSS animations
```

or a lightweight animation library.

Avoid adding infrastructure until needed.

## 11. Suggested Boundaries

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
│   └── generate-idea.ts
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

Responsibilities must remain separated.

UI components must not contain generation rules.

Storage must not contain domain logic.

Data catalogs must not depend on React.

## 12. Persistence

Only saved ideas need persistence.

Use:

```text
localStorage
```

Store:

```text
id
createdAt
ProjectIdea
```

Do not introduce:

* database;
* authentication;
* cloud sync.

## 13. Non-Goals

The MVP does **not** include:

* LLM generation;
* AI-generated specifications;
* authentication;
* user profiles;
* backend;
* database;
* social sharing;
* project scoring;
* GitHub integration;
* project tracking;
* community ideas.

These can be explored later.

## 14. Testing

Generation engine tests should verify:

* every generated idea contains all five fields;
* locked slots remain unchanged;
* unlocked slots can change;
* incompatible combinations are rejected;
* seeded/injected randomness produces deterministic output.

Storage tests should verify:

* ideas can be saved;
* saved ideas can be loaded;
* ideas can be removed.

UI tests should prioritize behavior over implementation details.

## 15. Acceptance Criteria

The MVP is complete when:

* [ ] the page shows five project slots;
* [ ] pressing `Spin` animates every unlocked slot;
* [ ] every slot can be independently locked;
* [ ] locked values survive subsequent spins;
* [ ] every completed spin produces a coherent project challenge;
* [ ] generated ideas can be saved;
* [ ] saved ideas survive a page refresh;
* [ ] saved ideas can be removed;
* [ ] generation logic has automated tests;
* [ ] the application works without a backend;
* [ ] the application works without an LLM.

## 16. Future Ideas

Possible future iterations:

### Filters

```text
AI
Backend
Frontend
DevTools
Hardware
Data
```

### Modes

```text
Weekend Project
Portfolio Project
Hard Mode
Local-first
AI Engineering
```

### Expand Idea

Use an LLM to transform a selected idea into:

* problem statement;
* requirements;
* architecture;
* milestones;
* stretch goals.

### Difficulty

Estimate:

```text
Easy
Intermediate
Advanced
```

### History

Remember previous spins.

### Share

Generate a shareable URL encoding the selected combination.

## 17. Product Rule

ProjectSpin should remain:

> A tool that generates ideas, not a project management platform.

New features should be rejected if they move the MVP away from that purpose.
