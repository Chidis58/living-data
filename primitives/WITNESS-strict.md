# WITNESS — Strict Definition

**Status: SETTLED**

---

## 10-Line System Definition

```
1. WITNESS is the only operation that accesses a data entity. READ does not exist.

2. WITNESS requires a persistent accessor identity. Anonymous access is undefined.

3. WITNESS appends an irrevocable record to the entity. Records are append-only.

4. WITNESS writes an imprint to the accessor's state. The imprint cannot be removed.

5. The entity's behavior changes as a function of its witness history.

6. The accessor's capabilities change as a function of what it has witnessed.

7. A return encounter between the same entity and accessor is structurally distinct
   from a first encounter.

8. The entity and accessor share a RelationshipObject after first contact.
   This object has its own state, separate from either party.

9. Neither party can act in a way that contradicts their witnessed state
   without that contradiction being structurally visible.

10. Removing WITNESS from a system eliminates lines 3–9.
    What remains is a logging system. That already exists.
```

---

## Mechanical Specification

### Function Signature

```typescript
function witness(
  entity: LivingDataEntity,
  accessor: PersistentIdentity
): WitnessExchange

// WitnessExchange is:
{
  content: EntityContent,          // what the accessor receives
  imprint: Imprint,                // permanently written to accessor state
  entityState: EntityState,        // entity after the encounter
  relationship: RelationshipObject // created or updated
}
```

### What Must Exist Before WITNESS Can Run

```typescript
accessor.identity          // must be persistent and non-anonymous
accessor.currentState      // captured at moment of encounter
entity.content             // what is being witnessed
entity.witnesses           // existing record — may be empty
```

### What Must Exist After WITNESS Runs

```typescript
// On the entity:
entity.witnesses.length === prior.witnesses.length + 1   // always
entity.stability            // recalculated — cannot be same if first witness
entity.witnesses.last()     // append-only, cannot be modified or deleted

// On the accessor:
accessor.imprints.includes(thisEncounter)   // permanently
accessor.canAttest(entity, contentState)    // new capability, cannot be revoked

// In the system:
RelationshipObject(entity.id, accessor.id)  // exists now, did not before (first encounter)
```

### What Cannot Happen

```typescript
// These are not errors. They are undefined operations.
// Attempting them is like dividing by zero — the operation has no result.

read(entity)                         // undefined — READ does not exist
witness(entity, anonymousAccessor)   // undefined — no persistent state to write imprint
entity.witnesses.delete(record)      // undefined — append-only
accessor.imprints.remove(imprint)    // undefined — permanent
```

---

## State Machine: Entity Stability

```
           0 witnesses          1–3 witnesses
[ SOVEREIGN ] ──────────────→ [ FORMING ]
      ↑                              │
      │                    4–12 witnesses
      │                              ↓
      │                        [ SETTLING ]
      │                              │
      │                       13+ witnesses
      │                              ↓
      └──────────────────────── [ SETTLED ]

Transitions:
- SOVEREIGN → FORMING: first witness. Entity is no longer isolated.
- FORMING → SETTLING: enough witnesses that the entity's form is emerging.
- SETTLING → SETTLED: entity's identity now includes its witness history.

Behavioral consequence per state:
- SOVEREIGN:  unrestricted modification, signals isolation to creator/steward
- FORMING:    modifications flagged against witnessed state
- SETTLING:   high friction for contradictory edits
- SETTLED:    entity resists change; witness history is part of its identity
```

---

## Failure Case: What Happens If WITNESS Is Removed

The failure case is precise. This is not hypothetical — it describes every existing system.

| WITNESS removed | What the system becomes |
|---|---|
| Line 3 removed (no record on entity) | View counter. Exists everywhere. |
| Line 4 removed (no imprint on accessor) | Session tracking. Exists everywhere. |
| Line 5 removed (no behavioral change on entity) | Analytics. Exists everywhere. |
| Line 6 removed (no capability change on accessor) | Read receipts. Exists everywhere. |
| Line 7 removed (return encounters are identical) | Stateless API. Exists everywhere. |
| Line 8 removed (no RelationshipObject) | Foreign key. Exists everywhere. |
| Line 9 removed (contradictions invisible) | Optimistic concurrency. Exists everywhere. |
| All removed | `GET /resource`. HTTP. Exists everywhere. |

Each line of the definition maps to something that exists. All of them together — mandatory, unskippable, structurally enforced — is what does not exist yet.

---

## Constraint Enforcement: How Bypass Is Prevented

The most common implementation question: *can someone fake witnessing, or read without it?*

**Answer: not through policy, through structure.**

The access path to entity content runs through `witness()`. There is no other path. This is not middleware. This is not a wrapper. The content field of a LivingDataEntity is not publicly accessible. The only method that returns content is `witness()` — and `witness()` requires a persistent accessor identity before it runs.

```typescript
class LivingDataEntity {
  private content: EntityContent  // not accessible directly. ever.

  public witness(accessor: PersistentIdentity): WitnessExchange {
    // accessor identity verified here — not by auth system, by structure
    // if accessor has no persistent state → operation is undefined
    // imprint written before content returned
    // no path exists that returns content before imprint is written
    return { content: this.content, imprint, entityState, relationship }
  }

  // no get content()
  // no read()
  // no peek()
  // no toString() that exposes content
}
```

If a developer circumvents this by accessing the raw data store directly — they have left the living-data system. They are using a different system that happens to share storage. This is equivalent to editing a Git repo by directly modifying the object store — technically possible, structurally outside the system's guarantees.
