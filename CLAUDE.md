# F1r3Faucet

This file gives guidance to AI assistants that work in this repository.

## Project Overview

F1r3Faucet is a general-purpose faucet and website for F1r3fly test net shards. `README.md` gives the purpose, the proposed architecture, and the roadmap.

- **Faucet:** Users request test tokens for an address on a selected test net shard. Rate limits and abuse controls apply.
- **Website:** The site shows each test net, its shards, its consensus model, the shard status, and the observer endpoints.
- **Model-neutral design:** Each test net runs one consensus model (`cbc-casper`, `casanova`, `cordial-miners`, or `rgb`). Each model connects through one adapter that implements a common interface. Do not put model-specific logic outside its adapter.
- **Shard discovery:** A test net can start new shards and retire old shards. Get the shard list from the shard registry. Do not hard-code shards.
- **Wallets of record:** SATCHEL, f1r3wallet, and the ASI Chain wallet. All three use the same vault address format
- **First target:** The F1r3fly CbC Casper test net (EPIC-014 in `f1r3node-rust/docs/ToDos.md`, design record `f1r3node-rust/docs/plans/test-net.md`).

## Tech Stack

- TypeScript in strict mode
- Web: Vite, React, and Tailwind CSS
- API: Node.js 24 LTS with Fastify
- Workspace and tests: pnpm, Vitest, and Playwright
- Deploy signing in TypeScript, checked against golden vectors from `rust-client`
- Hosting: OCI beside the test net
- `docs/designs/stack-and-hosting.md` records these decisions (accepted 2026-10-15)
- Never hard-code the token name. Each shard sets it at genesis, and the node returns it from its status call. Phlo is the fee unit and dust is the smallest token unit

## Security

- Never commit the faucet wallet key, validator keys, or other secrets. Get them from a secret store through environment variables.
- List each environment variable in `.env.example` with a placeholder value only.
- Partners get read-only observer access. The faucet must not need validator access.

## LLM Development Philosophy

This project follows Smart Assets' **document-first development** approach. The AI Coding Philosophy document gives complete details.

```yaml cross-reference
reference:
  purpose: current
  repository: https://gitlab.com/smart-assets.io/gitlab-profile
  checkout: ../../SA/top-level-gitlab-profile
  revision: master
  path: docs/common/ai-coding-philosophy.md
  url: https://gitlab.com/smart-assets.io/gitlab-profile/-/blob/master/docs/common/ai-coding-philosophy.md
```

### Key Principles

1. **Stigmergic Collaboration**: Coordinate with other agents through shared `.md` files
2. **Document-First**: Create design docs and specifications BEFORE implementation
3. **Signal vs. Slop**: Maximize code that solves problems; avoid over-engineering
4. **Acceptance Criteria**: Define measurable success criteria in task definitions

### Standard Document Structure

| Document | Purpose | Location |
|----------|---------|----------|
| User Stories | Business needs and acceptance criteria | `docs/UserStories.md` |
| Tasks/Epics | Implementation tracking | `docs/ToDos.md` |
| Completed Work | Historical reference | `docs/CompletedTasks.md` |
| Backlog | Deferred items | `docs/Backlog.md` |
| Work Logs | Session progress | `docs/work-logs/*.md` |
| Discoveries | Shared findings | `docs/discoveries/*.md` |

## Stigmergic Collaboration

This project uses **stigmergic collaboration** - agents coordinate through shared `.md` files rather than direct messaging. When using Claude Code agent teams, real-time IPC replaces file-based coordination; stigmergic files remain for cross-session continuity, audit trails, and cross-tool interop.

Full guide: Stigmergic Collaboration Guide.

```yaml cross-reference
reference:
  purpose: current
  repository: https://gitlab.com/smart-assets.io/gitlab-profile
  checkout: ../../SA/top-level-gitlab-profile
  revision: master
  path: docs/common/stigmergic-collaboration.md
  url: https://gitlab.com/smart-assets.io/gitlab-profile/-/blob/master/docs/common/stigmergic-collaboration.md
```

