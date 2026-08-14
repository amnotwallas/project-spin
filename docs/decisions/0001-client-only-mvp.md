# 0001 — Client-only MVP

## Status

Accepted

## Context

ProjectSpin is an idea generator for developers.

The MVP only needs to:

- generate project combinations;
- lock individual slots;
- reroll unlocked slots;
- save ideas locally;
- render the generated challenge.

None of these capabilities require a backend, database, authentication system, or LLM.

Adding those systems now would increase complexity without improving the core product validation.

## Decision

The MVP will be implemented as a client-only web application.

It will use:

- React
- TypeScript
- Vite
- localStorage

The MVP will not introduce:

- backend services;
- databases;
- authentication;
- cloud persistence;
- LLM APIs.

Project generation and compatibility rules will run locally in the browser.

## Consequences

### Positive

- simpler architecture;
- faster development;
- zero backend infrastructure;
- no API costs;
- deterministic generation;
- easier automated testing;
- easier local development for coding agents.

### Negative

- saved ideas are limited to the current browser;
- there is no cross-device synchronization;
- generation quality depends on curated catalogs and compatibility rules;
- advanced AI-powered expansion is deferred.

## Revisit

Revisit this decision if a future feature requires capabilities such as:

- account-based saved ideas;
- cross-device synchronization;
- collaborative features;
- server-side integrations;
- AI-powered idea expansion.

A new ADR should supersede this decision if the architecture changes.
