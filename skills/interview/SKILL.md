---
name: interview
description: Turn selected post ideas into a short interview doc the user answers out loud, then hand the answers to drafting. Generates 6-8 journalist-style questions TOTAL (not per idea), each one load-bearing: it either unlocks a draft that cannot be written without it, prevents a mistake, or marks what is off-limits. Hunts for what a recording structurally cannot hold. Use when the user says /interview, "interview me on these", "build the interview doc", "ask me questions about these ideas", or after /mine-calls once they have picked which ideas to develop. Run this before /draft-posts unless the user explicitly skips it.
---

# Interview

The step between ideas and drafting. Ideas are raw material from conversations the user already had.
This turns them into raw material from the conversation they have not had yet: the one with
themselves, about what they actually think.

## Why this exists

Every post drafted straight from a transcript quote is built from something the user said to somebody
else, weeks ago, filtered through a model. The specifics that make a post theirs never made it into
the recording: what they were actually thinking, the number they did not say out loud, the thing they
almost said instead.

Drafting skills try to catch this after the fact with a ghostwriter test: find the one sentence a
competent ghostwriter could not have written, and cut the post if none qualifies. That test fails a
lot, because **the raw material to pass it was never collected.** This step collects it.

It is also the step everybody skips, which is why so much AI-assisted content reads like AI-assisted
content. The model is not the problem. The input is.

**Read `config.md` first** for the ideas path, the interviews path, and the corrections log.
Look for the pack in `call-mining/` at the project root, or beside this skill file. If you cannot find it, ask the user for the pack path once, then continue.

---

## Step 1: Load the ideas

Read the most recent file in the configured ideas folder. If the user names an older file or a
specific idea, use that.

Ask which ideas to interview on, and offer the default: **the Top 3, plus any off-transcript
candidate.** Cap at 5 items.

More than five produces a doc too long to answer in one sitting, and the last answers get thin. A
half-answered doc is worse raw material than a short one answered fully.

If the user already named the ideas, skip the ask.

## Step 2: Read what already exists

Before writing a single question, for each selected idea:

- Re-read the source transcript section if the idea cites a call
- Check the published folder for anything covering the same ground
- Check the corrections log for standing corrections that change what to ask
- Check any voice or playbook files for an existing named concept covering this

**The point of this pass is to not ask what they already answered.** A question whose answer sits in
a file they wrote is a wasted question, and it makes the whole doc feel like busywork. Ask about the
gap, not the record.

## Step 3: Write the questions

**Hard cap: 6-8 questions total across the entire doc.** Not per idea. A doc with four ideas gets 6-8
questions, not 24. The user's time is the scarce resource here, not the model's.

### The load-bearing test

Every question has to survive this: **if they skip it, what breaks?**

If the answer is "nothing, the draft is just a bit richer," cut it. Only three kinds earn a slot:

- It **unlocks a draft** that cannot be written without it (a diagnostic post needs the mechanism, a
  scene-led post needs the scene)
- It **prevents a mistake** (a published position pointing the other way, a near-duplicate already
  drafted, a number that would be wrong)
- It **marks a line** (what is off-limits, who needs to approve)

Everything else is texture. Texture is what the drafting step invents around, and it is allowed to,
because the specifics that actually matter are the three above.

Rough allocation: one unlock question per idea being drafted, plus one or two mistake-preventers,
plus **a single combined off-limits question** covering every sensitive call in the batch. Do not
write a separate sensitivity question per idea.

**Put a one-line italic note under each question saying what it unlocks.** It proves the question
earned its slot, and it tells the user what they cost the draft by skipping it.

### The seven veins

Every question must hunt for something a transcript structurally cannot contain.

| Vein | What it gets | Example shape |
|---|---|---|
| **The unsaid** | What they were thinking while the other person talked, and chose not to say | "When she said that, what was the thing you decided not to say?" |
| **The scene** | Physical, specific, datable detail: where, when, what was on screen | "Where were you when this call happened, and what was in front of you?" |
| **The number** | The figure they know and did not cite on the call | "What was her actual revenue, and what did she think it was?" |
| **The cost** | What the mistake or pattern quietly cost, in money or months | "How long had she been doing this before it showed up in the numbers?" |
| **The reversal** | Where they changed their mind, lost the argument, or talked someone out of what they sell | "Did anything in that call move you off a position you walked in with?" |
| **The peer version** | What they would say about this to a peer, not to a client | "How would you describe this to another consultant over dinner?" |
| **The line** | What is off-limits publicly, so drafting does not walk into it | "Anything here you would not want traced back to her?" |

### Rules for the questions themselves

- **One idea per question.** No multi-part questions. If they are answering by voice, a two-part
  question gets one answer and the second half is lost.
- **Scene-seeking and concrete.** Never "tell me more about X" or "what are your thoughts on Y."
- **Answerable in 30-90 seconds out loud.** If it needs a whiteboard, it is the wrong question.
- **Lead with the highest-value question** for each idea, usually the scene or the reversal. If they
  run out of time halfway, the first answers still carry a draft.