### Before Starting Work

1. **Read `docs/ToDos.md`** to check task status and claims
2. **Check `docs/work-logs/`** for existing progress on related tasks
3. **Review `docs/discoveries/`** for relevant context from other agents

### When Claiming a Task

Update the task in `docs/ToDos.md`:

```yaml
---
id: TASK-001
status: in_progress          # Changed from 'pending'
claimed_by: claude-session-a1b2c3  # See Implementer Identification format
claimed_at: 2025-01-15T10:00:00Z
# Other valid claimed_by formats:
#   human-jeff@example.com        # Human (git config --get user.email)
#   design-sprint/researcher      # Agent team member ({team}/{name})
---
```

### During Work

1. **Create work log** at `docs/work-logs/task-{id}-{timestamp}.md`
2. **Document discoveries** in `docs/discoveries/` for other agents
3. **Update blockers** if you encounter dependencies

### Before Pausing/Completing

Update your work log with handoff notes:

```yaml
---
handoff_status: ready | paused | blocked
next_steps:
  - What remains to be done
---
```

### Document-First Workflow

For significant features:

1. **User Story**: Capture the business need in `docs/UserStories.md`
   - Define persona, capability, and benefit
   - List acceptance criteria

2. **Design Document**: Describe problem and solution
   ```bash
   cp ../../SA/top-level-gitlab-profile/docs/templates/design-doc.md.template docs/designs/[feature-name].md
   ```

3. **Specification**: Define interfaces and behavior
   ```bash
   cp ../../SA/top-level-gitlab-profile/docs/templates/specification.md.template docs/specs/[component-name].md
   ```

4. **Task Definition**: Add epic to `docs/ToDos.md` with tasks

5. **Implement**: Only after documentation is reviewed

6. **Complete**: Update user story status when epic completes

## AI Artifact Generation Guidelines

**Core strategy:** Default to **Markdown + Mermaid** as the source of truth for all generated artifacts. Use **HTML** only when high engagement or advanced interactivity is required.

**Preferred formats:**

| Format | Use for | Notes |
|--------|---------|-------|
| **Markdown + Mermaid** | Primary. Diagrams (flowcharts, sequences, architecture, timelines, Gantt, ERDs), structured documents, plans, specs | Relative links (`./images/`, `./docs/`) and GitHub/GitLab raw URLs for local/cloud asset referencing |
| **HTML (CSS/JS + embedded Mermaid)** | Secondary. Interactive dashboards, prototypes, dynamic reviews, stakeholder deliverables | When visual polish and engagement are critical (tabs, sliders, clickable elements) |

**Hybrid rule:** Always produce Markdown as the canonical, Git-friendly version first; generate a self-contained HTML export on request.

**Key principles:**

- Prioritize human readability, editability, and Git compatibility (clean diffs, relative paths, native rendering on GitHub/GitLab).
- Maximize information density while avoiding text walls — convert complex information into Mermaid diagrams.
- Support seamless referencing of local files and cloud artifacts (images, other docs, raw Git content).
- Favor Markdown for internal/agent use and long-term storage (token efficiency).
- Use HTML when delivering to stakeholders or for living documents (engagement).

**Output guidance:** When creating artifacts, ask whether HTML interactivity is needed. Default to clean Markdown with embedded Mermaid unless specified.

<!-- ste-policy: required -->

## Simplified Technical English
<!-- ste-policy: full -->

Smart Assets uses ASD-STE100 Simplified Technical English, Issue 9, dated January 2025, for applicable English technical prose.

This policy is a Smart Assets applicability profile. The ASD standard remains the authoritative source for its rules and controlled dictionary.

