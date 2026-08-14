# Product Context

## What is ProjectSpin?

ProjectSpin is a project idea generator for developers.

Its purpose is simple:

> Help developers answer: "What should I build next?"

The application uses a slot-machine-style interaction to generate project ideas by combining multiple dimensions.

A project idea is composed of:

```text
BUILD
FOR
THAT
WITH
CONSTRAINT
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

Which becomes:

> Build an AI Agent for Developers that analyzes unfamiliar repositories using GitHub + LLM while remaining local-first.

---

## Product Philosophy

ProjectSpin should be:

* fast;
* playful;
* simple;
* useful;
* slightly unpredictable;
* developer-oriented.

The application should create combinations that feel surprising without becoming meaningless.

The slot-machine interaction is part of the personality of the product, but ProjectSpin is not intended to look or behave like a gambling application.

The visual language should feel closer to a modern developer tool than a casino.

---

## Core User Flow

The primary flow is:

```text
Open ProjectSpin
        ↓
See current slots
        ↓
Press Spin
        ↓
Slots animate
        ↓
Receive project idea
        ↓
Lock interesting dimensions
        ↓
Spin remaining dimensions
        ↓
Save idea or continue spinning
```

This flow should remain extremely fast.

A user should be able to generate another idea with one interaction.

---

## Project Dimensions

### Build

Defines what kind of software should be created.

Examples:

* AI Agent
* CLI Tool
* API
* Dashboard
* Automation
* MCP Server
* Browser Extension
* Developer Tool
* RAG Application
* Monitoring Tool

---

### For

Defines the target user or audience.

Examples:

* Developers
* AI Engineers
* Students
* Open Source Maintainers
* Recruiters
* Small Businesses
* Data Teams
* Support Teams

---

### That

Defines the problem or capability.

Examples:

* analyzes unfamiliar repositories;
* reviews code changes;
* automates repetitive workflows;
* monitors external changes;
* evaluates LLM outputs;
* organizes knowledge;
* detects anomalies;
* generates structured reports.

---

### With

Introduces a technology, technique, or engineering concept.

Examples:

* tool calling
* RAG
* GitHub API
* local LLMs
* embeddings
* MCP
* WebSockets
* background jobs
* semantic search
* structured outputs

---

### Constraint

Introduces a restriction that makes the project more interesting.

Examples:

* local-first;
* privacy-first;
* human-in-the-loop;
* under $5/month;
* offline-capable;
* no database;
* real-time;
* must include automated evals;
* must expose an API;
* must work from the terminal.

---

## Locking

Every slot can be locked independently.

A locked slot must retain its current value when another spin occurs.

Example:

```text
BUILD       AI Agent      [locked]
FOR         Developers    [locked]
THAT        ...
WITH        ...
CONSTRAINT  ...
```

The user can therefore iteratively refine an idea instead of generating every dimension from scratch.

Locking is a core feature, not optional polish.

---

## Idea Quality

ProjectSpin should not behave like five completely independent random lists.

Generated ideas should usually make conceptual sense.

For example:

Good:

> Build a CLI Tool for Developers that analyzes dependency vulnerabilities using the GitHub API while working entirely from the terminal.

Bad:

> Build a CSS Library for Recruiters that detects heart rate using RAG with no database.

Unexpected combinations are desirable.

Nonsensical combinations are not.

The generation system should use lightweight compatibility rules rather than an LLM in the MVP.

---

## Saved Ideas

Users can save interesting generated ideas.

Saved ideas are local to the browser in the MVP.

No account is required.

Saved ideas should contain the complete generated combination rather than only the rendered sentence.

---

## MVP

The MVP contains:

* five project dimensions;
* spin interaction;
* slot animation;
* independent locking;
* coherent idea generation;
* saved ideas;
* local persistence.

---

## Non-Goals

The initial product is not:

* a project management application;
* an AI coding assistant;
* a social network;
* an idea marketplace;
* a GitHub project generator;
* a course platform.

The MVP does not require:

* authentication;
* backend services;
* cloud storage;
* database infrastructure;
* LLM APIs;
* GitHub integration;
* payments.

Do not add these unless a later specification explicitly requires them.

---

## Future Direction

Possible future capabilities include:

* project categories;
* difficulty levels;
* weekend-project mode;
* portfolio-project mode;
* AI engineering mode;
* history;
* shareable project URLs;
* custom catalogs;
* community-generated options.

A later AI-powered feature may expand a selected idea into:

```text
Problem
Requirements
Architecture
Milestones
Stretch goals
```

This should enhance the generator rather than replace it.

---

## Product Guardrail

When evaluating a new feature, ask:

> Does this help someone discover or refine what they should build next?

If the answer is no, it is probably outside the core product.
