# Setup

## The fast way

Put this folder somewhere you work, open Claude Code there, and say:

> **set up Call Mining**

That runs `/call-mining-setup`, which installs the skills, finds your recorder, fills in the config
one question at a time, and runs calibration. Plan on about an hour, with no prior Claude Code
experience needed.

**Everything below is the manual version of that**, for anyone who would rather do it themselves or
needs to fix one piece later.

---

## 1. What you need

**Required:**
- Claude Code, running in a folder you use for work
- A place your writing can be saved. Any folder works.

**Strongly recommended:**
- A call recorder that produces transcripts: Grain, Fathom, Fireflies, Otter, Gong, Granola, or Zoom
  with transcription on. If it has an MCP connector, better. If it only exports text files, that
  works too.

**Helpful but optional:**
- 30 or more of your own past posts, for calibration. On LinkedIn, request your data archive a day
  ahead: Settings & Privacy, then Data privacy, then Download your data, and pick the larger
  download. Your posts come in `Shares.csv`.
- Engagement data on those posts (impressions especially)
- A file where you log open decisions

**You can run this with none of the optional things.** Every skill degrades to asking you directly
instead of reading a file.

---

## 2. Install

**Put the whole pack inside the project you work in, and keep it together.** The skills read
`config.md`, `reference/`, and `templates/` at runtime, so they need to find the pack.

```bash
# from your project root
cp -r /path/to/call-mining ./call-mining
```

Then copy the skills into where Claude Code looks for them:

```bash
mkdir -p .claude/skills
cp -r call-mining/skills/* .claude/skills/
```

That leaves you with:

```
your-project/
  .claude/skills/       mine-calls, interview, draft-posts, calibrate-voice,
                        call-mining-setup, call-mining-update
  call-mining/          config.md, reference/, templates/
```

**Want the skills available in every project instead?** Copy them to `~/.claude/skills/` rather than
`.claude/skills/`, and keep the pack itself at a stable path. The first time a skill runs it will ask
where the pack lives, once.

**Copy the two templates into place:**

```bash
cp call-mining/templates/corrections.md  <your-content-path>/corrections.md
cp call-mining/templates/voice-lint.md   .claude/rules/voice-lint.md
```

**If a skill name collides** with one you already have, rename the folder and the `name:` field in
its `SKILL.md` to match. Nothing else references the names.

Verify the install by asking Claude Code: "what skills do you have?" All six should appear.

---

## 3. Fill in config.md

**This is the only file you edit.** Open it and work through the six sections.

The two that matter most on day one:

**Recording source.** Declare three operations: how to list meetings in a date range, how to fetch
one transcript, and what to do when a transcript is missing. Filled-in examples for the common
recorders are in the file. If you have no recorder, set them all to `none` and you will paste
transcripts instead.

**Who you are.** The Buyer scoring lens cannot work without this. It needs to know who qualifies as a
real buyer, and ideally where a list of real people lives. If you skip it, the scoring gate will
happily approve drafts that only impress your peers.

Everything else can stay on its default for the first run.

---

## 4. Run calibration once

```
/calibrate-voice
```

It will look for your past posts, measure them, and write four files: `pov.md`, `voice.md`,
`patterns.md`, and `terms.md`.

Part of it is a conversation rather than a measurement. It reads your archive, drafts three to five
positions you appear to argue, and asks you to correct it. Correcting it is the point: "that one is
close but it is really about X" is a better outcome than agreeing, and it is why it shows you a draft
instead of asking what your POV is.

**If you have 20 or more posts,** it measures them and reports what it found, including anything that
contradicts what you believed about your own writing. That contradiction is usually the most useful
output of the whole run.

**If you have fewer than 20,** it says so and interviews you for six questions instead, then writes
the same three files marked as stated preference rather than measured. This is the honest outcome,
not a degraded one. It will tell you to re-run at 30 posts.

Re-run quarterly, or after 50 new posts.

---

## 5. Your first week

### Friday morning, 10 minutes

```
/mine-calls
```

Pulls the week's recordings, extracts 8-12 post ideas, each anchored to something you actually said,
and ranks the top three. It also scans for the two formats a recording cannot contain: a genuine open
question you are sitting on, and a loop from an earlier post that now has a result.

Read the ideas. Pick three.

### Friday, 15 minutes

```
/interview
```