- **No yes/no questions** unless the follow-up is built into them.

### Special cases

**A genuine ask candidate** runs the other direction from everything above. Ask what they actually do
not know, what they would do differently depending on the answer, and what deadline is forcing it.
**If the answers reveal they already decided, kill the ask.** It is bait now.

**A scene-led or newsletter candidate** weights toward the cold open. A scene needs a person, a
place, a moment, and something at stake. Ask for all four explicitly. Also ask for any exercise or
takeaway in their own words, because that is the part that most often reads generic when a model
writes it.

## Step 4: Write the doc

Save to the configured interviews folder as `YYYY-MM-DD_interview.md`.

Format it **to be answered out loud**:

- Questions numbered continuously, 1 through 6-8, in a single flat list
- **Do not group by idea.** Grouping invites a question quota per idea, which is exactly what
  produces a bloated doc. One flat list of the questions that earned their slot.
- Each question on its own line, with its italic unlock note under it, and blank space between
- Name the person in the question itself so no context header is needed
- No preamble to read past before question 1

Then give the user the file path, and **recommend they answer out loud.**

Say why, in a line: speaking gets three or four times more out of them than typing does, and it keeps
the phrasing that makes a post sound like them. When people type, they edit as they go. They compress,
they formalize, they drop the aside that was the most useful part of the answer.

Typing is a fine fallback and better than skipping the step. Just do not present the two as equal.

## Step 5: Take the answers back

Three ways answers arrive, in order of how much they give the draft.

- **A pasted block of transcribed voice (best).** Expect dictation artifacts: no punctuation,
  run-ons, "um," restarts, mangled proper nouns. **Do not clean it into corporate prose.** Map each
  chunk back to its question number and keep the exact phrasing. Their spoken wording is the asset.
  That is the entire point of the step.
- **An audio file or a recording of themselves.** Transcribe and handle the same way.
- **Typed answers, or answers in chat.** Workable, and much better than skipping. Ask **one question
  at a time**, highest-value first. Expect shorter and more formal answers than speech would produce,
  so follow up more often: when a typed answer is a single tidy sentence, ask the follow-up that gets
  the detail underneath it.

Write the mapped answers back into the same interview file under each question. Flag any skipped
question and ask once whether it matters. Skipped twice: drop it, and note in the file that the draft
has to work without it.

**Never fill a gap yourself.** An unanswered question becomes an open question in the handoff, not a
guess. A guess here contaminates everything downstream, and it is invisible by the time it reaches
the draft.

## Step 6: Hand off

Say what is ready to draft and what is still thin. Then send it to `/draft-posts`, which reads the
interview file first and builds from the answers rather than the transcript quote.

---

## Output template

```markdown
# Interview : [date]

**Ideas:** [n] selected from `[ideas file]`
**Status:** unanswered | partially answered | answered [date]

*Checked against published work first. Skipped anything already covered: [list].*

---

**1.** [Question]

*Unlocks: [what this makes draftable]*

**2.** [Question]

*Unlocks: [what this makes draftable]*

...

**8.** [The combined off-limits question]

*Unlocks: [keeps drafting away from what is not shareable]*

---

## Answers

*(filled in Step 5, verbatim, mapped by number)*

**1.** [their exact words]

**2.** [their exact words]

**[n]. SKIPPED** : [does the draft need it: yes/no]
```

---

## Edge cases

- **No ideas file yet:** run `/mine-calls` first, or ask which specific idea to interview on. Do not
  invent ideas to interview on.
- **They want to skip the interview:** fine. Say so plainly and go to `/draft-posts`. Note in the
  handoff that it ran without an interview, so the ghostwriter test is carrying the realness load
  alone, which it fails more often.
- **Answers thinner than the questions:** draft only what the answers support. A two-line answer
  produces a short post, not a padded one. Say which ideas did not get enough to draft.
- **They answer with a different, better story:** take the better story. Log the swap in the file so
  drafting knows the idea moved.
- **Dictation mangled a name:** check it against any people or client files before correcting.
  Recorders reliably mangle unusual proper nouns, and a wrong name in a published post is expensive.

## What not to do

- Do not ask questions whose answers are already in a file. Step 2 exists to prevent this.
- Do not clean up spoken phrasing when mapping answers. Draft from it later. Store it raw.
- Do not batch more than 5 ideas into one doc.
- **Do not exceed 8 questions, ever.** Not "8 per idea," not "8 plus a couple of sensitivity ones."
  Eight. Every question past that costs more in abandoned docs than it earns in detail. If more than
  8 look load-bearing, the selection in Step 1 is too wide: cut an idea, not the question quality.
- Do not write multi-part questions.
- Do not draft anything here. The output is answers, not posts.
- Do not proceed to drafting by guessing what they would have said.
