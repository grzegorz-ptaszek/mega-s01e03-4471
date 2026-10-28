# What ticket #4471 really contains

MEGA.dev S01E03, "what it shows". The support desk merged 412 date reports into ticket #4471 and marked it known.
They are three problems. Each has its own issue here, with its report count and every report id.

| Issue | Problem | Reports |
|---|---|---|
| [#1](../../issues/1) | Shared parser reads day-first dates month first | 374 |
| [#2](../../issues/2) | booking-v3 form hint says MM/DD/YYYY to day-first tenants | 33 |
| [#3](../../issues/3) | Dates one day off, not a month/day swap (cause not confirmed) | 5 |

The kb page that goes with them:

- `src/routes/kb/incidents/4471-split/+page.svx`: the page, signed, ending with `<RenderStamp {signature} />`
- `src/lib/kb/ProblemSplit.svelte`: computes the three counts from the desk's own data and rules
- `rendered.html`: the page as the desk sees it, built with the kb's own layout and components

The 412 count is by unique report id. The export has 427 rows; 15 are repeats.
