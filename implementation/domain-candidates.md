# Domain Candidates: Where WITNESS Gets Embedded First

**Purpose:** Following the primitive adoption path, WITNESS must first be embedded in one narrow environment where it is the *only* way things work — and where removing it makes the system meaningfully worse.

This document ranks candidate domains and specifies what WITNESS would look like in each.

---

## The Selection Criteria

A domain is a strong candidate if:

1. **Access already matters** — the domain has problems around who saw what, when, and what changed as a result
2. **Neutral observation is already painful** — the domain suffers because reads leave no trace
3. **Identity is already present** — users have some form of persistent identity (removing the anonymous access problem)
4. **Consequence is visible** — users can perceive when something changes as a result of witnessing

---

## Candidate 1: Knowledge Systems / Internal Wikis

**Fit score: HIGH**

**The existing pain:**
Knowledge documents are read constantly and changed rarely. Nobody knows who has seen what, whether outdated information has been silently consumed, or whether critical knowledge has been witnessed by the people who need it. Information can be quietly wrong for months.

**What WITNESS adds:**
- Every document knows who has seen it and when
- A document never-witnessed signals its isolation — it surfaces to its creator or steward
- A document witnessed by many becomes more stable — casual edits are flagged against its witness history
- Readers carry an imprint — they can attest "I read version X on date Y" as a structural fact, not a claim
- Knowledge gaps become visible: topics with zero witnesses surface automatically

**What removing WITNESS would break:**
The attestation layer. Knowledge accountability. The difference between "this is documented" and "this is *known*."

**Implementation entry point:**
A document system (Notion, Confluence, internal wiki) where `viewing a document = witnessing it`, and the document's state visibly reflects its witness history.

---

## Candidate 2: Conversation / Messaging Systems

**Fit score: HIGH**

**The existing pain:**
Messages are marked "read" with a checkmark — the shallowest possible acknowledgment. There is no structural difference between someone who read a message and responded thoughtfully, someone who read it and said nothing, and someone who hasn't read it yet. The read receipt is purely informational.

**What WITNESS adds:**
- Reading a message is a witness event — both the message and the reader are structurally changed
- A message witnessed by its recipient cannot be denied ("I never saw that")
- A message that has been witnessed but not acknowledged carries a visible tension — the gap between witnessing and responding is structural, not inferred
- Conversation threads carry their witness history — who knew what, when, is part of the thread's identity

**What removing WITNESS would break:**
Accountability in communication. The structural basis for "you knew." Deniability would return — which is precisely what makes current messaging systems feel low-trust.

**Implementation entry point:**
A messaging layer where opening a message triggers `witness()`, writes an imprint to the reader, and changes the message's stability state — and where the reader's witnessed state is visible to the sender as more than a checkmark.

---

## Candidate 3: Document Collaboration / Creative Work

**Fit score: MEDIUM-HIGH**

**The existing pain:**
Collaborative documents track changes and comments, but not *understanding*. A document can be opened, skimmed, and closed — leaving a co-author with no knowledge of whether their collaborator actually engaged with the content. Version history records what changed, not who genuinely engaged.

**What WITNESS adds:**
- Engagement is structural, not inferred from edit history
- A section of a document that no collaborator has witnessed is flagged — not as unread, but as *unwitnessed*, carrying a different weight
- Witnesses to a section carry authority over its content — their imprint gives them standing to attest
- The document's identity includes its witness history — who shaped it through genuine encounter

**What removing WITNESS would break:**
The difference between having access to a document and having genuinely engaged with it. Collaborative accountability.

**Implementation entry point:**
A writing tool where paragraph-level witnessing is tracked, and the document's witness coverage is visible — showing which sections are settled and which are still sovereign.

---

## Candidate 4: Data Provenance / Research Records

**Fit score: MEDIUM**

**The existing pain:**
Research data is used, cited, and built upon — but the chain of who accessed what, in what state, and what they believed about it at the time, is almost entirely lost. Data reuse is built on trust in metadata, not structural guarantees.

**What WITNESS adds:**
- Every data access is a witness event — creating an irrevocable record of who accessed what in what state
- A dataset that has been witnessed by ten researchers carries different standing than one witnessed by none
- Researchers carry imprints — their attestation of the data's state at the time they used it is structural
- Data that changes after being widely witnessed carries visible tension with its prior witnesses

**What removing WITNESS would break:**
The structural basis for data provenance. The difference between "we cited this dataset" and "we witnessed it in this specific state."

**Implementation entry point:**
A research data platform where dataset access triggers `witness()`, and the dataset's witness history is part of its published record.

---

## Recommended First Domain: **Knowledge Systems**

**Reason:**
- Pain is immediate and recognizable — everyone has experienced the problem of unknown knowledge gaps
- Identity is already present — users are logged in
- Consequence can be made visible without disrupting workflow — witness state sits alongside the document naturally
- The attestation capability (I can prove I read this) has immediate practical value in organizational settings
- Removing WITNESS would return the system to exactly the painful state users already recognize

**First implementation should be:**
A single document type, in a single tool, where reading a document is structurally a witness event — and where the document's witness state is visible to its author and to anyone with access.

---

*This document is updated as domains are tested and eliminated or advanced.*
