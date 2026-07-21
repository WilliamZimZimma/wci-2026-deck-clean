# WCI-2026-Deck-Clean — Intelligence File

> Created 2026-07-15. The CLEAN presentation version (v3) of the WCI 2026 deck — speaker notes stripped.

Last Updated: 2026-07-21
Sessions Tracked: 3

## What This Is
Presentation-ready copy of `../WCI-2026-Deck-Site/` with all 8 `.notes` divs, the prep-only banner, and the unused notes CSS removed — AND (since later on 7/15) all eyebrow labels removed: the "DEVEREUX PA · COST CONTAINMENT INNOVATION SERIES" title-slide eyebrow, every "SECTION N · timing" badge, the MODERATOR meta row, and the "Moderator introduces the panelists…" line. Same 8 slides, same animations/backgrounds. **This is the version to put on screen at WCI and the DEFAULT target for any slide-content edit request.**

- Live: https://wci-3d-printing-panel.vercel.app (primary; old wci-2026-deck-clean.vercel.app still resolves)
- Repo: github.com/WilliamZimZimma/wci-2026-deck-clean (private, push → auto-deploy; Vercel project `wci-2026-deck-clean`)
- Verified 2026-07-21: HTTP 200, 8 slides, div balance clean, all anchors resolve, no duplicate ids (Codex-reviewed 6/6 PASS)

## File Map
| File | Purpose |
|------|---------|
| `index.html` | The whole clean deck — 8 slides + canvas animation JS, one file (~24.5 KB) |
| `soft-*.png` (4) | Slide background images (same assets as the notes version) |
| `.gitignore` | Ignores `.vercel` |
| `.vercel/` | Linked to Vercel project `wci-2026-deck-clean` |
| `index.html.stale-backup-20260721` | Pre-sync snapshot of the stale local copy (7/21). Safe to delete once the deck is final. |

## Rules
- **William's slide edits land HERE by default.** When he says "the deck" / "the new site" / "the slide," he means this clean site unless he explicitly says the notes version. (Learned the hard way 7/15 — an edit went to the notes site and had to be reverted.) **This supersedes the original "never edit here first, re-derive from notes" rule.**
- The notes version (`../WCI-2026-Deck-Site/`, Vercel project `deck-live-deploy`) is the INTERNAL prep/notes site. After a content change lands here, port it there so the two stay in sync — the sync direction is clean → notes, not the reverse.
- This deck has INTENTIONALLY diverged from the notes version: no notes, no eyebrows, no Devereux branding, no moderator lines (removal commits: `4741a76`, `8240cee`, `e6a5eee`), plus Mary Anne's 7/21 removals (per-segment minutes + panelist names, role labels kept — `6657f2e`).
- **ALWAYS `git fetch` and diff live vs local vs `origin/main` before editing.** All three can disagree independently. See the 7/21 session log.
- Deploy: commit + push (auto-deploys), or `vercel --prod --yes` from this folder. Never `vercel --prod` from an uncommitted state — it strands work on the deployment where git can't see it.
- Over the SSH side-door, `vercel` is not on PATH — export `~/.nvm/versions/node/v22.18.0/bin` first.
- Both video links are placeholders pending real URLs from William: slide 1 `▶ OPENING VIDEO` (`#video`), slide 4 `▶ HOW 3D PRINTING WORKS` (`#video2`).

## Suggested Improvements
- Slide 6 subtitle under "Quality & Jurisdictional Compliance" still reads "Standards, liability exposure & chain of custody" — heading and subtitle now disagree. Awaiting William's replacement wording.
- `CLAUDE.md` is not tracked in a committed state matching reality — commit it so a `git reset --hard` can't wipe it again (this happened 7/21).

## Session Log

