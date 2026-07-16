# The Ground Truth Protocol

One file and three pillars that stop your AI agent from confidently building the wrong thing.

**The idea in one line:** at every step, the agent works from what's actually true in your live systems — not from what a document claims, and not from what the model confidently assumes.

Full write-up: [The Ground Truth Protocol on [LinkedIn]([url](https://www.linkedin.com/pulse/ground-truth-protocol-one-file-three-pillars-stopped-my-patrick-o-dabyc/)

## What's in this repo

One file: [`agent_instructions.md`](agent_instructions.md) — the bootstrap. It's the same for every project and holds zero project content. Pointed at a project folder, it interviews you and builds the rest of the system for you:

- **`orientation.md`** — a living map of one project: every layer, exactly how to reach it, current state, and a one-line index of every session.
- **`Handoff_<date>.md`** — a frozen record of each session: what shipped, what's blocked, what not to relearn. The stack grows forever; nothing gets rewritten.

## Install (about 2 minutes)

1. You need an agent that can read/write files on your machine and reach your tools — [Cowork](https://claude.com/cowork), [Claude Code](https://claude.com/claude-code), or any file-capable harness. A plain chat window won't work (the article explains why).
2. Save `agent_instructions.md` somewhere permanent — or just paste the raw file URL to your agent and say: *"Fetch this and save it as `agent_instructions.md` in my projects folder."*
3. Pick one root folder where your projects will live, and swap in your path wherever the file says `<PROJECTS_ROOT>`.
4. Start a session: *"Read `agent_instructions.md` and set up a new project called `<name>`."* Answer the intake questions. Done.
5. Every session after that: *"Read `agent_instructions.md` and the `<name>` project folder, then follow it."*

## If you use it

Tell me what breaks — [open an issue](../../issues). That's usually where the next version comes from.
