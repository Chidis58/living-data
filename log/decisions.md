# Decision Log

This is the permanent record of every settled conceptual decision in the living-data project, in chronological order.

**Rules for this file:**
- Only settled decisions are recorded here — not discussions, not drafts
- Each entry states what was decided and why, concisely
- Entries are never modified after being written — if a decision is reversed, a new entry is added
- This file exists to prevent relitigating settled questions

---

## Decisions

---

### D001 — The foundational problem is the passive-data assumption
**Settled:** Session 1

The bottleneck being addressed is not a missing feature, framework, or tool. It is the passive-data assumption embedded in every computing architecture: data is inert matter, code is the active force. Every innovation in the last 70 years inherits this assumption. The living-data project replaces it.

---

### D002 — WITNESS is the first primitive
**Settled:** Session 1

WITNESS was selected as the first primitive because it requires only one new idea added to something that already exists: observation is not free. It does not require solving existence or belief first. It is the entry point because it is the simplest, not because it is the most important.

---

### D003 — ACCESS = WITNESS (no separate read operation)
**Settled:** Session 1

The early formulation had `read()` and `witness()` as separate operations, with `witness()` as optional. This was rejected. Optionality kills primitives — a behavior that can be skipped will be skipped, and it will never become load-bearing. The correct architecture has no `read()`. Access and witness are the same act. This is enforced by architecture, not by validation.

---

### D004 — The imprint must be externally verifiable
**Settled:** Session 1

An early definition of the imprint (observer-side change) described it as internal awareness — the observer "carries" the encounter. This was rejected. Internal-only awareness collapses WITNESS into a logging system. The imprint must be externally verifiable — other parties must be able to confirm that this observer witnessed this entity in this state. This is what gives the observer attestation capability.

---

### D005 — Deniability is what WITNESS makes impossible
**Settled:** Session 1

The primitive test: "After WITNESS happens, what becomes impossible that was previously possible?" The answer is deniability — the ability of either party to behave as if the encounter never happened. This is not a policy. It is structural. Neither the data nor the observer can return to a pre-encounter state. You cannot un-witness.

---

### D006 — Anonymous access is architecturally impossible, not blocked
**Settled:** Session 1

Anonymous access fails not because it is rejected, but because the operation is undefined. WITNESS requires writing an imprint to the accessor's state. An anonymous accessor has no persistent state. The operation cannot complete — like attempting to COPY with no clipboard. This is an architectural property of WITNESS, not an access control decision.

---

### D007 — Stability is a behavioral modifier, not a log field
**Settled:** Session 1

The witness record on a data entity is not a log or a view count. It is a behavioral modifier. The entity's capability state changes as a function of its witness history. `sovereign`, `forming`, `settling`, `settled` are behavioral states — they change what the entity can do, not just what it records about itself.

---

### D008 — Knowledge systems is the recommended first implementation domain
**Settled:** Session 1

From the candidate domains evaluated, knowledge systems (internal wikis, documentation) scored highest on: recognizable pain, existing identity infrastructure, visible consequence, and meaningful degradation when WITNESS is removed. The first implementation should be a single document type where reading a document is structurally a witness event.

---

### D009 — The repo name is living-data
**Settled:** Session 1

`witness-primitive` was too narrow. `new-computing-model` was too vague. `living-data` names the territory being built toward — data as organism rather than matter — while remaining precise enough to be a project name. WITNESS is the first law inside living-data, not the whole of it.

---

*New decisions are appended below as they are settled.*
