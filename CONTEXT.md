# CONTEXT.md

The vocabulary of **test-4** — what the words mean here, so every ticket, plan,
commit and review uses the same word for the same thing.

Companion file: [AGENTS.md](./AGENTS.md) — how to work in this repository
(stack, commands, conventions). This file is about *nouns*; that one is about
*rules*.

## What test-4 is

A project created with [Fredrin](https://fredrin.com) and currently a bare
scaffold: version-controlled, wired into a board, and carrying no application
code yet. It exists so that work can be described, parallelized and merged from
day one, before there is anything to run.

Because the domain is not yet chosen, this document defines the **process
vocabulary** — the words the board and the workflow force everyone to share. As
soon as the project acquires a subject, add a **Domain vocabulary** section
below and define its entities there.

## Process vocabulary

These come from Fredrin and are binding regardless of what the project turns
into.

**Project** — this repository plus its board. One project, one checkout,
one `main`. Slug: `test-4`.

**Board** — the kanban of every ticket in the project. Tickets move
left-to-right through columns, driven by deterministic signals rather than by
anyone remembering to move a card.

**Ticket** — one unit of work, sized to be finished by a single agent session
in a single branch. A ticket carries a title, a description (the problem and
its acceptance criteria), and a plan (how it will be done). If work cannot be
finished in one session, it is more than one ticket.

**Plan** — the ticket's implementation plan, written before building. Its
`## Action items` checklist is live: items are checked off as they are
completed, so the board shows real progress rather than a status guess.

**Acceptance criteria** — the observable conditions that make a ticket done,
written in the description as things that can be checked, not as intentions.

**Worker** — the AI agent session that builds one ticket. One ticket, one
Worker. Throughput comes from running many Workers at once, which is why
isolation between them matters more than it would in a single-developer repo.

**Worktree** — the isolated checkout a Worker builds in, created when the
ticket starts and removed when its work lands. Several exist simultaneously,
all sharing one git object store — which is why the stash stack is shared and
must not be used casually.

**Branch** — the per-ticket line of work inside its worktree. It is local; it
is never pushed anywhere, because this project has no remote.

**Review** — reading the ticket's local diff against `main`. There is no pull
request to open and no CI service to wait on; a human reads the change.

**Ship / merge** — landing a reviewed ticket onto `main` as a local
squash-merge. One ticket becomes one commit on `main`.

**Blocked** — a ticket that cannot proceed without a decision or another
ticket. Blocked is a real state to move to, not a reason to guess and continue.

**Artifact** — a file attached to a ticket (a screenshot, a recording, a
document, a log). Content deliverables that are not code live here, on the
ticket, rather than as loose files in a worktree.

**Project context** — the committed documents every Worker is seeded from:
this file and `AGENTS.md`. They are the shared memory of the project; when a
change makes them wrong, the change is not finished until they are fixed.

## Domain vocabulary

_Nothing yet — the project has no subject matter._

When test-4 acquires one, define its entities here: one term per bolded entry,
one or two sentences each, stating what the thing **is** and what distinguishes
it from the term nearest to it. Prefer defining the word that is already being
used in conversation over inventing a tidier one, and record the words this
project deliberately does **not** use, with the word it uses instead — most
confusion in a parallel board comes from two names for one thing.
