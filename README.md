# clay-ralph

Design autonomous coding loop prompts for [Clay](https://github.com/chadbyte/claude-relay)'s Ralph Loop.

Ralph Loop runs your coding tasks autonomously — you describe what to build, this skill crafts the perfect prompt and judge criteria, then Clay executes iteratively until the job is done.

## Prerequisites

- [Clay](https://github.com/chadbyte/claude-relay) must be installed and running. Ralph Loop is a Clay feature — this skill is used by Clay to craft loop prompts.

## Install

```bash
npx skills add chadbyte/clay-ralph
```

## What it does

When you invoke `/clay-ralph`, the skill:

1. **Explores your codebase** — understands the tech stack, patterns, and conventions
2. **Interviews you** — asks targeted questions to nail down exactly what you want
3. **Writes `PROMPT.md`** — a self-contained task description that a fresh Claude session can execute cold
4. **Writes `JUDGE.md`** — clear, diff-verifiable criteria for automated pass/fail evaluation

Then Clay's Ralph Loop engine takes over: running iterations, judging results, and looping until the judge says PASS.

## How Ralph Loop works

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  PROMPT.md  │────▶│   Claude    │────▶│  git commit  │
│  (the task) │     │  (execute)  │     │  (changes)   │
└─────────────┘     └─────────────┘     └──────┬───────┘
                                               │
                    ┌─────────────┐             │
                    │   Judge     │◀────────────┘
                    │  JUDGE.md   │
                    │  + git diff │
                    └──────┬──────┘
                           │
                    PASS? ──┴── FAIL?
                      │           │
                    Done!     Next iteration
```

- Each iteration runs in a **fresh session** — no memory of previous runs
- The only continuity is the **file system** (git commits)
- The judge evaluates from **code changes only**, not conversation output
- Interactive tools are blocked — fully autonomous execution

## Usage

```
/clay-ralph
```

That's it. The skill will guide you from there.

## License

MIT
