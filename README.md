# close-gaps

A self-improving loop for Claude Code, packaged as a plugin.

When a working session ends, a **Stop hook** runs the `close-gaps` skill over the
session and asks one question: *what would let the next run do this — and validate it
as the project's real user — without re-deriving it?* Anything durable is captured as a
**project-local skill**, so the project compounds knowledge and tooling over time.

## What it captures

Three kinds of skill, all written to the project's own `.claude/skills/`:

1. **Docs skills** — knowledge as an index of documents (how to use the project's
   libraries, its conventions, the gotchas). The anchor is a self-healing
   `project-overview`. Always *known*, because a skill's description is always loaded.
2. **Validation-tool skills** — a generic CLI that drives the project's real interface
   (UI / command / endpoint / public API) so a result is proven the way its consumer
   sees it — never a build/lint/test proxy.
3. **External-context tool skills** — a generic CLI over an external system (a DB, an
   issue tracker, a third-party API). The one gap that can need *you*: authentication.

## Install

```shell
/plugin marketplace add christianalfoni/close-gaps
/plugin install close-gaps@christianalfoni
```

Then `/clear` (or start a new session). The Stop hook activates automatically — no
`settings.json` edits.

### Try it locally first (no GitHub needed)

```shell
/plugin marketplace add /Users/christianalfoni/Development/close-gaps
/plugin install close-gaps@christianalfoni
```

## How it works

- `plugins/close-gaps/skills/close-gaps/SKILL.md` — the review + the three skill formats.
- `plugins/close-gaps/hooks/hooks.json` — registers the `Stop` hook on enable.
- `plugins/close-gaps/hooks/close-gaps-stop.sh` — fires once per *working* session
  (guarded by `stop_hook_active`; skips pure Q&A via a transcript relevance check).

## Requirements

The Stop hook is a bash script using `jq` and `grep` — works on macOS/Linux. Native
Windows (without WSL/Git Bash) is not yet supported; see [PLAN.md](PLAN.md).

## License

MIT
