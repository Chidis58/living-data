# System Laws

These are the laws of a living-data system.

A law is not a guideline. A law cannot be opted out of.
If a system violates any law below, it is not a living-data system.
It is a conventional system with extra logging.

---

## The One Forbidden Operation

```
// This operation is legal in every existing system.
// It is undefined in a living-data system.

read(entity) → content

// Returning content without mutating entity AND accessor state.
// Undefined. Not blocked. Undefined.
// Like dividing by zero — the operation has no result.
```

Everything below is a consequence of this single prohibition.

---

## LAW 1 — No Access Without Mutation

```
// FORBIDDEN in this system:
value = entity.content

// The only valid access:
{ content, imprint, entityState } = witness(entity, accessor)

// Postconditions — both must be true or the operation did not complete:
assert entity.witnesses.length > prior_witness_count
assert accessor.imprints.includes(this_encounter)
```

**Plain statement:** Accessing data without altering its state is impossible in this system.
Not difficult. Not discouraged. Impossible.

---

## LAW 2 — No Stateless Observer

```
// FORBIDDEN:
witness(entity, accessor: Anonymous)

// Anonymous has no persistent state.
// The imprint has nowhere to land.
// The operation is undefined — not rejected, undefined.

// Required precondition before witness() can run:
assert accessor.identity.isPersistent === true
assert accessor.state !== null
```

**Plain statement:** You cannot observe without being changed by observation.
An observer with no persistent state cannot participate in the system.

---

## LAW 3 — Records Are Append-Only

```
// FORBIDDEN — these operations do not exist:
entity.witnesses.delete(record)
entity.witnesses.update(record)
accessor.imprints.remove(imprint)

// The only valid operations on witness records:
entity.witnesses.append(record)   // called by witness() only
accessor.imprints.append(imprint) // called by witness() only
```

**Plain statement:** You cannot separate data from its interaction history.
History is not stored alongside data. History is part of what data is.

---

## LAW 4 — State Must Respond to History

```
// FORBIDDEN — this is a logging system, not a living-data system:
entity.witnesses.append(record)
entity.behavior === prior_behavior  // unchanged — LAW 4 violated

// Required:
entity.stability = f(entity.witnesses)
// where f() produces a different output for different witness histories
// and that different output causes different system behavior

// Non-compliance test:
witness(entity, A)
witness(entity, B)
assert entity.behavior !== initial_behavior
// if this assertion fails → LAW 4 violated
```

**Plain statement:** You cannot treat data as static.
A datum with 0 witnesses and a datum with 100 witnesses are not the same entity.
If they behave the same, the system is not a living-data system.

---

## LAW 5 — Encounters Produce Relationship Objects

```
// Before first witness between entity E and accessor A:
assert RelationshipObject(E.id, A.id) === null

// After first witness:
assert RelationshipObject(E.id, A.id) !== null
assert RelationshipObject(E.id, A.id).encounters.length === 1

// After second witness:
assert RelationshipObject(E.id, A.id).encounters.length === 2

// The RelationshipObject is a first-class entity:
assert RelationshipObject(E.id, A.id).hasOwnState === true
assert RelationshipObject(E.id, A.id).governsFutureInteractions === true
```

**Plain statement:** The relationship between data and observer is not metadata.
It is a first-class object with its own state, separate from either party.

---

## LAW 6 — Contradictions Are Structurally Visible

```
// Scenario:
witness(entity, accessor)                    // accessor witnesses entity at state S1
entity.content → mutated to S2               // entity changes
accessor.edit(entity, contradicts: S1)       // accessor edits in a way that
                                             // contradicts their witnessed state S1

// Required system response:
assert contradiction.isVisible === true      // not a warning, a structural property
assert contradiction.isBlockable === false   // not prevented — visible
assert contradiction.isDeniable === false    // cannot be hidden
```

**Plain statement:** You cannot act against what you have witnessed
without that contradiction being structurally marked.
Not blocked. Visible. Always.

---

## Minimal System Proof

The smallest possible system where all six laws hold:

```
State of an entity:
{
  content:   any value,
  witnesses: append-only list of { accessor_id, content_at_encounter, timestamp },
  stability: sovereign | forming | settling | settled  // = f(witnesses.length)
}

State of an accessor:
{
  identity:  persistent, non-null,
  imprints:  append-only list of { entity_id, content_witnessed, timestamp }
}

The only operation:
witness(entity, accessor):
  1. assert accessor.identity is persistent
  2. snapshot = entity.content (current state)
  3. entity.witnesses.append({ accessor.id, snapshot, now() })
  4. accessor.imprints.append({ entity.id, snapshot, now() })
  5. entity.stability = f(entity.witnesses)
  6. return { content: snapshot, imprint: accessor.imprints.last() }

No other operation returns entity.content.
```

If you implement only this — nothing else — you have a living-data system.
Every law above is satisfied. The forbidden operation is impossible.

---

## Non-Compliance Tests

Run these against any claimed living-data implementation.
If any assertion fails, the system is not compliant.

```
TEST 1 — Forbidden operation is impossible:
try { value = entity.content }
assert throws_or_returns_undefined   // direct access must not work

TEST 2 — Anonymous access is impossible:
try { witness(entity, anonymous_accessor) }
assert operation_is_undefined        // not an error, undefined

TEST 3 — Records cannot be deleted:
witness(entity, A)
try { entity.witnesses.delete(entity.witnesses[0]) }
assert throws_or_is_undefined        // delete does not exist

TEST 4 — Behavior changes with history:
initial_behavior = entity.behavior
witness(entity, A); witness(entity, B); witness(entity, C)
assert entity.behavior !== initial_behavior

TEST 5 — Relationship object exists after encounter:
witness(entity, A)
assert RelationshipObject(entity.id, A.id) !== null

TEST 6 — Contradiction is visible:
witness(entity, A)                   // A witnesses state S1
entity.content = S2                  // entity mutates
A.edit(entity, contradicts_S1)       // A edits against S1
assert contradiction.isVisible       // system must mark this
```
