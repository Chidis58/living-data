# living-data

**The systems that shape our world — governments, markets, platforms — are making decisions based on signals that are disconnected from how life is actually being lived.**

Not because data doesn't exist. Because data was never designed to carry lived experience.

---

## The Problem

Every digital system ever built rests on one silent assumption:

```
read(data) → output
// data unchanged. reader unchanged. nothing happened.
```

Data is passive. Code acts on it. And that works fine — until you need a system to reflect reality as humans actually live it.

Right now, there is no reliable way for the conditions people experience daily — the power that cuts out, the medicine that isn't available, the road that's impassable — to continuously enter the systems that are supposed to respond to them.

Decisions get made on approximations. Conditions become invisible. Nothing improves because nothing was ever seen.

---

## Three Human Scenarios

These are not edge cases. They are the everyday texture of life for billions of people.

---

### Scenario 1 — The Hospital That Doesn't Know It's Failing

A regional hospital in a mid-sized city has been running on a backup generator for 11 days after the main power supply failed. Nurses manually log equipment failures. Patients are being diverted. Surgeries are being postponed.

None of this appears in any government health system. The infrastructure ministry has no record of an extended outage. The health ministry is tracking bed availability, not operational conditions. The national grid reports show "intermittent disruptions" — which is technically accurate.

The system that could respond to this situation does not know the situation exists.

**What living-data changes:** Every interaction with the hospital's environment — a nurse confirming generator status, a patient experiencing a delayed procedure, a doctor logging equipment unavailability — becomes a witness event. The condition enters the system as lived state, not as a report written three weeks later.

---

### Scenario 2 — The Farmer Who Can't Trust the Forecast

A smallholder farmer in a drought-prone region plants based on seasonal forecast models maintained by a national agricultural service. The models are updated quarterly. The last field survey was 14 months ago.

This season, soil conditions have changed significantly in her sub-region due to upstream water diversion — a change that happened after the last survey. The forecast says conditions are favorable. Her neighbors, farming the same land for decades, know they aren't.

She plants. The crop fails. The forecast was never wrong — it just wasn't connected to current reality.

**What living-data changes:** Real conditions from real farmers — soil readings, water availability observations, local experience — flow continuously into the model as witness events. The forecast and the ground are no longer disconnected. Her neighbors' knowledge becomes system state, not anecdote.

---

### Scenario 3 — The Child Whose School Was Never Counted

A school in a peri-urban neighborhood has been operating at 180% capacity for two years. There are three teachers for nine classes. Children share textbooks. The local education office has the school listed at 60% enrollment — the figure from the last official census, taken before the neighborhood's population doubled after a nearby factory opened.

The district's resource allocation model runs on that census. The school will not receive additional teachers or materials until the next census — scheduled for two years from now.

The system that could fix this doesn't know the problem exists at the scale it exists.

**What living-data changes:** The school's actual conditions — class sizes, resource gaps, teacher-to-student ratios — are witnessed continuously through interaction with the system. Enrollment is not a census figure. It is a living state, updated by every encounter with the school's reality.

---

## The Root Cause

These three scenarios look like different problems. They are the same problem.

