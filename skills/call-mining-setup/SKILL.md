---
name: call-mining-setup
description: Install and configure the Call Mining system for a first-time user. Copies the four skills into place, detects which call recorder is connected, fills in config.md one question at a time, installs the templates, and offers to run calibration. Use when the user says "set up Call Mining", "install Call Mining", "/call-mining-setup", "help me set this up", "get this working", or when they have the Call Mining pack in their folder and have not configured it yet. Also use when a Call Mining skill reports that config.md is missing or unfilled.
---

# Call Mining Setup

**Assume the user has never used Claude Code before.** Do the work for them rather than telling them
what to do. Ask one question at a time. Never present the whole config file as a form to fill in.

The whole thing takes about an hour of their attention.

---

## Step 0: Orient

Find the pack. It is the folder containing `config.md`, `skills/`, `reference/`, and `templates/`.
Usually `call-mining/` in the current directory.

If you cannot find it, ask where they unzipped it.

Then say what this is, briefly, in your own words: a system that reads their call recordings, finds
what is worth posting about, asks them a few questions a recording could not answer, and drafts from
those answers. Three commands, once a week.

Ask: **"Ready to set it up? Plan on about an hour."**

If they post on LinkedIn, ask them to request their data archive before anything else: Settings &
Privacy, then Data privacy, then Download your data, and pick the larger download. LinkedIn says it
can take up to 24 hours, and Step 5 reads their past posts from it. Skip this if their posts already
live somewhere you can read.

## Step 1: Install the skills

Do this yourself. Do not print instructions.

```bash
mkdir -p .claude/skills
cp -r <pack>/skills/* .claude/skills/
```

Check for name collisions with skills they already have. If one collides, rename the folder and the
`name:` field inside its `SKILL.md`, and tell them the new name.

Then confirm: six skills are now installed, and list them.

**Record the version.** Read `VERSION` from the pack and write it into the Updates section of
`config.md`. It is what makes a bug report actionable later.

**If they have never used Claude Code**, add one sentence: a skill is a set of instructions Claude
loads when it is relevant, and they invoke these by typing the slash command or just asking in plain
language.

## Step 2: Find their recorder

**Check what is actually connected before asking them anything.** Look for meeting or transcript
tools among the tools available to you: Grain, Fathom, Fireflies, Otter, Gong, Granola, Zoom, or
anything else that can list meetings and return a transcript.

**If you find one:** say which one, confirm it is the one they use, and move on. Do not make them
choose.

**If you find none, ask what they use to record calls.** Then take the matching path.

### They already use a recorder, it is just not connected to Claude

Say which one they named and walk them through connecting it:

1. Open their Claude connector settings (in the Claude app or on claude.ai, under Settings then
   Connectors). If they are in a terminal Claude Code session, `/mcp` lists and adds connectors there
   instead.
2. Find their recorder in the directory and authorize it. It opens a normal sign-in page for that
   tool.
3. Come back and say "done," and you will re-check.

**You cannot do this part for them.** Authorizing a connector requires them to sign in themselves.
Say that plainly rather than trying and failing.

If their tool has no connector available, ask whether it can export transcripts to a folder. Most can.
That is a fully supported path: they export, and the system reads the files.

### They do not record calls yet

This is worth fixing, because it is the input the whole system runs on. Recommend two or three and
let them pick. Describe what makes each different, and **do not quote prices or plan limits**, since
those change and a wrong number here costs them money.

- **Fathom** : joins your calls as a notetaker and has a Claude connector. Common default choice.
- **Fireflies** : joins your calls, has a Claude connector, strong search across past meetings.
- **Grain** : joins your calls, has a Claude connector, built around pulling clips and quotes out of
  recordings, which suits this system well.
- **Granola** : a Mac app that records from your machine rather than joining as a visible bot
  participant. Worth naming if they dislike a notetaker showing up in the meeting.
- **Zoom, Teams, or Meet** : if they already use one, turning on cloud recording with transcription
  may be enough. No new tool, but the transcripts are usually harder to get at.

The only real requirement: **it has to produce a text transcript they can reach**, either through a
Claude connector or by exporting files.

Tell them what to do:

1. Pick one and sign up. Most connect to their calendar and start joining calls automatically.
2. Record at least one real call.
3. Come back and say "set up Call Mining" again, and you will connect it.

Then offer to **finish setup now anyway**, so it is ready when their first recording lands. Say the
one thing that will actually matter: recording has to be running before there is anything to mine, so
the sooner it is on, the sooner the first Friday works.

### They do not want a recorder at all

Fine. Set the recorder rows to `none` and say plainly how it works instead: they paste a transcript,
or even rough notes from a call they did not record. The four mining questions work on any account of
a real conversation. It is more manual every week, and everything downstream is identical.

**Do not stall setup on any of this.** A missing recorder is a `none` in the config, not a blocker.

## Step 3: Fill in config.md

Work through it **one question at a time**, writing each answer into `config.md` as you go. Do not
ask them to open the file.

**Question 1, recorder.** Already answered in Step 2. Write the three operations in yourself, using
the real tool names you found. Do not make tool names up: if you did not see the tool, write `none`
and note that it needs connecting.

**Question 2, where files go.** Ask: *"Where should your content live? I can make a `content/` folder
here, or use somewhere you already have."* Default to `content/` in the current directory. Create the
subfolders: `ideas/`, `interviews/`, `published/`, `calibration/`.

**Question 3, who they help.** Ask: *"Who do you help, and with what?"* In their words. Write it down
as they say it.

**Question 4, the qualifying threshold.** Ask: *"What tells you someone is a real potential client
rather than just an interested reader? Revenue, team size, stage, something else?"*

