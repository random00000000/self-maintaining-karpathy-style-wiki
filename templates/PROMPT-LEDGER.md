# <Project> — Prompt Ledger

A running ledger of every human request, newest at the TOP — prepend new rows,
with a one-line result. One page: what was asked, what worked, what failed.

Format rules:
- One row per request. Quote or tightly summarize; never invent content.
- Results are ONE LINE. Details live in the Systems pages, never here.
- Result states: DELIVERED / DELIVERED (unverified) / PARTIAL / FAILED / DECLINED / DISCUSSION.
- Never silently drop a failure.
- Late updates: append `UPDATE (date): ...` to a row's Notes; never rewrite the row.

| Date | Request | Result (one line) | Notes |
|------|---------|-------------------|-------|
