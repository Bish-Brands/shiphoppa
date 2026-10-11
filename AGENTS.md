## 4. The rules

### 4.1 Operator rules for every repository and project (11 October 2026)

These four rules bind Codex and Claude, every agent either one runs, in every repository and project the operator owns, now and in future. The operator's words, 11 October 2026: "These critical classification, critical deploy and non-critical deploy, as well as the process rule (Investigate, plan, audit plan, edit code, audit edits, fix code) should apply to every repo, every project. They need to be claude rules as well as agents rules."

1. **The working method.**
   - Investigate, plan, audit the plan, edit code, audit the edits, fix what the audits found. Six steps, in that order, for every piece of work.
   - Each step is written on disk under its own heading (Investigation, Plan, Audit of the plan, Edits, Audit of the edits, Fixes) in the issue's dossier or plan document before the change is offered.
   - The plan audit comes before the first edit.
   - The edit audit includes a removal probe for every new guard: take the guard out, the test must fail, put the exact bytes back and prove it by hash.
   - Smaller work gets shorter entries, never fewer steps.
   - A report names the file that holds the six headings. A report without it is not finished.
2. **Critical classification.**
   - Only the operator makes work critical, by saying so in chat against the exact work (issue, branch, commit).
   - An agent may propose a designation with the concrete live impact. A label, a priority word or an agent's own judgement is not a designation.
   - Record the operator's words, the exact work and the date in the repository's record.
3. **Critical release.**
   - Approved critical work runs its required checks and releases immediately.
   - Every ready non-critical bank goes out with it in the same frozen release and the same hosted CI run, as long as including it does not delay or compromise the critical repair.
   - Every report lists its ready banks.
   - A critical release does not consume or cancel the daily non-critical train.
4. **Non-critical release.**
   - Non-critical work is committed and pushed to its unique task branch at once, and banked.
   - On its own it runs no hosted CI, Vercel or Railway build and opens no ready pull request. Inspect workflow triggers and preview settings before every push.
   - It goes live only in one daily non-critical train per repository per rolling 24 hours, or inside a critical release.
   - An empty train is not run, and a documents-only bank never starts one.

### 4.2 Release and checks

- Run hosted CI once per repository per train, after source freeze and local audits.
  - Never for individual checkpoints, word changes or progress notes.
  - Never trigger a deployment merely to save work.
- Checks may run at the same time only when isolated:
  - each concurrent group has its own database, ports, temporary directories, caches and build output;
  - at most two heavy local check groups run on one machine;
  - never kill another owner's process.
- Keep the full required test set, including database-marked and security tests. A failed, missing, cancelled or partial group is not a pass.
- Merge with merge commits (`gh pr merge --merge`). Squash merges are banned.

### 4.3 Git preservation

- **Before editing tracked files:**
  - fetch `origin`;
  - make a uniquely named branch in its own clean worktree from `origin/main`;
  - work in a worktree of the existing checkout, never a fresh clone of a repository already on the machine.
- **Checkouts.**
  - The shared `main` or `master` checkout is read-only. Never commit from it.
  - Never use a detached HEAD for editable work.
- **Worktree cap.** The operator's words, 11 October 2026: "The worktree rule is 3 worktrees plus main". Count with `git worktree list` before adding one.
  - Remove clean worktrees whose HEAD is already on `origin/main`.
  - Never remove a worktree touched in the last few hours or owned by another session.
- **Pushing.** Push every coherent commit to its task branch immediately. A local-only commit is not a checkpoint.
- **Never:**
  - `--no-verify` or `--no-gpg-sign`;
  - force push to `main` or `master`;
  - history rewriting or destructive reset;
  - amending a pushed commit;
  - deleting an unmerged branch;
  - a bare `git stash`;
  - `git add -A` or `git add .`. Stage by name.
- **Secrets.** `.env` files, credentials and keys are never staged or printed.
- **Integration.** Integrate through a pull request after fetching `origin/main`. Resolve conflicts by keeping the complete behaviour of every branch.
- **Deployment.** Deploy only from a clean checkout whose HEAD equals `origin/main`.
- **Before claiming completion, prove:**
  - the branch exists on `origin`;
  - the merged commit is reachable from `origin/main`;
  - the deployment is that canonical commit;
  - the live feature works.
- **Cleanup.** Then remove the worktree. The branch stays on `origin`.
- **Ambiguity.** If ownership of any branch, worktree or deployment is unclear, stop Git changes and inventory status, worktrees, branches and reflogs first.

### 4.4 No skipping, no deferring, no stubbing

- Banned in production comments, docstrings, commit text, handovers and final reports:
  - `TODO`, `FIXME`, `HACK`, `WIP`, `work in progress`, `stub`, `not implemented`, `not yet implemented`, `incomplete`, `placeholder`, `temporary fix`, `temporary workaround`;
  - `for now`, `tracked as follow-up`, `will add later` or `will fix later`, `in a future phase`, `next session`, `come back to`;
  - `out of scope`, `minimum blast radius`, `simpler pathway`, `reduced scope`, `safe enough for now`.
- Also banned, as reasons for not fixing something: `not my code`, `unrelated to my work`, `stale cache`, `outside scope`, `pre-existing`.
- If a check fails during your work, it is yours to fix, whoever wrote the code.
- The only alternatives to finishing in scope:
  - BLOCKED: a genuine external dependency, a missing credential or an operator decision. Say it in one sentence and keep working on adjacent work.
  - REMOVED: the operator explicitly descopes it.
