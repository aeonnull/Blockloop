# BLOCKLOOP // setup guide

From zero to your first cost-optimized build loop. This guide assumes nothing. If you have never opened a terminal, you are in the right place.

## Part 1 — What you are about to use

Blockloop does not run in the Claude app where you normally chat. It runs in **Claude Code**, a separate program from Anthropic that can create and edit files on your computer. Think of it this way:

- **The Claude app** (Fable/Opus in the chat): great for brainstorming your idea, writing your design brief, thinking out loud.
- **Claude Code**: the builder. It sits in your project folder and actually writes the files.

Blockloop is a set of instructions you give to Claude Code so it builds smart and cheap instead of burning credits.

Get Claude Code here if you don't have it: https://docs.claude.com/en/docs/claude-code/overview. Follow the install steps for your computer and log in with your Anthropic account. Claude Code also exists as a desktop app if the terminal feels foreign.

## Part 2 — Prepare before you start (the checklist)

Blockloop will interview you before building. You'll get much better results if you have these ready:

- [ ] **Your idea in one or two sentences.** "An endless runner where a pixel character jumps over obstacles, retro style."
- [ ] **Who it's for.** Kids? Your community? Just you?
- [ ] **Where it should live.** A web page? A single HTML file you can share? Your phone?
- [ ] **References.** Screenshots of games or apps with the look and level you're aiming for. Put them in a folder.
- [ ] **A design brief if you have one.** A short document describing style, mood, colors. Not required, but gold if you have it.
- [ ] **Scope.** Roughly how big? Three levels or thirty? Prototype or polished?

No stress if some answers are missing. Blockloop will ask, and "I don't know, suggest something" is a valid answer.

## Part 3 — Install Blockloop (one time, about 5 minutes)

1. Create a folder for your project. Anywhere is fine, for example a folder called `my-runner` on your desktop.
2. Put your reference images and any brief inside that folder, for example in a subfolder called `references`.
3. Unzip the Blockloop package you downloaded.
4. Inside your project folder, create a folder called `.claude` (note the dot). Inside it, create two folders: `skills` and `agents`.
5. Copy the whole `blockloop` folder into `.claude/skills/` so the path becomes `.claude/skills/blockloop/SKILL.md`.
6. Copy the three files from `blockloop/agents/` (light.md, mid.md, heavy.md) into `.claude/agents/`.

When you're done, your project looks like this:

```
my-runner/
├── references/          <- your screenshots and brief
└── .claude/
    ├── skills/
    │   └── blockloop/   <- the whole blockloop folder
    └── agents/
        ├── light.md
        ├── mid.md
        └── heavy.md
```

Tip: if this folder juggling feels fiddly, you can open Claude Code in your project folder and simply ask it: "Install the blockloop skill from this zip file into this project" and it will do steps 4 to 6 for you.

## Part 4 — Your first loop

1. Open Claude Code **in your project folder**. In the terminal that means: navigate to the folder and type `claude`. In the desktop app: open the folder as a project.
2. Write your first message. For example:

> Use blockloop. I want to build an endless runner game. My references are in the references folder.

3. Now Blockloop takes over, and this is what will happen, in order:
   - **It interviews you.** A few questions at a time: goal, audience, platform, scope. Answer in plain language.
   - **It gives you an honest expectation check.** What it can build well on its own, where the gap is compared to your references, and a path across the gap (free options first). You choose the direction.
   - **It sanity-checks the plan.** If something in your idea tends to go wrong (too big a first step, a paid service where a free one works), it flags it and offers alternatives. You decide, your choice stays the default.
   - **It writes the plan.** A file called `BLOCKLOOP.md` appears in your project. You don't create or move this file, Claude Code does it automatically. It shows you the plan before building.
   - **It builds in a loop.** Cheap model for simple tasks, mid model for features, the expensive model only for hard parts or rescues. You can watch the boxes get checked in BLOCKLOOP.md.
   - **It reports.** What got built, which tier did what, where it escalated, and what's left for you (like swapping in real artwork).

## Part 5 — Reading BLOCKLOOP.md

Open the file anytime. Checked boxes are done. The Log section shows every escalation, which is exactly where your credits went and why. That transparency is the point.

## Tips

- The bigger the task, the more Blockloop saves. For a one-line fix, just ask normally.
- If a task landed in the wrong tier, edit BLOCKLOOP.md before the loop reaches it, or just say so.
- Don't delete BLOCKLOOP.md mid-run, it's the loop's memory.
- You can stop anytime and continue in a new session. The file remembers where you were.

## Troubleshooting

- **Claude ignores the skill**: say "use blockloop" explicitly in your first message.
- **It starts building without interviewing you**: say "stop, run the blockloop interview first."
- **A task keeps failing**: the loop stops after the top tier fails twice and reports to you. Read the report, adjust, rerun.
- **Wrong models used**: check that light.md, mid.md and heavy.md are in `.claude/agents/` and each has a `model:` line.

---

Built by Blockheads // blockheadsbtc.xyz
