# Self-Maintaining Karpathy-Style Wiki

A universal, **model- and harness-agnostic** pattern that turns any coding project into a project that *remembers*. Once integrated, your AI agent (any agent) automatically maintains a living Obsidian wiki while it codes:

- a **prompt ledger** — one row per request you make, with a one-line result; failures are never silently dropped;
- **Systems pages** — one wiki page per system, written *on the fly as the system is built*, capturing your intent, the rules, the decisions, and what was tried and rejected;
- a **Wiki Home** — the entry point that makes any fresh agent (or you, months later) productive in minutes.

> The wiki is the brain. The model is temporary compute.

No Obsidian plugins required. No vendor lock-in. Plain Markdown and `[[wikilinks]]` only.

## How it works

The enforcement mechanism is your project's **agent instruction file** (`AGENTS.md`, `CLAUDE.md`, `.cursorrules`, `GEMINI.md`, or whatever your harness reads). This repo gives you a proven section to paste into it that obligates every future agent session to:

1. Read the wiki (`Wiki Home.md` + latest ledger rows) before working.
2. Write one ledger row per prompt, immediately, in a fixed format.
3. Create/update the Systems page for anything it builds, in the same session.
4. Run a memory pass at session end.

Because the rules live in the instruction file — not in a plugin, prompt, or product — they work with Claude Code, ZCode, Cursor, Codex, Aider, or a raw LLM with file access.

## Quick start (any harness, any model)

1. Copy [`INJECT-AGENTS.md`](INJECT-AGENTS.md) into your project.
2. Rename `<Project> - Wiki` placeholders to your project's display name.
3. Append its contents to your agent instruction file (`AGENTS.md`, `CLAUDE.md`, etc.). If your project has no such file, the appended text *is* the file.
4. Copy the three files from [`templates/`](templates/) into a new `<Project> - Wiki/` folder at your repo root, renaming `<Project>` accordingly.
5. Tell your agent: *"Read AGENTS.md and follow the wiki mandate."* From then on the wiki maintains itself — and backfill the ledger with your current session's requests.

Open `<Project> - Wiki/` as your Obsidian vault. Done.

## Quick start (harnesses with a skills system)

If your harness supports the `SKILL.md` skill convention, copy [`skills/karpathy-wiki/`](skills/karpathy-wiki/) into your skills directory and invoke the `karpathy-wiki` skill in the target project; it performs all the steps above for you (survey, scaffold, injection, backfill).

## What you get in practice

- **Compounding development**: every session starts from accumulated knowledge instead of zero context.
- **A babysitting-detector**: the ledger is one page you can scan in a minute — a missing row means your agent skipped the rule.
- **Honest history**: results are never rewritten; late corrections are appended as `UPDATE (date):` notes.
- **Intent that survives**: Systems pages quote *your* requests, so future agents know why code is the way it is — and what was already tried and rejected.

## Repository layout

```
INJECT-AGENTS.md                  The agent-instruction mandate (the core artifact)
templates/Wiki Home.md            Entry-point template
templates/PROMPT-LEDGER.md        Ledger template with its format rules
templates/System Page.md          Per-system page template
skills/karpathy-wiki/SKILL.md     Optional skill wrapper that automates integration
REFERENCE.md                      Pointers to the living reference implementation
```

## License

MIT — do whatever you want; attribution appreciated.
