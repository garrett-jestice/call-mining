# Changelog

The version you are running is in `VERSION` and recorded in `config.md`. When you report a bug,
include it.

Each entry says whether the update needs anything from you after installing. `/call-mining-update`
reads that line and tells you.

---

## 1.1.1

**Requires after update:** nothing. If the Update source in your `config.md` still says `manual` or
shows the old placeholder, you can paste in the repo link from the new `config.md`, so future
updates fetch on their own.

- **Setup time.** The README, SETUP.md and the setup skill said about 15 minutes, which was too low.
  They now say to plan on about an hour.
- **LinkedIn posts.** LinkedIn's analytics export has impressions but stops at 365 days. The full
  data archive holds your posts in `Shares.csv`, without impressions, and LinkedIn says it can take
  up to 24 hours to arrive. Setup now asks LinkedIn posters to request the archive first,
  `/calibrate-voice` steers to it, and SETUP.md has a troubleshooting entry for the one-year wall.
- **Updates come from GitHub.** `config.md` ships with the public repo as the update source.
  `/call-mining-update` downloads it with `curl`, and offers the repo when your source says `manual`.
- `/calibrate-voice` sent a thin sample to the wrong step in its last section. Fixed.

## 1.1.0

**Requires after update:** re-run `/calibrate-voice` to generate `pov.md`. Until you do, ideas are
tagged without a POV, which is the same behavior as 1.0.0.

- **New: POV layer.** Calibration now reads your archive and drafts what you appear to argue, what
  you argue against, and the through-line under posts that look unrelated. You correct the draft. It
  saves to `calibration/pov.md`.
- `/mine-calls` tags every idea `on / adjacent / off / contradicts` against that file. `contradicts`
  is the highest-value tag, not the lowest: changing your mind in public is the strongest post
  available. POV breaks ties in the Top 3 but **never filters**, and moment strength still comes
  first.
- `/draft-posts` handles a `contradicts` draft deliberately: name the position you held, say what
  changed it, put the admission in the hook. It flags the post in review so you decide before it
  goes out.
- `/mine-calls` now calls out a week where every idea came back `on`, which usually means the mining
  got comfortable rather than that the week was.
- Added `VERSION`, this changelog, and `/call-mining-update`.

## 1.0.0

First release.

- `/call-mining-setup` : conversational install, recorder detection and recommendations, config
  filled one question at a time, then it runs your first batch with you.
- `/mine-calls` : mines the week's recordings for 8-12 ideas via four classification questions, plus
  an off-transcript scan for the two formats a recording cannot contain.
- `/interview` : 6-8 load-bearing questions, answered out loud, kept verbatim.
- `/draft-posts` : drafts from your answers, scores against four lenses before you see anything, logs
  every edit you make as a rule for next week.
- `/calibrate-voice` : derives your writing targets from your own posts instead of shipping
  somebody else's benchmarks.
