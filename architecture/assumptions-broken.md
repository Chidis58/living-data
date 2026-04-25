# Assumptions Broken

This document records every foundational assumption of current computing architecture that the living-data model structurally challenges or replaces.

This is not a critique. It is a precise map of what we are departing from — and why.

---

## The Foundation We Inherited

Every software system ever built rests on three silent assumptions inherited from the earliest computing models. They were never chosen. They were never debated. They arrived with the hardware and stayed.

---

## Assumption 1: Data is Passive

**The current model:**
Data is inert material. It has no behavior, no orientation, no awareness. It exists as a substrate for programs to act upon. Without an external agent reading, writing, or executing it, data does nothing.

**Why this made sense:**
Early computers were sequential instruction-followers. The separation of data (what to process) from code (how to process) was a practical necessity. It made systems predictable, debuggable, and fast.

**What this costs:**
Every meaningful property of data — its relevance, its history, its relationships, its integrity — must be managed *externally*. Applications are, in large part, elaborate systems for managing properties that data cannot hold about itself.

**What living-data replaces it with:**
Data carries behavior as an intrinsic property — not attached by code, not triggered by external agents. Native.

---

## Assumption 2: Data Needs Infrastructure to Exist

**The current model:**
Data persists because something stores it. Remove the storage layer — the disk, the database, the memory address — and data ceases to exist. Its continued existence is entirely dependent on external infrastructure.

**Why this made sense:**
Physical reality: early storage was scarce and expensive. Data had to live somewhere concrete. The infrastructure *was* the existence.

**What this costs:**
Data sovereignty is impossible. Data is always a guest in someone else's infrastructure. It can be deleted, corrupted, or made inaccessible by forces entirely external to its content or meaning.

**What living-data replaces it with:**
Data can persist through internal coherence — a property of what it *is*, not where it's *kept*. The direction of travel: existence as intrinsic, infrastructure as optional enhancement.

---

## Assumption 3: Observation is Neutral

**The current model:**
Reading data leaves both the data and the reader unchanged. A `read()` operation is free. The system before and after a read is identical except for whatever the reader does with the output. Access costs nothing structurally.

**Why this made sense:**
Predictability. Systems that change state on every read are harder to reason about. The stateless read is a simplification that made systems tractable.

**What this costs:**
There is no record of knowing. No structure for witnessing. Accountability, trust, and authentic engagement cannot be primitives — they have to be bolted on as applications, and they can always be stripped away.

**What living-data replaces it with:**
WITNESS — observation as a state-changing act. Every encounter permanently modifies both the data and the observer. There is no neutral read. Deniability is structurally impossible.

---

## Assumption 4: Meaning is External

**The current model:**
Data has no inherent meaning. A sequence of bytes means what the code that reads it says it means. Strip the interpreter, and data is meaningless. The *why* of data — why it was created, what it was meant to convey — is metadata at best, documentation at worst.

**Why this made sense:**
Separation of concerns. Data formats change. Interpretations evolve. Keeping meaning external makes systems more flexible.

**What this costs:**
The *why* is always the first thing lost. Intent cannot be preserved with fidelity. Systems cannot reason about the purpose of data — only its structure.

**What living-data replaces it with:**
INTEND — data carries the purpose for which it was created as an intrinsic property. Not a comment. Not a field. The why is part of the structure itself.

---

## Assumption 5: State Lives in Data, Not Relationships

**The current model:**
State is a property of objects. Relationships between objects are pointers, foreign keys, or references — structural links, not first-class entities with their own state.

**Why this made sense:**
Simplicity. Relational databases made data queryable by normalizing relationships into tables. Objects in memory know their own state. The relationship was the seam, not the substance.

**What this costs:**
The most meaningful things in any system — trust, history, shared context — live in relationships, not objects. Every system that needs to model these has to build elaborate workarounds.

**What living-data replaces it with:**
Relationships as first-class objects with properties, history, and behavior. REIFY — making the connection itself into data. WITNESS begins this: the relationship between data and observer is now operative state.

---

## Summary Table

| Current Assumption | Living-Data Replacement | First Primitive |
|---|---|---|
| Data is passive | Data carries intrinsic behavior | (all primitives) |
| Data needs infrastructure to exist | Data persists through coherence | EXIST (pending) |
| Observation is neutral | Observation is state-changing | WITNESS ✓ |
| Meaning is external | Intent is intrinsic | INTEND (pending) |
| State lives in objects | State lives in relationships | WITNESS ✓ (partial) |

---

*This document grows as new primitives are defined. Every primitive should map to at least one assumption it breaks.*