Get the current standard from the [official ASD-STE100 website](https://www.asd-ste100.org/) or its [official downloads page](https://www.asd-ste100.org/STE_downloads.html).

ASD owns the standard and the ASD-STE100 trademark. Do not copy its controlled dictionary, examples, or substantial rule text into this repository.

## UI Test Assertions

React UI tests should prove user-observable DOM structure and state, not incidental copy or formatted sample values. Treat exact text/value assertions as a last resort unless the behavior under test is specifically copy, formatting, or content transformation.

- **Preferred:** Accessibility-first queries for DOM elements and states: `getByRole`, `getByLabelText`, `aria-label`, `aria-labelledby`, `aria-selected`, `aria-expanded`, `aria-disabled`, focus state, and ARIA relationships.
- **Preferred:** Assert semantic regions/components are present and wired correctly (tabs, tabpanels, dialogs, forms, buttons, lists), then assert behavior through state changes or callback/data-source calls.
- **Acceptable:** `data-testid` attributes when no accessible handle exists, the element is purely presentational, or the test needs to identify a stable component boundary rather than text content.
- **Acceptable:** HTML `id` attributes for form elements and ARIA relationships.
- **Avoid:** `getByText`/`queryByText` for literal strings that are merely display copy, repeated metrics, formatted numbers, or mock-data values.
- **Avoid:** `getAllByText(...).length` as a substitute for a meaningful DOM assertion; it couples tests to duplicated visual text rather than behavior.
- **Avoid:** CSS class selectors that may change with styling updates.

Examples:

```tsx
// GOOD: accessibility-first DOM element + state
expect(screen.getByRole("button", { name: "Refresh agents" })).toBeEnabled();

// ACCEPTABLE: fallback when no accessible role/name fits
expect(screen.getByTestId("cost-optimization-panel")).toBeInTheDocument();

// GOOD for data-flow behavior: verify source + rendered component boundary,
// not a duplicated metric string like "7.5%".
expect(fetchQualityPipeline).toHaveBeenCalledTimes(1);
expect(screen.getByRole("tablist", { name: "Quality Pipeline tabs" })).toBeInTheDocument();
expect(screen.getByRole("tab", { name: /overview/i })).toHaveAttribute("aria-selected", "true");

// BAD: brittle copy assertion
expect(screen.getByText("Priority set by BountyForge routing")).toBeInTheDocument();

// BAD: brittle mock-value / duplicated visual text assertion
expect(screen.getByText("7.5%")).toBeInTheDocument();
expect(screen.getAllByText("7.5%").length).toBeGreaterThan(0);
```

**When exact text is appropriate:** Use exact text assertions only when the acceptance criteria is about user-facing copy, accessibility name computation, validation messages, formatting rules, or transformed content. Prefer scoping with `within(...)` to a semantic container so the assertion remains tied to the behavior under test.

## Worktree Policy

Git worktrees are an **agentic-mode-only** tool in this workspace. In safe /
interactive mode:

- **NEVER create a git worktree** unless the user explicitly asks for one in
  their own words. This covers every creation path equally: `git worktree add`,
  harness-native tools (e.g. an `EnterWorktree` tool, subagent
  `isolation: "worktree"`, workflow worktree isolation), and any script that
  wraps them.
- All work happens in the single main checkout on the current branch.
- `git worktree list` is read-only and permitted.
- `git worktree remove` and `git worktree prune` require explicit user
  confirmation.

**Why:** worktrees fragment local state, are invisible to `/recursive-push`
repository discovery, and were the root cause of an accidental push to a
protected branch. A worktree created silently by an assistant is a worktree
nobody pushes, cleans up, or audits.

**Exception:** In agentic mode (`claude-agentic`), all restrictions are lifted.
YOLO mode runs *inside* a worktree the human created; running in a worktree
never authorizes creating more of them.

Canonical policy: Git Interaction Policy, Worktrees section.

```yaml cross-reference
reference:
  purpose: current
  repository: https://gitlab.com/smart-assets.io/gitlab-profile
  checkout: ../../SA/top-level-gitlab-profile
  revision: master
  path: docs/common/git-interaction-policy.md
  url: https://gitlab.com/smart-assets.io/gitlab-profile/-/blob/master/docs/common/git-interaction-policy.md
```

## Cross-Repository References

Use the reference form that matches the location of the target. The Cross-Reference Standards document contains the full rules.

| Target | Required form |
| --- | --- |
| File in the same repository | Document-relative Markdown link |
| Current guidance in another repository | `yaml cross-reference` block or `cross_references` frontmatter with `purpose: current` |
| Evidence or an approved decision | Record with `purpose: evidence` and a full commit ID |

Obey these rules when you write a record:

- Set `checkout` relative to the directory of the source document.
- Set `path` relative to the root of the target repository.
- Take the hosted project path from the configured remote or from `repo-mapping.yaml`. Local directory names and hosted project names can be different.
- Set `revision` to the branch that holds the current content. Do not assume `master` or `main`.
- Do not write a Markdown link to a file in another repository. A single-repository clone cannot resolve that link, and the CI link check fails.
- Before you commit, run `scripts/check-broken-links.py --references-only` from the top-level profile on each changed Markdown file.

Do not copy the link form of older text. Older text can contain the two-label form that version 2 of the standard replaced.

```yaml cross-reference
reference:
  purpose: current
  repository: https://gitlab.com/smart-assets.io/gitlab-profile
  checkout: ../../SA/top-level-gitlab-profile
  revision: master
  path: docs/common/cross-reference-standards.md
  url: https://gitlab.com/smart-assets.io/gitlab-profile/-/blob/master/docs/common/cross-reference-standards.md
```

### Configuration File Conventions

When creating or modifying configuration files, follow these conventions to respect existing project preferences:

**JSON Format Preference Order:**

1. **Check for existing files first**: Before creating any `.json` file, check if `.jsonc` or `.json5` variants exist
2. **Prefer existing format**: If `config.jsonc` or `config.json5` exists, use that format instead of creating `config.json`
3. **Default to JSONC**: When creating new config files, prefer `.jsonc` (JSON with Comments) for better maintainability

**Why This Matters:**
- Projects may have established preferences for comment-supporting JSON formats
- Creating duplicate configs (e.g., both `biome.json` and `biome.jsonc`) causes confusion
- JSONC allows inline documentation which improves maintainability

**Examples:**

| If exists... | Don't create... | Instead... |
|--------------|-----------------|------------|
| `biome.jsonc` | `biome.json` | Edit the existing `biome.jsonc` |
| `tsconfig.json5` | `tsconfig.json` | Edit the existing `tsconfig.json5` |
| `eslint.config.jsonc` | `eslint.config.json` | Edit the existing file |
| Nothing | - | Create new file as `.jsonc` when comments are useful |

**File Discovery Pattern:**

Before creating any config file, check for variants:
```bash
# Check for config variants (example for biome)
ls biome.json biome.jsonc biome.json5 2>/dev/null
```

This applies to all slash commands and scripts that create configuration files.

### Slash Commands
<!-- SYNC:standard -->

The workspace `AItools` directory in the top-level profile provides the following slash commands. The Slash Command Requirements document defines them.

```yaml cross-reference
reference:
  purpose: current
  repository: https://gitlab.com/smart-assets.io/gitlab-profile
  checkout: ../../SA/top-level-gitlab-profile
  revision: master
  path: docs/common/slash-command-requirements.md
  url: https://gitlab.com/smart-assets.io/gitlab-profile/-/blob/master/docs/common/slash-command-requirements.md
```

#### Git Operations
- `/quick-commit` - Stage and commit changes (required in safe mode)
- `/recursive-push` - Push across repositories

#### Task Management
- `/nextTask` - Find and select next task to work on
- `/implement` - Begin implementation of a task
- `/epic-review` - Preview and summarize epics
- `/epic-hygiene` - Archive completed epics

#### Workspace Sync
- `/harmonize` - Sync workspace policies into this repo
- `/multi-repo-sync` - Workspace-wide sync orchestration

[OPTIONAL_COMMANDS]

## Development Modes
<!-- SYNC:standard -->

This project supports three operational modes for AI-assisted development.

| Mode | Command | Git Access |
|------|---------|------------|
| **Safe** | `claude` / `claude-safe` | Via `/quick-commit`, `/recursive-push` only |
| **Agentic** | `claude-agentic` | Direct git permitted |
| **YOLO** | `claude-agentic` (in user-created worktree) | Full autonomy, isolated |

**Safe mode** is the default. Use slash commands for all git operations.
**Agentic mode** requires branch consistency (`check-repo-consistency.sh --strict`).
**YOLO mode** requires a git worktree for isolation; the human creates the worktree (agents never create worktrees outside agentic mode - see Worktree Policy).

Reference: Development Modes.

```yaml cross-reference
reference:
  purpose: current
  repository: https://gitlab.com/smart-assets.io/gitlab-profile
  checkout: ../../SA/top-level-gitlab-profile
  revision: master
  path: docs/common/development-modes.md
  url: https://gitlab.com/smart-assets.io/gitlab-profile/-/blob/master/docs/common/development-modes.md
```

## PII Guidelines for Contributors

**CRITICAL - Before submitting any contribution:**

Contributors MUST ensure their code, commits, and documentation do NOT contain PII:

**Check before committing:**
- [ ] No absolute file paths with usernames in code or documentation
- [ ] No personal email addresses in code (use generic examples like `user@example.com`)
- [ ] No real user data in tests or examples (use synthetic/fake data only)
- [ ] No PII in log statements (sanitize or use user IDs instead)
- [ ] No PII in error messages or stack traces
- [ ] No PII in code comments or documentation
- [ ] No credentials, tokens, or secrets in code (use environment variables)
- [ ] No IP addresses, MAC addresses, or device identifiers in examples

**If you accidentally committed PII:**
1. **DO NOT** push to remote repository
2. Use `git reset` to remove the commit
3. If already pushed, contact maintainers immediately
4. Repository history may need to be rewritten to remove PII

**Use these instead:**
- File paths: Use relative paths or generic placeholders (`[WORKSPACE_ROOT]/project/`)
- Email addresses: Use `user@example.com`, `admin@example.com`
- Names: Use `John Doe`, `Jane Smith`, `User123`
- Phone numbers: Use `+1-555-0100` (officially reserved for examples)
- IP addresses: Use reserved ranges (`192.0.2.1`, `198.51.100.1`, `203.0.113.1`)
- Dates: Use recent but generic dates, not specific personal dates

**For test data:**
- Use test data generators that create realistic but fake data
- Use well-known test fixtures (e.g., `test@example.com`)
- Never use production or real user data in development/testing

## grepai - Semantic Code Search

`grepai` is an optional, MIT-licensed semantic-search tool. If it is installed
and indexed locally for this repo, prefer it for intent-based code exploration;
if it is unavailable, fall back to your harness's native search and file-reading
tools. It is recommended but never required. Nothing here is harness-specific -
substitute your tool's equivalents for the generic actions described below.
Setup (with the privacy-first local Ollama embedder as default) lives in the
CLI Setup guide's "Optional: Semantic Code Search (grepai)" section.

# important-instruction-reminders
Do what has been asked; nothing more, nothing less.
NEVER create files unless they're absolutely necessary for achieving your goal.
ALWAYS prefer editing an existing file to creating a new one.
NEVER proactively create documentation files (*.md) or README files. Only create documentation files if explicitly requested by the User.
Before making any code changes, first state: (1) which files you plan to modify, (2) what approach you'll take, (3) any assumptions you're making. Wait for my confirmation before proceeding. For simple single-file edits, a one-line summary is sufficient.
