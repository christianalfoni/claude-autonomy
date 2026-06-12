# PLAN — close-gaps plugin + marketplace + site

Handoff for a fresh session rooted in this folder (`~/Development/close-gaps`).

## What's already scaffolded
- Plugin: `plugins/close-gaps/` — `plugin.json`, `skills/close-gaps/SKILL.md` (copied
  from the working global skill), `hooks/hooks.json` + `hooks/close-gaps-stop.sh`.
- Marketplace: `.claude-plugin/marketplace.json` (name `close-gaps`, plugin source `./plugins/close-gaps`).
- Site: `docs/index.html` (static, GitHub Pages-ready landing page).
- README.md. `git init` done; **nothing committed yet**.

> Note: the skill + hook were **copied**, not moved. The active global copies in
> `~/.claude/` keep running until the plugin is installed and verified, so there's no
> gap. Dedup (remove the global copies) only after the plugin path is proven.

## Do next

### 1. Verify the plugin locally (before any GitHub)
```
/plugin marketplace add /Users/christianalfoni/Development/close-gaps
/plugin install close-gaps@close-gaps
/clear
```
- Confirm the skill loads (namespaced as `close-gaps:close-gaps`).
- Do a tiny real edit in a throwaway project → confirm the Stop hook fires the review.
- Run `claude plugin validate ./plugins/close-gaps` (and the marketplace) — fix anything.

### 2. Open questions to resolve while testing
- **`${CLAUDE_PLUGIN_ROOT}`** in `hooks/hooks.json` — confirm it resolves to the cached
  plugin dir so the script path works. (High confidence, but validate by actually firing it.)
- **Namespacing vs the hook text** — the hook's reason says "invoke the `close-gaps`
  skill", but installed it's `close-gaps:close-gaps`. Verify the model still loads it; if
  flaky, either rename so the bare name survives, or inline the review steps into the hook reason.
- **Marketplace/plugin both named `close-gaps`** → install reads `close-gaps@close-gaps`.
  Decide on branding (rename the marketplace to a personal handle if preferred).

### 3. Publish
- Create GitHub repo `christianalfoni/close-gaps`, push `main`.
- Enable **GitHub Pages**: Settings → Pages → Deploy from branch → `main` / `/docs`.
  Site lands at `https://christianalfoni.github.io/close-gaps/`.
- Real install path becomes: `/plugin marketplace add christianalfoni/close-gaps`.

### 4. Hardening / reach (later)
- **Windows portability**: rewrite `close-gaps-stop.sh` in Node (no `jq`/`grep`) so it
  runs cross-platform. User already has Node; the relevance-gate grep → JSON parse.
- **Tunable behavior**: document/allow disabling the relevance gate or adjusting the
  iteration the hook expects.
- **Community marketplace**: `claude plugin validate`, then submit to `claude-community`
  via the Console/claude.ai form for public discovery.
- **Site polish**: real copy, an example of a generated skill, maybe a short asciinema.

## Decisions still open
- Audience: personal / team / public? (only changes README + repo visibility + branding)
- Marketplace name / handle.
- Keep site in this repo (`/docs`) vs a separate repo / custom domain.
