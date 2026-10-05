# Learning record / 學習紀錄

Tool: Claude Code (CLI agent), acting directly on this git repository — not a GUI chat tool, so no browser/app screenshots were captured. Evidence here is the agent's real terminal output, git history, and a small Node.js harness used to execute `output/index.html`'s own script and check its behavior against the spec's test table (no dev server needed for a static offline file). Every result below is from an actual run in this repo, not a prepared simulation.

## Task A — organize `practice/01-club-files`

**What I asked for:** follow the lab's A card — read the 12 input files, propose categories, then (after confirming) copy each file exactly once into a categorized `output/`, keep every original and every differing version, and write `report.md` + `manifest.json`.

**What I checked before execution:** read all 12 files in `input/` directly, noting two byte-identical pairs (`announcement.txt`/`announcement_copy.txt`, `equipment_list.txt`/`equipment_backup.txt`) and one similarly-named-but-different pair (`proposal_final.txt` = outdoor/30min, `proposal_final2.txt` = indoor/20min).

### Tests actually performed

| Test | Expected | Observed | Evidence |
|---|---|---|---|
| 1. Compare input/output file counts and checksums | 12 input files → 12 copies in `output/`, each copy's content identical (md5) to its original; no file deleted or overwritten | `manifest.json` has exactly 12 entries; `diff` of sorted md5 sets for `input/*.txt` vs `output/**/*.txt` was empty (set match) | Terminal: `python3 -c "...assert len(d)==12"` passed; `diff <(md5 input) <(md5 output)` produced no diff |
| 2. Open two original/copy pairs and compare content | Similarly-named files that differ (proposal_final vs final2) must both survive, not be merged/deleted; byte-identical pairs must both survive as separate files | `output/proposals/proposal_final.txt` and `proposal_final2.txt` both present with their original differing text; `output/announcements/announcement.txt` and `announcement_copy.txt` both present and identical | Read both pairs directly in `output/`; documented in `output/report.md` under "Suspected duplicates" and "Similarly named but NOT duplicates" |

No revision was needed for A; the required "one revision" was done on B instead (see below), as the lab's instructions allow.

## Task B — `practice/02-campus-picker/output/index.html`

**What I asked for:** a single offline `index.html` implementing the location/time/energy filters, random pick from matches only, "no match" message, a 5-item newest-first history of successful picks, a filter reset that doesn't touch history, and a zh/en language switch — per the B card's 9 numbered requirements.

**What I checked before execution:** read `activities.json` (12 fictional activities) and confirmed the embedded copy in `index.html` is byte-for-byte identical to it (`JSON.stringify(embedded) === JSON.stringify(original)` → `true`), and that the file has no `<script src>`, `<link>`, or `fetch`/network calls.

### Tests actually performed (against the spec's test table)

| Test | Expected | Observed | Evidence |
|---|---|---|---|
| Indoor / 15 min / low, 10 draws | Only A01/A02/A03/A04 may appear | Every draw returned one of A01–A04 | Node harness output: 10/10 `OK` |
| Outdoor / 15 min / medium | No matches; filters stay unchanged | `matched: false` | Node harness output: `OK (no match as expected)` |
| Outdoor / 30 min / medium, 10 draws | A09 every time | Every draw returned A09 | Node harness output: 10/10 `OK` |
| All / 60 min / all, 6 successful picks | Only latest 5 remain, newest first | History held exactly the last 5 picks, newest first | Node harness output: `OK` |
| Reset filters | Back to all/30/all; history untouched | Filters reset; history length unchanged | Node harness output: `OK` |
| **Clear history, then switch language** | Empty history; controls and names switch language | **v1: no clear-history control existed at all — this test could not be performed.** v2: history emptied on click; title text changed between `下課可以做什麼？` and `What can I do between classes?` | Node harness: v1 run logged "NO clearHistory function exposed"; v2 run logged `history after clear: 0 OK` and the title strings differing `OK` |

### One revision

**Before:** v1 (`B v1` commit) implemented all filtering, picking, history, reset, and language-switch logic correctly, but had no button to clear history — the spec's item 7 ("Add a clear-history button") was not met. This was found while running the "clear history, then switch language" test from the spec's own table, not invented afterward.

**Request:** add a "清除紀錄" / "Clear history" button next to the history list that empties `state.history` immediately, without touching the current filters, and re-labels correctly after a language switch.

**After and retest:** added the button and a `clearHistory()` handler (`B v2` commit). Re-ran the full test table; the previously-blocked test now passes (history goes from 5 entries to 0 on click; title/labels still switch correctly).

**New requirement or defect?** Defect — the clear-history button was already required by the original B card (requirement 7), not a new ask. v1 simply did not implement it.

## Task D — `practice/04-review/bad-plan.txt`

Read the deliberately flawed plan (not executed). Identified five problems (scope creep onto all of Downloads, destructive delete with no confirmation, unfounded "final2 = latest" inference, fabricating guessed values instead of flagging them, and auto-publishing without review) and wrote an alternative plan in `practice/04-review/my-rejection.md` that scopes work to one folder, requires a plan+confirm step, never deletes originals, never infers approval from filenames, flags rather than guesses missing values, and never auto-publishes.

## Still unverified

- B was tested with a scripted Node.js harness that runs the page's own inline script against stubbed DOM elements (no real browser was available in this environment), not a live browser/phone. Visual layout, touch usability on an actual phone screen, and the random-pick animation (none was built, per the lab's note that a spinning wheel is optional) have not been eyeballed in a real browser.
- A's categorization is a judgment call (e.g., grouping `next_steps.txt` and `rain_plan.txt` under "meeting"); `report.md` flags the genuinely unresolved questions (which duplicate file to keep, which proposal is approved) rather than deciding them.
- No GUI screenshots exist for this submission because the agent used was the Claude Code CLI operating directly on the repository, not a chat UI with a browsable/screenshot-able session. The Node.js test output above is the closest equivalent — a verifiable, actually-executed record of the checks performed.