Builds a doc of 6-8 questions. Not 6-8 per idea. Six to eight total.

Every question is load-bearing: it either unlocks a draft that cannot be written without it, prevents
a mistake, or marks what is off-limits. Each carries a one-line note saying what it unlocks, so you
can see what you cost the draft by skipping one.

**Answer them out loud.** Voice memo, dictation app, whatever. Then paste the transcript back. Do not
tidy it up first: the messy spoken version is the asset, and it gets kept verbatim.

Speaking rather than typing is the recommendation, not a preference. Typed answers get edited while
you write them: you compress, you formalize, you drop the aside that was the most useful part.
Talking gets several times more out of you. Typing works if you prefer it, it just gives the draft
less to build from.

This is the step everyone skips, and it is the reason most AI-assisted content reads like AI-assisted
content. The model is not the problem. The input is.

### Monday, 20 minutes

```
/draft-posts
```

Drafts from your answers, scores every draft against four lenses, revises anything under threshold,
and only then shows you the result one post at a time.

When you change a line, it writes down what it wrote, what you changed it to, and the rule underneath
before applying your edit. Next week it reads that log first.

---

## 6. How it gets better

Three loops, all running on their own.

**The corrections log.** Every edit you make becomes a rule written for the next post. At three
strikes, the rule graduates out of the log into the file that owns it: voice-lint if it is binary,
your voice file if it needs judgment. The log stays short on purpose.

**Recalibration.** Quarterly, or after 50 new posts. Your writing changes and feeds change. A
calibration file older than a quarter is a hypothesis, not a target.

**Updates.** Run `/call-mining-update` now and then. It checks the public repo and stops if you are
already current. Otherwise it replaces the system and leaves your config, your calibration files,
your corrections log, and anything you customized alone. It backs up the old version first, and
asks before touching a skill you edited.

**The published folder.** `/mine-calls` reads it to find loops worth closing and to flag overlap.
`/interview` reads it to avoid asking what you already answered publicly.

---

## 7. Optional: schedule the Friday run

If your setup supports scheduled tasks, point one at Friday morning with the instruction: invoke
`mine-calls` and follow it end to end.

Two things to get right in the scheduled version:

- **It must never need a click.** An unattended task that stops for approval is a task that silently
  does nothing. Mining and writing a file are safe to automate. Posting is not.
- **It should not draft.** The scheduled run produces ideas and stops. Drafting needs your interview
  answers, and those cannot be scheduled.

---

## 8. Troubleshooting

**"No calls found this week."** Check that the list-meetings operation in `config.md` matches a tool
Claude Code can actually call. Ask it: "what tools do you have for my recorder?"

**"My recorder has no MCP."** Export transcripts to a folder and set the recorder rows to
`read files in <path>`. Everything downstream is identical.

**"I have no recorder at all."** Set every recorder row to `none`. `/mine-calls` will ask you to
paste transcripts. You can also paste notes from a call you did not record: the four classification
questions work on any account of a real conversation.

**"LinkedIn only gave me the last year of posts."** LinkedIn's analytics export stops at 365 days.
Request the full data archive instead (see What you need). If you still end up under 20 posts, paste
older ones in by hand from your activity page.

**"The interview asks about things I already wrote about."** Point `config.md` at your published
folder. Step 2 of the interview reads it specifically to avoid this.

**"Every draft scores 8 or higher on the first pass."** The scoring is grading generously, which
usually means the Buyer lens has no real reader to check against. Fill in the reader list in
`config.md`. If nobody real comes to mind for a post, that lens is capped at 6 by design.

**"The drafts do not sound like me."** In order of likelihood: calibration has not run, you skipped
the interview, or the corrections log is empty because you have been approving drafts without
editing them. The third one fixes itself over a few weeks.

**"It used an em dash."** It is in voice-lint for exactly that reason. Tell it, and log the
correction.

---

## 9. What this system will not do

- **It will not post for you.** Every skill stops at a draft you approve.
- **It will not invent a number, a quote, or a client detail.** When the raw material does not support
  a claim, it flags a gap instead of filling it. This is the constraint that makes the output usable.
- **It will not make you sound like somebody else.** There are no borrowed benchmarks in here. The
  voice comes from your posts and your answers.
- **It will not write good posts from nothing.** If you did not have interesting conversations this
  week, it will tell you that instead of padding the list.
