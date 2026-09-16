# PLAN.md — Letting Muse Create Songs on suno.com

> Goal: go from a song idea to a finished Suno track (MP3 in hand) with Muse
> driving the browser end-to-end. This doc is the runbook any future Muse
> session can follow.

## Current state

- ✅ Prompt pipeline exists: `index.html` builds Suno-ready **style prompts**
  (SUNO-Bible formula) and **tagged lyrics** (`[Verse]`, `[Chorus]`, …).
- ✅ `artist-database.json` for style inspiration.
- ❌ No Suno auth wired up. No automation runbook — that's this file.

## How it will work (big picture)

```
idea → prompt builder app → style + lyrics + title
      → Muse browser task → suno.com/create (Custom mode)
      → fill form → Create → wait for 2 variants
      → download MP3 → deliver to user
```

Suno has no public generation API, so **browser automation** is the route
(the same approach community Suno skills use).

## Phase 0 — Auth setup (one-time, needs the user)

1. User confirms their Suno login method (Suno offers Google / Discord /
   Microsoft sign-in).
2. Muse opens `https://suno.com/create` in the live browser and signs in
   using the saved login / Secure Vault flow. If a one-time code or 2FA
   step appears, pause and ask the user — never bypass it.
3. Verify: the create page loads, account is logged in, credits/plan are
   visible. Record the plan tier (free tiers have limited credits and may
   restrict downloads).

**Do not proceed past this phase without a confirmed logged-in session.**

## Phase 1 — Prompt pipeline (no browser needed)

1. Build the **style prompt** with the app (or hand-write per SUNO-Bible):
   - Formula: `decade, genre, subgenre, country, vocalist info, style + mood + instruments`
   - Keep it **≤ 1000 chars**, most important tags first.
   - Anti-pop armor when the target isn't pop (`no pop, no polished hooks…`).
2. Build **lyrics** with proper tags (`[Intro]`, `[Verse]`, `[Pre-Chorus]`,
   `[Chorus]`, `[Bridge]`, `[Outro]` …). Keep **≤ 5000 chars**.
   For instrumentals, leave lyrics empty and put `instrumental` in the style.
3. Pick a **title** (≤ 80 chars), **exclude styles** (comma-separated), and
   **vocal gender** if the song has vocals.

## Phase 2 — Browser automation runbook (per song)

Follow exactly, in order. Re-find page elements after any scroll/click —
Suno's element refs go stale.

| # | Step | Detail |
|---|------|--------|
| 1 | Open `https://suno.com/create` | Confirm logged in (avatar/menu visible). If not, stop and ask user. |
| 2 | Select **Custom** mode | Not Simple — Custom exposes lyrics/style/title fields. |
| 3 | Model selector (top of create area) | Default is v5; change only if the user asked for another (v4.5, v4…). |
| 4 | Fill **Lyrics** textarea | Full tagged lyrics from Phase 1. |
| 5 | Fill **Style of Music** | Style prompt from Phase 1. |
| 6 | Fill **Title** (optional field) | From Phase 1. |
| 7 | Expand **Advanced Options** | Click to reveal. |
| 8 | Fill **Exclude Styles** | Comma-separated exclusions. |
| 9 | Set **Vocal Gender** | Click Male/Female per Phase 1. **Don't skip this.** |
| 10 | Click **Create** | Song costs credits — see guardrails below. |
| 11 | Wait for **both variants** to finish | Poll the queue; don't navigate away. |
| 12 | Open preferred variant → **Download** | Save the MP3. Verify the download completed. |

## Phase 3 — Delivery

1. Save MP3 to `~/workspace/your_files/` as `suno-<slug-title>-<yyyymmdd>.mp3`.
2. Present it to the user as an attachment with the title, style prompt,
   and which variant was picked (1 or 2).
3. Log what was made (date, title, model, prompt hash) in memory so
   follow-ups ("make it faster", "extend it") have context.

## Guardrails

- **Credits cost money.** Never click Create without the user's explicit
  go-ahead for that song (a "yes, generate this" counts; a vague "make
  something" does not — confirm the prompt first).
- **One retry max** on generation failure: capture the visible error, retry
  once with the same prompt, then report instead of looping.
- **Queue/credits exhausted** → stop and report. Don't hammer the site.
- **Rate limits / blocks** (429/403): hard stop for the session, report it.
- **Login expired mid-run** → pause and ask the user to re-auth via
  browser takeover.
- Keep request volume human-like; this is the user's own account.

## Milestones

- [x] **M1 — Auth:** logged-in session on suno.com verified (Google: Xerohour@gmail.com / @xerohour; Pro Plan monthly, 2450 credits + 27 downloads as of 2026-09-16; Advanced/Custom mode accessible).
- [ ] **M2 — Dry run:** form fills correctly on the live create page
  (fill everything, screenshot, confirm with user *before* Create).
- [ ] **M3 — First song:** full run → MP3 delivered to the user.
- [ ] **M4 — Iteration:** follow-up ops work (remix/extend a delivered track).

## Open questions for the user

1. Which sign-in method does your Suno account use (Google/Discord/Microsoft)?
2. Free or paid Suno plan? (affects credits + download rights)
3. Default model — v5, or do you prefer v4.5?
4. Where should finished MP3s live — just chat attachments, or also a
   `songs/` folder in the repo?
