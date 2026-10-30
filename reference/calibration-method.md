# Calibration Method

How to derive writing targets from someone's own posts instead of inheriting somebody else's.

This file is the method. `/calibrate-voice` is what runs it. The output lands in the calibration
folder named in `config.md`.

---

## Why this exists

Most LinkedIn advice is one person's measurements, generalized. The numbers were real when they were
taken, on that account, with that audience. They travel badly, and they travel silently: a rule like
"keep posts to 12 paragraph blocks" arrives with no sample size, no date, and no account attached, so
there is no way to tell whether it applies.

Calibrating against your own posts fixes the attribution problem. It also surfaces what you already
do well, which is usually more useful than what a playbook says you should do.

**It does not fix everything.** Your own history calcifies your habits, including the bad ones, and
it says nothing at all if you have barely posted. Both cases are handled below.

---

## The five rules

### 1. Rank by rate, never by totals

Total reactions mostly measure how far a post travelled, and reach is distributed unevenly for
reasons unrelated to quality. A post that reached 20,000 people and got 200 reactions performed worse
than one that reached 1,000 and got 60.

Use **engagement rate**: interactions divided by impressions. If impressions are not available, use
comments divided by reactions as a secondary signal, which measures how hard the post made people
work.

Reach and rate can correlate negatively. Ranking by totals will hand you the wrong lessons with high
confidence.

### 2. Record provenance on every number

Every line in the output files carries: **the date measured, the sample size, and the source.**

```
Paragraph blocks: 14-20 works best (measured 2026-08-04, n=312 posts with impressions, LinkedIn export)
```

Not:

```
Paragraph blocks: 14-20
```

A number without provenance cannot be re-evaluated later, and it cannot be told apart from a number
somebody made up.

### 3. Write down contradictions instead of overwriting them

When a re-measure disagrees with what the file said before, **keep both and date them.**

```
Posts opening on a client story: 1.09x baseline rate (measured [date], n=[full set])
  Superseded: an earlier pass on a partial set scored these at 1.28x ([earlier date], n=[small set]).
  The larger sample is the better estimate. Noting it because the 1.28x figure had already
  been quoted in two other places before the correction.
```

This is the habit that separates a calibration file from a pile of assertions. It also catches the
case where the first measurement was taken on a sample too small to mean anything, which is common
and easy to forget.

### 4. One account is never evidence about the platform

If your data disagrees with a widely repeated rule, that is interesting but not conclusive. Record
the disagreement, note that it is a single account, and do not rewrite the rule as universal.

The same applies in reverse: your calibration describes you. It is not advice for anyone else.

### 5. Re-run quarterly, or after 50 new posts

Whichever comes first. Feeds change, audiences change, and your writing changes. A calibration file
older than a quarter should be treated as a starting hypothesis, not a target.

---

## What to measure

Pull the last 30-50 posts. More is better up to a few hundred. Then measure:

**Rhythm**
- Average sentence length in words
- Average paragraph blocks per post
- Share of blocks that are a single sentence
- Reading level

**Shape**
- Word count, and how it correlates with rate
- Hook length in characters, and how many exceed the mobile fold
- Opener type: second person, first person, question, number, quote, claim. Rate for each.
- Closer type: line, question, CTA. Rate for each.

**Mix**
- Format distribution: story, list, observation, rant, ask, and the rest
- Classification distribution: Problem, Process, Proof, Personal
- Business to personal ratio
- Posting cadence, and whether rate holds as volume rises

**Language**
- Terms and concepts that recur across posts. These are the ones worth repeating on purpose.
- Words and constructions that never appear. This is often the most useful output, because it
  defines the voice by its edges.
- Contractions, sentence fragments, profanity, emoji: present or absent, and how consistently

**Signals other than reactions**
- Saves, if available. They behave differently from reactions and often reward different posts.
- Comment to reaction ratio, per post and overall

---

## What to do with a small sample

**Under about 20 posts, do not pretend to measure.** Correlations on that little data are noise, and
a confident-sounding file built on noise is worse than no file.

Instead:

1. Say plainly how many posts were found and that it is not enough to derive targets from
2. Fall back to the universal defaults in `writing-mechanics.md`
3. Run a short stated-preferences interview: what they want to sound like, whose writing they
   admire and specifically what about it, what they would never say, what they say constantly
4. Write the output files with `basis: stated preference, not measured` on every line
5. Set a re-run trigger at 30 posts

Stated preferences are weaker than measurements but they are honest, and they are far better than
inheriting a stranger's numbers.

---

## Output files

Three files, in the calibration folder from `config.md`.

**`voice.md`** : register and identity. What they sound like, what they never do, the constructions
that are theirs, the ones that are off-limits. Mostly qualitative.

**`patterns.md`** : the measured targets. Rhythm, shape, mix, cadence. Every line carries provenance.
This is the file `/draft-posts` scores the Editor lens against.

**`pov.md`** : what they argue, what they argue against, and the through-line under posts that look
unrelated. **This one is derived and then corrected, not measured.** Read the archive, draft three to
five positions with the evidence attached, and hand it to them to fix. Asking someone to state their
POV cold produces a mission statement. Showing them a draft of what they appear to believe produces a
correction, and the correction is the useful part.

Re-derive it when the other files get re-measured, and expect it to move faster than they do.

**`terms.md`** : the words, concepts, and named ideas they repeat on purpose, plus the ones to avoid.
Repetition across posts is what turns scattered content into a body of work, so this file exists to
make the repetition deliberate rather than accidental.

Each file opens with a header:

```
Calibrated: [date]
Sample: [n] posts, [date range]
Source: [export, MCP tool, manual paste]
Engagement data: [available / not available]
Re-run at: [date, or n posts]
```
