# D1 Stables — Brand rules for the app

Taken from the Day One Racing design brief (8 Oct 2026). These are fixed. Ask Tadgh before deviating.

## Feel

British racing heritage × modern members' club. Premium, understated, editorial, credible, young without trying.
References: The Gentlewoman, Monocle, Soho House print, Aimé Leon Dore lookbooks, Royal Ascot programmes stripped of fuss.
NOT: a startup template, a betting app, a neon "Gen-Z" brand, or a tweedy establishment site.

Test for every screen: would a 22-year-old who loves racing screenshot it and send it to the friend they go racing with?

## Colour tokens

| Token | Hex | Use |
| --- | --- | --- |
| navy | #1E2938 | Primary background |
| navy-deep | #151D28 | Depth, cards on navy |
| navy-line | #2E3B4F | Dividers, borders |
| champagne | #E7CC91 | Accent: wordmark, key numbers, active states, hairline rules |
| champagne-muted | #B8A77E | Secondary accent text |
| bone | #F4EFE3 | Light surfaces where needed |
| white | #FFFFFF | Body text on navy |

- No other hues. **No red or green** (they read as betting odds) — show price rises/falls with ▲/▼ and champagne vs muted, not red/green.
- No gradients beyond subtle navy → navy-deep. No neon, no gold foil.
- Never champagne text on white or bone.

## Type

- Display: **Cormorant Garamond SemiBold (600)** — headings, big numbers (points, prices), wordmark. Uppercase headings +4–8% tracking.
- Support: **Inter** — labels, body, tables, buttons. Uppercase small labels +12–18% tracking.
- Max two typefaces.

## Mark

Logo files are in `public/brand/` (all champagne artwork; `-navy` versions include the navy background):

| File | Use |
| --- | --- |
| `wordmark-horizontal.svg` | DAY ◆◆◆ ONE, transparent — headers on navy |
| `wordmark-horizontal-navy.svg` | Same on a navy panel — social/OG images |
| `logo-stacked-racing.svg` | DAY ONE / ◆◆◆ / RACING, transparent — splash, login |
| `logo-stacked-racing-navy.svg` | Same on navy — app icon source |
| `diamonds.svg` | The three diamonds alone — dividers, loading, favicon |
| `diamonds-navy.svg` | Diamonds on navy — favicon/app icon |

Use the SVGs as supplied; never redraw or retype the wordmark.

Champagne is `#E7CC91` (confirmed by Tadgh, matches the logo files).

- Wordmark: DAY ◆◆◆ ONE (three elongated vertical diamonds). The game wordmark: D1 STABLES with the three diamonds as a divider.
- Diamonds are a sign-off/divider/bullet — one cluster per screen, never a pattern.

## Layout

- Generous negative space; one focal point per screen.
- Racecard/programme cues: hairline champagne rules (1px), small-caps labels, course names, dates, race numbers.
- Asymmetric editorial layouts over centred templates.
- Mobile first.

## Words

- Short, declarative, insider. Bracketed sub-labels are a house device: e.g. TRANSFERS [ONE FREE THIS WEEK].
- Never use: odds, tips, "winners" as a selling word, profit, returns, invest, VIP, emojis in UI, exclamation marks.
- Say "picks", "stable", "runs", "points".

## Imagery

- No photos of named horses unless licensed. No AI-generated "photographic" horses. Type-led design and clearly marked placeholders until Tadgh supplies photos.
- Silks/colours: don't reproduce real owners' silks as artwork.
