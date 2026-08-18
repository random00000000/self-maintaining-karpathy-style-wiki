# <Project> — Prompt Ledger

A running ledger of every human request, newest at the TOP — prepend new rows,
with a one-line result and which model did the work. One page: what was
asked, what worked, what failed, and by whom.

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
