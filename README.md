# gym-wiki-template

A template for running your own "gym-wiki" — a training/nutrition journal kept together with an LLM assistant (e.g. [Claude Code](https://claude.com/product/claude-code)), as plain Markdown files readable in [Obsidian](https://obsidian.md/).

Principle: **you dictate your day in a few sentences, the agent normalizes it into the schema and maintains the rest of the wiki** (plans, exercise pages, weekly reviews, insights). Everything stays as plain `.md` files in this repo — no external app.

## What logging actually looks like

You, in chat, after training:

> squats 3x8 at 55kg felt easy, deadlift 3x6 at 90kg last set was grinding, slept 6h, right shoulder pinched a bit on the last set of bench, like a 2/10

The agent writes `raw/journal/2026-08-25.md` in the schema from `AGENT.md` — structured sets/reps/RIR table, pain logged with location/scale/timing, nothing invented for what you didn't say. Sunday, you ask for a `weekly review`; it rebuilds the rolling weight average, flags which lifts are ready to progress, and updates the shoulder's exercise page if 2/10 pain shows up again on the same movement. That's the whole workflow — no app, no manual spreadsheet upkeep, just talking and re-reading Markdown.

## Is this for you?

Honestly, probably not, unless several of these are true: you already use an AI coding agent (Claude Code or similar) for other things, you're comfortable with git, and you'd rather *think out loud in a chat* than tap numbers into an app. If you just want to log a workout in 10 seconds on your phone, [Hevy](https://www.hevyapp.com/) or [LiftLog](https://github.com/LiamMorrow/LiftLog) will serve you better — they're built for that.

What this gets you that an app doesn't: the agent is a curator, not just a logger — it maintains prose pages that explain *why* your plan looks the way it does, catches contradictions between what you decided last month and what you're doing now, and lets you ask free-form questions ("has my shoulder pain ever shown up on machine work vs. free weights?") against months of journal entries instead of scrolling a chart.

## Start

1. **Clone the repo:**
   ```bash
   git clone https://github.com/kamilz12/gym-wiki-template.git your-gym-wiki
   cd your-gym-wiki
   ```
2. **Read [`AGENT.md`](AGENT.md)** — this is the whole schema: folder structure, daily entry format, operations (`entry`, `weekly review`, `plan update`, `question`, `lint`). Adjust it to yourself *before* you start — in particular:
   - the **"Content language"** line near the top — the single place that controls what language everything gets written in (journal entries, wiki pages),
   - the **"Project goal"** section (what you're training for, what your goal is, what time horizon),
   - **"General rules — health"** — add your own injuries/constraints, if you have any,
   - **"General rules — repo"** — decide whether to keep the repo local without a remote (health data), or with a private remote.
3. **Open the repo in Claude Code** (or another agent) and ask for `grilling` to get started:

   > Read `AGENT.md`. Grill me about setting up my gym-wiki — I want to nail down goal, time horizon, health constraints, daily rhythm, and nutrition before we write anything. Based on the answers, update `AGENT.md` (goal section, health/repo rules), write `raw/journal/baseline.md` as the zero point, propose a first draft of `wiki/plan/current-plan.md`, update `index.md`, and add a first entry to `log.md`. Don't guess numbers I didn't give you — leave them blank or ask.

   The `grilling` skill is bundled with this repo in `.claude/skills/grilling` (see the section below) — it works right away, no plugin install needed. The agent will ask questions in rounds (one at a time, with a recommended answer for each) instead of a one-shot survey, and won't start writing anything until things are settled.
4. From there, just **dictate your days** (the `entry` operation) and once a week ask for a **`weekly review`** — the agent builds out `wiki/` pages (plan, exercises, nutrition, insights) and updates `index.md`.
5. Optional: open the folder in Obsidian to read the wiki with `[[...]]` links and the graph view.

## Skill: `grilling`

This repo bundles a project skill at `.claude/skills/grilling` (copied from [mattpocock/skills](https://github.com/mattpocock/skills), MIT — see [NOTICE](.claude/skills/grilling/NOTICE.md)). Works right away after cloning, no plugin install needed.

It grills you question by question (with a recommended answer for each), instead of waiting for you to think of every decision yourself — good for anything with a lot of branches where it's easy to overlook something or cut a corner. Beyond the initial setup (step 3 above), it's also worth reaching for on:

- **restructuring your training/nutrition plan** — when you're changing something structural (a new rotation, new macro targets), not just adding one dish or one exercise,
- any situation where a decision has a lot of branches and it's easy to lose track along the way.

Invocation: just ask the agent directly, e.g. *"grill me about restructuring my nutrition plan"*.

## Structure

```
gym-wiki/
├── AGENT.md    conventions and operations — start here
├── index.md    wiki page index
├── log.md      chronological log of agent operations
├── raw/
│   ├── journal/  daily entries, immutable once written
│   └── assets/   photos, scans
└── wiki/
    ├── plan/         current training plan
    ├── exercises/    one page per exercise
    ├── nutrition/    macro targets, meals
    ├── reviews/      weekly reviews
    └── insights/     durable conclusions from the data
```

## A note on data

This repo holds health data (weight, loads, pain, possibly photos). `AGENT.md` defaults to suggesting you consider keeping the repo without a remote. If you do add a remote (GitHub etc.), **make it private**.
