# AGENTS.md

Conventions for AI coding agents working in **test-4**. This file is the
canonical entry point under the [AGENTS.md](https://agents.md) standard, and it
is the first thing a Fredrin Worker reads.

Companion file: [CONTEXT.md](./CONTEXT.md) — the shared vocabulary. Read it
before writing a ticket description, a plan, or a commit message, so everyone
names the same thing the same way.

## Project

**test-4** is a project created with [Fredrin](https://fredrin.com), the desktop
kanban that runs many AI-coding tickets in parallel. It runs on **local git**:
there is no remote, so review is a local diff and shipping is a local
squash-merge onto `main`.

The repository is currently a **bare scaffold**. As of this file's writing the
only tracked files are `.gitignore`, `README.md`, `AGENTS.md` and `CONTEXT.md` —
there is no application code, no package manifest, and no toolchain yet. What
this project *becomes* is decided by the tickets that follow; the first ticket
that introduces a stack owns updating the **Commands** section below.

## Commands

There are none yet. No `package.json`, `Makefile`, `pyproject.toml`,
`Cargo.toml`, or equivalent is checked in, so there is nothing to install, run,
test or build.

Do not invent commands to fill this section, and do not run a build or test
command "just in case" — it will fail because no toolchain exists, not because
something is broken. Fill the table in as the tooling actually lands:

| Purpose | Command |
| --- | --- |
| Install | _not established yet_ |
| Run (dev) | _not established yet_ |
| Test | _not established yet_ |
| Build | _not established yet_ |
| Lint / typecheck | _not established yet_ |

**Rule:** the ticket that introduces a runtime or a package manager must add its
real commands here in the same change. A command that is not in this table is
not a command a Worker is expected to know.

## Conventions

Things a new contributor — human or agent — would otherwise get wrong on the
first try.

### Git and shipping

- **No remote.** `git push` has nowhere to go. Work is reviewed as a local diff
  against `main` and lands as a local squash-merge. Don't add a remote, and
  don't reach for `gh` — there is no GitHub repository behind this project.
- **One ticket, one branch, one worktree.** Fredrin creates the worktree when a
  ticket starts and tears it down when the ticket's work merges. Run every
  command from the worktree root; never `cd` into the main checkout.
- **Never `git stash` bare.** The stash stack is shared across every worktree
  and other Workers may be running concurrently. Set work aside with a
  temporary WIP commit instead. If you must stash, use
  `git stash push -u -m "<unique-tag>"` and restore with `git stash apply <sha>`.
- **Commits are conventional**: `type: imperative subject` (`feat:`, `fix:`,
  `docs:`, `chore:`, `refactor:`), subject ≤ 72 chars, body explaining *why*.
  Changes to project context documents go in their own commit prefixed
  `context:`.

### Files and layout

- `.fredrin/` is **git-ignored on purpose**. It holds machine-local tool state
  and the per-worktree `fredrin` CLI wrapper, which carries a scoped API
  credential — never commit it, never print its contents, never paste it into a
  ticket, log or comment.
- `.env` and `.env.*` are ignored; `.env.example` is not. Every environment
  variable the project starts depending on must appear in `.env.example` with a
  placeholder value and a one-line comment, in the same change that introduces
  it.
- Keep the repository root shallow. `AGENTS.md`, `CONTEXT.md` and `README.md`
  are root documents; anything else new belongs in a directory with a purpose.

### Documentation

- `AGENTS.md` describes **how to work here** — stack, commands, conventions.
  `CONTEXT.md` describes **what is being built** — the nouns and their meanings.
  When a change makes either stale, update it in the same change; a stale
  convention is worse than a missing one, because it gets followed.
- Improve these files **in place**. Don't replace a document wholesale to make a
  small correction — later tickets are seeded from them, and rewrites destroy
  decisions nobody wrote down twice.
- Write down decisions, not narration. "Dates are stored as UTC ISO-8601
  strings" is worth a line forever; "refactored the date helper" is not.

### Working style

- Prefer the smallest change that fully satisfies the ticket. Scope creep across
  parallel worktrees is what produces merge conflicts here.
- Don't add a dependency, a framework or a build step without saying so in the
  ticket. In a scaffold this early, the first choice of each becomes the
  project's default by accident.
