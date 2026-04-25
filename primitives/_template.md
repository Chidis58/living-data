
# Primitive: [NAME]

**Status: [DRAFT | IN PROGRESS | SETTLED]**

---

## Definition

> One precise sentence. No qualifiers. No "kind of" or "similar to."

---

## What [NAME] Is Not

- Distinguish from the closest existing behavior
- Distinguish from the closest primitive already defined in this repo
- Distinguish from any naive implementation (logging, caching, tagging, etc.)

---

## The Core Law

State the irreducible rule. One line if possible.

---

## Anatomy

Break the primitive into its minimum necessary parts. Each part must be:
- Named
- Distinct (not reducible to another part)
- Consequential (removing it collapses the primitive into something that already exists)

---

## What Becomes Impossible After [NAME]

> This is the primitive test. If you cannot answer this precisely, the primitive is not ready.

Name the one thing that was previously possible — and is now structurally impossible. Not harder. Not discouraged. **Impossible.**

---

## What [NAME] Destroys in Current Architecture

| Current Assumption | What [NAME] Replaces It With |
|---|---|
| | |

---

## Relationship to Other Primitives

- **Requires:** primitives that must exist before this one can be implemented
- **Enables:** primitives that become constructable once this one exists
- **Conflicts with:** any existing system behavior that this primitive structurally contradicts

---

## Implementation Path

### Layer 1 — Conceptual
Is the definition settled? Has the primitive test been passed?

### Layer 2 — Domain Embedding
Which narrow environment will this be embedded in first?

### Layer 3 — Behavioral Dependency
What breaks — meaningfully — if this primitive is removed?

### Layer 4 — Exportability
What is the signal that this primitive has spread beyond its origin?

---

## Decision Log

| Date | Decision | Reason |
|---|---|---|
| | | |
