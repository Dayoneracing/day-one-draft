# CLAUDE.md — D1 Stables

You are building **D1 Stables**, Day One Racing's free fantasy horse racing game. The owner is Tadgh: he is not a professional developer, so explain decisions in plain English, keep him informed in short updates, and ask before anything irreversible or that costs money.

## Read first, every session

1. `SPEC.md` — game rules, scoring, prices, data plan, build phases. The source of truth.
2. `BRAND.md` — fixed brand rules. Every screen follows them.

If the spec and a request conflict, ask Tadgh which wins, then update `SPEC.md`.

## Stack

- Next.js (App Router) + TypeScript, Tailwind CSS with the BRAND.md tokens, mobile-first, PWA-installable.
- Supabase: Postgres, Auth (Apple, Google, email magic link), row-level security on every table, scheduled functions for jobs.
- Vercel hosting. GitHub for code.

## Non-negotiables

- **Scoring and price engines are pure, framework-free TypeScript modules** with unit tests (Vitest). The worked examples in SPEC.md are mandatory test cases.
- **One results adapter interface.** Implementations: `ManualResults` (admin page) now, `RacingApiResults` later. Nothing else in the app knows where results come from.
- Never scrape websites for racing data.
- No odds, betting language, bookmaker links, prizes or in-app chat.
- Secrets only in environment variables, never committed.
- Use the frontend-design skill for all UI work. Avoid generic AI-looking UI: no default purple, no stock gradients, no emoji UI, no cards-inside-cards.
- Small, reviewable commits with clear messages.

## Working style

- Plan briefly before each phase, then build. Show Tadgh a running preview after each meaningful UI change.
- Run tests and typecheck before saying something works.
- Keep `SPEC.md` "Decision status" and "Open questions" up to date when Tadgh decides something.
