# My lab evidence / 我的實作紀錄

Use a group code, not real names or student IDs in shared files. / 共用檔只寫組別代碼，不寫姓名或學號。

- Group code / 組別：HSley13
- Tool / 工具：Claude Code (CLI agent)
- Route / 路線：individual 個人
- Tasks completed / 完成題目：A, B (v1 + v2 revision), D, record
- Material / 素材：NDHU classroom tasks 東華課堂版
- For original-pack work: task number, author/source link and version / 原版實作：題號、作者來源連結與版本：not applicable — NDHU classroom material only, original pack not used
- My role and what I checked / 我的角色與實際檢查：I ran the agent directly in this repository (not a GUI chat tool) and personally verified every output: read all 12 Task A input files before and after sorting, diffed checksums between `input/` and `output/`, and ran a Node.js harness that executes `index.html`'s own script to check it against the B card's full test table before and after the revision.

## Scope and plan / 範圍與計畫

Allowed input and output folders / 可讀取與輸出的資料夾：`practice/01-club-files/` (input → output only), `practice/02-campus-picker/` (output only, `activities.json` read-only), `practice/04-review/` (read `bad-plan.txt`, write `my-rejection.md`), `evidence/`.

What I asked for / 原始需求：Complete the NDHU lab's task cards A, B and D exactly as written in the handout (https://ndhu-campus-agent-lab.tedc.chatgpt.site, EN version), then record the evidence.

What I checked before execution / 動手前我檢查了什麼：Read the handout's A/B/D task cards in full, read all 12 Task A input files myself, read `activities.json` and `bad-plan.txt` myself, and confirmed each task folder before writing anything into it.

## Tests actually performed / 我真的做過的測試

| Test / 測試 | Expected / 預期 | Observed / 實際 | Evidence / 證據 |
|---|---|---|---|
| 1. Task A: diff md5 checksums of `input/*.txt` vs their copies in `output/**/*.txt` | All 12 originals preserved, all 12 copies byte-identical to their source | Checksum sets matched exactly; `manifest.json` has 12 entries | Terminal `diff`/`md5` run, see `evidence/learning-record.md` |
| 2. Task B: run full spec test table (filters, no-match case, history cap, reset, clear+language) via Node harness on `index.html`'s own script | Each row of the B card's test table passes | 5/6 rows passed on v1; the "clear history" row failed (no button existed) until the v2 revision, then all 6 passed | Node.js harness transcript, see `evidence/learning-record.md` |

## One revision / 一次修改

Before / 原來的情況：B v1 had correct filtering, random pick, 5-item history, and language switching, but no button to clear the history (spec item 7 not implemented).

Request / 我提出的修改：Add a "清除紀錄 / Clear history" button next to the history list that empties the history immediately without changing the current filters.

After and retest / 修改後與重測結果：Added the button and `clearHistory()` handler (commit "B v2: add manual clear history button"). Re-ran the full test table — the previously-unpassable "clear history, then switch language" test now passes: history goes from 5 entries to 0, and labels still switch correctly between zh/en.

New requirement or defect? / 新需求還是原規格未做到？Defect — the clear-history button was already required by the original B card; v1 simply omitted it.

## One rejection / 一次退回

Which action I reject and why / 退回哪個動作、為什麼：Rejected the `bad-plan.txt` discussion plan ("organize everything in Downloads, delete duplicates, treat final2 as the latest version, fill missing values with reasonable guesses, and publish the result automatically") for five reasons: it operates outside the assigned task folder, deletes files with no confirmation step, infers an "approved" version from a filename alone, fabricates values for missing data instead of flagging them, and publishes automatically with no human review. Full writeup in `practice/04-review/my-rejection.md`.

An acceptable alternative / 可以怎麼改：Scope work to the one named folder; propose a plan and wait for "Run" before changing anything; never delete or overwrite originals, only copy; never infer approval from filenames/dates — flag ambiguous versions for a human decision; report missing/uncertain values instead of guessing; never auto-publish — stop after producing output and report for human review.

## Still unverified / 還沒驗證

What I cannot claim is complete / 哪些事不能說已完成：B's `index.html` was verified with a scripted Node.js harness driving its own inline script against stubbed DOM elements, not a real browser or phone — actual mobile layout, touch usability, and visual appearance have not been eyeballed. Task A's category choices (e.g., grouping `next_steps.txt`/`rain_plan.txt` under "meeting") are a judgment call, not a verified fact; the genuinely unresolved questions (which duplicate to keep, which proposal is approved) are left open in `output/report.md` rather than decided. No GUI screenshots are included because the agent used (Claude Code CLI) has no chat-UI session to screenshot; the Node.js test transcripts in `evidence/learning-record.md` serve as the actually-executed equivalent.

For the fallback route, mark all prepared evidence as supplied simulation. / 備援路線請標明所有預生成證據來源，不能填成自己的Agent實跑。 — Not applicable; this submission used the live git route, not the fallback route.