### 2026-07-21 - Slide 6 labels + second video link (Grade: B-)
- **Built:** Slide 6 label tweaks ("Quality & Liability" → "Quality & Jurisdictional Compliance"; "Reimbursement & Coding" → "Reimbursement"); second video link on slide 4 ("▶ HOW 3D PRINTING WORKS") with matching `id='video2'` anchor. Commits `7d0c06e`, `e4840c2`, + anchor fix — all pushed, deployed, codex-verified (6/6 PASS).
- **Learned:** A live Vercel deploy can be AHEAD of BOTH the local folder and git. `vercel --prod` from an uncommitted state strands work on the deployment where `git status` shows nothing.
- **Learned:** Mary Anne's edits ("remove per-segment minutes + panelist names, keep role labels", `6657f2e`) were committed from ANOTHER machine. Local was one commit behind; the `git push` rejection was the first signal.
- **Learned:** Slide 1's `href='#video'` resolves only because the slide-1 `.wrap` carries `id='video'`. A new video link needs its own matching id or it's a dead anchor — codex caught this, manual review did not.
- **Learned:** `vercel` is not on PATH over the SSH side-door; needs the explicit nvm path.
- **Broke:** `git reset --hard origin/main` silently discarded the slide-4 video-link position, which lived ONLY on the live deploy and was NOT in Mary Anne's commit. I conflated the two and assumed her commit covered all the drift. William caught the regression, I did not.
- **Broke:** The same `reset --hard` also wiped the uncommitted, much richer `CLAUDE.md` (~4.4 KB → 982 B), restoring an OLD version whose "never edit here first" rule directly contradicts the corrected default-target rule. Rebuilt from session context.
- **Broke:** First drift diagnosis ("deployed but never committed") was wrong — the names/minutes WERE committed, just remotely. Should have run `git fetch` before concluding anything.
- **Pattern:** Before editing a deployed single-file site, do a THREE-way diff: live vs local vs `origin/main`. `git fetch` FIRST — `git status` says nothing about the remote. And never `reset --hard` over uncommitted work without checking what else is dirty.

### 2026-07-15 - Created (v3 derivation) + label removals
- Derived from the notes deck (stripped `.notes`, prep banner, notes CSS), then in follow-up commits removed the per-slide "WCI Deck · Slide N" labels, page header, Devereux eyebrow, section/timing badges, and moderator lines. Deployed + Codex-verified.

### 2026-07-15 (later) - Confirmed already-clean during the wrong-site incident
- William asked for the Devereux/MODERATOR/section-label removals; they were applied to the notes site by mistake (and reverted there). Verified live + local that THIS deck already had all of them removed — zero changes needed here. Both CLAUDE.md files updated with the two-sites rule so the default target is unambiguous.

### 2026-07-15 (wrap-up) - New primary URL + Mary Anne email (Grade: C+)
- **Built:** New primary URL https://wci-3d-printing-panel.vercel.app (William picked from 3 options); Mary Anne "deck ready, just slides" email → `~/Desktop/email-mary-anne-wci-clean-deck.txt` + Google Doc `1qf0DRyEPU2oiXb1ajadj5-akD_l79Mq6gAZfP8rC4eo`; memory file `project_wci_deck_two_sites.md`.
- **Learned:** `vercel alias set` on this team hits SSO deployment protection (302 to vercel.com/sso-api) — a manually-set alias does NOT bypass it; `vercel domains add <name>.vercel.app` (project domain) does. Old URL keeps resolving after the new domain is added.
- **Learned:** Duplicate-doc gotcha — running upload-as-google-doc.js twice creates two docs; capture the URL on the first run or trash the dupe via Drive API.
- **Broke:** First alias attempt served a Vercel SSO redirect instead of the deck — removed the alias, added as project domain instead.
- **Pattern:** For a client-friendly .vercel.app URL on a protected team: `vercel domains add`, never `vercel alias set`.
- **Grade reasoning:** C+ — everything shipped and is verified live, but the session started with a wrong-site edit that cost ~35 min and a manual revert.
