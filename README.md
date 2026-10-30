# Call Mining

`v1.1.0` : see [CHANGELOG.md](CHANGELOG.md). Update with `/call-mining-update`.

**Turn the calls you already had into the posts you never get around to writing.**

You said something genuinely good on a client call this week. A specific number, a sharp reframe, an
argument you lost. It is sitting in a transcript nobody will ever open again.

This is a system for Claude Code that finds those moments, asks you the handful of questions a
recording could not capture, and drafts from your answers.

---

## Start here

Download it with the green **Code** button, then **Download ZIP**, and unzip it somewhere you work.
Or clone it: `git clone https://github.com/garrett-jestice/call-mining.git`

Open Claude Code in that folder. Say:

> **set up Call Mining**

It installs itself, works out which call recorder you use, asks you six questions, and learns your
writing from your past posts. About 15 minutes, and you do not need to have used Claude Code before.

Prefer to do it by hand? [SETUP.md](SETUP.md) has every step.

---

## The weekly loop

```
/mine-calls     Friday, 10 min    Pulls the week's recordings, ranks 8-12 post ideas
/interview      15 min            It interviews you: 6-8 questions, answered out loud
/draft-posts    Monday, 20 min    Drafts, scores, reviews one at a time
```

Two more you run rarely: `/call-mining-setup` once at the start, and `/calibrate-voice` once at setup
and then quarterly.

---

## Why the middle step exists

Most AI content tools go straight from transcript to draft. That is why the output reads the way it
does.

A transcript holds what you said to somebody else, weeks ago. It does not hold what you were actually
thinking, the number you chose not to cite, the thing you almost said instead, or the moment you
realized you were wrong. **Those are the only parts that make a post yours,** and they were never
recorded.

So the system stops and asks. Six to eight questions total, never more, each one load-bearing enough
that skipping it visibly costs the draft. Answer them out loud and paste the transcript back messy.
Speaking is not a preference here: typed answers get edited as you write them, and the compressing is
exactly what strips out the phrasing worth keeping. Your spoken wording is kept verbatim.

Realness cannot be generated. It can only be retrieved.

---

## What is actually in here

**A scoring gate that runs before you see anything.** Every draft gets scored 1 to 10 on four lenses:
would a real buyer comment on this, does it survive the sharpest objection, is the writing any good,
and could a ghostwriter have written it. **The gate is the lowest score, not the average.** Anything
under 8 gets revised, twice, and if it still fails it comes to you with the failing lens named and
the specific line quoted.

**A learning loop.** When you change a line, the system writes down what it wrote, what you changed it
to, and the rule underneath, before applying your edit. Next week it reads that log first. At three
strikes a rule graduates into your permanent style file. The gap between what you were shown and what
you approved is the sharpest signal about your taste that exists, and normally it evaporates in chat.

**A through-line, not just good posts.** Setup drafts what you appear to argue from your own archive
and hands it to you to correct. After that, every idea gets tagged against it: does this reinforce
what you are known for, or is it just a strong moment? It never filters on that. An idea that
contradicts your stated position gets flagged as the most valuable one on the list, because changing
your mind in public is the strongest post available.

**No borrowed benchmarks.** The writing guidance ships in two layers. A thin universal file holds only
what is true for everyone: the hook has to earn the click, one idea per post, nothing invented, and
the list of AI tells to scrub. Everything measurable, rhythm and length and format mix, comes from
`/calibrate-voice` reading **your** posts. Rules like "keep it to 12 paragraphs" are one person's
measurements wearing a lab coat. Yours will be different.

**A hunt for what recordings cannot hold.** Two of the strongest post formats never appear in a
transcript: a genuine open question you would actually act on, and a loop from an earlier post that
now has a result. The system looks for them somewhere else, deliberately, every week.

---

## What it will not do

- Post anything. Every skill stops at a draft you approve.
- Invent a number, a quote, or a client detail. Gaps become open questions, not filler.
- Pretend to measure your voice from six posts. It says so and interviews you instead.
- Pad the list when you had a boring week. It will just tell you.

---

## Getting started

Open Claude Code in this folder and say **"set up Call Mining"**. That is the whole thing.

If you would rather do it manually, [SETUP.md](SETUP.md) walks through every step: copy `skills/`
into your Claude Code skills folder, fill in `config.md`, run `/calibrate-voice` once, then run
`/mine-calls` on Friday.

```
README.md      you are here
SETUP.md       the build walkthrough
config.md      the only file you edit
VERSION        what you are running. Include it in any bug report.
CHANGELOG.md   what changed, and what each update needs from you
skills/        the six skills
reference/     universal writing mechanics, and how to measure your own posts
templates/     the corrections log and the voice-lint gate, both start near-empty
```

Run `/call-mining-update` when there is a new version. It updates the system and leaves your config,
calibration, corrections log, and any customizations untouched.
