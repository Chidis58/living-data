# living-data

**A system where data is permanently changed by interaction — and so is the thing that interacted with it.**

This is not a framework. Not a library. Not a product.

It is a set of **interaction laws** for data systems — laws strict enough that violating them collapses the system into something that already exists.

---

## The One Thing This Changes

In every existing system:

```
read(data) → output
// data is unchanged. reader is unchanged. nothing happened.
```

In this system:

```
witness(data, accessor) → { content, imprint, newEntityState }
// data is changed. accessor is changed. encounter is irrevocable.
```

There is no `read()`. It does not exist.

---

## First Primitive: WITNESS

| Property | Value |
|---|---|
| **Object** | Any data entity |
| **Operation** | `witness(entity, accessor)` |
| **Precondition** | Accessor must have persistent identity. Anonymous access is undefined — not blocked, undefined. |
| **State change — entity** | Witness record appended. Stability state recalculates. Future behavior changes. |
| **State change — accessor** | Imprint written. Attestation capability granted. Obligation recorded. |
| **Irreversibility** | Neither party can return to pre-encounter state. Records are append-only. |
| **Constraint** | `witness()` is the only access path. There is no bypass. |

**What becomes impossible after WITNESS:** Deniability. Neither party can structurally behave as if the encounter did not happen.

**What breaks if WITNESS is removed:** Attestation collapses. Stability collapses. The system becomes a logging system with no behavioral consequence — which is every system that already exists.

---

## Minimal Example

See [`examples/witnessed-document.md`](./examples/witnessed-document.md) — the smallest possible system where WITNESS must exist.

---

## Repository Map

```
primitives/     — formal definitions of each interaction law
architecture/   — the assumptions being replaced
implementation/ — specs and domain candidates for building
examples/       — minimal systems demonstrating each primitive
log/            — settled decisions, append-only
```

---

## Status

One primitive defined and settled: **WITNESS**

Everything else is under construction. Nothing is added to `primitives/` until it passes the primitive test:

> What becomes impossible that was previously possible?

If that question cannot be answered precisely, it is not a primitive.
