---
doc_type: backlog
version: "1.0"
last_updated: 2026-10-15
cross_references:
  - purpose: current
    repository: https://gitlab.com/smart-assets.io/gitlab-profile
    checkout: ../../../SA/top-level-gitlab-profile
    revision: master
    path: docs/common/epic-task-structure.md
    url: https://gitlab.com/smart-assets.io/gitlab-profile/-/blob/master/docs/common/epic-task-structure.md
---

# Backlog

This document captures deferred work, future ideas, and low-priority items that are not ready for active development. The frontmatter records the Epic Task Structure Reference.

**Document Structure**
- Active work: [ToDos.md](ToDos.md)
- User stories: [UserStories.md](UserStories.md)
- Completed work: [CompletedTasks.md](CompletedTasks.md)
- Deferred work: This file (`docs/Backlog.md`)

---

## Backlog Categories

Items are organized by category and rough priority within each category.

---

### Technical Debt

None yet.

---

### Feature Ideas

#### BACKLOG-FI-001: Wallet Connect for Claims

```yaml
---
backlog_id: BACKLOG-FI-001
title: "Claim with a connected wallet instead of a pasted address"
category: feature_idea
priority: p3
added_at: 2026-10-15
reason_deferred: "No browser wallet for F1r3fly has a stable connect protocol yet. SATCHEL integration (EPIC-007) covers the main wallet"
promotion_criteria:
  - "A F1r3fly wallet connect protocol is published"
---
```

#### BACKLOG-FI-002: Claim History for Each Address

```yaml
---
backlog_id: BACKLOG-FI-002
title: "Show the claim history of an address"
category: feature_idea
priority: p3
added_at: 2026-10-15
reason_deferred: "Not needed for the first test net launch"
promotion_criteria:
  - "Users or operators ask for it after v0.3.0"
---
```

---

### Research & Exploration

#### BACKLOG-RE-001: Report ASI Faucet Gaps Upstream

```yaml
---
backlog_id: BACKLOG-RE-001
title: "Report the ASI faucet gaps to the ASI maintainers"
category: research
priority: p2
added_at: 2026-10-15
reason_deferred: "Waits for design question Q11"
promotion_criteria:
  - "A maintainer approves contact with the ASI maintainers"
---
```

**Description:** Section 2.2 of [designs/faucet-architecture.md](designs/faucet-architecture.md) lists gaps in the ASI faucet at commit `2b333b4`. Two of them have a security effect: the balance ceiling unit error, and the private key in debug logs.

#### BACKLOG-RE-002: Contract Wallet Support

```yaml
---
backlog_id: BACKLOG-RE-002
title: "Fund contract wallets such as MultiSigSystemVault"
category: research
priority: p3
added_at: 2026-10-15
reason_deferred: "No SATCHEL repository uses a contract wallet today (design question Q1)"
promotion_criteria:
  - "SATCHEL or another wallet adopts a contract wallet on F1r3fly"
---
```

---

### Dependencies & Blockers

#### BACKLOG-BE-002: Cosmos Addresses Through the ASI Bridge

```yaml
---
backlog_id: BACKLOG-BE-002
title: "Analyze the ASI bridge and decide whether the faucet accepts Cosmos addresses"
category: blocked_external
priority: p3
added_at: 2026-10-15
reason_deferred: "The ASI Chain bridge maps addresses, but it is not public. The maintainer will get access first (design question Q15)"
promotion_criteria:
  - "The maintainer has access to the ASI bridge and completes the analysis"
---
```

**Description:** The ASI Alliance projects are on [GitHub](https://github.com/asi-alliance). The ASI Chain wallet code shows only vault and ETH addresses. Cosmos address mapping happens in the ASI bridge.

**When Unblocked:** Add a task to EPIC-007 if the faucet must accept Cosmos addresses.

#### BACKLOG-BE-001: Neutral Client Endpoints

```yaml
---
backlog_id: BACKLOG-BE-001
title: "Wait for the neutral client endpoints of f1r3node-rust TASK-025-5"
category: blocked_external
priority: p2
added_at: 2026-10-15
reason_deferred: "The endpoints are not defined yet. PR #627 is open"
promotion_criteria:
  - "TASK-025-5 merges to f1r3node-rust dev"
---
```

**Description:** EPIC-010 needs these endpoints for the Casanova and Cordial Miners adapters.

**When Unblocked:** Start TASK-010-1.

---

## Backlog Template

Use this template when adding new backlog items:

```yaml
---
backlog_id: BACKLOG-XX-XXX
title: "Short descriptive title"
category: technical_debt | feature_idea | research | blocked_external
priority: p3
added_at: YYYY-MM-DD
reason_deferred: "Why this isn't active yet"
promotion_criteria:
  - "Condition that would make this active"
---
```

---

## Promoting Items to Active Work

When a backlog item is ready for active development:

1. Create an epic in `docs/ToDos.md` based on the backlog item
2. Create or link a user story in `docs/UserStories.md` if needed
3. Remove the item from this backlog (or mark as `promoted: true`)
4. Add a note referencing the original backlog ID
