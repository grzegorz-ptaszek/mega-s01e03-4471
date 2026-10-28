Dates one day off, not a month/day swap (5 reports)

**Reports covered: 5**

**Problem.** These reports describe a date that is one day off, or a time that arrives wrong, not a month and day swapped. A parser that reads month first cannot explain them. The desk already sets the same five aside as "read as a one-day move" in `desk-notes.json`, and then counts them under the parser.

Quotes:
- R-41202: "Invite says Tuesday 12 May. Calendar says Monday 11 May."
- R-41209: "Every booking in June is one day off. Only June."
- R-41236: "The invite arrived before I made the booking."
- R-41344: "Client in Lisbon got Tuesday. Client in Toronto got Monday. Same meeting."
- R-41620: "Tuesday 6 October showed as Monday."

**Cause: not confirmed.** The quotes point at a time-zone or daylight-saving error (a date near midnight moves a day when the zone is applied twice). The export has no field that proves it. Needs an engineer to check how invite times are converted.

- First report 2026-04-02, last 2026-10-04
- Tenants: kettle.books (1), alder.physio (1), nine.lanterns (1), pale.harbour (1), lantern.row (1)
- Intake tags: parser ×5 (all five tagged `parser`)

<details><summary>Report ids (5)</summary>

R-41202, R-41209, R-41236, R-41344, R-41620

</details>
