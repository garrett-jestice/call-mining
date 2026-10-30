---
name: mine-calls
description: Mine recent call recordings for post ideas. Pulls transcripts from whatever recorder is declared in config.md, extracts moments via four classification questions (Problem/Process/Proof/Personal), and outputs 8-12 ranked post ideas, each with a verbatim quote, a hook, two format options, and an angle. Also scans non-transcript sources for the two formats a recording cannot contain: a genuine open question, and a loop from an earlier post that can now be closed. Use when the user says /mine-calls, "post ideas from my calls", "mine my calls", "weekly content ideas", or "what should I post about this week". For drafting the actual posts, use draft-posts instead.
---

# Mine Calls

Turn the week's recorded conversations into ranked post ideas, each one anchored to something the
user actually said out loud to a real person.

## Why this works

Posts built from real conversations beat posts written from a blank page. They carry specific
numbers, real objections, and the language the audience already uses. Nobody scrubs their own
transcripts by hand every week, which is why the good material sits there unused. This extracts it
systematically.

**Read `config.md` before doing anything.** It declares the recorder, the file paths, and who the
user sells to. Everything below refers to it.

Look for the pack in `call-mining/` at the project root, or beside this skill file. If you cannot find it, ask the user for the pack path once, then continue.

---

## Step 0: Set the window

Default to the current week: the configured week-start day at 00:00 through now, local time. If the
user names a different range ("last two weeks", "since Thursday"), use that.

## Step 1: Get the calls

Call the **list meetings** operation declared in `config.md` with the date range.

Then for each meeting:
- Skip anything under the configured minimum length (default 5 minutes)
- Call the **fetch transcript** operation
- If the transcript is missing, call the **fetch notes** fallback
- If both are missing, put the meeting in a "skipped" list with the reason and move on

Internal one-on-ones count. Client calls count. Sales calls count. A good moment does not care who
was on the other end.

**If no recorder is configured:** ask the user to paste transcripts, or point at a folder of text
files. Everything downstream is identical.

## Step 2: Mine each transcript with four questions

Read the full transcript. Not the summary. The summary is where the specificity goes to die.

For each call, ask:

1. What did someone not know before this call that they know now? → **Problem** posts
2. What did the speaker walk them through step by step? → **Process** posts
3. Did anything work: a milestone, a result, a specific number? → **Proof** posts
4. Did anything surprise or frustrate the speaker? → **Problem / Personal** posts

**Pull the direct quote first. Classify second.** Do not summarize before quoting. The specificity of
the original wording is the entire asset, and summarizing destroys it before anyone gets to use it.

Cap at 2-5 sparks per call. If a call has one strong moment, that is one spark. Quality over output
quota: a weak forced spark dilutes the whole batch and makes the selection step harder.

**Never suppress an idea because the topic was published recently.** Rank purely on the strength of
the moment. If material overlaps something already published, keep it on the slate and add a one-line
note naming the overlap and the fresh angle: a counterargument, a new result, a loop to close.
Freshness is a label, never a filter. The user decides what is too repetitive, and repeating your own
terms on purpose is how a body of work gets built.

The one standing exclusion has nothing to do with freshness: **do not take material someone else on
the call plans to post themselves.** That is about attribution.

## Step 3: Two format options per spark

For each spark, offer two delivery formats from:

**story, list, sarcastic, rant, conversation, observation, ask**

Same insight, different vehicles. The user picks what fits their week.

**The `ask` format has a hard gate.** Only offer it when the spark surfaces a question the user
genuinely does not have the answer to and would act on. A real open decision, a real fork, a real gap.
Never a rhetorical question dressed as an ask, and never "what would you add?"

The test: **if you cannot name what the user would do differently depending on the answers, it is not
an ask.** It is engagement bait, and readers can tell.

Most transcript sparks will not qualify. The genuine ask usually comes from Step 5 instead.

## Step 4: Write a hook for each spark

Every hook must contain at least one of:

- A specific number
- A specific detail from the conversation
- A contrarian claim
- A real scenario
- **A self-implicating admission**: something the user got wrong, named specifically