- Every project carries a deferral-language gate in its tests, with an approvals file and a drift test. Install one at the first non-trivial change if missing.

### 4.5 Wired-up audit: nothing ships that nothing calls

Before calling anything done:
- every new export has a non-test caller;
- every new request field is read by its receiver, proved by a test at the boundary;
- every new UI control is traced from click to handler to network call to server effect;
- every new route, cron, webhook or job is registered;
- every new guard has a named input that makes it refuse.

Report anything you find dead, including code that existed before your work.

### 4.6 Before writing code

- Read the neighbouring code and match its patterns. Training memory of a library is a hypothesis: check the installed version and its own docs.
- Never port complex code with sed or bulk scripts.
- Read every AGENTS.md, CLAUDE.md and README warning literally, before the first line of relevant code.

### 4.7 Production and safety

- Never print or log a secret, environment value, database URL or database exception text. Log the exception class name only.
- No personal health information in logs: a patient ID is fine; name, email and medical detail are not.
- Ask the operator first for any of these:
  - live charges;
  - real emails or SMS to real customers outside the current task;
  - destructive production database operations (DELETE, DROP, TRUNCATE).
- Never create accounts or sign in on a production site.

### 4.8 Words

- The operator's ruling, 11 October 2026: "It doesnt matter for code or handover documents. Dash's are banned in SEO engine output and on websites." No em dash or en dash in any website text or SEO engine output.
- Medio's own patient-facing wording rules in its AGENTS.md apply.
- Reports to the operator are plain English:
  - short;
  - no internal codenames;
  - no commit hashes in the prose;
  - no tables of file paths when a sentence will do;
  - end-of-task summaries under about 120 words.

### 4.9 Working hours and delegation

- "Overnight" means until sunrise in the operator's local time (Brisbane/Sydney). Finishing a batch is not a reason to stop: start the next item.
- Delegated work must meet the same standard as your own. Use no lower-tier model for agent work.
- One agent per piece of work. Agents do not spawn agents.

## Operator check concurrency policy (10 October 2026)

The operator explicitly instructed: "Update to permit simultaneous checks."
This policy applies to Codex and Claude across all current and future
operator-owned projects and workspaces. It supersedes older instructions
requiring only one heavy local verification process. The daily release train,
required checks, source preservation and deployment rules remain binding.

- Run independent checks simultaneously when their dependencies and resources
  are isolated. Different Git branches isolate source files; they do not isolate
  CPU, memory, databases, ports or generated artifacts. Validate each frozen
  release against one integrated source revision and exact input manifest.
- Permit at most two heavy local check groups across the machine. Admit groups
  atomically using PID/start-bound ownership leases and declared memory
  reservations. The combined local reservation budget is at most8GiB and
  at most half the host's physical RAM, with at least4GiB host headroom and
  any stricter measured host-pressure limit. A large check may reserve the
  whole budget. Lightweight isolated checks may overlap within that budget.
- Count complete owned process trees, servers and PostgreSQL/background groups
  in capacity monitoring, including reparented descendants. RSS sampling is an
  observation rather than a kernel memory guarantee. Refuse excess admission;
  cleanly stop owned groups on pressure, capacity, timeout, signal or drift.
  Never kill another owner's process or reclaim an ambiguous lease. Reclaim a
  stale lease only after PID/start and every owned group are proved absent.
- Give each concurrent group separate databases/schemas, ports, temporary
  directories, caches, outputs and dependency/build artifacts. Keep locked
  installation, Prisma/contracts/generated source, migrations, shared .next
  builds and actual dependency chains sequential. Complete source/fixture/
  vocabulary/schema and exact test-collection preflight before heavy lanes.
  Shared Hub database seed, integration and customer checks retain their chain.
- Preserve the full required test set, including every database-marked security
  case. Prove exact collected test-ID ownership with no missing or duplicated
  cases. Freeze source while checks run. A failed, missing, cancelled, drifted
  or partially completed parallel group cannot produce a complete pass.
- Preserve per-stage outcomes, resource ownership, exact-source proof, CPU time
  and whole elapsed time. Reused successful checks must be labelled as reused.
  Measure savings before claiming a percentage; parallelism alone proves no
  reduction in runtime or cost.
- Hosted CI may run independent required jobs in parallel within the same
  admitted frozen train. Do not trigger extra workflows, paid workers, preview
  builds or Railway/Vercel deployments merely to gain concurrency. Parallel
  checks do not authorize parallel releases or extra daily release trains.

## This computer's release role

These rules supersede conflicting older instructions below. This computer banks
non-critical work only. Open no pull request when it would start hosted checks,
and never merge to main or deploy unless the operator explicitly appoints this
session as integrator for that exact release. Inspect triggers before every
push. Use codex/<topic>-<yyyymmdd> branches. Include rules-only changes with real
code, never in an independent release. If a branch push starts hosted work,
keep the commit local and report the blocking configuration to the operator.

## Preserved project guidance

The full operator rules and concurrency policy above govern this project.
They supersede conflicting older limits, sequential-check requirements,
release instructions and worktree cleanup instructions below. Preserve all
compatible project-specific safety rules. Project dependency chains remain
sequential when they share resources; independent isolated checks run together.
