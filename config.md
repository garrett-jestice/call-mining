# Call Mining Config

**This is the only file you edit.** All four skills read it before they do anything. Fill in the
brackets and you are done.

If a line says `none`, the skill that depends on it degrades gracefully instead of failing. Nothing
here is required to get a first run out.

---

## 1. Recording source

Where your call transcripts live. The skills never call a recorder directly: they call the three
operations you declare here, so any recorder works.

| Setting | Your value |
|---|---|
| Recorder | `[Grain / Fathom / Fireflies / Otter / Gong / Granola / Zoom / local folder]` |
| List meetings in a date range | `[MCP tool name, or "read files in <path>"]` |
| Fetch one transcript | `[MCP tool name, or "read the file"]` |
| Fetch notes (fallback when a transcript is missing) | `[MCP tool name, or "none"]` |
| Minimum call length to bother with | `5 minutes` |

**Filled-in examples.** Copy the row that matches your setup.

```
Grain      list_attended_meetings  /  fetch_meeting_transcript  /  fetch_meeting_notes
Fathom     list_meetings           /  get_meeting_transcript    /  get_meeting_summary
Fireflies  (via its MCP)           /  (via its MCP)             /  none
Local      read files in ~/transcripts/  /  read the file       /  none
```

If you have no recorder at all, set every row to `none`. `/mine-calls` will ask you to paste
transcripts instead, and everything downstream works the same.

---

## 2. Where files get saved

The four skills hand off by writing files each other reads. That is what lets you mine on Friday,
answer questions on Saturday, and draft on Monday without holding it all in one session.

| What | Path |
|---|---|
| Post ideas | `[<your-content-path>/ideas/]` |
| Interview docs | `[<your-content-path>/interviews/]` |
| Approved posts | `[<your-content-path>/published/]` |
| Corrections log | `[<your-content-path>/corrections.md]` |
| Calibration output | `[<your-content-path>/calibration/]` |

A reasonable default if you have no preference: `content/ideas/`, `content/interviews/`, and so on
under whatever folder you run Claude Code in.

---

## 3. Who you are

`/draft-posts` cannot score a draft on whether a real buyer would respond to it unless it knows who
your buyer is. This section is what makes the Buyer lens work.

| Setting | Your value |
|---|---|
| I help | `[who you serve, in your own words]` |
| The threshold that qualifies a real buyer | `[revenue, headcount, stage, whatever actually qualifies]` |
| A second, occasional audience | `[or "none"]` |
| List of real readers | `[path to a client or contact list, or "none"]` |

**On the reader list.** The Buyer lens asks you to name a specific real person who would leave the
comment your post is engineered to earn. If you point at a file of real clients and contacts, the
skill picks from it. If you say `none`, it asks you to name someone from memory. Do not skip this by
letting it invent a persona: an invented reader always approves of your draft.

---

## 4. Open decisions log

Powers the off-transcript scan in `/mine-calls` Step 5. Two of the strongest post formats never
appear in a call transcript, so they have to be hunted somewhere else.

| Setting | Your value |
|---|---|
| Where you log decisions and open questions | `[path, or "none"]` |
| Where you log tasks you are sitting on | `[path, or "none"]` |

If both are `none`, `/mine-calls` asks you two questions live instead. That works fine. It is just
slower every week than reading a file.

---

## 4b. Updates

| Setting | Your value |
|---|---|
| Version installed | `[filled in at setup]` |
| Update source | `https://github.com/garrett-jestice/call-mining/archive/refs/heads/main.zip` |

That link is the public repo, so `/call-mining-update` can fetch a new version on its own. Change it
to `manual` if you would rather install updates from a zip yourself. Include the version when you
report a bug.

---

## 5. Optional

| Setting | Your value | Notes |
|---|---|---|
| Platform | `LinkedIn` | The mechanics assume LinkedIn. Most carry to other feeds. |
| Newsletter branch | `off` | Set to `on` if you also write a short newsletter and want `/mine-calls` to flag issue candidates. |
| Week starts | `Monday` | The default mining window is this day through now. |

---

## 6. Your voice files

Written by `/calibrate-voice`, not by you. Listed here so the other skills know where to look. Leave
them alone until you have run calibration once.

One exception worth knowing: `pov.md` is the one file worth editing by hand later. Calibration drafts
it from your posts and you correct it, but what you argue changes faster than how you write, so open
it when your thinking moves.

| File | Holds |
|---|---|
| `<calibration path>/pov.md` | What you argue, what you argue against, and the through-line |
| `<calibration path>/voice.md` | Your register, what you sound like, what you never do |
| `<calibration path>/patterns.md` | Your measured rhythm, length, format mix, and openers |
| `<calibration path>/terms.md` | The words and concepts you repeat on purpose |

**Status:** `not yet calibrated`

Change that line to `calibrated [date], n=[number of posts]` when `/calibrate-voice` finishes. The
drafting skill checks it, and falls back to universal defaults if it still says not yet calibrated.
