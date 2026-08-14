# Design Context

## Direction

ProjectSpin combines:

**Minimalism × Neobrutalism**

The interface should feel like a modern developer tool with a playful and opinionated visual identity.

Minimalism provides:

* clarity;
* whitespace;
* strong hierarchy;
* low visual noise;
* focused interactions.

Neobrutalism provides:

* personality;
* strong borders;
* bold typography;
* visible structure;
* hard shadows;
* expressive interactive states.

The goal is not to reproduce a full neobrutalist website.

ProjectSpin should remain minimal first, with neobrutalist elements used intentionally.

---

## Product Feel

The interface should feel:

* experimental;
* technical;
* playful;
* fast;
* tactile;
* slightly unconventional.

It should not feel:

* corporate;
* overly polished;
* casino-like;
* childish;
* visually noisy;
* heavily futuristic.

ProjectSpin is a developer tool, not a gaming interface.

---

## Visual Principles

### 1. Clear structure

Every screen should make the primary action obvious.

Avoid unnecessary containers, decorations, and repeated information.

The user should immediately understand:

> Spin → refine → save.

---

### 2. Strong surfaces

Important elements may use:

* visible borders;
* slightly oversized typography;
* hard shadows;
* offset surfaces;
* high-contrast states.

Use these elements to communicate structure rather than decoration.

Not every component needs a brutalist treatment.

---

### 3. Limited color

Prefer a neutral base with one primary accent and occasional semantic colors.

Avoid using many competing accent colors.

Color should communicate:

* interaction;
* selection;
* state;
* hierarchy.

The product should still work visually when mostly monochromatic.

---

### 4. Motion with purpose

Animation should explain state changes.

Motion may be used for:

* slot spinning;
* page initialization;
* generated results;
* agent activity;
* progress;
* transitions between states.

Avoid decorative motion that does not communicate information.

---

## Core UI Patterns

ProjectSpin may use the following patterns as part of its visual language.

### Slot Machine

The primary interaction.

Each project dimension behaves like a vertical slot:

```text
BUILD
AI Agent

FOR
Developers

THAT
Analyzes repositories

WITH
GitHub API

CONSTRAINT
Local-first
```

Unlocked slots animate during a spin.

Locked slots remain stable.

The slot animation should feel mechanical and satisfying without resembling a casino machine.

---

### Text Scramble

Text scramble may be used when transitioning from an unknown value to a generated value.

Good use cases:

* generated project title;
* challenge reveal;
* loading labels;
* mode transitions.

Example:

```text
PR0J#C? SP!N
      ↓
PROJECT SPIN
```

Text scramble should be short.

It should never reduce readability for long periods.

Respect `prefers-reduced-motion`.

---

### Skeletons

Skeleton states should be used during application initialization or while content is being prepared.

They may represent:

* slots;
* generated challenge;
* saved ideas;
* future AI-generated content.

Skeletons should resemble the final layout closely.

Avoid generic full-page loading spinners when the structure of the page is already known.

---

### Bento Grid

Bento layouts may be used for secondary information.

Potential uses:

* generated idea summary;
* project attributes;
* difficulty;
* technologies;
* saved ideas;
* statistics;
* future generated architecture.

Example:

```text
┌─────────────────────────────┐
│ PROJECT IDEA                │
│ RepoSherpa                  │
├───────────────┬─────────────┤
│ Difficulty    │ Category    │
│ Intermediate  │ DevTools    │
├───────────────┴─────────────┤
│ GitHub + LLM + Local-first  │
└─────────────────────────────┘
```

Do not use a bento grid when a simple vertical layout communicates the information better.

---

### Steps

Steps communicate processes with multiple explicit phases.

Potential future uses:

```text
Idea
 ↓
Refine
 ↓
Architecture
 ↓
Build
```

For future AI-powered workflows:

```text
Understanding idea
      ↓
Generating requirements
      ↓
Designing architecture
      ↓
Creating build plan
```

Steps should represent real system states, not decorative progression.

---

### Avatar Group

Avatar groups should represent actors or agents, not arbitrary decoration.

For future multi-agent capabilities, an avatar group may represent active agents such as:

```text
[ PM ] [ UX ] [ ARCH ] [ ENG ]
```

Possible agents:

* Product Agent
* Design Agent
* Architecture Agent
* Engineering Agent
* Research Agent

Each agent should have a clear responsibility.

The UI should communicate agent status when relevant:

```text
idle
working
complete
failed
```

Do not add fake agents purely to make the product appear more sophisticated.

---

## Future Multi-Agent Direction

ProjectSpin may eventually evolve from:

```text
idea generator
```

into:

