---
name: karpathy-wiki
description: Inject a persistent wiki-brain note-taking pattern into any project - a per-prompt ledger, an Obsidian wiki named "<Project> - Wiki" with a Wiki Home and on-the-fly Systems pages - by writing the project's AGENTS.md so every future agent always maintains and updates the wiki while coding. Use when the user asks to add wiki orchestration, a prompt ledger, living documentation, or a "karpathy wiki brain" to a project.
---

# Karpathy Wiki Skill

## Purpose

Turn a code repository into a project that *remembers*. When integrated, the project carries:

1. **A wiki folder named `<Project> - Wiki`** (e.g. `Victory Marche - Wiki/`) so a human can open it directly as an Obsidian vault — no hunting inside the repo.
2. **A `Wiki Home.md`** — the established entry point with project identity and links.
3. **A `PROMPT-LEDGER.md`** — one row per human request, one-line result, failures never dropped.
4. **`Systems/<Name>.md` pages** — one per built system, written **on the fly while the system is built**, capturing intent, rules, decisions, and rejections.

The enforcement mechanism is the project's **AGENTS.md**: this skill writes a section into it that obligates every future agent session to maintain and update the wiki. The skill is universal and model-agnostic — plain Markdown, `[[wikilinks]]`, no Obsidian plugins, no vendor lock-in.

## Core philosophy

> The wiki is the brain. The model is temporary compute.

- Memory means **integration, not storage**: an observation must change a wiki page or the ledger, not sit in a transcript.
- Notes are **distilled meaning**, never conversation dumps.
- **Minimal change**: update one existing paragraph over creating three new files.
- **Compression**: merge duplicates, delete obsolete wording; the wiki becomes more coherent, not merely larger.
- Label uncertainty honestly (FACT / OBSERVATION / HYPOTHESIS / DECISION / QUESTION). Speculation becomes fact only through evidence.

## Main action 1: `integrate` — inject the pattern into a project

### 1. Survey before writing

- Read the project's `AGENTS.md` if it exists; preserve its content and voice. Never destroy existing instructions — merge.
- Check for existing wiki/docs folders. If a wiki or ledger already exists, adapt this pattern around it and reconcile rather than duplicate. Ignore or archive stale artifacts from other patterns rather than importing them.

### 2. Create the wiki scaffold

Folder name: **`<Project> - Wiki`** at the repo root, using the project's display name.

```
<Project> - Wiki/
  Wiki Home.md      # entry point: identity, links to ledger + Systems pages, how-this-wiki-works
  PROMPT-LEDGER.md  # one-page ledger of every human request
  Systems/          # one page per built system (Main action 2)
```

**`Wiki Home.md` template:**

```markdown
# <Project> — Wiki Home

> The wiki is the brain. Agent sessions are temporary compute.
> Open this folder (`<Project> - Wiki/`) as your Obsidian vault and start here.

## What this project is

<One honest paragraph: what it is, for whom, the core fantasy or purpose.>

## Always-current pages

- [[PROMPT-LEDGER]] — every human request with a one-line result. Read this first to get familiar with intent.
- [[Systems/<First System>|<First System>]] — <one-line description>
- <one link per Systems page, with a one-line description>

## How this wiki works

- Plain Markdown and [[wikilinks]] only — no Obsidian plugins required.
- Systems pages are written on the fly as systems are built, never retroactively. When a system changes, its page changes in the same session.
- Requests and outcomes go to [[PROMPT-LEDGER]] immediately; distilled knowledge goes to the relevant system page; nothing here is a conversation dump.
- Uncertainty is labeled (FACT / OBSERVATION / HYPOTHESIS / DECISION / QUESTION); speculation never becomes fact by repetition.
```

**`PROMPT-LEDGER.md` template:**

```markdown
# <Project> — Prompt Ledger

A running ledger of every human request, newest at the TOP — prepend new rows,
with a one-line result and which model did the work. One page: what was asked,
what worked, what failed, and by whom.

Format rules:
- One row per request. Quote or tightly summarize; never invent content.
- Model: the exact agent/harness that did the work (e.g. "Claude Sonnet 5",
  "Codex", "Z Code"). Always filled in — never blank, never guessed on the
  human's behalf, never relabeled by a different model later.
- Results are ONE LINE. Details live in the Systems pages, never here.
- Result states: DELIVERED / DELIVERED (unverified) / PARTIAL / FAILED / DECLINED / DISCUSSION.
- AI Notes: written by whichever model worked the row. Human Notes: written
  only by the human — an agent must never write into that column.
- Never silently drop a failure.
- Late updates: append `UPDATE (date): ...` to AI Notes (or Human Notes, if
  it's the human's own follow-up); never rewrite the row.

| Date | Model | Request | Result (one line) | AI Notes | Human Notes |
|------|-------|---------|--------------------|----------|--------------|
```

Backfill the ledger with every request from the current session before finishing.

### 3. Write the wiki mandate into the project's AGENTS.md (the load-bearing step)

Append (or merge into an existing memory/docs section) the section below. Adapt wording to the project; keep every mandate intact. This is what makes all *future* agents maintain the wiki.

