# D1 Stables — Game Rules & Build Spec

Version: 9 Oct 2026 · Owner: Tadgh (Day One Racing)

## Overview

D1 Stables is Day One Racing's free fantasy racing game: players buy a stable of 10 real horses with a £15m budget, score points when they run, and compete against mates in private leagues across a full Flat season.

- **Its job:** recruitment. It gives young fans a reason to care about racing every week and pulls them towards Day One membership and paid Racedays.
- **What it is not:** a betting product. It is free to play, with no prizes, ever.
- **Format:** classic pick-any (like Fantasy Premier League). Any number of players can own the same horse.
- **Name:** D1 Stables. D1 reads as Day One and Division One. Can be changed later.

## Decision status

| Area | Status | Decision |
| --- | --- | --- |
| Format | Agreed | Pick-any, price per horse, team budget |
| Prices | Agreed | Real bloodstock-style values; prices move during the season |
| Scoring | Agreed | Placings, percentile bands, run points, race-level multipliers, winning-margin bonus |
| Coverage | Agreed | All UK and Ireland runs (all-weather included); France Group and Listed only; Arc weekend entered manually |
| Gameweek | Agreed | Saturday to Friday; deadline 11am Saturday |
| Pool | Agreed | About 100 horses; about 10 added each month |
| Injured or retired horse | Agreed | Free replacement transfer |
| Eligibility | Agreed | 18+, self-declared, no ID checks |
| Login | Proposed | Apple, Google and email-link sign-in |
| Squad, budget, transfers, captain detail | Proposed | See Game format |
| Price movement formula | Proposed | See Price movement engine |
| Dermot's horse | Parked | Left out of the game for now |
| Club horse slot | Parked | Optional setting, off by default |
| Divisions with promotion and relegation | Later | Season 2 |
| Native App Store app | Later | Web app first; wrap later |

## Game format

| Rule | Setting |
| --- | --- |
| Squad size | 10 horses |
| Budget | £15,000,000 at the start of the season |
| Same-trainer limit (proposed) | Max 3 horses from one trainer |
| Gameweek | Saturday to Friday; every run in that window counts |
| Deadline | 11:00 UK time each Saturday; transfers and captain lock |
| Free transfers | 1 per gameweek; unused ones bank, up to 2 |
| Extra transfers | −4 points each |
| Captain | Picked each gameweek; scores double that week |
| Vice-captain (proposed) | Takes the double if the captain doesn't run that week |
| Injured or retired horse | Free replacement transfer once the news is confirmed |
| Selling price | Current market price (no FPL-style profit cut) |
| Joining late | Players can join any time; they start from zero with the full £15m |

A new player's first squad is free to build; transfer rules only apply from their first deadline onwards.

## Horse pool and prices

| Tier | Horses | Price range | Role in the game |
| --- | --- | --- | --- |
| Group 1 stars | ~10 | £3m–£6m | Glamour and big-day points; run rarely |
| Group 2/3 and Listed | ~15 | £1m–£3m | Solid pattern-race scorers |
| Top handicappers (rated 90–105) | ~35 | £400k–£1m | Heritage handicaps; regular points |
| Handicappers (rated 75–90) | ~40 | £150k–£400k | Frequent runners; the value picks |

- **Selection:** Tadgh picks the pool by hand, favouring horses expected to run often. Opening prices set by Tadgh.
- **Price steps:** nearest £10k (shown e.g. £2.45m). Floor £100k.
- **Monthly additions:** about 10 horses added each month.
- **Horse info in the app:** name, age, sex, trainer, jockey where known, official rating, recent form, next declared run, current price and price history, % of players who own it.
- **Notes:** optional. Tadgh's picks come mainly through video; the app can link to them.
- **Disclaimer in the rules:** prices are game prices, not valuations of any horse.

## Scoring rules

Every run scores: base points for finishing position, plus any winning-margin bonus, then × race level × 2 if captain.

**Base points** (single highest band it qualifies for, plus the run point)

| Result | Points |
| --- | --- |
| Ran | 1 |
| Finished in the top 75% of runners | +1 |
| Finished in the top 50% of runners | +2 (instead of the +1) |
| 4th | +4 (instead of the band) |
| 3rd | +6 |
| 2nd | +9 |
| Won | +15 |

**Small-field rule:** 4th only pays in races of 8+ runners and 3rd only in 5+. Otherwise the horse falls back to its percentile band.

**Winning-margin bonus** (winners only, before multipliers): 2 lengths or more +2; 5 lengths or more +4 (instead of +2).

**Race-level multipliers:** Group 1 ×2.5 · Group 2 ×2 · Group 3 ×1.6 · Listed ×1.3 · all other races ×1.

**Formula:** points = (run + finish + margin) × race level × captain

**Worked examples (use as unit tests)**

