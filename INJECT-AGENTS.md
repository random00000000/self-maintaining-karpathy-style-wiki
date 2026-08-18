# Agent Instruction Mandate — paste into your AGENTS.md / CLAUDE.md / .cursorrules

> Replace `<Project>` with your project's display name (e.g. `Victory Marche`).
> Append this section to your agent instruction file. If none exists, this file becomes it.
> Keep every mandate intact when adapting wording to your project.

---

## Persistent Project Wiki (Wiki Brain)

Development must compound across sessions. The wiki is the brain; agent sessions are temporary compute. The wiki lives in `<Project> - Wiki/` as plain Obsidian-compatible Markdown with [[wikilinks]] — the human opens that folder as their Obsidian vault.

### Session startup

Before non-trivial work, read the wiki's `Wiki Home.md` and `PROMPT-LEDGER.md` (latest rows = latest intent), plus only the Systems pages the task touches. Load the smallest context that is sufficient.

### Prompt ledger (mandatory, every prompt, immediately)

Every single human prompt gets its own row in `<Project> - Wiki/PROMPT-LEDGER.md`, written immediately when the work for that prompt is finished — never batched to the end of a session. No exemptions for small prompts, bug reports, questions, or meta-requests. The ONLY exception is an explicit instruction from the human to not log that specific prompt. Prepend new rows at the top of the table (latest first). Every row records a Model column naming the exact agent/harness that did the work (e.g. "Claude Sonnet 5", "Codex", "Z Code") — always filled in, never blank, never guessed on the human's behalf, and never relabeled by a different model later. One-line results only. Notes are split into AI Notes (written by whichever model worked the row) and Human Notes (written only by the human — an agent never writes there). Failures are never silently dropped; late changes are `UPDATE (date):` notes appended to AI Notes (or Human Notes for the human's own follow-up), never rewrites.

### Systems wiki (build it while you build the system)

Whenever a system is created or substantially extended, create or update `<Project> - Wiki/Systems/<System>.md` IN THE SAME WORK SESSION — never as a deferred backlog item. Capture: the human intent (quote the request, link the ledger row), how it works (rules, constants, file references), decisions with "revisit if" conditions, what was tried and rejected, and open edges.

### During work: capture as you go

When important information appears naturally — the human says something feels wrong, a test reveals a problem, an approach fails, an assumption breaks — update the relevant wiki page without being asked. Label knowledge honestly (FACT / OBSERVATION / HYPOTHESIS / DECISION / QUESTION). Speculation becomes fact only through evidence, never repetition.

### End of every session: memory pass

Before finishing meaningful work: ensure every prompt from the session is in the ledger; ensure the Systems pages for anything touched are current; keep `Wiki Home.md` links accurate; merge or delete stale material. Skip only for trivial sessions — when in doubt, do the pass.

### Principles

- Memory means integration, not storage: an observation must change a page or the ledger, not sit in a transcript.
- Notes are distilled meaning, never conversation dumps.
- Minimal change: update one existing paragraph over creating three new files.
- Never rewrite ledger rows or history; append updates.

The test: a completely fresh session reading only `Wiki Home.md` and `PROMPT-LEDGER.md` should know what exists, what was tried and rejected, what is being built now, and what to do next — without the human reconstructing context.