```text
idea generator
      ↓
idea refinement
      ↓
multi-agent exploration
      ↓
project blueprint
```

Example:

```text
Generated Idea

"Build a local-first repository onboarding agent."

              ↓

        EXPAND IDEA

              ↓

┌────────────────────────────────────┐
│ Agents                             │
│                                    │
│ [PM] [UX] [ARCH] [ENG]             │
│                                    │
│ ● Product        complete           │
│ ● Design         working            │
│ ○ Architecture   waiting            │
│ ○ Engineering    waiting            │
└────────────────────────────────────┘
```

The user should be able to understand:

* which agents exist;
* what each agent is responsible for;
* which agent is currently active;
* what output each agent produced.

Multi-agent behavior must provide real product value.

It should not be introduced only as a visual effect.

---

## Typography

Typography should be one of the strongest elements of the interface.

Prefer:

* strong headings;
* compact labels;
* readable body text;
* selective monospace usage.

Monospace is appropriate for:

* project dimensions;
* technical metadata;
* constraints;
* status labels;
* generated technical concepts.

Do not render the entire application in monospace.

---

## Borders and Shadows

Neobrutalist personality may be introduced through:

* visible borders;
* strong outlines;
* small offset shadows;
* abrupt hover-state movement.

Example concept:

```text
Default

┌─────────────────┐
│   SPIN          │
└─────────────────┘
  ▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀

Pressed

  ┌─────────────────┐
  │   SPIN          │
  └─────────────────┘
```

Interactive movement should remain subtle.

Avoid large shadows on every element.

---

## Corners

Prefer slightly rounded or nearly-square surfaces.

Avoid excessively rounded "pill everything" interfaces.

Pills are appropriate for:

* tags;
* filters;
* statuses;
* compact controls.

Primary cards and slots should retain stronger rectangular geometry.

---

## Spacing

Whitespace is part of the design.

Prefer:

* fewer components;
* more breathing room;
* clear vertical rhythm;
* strong separation between primary and secondary areas.

Do not fill empty space merely because it exists.

---

## Initial Page Experience

The initial page can intentionally reveal itself.

Example sequence:

```text
Skeleton layout
      ↓
ProjectSpin title scramble
      ↓
Slots become available
      ↓
Spin CTA appears
```

The entire sequence should remain short.

The user should be able to interact quickly.

Initialization animation must not artificially delay the application.

---

## Primary Screen

The initial screen should prioritize the generator.

Conceptually:

```text
PROJECTSPIN

What should I build next?


BUILD
┌──────────────────────────────────┐
│ AI Agent                      🔓 │
└──────────────────────────────────┘

FOR
┌──────────────────────────────────┐
│ Developers                    🔓 │
└──────────────────────────────────┘

THAT
┌──────────────────────────────────┐
│ Understands repositories      🔓 │
└──────────────────────────────────┘

WITH
┌──────────────────────────────────┐
│ GitHub + LLM                  🔓 │
└──────────────────────────────────┘

CONSTRAINT
┌──────────────────────────────────┐
│ Local-first                   🔓 │
└──────────────────────────────────┘


        [ SPIN PROJECT ]


Generated challenge

Build an AI Agent for Developers that...
```

The generator should dominate the visual hierarchy.

Secondary features should not compete with it.

---

## Interaction Feedback

Interactive elements should visibly react.

Use combinations of:

* position;
* border;
* shadow;
* background;
* typography.

Hover and press states should feel tactile.

Avoid interaction feedback based entirely on opacity.

---

## Accessibility

ProjectSpin should:

* support keyboard navigation;
* expose visible focus states;
* maintain sufficient contrast;
* avoid color-only state communication;
* support `prefers-reduced-motion`;
* avoid animations that prevent interaction;
* use semantic HTML when possible.

Reduced-motion mode should preserve meaning while removing unnecessary animation.

---

## Responsive Design

Desktop may use wider compositions and bento layouts.

Mobile should favor vertical stacking.

Core functionality must remain accessible:

```text
Spin
Lock
Reroll
Save
```

Avoid forcing desktop layouts into narrow screens.

---

## Design Boundaries

Avoid:

* excessive gradients;
* glassmorphism as the primary style;
* glowing cyberpunk interfaces;
* casino visuals;
* decorative 3D;
* excessive rounded cards;
* animation on every component;
* unnecessary dashboards;
* dense navigation;
* multiple competing accent colors.

---

## Design Rule

When adding a visual element, ask:

> Does this improve hierarchy, interaction feedback, or understanding?

If the answer is no, remove it.

ProjectSpin should feel expressive because of a few strong decisions, not because every surface is decorated.