| Run | Calculation | Points |
| --- | --- | --- |
| Wins a Group 1 by 3 lengths | (1 + 15 + 2) × 2.5 | 45 |
| Same, as captain | 45 × 2 | 90 |
| 2nd in a 12-runner Listed race | (1 + 9) × 1.3 | 13 |
| 4th of 6 in a Class 4 handicap | 4th doesn't pay under 8 runners; top 75% → 1 + 1 | 2 |
| 7th of 14 in a Class 2 handicap | Top 50% → 1 + 2 | 3 |
| 13th of 14 | Ran only | 1 |

**Edge cases**

- Non-runners: 0 points.
- Pulled up, fell, unseated, refused to race: 1 point (ran) only.
- Dead heats: each horse gets the full points for that place.
- Disqualifications and amended results: the official result at 22:00 UK time on race day is final.
- Runner count: horses that actually started, not the declared field.

## Price movement engine

Prices update once a week after the Friday close, from form and demand, capped at ±10% a week.

**1. Form move (tunable)**

| Result that gameweek | Price change |
| --- | --- |
| Won | +6% |
| Placed 2nd–4th (paying place) | +3% |
| Top 50% | 0% |
| Bottom 50% | −3% |
| Last, pulled up or fell | −5% |
| Didn't run | 0% |

In Group and Listed races the form move is multiplied by the race-level multiplier (a Group 1 win = +15% before the cap). Two runs in a week: moves add up.

**2. Demand move:** 0.5 × net transfers in as % of active stables, capped at ±4%.

**3. Combined:** total = form + demand, capped ±10%; rounded to nearest £10k; floor £100k; admin can freeze or set any price; every change logged for price history.

## Race coverage and results data

- **UK and Ireland:** all runs count, turf and all-weather.
- **France:** Group and Listed runs only. Arc weekend can be entered manually.
- **Season:** the whole British Flat season.

**Data source plan**

1. Build stage: test data plus a manual results page. No paid data needed to build.
2. Pool building: one month of The Racing API paid plan for ratings and run histories.
3. Live season: The Racing API polled every evening. Free tier tested first.
4. Fallback, always: the manual results page.

All results go through ONE results layer (adapter interface) so the source can change without a rebuild.

**Rules on data**

- No scraping the Racing Post or any other site (racing data carries database right).
- Confirm with The Racing API before launch that a free public game is within their terms.
- Results are stored in our own database; the app never calls the data provider from players' phones.

## Leagues, accounts and eligibility

**Leagues**

- Overall table: every stable, ranked by total points; weekly and season rankings.
- Private leagues: anyone can create one; 6-character join code and share link; no limit per player.
- League views: season table, this gameweek's table, each rival's stable after the deadline.
- Later (Season 2): divisions with promotion and relegation.

**Accounts**

- Sign-in with Apple, Google or an email link (no passwords).
- Profile: display name, stable name, date of birth, marketing opt-in (unticked by default).
- One stable per account.

**Eligibility and safety**

- 18+: date of birth and confirmation tick at sign-up. No ID checks.
- No in-app chat or messaging in Season 1.
- Stable and league names pass a profanity filter; admin can rename or remove any name.
- Report button on names, plus a contact email.
- Privacy policy and terms of play published before launch.

## Tech stack

| Part | Tool |
| --- | --- |
| Code | GitHub (private repo) |
| App | Next.js + TypeScript, mobile-first, installable (PWA) |
| Database and logins | Supabase (Postgres + Auth with row-level security) |
| Scheduled jobs | Supabase scheduled functions: nightly results import, weekly price update |
| Hosting | Vercel (subdomain e.g. play.dayoneracing.com) |
| Emails | Brevo |
| Native app (later) | Capacitor wrap |

## Build phases

1. **Foundations:** repo, database design, sign-in, test horse data.
2. **Game engine:** scoring, small-field rule, multipliers, captain and vice-captain, price engine; unit-tested against the worked examples.
3. **Player app:** pick stable within budget, transfers, captain, deadline lock, horse pages, overall and private league tables.
4. **Admin:** manual results entry, pool management, price overrides, name moderation.
5. **Live data and test:** The Racing API import, then 2–3 weeks with 10–20 friends; tune; launch.

## Legal guardrails

- Free to play, no prizes, no entry fee. Any change needs a legal check first.
- No inside information in picks, videos or notes: public form only.
- Game picks, not betting tips; no bookmaker links; no odds anywhere in the app.
- No in-app chat in Season 1 (Online Safety Act).
- No scraped data.

## Open questions

- [ ] Confirm sign-in: Apple, Google and email link?
- [ ] Accept same-trainer limit (max 3)?
- [ ] Accept vice-captain?
- [ ] Email The Racing API to confirm a free public game is allowed.
- [ ] Check "D1 Stables" on the UK IPO trademark database before merch.
