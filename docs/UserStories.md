---
doc_type: user_stories
version: "1.0"
last_updated: "2026-10-15"
cross_references:
  - purpose: current
    repository: https://gitlab.com/smart-assets.io/gitlab-profile
    checkout: ../../../SA/top-level-gitlab-profile
    revision: master
    path: docs/common/user-stories-standard.md
    url: https://gitlab.com/smart-assets.io/gitlab-profile/-/blob/master/docs/common/user-stories-standard.md
---

# User Stories

This document captures user stories that drive feature development. The frontmatter records the User Stories Standard.

**Document Structure**
- Active stories: This file (`docs/UserStories.md`)
- Implementation tracking: [ToDos.md](ToDos.md)
- Completed work: [CompletedTasks.md](CompletedTasks.md)

**Format:** Each story follows the standard template:
> As a [persona], I want [capability] so that [benefit].

---

## Completed Stories

None yet.

---

## Planned Stories

#### US-001: Get Test Tokens on a Selected Shard

> As a **developer on F1r3fly**, I want **test tokens for my vault address on a shard that I select** so that **I can pay phlo for my deploys**.

**Implemented in:** EPIC-001, EPIC-002, EPIC-004, EPIC-009

**Acceptance Criteria:**
- [ ] I can select a test net and a shard and enter a vault address
- [ ] The faucet refuses an address with a bad checksum before it sends a deploy
- [ ] The tokens arrive and the claim shows finalized

**Completed:** Planned

#### US-002: Fund a SATCHEL Wallet

> As a **SATCHEL wallet user on the RGB test net**, I want **to fund my wallet from the wallet app** so that **I can deploy contracts and issue RGB assets without a manual transfer**.

**Implemented in:** EPIC-011

**Acceptance Criteria:**
- [ ] The wallet opens the faucet with my network and address already entered
- [ ] I can prove that I own the address and get a higher limit
- [ ] The address that the faucet derives from my public key is the same as the address in my wallet

**Completed:** Planned

#### US-003: See the Test Nets and Their Status

> As a **visitor or partner**, I want **to see each test net, its consensus model, its shards, and their status** so that **I know where to connect and what to expect**.

**Implemented in:** EPIC-006

**Acceptance Criteria:**
- [ ] Each test net shows its consensus model and shards
- [ ] Each shard shows its status (active, retiring, retired) and its observer endpoints
- [ ] A shard that is out of faucet funds shows that state

**Completed:** Planned

#### US-004: Protect Faucet Funds from Abuse

> As a **test net operator**, I want **rate limits, human verification, and balance ceilings on claims** so that **scripts cannot drain the faucet**.

**Implemented in:** EPIC-005

**Acceptance Criteria:**
- [ ] A recipient over the balance ceiling cannot claim
- [ ] Limits apply for each IP address, each address, and each network
- [ ] Claims stop when the faucet balance is below its floor

**Completed:** Planned

#### US-005: Monitor the Faucet

> As a **test net operator**, I want **metrics and alerts for claims and faucet balances** so that **I can refill or fix the faucet before users see a failure**.

**Implemented in:** EPIC-008

**Acceptance Criteria:**
- [ ] Metrics show claims by state and network, and the faucet balance
- [ ] An alert fires when a faucet balance is below its floor
- [ ] Readiness fails when no node of a network answers

**Completed:** Planned

#### US-006: Add a Shard or a Test Net Without a Code Change

> As a **test net operator**, I want **to add, retire, or remove a shard through the network registry** so that **a new shard after an incompatible release does not need a faucet release**.

**Implemented in:** EPIC-003, EPIC-009

**Acceptance Criteria:**
- [ ] A new registry entry adds a shard to the website and the API
- [ ] A retired shard stays visible but accepts no claims
- [ ] The faucet reads the shard ID and token metadata from the node

**Completed:** Planned

#### US-007: Track a Claim to Finality

> As a **developer**, I want **to see my claim move from accepted to finalized** so that **I know when I can use the tokens**.

**Implemented in:** EPIC-004, EPIC-006

**Acceptance Criteria:**
- [ ] The claim page shows each state until a final state
- [ ] I can reload or share the claim URL
- [ ] An expired deploy is sent again one time without a new claim

**Completed:** Planned

#### US-008: Get Funds on Test Nets of Other Consensus Models

> As a **developer on Casanova, Cordial Miners, or RGB**, I want **the same faucet for the test net of my model** so that **I do not need a different tool for each model**.

**Implemented in:** EPIC-010

**Acceptance Criteria:**
- [ ] The faucet lists the test net of each model that has a running shard
- [ ] A claim on each model reaches its final state
- [ ] The RGB test net dispenses the assets that its design record requires

**Completed:** Planned

#### US-009: Fund an f1r3wallet or ASI Chain Wallet

> As a **user of f1r3wallet or the ASI Chain wallet**, I want **to paste the address that my wallet shows, or open the faucet from my wallet** so that **I get test tokens without a conversion step**.

**Implemented in:** EPIC-007

**Acceptance Criteria:**
- [ ] The faucet accepts the vault address, the ETH address, or the public key that my wallet shows
- [ ] A link from my wallet opens the faucet with my network and address already entered
- [ ] The network names on the faucet match the names in my wallet

**Completed:** Planned

#### US-010: Get Higher Limits as a Partner

> As a **partner or customer of F1r3fly**, I want **higher claim limits with an API key** so that **my team can test the shards without the public limits**.

**Implemented in:** EPIC-005

**Acceptance Criteria:**
- [ ] An operator can issue and revoke my key
- [ ] Claims with my key use the partner limits

**Completed:** Planned

---

## Story Template

Use this template when adding new user stories:

```markdown
#### US-XXX: [Short Title]

> As a **[persona]**, I want **[capability]** so that **[benefit]**.

**Implemented in:** [EPIC-ID or "Planned"]

**Acceptance Criteria:**
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

**Completed:** [Date or "Planned"]
```

---

## Relationship to Epics

User stories capture the **why** (user need and benefit). Epics capture the **what** (technical implementation tasks).

| Artifact | Purpose | Location |
|----------|---------|----------|
| User Story | Business/user need | `docs/UserStories.md` |
| Epic | Implementation scope | `docs/ToDos.md` |
| Task | Technical work item | Nested in epic YAML |
| Acceptance Criteria | Definition of done | In user story |
