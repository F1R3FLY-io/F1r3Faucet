---
doc_type: todos
version: "1.0"
last_updated: 2026-10-15
mr_status:
  ready: false
  target_branch: main
cross_references:
  - purpose: current
    repository: https://gitlab.com/smart-assets.io/gitlab-profile
    checkout: ../../../SA/top-level-gitlab-profile
    revision: master
    path: docs/common/epic-task-structure.md
    url: https://gitlab.com/smart-assets.io/gitlab-profile/-/blob/master/docs/common/epic-task-structure.md
  - purpose: current
    repository: https://gitlab.com/smart-assets.io/gitlab-profile
    checkout: ../../../SA/top-level-gitlab-profile
    revision: master
    path: docs/common/todos-mr_pr-tracking-standard.md
    url: https://gitlab.com/smart-assets.io/gitlab-profile/-/blob/master/docs/common/todos-mr_pr-tracking-standard.md
---

# Tasks and Epics

This document tracks implementation work through **epics** (logical groupings of related tasks).

**Document Structure**
- Active work: This file (`docs/ToDos.md`)
- User stories: [UserStories.md](UserStories.md)
- Release plan: [roadmap.md](roadmap.md)
- Architecture and open questions: [designs/faucet-architecture.md](designs/faucet-architecture.md)
- Stack and hosting record: [designs/stack-and-hosting.md](designs/stack-and-hosting.md)
- Node compatibility proposal: [designs/node-compatibility.md](designs/node-compatibility.md)
- Completed work: [CompletedTasks.md](CompletedTasks.md)
- Backlog: [Backlog.md](Backlog.md)

The frontmatter records the Epic Task Structure Reference and the MR/PR Tracking Standard in the top-level profile.