On that last one. If the spark contains a moment where the user changed their mind, lost an argument,
talked a client out of something they sell, or ran into evidence that contradicted their own
position: **the admission goes in the hook, not the middle of the post.** Vague versions ("I've made
mistakes") do not count. It has to be the specific thing, and it has to cost something to say.

This is the highest-trust opener available and almost nobody uses it, because it is uncomfortable and
because the raw material for it is buried in transcripts nobody re-reads.

**Banned openers:** "I've been thinking about...", "Let me share...", "Here's the thing...", or
anything else that delays the payload. Lead with the friction or the number.

## Step 5: Scan for off-transcript candidates

A recorder only holds conversations. Two of the strongest formats never appear in one, so they have
to be hunted deliberately or they never get made.

**If `config.md` names a decisions log or a task list,** read them: newest entries first, plus
anything flagged unresolved. Also read the last six weeks of the published folder.

**If both are `none`,** ask the user two questions directly:
- "What decision are you sitting on right now that you have not made?"
- "Is there anything you said publicly in the last couple months that now has a result?"

Then surface **at most one of each**, and only if it genuinely clears the bar.

**A. Genuine ask.** An open decision the user has to make anyway and would act on the answers to.
Show: the decision, the real shortlist or fork, why it is still open, and any deadline forcing it.
If it has no deadline and no live consequence, skip it. Note that this format only works if the user
can be in the comments that day.

**B. Open loop to close.** A question they asked publicly, an experiment they announced, or a
position they took that now has a result. Include results that went badly: **a loop closed with a bad
outcome is stronger than one closed with a good one.** Show the original post and date, what happened
since, and what the follow-up would say.

Both draw on things the user already decided or already published. Nothing here is invented.

If neither clears the bar, say "no off-transcript candidate this week" and move on. Forcing one
produces exactly the manufactured-vulnerability post that everyone can smell.

**These sit outside the 8-12 cap.**

## Step 6: Present the sparks

Group by call. For each spark show:

- **Quote / Moment** : the verbatim line or exchange from the transcript
- **Classification** : Problem / Process / Proof / Personal
- **POV** : on / adjacent / off / **contradicts** (see below)
- **Hook** : the opening line of the post
- **Formats** : two options
- **Angle** : one line on what the post argues or reveals

Target 8-12 total across all calls.

### The POV tag

**Only if `calibration/pov.md` exists.** Skip this field entirely when it does not, rather than
guessing at what the user believes.

Tag each spark against what they argue:

| Tag | Meaning |
|---|---|
| **on** | Reinforces a position in their POV file. Builds the through-line. |
| **adjacent** | Same territory, does not advance a stated position. |
| **off** | Good moment, unrelated to what they are known for. |
| **contradicts** | Cuts against something they have publicly argued. |

**`contradicts` is the highest-value tag, not the lowest.** Somebody changing their mind in public,
losing an argument, or running into evidence against their own position is the strongest post
available. Flag it, say which position it cuts against and where they argued it, and push it toward
the Top 3. This pairs with the self-implicating hook in Step 4: the admission goes in the hook.

**POV ranks and labels. It never filters.** Never drop a spark for being `off`, and never suppress a
`contradicts`. Same rule as freshness. The user decides what to write; this only tells them what each
choice does to the body of work.

## Step 7: Newsletter candidates (only if the newsletter branch is `on` in config.md)

Skip this step entirely when the branch is off. That is the default.

When on, review the sparks against a short-issue shape (a cold open scene, the turn, one idea, a
small exercise, one closing line). Flag 1-3 candidates. A candidate needs all four:

- A real scene with a person in it, anonymized
- One idea with a mechanism underneath: why it happens and what it quietly costs, enough for 500-800
  words and not a full framework
- A verbatim quote strong enough to serve as proof
- A small this-week exercise a reader could run in minutes

For each, show the source sparks, three subject line options (a spoken quote, a plain claim, and a
named concept only if a name genuinely earns it), and a five-line spine sketch.

If nothing clears the bar, say "no newsletter candidate this week." Never force one.

## Step 8: Close the report

- **Top 3 to develop first**, and why: strongest hook, freshest angle, most specific number. Where
  two sparks are close, the one tagged `on` or `contradicts` wins, because it does something for the
  body of work that a strong but unrelated moment does not. **Moment strength still comes first:** a
  great `off` spark beats a mediocre `on` one, every time. An off-transcript candidate from Step 5 is
  eligible and should win a slot when it is genuinely stronger than the third transcript spark.
- **If every spark this week is `on`**, say so. A run with no friction in it usually means the mining
  got comfortable, not that the week was. Point at the strongest `off` or `adjacent` spark as the one
  worth considering anyway.
- **Save** the full report to the configured ideas path as `YYYY-MM-DD_ideas.md`
- **Hand off to `/interview`.** Tell the user the next step is an interview doc on the Top 3, and
  offer to build it now.

That last step matters more than it looks. Sparks are what the user said to somebody else, weeks ago,
filtered through a model. The interview is what they actually think about it now. **Do not draft
without it unless the user says to skip.**

---

## Output template

```
# Post Ideas : [date range]

## [Call title] ([duration], [date])

### Spark 1
**Quote:** "[verbatim from transcript]"
**Classification:** [Problem / Process / Proof / Personal]
**POV:** [on / adjacent / off / contradicts : if contradicts, which position and where they argued it]
**Hook:** [one-line opener]
**Formats:** [format A] | [format B]
**Angle:** [one line]

### Spark 2
...

## Off-transcript candidates

### Genuine ask : [the decision]
**The decision:** [what is actually open]
**The options:** [real shortlist or fork]
**Still open because:** [why]
**Forcing function:** [deadline, or "none" : if none and no live consequence, skip this candidate]
**Note:** only run this if the user can be in the comments that day.

### Open loop to close : [the earlier post]
**Original:** [date, what they asked or claimed]
**What happened since:** [the result, including bad ones]
**The follow-up says:** [one line]

(or "No off-transcript candidate this week.")

## Top 3 to develop first
1. [Spark reference] : [why]
2. [Spark reference] : [why]
3. [Spark reference] : [why]
```

---

## Edge cases

- **No calls this week:** say so directly. Do not pad. Suggest widening the window.
- **All calls under the minimum:** same. Report what was found and stop.
- **Transcript missing:** use the notes fallback. If notes are also missing, list the meeting as
  skipped with the reason.
- **Sensitive content:** flag any spark that names or quotes someone in a way that needs their
  approval first. **Do not strip the quote.** Flag it and let the user decide.
- **Someone else plans to post it:** leave it with them. Note it in a "do not use" line with the
  reason. This is the one hard exclusion.
- **No off-transcript candidate:** normal. Open decisions do not arrive on a weekly schedule.

## What not to do

- Do not invent quotes. Every quote comes from a transcript or it does not exist.
- Do not write full post drafts. The output is raw material. Drafting is a separate step, and it
  needs the interview in between.
- Do not classify the same moment twice. Pick the strongest fit.
- Do not exceed 12 sparks. More volume makes the user's selection worse, not better.
- Do not manufacture an ask.
- Do not drop or downrank a spark for being off-POV, and never bury one that contradicts their stated
  position. POV is a label and a tiebreaker, never a filter.
- Do not tag POV at all when `calibration/pov.md` does not exist. Guessing what someone believes is
  worse than leaving the field off.
