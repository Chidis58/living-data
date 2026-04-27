# living-data

> "No system state exists without grounded interaction."

A **Reality Ingestion and Alignment Engine** — a system that continuously captures real-world human conditions through interaction, aggregates them, contrasts them across regions and time, and makes them visible to the people and systems that need to act on them.

This is not a philosophy project. It is a system specification.

---

## What This System Does

Every second, somewhere in the world, a condition exists that no system knows about.

A hospital running on a backup generator for 11 days. A school at 180% capacity that the district database lists at 60% enrollment. A farmer planting on a forecast built from data 14 months out of date.

These conditions are invisible — not because they aren't real, but because no system was designed to continuously receive lived experience as input.

This system is designed exactly for that.

---

## Core Loop — What Happens When Someone Opens This System

```
1. A real-world condition exists
       ↓
2. A human or sensor interacts with it
       ↓
3. That interaction is recorded as WITNESS
       (both the condition and the actor are permanently changed)
       ↓
4. The system aggregates witnesses across actors, regions, time
       ↓
5. The system contrasts — compares regions, ISPs, hospitals, schools
       ↓
6. The result is made visible — map, score, trend, alert
       ↓
7. Users and decision-makers update their understanding
       ↓
8. Reality improves — or the gap is at least visible
       ↓
       └──────────────────────────────→ back to step 1
```

Nothing in this system runs without step 3. No system state exists without grounded interaction.

---

## WITNESS — The Unit of Reality

WITNESS is not a concept. It is a callable mechanism. It is the only way reality enters this system.

```typescript
witness({
  actor_id:    string,      // persistent identity — anonymous actors are undefined
  domain:      string,      // "internet" | "power" | "health" | "education" | ...
  signal_type: string,      // "passive" | "active" | "sensor"
  value:       any,         // the measured or confirmed condition
  location:    string,      // GPS-obfuscated region identifier
  timestamp:   number,      // unix ms
  confidence:  0.0–1.0      // cross-validation weight
})
→ {
  witness_id:     string,   // irrevocable record
  actor_imprint:  object,   // permanent change to actor's state
  domain_state:   object,   // updated domain state for this region
  stability:      string    // "sovereign" | "forming" | "settling" | "settled"
}
```

**What WITNESS is not:** logging, analytics, a view counter, a transaction record.

**What WITNESS is:** the point where experience becomes system state — permanently, irrevocably, for both the actor and the entity being witnessed.

### One Concrete Example

```
A user in Abuja opens the system
  → speed test runs automatically (passive signal)
  → latency: 120ms, packet loss: 4%, throughput: 1.2 Mbps
  → user confirms: "this reflects my actual experience" (active signal)
  → system calls witness({
        actor_id: "usr_abc123",
        domain: "internet",
        signal_type: "active",
        value: { latency: 120, packet_loss: 4, throughput: 1.2 },
        location: "NG-FC-ABJ-03",
        timestamp: 1714210800000,
        confidence: 0.9
      })
  → witness_id recorded — irrevocable
  → actor carries imprint: "I witnessed internet conditions in ABJ-03 at this state"
  → regional internet state updates
  → Abuja's value score recalculates
  → map reflects new state
```

That is the entire loop in one interaction. One person. One moment. Reality entered the system.

---

## Domain Model — How This Scales Without Overreaching

This system does not solve everything at once. It operates through **domains** — independent slices of reality, each with its own witness schema, aggregation rules, and contrast dimensions.

Each domain plugs into the same core loop. The primitives (WITNESS, CONTRAST, RECALIBRATION) are the engine. The domains are what the engine runs on.

| Domain | What It Measures | Key Witness Signal |
|---|---|---|
| Internet Value | Speed, cost, real usability | Speed test + user confirmation |
| Power Stability | Uptime, outage duration, reliability | Outage report + duration confirmation |
| Healthcare Access | Availability, wait times, supply | Appointment outcome + resource flag |
| Education Conditions | Enrollment vs. capacity, materials | Teacher or student confirmation |
| Cost of Living | Basket price vs. income | Price report + purchase confirmation |

**First domain in implementation:** Internet Value Index.

Adding a new domain requires:
1. Define the witness schema for that domain
2. Define the aggregation rules (how witnesses combine into a regional score)
3. Define the contrast dimensions (what to compare against)
4. Define the representation (what users see)

No changes to the core engine.

---

## System Architecture