**External dependencies.** Two epics in f1r3node-rust gate this work. EPIC-014 delivers the CbC Casper test net. EPIC-025 (PR #627) delivers the consensus-neutral boundary that the other models need.

[git@github.com:F1R3FLY-io/f1r3node-rust.git](https://github.com/F1R3FLY-io/f1r3node-rust)

```yaml cross-reference
reference:
  purpose: evidence
  repository: https://github.com/F1R3FLY-io/f1r3node-rust
  checkout: ../../f1r3node-rust
  revision: 19bed60a334f86caa32e38ab4c10ce73b7b12287
  path: docs/ToDos.md
  url: https://github.com/F1R3FLY-io/f1r3node-rust/blob/19bed60a334f86caa32e38ab4c10ce73b7b12287/docs/ToDos.md
  anchor: epic-014-f1r3fly-cbc-casper-test-net-continuously-running-shards
```

```yaml cross-reference
reference:
  purpose: evidence
  repository: https://github.com/F1R3FLY-io/f1r3node-rust
  checkout: ../../f1r3node-rust
  revision: 6609305bbde5a13ab6df4d1f0877bfbe53e74f2a
  path: docs/ToDos.md
  url: https://github.com/F1R3FLY-io/f1r3node-rust/blob/6609305bbde5a13ab6df4d1f0877bfbe53e74f2a/docs/ToDos.md
  anchor: epic-025-pluggable-state-machine-replication-boundary
```

---

## MR/PR Tracking

When all tasks in this file are complete and ready for merge, update the frontmatter:

```yaml
mr_status:
  ready: true
  target_branch: main
  title: "feat: <MR title>"
  description: |
    ## Summary
    - <Completed items>

    ## Test plan
    - [x] All tests passing
  labels: ["feature", "enhancement"]
```

---

## Active Epics

<!-- Epics are ordered by priority. Work on the highest priority epic first. -->

---

### EPIC-001: Stack Decisions and Repository Scaffolding

```yaml
---
epic_id: EPIC-001
title: "Stack Decisions and Repository Scaffolding"
status: pending
priority: p0
user_story: US-001
blocked_by: []
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-001-1
    title: "Accept the stack and hosting record (design questions Q8 and Q9)"
    status: complete
    notes:
      - "2026-10-15: docs/designs/stack-and-hosting.md proposes Vite and Fastify, pnpm, Vitest and Playwright, and signing in TypeScript"
      - "2026-10-15: the maintainer accepted the record (decision S1)"
    acceptance:
      - "A maintainer accepts docs/designs/stack-and-hosting.md, or records changes to it"
      - "README.md and CLAUDE.md show the accepted stack"
  - id: TASK-001-2
    title: "Scaffold the workspace (apps/web, apps/api, packages/*)"
    status: pending
    blocked_by: [TASK-001-1]
    acceptance:
      - "TypeScript strict mode is on in every package, with a shared base tsconfig"
      - "apps/web builds with Tailwind CSS and shows one placeholder page"
      - "apps/api starts and answers GET /healthz with 200"
      - "The lockfile is committed. The Node.js version is pinned (.nvmrc or engines)"
  - id: TASK-001-3
    title: "Add lint, format, type check, and test commands"
    status: pending
    blocked_by: [TASK-001-2]
    acceptance:
      - "One root command runs lint, type check, and tests for every package"
      - "One example unit test passes in each package"
  - id: TASK-001-4
    title: "Add GitHub Actions CI"
    status: pending
    blocked_by: [TASK-001-3]
    acceptance:
      - "CI runs install, lint, type check, test, and build on each push and pull request"
      - "CI runs the canonical markdown link check, including declared cross-references"
  - id: TASK-001-5
    title: "Fill .gitignore and add .env.example"
    status: pending
    blocked_by: [TASK-001-2]
    acceptance:
      - ".gitignore covers node_modules, build output, coverage, .env files except .env.example, and editor files"
      - ".env.example lists each variable with a placeholder value only"
---
```

**Context:** The repository has documents only. The ASI faucet has no tests, no CI for lint or build, and no committed lockfiles. This epic sets a stronger base before feature work starts.

**Scope:**
- Included: stack decisions, workspace layout, tooling, CI.
- Excluded: features. Hosting (EPIC-008).

---

### EPIC-002: F1r3fly Client Package

```yaml
---
epic_id: EPIC-002
title: "F1r3fly Client Package (address, signing, node API)"
status: pending
priority: p0
user_story: US-001
blocked_by: [EPIC-001]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-002-1
    title: "Vault address derivation and validation"
    status: pending
    acceptance:
      - "Derive a vault address from a secp256k1 public key (compressed or uncompressed)"
      - "Validation checks Base58, the coin ID, the version, and the Blake2b-256 checksum"
      - "Test vectors come from f1r3node-rust vault_address.rs and from addresses in the genesis wallets file. All pass"
      - "An address with one changed character fails validation"
      - "An ETH address (0x and 40 hex characters) converts to the same vault address that f1r3wallet and the ASI Chain wallet show"
  - id: TASK-002-2
    title: "Deploy data encoding and secp256k1 signing"
    status: pending
    acceptance:
      - "The signature is over Blake2b-256 of the protobuf DeployDataProto encoding, as the node requires"
      - "The protobuf types are generated from CasperMessage.proto at a pinned node commit. The signed bytes omit the language field and default values"
      - "CI compares signatures with golden vectors from rust-client, including deploys that set expirationTimestamp and parameters"
      - "A deploy that the package signs is accepted by a local f1r3node shard"
      - "The private key is held only by a signer object that has no serialization and no log output"
  - id: TASK-002-3
    title: "Node HTTP client"
    status: pending
    acceptance:
      - "Typed calls for /api/status, /api/deploy, /api/deploy-finalization-status/{sig}, /api/is-finalized/{hash}, /api/last-finalized-block, and /api/balance/{address}"
      - "Each call has a timeout and maps node errors to typed error codes"
  - id: TASK-002-4
    title: "SystemVault transfer and balance terms"
    status: pending
    acceptance:
      - "The transfer term uses the vault URI of the shard (default rho:vault:system) with findOrCreate, deployerAuthKey, and transfer"
      - "Amounts are bigint dust. The term builder rejects a negative or zero amount"
      - "A contract test transfers tokens on a local shard and reads the new balance"
  - id: TASK-002-5
    title: "Local shard test fixture"
    status: pending
    acceptance:
      - "One command starts a local f1r3node shard in Docker with a funded test faucet key"
      - "Contract tests run against it in CI, or as a separate job if CI time is too long"
---
```

**Context:** Execution stays Rholang on RSpace for every consensus model (PR #627). The address format, the deploy signature, and the SystemVault contract are therefore common to all adapters. The ASI faucet checks only the address prefix and length.

**Notes:**
- The node renamed RevVault to SystemVault at `rho:vault:system`. The address type is VaultAddress.
- Design question Q9 decides whether this package signs in TypeScript or calls the Rust rust-client.

---

### EPIC-003: Consensus Adapter Interface, Network Registry, and CbC Casper Adapter

```yaml
---
epic_id: EPIC-003
title: "Consensus Adapter Interface, Network Registry, and CbC Casper Adapter"
status: pending
priority: p0
user_story: US-006
blocked_by: [EPIC-002]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-003-1
    title: "Define the ConsensusAdapter interface"
    status: pending
    acceptance:
      - "The interface has capabilities, networkInfo, progress, balance, submitTransfer, and status (design Section 5.2)"
      - "The type names follow the neutral types of PR #627 (CommitRecord.sequence, FinalityEvent)"
      - "A stub adapter implements the interface for tests"
  - id: TASK-003-2
    title: "Network registry schema and loader"
    status: pending
    acceptance:
      - "The loader reads the shard registry that the test net publishes (test net design, Section 12.4, item 2) and joins it with the faucet settings of each shard"
      - "A JSONC file gives the same data for local development: id, consensusModel, status, deploy and observer endpoints, faucetKeyRef, vaultUri, claim settings"
      - "The loader rejects an unknown consensusModel and a duplicate id"
      - "Shard ID and token metadata come from the node status call, not from the file"
      - "A shard with status retired shows on the website but accepts no claims"
  - id: TASK-003-3
    title: "cbc-casper adapter"
    status: pending
    blocked_by: [TASK-003-1, TASK-003-2]
    acceptance:
      - "Deploys go to a validator. Balance and status reads go to the observer"
      - "validAfterBlockNumber comes from the last finalized block"
      - "Status maps FINALIZED, FAILED, PENDING, and EXPIRED to the claim states of design Section 5.4"
      - "Contract tests pass against the local shard of TASK-002-5"
---
```

**Context:** Each test net runs one consensus model, and a test net can start new shards. The ASI faucet supports one network and fixes the shard ID to `root`.

---

### EPIC-004: Faucet API Service

```yaml
---
epic_id: EPIC-004
title: "Faucet API Service"
status: pending
priority: p0
user_story: US-001
blocked_by: [EPIC-003]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-004-1
    title: "API routes"
    status: pending
    acceptance:
      - "GET /networks, GET /networks/{id}/balance/{address}, POST /claims, GET /claims/{id}, GET /healthz, GET /readyz"
      - "An OpenAPI document describes each route"
      - "Errors use typed codes. No raw node text reaches the client"
  - id: TASK-004-2
    title: "Claim store"
    status: pending
    acceptance:
      - "Claims persist with network, address, amount, state, deploy ID, and timestamps"
      - "A restart does not lose a claim in the queued or submitted state"
  - id: TASK-004-3
    title: "Signer queue for each faucet key"
    status: pending
    blocked_by: [TASK-004-2]
    acceptance:
      - "One deploy at a time is in flight for each faucet key"
      - "An expired claim is sent again one time with a new validAfterBlockNumber"
      - "A test with 50 concurrent claims gives 50 distinct transfers and no duplicate"
  - id: TASK-004-4
    title: "Idempotent claims"
    status: pending
    acceptance:
      - "POST /claims takes an idempotency key. A repeated key returns the first claim"
  - id: TASK-004-5
    title: "Faucet key loading"
    status: pending
    acceptance:
      - "The key comes from the secret store reference in the registry, or from an environment variable in local mode only"
      - "A test proves that the key does not appear in logs, errors, or debug output of the configuration"
      - "The service does not start when a network has no key. There is no default key"
  - id: TASK-004-6
    title: "Amounts in dust with a correct balance ceiling"
    status: pending
    acceptance:
      - "All amounts are bigint dust from input to deploy"
      - "Boundary tests: balance at the ceiling minus one dust passes, at the ceiling fails"
---
```

**Context:** The ASI faucet has three gaps here. A unit error disables its balance ceiling. Its debug log can contain its private key. It signs concurrent claims without a queue. This epic fixes each of these gaps by design.

---

### EPIC-005: Abuse Controls

```yaml
---
epic_id: EPIC-005
title: "Abuse Controls"
status: pending
priority: p1
user_story: US-004
blocked_by: [EPIC-004]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-005-1
    title: "Rate limits and cooldowns"
    status: pending
    acceptance:
      - "Limits for each IP address, each recipient address, and each network, set in the registry"
      - "A refused claim returns a typed error with the time of the next allowed claim"
  - id: TASK-005-2
    title: "Human verification"
    status: pending
    blocked_by: [TASK-005-1]
    acceptance:
      - "The selected provider (design question Q7) protects POST /claims"
      - "The API checks the token on the server side"
  - id: TASK-005-3
    title: "CORS allowlist and request limits"
    status: pending
    acceptance:
      - "CORS allows only the configured web origins"
      - "Body size and request timeout limits are set"
  - id: TASK-005-4
    title: "Faucet balance floor"
    status: pending
    acceptance:
      - "Claims on a network stop when the faucet balance is below its floor"
      - "The website shows that the network is out of funds"
  - id: TASK-005-5
    title: "Partner tier"
    status: pending
    blocked_by: [TASK-005-1]
    acceptance:
      - "An operator can issue an API key to a partner or customer"
      - "A claim with a valid key gets the partner limits from the registry"
      - "An operator can revoke a key"
---
```

**Context:** The ASI faucet has no rate limit and no captcha on its transfer route, and CORS allows any origin. The audience is anyone who tests F1r3fly shards, with partners and customers first (design question Q13). The site is therefore public, and the partner tier gives higher limits to known users.

---

### EPIC-006: Website

```yaml
---
epic_id: EPIC-006
title: "Website: Networks, Claims, and Status"
status: pending
priority: p1
user_story: US-003
blocked_by: [EPIC-004]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-006-1
    title: "Network list and network detail pages"
    status: pending
    acceptance:
      - "Each test net shows its consensus model, its shards, their status, and the observer endpoints"
      - "Token name, symbol, and decimals come from the API"
  - id: TASK-006-2
    title: "Claim form"
    status: pending
    acceptance:
      - "The user selects a network, enters a vault address or a public key, and sees the current balance"
      - "The form validates the address on the client with the same package as the API"
  - id: TASK-006-3
    title: "Claim tracker"
    status: pending
    acceptance:
      - "The page shows each claim state of design Section 5.4 until a final state"
      - "The claim URL can be shared and reloaded"
  - id: TASK-006-4
    title: "Accessibility and UI tests"
    status: pending
    acceptance:
      - "Tests use role and label queries, as CLAUDE.md requires"
      - "The pages pass an automated accessibility check with no serious violations"
---
```

**Context:** The ASI faucet has one page, plain CSS, and one network. F1r3Faucet is also the public face of each test net.

---

### EPIC-007: Wallet Integration: f1r3wallet and ASI Chain Wallet

```yaml
---
epic_id: EPIC-007
title: "Wallet Integration: f1r3wallet and ASI Chain Wallet"
status: pending
priority: p1
user_story: US-009
blocked_by: [EPIC-006]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-007-1
    title: "Accept the address forms of the wallets of record"
    status: pending
    acceptance:
      - "The claim form and API accept a vault address, an ETH address, and a secp256k1 public key"
      - "Each form gives the same vault address that the wallet shows"
  - id: TASK-007-2
    title: "Prefill link"
    status: pending
    acceptance:
      - "A documented URL (?network=<id>&address=<address>) opens the claim form with both fields entered"
      - "The website shows the network names and shard IDs that the wallets use"
  - id: TASK-007-3
    title: "Report the vault URI mismatch to the wallet maintainers"
    status: in_progress
    notes:
      - "2026-10-15: the maintainer fixes the registry in f1r3node-rust, so that the older vault URIs resolve on new shards"
    acceptance:
      - "The f1r3wallet and ASI Chain wallet maintainers know that a current F1r3fly shard registers only rho:vault:system (design question Q16)"
      - "The registry entry of each shard records its vault URI"
  - id: TASK-007-4
    title: "Ask the wallet maintainers to add the faucet link"
    status: pending
    blocked_by: [TASK-007-2]
    acceptance:
      - "The ASI Chain wallet Faucet link can point to F1r3Faucet with the prefill parameters"
      - "f1r3wallet has a link to F1r3Faucet, or its maintainers decline"
---
```

**Context:** The F1r3fly projects have three wallets of record: SATCHEL, f1r3wallet, and the ASI Chain wallet (design Section 3.1). f1r3wallet and the ASI Chain wallet work on CbC Casper shards today, so they come first. SATCHEL integration is EPIC-011.

---

### EPIC-012: Node Compatibility and Versioning

```yaml
---
epic_id: EPIC-012
title: "Node Compatibility and Versioning"
status: pending
priority: p1
user_story: US-006
blocked_by: [EPIC-003]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-012-1
    title: "Propose the versioning standard to f1r3node-rust"
    status: pending
    acceptance:
      - "A f1r3node-rust pull request proposes Section 3 of docs/designs/node-compatibility.md as a change to docs/release-process.md"
      - "The f1r3node-rust maintainers decide V1, V2, and V3"
  - id: TASK-012-2
    title: "Adapter version ranges and status probe"
    status: pending
    acceptance:
      - "Each adapter declares its supported API versions and node release range"
      - "The faucet probes each deploy validator and the observer at start and on a schedule"
      - "A shard outside the range accepts no claims, the website shows the reason, and an alert fires"
  - id: TASK-012-3
    title: "Capability checks"
    status: pending
    blocked_by: [TASK-012-1]
    acceptance:
      - "The adapter uses an optional feature only when every deploy validator lists its capability"
      - "Without a capability list, the adapter uses the base capabilities of its release range (record Section 4.1)"
  - id: TASK-012-4
    title: "Contract tests by node release"
    status: pending
    acceptance:
      - "CI runs the adapter contract tests against the latest stable release and the newest canary"
      - "A nightly job runs them against each new test net candidate and reports a failure before enrollment"
  - id: TASK-012-5
    title: "Compatibility matrix"
    status: pending
    acceptance:
      - "The documentation shows which faucet release supports which node releases and shards"
---
```

**Context:** f1r3node-rust has SemVer release tags, but no rule for when the client API changes, a fixed `version.api` of "1", and no capability list. The vault URI rename (design question Q16) broke two wallets of record without a signal. The [node compatibility record](designs/node-compatibility.md) proposes a standard for f1r3node-rust and a mechanism for the faucet.

---

### EPIC-008: Observability, Packaging, and Deployment

```yaml
---
epic_id: EPIC-008
title: "Observability, Packaging, and Deployment"
status: pending
priority: p1
user_story: US-005
blocked_by: [EPIC-004]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-008-1
    title: "Logs and metrics"
    status: pending
    acceptance:
      - "Structured logs carry the request ID in each span"
      - "Prometheus metrics: claims by state and network, queue depth, node latency, faucet balance"
  - id: TASK-008-2
    title: "Faucet balance alert"
    status: pending
    acceptance:
      - "An alert fires when a faucet balance is below its floor"
  - id: TASK-008-3
    title: "Container images"
    status: pending
    acceptance:
      - "The web and API images build in CI, go to the selected registry (OCIR proposed), and are pinned by digest"
      - "The API image runs as a user that is not root"
  - id: TASK-008-4
    title: "OCI deployment beside the test net"
    status: pending
    acceptance:
      - "The faucet runs on OCI beside the test net, as docs/designs/stack-and-hosting.md Section 5 describes"
      - "The API reads each faucet key from OCI Vault through an instance principal. No key is in an environment file"
      - "Only the faucet can reach the deploy endpoint (network security group rule)"
---
```

---

### EPIC-009: CbC Casper Test Net Launch

```yaml
---
epic_id: EPIC-009
title: "CbC Casper Test Net Launch"
status: blocked
priority: p1
user_story: US-001
blocked_by: [EPIC-005, EPIC-008, "f1r3node-rust EPIC-014 first apply", "f1r3node-rust TASK-014-10"]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-009-1
    title: "Faucet wallet in the test net genesis"
    status: pending
    acceptance:
      - "The test net wallets file funds the faucet address before the first shard starts (test net design, Section 12.4, item 1)"
      - "The faucet key is in OCI Vault. No person holds a copy outside the secret store"
  - id: TASK-009-2
    title: "Deploy access for the faucet"
    status: pending
    notes:
      - "2026-10-15: the maintainer accepted S2 option A (the three Anchors, with failover) and S3 option A (a private subnet in the test net VCN)"
    acceptance:
      - "f1r3node-rust PR #654 records decisions S2 and S3 in test net design Sections 10, 13.2, and 14"
      - "A network security group rule lets only the faucet reach the HTTP API port of the three Anchors (S2)"
      - "The faucet runs in a private subnet of the CbC Casper test net VCN, behind a load balancer (S3)"
      - "The faucet API can send deploys to those validators from OCI, with failover between them"
      - "Partners still reach only the observer"
  - id: TASK-009-3
    title: "Launch and smoke test"
    status: pending
    blocked_by: [TASK-009-1, TASK-009-2]
    acceptance:
      - "A claim on the main shard reaches finalized"
      - "The registry entry for the main shard has status active"
  - id: TASK-009-4
    title: "New shard procedure"
    status: pending
    acceptance:
      - "A runbook covers a new shard after an incompatible release: new faucet wallet in genesis, new registry entry, old entry set to retiring"
---
```

**Context:** f1r3node-rust TASK-014-10 and test net design Section 12.4 define what the test net supplies. The items are genesis funding, the shard registry, a deploy path for the faucet only, key custody in OCI Vault, and operation on OCI. The genesis wallets file has no faucet entry today.

---

### EPIC-010: Adapters for Other Consensus Models

```yaml
---
epic_id: EPIC-010
title: "Adapters for Casanova, Cordial Miners, and RGB"
status: blocked
priority: p3
user_story: US-008
blocked_by: [EPIC-003, "f1r3node-rust EPIC-025 TASK-025-5", "f1r3node-rust EPIC-014 TASK-014-9"]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-010-1
    title: "Neutral adapter on the EPIC-025 neutral endpoints"
    status: pending
    acceptance:
      - "One adapter uses the neutral deploy, status, and finality endpoints of TASK-025-5"
      - "Progress uses CommitRecord.sequence and accepts a null sequence"
  - id: TASK-010-2
    title: "Cordial Miners adapter"
    status: pending
    blocked_by: [TASK-010-1]
    acceptance:
      - "Contract tests pass against a Cordial Miners shard"
  - id: TASK-010-3
    title: "Casanova adapter"
    status: pending
    blocked_by: [TASK-010-1]
    acceptance:
      - "Contract tests pass against a Casanova shard"
  - id: TASK-010-4
    title: "RGB test net faucet design"
    status: pending
    acceptance:
      - "A design record answers design question Q12 (test BTC, Lightning liquidity, RGB assets)"
      - "The record follows the RGB test net design record of f1r3node-rust TASK-014-9"
  - id: TASK-010-5
    title: "RGB adapter"
    status: pending
    blocked_by: [TASK-010-1, TASK-010-4]
    acceptance:
      - "A claim on the RGB test net reaches its final state"
      - "The adapter dispenses the extra assets that TASK-010-4 requires"
---
```

**Context:** Each model has its own test net. Only CbC Casper is implemented today. The neutral client endpoints do not exist yet. The RGB adapter is a prerequisite of SATCHEL integration (EPIC-011).

---

### EPIC-011: SATCHEL Integration on the RGB Test Net

```yaml
---
epic_id: EPIC-011
title: "SATCHEL Integration on the RGB Test Net"
status: blocked
priority: p2
user_story: US-002
blocked_by: [EPIC-007, "TASK-010-5", "f1r3node-rust EPIC-025"]
created_at: 2026-10-15
claimed_by: null
claimed_at: null
tasks:
  - id: TASK-011-1
    title: "SATCHEL public key and address"
    status: pending
    acceptance:
      - "A key from the SATCHEL path m/1337'/0'/0'/0/0 gives the same address in the faucet and in the SATCHEL server"
  - id: TASK-011-2
    title: "Fund my SATCHEL link"
    status: pending
    acceptance:
      - "The SATCHEL wallet opens the prefill link of TASK-007-2 for the RGB test net"
      - "The SATCHEL team accepts the link format"
  - id: TASK-011-3
    title: "Ownership proof by signed challenge"
    status: pending
    acceptance:
      - "The API issues a single-use challenge. A valid secp256k1 signature over it proves ownership"
      - "A proven owner gets the higher limit from the registry"
      - "The SATCHEL team agrees to add a challenge-signing endpoint (design question Q3)"
  - id: TASK-011-4
    title: "Replace the SATCHEL regtest vault faucet on the shared test nets"
    status: pending
    acceptance:
      - "The SATCHEL team agrees which faucet the wallet uses on each network (design question Q4)"
      - "The private key fallback in rgb-satchel is reported to its maintainers"
---
```

**Context:** SATCHEL is the main wallet of record. It deploys on the RGB test net first, and that test net needs the consensus and SMR boundary of f1r3node-rust EPIC-025 (design Section 3.1).

---

## Epic Template

Use this template when adding new epics:

```yaml
---
epic_id: EPIC-XXX
title: "Short descriptive title"
status: pending
priority: p2
user_story: US-XXX
blocked_by: []
created_at: YYYY-MM-DD
claimed_by: null         # Implementer ID: human-{email}, {tool}-session[-{id}], or {team}/{role}
claimed_at: null
tasks:
  - id: TASK-XXX-1
    title: "Task description"
    status: pending
    acceptance:
      - "Measurable acceptance criterion"
---
```

---

## Task States

| Status | Meaning | Next Action |
|--------|---------|-------------|
| `pending` | Not started | Available to claim |
| `in_progress` | Being worked on | Continue or handoff |
| `blocked` | Waiting on dependency | Check `blocked_by` |
| `review` | Ready for review | Review and approve |
| `complete` | Done | Move to CompletedTasks.md |

---

## Workflow

1. **Find next task**: Use `/nextTask` to identify the highest priority unclaimed task
2. **Claim task**: Set `claimed_by` in the Implementer Identification format (`human-{email}`, `{tool}-session[-{id}]`, or `{team}/{role}`) and `status: in_progress`
3. **Implement**: Use `/implement` to execute with full context
4. **Complete**: Mark `status: complete` when acceptance criteria met
5. **Move epic**: When all tasks complete, move epic to [CompletedTasks.md](CompletedTasks.md)