**The measurement gap:** What systems record (census numbers, quarterly reports, grid averages) is not what humans experience (the generator running for 11 days, the soil that changed, the classroom that's overflowing today).

**The invisibility gap:** Because experience isn't captured as state, conditions can worsen for months — even years — without appearing in any system that could respond. Invisibility protects the problem.

**The accountability gap:** Because conditions are invisible, they can't be compared. Because they can't be compared, there's no pressure to improve. The cycle continues.

---

## What We Are Building

A system where the act of experiencing a condition *is* the data point.

Not a report about the condition. Not a measurement taken separately from the experience. The encounter itself becomes state.

This requires replacing the passive-read assumption at the root of every current system with a new primitive:

```
witness(entity, accessor) → { content, imprint, entityState }
```

Every access is an exchange. Both parties are permanently changed. The condition and the person who experienced it carry a mutual record of the encounter. Neither can behave as if it did not happen.

---

## System Architecture

```
        ┌──────────────────────────────────────────┐
        │              REAL WORLD                         │
        │   (power, health, food, infrastructure)         │
        └─────────────────┬────────────────────────┘
                          │
                          ▼
                ┌─────────────────┐
                │     HUMAN          │
                │  (experience)      │
                └────────┬────────┘
                           │
         ┌───────────────┼────────────────┐
         ▼               ▼                ▼
  ┌─────────────┐  ┌───────────┐  ┌──────────────┐
  │ Device data   │  │ Confirmed.  │  │ System          │
  │ (passive)     │  │ experience. │  │ sensors         │
  └──────┬──────┘  └─────┬─────┘  └──────┬───────┘
          └───────────────┼────────────────┘
                             │
                             ▼
         ┌───────────────────────────────┐
         │         WITNESS LAYER               │
         │  experience → system state         │
         │  both parties permanently           │
         │  changed. deniability removed.      │
         └──────────────┬────────────────┘
                           │
                           ▼
         ┌───────────────────────────────┐
         │          AGGREGATION                │
         │  region · time · patterns           │
         └──────────────┬────────────────┘
                           │
                           ▼
         ┌───────────────────────────────┐
         │           CONTRAST                  │
         │  compare regions · trends           │
         │  expose what was invisible          │
         └──────────────┬────────────────┘
                           │
                           ▼
         ┌───────────────────────────────┐
         │        REPRESENTATION              │
         │  conditions made visible           │
         │  continuously, not by report       │
         └──────────────┬────────────────┘
                           │
                           ▼
                ┌───────────────┐
                │     HUMAN       │
                │  (perception)   │
                └───────┬───────┘
                         │
                         ▼
         ┌───────────────────────────────┐
         │        RECALIBRATION               │
         │  decisions grounded in             │
         │  current reality                   │
         └───────────────────────────────┘
                        │
                        └─────────────────────→ back to real world
```

---

## The Six System Laws

A system built on living-data is defined by what is **impossible** inside it — not what is encouraged.

```
LAW 1: Accessing data without altering it → undefined
LAW 2: Anonymous participation → undefined
LAW 3: Deleting a witness record → undefined
LAW 4: Data that does not change with its witness history → not a living-data system
LAW 5: A first encounter that produces no relationship object → not a living-data system
LAW 6: A contradiction that is invisible → not a living-data system
```

See [`LAWS.md`](./LAWS.md) for precise, code-form definitions and compliance tests.

---

## Core Primitives

**WITNESS**
The only access operation. Returns content while permanently changing both the entity and the accessor. There is no `read()`. `Status: SETTLED`

**CONTRAST**
A comparison operation across regions, systems, or time. Conditions are only meaningful when placed against other conditions. `Status: DRAFT`

**RECALIBRATION**
Adjustment of understanding based on new witnessed conditions — not a manual update, a structural response to accumulated witness state. `Status: DRAFT`

---

## What Makes This Different

Existing systems record *events*. A transaction happened. A form was submitted. A sensor fired.

This system records *experience as state*. The moment a nurse interacts with a failing generator, that encounter permanently modifies both the system's understanding of that hospital's condition and the nurse's standing as a witness to it. Neither can be undone.

> Blockchain proves something occurred.
> WITNESS captures that the experience was real.

Those are not the same operation.

---

## Repository Map

```
LAWS.md                         — six system laws with compliance tests
MANIFESTO.md                    — the foundational argument
primitives/                     — formal definitions of each primitive
  WITNESS.md                    — settled
  ACKNOWLEDGE.md                — draft
  _template.md                  — structure for future primitives
architecture/
  assumptions-broken.md         — what current architecture gets wrong
  ontology.md                   — the three intrinsic properties of living data
implementation/
  witness-spec.md               — technical specification
  domain-candidates.md          — where to build first
examples/
  witnessed-document-app/       — minimal running system, all 6 laws enforced
log/
  decisions.md                  — settled decisions, append-only
```

---

## Guiding Principle

> What is experienced becomes visible.
> What is visible becomes improvable.
> What is measured becomes what is seen.

The bottleneck has never been data volume. It has been the distance between experience and state.

This project closes that distance.