Explain why in one line: the drafting step scores every post on whether a real buyer would respond,
and it cannot do that without knowing who counts.

**Question 5, the reader list.** Ask: *"Do you keep a list of clients or contacts anywhere I could
read?"* If no, that is fine: write `none`, and note that the scoring step will ask them to name
someone from memory instead.

**Question 6, open decisions.** Ask: *"Do you keep notes anywhere on decisions you have not made yet,
or things you are sitting on?"* If no, write `none`. The mining skill will ask them live each week
instead.

Leave everything in the Optional section on its defaults unless they raise it.

Then show them the filled config in a short summary, not as a file dump, and ask if anything is
wrong.

## Step 4: Install the templates

Do it yourself:

```bash
cp <pack>/templates/corrections.md  <their-content-path>/corrections.md
mkdir -p .claude/rules
cp <pack>/templates/voice-lint.md   .claude/rules/voice-lint.md
```

Say what each one is, in one line each:

- **corrections.md** starts empty and fills up as they edit drafts. Every edit becomes a rule for
  next week.
- **voice-lint.md** is a pass/fail checklist that runs before they see anything. It starts with a
  handful of universal rules and grows from their own corrections.

## Step 5: Calibrate

Ask: *"Do you have past posts I could learn your writing from? Thirty or more is ideal."*

**If yes:** run `/calibrate-voice`. It handles finding them.

**If their LinkedIn archive has not arrived yet:** go on to Step 6 and come back here when it lands.
Calibrate before drafting in 6c.

**If they are unsure:** run it anyway. It reports what it found and takes the right path.

**If they are brand new to posting:** say so plainly, run it, and let it take the interview path.
Six questions, and it writes their voice files from stated preference rather than measurement. Tell
them it will improve once they have thirty posts up.

**Do not skip this step.** Without it the drafting skill falls back to generic defaults, and generic
defaults are what makes AI content sound like AI content.

## Step 6: Run the first cycle with them, now

**Do not stop at setup and hand them a list of commands.** A person who finishes setup and reads
"run /mine-calls on Friday" will not come back. Take them through one real cycle while they are here.

### 6a. Mine their calls

Run `/mine-calls` immediately. Do not ask permission, just say what you are doing.

- **They had calls this week:** it produces real ideas from their real conversations. This is the
  moment the system becomes obviously worth using. Let it land before explaining anything.
- **They had no calls this week:** widen the window to the last two or three weeks and say why.
- **They have no recorder connected:** ask them to paste one transcript, or even rough notes from any
  recent call. One is enough to demonstrate the whole loop.
- **They have nothing at all:** say so plainly and stop here. Tell them to come back after their next
  recorded call. Do not fabricate material to demo with.

### 6b. Build the interview

Ask them to pick their top three ideas, or recommend three and let them confirm.

Then run `/interview` and give them the questions.

**Now explain the one thing they have to do themselves,** and be direct about it:

> These are the questions the recording could not answer. Answer them out loud into a voice memo or
> a dictation app, then paste the transcript back here. Do not clean it up first.
>
> Speaking rather than typing matters more than it sounds. When you type you edit as you go: you
> compress, you tidy, you drop the aside. Talking gets three or four times more out of you and keeps
> the phrasing that makes the post sound like you. The messy spoken version is the point, and it gets
> kept word for word.
>
> If you would rather type or just talk it through with me here, that works too. It gives the draft
> less to build on, so I will ask more follow-ups.

**This step cannot be automated and should not be.** It is the reason the output is good. Say that
plainly rather than apologizing for it.

Tell them the questions are saved to a file, so they can close the session and come back with their
answers whenever. Give them the file path.

### 6c. When they come back with answers

Map the answers into the interview file verbatim, then run `/draft-posts`.

Walk them through the drafts one at a time, the way the skill specifies. When they change a line,
show them the correction being logged and say in one line what that means: next week it reads this
first and does not make that mistake again.

### 6d. Then hand them the loop

Only now, once they have posts in hand:

```
Friday      /mine-calls     10 min. Ranks post ideas from the week's calls.
Then        /interview      It interviews you. 6-8 questions, 15 min.
Monday      /draft-posts    20 min. Drafts, scores, reviews one at a time.
```

And the one thing worth repeating: **nothing posts automatically.** Every skill stops at a draft they
approve.

Mention once that `/call-mining-update` exists for when they are told there is a new version, and
that it leaves everything of theirs alone. Do not walk through it now.

---

## Edge cases

- **They have not connected any MCP tools and do not know what that means:** do not teach MCP.
  Set the recorder rows to `none`, finish setup, and tell them the system works by pasting
  transcripts until they connect a recorder.
- **They are not in a folder they own** (a temp directory, a downloads folder): say so and ask where
  their work lives. Installing into a folder they will not return to wastes the whole setup.
- **A previous config already exists:** do not overwrite it. Show what is there and ask what they
  want changed.
- **They want to skip config and just try it:** fill in the recorder and the paths, set everything
  else to `none`, and run `/mine-calls`. The mining step needs almost nothing. The scoring step is
  the one that degrades, and they will feel that later rather than now.
- **They ask what happens to their data:** everything the system writes stays in their folder.
  Transcripts and drafts are read by Claude, the same as anything else in a Claude Code session, and
  nothing posts without their approval.

## What not to do

- Do not print shell commands for them to run. Run them.
- Do not present `config.md` as a form. One question at a time.
- Do not invent MCP tool names you have not seen. Write `none`.
- Do not skip calibration because it seems optional. It is the difference between their voice and a
  generic one.
- Do not explain the whole system twice. Step 0 is the overview, Step 6 is the real run.
- Do not end setup with a list of commands and no output. Take them through a real cycle.
- Do not fabricate calls or transcripts to demo with. If there is no material, say so and stop.
