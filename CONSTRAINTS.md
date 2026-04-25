# Interaction Laws

These are the constraints that define living-data systems. They are not guidelines. They are not best practices. They are laws — violating them produces a system that is no longer a living-data system, just a system with extra logging.

---

## Law 1: No Neutral Access

> In a living-data system, there is no operation that returns data without changing both the data and the accessor.

**What this eliminates:** `GET`, `read()`, `fetch()`, `load()`, `query()` as neutral operations. Any operation that returns entity content must be a witness operation.

**How to test compliance:** Can a developer access entity content without triggering a state change on both entity and accessor? If yes — Law 1 is violated.

---

## Law 2: No Anonymous Participation

> An accessor without persistent identity cannot participate in a living-data system. Anonymous access is not forbidden — it is undefined.

**What this eliminates:** Guest modes, preview modes, public read access without identity. These are not blocked — they are outside the system boundary. A system that has anonymous access is not a living-data system for those accessors.

**How to test compliance:** Can entity content be accessed without writing an imprint to a persistent accessor state? If yes — Law 2 is violated.

---

## Law 3: Irrevocable Records

> Witness records on entities and imprints on accessors are append-only and permanent. No operation exists to delete or modify them.

**What this eliminates:** "Delete my history," "clear read receipts," admin log purges. These operations are undefined — not restricted, undefined. A system that allows deletion of witness records is not a living-data system.

**How to test compliance:** Can any actor — user, admin, system — remove or modify a witness record or imprint? If yes — Law 3 is violated.

---

## Law 4: Behavioral Consequence Is Mandatory

> Entity behavior must change as a function of witness history. A system where witness records exist but affect nothing is a logging system — not a living-data system.

**What this eliminates:** Witness records as pure audit trails with no behavioral consequence. The records must change what the entity does.

**How to test compliance:** Is there any observable behavioral difference between an entity with 0 witnesses and the same entity with 100 witnesses? If no — Law 4 is violated.

---

## Law 5: Relationships Are First-Class

> When two entities encounter each other through WITNESS, a RelationshipObject is created. This object has its own state, separate from either party, and governs future interactions between them.

**What this eliminates:** Treating witness history as a flat list. The encounter between entity A and accessor B is a first-class object — not a record in a table, but an entity in its own right.

**How to test compliance:** Does the system have a distinct, addressable object representing the relationship between a specific entity and a specific accessor? If no — Law 5 is violated.

---

## Law 6: Contradiction Is Visible

> When an accessor acts in a way that contradicts their witnessed state, this contradiction is structurally visible. It is not an error. It is not blocked. It is visible.

**What this eliminates:** The ability to quietly act against what one has witnessed. The contradiction must be surfaced — not as a warning, but as a visible property of the action.

**How to test compliance:** Can an accessor edit an entity in a way that directly contradicts what they witnessed, with no structural indication of the contradiction? If yes — Law 6 is violated.

---

## Compliance Summary

A system is a living-data system if and only if all six laws hold simultaneously.

| Law | Tests As |
|---|---|
| No Neutral Access | `witness()` is the only access path |
| No Anonymous Participation | Content unreachable without persistent identity |
| Irrevocable Records | No delete or modify operation exists for witness records |
| Behavioral Consequence | Entity behavior differs based on witness history |
| Relationships First-Class | RelationshipObject exists and is addressable |
| Contradiction Visible | Contradictory actions are structurally marked |

Partial compliance is not living-data. A system that satisfies 5 of 6 laws is a sophisticated conventional system with some novel features. All 6 laws together produce something that did not exist before.
