---
name: poll-follow-up
description: Follow up on a WhenNOT poll - see who has answered and the best dates, remind the people who have not answered, and pick the final dates. Use when the user asks how a poll is going, who still has not answered, which dates work best, to chase or nudge people, or to close a poll and set the date.
---

# Poll follow-up

Report where a poll stands, chase the missing answers and close it on the dates the user picks.

## Rules for every step

- `get_poll_results` and `list_my_polls` only read.
- `remind_poll_participants` sends email, and `finalize_poll` closes the poll. Say what will happen
  and wait for a yes before you call either of them.
- Only the organiser can remind people or pick the final dates. If the tool refuses, say so and do
  not try again.
- When the poll hides responder details and the user is not the organiser, the answer has counts
  (`cannotCount`, `maybeCount`) and no names. Report the counts. Do not guess who is out.
- Do not invent dates. Suggest only dates from the `best` list of the tool answer.

## Workflow

1. **Find the poll.** If the user gave a link (`https://whennot.com/poll/…`), use it. Otherwise
   call `list_my_polls` and match the name. Ask when two polls fit.
2. **Read the results.** Call `get_poll_results`. Say how many people answered, how many
   invitations are still open, and the best dates: the ones with the fewest people who cannot
   make it. A "maybe" is weaker than a "cannot", so name both numbers.
3. **Chase.** When people have not answered and the user wants a nudge, call
   `remind_poll_participants`. WhenNOT reminds each person at most once a day, so the answer can be
   "nobody to remind right now". Say how many were reminded.
4. **Pick the final dates.** When the user chooses, call `finalize_poll` with `start` and `end`:
   - a DAYS poll takes days (YYYY-MM-DD, the last day is included);
   - a SLOTS poll takes instants (ISO 8601) from the results.
   Add `title` and `location` when the user gives them. `notify` is false by default: ask if
   WhenNOT should email the final dates to everyone who answered, and send `notify: true` only
   after a yes.
5. **Confirm.** Say the final dates in plain words and whether people were told.
