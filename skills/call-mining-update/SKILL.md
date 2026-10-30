---
name: call-mining-update
description: Update the Call Mining system to a newer version without touching the user's own config, calibration files, corrections log, or any customizations they made. Fetches the latest pack from the update source in config.md or from a zip the user points at, shows what changed, protects local edits, and reinstalls the skills. Use when the user says /call-mining-update, "update Call Mining", "is there a new version", "I got sent a new version", or when they report a bug that a newer version already fixes.
---

# Call Mining Update

Replace the stock parts of the system. **Never touch the parts that are theirs.**

Getting this wrong destroys work that cannot be regenerated, so the whole skill is built around one
rule: **when in doubt, do not overwrite. Ask.**

---

## What is theirs, and never gets replaced

| Never overwrite | Why |
|---|---|
| `config.md` | Their settings, filled in by hand |
| Their `calibration/` folder | Derived from their posts. `pov.md` may have hand edits. |
| Their corrections log | Weeks of accumulated rules. Not regenerable. |
| Their installed `voice-lint.md` (in `.claude/rules/`) | Started as a template, has grown their promoted rules |
| Their `ideas/`, `interviews/`, `published/` folders | Their work |
| Any skill they modified | See Step 4 |

**The templates inside the pack are not the same files as their installed copies.**
`templates/corrections.md` in the pack is a blank starter. Their live corrections log is at the path
in `config.md` and holds real content. Updating the first must never touch the second. This is the
single easiest way to do real damage here, so check the paths before any copy.

## What is stock, and gets replaced

`skills/`, `reference/`, `README.md`, `SETUP.md`, `CHANGELOG.md`, `VERSION`, and the files in
`templates/`.

---

## Step 1: Find out what they are running

Read `VERSION` and the Updates section of `config.md`.

If neither has a version, they are on 1.0.0 or earlier. Say so and continue.

## Step 2: Get the new pack

Check the update source in `config.md`.

- **A URL:** fetch it. Use whatever is available: a web fetch tool, or `curl -L` through the shell.
- **`manual`, or blank:** ask whether they have been sent a new zip. If yes, get the path. If no, say
  there is nothing to update from and stop. Do not invent a source.
- **The fetch fails:** say what failed and fall back to asking for a zip. Do not retry silently.

Unpack it to a scratch location. **Do not unpack over their existing pack.**

## Step 3: Compare

Read the new `VERSION` and `CHANGELOG.md`.

- **Same version:** say they are current and stop. Do not reinstall for no reason.
- **Theirs is newer:** something is wrong. Say so and stop rather than downgrading.
- **Newer available:** show them the changelog entries between their version and the new one, in
  plain language. Then ask whether to install.

**Note any `Requires after update` line** in those entries. That is the thing they have to do
afterward, and it is the part people miss.

## Step 4: Protect their customizations

**Before copying anything**, compare each installed skill in `.claude/skills/` against the same file
in their current pack.

Any file that differs has been modified by them or by an earlier partial update.

For each one:

1. Say which file, and summarize what their version does differently
2. Ask: keep theirs, take the new one, or merge

**Default to keeping theirs when they do not answer clearly.** Somebody who adapted a skill (a second
input source, a changed question set, their own scoring lens) has done real work, and the new version
almost certainly does not include it.

If they want a merge, do it properly: apply their change on top of the new file rather than pasting
the new file over their edit. Show them the result before writing it.

## Step 5: Install

1. **Back up their current pack** to a sibling folder with the old version in the name, for example
   `call-mining-1.0.0-backup/`. Cheap, and it is what makes an unwind possible.
2. Replace the stock files listed above.
3. Leave `config.md` exactly as it is. **Do not merge, reformat, or reorder it.**
4. If the new version added a config field, add just that field with a blank value, and tell them what
   it is for. Do not touch anything else in the file.
5. Re-copy `skills/` into `.claude/skills/`, honoring every decision from Step 4.
6. Write the new version into `VERSION` and into the Updates section of `config.md`.

## Step 6: Report

Say, in this order:

1. What version they are on now
2. What actually changed, in a sentence or two, not the raw changelog
3. **Anything they need to do**, from the `Requires after update` lines. Offer to do it now.
4. Which of their files were left alone, so they can see nothing was lost
5. Where the backup is

Then stop. Do not run a mining pass unless they ask.

---

## Edge cases

- **They never ran setup:** this is an install, not an update. Point them at `/call-mining-setup`.
- **Their pack folder has moved or is missing:** ask where it lives. Do not guess and do not install a
  second copy alongside the first.
- **They installed skills globally** (`~/.claude/skills/`) rather than per project: update there
  instead. Check both if you are unsure, and say which one you changed.
- **The update needs a re-calibration** and they decline: fine. Say what stays inactive until they run
  it, and leave it. A missing `calibration/pov.md` degrades cleanly.
- **They are mid-cycle** with an unanswered interview or undrafted ideas: those files are theirs and
  are not touched. Say that explicitly, because it is the first thing someone worries about.
- **Something goes wrong partway:** stop, say exactly what was copied and what was not, and point at
  the backup. Do not attempt a clever repair.

## What not to do

- Do not overwrite `config.md`, their calibration folder, their corrections log, or their installed
  voice-lint. Ever.
- Do not confuse the pack's `templates/` with their live installed copies.
- Do not overwrite a modified skill without asking.
- Do not skip the backup.
- Do not reformat or "tidy" their config while adding a field.
- Do not report an update as clean if any step failed.
