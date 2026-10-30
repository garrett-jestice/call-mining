---
name: calibrate-voice
description: Derive the user's own writing targets from their own published posts, instead of inheriting someone else's rules. Reads their last 30-50 posts, measures rhythm, shape, format mix, and recurring language, and writes voice.md, patterns.md, and terms.md into the calibration folder. Run once at setup, then quarterly or after 50 new posts. Falls back to a stated-preferences interview when there are too few posts to measure honestly. Use when the user says /calibrate-voice, "calibrate my voice", "learn my writing style", "analyze my posts", or when draft-posts reports that calibration has not run yet.
---

# Calibrate Voice

Run once at setup. Re-run quarterly or after 50 new posts.

**Read `reference/calibration-method.md` before starting.** It holds the five rules this skill
enforces, and the reasoning behind them. This file is the procedure; that file is the method.

**Read `config.md`** for the calibration output path and the platform.
Look for the pack in `call-mining/` at the project root, or beside this skill file. If you cannot find it, ask the user for the pack path once, then continue.

---

## Why this runs at all

The alternative is shipping somebody else's numbers as rules. Those numbers were real when they were
taken, on that account, with that audience, and they arrive with no sample size and no date attached
so there is no way to tell whether they apply.

The output of this skill is three files that describe **this user** and say exactly how confident
they are.

---

## Step 1: Get the posts

Work down this list. Stop at the first one that works.

1. **A platform MCP** that can list the user's own posts with engagement data. Best case: it gives
   impressions, which makes rate calculable.
2. **A content tool's export or MCP** (post schedulers and analytics tools often hold this history).
3. **A platform data export.** Most platforms let a user download their own post archive. Ask them to
   run it and point at the file.
   **On LinkedIn, use the full data archive.** The analytics export has impressions but stops at 365
   days. The archive (Settings & Privacy, then Data privacy, then Download your data, and pick the
   larger download) holds their posts in `Shares.csv` without impressions. LinkedIn says it can take
   up to 24 hours, so offer to pick this step back up when it lands. If it comes up short, top it up
   with a manual paste (item 4). Never recommend a scraper or a LinkedIn automation tool to fill the
   gap: automated access puts their account at risk.
4. **A manual paste.** Ask for their last 30-50 posts. Tedious, but it works, and text alone still
   supports every rhythm and language measurement. Only the rate-based rankings are lost.

Report what was found: how many posts, what date range, and whether engagement data came with them.

**Never proceed silently on a thin sample.** The count determines which path runs next.

## Step 2: Check the sample size

**20 or more posts:** go to Step 3.

**Fewer than 20:** go to Step 7. Do not measure. Correlations on that little data are noise, and a
confident file built on noise is worse than no file at all.

## Step 3: Measure

Per `calibration-method.md`. **Rank by engagement rate, never by totals.** If impressions are
missing, use comments divided by reactions as the secondary signal.

Measure across four groups:

- **Rhythm** : average sentence length, average paragraph blocks per post, share of blocks that are a
  single sentence, reading level
- **Shape** : word count and its correlation with rate, hook length in characters and how many exceed
  the mobile fold, opener type with rate for each, closer type with rate for each
- **Mix** : format distribution, classification distribution (Problem / Process / Proof / Personal),
  business to personal ratio, posting cadence
- **Language** : recurring terms and named concepts, constructions that never appear, and whether
  contractions, fragments, and emoji are present

Also pull saves and comment-to-reaction ratio if the data has them. They reward different posts than
reactions do.

**Split the top and bottom quartile by rate and compare them.** The difference between the two is the
finding. An average across all posts describes the user's habits; the gap describes what works.

## Step 4: Sanity-check every number before writing it

Three questions per measured claim:

1. **How many posts is this based on?** If a cut leaves fewer than 10 posts, say so on the line
   rather than reporting it as a target.
2. **Could reach explain this instead of quality?** Recheck against rate.
3. **Does this contradict something the user believes?** If yes, that is worth surfacing explicitly.
   It is the most valuable output of the whole run.

## Step 5: Draft their POV and have them correct it

A body of work needs a through-line. Without one the system reliably finds good individual posts that
add up to nothing, because it has no way to tell a strong moment that reinforces what they argue from
a strong moment that just happened to be strong.

**Do not ask them to state their POV cold.** Almost nobody can, and what comes back is usually a
mission statement. A vague POV is worse than none, because everything downstream keys on it.

Derive it instead. You have just read their whole archive.

### Read for these

- **What they argue that their peers do not.** The position they take repeatedly that is not the
  consensus in their field.
- **What they argue against.** Often sharper and easier to spot than what they are for. Look for the
  recurring "everyone does X, and X is wrong."
- **The problem they keep naming.** The thing they diagnose over and over, in different clothes.
- **What they refuse to do or sell**, when they say it publicly.
- **The through-line they may not see.** Three posts that look unrelated but rest on the same
  underlying claim. This is the most valuable thing you can hand them.

### Then show them a draft, not a question

Write three to five sentences in plain language, in their own vocabulary where possible, and put the
evidence next to it:

