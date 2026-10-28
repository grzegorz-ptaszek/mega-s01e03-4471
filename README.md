# What ticket #4471 really contains

MEGA.dev S01E03, "what it shows". The support desk merged 412 date reports into ticket #4471 and marked it known.
They are two problems. Each has its own issue here, with its report count and every report id.

| Issue | Problem | Reports | Outcome (engineering, 5 Oct) |
|---|---|---|---|
| [#1](../../issues/1) | Shared parser reads day-first dates month first | 379 | fixed (`fix(dates): parse dd/mm for eu locales`), closed as completed |
| [#2](../../issues/2) | booking-v3 form hint says MM/DD/YYYY to day-first tenants | 33 | won't fix (booking-v3 form retired), closed as not planned |

Five of the 379 parser reports read as a one-day move (not a month/day swap). The desk counts them with the parser, so #1 does too and lists them in a note. Issue #3 was an earlier split of those five and is withdrawn.

The kb page that goes with them:

- `src/routes/kb/incidents/4471-split/+page.svx`: the page, signed, ending with `<RenderStamp {signature} />`
- `src/lib/kb/ProblemSplit.svelte`: computes the counts from the desk's own data and rules
- `rendered.html`: the page as the desk sees it, built with the kb's own layout and components

The 412 count is by unique report id. The export has 427 rows; 15 are repeats.