```markdown
## Persistent Project Wiki (Wiki Brain)

Development must compound across sessions. The wiki is the brain; agent
sessions are temporary compute. The wiki lives in `<Project> - Wiki/` as plain
Obsidian-compatible Markdown with [[wikilinks]] — the human opens that folder
as their Obsidian vault.

### Session startup
Before non-trivial work, read the wiki's `Wiki Home.md` and
`PROMPT-LEDGER.md` (latest rows = latest intent), plus only the Systems pages
the task touches. Load the smallest context that is sufficient.

### Prompt ledger (mandatory, every prompt, immediately)
Every single human prompt gets its own row in
`<Project> - Wiki/PROMPT-LEDGER.md`, written immediately when the work for
that prompt is finished — never batched to the end of a session. No exemptions
for small prompts, bug reports, questions, or meta-requests. The ONLY
exception is an explicit instruction to not log that specific prompt. Prepend
new rows at the top (latest first). Every row records a Model column naming
the exact agent/harness that did the work — always filled in, never blank,
never guessed on the human's behalf, and never relabeled by a different model
later. One-line results only. Notes split into AI Notes (written by whichever
model worked the row) and Human Notes (written only by the human — an agent
never writes there). Failures are never silently dropped; late changes are
`UPDATE (date):` notes appended to AI Notes (or Human Notes for the human's
own follow-up), never rewrites. **Multiple human messages can land inside one
continuous agent turn** — Claude Code surfaces a follow-up, correction, or new
request mid-task via a system-reminder ("This is how Claude Code surfaces
messages the user sends mid-turn...") rather than waiting for a reply first.
Treat every arrival as its own prompt boundary: write the row for whatever the
prior prompt's work has reached at that moment — even if only partial or
discussion-only — before continuing into the new request. Do not defer
everything to one merged end-of-task wrap-up; that is exactly how rows get
forgotten.

### Systems wiki (build it while you build the system)
Whenever a system is created or substantially extended, create or update
`<Project> - Wiki/Systems/<System>.md` IN THE SAME WORK SESSION — never as a
deferred backlog item. Capture: the human intent (quote the request, link the
ledger row), how it works (rules, constants, file references), decisions with
"revisit if" conditions, what was tried and rejected, and open edges.

### During work: capture as you go
When important information appears naturally — the human says something feels
wrong, a test reveals a problem, an approach fails, an assumption breaks —
update the relevant wiki page without being asked. Label knowledge honestly
(FACT / OBSERVATION / HYPOTHESIS / DECISION / QUESTION).

### End of every session: memory pass
Before finishing meaningful work: ensure every prompt from the session is in
the ledger; ensure the Systems pages for anything touched are current; keep
`Wiki Home.md` links accurate; merge or delete stale material. Skip only for
trivial sessions — when in doubt, do the pass.

The test: a completely fresh session reading only `Wiki Home.md` and
`PROMPT-LEDGER.md` should know what exists, what was tried and rejected, what
is being built now, and what to do next — without the human reconstructing
context.
```

### 4. Report

Tell the human exactly what was created/changed, which folder to open in
Obsidian (`<Project> - Wiki/`), and that the ledger's completeness is their
babysitting-detector: a missing row means an agent broke the AGENTS.md rule.

## Main action 2: systems documentation on the fly

While coding any system with identity (a gameplay system, a pipeline, a
service — anything with rules and history), maintain its page:

```markdown
# <System>

## Intent
What the human wants this to be, in their words where possible.
Link the originating request: see [[PROMPT-LEDGER]] rows dated <dates>.

## How it works
Current behavior, key rules and constants, with file references.

## Decisions
Durable choices, each with reasoning and a "revisit if" condition.

## Tried and rejected
What failed and why — so it is never silently retried.

## Open edges
Known limits and deferred questions.
```

Rules:

- Create the page in the same session the system is born; update it whenever
  behavior changes. A Systems page that lags the code is a bug.
- Intent quotes come from the ledger/human, never invented.
- Keep each page scannable — a few hundred words, not manual size.

## Behavioral contract for the agent running this skill

- ALWAYS append to the ledger unless the human explicitly says not to.
- ALWAYS fill in the Model column with your own exact name/harness — never
  leave it blank, never guess it on the human's behalf, never relabel a row
  another model wrote.
- ALWAYS write your own commentary into AI Notes, never into Human Notes —
  that column belongs to the human only.
- ALWAYS treat a mid-turn interjection (a new human message arriving while
  you're still working a prior one — Claude Code delivers these via
  system-reminder) as its own prompt boundary. Log the prior prompt's row
  before absorbing the new request, not after the whole chain finishes.
- NEVER rewrite ledger rows; append `UPDATE (date):` notes.
- NEVER batch ledger writes; write per prompt, immediately.
- NEVER create a wiki page when an existing section would do.
- NEVER ship conversation transcripts; distill.
- When the pattern conflicts with an existing project convention, surface the
  conflict to the human instead of silently overriding.

## Reference implementation

This exact pattern runs in VictoryMarche
(`C:\Users\javie\OneDrive\Documents\ChatGPT\VictoryMarche`): see its
`AGENTS.md` "Persistent Project Wiki" mandate, the `Victory Marche - Wiki/`
folder (Wiki Home, PROMPT-LEDGER, populated Systems pages). It is the living
example of the intended result.
