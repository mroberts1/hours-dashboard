# hours-dashboard

Weekly dashboard of Martin's teaching hours vs driving hours, Fall 2026
semester (16 weeks, starting Mon 31 Aug 2026). Live at
https://mroberts1.github.io/hours-dashboard/ (GitHub Pages, branch `main`).

## Files

- `index.html` is the whole app: HTML, CSS, JS and data in one file.
  No build step, no dependencies. Only external fetch is the Inter font.
- Data lives in the `const DATA = {...}` line inside the `<script>`.
  `DATA.master` is the totals card, `DATA.weeks[]` has one entry per week.

## Workflow

- Martin opens `index.html` in Safari and refreshes (Cmd+R) after each edit.
  Keep it a single self-contained file so that stays true.
- Commit and push only when Martin asks. Pages updates about a minute later.
- Exception to the usual "never push to main" rule: this repo has no PR
  flow and GitHub Pages deploys from `main`, so push straight to `main`.
- This repo is the master copy. Another agent (Hermes) also edits it, so
  `git pull` before starting work.
- Use semantic commit prefixes (`feat:`, `fix:`, `chore:`).

## Data model (per week)

- `teaching[]`: one row per course. `actual` = hours taught, `base` = hours
  scheduled that week. Colour is per row.
- `driving[]`: one row per route, same fields plus `trips`.
- `stats[]`: Taught, Driven, and a grey running tally
  (`cum: true`, `v` = taught to date, `v2` = driven to date).
- `badge`: short red note for unusual weeks (e.g. "Labor Day"). Optional.
- Hours are decimal (1.75 = 1h45). Display via `fmt()` as `1h45`.
- The totals card's `base` values are the sum of the weekly `base` values.

## Design decisions (settled, ask before reversing)

- One card per tab; arrow keys move between cards. First tab = totals.
- Teaching and Driving shown side by side, full width. Stacks under 1100px.
  There used to be a toggle; it was removed on purpose.
- Rings = each item's share of that week's teaching or driving hours.
- Grid shows hours done, large and coloured, then "of X" scheduled, small grey.
- "Scheduled" means what was scheduled that week, so short weeks (term start,
  holidays) read 100% when nothing was missed.
- Removed on purpose: a "semester runs 16 weeks" badge, a drive:teach ratio.

## Logging rules

- Weeks 1-5 are filled in. Week 1: term began Wed 2 Sep, one class per
  Emerson course, Boston trip Wed 2, Wachusett trip Thu 3, 5 Saxtons runs.
- Weeks 6 onward stay empty until Martin logs them. He sends a short note at
  the end of each week (Fri or Sat), e.g. "wk6: IN 206 cancelled Mon,
  Saxtons x4". Anything not mentioned happened as timetabled.

## Timetable

| Item                 | Days       | Per session      |
|----------------------|------------|------------------|
| IN 206 (Emerson)     | Mon + Wed  | 1h45 class       |
| VM 641 (Emerson)     | Mon + Wed  | 1h45 class       |
| VM 303 (Emerson)     | Tue + Thu  | 1h45 class       |
| COMM 2003 (Fitchburg)| Fri        | 1h15 class       |
| Boston drive         | Mon + Wed  | 3h00 round trip  |
| Wachusett MBTA drive | Tue + Thu  | 1h40 round trip  |
| Fitchburg drive      | Fri        | 1h40 round trip  |
| Saxtons River drive  | Mon-Fri    | 1h20 round trip  |

Saxtons "double Friday" weeks have 6 runs instead of 5.

## Open questions (don't guess, ask Martin)

- Tue 13 Oct and Tue 10 Nov: VM 303's schedule and the Mon/Wed courses'
  schedules disagree. Martin is checking.
- Vermont Academy calendar (affects Saxtons runs from week 13): unknown.
- Known design nits Martin hasn't ruled on yet: ring colours (red/blue) are
  reused with a different meaning in the bottom split bar; "over schedule"
  is only shown in small text.

## Style

- Dark theme, CSS variables at the top of `<style>`. Match existing style.
- No em dashes in any visible text.
