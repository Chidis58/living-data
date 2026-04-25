# living-data

**One operation that exists in every computing system ever built is undefined here.**

```
read(entity) → content
```

Returning content without mutating the state of both the entity and the accessor.

Legal everywhere. HTTP GET. SQL SELECT. File open. All of them.

**Undefined here.** Not blocked. Not logged. Undefined — the way division by zero is undefined.

---

## What Replaces It

```
witness(entity, accessor) → { content, imprint, entityState }
```

Every access is an exchange. Both parties are permanently changed. Neither can behave as if the encounter did not happen.

That is the only operation that returns content in this system.

---

## What This Makes Impossible

- Accessing data without altering it: **impossible**
- Observing without being changed by observation: **impossible**
- Separating data from its interaction history: **impossible**
- Treating data as static: **impossible**

These are not forbidden. They are undefined. The operations do not exist in the system.

---

## The Six Laws

See [`LAWS.md`](./LAWS.md) for precise, code-form definitions of every constraint.

Each law includes:
- The exact forbidden operation
- The required postconditions
- A non-compliance test

---

## The Minimal System

```
Entity state:    { content, witnesses: append-only[], stability: f(witnesses) }
Accessor state:  { identity: persistent, imprints: append-only[] }

One operation:   witness(entity, accessor)
                   → appends to entity.witnesses
                   → appends to accessor.imprints
                   → recalculates entity.stability
                   → returns content + imprint

No other operation returns content. Ever.
```

See [`examples/witnessed-document.md`](./examples/witnessed-document.md) for the smallest real system built on this.

---

## What This Is

A new constraint on interaction — not a philosophy of data.

Primitives are always constraints. UNDO constrained time. CLIPBOARD constrained copy. WITNESS constrains observation.

The constraint is: **observation is never free**.

---

## Repository Map

```
LAWS.md              — six system laws in code-like precision
CONSTRAINTS.md       — compliance tests for each law
primitives/          — formal definitions of each primitive
examples/            — minimal systems where the laws must hold
architecture/        — the assumptions being replaced
log/                 — settled decisions, append-only
```
