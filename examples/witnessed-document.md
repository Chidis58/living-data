# Minimal System: Witnessed Document

**Purpose:** The smallest possible system where WITNESS must exist — and where removing it produces a system that is recognizably worse in a way users feel without being told why.

This is not a full application. It is a mental model made concrete enough to implement.

---

## The System in One Paragraph

A document system where opening a document is a witness event. The document knows who has seen it, in what state, and when. Readers carry an imprint — a structural record that they witnessed this document in this specific state. The document's behavior changes based on its witness history. Removing any of these properties returns the system to Notion, Confluence, or Google Docs — which already exist.

---

## The Rules (complete — nothing omitted)

```
Rule 1: A document cannot be opened without a persistent user identity.
        Anonymous access is undefined. Guest mode does not exist.

Rule 2: Opening a document = witnessing it.
        There is no "preview". There is no "peek". Open = witness.

Rule 3: Every witness appends an irrevocable record to the document.
        Records cannot be deleted. Not by the user. Not by the admin.

Rule 4: Every witness writes an imprint to the user's account.
        The imprint states: "I witnessed document X in state Y at time Z."
        This imprint cannot be removed.

Rule 5: The document's stability state is a function of its witness count.
        0 witnesses   → SOVEREIGN  (glows differently — signals isolation)
        1–3 witnesses → FORMING    (edit friction begins)
        4–12 witnesses→ SETTLING   (contradictory edits flagged)
        13+ witnesses → SETTLED    (witness history shown as part of identity)

Rule 6: A user who has witnessed a document can attest to its state.
        Attestation is structural — not a claim, not a button — a verifiable
        property of their account state.

Rule 7: A user cannot act in a way that contradicts what they witnessed
        without the contradiction being visible.
        If they edit a document in a way that contradicts their witnessed state,
        the system marks this — not as an error, but as a visible tension.
```

---

## What It Looks Like

### Document A — never opened

```
Title: "Q3 Strategy Draft"
Stability: SOVEREIGN
Witnesses: 0
Visual indicator: dim border, isolation signal visible to creator
Behavior: fully editable, no friction, signals "no one has seen this"
```

### Document A — after 1 person opens it

```
Title: "Q3 Strategy Draft"
Stability: FORMING
Witnesses: 1 [Sarah Chen | state:v1 | 09:14 Apr 25]
Visual indicator: border changes
Behavior: edits that contradict v1 now carry a flag
Sarah's account: imprint { doc:A, state:v1, time:09:14 } — permanent
```

### Document A — after 14 people open it

```
Title: "Q3 Strategy Draft"
Stability: SETTLED
Witnesses: 14
Visual indicator: settled state visible to all
Behavior: high friction for edits; witness list is part of document identity
Any of the 14 users: can attest "I witnessed this document in state vX"
```

---

## The Failure Case — Shown Concretely

Remove Rule 2 (witness is optional):
→ Users open documents without being witnessed. Nothing changes. This is Google Docs.

Remove Rule 3 (records can be deleted):
→ Admin deletes the witness log. Deniability returns. This is an audit log.

Remove Rule 4 (no imprint on user):
→ Document knows it was seen, but user carries nothing. This is a view counter.

Remove Rule 5 (stability doesn't change):
→ Witness count exists but affects nothing. This is analytics.

Remove Rule 6 (no attestation):
→ Users can claim they read something but cannot prove it structurally. This is the current state of every knowledge system.

Remove Rule 7 (contradictions invisible):
→ Users can act against what they witnessed with no visible consequence. This is every existing editor.

**Remove all rules → you have a document editor. Those already exist.**

---

## What a Developer Must Build

To implement this minimal system, a developer needs to build exactly five things:

**1. Identity gate**
No session begins without a persistent user identity. This is the precondition for all else.

**2. The witness() method on every document**
Returns content. Before returning, appends a WitnessRecord to the document and writes an Imprint to the user. Both operations complete before content is returned. If either fails, access fails.

**3. Stability calculator**
A pure function: `calculateStability(witnesses: WitnessRecord[]) → StabilityState`
Called after every witness operation. Updates the document's visual state.

**4. Imprint store on user accounts**
An append-only record on each user account. Not a history tab. A structural property of the account that other parts of the system can query.

**5. Contradiction detector**
When a user edits a document, compare the edit against the state they witnessed. If the edit contradicts their witnessed state — flag it visibly. Not a block. A visible tension.

---

## What This Minimal System Proves

If you build only these five things — nothing else — you have a system where:

- A document that no one has opened behaves differently from one that many people have read
- A user cannot deny having read a document in a specific state
- An edit that contradicts a user's witnessed knowledge is visible as a contradiction
- Removing any of these five things makes the system worse in a way users will feel

That is the test. That is the proof. That is the smallest version of living-data that is real.
