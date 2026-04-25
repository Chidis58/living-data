
# Primitive: WITNESS

**Status: SETTLED**

---

## Definition

> An interaction in which accessing an entity irreversibly alters both the entity and the accessor — making deniability impossible, neutral observation illegal, and future interactions between them structurally distinct from all other interactions.

---

## What WITNESS Is Not

- **Not logging.** A log is external, optional, and deletable. WITNESS is structural and irreversible.
- **Not view tracking.** Analytics records that access happened. WITNESS changes what is possible after access happens.
- **Not a permission system.** Permissions control who can access. WITNESS is about what access *does* — always, to both parties.
- **Not caching.** A cache stores a copy for performance. An imprint is a permanent change to the observer's state.
- **Not an audit trail.** An audit trail can be ignored. WITNESS cannot — it changes behavior, not just records.

---

## The Core Law

```
ACCESS = WITNESS
```

There is no read without witness. Not as a rule enforced by code — as a property of how access is defined in this system.

This means:
- Anonymous access is **architecturally impossible** — not blocked, not logged, impossible
- Passive observation **does not exist** — every viewer is a participant
- The cost of knowing something is **being known to have known it**

---

## Anatomy: Three Parts

### 1. The Mark (data side)

Not a log entry. A **behavioral modifier**.

The data's capability state changes based on who has witnessed it. The witness list isn't history — it is current operative state.

- Data witnessed by zero entities is in a *sovereign state*: it can change freely, it signals its isolation
- Once witnessed, data begins to **stabilize around its witnessed form**
- It resists changing in ways that would contradict what its witnesses know
- Data witnessed by many entities reaches a *settled state*: high stability, its witness history is part of its identity

### 2. The Imprint (observer side)

Not a memory note. A **capability change**.

After witnessing, the observer gains something they didn't have — or loses something they did.

- An observer who has witnessed data can **attest to its state at that moment** — they carry that authority
- They also carry **obligation**: they cannot act in a way that contradicts what they witnessed without that contradiction being structurally visible
- The imprint is externally verifiable — it is not merely internal awareness

### 3. The Consequence (systemic)

Future interactions between two entities that have witnessed each other are **permanently distinct** from their interactions with any other entity.

- Data responds differently to a return visitor than to a first encounter
- An observer's access to related data is conditioned by what they've already witnessed
- The relationship between data and observer becomes a **first-class object** — it has properties, history, and behavior of its own

---

## What Becomes Impossible After WITNESS

**Deniability.**

Before WITNESS: both parties can behave as if the encounter never happened. The data doesn't know. The observer isn't marked. Access is free.

After WITNESS: neither party can return to a state of non-encounter.

- The data's future behavior is permanently conditioned by who has seen it
- The observer carries a changed state they cannot shed
- Not because a log says so — because their structure is different now

**You cannot un-witness.**

---

## What WITNESS Destroys in Current Architecture

| Current Assumption | What WITNESS Replaces It With |
|---|---|
| Reading is free | Access has permanent cost |
| Observation is neutral | Every observer is a participant |
| State lives in the data | State lives in the *relationship* |
| Logs can be deleted | Encounter is structurally irreversible |
| Anonymous access is possible | Identity is the price of knowing |
| Data and observer are separate | They are permanently altered by contact |

---

## Implementation Path

### Layer 1 — Conceptual (current)
WITNESS is defined as a primitive. Its anatomy is settled. Its consequences are specified.

### Layer 2 — Domain Embedding
Pick one narrow environment — documents, conversations, or knowledge systems — and redesign it with WITNESS as a law, not a feature. No escape hatch.

See [`implementation/domain-candidates.md`](../implementation/domain-candidates.md) for candidates.

### Layer 3 — Behavioral Dependency
Design the system so that removing WITNESS degrades it meaningfully — not just breaks a feature, but removes something users rely on unintentionally.

### Layer 4 — Exportability
Other developers begin to ask: *"I need this behavior too."* That is when WITNESS has become a primitive.

---

## Derived Primitives (not yet defined)

WITNESS is load-bearing. The following primitives are expected to derive from it:

- **ACKNOWLEDGE** — a witness choosing to make their imprint visible to others
- **TRUST** — what accumulates between two entities through repeated witnessing without contradiction
- **AMPLIFY** — the effect of many witnesses on a piece of data's stability and authority
- **CONVERGE** — two witnessed states moving toward shared ground through encounter history

These are named but not yet settled. See [`primitives/`](.) for their status.

---

## Decision Log

| Date | Decision | Reason |
|---|---|---|
| 2025 | `read()` and `witness()` merged into single operation | Optionality kills primitives. ACCESS = WITNESS is a law, not a choice. |
| 2025 | Imprint defined as externally verifiable | Internal-only awareness collapses WITNESS into a logging system. |
| 2025 | Deniability named as the thing that becomes impossible | This is the precise answer to the primitive test: what becomes impossible that was previously possible? |
