# Reference Implementation

The reference for this pattern is this repository itself:

- [`INJECT-AGENTS.md`](INJECT-AGENTS.md): the "Persistent Project Wiki (Wiki Brain)" mandate that goes into a project's agent instruction file.
- [`templates/Wiki Home.md`](templates/Wiki%20Home.md): the entry point, with identity and links.
- [`templates/PROMPT-LEDGER.md`](templates/PROMPT-LEDGER.md): the ledger, with its format rules.
- [`templates/System Page.md`](templates/System%20Page.md): the per-system page.

What a healthy integration looks like after a day of work:

- The ledger has one row per human request, with the exact prompt, including honest PARTIAL and FAILED entries, `UPDATE (date):` notes, and a Model column that shows which agent or harness did each row.
- `Systems/` has a page for each system touched that day, written in the same session the system changed, with intent, decisions, and what was tried and rejected.
- `Wiki Home.md` links every page, and a fresh session reading only it and the ledger knows what exists and what comes next.

Agents: do not open other local projects as examples. Each project's wiki belongs to that project alone.
