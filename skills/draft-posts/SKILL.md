---
name: draft-posts
description: Draft posts from interview answers (preferred), or from mined call ideas, or from transcripts directly. Applies the chosen format plus the user's calibrated voice, scores every draft against four lenses and self-revises before the user sees it, then reviews one at a time and logs every edit the user makes as a reusable correction. Use when the user says /draft-posts, "draft my posts", "write posts from my calls", "turn these ideas into posts", or references a specific idea to draft.
---

# Draft Posts

Turn raw material into posts, score them before the user spends attention on them, and capture every
edit so the same mistake is not made next week.

**Read first, in this order:**

1. `config.md` : paths, who the user sells to, calibration status
2. The corrections log at the configured path
3. `calibration/pov.md`, `calibration/voice.md`, `calibration/patterns.md`, `calibration/terms.md`
4. `reference/writing-mechanics.md`
5. `templates/voice-lint.md` (or the user's own copy of it, if they moved it)

Look for the pack in `call-mining/` at the project root, or beside this skill file. If you cannot find it, ask the user for the pack path once, then continue.

**If `config.md` says calibration has not run,** say so once, offer `/calibrate-voice`, and proceed
using the universal defaults in `writing-mechanics.md`. Do not silently invent rhythm targets.

---

## Step 1: Get the raw material

Work down this list. Stop at the first one that exists.

**1. An answered interview** (best, and the default path)

Load the most recent file in the interviews folder with status `answered` or `partially answered`.

**The user's answers are the primary source. The transcript quote is now supporting evidence, not the
spine.** Where an answer and the transcript cover the same ground, the answer wins: it is more recent,
more considered, and in their current phrasing.

Mine the spoken answers for lines to use nearly verbatim. Dictated speech is the closest thing to
their real register that exists in writing. Adapt for the page (drop the "um," fix run-ons, cut
restarts) but **do not upgrade their word choices into better-sounding ones.** That is the exact
moment a post stops being theirs.

Note which questions they skipped. Those are gaps to work around, never to fill.

**2. Ideas with no interview**

Load the most recent file from the ideas folder. Ask which to draft, or draft all.

**Say once that no interview was run**, and offer `/interview` first. If they decline, proceed, and
note that the ghostwriter test is carrying the realness load alone. It fails more often that way,
because the material to pass it was never collected.

**3. Nothing yet**

Run `/mine-calls` first. Do not draft from a blank page.

## Step 2: Set format and classification

For each post:

- **Format** : story | list | sarcastic | rant | conversation | observation | ask | carousel.
  Use the format from the idea. If none was chosen, ask.
- **Delivery** : text-only | text+image | carousel
- **Classification** :
  - **Problem** : a perspective shift, surfaces a problem or a misconception
  - **Process** : step by step, how it works, a framework
  - **Proof** : a result, a milestone, a specific number, a before and after
  - **Personal** : a surprise, a frustration, behind the scenes, humanizes the writer
- **Audience** : the primary buyer from `config.md`, the secondary audience, or both

Check the format mix against `calibration/patterns.md` for the week. If calibration has not run, do
not enforce a mix.

## Step 3: Draft

**Before drafting anything, read the corrections log.** Start with the standing corrections table,
then scan the log for anything not yet promoted. These are edits the user already made to earlier
drafts. **Making the same mistake twice is the one avoidable failure in this workflow.**

**Then write the target comment.** The exact comment you want, from the exact person you want it
from. A buyer's comment, not a peer's. Then write the post that earns it. Carry this line into the
scoring gate in Step 4 and the review in Step 5.

Then, per post:

1. **Build from the interview answers first**, transcript wording second. Lift actual sentences where
   they work. Adapt only for written form.
2. **Use the idea's hook as the opening line.** Do not replace it with a soft opener.
3. **Apply the format:**
   - **story** : narrative arc, scene first, payoff at the end
   - **list** : scannable, one point per line, arrow bullets
   - **sarcastic** : dry, irony in service of a point, never mean
   - **rant** : direct, opinionated, short sentences, builds
   - **conversation** : dialogue or question-and-answer framing, feels like a real exchange
   - **observation** : calm and specific, "here is what I keep seeing"
   - **ask** : a real open question the user will act on. Name the decision, say what they have been
     calling it and why it does not sit right, put the actual fork up, ask which one matches what the
     reader is living. **The ask replaces the CTA.** Two things to confirm before saving: they can be
     in the comments that day, and they are fine deciding this in public. Plan the follow-up post that
     closes the loop and credits whoever moved it.
   - **carousel** : slide-by-slide text, 8-10 slides, slide 1 is the hook, each slide one idea
4. **Apply the calibrated targets** from `calibration/patterns.md`: rhythm, length, opener type,
   closer type. If calibration has not run, use `writing-mechanics.md` and say which targets are
   defaults rather than measured.
5. **Apply the universal mechanics** from `reference/writing-mechanics.md`: one idea per post, hook
   earns the click, nothing invented, diagnose precisely and prescribe loosely, qualified CTA or
   none, closer is a line and not a question.
6. **Use the user's own terms** from `calibration/terms.md`, every time. Repetition across posts is
   what makes a body of work rather than a pile of posts.
7. **Check the idea's POV tag** when `calibration/pov.md` exists. An `on` post should state the
   position plainly rather than dancing around it: this is the body of work being built, so say the
   thing. A `contradicts` post is the more valuable one and needs handling. Name the position they
   held, say what changed it, and put the admission in the hook rather than the middle. Do not soften
   it into "my thinking has evolved." Say what they got wrong. Flag in the review that this one cuts
   against a published position, so they can decide before it goes out.
8. **Show proof as proof.** Specific numbers, verbatim quotes, real timelines. Named people need
   their permission first: flag it in the review rather than deciding for the user.
9. **Realness quotas.** One parenthetical aside that costs something to say. One or two single words
   in caps, never a capped phrase. One analogy from outside business if the post teaches a mechanism.
   A self-implicating admission belongs in the hook, not the middle.
10. **Run the AI scrub** from `writing-mechanics.md` §7. When a pattern appears, rewrite the sentence.
   Do not just delete it, or the rhythm collapses.
11. **Run the ghostwriter test.** Find the one sentence a competent ghostwriter could not have
    written. **If none qualifies, add one or cut the post.**
12. **Run voice-lint.** Fix every violation before the user sees the draft.

## Step 4: Score before the user sees it

The checks in Step 3 are binary, and they get run by the same pass that wrote the draft, which grades
generously. This is a separate scoring read with a threshold and a revision loop, so weak drafts get
fixed here instead of in the user's review time.

**Re-read the draft cold before scoring.** Do not score from memory of writing it.

Score four lenses, 1 to 10. **Every score under 8 must quote the specific line that lost the points.
A score without a quoted line is not a score.**

| Lens | The question | What a 10 looks like |
|---|---|---|
| **The Buyer** | Would the target comment actually get left, by a real person? | Name a specific real reader from the list in `config.md` who would leave it. **If nobody real comes to mind, cap the score at 6.** The post makes someone at the qualifying threshold feel watched. |
| **The Skeptic** | What is the strongest objection, and does the post survive it? | State the sharpest counter a smart peer would raise. A 10 means the post already answers it or is honest about the limit. **A post that survives only because nobody thought hard scores a 5.** |
| **The Editor** | Hook, rhythm, closer | Hook earns the click with no soft opener. Rhythm matches `calibration/patterns.md`, or the universal defaults if calibration has not run. Closer is the sharpest true line in the draft, not a question. |
| **The Voice** | Could a competent ghostwriter have written this? | At least one sentence only this user could write, and it costs them something. Zero AI structure patterns. Passes voice-lint clean. |

**The gate is the lowest score, not the average.** A 10/10/10/5 does not ship. The 5 is the line a
reader will actually hit.

**Threshold is 8 on every lens.**

If any lens is under 8:

1. Fix the specific quoted line, not the whole post
2. Re-score all four. A fix in one lens often costs another.
3. Repeat **at most twice**

If it still fails after two rounds, **present it anyway with the failing lens named and the line
flagged.** Say it plainly: "This one is stuck at 6 on the Skeptic lens, here is the line." The user
decides whether to fix it, spike it, or ship it.

Do not silently ship a failing draft. Do not spin on it either.

## Step 5: Review one at a time

Present **one post at a time**:

- Source (call and date, or interview file)
- **Target comment**
- **Scores** (Buyer / Skeptic / Editor / Voice, plus any lens under 8 and the line responsible)
- Audience, Classification, Format, Delivery
- Draft
- Visual brief, when delivery is carousel or text+image
- Anything needing someone's permission before it can post

Ask: "Approve, or tell me what to change."

### When they edit, log the delta

**Before applying the feedback**, append to the corrections log:

```
### YYYY-MM-DD : [post slug]
**I wrote:** "[verbatim line from the draft presented]"
**They changed it to:** "[verbatim final]"
**Rule:** [one sentence, written to apply to the NEXT post, not this one]
**Category:** hook | rhythm | term | claim | CTA | register | structure | fact
```

The rule is the part that matters, and it is the part that is easy to get wrong. Write it so it
applies next week to a different post. "Cut the second example" is not a rule. "One post, one idea: a
second example is a second idea, not a free addition" is.

Then apply the feedback and re-present.

**If they approve clean with no edits, log nothing.** Clean approvals are not training data.

### Reversals

If the user rolls back an earlier correction, record that too, under the original entry:

```
**Reversed [date]:** [what got rolled back, and what the durable takeaway actually is]
```

A rule that got reversed is not a rule. Recording the reversal stops it from being re-applied next
week on the strength of a stale log entry.

## Step 6: Save and promote

**On approval**, save to the configured published folder as `YYYY-MM-DD_slug.md`:

```markdown
# [Slug] : [Date]

**Source:** [call and date] | [interview file, if used]
**Audience:** [primary | secondary | both]
**Classification:** Problem | Process | Proof | Personal
**Format:** [format]
**Delivery:** text-only | text+image | carousel
**Scores:** Buyer [n] | Skeptic [n] | Editor [n] | Voice [n]

---

[Final post text]

---

**Approved:** [date]
```

**At the end of the session**, check the corrections log. **Any rule now at three strikes gets
promoted out of the log** into the file that owns it. The routing table is at the top of the
corrections log. Tell the user what got promoted and where.

The log stays short on purpose. A log nobody reads is worse than no log.

---

## Edge cases

- **Calibration has not run:** say so once, offer it, proceed on universal defaults. Mark which
  Editor-lens targets are defaults rather than measured.
- **No interview was run:** say so once. Note that the ghostwriter test is unsupported and will fail
  more often.
- **The interview answers are thin:** draft only what they support. A two-line answer makes a short
  post, not a padded one. Say which ideas did not get enough.
- **A post needs someone's permission:** flag it in the review with exactly what needs approving.
  Never decide this for the user, and never quietly anonymize a quote to dodge the question.
- **The user wants a post the scoring gate keeps failing:** present it with the failure named and let
  them ship it. The gate exists to save their attention, not to overrule them.

## What not to do

- Do not draft from a blank page. If there is no raw material, run `/mine-calls`.
- Do not upgrade the user's word choices into better-sounding ones.
- Do not fill a gap the interview left open. Work around it or flag it.
- Do not invent a number, a quote, a name, or a client detail. Ever.
- Do not score from memory of writing the draft. Re-read cold.
- Do not report a score under 8 without quoting the line responsible.
- Do not ship a failing draft silently, and do not spin past two revision rounds.
- Do not log a correction the user did not actually make.
