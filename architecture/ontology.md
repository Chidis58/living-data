# Ontology: What Living Data Is

This document defines the conceptual model that underlies all primitives in this project. It is the philosophical foundation — not implementation-facing, but structurally necessary.

Every primitive defined in `primitives/` should be derivable from this model.

---

## The Central Claim

Current computing treats data as **matter** — inert substance shaped by external forces.

Living-data treats data as **organism** — an entity with intrinsic properties that persist, orient, and respond independent of external infrastructure.

This is not a metaphor. It is a structural definition with testable consequences.

---

## The Three Intrinsic Properties

A data entity in the living-data model carries three properties that are not assigned, attached, or computed externally. They are native.

### 1. Existence

The capacity to persist through coherence, not location.

Current data exists because something stores it. Living data exists because of what it *is* — its internal relationships, its coherence, its identity. Storage becomes an optimization, not a requirement.

This property underpins: **EXIST** (pending primitive)

### 2. Epistemic State

The capacity to hold belief, doubt, and uncertainty as native conditions — not error states.

Current systems are either certain (value present) or failing (null, error, exception). There is no native model for *holding two conflicting possibilities simultaneously*, for *being committed to something while remaining open to being wrong*, or for *orienting behavior around something not yet confirmed*.

Living data has intrinsic epistemic state. It can:
- **Believe** — hold something as operative truth without continuous verification
- **Doubt** — hold conflicting states without resolving them
- **Hope** — orient current behavior toward a possible future state

These are not fields. They are native behavioral modes.

This property underpins: **BELIEVE**, **DOUBT**, **HOPE** (pending primitives)

### 3. Temporal Orientation

The capacity to carry history and lean toward futures.

Current data is present-tense. It holds its current value. Its history, if kept at all, is external metadata. Its future is entirely determined by external code.

Living data is oriented in time:
- It **remembers** — its history is part of its current value, not separate from it
- It **forgets** — selective, graceful loss of detail while the shape remains
- It **hopes** — it has orientation toward states that don't exist yet, and that orientation shapes its present behavior

This property underpins: **REMEMBER**, **FORGET**, **HOPE** (pending primitives)

---

## The Relationship Model

In current architecture, relationships between data objects are pointers — structural links with no behavior, no history, no state of their own.

In the living-data model, **relationships are first-class entities**.

A relationship between two data objects:
- Has its own state (separate from either object's state)
- Has history (a record of every encounter between the two)
- Has behavior (future interactions between those objects are conditioned by their relationship)

This is the foundation of WITNESS — the first primitive to implement this model. When data is witnessed, the relationship between data and observer becomes a first-class object.

---

## What This Model Produces

When data has existence, epistemic state, temporal orientation, and relational identity:

- An application running without a server is not "offline" — it is **sovereign**
- A file shared without a network hasn't been "transferred" — it has **moved itself**
- A system that hasn't been told something new can still **evolve its understanding** based on what it believes and hopes
- Two systems that have never communicated can reach **shared state** because their data naturally negotiates through encounter history

---

## What This Model Is Not

- Not object-oriented programming (OOP assigns behavior through class definitions — external to the data)
- Not reactive programming (reactive systems respond to change — but the data itself is still passive)
- Not AI / machine learning (ML infers patterns from data — but the data itself has no intrinsic state)
- Not blockchain (blockchain records immutable history externally — WITNESS makes history intrinsic)

---

## Primitive Dependency Map

```
EXIST
  └── enables → BELIEVE, HOPE, REMEMBER

WITNESS (SETTLED)
  └── enables → ACKNOWLEDGE, TRUST, AMPLIFY, CONVERGE
  └── requires → (none — first primitive)

BELIEVE
  └── requires → EXIST
  └── enables → DOUBT, INTEND

HOPE
  └── requires → EXIST, BELIEVE
  └── enables → CONVERGE, NEGOTIATE

REMEMBER / FORGET
  └── requires → EXIST
  └── enables → TRUST, DECAY
```

*This map is updated as primitives are defined and settled.*

---

*This document is the ontological anchor. When a primitive is proposed, test it here: does it arise naturally from existence, epistemic state, or temporal orientation? If not, it may be a feature — not a primitive.*