```
┌─────────────────────────────────────────────────┐
│                  REAL WORLD                             │
│  (internet · power · health · food · education)         │
└──────────────────────┬──────────────────────────┘
                       │
                       ▼
             ┌─────────────────┐
             │     HUMAN          │
             │  lived experience. │
             └────────┬────────┘
                        │
       ┌──────────────┼──────────────┐
       ▼              ▼              ▼
  [passive]     [confirmed]     [sensor]
  device data   experience      system measure
       └──────────────┼──────────────┘
                      │
                      ▼
       ┌──────────────────────────────┐
       │         WITNESS LAYER         │
       │  witness(actor, domain, ...)  │
       │  both parties permanently     │
       │  changed · no neutral access  │
       └──────────────┬───────────────┘
                      │
                      ▼
       ┌──────────────────────────────┐
       │          AGGREGATION          │
       │  region · time · confidence   │
       └──────────────┬───────────────┘
                      │
                      ▼
       ┌──────────────────────────────┐
       │           CONTRAST            │
       │  region vs region · ISP vs   │
       │  ISP · today vs last month   │
       └──────────────┬───────────────┘
                      │
                      ▼
       ┌──────────────────────────────┐
       │        REPRESENTATION         │
       │  map · score · trend · alert  │
       └──────────────┬───────────────┘
                      │
                      ▼
             ┌─────────────────┐
             │     HUMAN        │
             │  perception      │
             └────────┬─────────┘
                      │
                      ▼
       ┌──────────────────────────────┐
       │        RECALIBRATION          │
       │  decisions grounded in        │
       │  current witnessed reality    │
       └──────────────────────────────┘
                      │
                      └─────────────────→ back to real world
```

---

## The Three Primitives

### WITNESS `status: SETTLED`
The only operation that returns system state. Calling it permanently changes both the entity and the actor. There is no read-only mode.

### CONTRAST `status: DRAFT`
A comparison operation across regions, systems, or time. A condition has no meaning without something to compare it against. Nigeria vs. Kenya. ISP A vs. ISP B. This week vs. last month.

### RECALIBRATION `status: DRAFT`
The structural update of interpretation when new witnessed conditions arrive. Not a manual refresh — a consequence of accumulated witness state crossing a threshold.

---

## System Laws — What Is Impossible Here

```
LAW 1: read(entity) → content          — UNDEFINED. No neutral access.
LAW 2: witness(entity, anonymous)      — UNDEFINED. No persistent state to write to.
LAW 3: witnesses.delete(record)        — UNDEFINED. Append-only. Forever.
LAW 4: entity.behavior == initial      — INVALID. State must respond to witness history.
        after 100 witnesses
LAW 5: no RelationshipObject after     — INVALID. Encounter produces first-class object.
        first encounter
LAW 6: contradiction.isVisible == false — INVALID. Contradictions are always visible.
```

See [`LAWS.md`](./LAWS.md) for precise code-form definitions and non-compliance tests.

---

## What Currently Exists

| File | Status | What it contains |
|---|---|---|
| `LAWS.md` | Complete | Six system laws with compliance tests |
| `primitives/WITNESS.md` | Settled | Full definition, anatomy, failure cases |
| `primitives/ACKNOWLEDGE.md` | Draft | Derived from WITNESS |
| `implementation/witness-spec.md` | Draft | TypeScript spec, state machine |
| `implementation/domain-candidates.md` | Draft | Four domains ranked for first build |
| `examples/witnessed-document-app/` | Running | Minimal system — all 6 laws enforced |
| `architecture/assumptions-broken.md` | Complete | Five broken assumptions of current architecture |
| `log/decisions.md` | Live | Settled decisions, append-only |

---

## What Gets Built Next

**Phase 1 — Internet Value Index (current)**
One domain. One running witness loop. Real data. Real users. Real regional scores.

**Phase 2 — Power Stability + Cost of Living**
Two domains plugged into the same engine. Witness schema differs. Core loop identical.

**Phase 3 — Composite Human Outcome Index**
Cross-domain aggregation. A region's overall condition score built from multiple witnessed domains.

---

## For Builders

If you want to contribute, the entry point is clear:

1. Read [`LAWS.md`](./LAWS.md) — understand what the system cannot do
2. Read [`primitives/WITNESS.md`](./primitives/WITNESS.md) — understand the only access operation
3. Run [`examples/witnessed-document-app/`](./examples/witnessed-document-app/) — see all six laws running
4. Read [`implementation/domain-candidates.md`](./implementation/domain-candidates.md) — pick where to build

The first function you write should be `witness()`. Everything else is built on top of it.
