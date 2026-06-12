# Make Claude autonomous on your repo

A small, growing set of open, **self-contained setup prompts** for
[Claude Code](https://claude.com/claude-code) that make it work without you in the loop.

Paste one into a Claude Code session opened in your repo and it builds the capability into
your repo as files **you own and edit** — no plugin, no install, no marketplace, and no
runtime dependency on this repo. Each prompt carries everything Claude needs.

**→ [christianalfoni.github.io/claude-plugins](https://christianalfoni.github.io/claude-plugins) — copy a prompt.**

## The prompts

### close-gaps — Claude that improves itself

When a working session ends, a **Stop hook** reviews the work and captures what would make
the next run faster — as project-local skills committed to your repo. The prompt writes the
review skill and the Stop hook into your `.claude/`, then hands them to you. Three kinds of
skill it captures:

- **Docs** — how to use the project's libraries and conventions, indexed as a table of
  contents, anchored by a self-healing `project-overview`.
- **Validation tools** — a generic CLI that drives the real interface (UI, command,
  endpoint, API) so a result is proven the way its user sees it. Never a proxy.
- **External context** — a generic CLI over an external system (a DB, an issue tracker, an
  API). The one gap that may need you: authentication.

### /claude agent — Claude that works without you

Comment `/claude …` on a GitHub issue or PR and a Claude session in Anthropic's cloud does
the work and reports back — your laptop off, on your Max subscription. The prompt creates a
small **dispatcher GitHub Action** (detect, gate, fire) and walks you through configuring a
**Claude Code routine** that clones the repo, implements the change, and opens or updates a
PR. The dispatcher does zero Claude work; all behaviour lives in the routine.

## How to use

1. Open Claude Code in the repo you want to enhance.
2. Copy a prompt from the [site](https://christianalfoni.github.io/claude-plugins) (Edit it
   first if you want to tweak it).
3. Paste it as your first message and follow along. Each prompt creates files you own, so
   you can tune the behaviour afterwards.

## Requirements

- **close-gaps** — the Stop hook is bash using `jq` and `grep`: macOS/Linux, or Windows via
  WSL/Git Bash.
- **/claude agent** — a claude.ai Pro/Max/Team/Enterprise plan with Claude Code on the web
  (routines) enabled, a GitHub repo, and the ability to add repo secrets. Routines and the
  routine-fire API are a research preview.

## How it's built

The prompts live inline in [`docs/index.html`](docs/index.html) — that page is both the
site and the single source for the prompt text. The Copy/Edit buttons read them with no
network fetch, and the prompts themselves install nothing *from* this repo. There is
nothing to install to use these; you copy a prompt and run it in your own repo.

## License

MIT
