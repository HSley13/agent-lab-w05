# Club files organization report

Input: 12 files in `input/`. Output: 12 copies in `output/`, sorted into 7 category folders. No originals were deleted, moved, or overwritten; every file in `input/` is untouched and a copy of it exists under `output/`.

## Categories

| Folder | Files | Why grouped |
|---|---|---|
| `announcements/` | announcement.txt, announcement_copy.txt | Club announcement text |
| `budget/` | budget_draft.txt | Draft (unapproved) budget figure |
| `equipment/` | equipment_list.txt, equipment_backup.txt | Equipment counts |
| `feedback/` | feedback_questions.txt | Post-activity feedback questions |
| `meeting/` | meeting_notes.txt, next_steps.txt, rain_plan.txt | All concern the same open indoor/outdoor decision |
| `creative/` | poster_text.txt | Poster/creative copy |
| `proposals/` | proposal_final.txt, proposal_final2.txt | The two competing activity proposals |

## Suspected duplicates (identical content, kept separately)

- `announcement.txt` and `announcement_copy.txt` — byte-identical content. Likely the same announcement saved under two filenames. Not deleted; a human should confirm which filename to keep before removing either.
- `equipment_list.txt` and `equipment_backup.txt` — byte-identical content. Likely the same count saved as a backup copy. Not deleted; a human should confirm which filename to keep before removing either.

## Similarly named but NOT duplicates

- `proposal_final.txt` (v1: outdoor activity, 30 minutes) and `proposal_final2.txt` (v2: indoor activity, 20 minutes) have different content despite the "final"/"final2" names. Neither file's own text claims to be approved — v1 says "尚未定案" (not yet decided) and v2 says "仍待討論" (still under discussion). The filename alone does not indicate which is the final, approved version, so **both are kept** and no decision between them was made here.

## Unresolved questions (need a human decision)

1. Which of `announcement.txt` / `announcement_copy.txt` is the canonical file to keep, if only one should remain?
2. Same question for `equipment_list.txt` / `equipment_backup.txt`.
3. Which proposal (v1 outdoor/30min or v2 indoor/20min) is actually approved — this report does not decide that, since neither the "final" naming nor the modification dates are reliable evidence of approval.
4. `meeting_notes.txt`, `next_steps.txt` and `rain_plan.txt` all point at the same pending indoor/outdoor decision; nothing in the input data says which way it was decided.
