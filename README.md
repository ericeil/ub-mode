# ub-mode

`ub-mode` is an agent skill that enforces disciplined software engineering principles when writing or changing code. It is loosely based on portions of [@poteto](https://github.com/poteto)'s rules (`poteto-mode` / `pstack`), reduced and paired with deterministic quality-gate tools:

1. **First Make it Work** — Laziness Protocol, Foundational Thinking, TDD, Redesign From First Principles, Attack the Premise, Subtract Before You Add, Outcome-Oriented Execution, Build the Lever, and Architecture (Model the Domain, Boundary Discipline, Type System Discipline, Make Operations Idempotent, Separate Before Serializing Shared State).
2. **Then Make it Right** — Fix Root Causes, Sequence Work into Verifiable Units, Test Behavior (Not Implementation), [Crapper](https://github.com/ericeil/crapper) (`CRAP < 10`), [Dryer](https://github.com/ericeil/dryer) (duplication `< 0.8`), [Mutator](https://github.com/ericeil/mutator) (cover the uncovered, kill the survivors, delete dead code), and Refactoring.
3. **Practice** — Keep a Log, Guard the Context Window, Worktree Cleanup, and Commit and Push in small ordered commits.

## Companion Tool Repositories

`ub-mode` relies on deterministic quality-gate tools to enforce structure, complexity, duplication, and test thoroughness. crapper, dryer, and mutator here are forks of unclebob's tools with Kotlin support:

- [ericeil/crapper](https://github.com/ericeil/crapper) — Computes cyclomatic complexity, test coverage, and CRAP score per function so every function stays under the CRAP threshold (`< 10`).
- [ericeil/dryer](https://github.com/ericeil/dryer) — Detects structural code duplication so duplicate blocks (`>= 0.8` similarity) are eliminated.
- [ericeil/mutator](https://github.com/ericeil/mutator) — Runs mutation testing to expose uncovered code and surviving mutants that tests fail to catch.
- [unclebob/uml-viewer](https://github.com/unclebob/uml-viewer) — Visualizes components, coverage, CRAP, mutation scores, and dependency directions.

## Setup

Before running crapper, dryer, or mutator, check that each is installed and that its checkout's origin is the ericeil fork. If not, install it from that fork. crapper and dryer use `master`. mutator uses `main`. Clone them into one parent directory so mutator sees crapper at `../crapper`.

```bash
git clone https://github.com/ericeil/crapper
git clone https://github.com/ericeil/dryer
git clone https://github.com/ericeil/mutator
```

The first run of `./crapper`, `./dryer`, or `./mutator` creates `.venv` and installs the tool. Mutator needs that crapper checkout for Kotlin function names.

When a project needs extra build flags, pass `--gradle-arg` or `--maven-arg` to crapper and mutator. Repeat the option for each flag.

## Installation

Copy `SKILL.md` into your agent's skills directory as `ub-mode/SKILL.md` (for example `~/.grok/skills/ub-mode/SKILL.md`, `~/.claude/skills/ub-mode/SKILL.md`, or `~/.cursor/skills/ub-mode/SKILL.md`), then invoke `/ub-mode`.
