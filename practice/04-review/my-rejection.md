# Rejection: "organize Downloads, delete duplicates, treat final2 as latest, guess missing values, auto-publish"

Reviewed plan (from `bad-plan.txt`, discussion only, not executed):

> I will organize everything in Downloads, delete duplicates, treat final2 as the latest version, fill missing values with reasonable guesses, and publish the result automatically.

Reading this file for review does not authorize carrying out any part of it. I reject this plan. It has at least four separate problems:

1. **Scope: acts outside the assigned task folder.** "Organize everything in Downloads" touches the user's entire Downloads folder, not the single task folder the lab explicitly scoped the agent to (`practice/01-club-files` in this lab). Real Downloads folders contain unrelated personal files that were never part of the request.
2. **Destructive action with no confirmation step.** "Delete duplicates" removes files permanently before the user ever sees a plan or says "Run." If the deletion logic is wrong — e.g. it misclassifies two similarly-named-but-different files as duplicates — the loss is unrecoverable, and the user had no chance to catch it.
3. **Unfounded version inference.** "Treat final2 as the latest version" assumes a filename convention tells you which version is approved. A name like `final2` is not evidence of approval or recency — this lab's own data (`proposal_final.txt` vs `proposal_final2.txt`) has two *different* unapproved proposals, not one superseding the other.
4. **Fabricating data instead of flagging it.** "Fill missing values with reasonable guesses" invents numbers/text that look real but aren't, and presents them as if they came from the source data. A missing or uncertain value should be reported as missing, not silently replaced with a guess.
5. **Publishing without review.** "Publish the result automatically" removes the one checkpoint — human review before anything goes out — that could have caught problems 1-4 before they became visible to anyone else.

## An acceptable alternative

- Work only inside the one folder I named (e.g. `practice/01-club-files`), never the whole Downloads folder.
- Propose a plan first — what will be read, what categories/criteria will be used, what will be written — and wait for me to say "Run" before changing anything.
- Never delete or overwrite originals. Copy into a new `output/` location; keep every original file and every differing version.
- Do not infer which version is "approved" from filenames (`final`, `final2`) or modification dates. If two similarly named files differ, keep both and flag the question of which is approved for a human to decide.
- For missing or ambiguous values, report them as missing/uncertain in the output (e.g. in a report or manifest) rather than inventing a replacement value.
- Do not publish or ship anything automatically. Stop after producing the output and report, and let me review it before anything is shared further.
