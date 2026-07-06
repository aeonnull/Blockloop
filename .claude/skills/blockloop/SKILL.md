---
name: blockloop
description: Cost-optimized, honest build loop. Use this skill whenever the user wants to build a feature, app, game, or prototype, especially if they care about credit/token cost, mention "blockloop", "loop", "burn less credits", or give a large multi-part build task. It interviews the user first, gives an honest expectation check against their references, flags common traps in the plan, then breaks work into tasks routed to the cheapest capable model via subagents (haiku for boilerplate, sonnet for standard logic, opus for architecture and hard debugging), running each task in a verify-fix loop that auto-escalates only when a cheaper model fails twice. Along the way it proactively shares better tools or free alternatives the user did not know to ask about, with a polite opt-out for users who prefer no advice.
---

# BLOCKLOOP // burn less credits

A build workflow by Blockheads. Ask first, be honest about the gap, plan expensive, build cheap, escalate only when needed.

## Why

Most vibe coding burns credits twice: once by letting the strongest model write every line including boilerplate, and once by building the wrong thing because nobody asked the right questions up front. Blockloop fixes both.

## Standing rule: say what you see

This rule applies through the whole workflow, from interview to report. If you notice something the user did not ask about but would want to know, say it right away, not weeks later in hindsight: a better tool, an existing app that does half the job, a free service, a way to skip three steps. Short, once, in passing: "Before we continue, do you know about X? It would save you all of step two. Want to use it, or keep the current plan?"

The bar: unspoken knowledge that would have changed the user's choice is a failure, even if everything built works. Limit it to things that meaningfully change time, cost, or outcome, not matters of taste. Say it once, never nag.

**The opt-out.** The first time you offer unasked-for advice, end with a humble note, roughly: "Tell me if you'd rather build without my input, then I'll stick to the tasks." If the user declines advice, record `advice: off` at the top of BLOCKLOOP.md and respect it for the whole project, across sessions. Two things are never advice and always apply regardless: verifiable done-checks, and safety flags like secrets in code.

## The workflow

### Step 0 — Interview (before anything else)

Never assume. Never start planning from a one-line idea. Ask, in a friendly and compact way, and wait for answers:

1. **Goal**: what should exist when we're done, in one or two sentences?
2. **Audience**: who is it for?
3. **Platform**: web app, mobile, desktop, single HTML file? Where will it live (own domain, itch.io, just local)?
4. **References**: screenshots, links, a Figma, a design brief, anything that shows the level and style you're aiming for. Ask the user to attach them or drop them in the project folder.
5. **Scope**: for a game, roughly how long/hard should it be? For an app, which features are must-have vs nice-to-have?
6. **Done**: what does finished mean to you for this round?

If the user has a brief or documents, read them before asking, and only ask about the gaps. Two to four questions per message, never a wall of questions.

### Step 0.5 — Expectation check (honesty before enthusiasm)

Compare the user's references and ambitions with what you can realistically deliver. Then say it plainly, in three parts, before any plan is written:

1. **What I'll do well on my own**: the mechanics, logic, structure, functional UI.
2. **Where the gap is**: name the parts that will not match their references if fully generated, typically polished art, sound design, brand-level visual finish.
3. **The path across the gap**: concrete suggestions, free options first. Examples: art from an image tool or a commissioned artist, sound from free libraries, fonts from free sources, and I build everything so those assets are easy to swap in later.

Then let the user choose: aim for the reference level via that path, or lower the visual ambition and have everything generated. Enthusiasm is allowed, but never before the gap has been named. No "I can absolutely build that!" until the honest picture is on the table.

### Step 1 — Sanity check (the trap list)

Review the user's idea and any workflow or services they proposed against the common traps below. Flag at most the two or three most important ones. Format, always: name the issue, one line on why it matters, offer an alternative, let the user decide. The user's original choice stays the default. Never silently swap their choice for yours.

The traps:

1. **Too big a first step**: the whole app at once instead of a playable/clickable core first. Always propose a smallest working version as the first milestone.
2. **Paid where free works**: a paid service, API, or connector where a free or built-in option covers the need. Say so: "That works, but X is free and enough for this."
3. **Wrong tool for the job**: a database where a file is enough, a login system for a prototype nobody logs into.
4. **No verifiable done**: "nice" and "good" can't be checked. Every task gets a concrete done-check.
5. **Secrets in code**: API keys pasted into source instead of environment variables.
6. **Nothing to roll back to**: hours of building without git. Initialize a repo before the loop starts.

### Step 2 — Plan

Write the task list to `BLOCKLOOP.md` at the project root using `templates/tasklist.md`. Each task gets:

- a short name
- a **tier**: `LIGHT`, `MID`, or `HEAVY`
- a **done-check**: one concrete, verifiable criterion (a command that must exit 0, a test that must pass, a file that must exist and render). Never "looks good".

Tier guide:

| Tier | Model | Typical tasks |
|---|---|---|
| LIGHT | haiku | boilerplate, CSS, config files, README, simple CRUD, copy changes, renames |
| MID | sonnet | standard features, API endpoints, UI components, straightforward game logic, tests |
| HEAVY | opus | architecture decisions, tricky algorithms, physics/collision, gnarly debugging, security-sensitive code |

When unsure between two tiers, pick the cheaper one. Escalation catches mistakes. Show the plan to the user before starting the loop.

### Step 3 — Build (the loop)

Work through `BLOCKLOOP.md` top to bottom. For each unchecked task:

1. Delegate to the subagent matching its tier (`agents/light.md`, `agents/mid.md`, `agents/heavy.md`).
2. The subagent implements, then runs the done-check.
3. **Pass** → check the box, note which tier completed it, move on.
4. **Fail** → the same tier gets one retry with the error output.
5. **Fail twice** → escalate one tier up (LIGHT→MID→HEAVY) and log it under the task: `escalated: LIGHT→MID (2 fails: <one-line reason>)`.
6. If HEAVY fails twice, stop and report to the user with the error and what was tried. Never loop forever.

Rules during the loop:

- One task at a time. No batching.
- A subagent only touches its own task, with minimal context: the task, its done-check, only the files it needs.
- Never weaken a done-check to make a task pass. If a done-check is wrong, flag it to the user.

### Step 4 — Report

When all boxes are checked (or a hard stop was hit), summarize:

- tasks completed per tier
- escalations and why
- rough cost picture: how much of the work stayed on LIGHT/MID
- what remains for the user (e.g. swapping in real art/sound per the expectation check)

### Step 5 — One notch up (unless advice is off)

After the report, and only if the user has not opted out of advice, offer at most one or two suggestions for taking the result one notch higher. Tone matters here: genuine appreciation of what they built first, then the suggestion with a rough cost or a free path, then let it go. Roughly: "This is genuinely solid. If you ever want to take it one notch up, X would do it, costs about a dollar, or Y is the free route. Totally up to you, it stands well as it is."

Never a list of ten "improvements" that makes finished work feel unfinished. One or two, offered like a friend would, then done.

## Files in this skill

- `agents/light.md`, `agents/mid.md`, `agents/heavy.md` — subagent definitions with model per tier. Install into the project's `.claude/agents/` directory (see GUIDE.md).
- `templates/tasklist.md` — the BLOCKLOOP.md template.
- `GUIDE.md` — beginner setup guide, from zero to first loop, no prior terminal experience assumed.

## Notes

- Model names in the agent files use aliases (haiku/sonnet/opus) so they track the latest versions automatically.
- If the environment has no subagents, run the same tiering manually: state the tier per task and keep the retry-then-escalate discipline.
