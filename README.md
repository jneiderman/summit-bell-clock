# Summit Bell Clock

Web pages for the ScreenCloud footer at Summit School: the current-period display (`index.html`) and the weather box (`weather.html`). Hosted by GitHub Pages at **https://jneiderman.github.io/summit-bell-clock/**.

---

## Run an extended-homeroom day (2 minutes, works from a phone)

1. Open the override file for editing:
   **https://github.com/jneiderman/summit-bell-clock/edit/main/overrides.json**
   (sign in as `jneiderman` if prompted)
2. Add one line per date inside the braces, using `am` or `pm`. Keep the commas between lines:
   ```json
   {
     "_comment": "...",
     "2026-09-24": "am",
     "2026-10-02": "pm"
   }
   ```
   Format is `"YYYY-MM-DD": "am"`. Zero-pad the month and day. Past dates are ignored, so you can leave old ones in or delete them.
3. Click **Commit changes…**, then **Commit changes** again in the dialog.
4. Wait about 5 minutes. GitHub republishes the site (1–2 min) and the sign re-reads the file every 5 min. **No ScreenCloud publish is needed.**
5. Optional check: open https://jneiderman.github.io/summit-bell-clock/ on that day — it should show the extended times.

### Same-day emergency (need it in under a minute)

In ScreenCloud Studio → Channels → *September 26* → **Period** zone, add a new Link with the URL
`https://jneiderman.github.io/summit-bell-clock/?schedule=am` (or `?schedule=pm`), remove the regular "Summit Bell Clock" item, and Publish. Reverse it the next day. The `?schedule=` parameter overrides the JSON file.

---

## What each schedule shows

| Key | Card | Notable blocks on the sign |
|---|---|---|
| `regular` | Regular Day (default) | 47-min periods; short homerooms labeled PRE-LUNCH / POST-LUNCH / END OF DAY |
| `am` | AM Extended Homeroom | 8:35–9:30 shows **Homeroom** with EXTENDED MORNING above it; 41-min periods |
| `pm` | PM Extended Homeroom | 2:10–3:00 shows **Homeroom** with STUDENT SUPPORT MEETING above it; 41-min periods |

Weekends show "No School". Before 8:35 shows "Welcome"; between blocks "Passing"; after 3:00 "Dismissal". Lunch blocks show both teams (9/10 and 11/12).

---

## Change the bell times themselves

1. Edit `index.html`: https://github.com/jneiderman/summit-bell-clock/edit/main/index.html
2. Find the `SCHEDULES` block near the top of the `<script>`. Each line is
   `{ s: T(h,m), e: T(h,m), name: "..." }` using 24-hour times, e.g. `T(13,17)` = 1:17 PM.
3. Optional fields: `tag` (small yellow label above the name), `short` (used in the "Next:" line), `split: LR` or `RL` (two-team lunch/recess rows).
4. Commit. Live in about 2 minutes.
5. Keep block names to 8–9 characters ("Homeroom", "Period 7"). Longer names won't fit the 480×130 zone — put extra words in `tag` instead.

---

## A/B week box (automatic)

The Week zone shows **A Week / B Week** from `week.html`, computed from `week-config.json`. Nothing to schedule month to month.

Rules it follows:
- Alternates every calendar week from the anchor (`2026-08-31` = A).
- A week with some days off still counts (Labor Day week was B).
- A **full** week off (Mon-Fri) does not count; the rotation resumes where it left off.
- Sat/Sun it shows the coming week. During a week off it shows "No School" and when the next letter resumes.

**Once each summer** (takes 2 minutes):

1. Open https://github.com/jneiderman/summit-bell-clock/edit/main/week-config.json
2. Set `anchorMonday` to the first Monday of the new school year and `anchorLetter` to its letter.
3. Replace `weeksOff` with the Mondays of every full week off on the new school calendar (winter recess, February recess, spring break).
4. Commit. Live in about 2 minutes.

2026-27 weeks off already entered: `2026-12-28`, `2027-02-15`, `2027-03-22`.

---

## Where things live

| Thing | Location |
|---|---|
| Bell clock page | `index.html` → https://jneiderman.github.io/summit-bell-clock/ |
| Weather page | `weather.html` → https://jneiderman.github.io/summit-bell-clock/weather.html (Open-Meteo, no API key, Upper Nyack coordinates) |
| Day overrides (extended homeroom) | `overrides.json` |
| A/B week page + config | `week.html`, `week-config.json` → https://jneiderman.github.io/summit-bell-clock/week.html |
| ScreenCloud layout | Custom layout "Main + 4 Zone Footer": main 1920×950, footer 130 px tall, four 480 px zones — Time / Period / Weather / Week |
| ScreenCloud links | "Summit Bell Clock" (Period), "Summit Weather" (Weather), "Summit Week Letter" (Week), under Links |

The Studio preview caches web links for a few minutes; the players refresh on their own. If a zone looks stale in Studio, that's the cache, not the page.
