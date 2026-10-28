booking-v3 form hint says MM/DD/YYYY to day-first tenants (33 reports)

**Reports covered: 33**

**Problem.** The booking-v3 form prints `MM/DD/YYYY` under its date field. People at day-first tenants type what the hint tells them, month first, and the form reads it their way. The date is wrong from the first keystroke. This is not the parser bug: fixing the parser does not fix it.

**How it is told apart.** Channel is `form`, and the tenant runs booking-v3. Only three tenants do: alder.physio (12), copper.studio (11), pale.harbour (10). Every report from these three tenants through the form is here; their app and email reports belong to the parser issue.

- First report 2026-04-17, last 2026-09-22
- Intake tags: hint ×18, parser ×15. 15 of the 33 were tagged `parser` and merged into #4471, where this problem has no ticket of its own.

**Fix direction.** Show the tenant's own date order in the hint, or have booking-v3 read day first for day-first locales.

<details><summary>Report ids (33)</summary>

R-41230, R-41241, R-41251, R-41259, R-41262, R-41275, R-41294, R-41305, R-41308, R-41366, R-41372, R-41384, R-41387, R-41396, R-41400, R-41406, R-41415, R-41416, R-41418, R-41428, R-41439, R-41441, R-41449, R-41453, R-41456, R-41460, R-41472, R-41485, R-41493, R-41539, R-41572, R-41582, R-41584

</details>
