# Technical Specification: WITNESS

**Status: DRAFT — awaiting domain embedding**

This document translates the settled WITNESS primitive into implementable terms. It is the bridge between the conceptual definition in `primitives/WITNESS.md` and a working system.

---

## Core Constraint

```
ACCESS = WITNESS
```

There is no separate `read()` operation. Any system implementing WITNESS must treat access and witness as the same act. This is not enforced by validation — it is enforced by architecture. The path to data does not exist without the witness contract.

---

## Data Entity Structure

Every living-data entity exposes the following structure:

```typescript
interface LivingDataEntity {
  // The content — whatever the data holds
  content: unknown;

  // The witness record — behavioral modifier, not a log
  witnesses: WitnessRecord[];

  // Current stability state — a function of witness history
  stability: 'sovereign' | 'forming' | 'settling' | 'settled';

  // The access interface — there is no other way in
  witness(accessor: AccessorIdentity): WitnessExchange;
}

interface WitnessRecord {
  accessor: AccessorIdentity;
  contentStateAtEncounter: unknown;   // snapshot of content at time of witness
  accessorStateAtEncounter: unknown;  // snapshot of accessor's relevant state
  timestamp: number;
  consequenceApplied: boolean;
}

interface WitnessExchange {
  content: unknown;          // what the accessor receives
  imprint: Imprint;          // what the accessor carries away permanently
  entityNewState: EntityState; // how the entity changed
}

interface Imprint {
  entityId: string;
  contentStateWitnessed: unknown;
  timestamp: number;
  attestationCapability: boolean;  // accessor can now attest to this content state
  obligationRecord: ObligationRecord;
}

interface ObligationRecord {
  cannotDenyEncounter: true;  // always true — this is the structural irreversibility
  contradictionVisible: boolean; // if accessor acts against witnessed state, this flags
}
```

---

## Stability States

Stability is not set by an external agent. It is a function of witness count and witness diversity.

| State | Condition | Behavior |
|---|---|---|
| `sovereign` | 0 witnesses | Content is maximally fluid. Entity signals its isolation. Changes are unrestricted. |
| `forming` | 1–3 witnesses | Content is in negotiation with its witnesses. Changes that contradict witnessed state are flagged. |
| `settling` | 4–12 witnesses | Entity resists casual modification. Witness history is visible. |
| `settled` | 13+ witnesses | Entity's identity includes its witness history. High resistance to contradiction. |

*Thresholds are illustrative. Domain embedding will calibrate these.*

---

## The Witness Operation — Step by Step

```
1. Accessor requests access to entity

2. System captures:
   - Accessor identity (cannot be anonymous — access requires identity)
   - Current content state
   - Current accessor state (relevant portion)
   - Timestamp

3. Exchange occurs:
   - Accessor receives content
   - Entity receives WitnessRecord (appended to witnesses[])
   - Accessor receives Imprint (written to accessor's own state)

4. Stability state recalculates

5. Consequence rules evaluate:
   - Does this witness change what the entity can do?
   - Does this witness change what the accessor can do?
   - Does this witness create a new relationship object between entity and accessor?

6. Relationship object is created or updated:
   - First encounter → new RelationshipObject created
   - Return encounter → existing RelationshipObject updated
   - RelationshipObject holds shared history, shared state, behavioral rules for future interactions
```

---

## Anonymous Access: Why It Is Architecturally Impossible

This is frequently the first implementation question. The answer is structural, not policy-based.

WITNESS requires that the imprint is written to the accessor's state. An anonymous accessor has no persistent state to write to. Therefore, an anonymous accessor cannot complete a witness exchange. Therefore, access cannot complete.

This is not a rejection error. It is an incomplete operation — like attempting to COPY with no clipboard. The operation is undefined, not forbidden.

Systems implementing WITNESS must require accessor identity before the access path is available. This is not authentication bolted on — it is a structural prerequisite.

---

## The Relationship Object

The most novel structure in WITNESS implementation. When two entities (data entity + accessor) first witness each other, a RelationshipObject is created.

```typescript
interface RelationshipObject {
  entityId: string;
  accessorId: string;
  encounters: WitnessRecord[];
  sharedState: unknown;           // state that belongs to neither party alone
  behaviorRules: BehaviorRule[];  // how future interactions between these two differ
}
```

**Behavior rules example:**
- On return encounter: entity presents itself with awareness that this accessor has seen it before
- On return encounter: accessor's attestation capability for this entity is updated to current state
- On contradiction: if accessor acts against witnessed state, RelationshipObject flags the contradiction — visibly

---

## What a Domain Implementation Must Provide

A domain (documents, conversations, knowledge systems) implementing WITNESS must:

1. **Define accessor identity** — what constitutes an accessor in this domain
2. **Define relevant accessor state** — what portion of accessor state is captured at witness
3. **Define contradiction** — what constitutes an accessor acting against a witnessed state
4. **Define consequence rules** — what specifically changes in entity behavior based on witness count/identity
5. **Make the RelationshipObject visible** — users must be able to perceive that something changed

The last point is critical: *if the effect is invisible, the primitive dies.*

---

## Anti-Patterns to Avoid

| Anti-pattern | Why it collapses WITNESS |
|---|---|
| Making witness() optional alongside read() | Optionality kills primitives. There is no read. |
| Storing WitnessRecords in a separate log table | Externalized records can be deleted. The mark must be intrinsic. |
| Anonymous access with a generated ID | Generated IDs have no persistent state — the imprint has nowhere to land. |
| Witness without visible consequence | Invisible change is logging. Consequence must be perceptible. |
| Mutable WitnessRecords | The irrevocability of encounter is the structural guarantee. Records are append-only. |

---

## Next Step

Select a domain from `domain-candidates.md` and implement Layer 2 — a system where WITNESS is the *only* access model and removing it degrades the system in a way users notice without being told why.