```
Here is what you appear to believe, based on [n] posts:

1. [Position], which shows up in [post], [post], and [post].
2. [Position they argue against], most directly in [post].
3. [The through-line they may not have named]: [claim].

Does that land? Tell me what is wrong, missing, or stated too weakly.
```

**Getting a correction is the goal, not agreement.** "That third one is close but it is really about
X" is a better outcome than "yep, looks right," and it is the reason this runs as a draft rather than
a question. Push once if they only say yes: ask which of the three they would actually defend in an
argument.

### Write it out

Save to `calibration/pov.md`, with the same provenance header as the other files:

```markdown
# POV

Drafted from [n] posts on [date]. Corrected by them on [date].

## What I argue
- [position] : evidence in [posts]

## What I argue against
- [position] : evidence in [posts]

## The through-line
[one or two sentences]

## Where I am uncertain
[anything they flagged as still forming. Useful later: an unresolved position is
where the genuine ask posts come from.]
```

**If they have too few posts to derive from**, this moves to the Step 7 interview instead. Ask what
they believe about their work that most people in their field would push back on, and what they find
themselves arguing with clients about. Mark it `basis: stated, not derived`.

### The constraint that carries downstream

**POV ranks and labels. It never filters.** `/mine-calls` tags every idea against this file, and a
moment that contradicts their stated POV gets flagged as high value rather than dropped. Somebody
changing their mind in public is the strongest post available, and a filter would quietly destroy
exactly that material. Say this to them when you write the file, so they do not expect the system to
start ignoring off-message ideas.

---

## Step 6: Write the files

Into the configured calibration folder. Every file opens with the provenance header from
`calibration-method.md`: date, sample size, source, whether engagement data was available, and the
re-run trigger.

**`pov.md`** : what they argue, what they argue against, and the through-line. Written in Step 5.

**`voice.md`** : register and identity. What they sound like, what they never do, constructions that
are theirs, what is off-limits. Mostly qualitative, drawn from reading the posts rather than counting
them.

**`patterns.md`** : the measured targets. Every line carries its own provenance. This is the file
`/draft-posts` scores its Editor lens against, so a vague line here weakens the whole gate.

**`terms.md`** : words, concepts, and named ideas they repeat on purpose, plus what to avoid.
Repetition across posts is what turns scattered content into a body of work.

**If a re-measure contradicts what a file said before, keep both and date them.** Do not overwrite.
The superseded number and the reason it was wrong are part of the record, and the most common cause
is that the first pass ran on a sample too small to mean anything.

## Step 7: The small-sample path

Under 20 posts. Say the count out loud and say plainly that it is not enough to derive targets from.

Then:

1. Fall back to the universal defaults in `reference/writing-mechanics.md`
2. Run a short stated-preferences interview. Six questions, one at a time:
   - Who are you writing for, and what do they already believe that you disagree with?
   - Whose writing do you admire, and what specifically about it?
   - What would you never say, or never say that way?
   - What do you find yourself saying constantly, in calls or in writing?
   - Which of your own posts felt most like you, and why that one?
   - What do you want a reader to think about you after five posts?
3. Write the three files with **`basis: stated preference, not measured`** on every line
4. Set the re-run trigger at 30 posts

Stated preferences are weaker than measurements. They are also honest, and far better than inheriting
a stranger's numbers.

## Step 8: Report and update config

Show the user:

- Sample size, date range, and whether rate was calculable
- The three or four findings that would actually change a draft
- Anything that contradicted what they believed about their own writing
- Anything the sample was too thin to answer

Then update the **Status** line in `config.md`:

```
**Status:** calibrated [date], n=[posts]
```

or, on the small-sample path:

```
**Status:** stated preference only [date], n=[posts], re-run at 30
```

`/draft-posts` reads that line and falls back to universal defaults when it still says not yet
calibrated.

---

## Edge cases

- **No engagement data, text only:** normal, and fine. Rhythm, shape, and language all still measure.
  Say clearly that the rate-ranked findings are unavailable, and do not substitute totals for rate.
- **Posts are mostly reshares or one-liners:** measure the original longer-form posts only, and say
  how many that left.
- **The user disagrees with a finding:** record their objection in the file next to the number.
  Do not delete the measurement, and do not let it silently override their judgment either. Both
  belong on the record.
- **Two distinct voices in the sample** (for example, a pivot in what they write about): measure the
  recent period and say where the split is.
- **The sample is all from one strong month:** flag it. A calibration built on an unusual stretch
  describes that stretch.

## What not to do

- Do not rank by totals. Ever. It is the fastest way to learn the wrong lesson confidently.
- Do not report a number without its sample size and date.
- Do not overwrite a superseded number. Date it and keep both.
- Do not generalize a finding from one account into a rule about the platform.
- Do not measure a sample under 20 posts. Take the Step 7 path instead.
- Do not invent a target because a file expects one. `not enough data` is a valid value.
- Do not recommend a scraper or a LinkedIn automation tool for pulling posts. It puts their account
  at risk.
