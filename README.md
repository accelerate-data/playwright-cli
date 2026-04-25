# Playwright CLI

Accelerate Data wrapper plugin for the upstream [Microsoft Playwright CLI](https://github.com/microsoft/playwright-cli) skill.

This repository vendors the useful upstream skill content from `skills/playwright-cli` and adds the plugin manifests required by both Claude Code and Codex.

## Contents

- `.claude-plugin/plugin.json` - Claude Code plugin manifest
- `.codex-plugin/plugin.json` - Codex plugin manifest, categorized as `Coding`
- `skills/playwright-cli/` - vendored upstream Playwright CLI skill and references
- `UPSTREAM-README.md` - snapshot of the upstream README
- `.github/workflows/sync-upstream.yml` - weekly sparse sync from upstream

## Marketplace Source

Marketplace entries should point to this wrapper repository:

```json
{
  "source": "url",
  "url": "https://github.com/accelerate-data/playwright-cli.git"
}
```

Do not point Codex directly at `microsoft/playwright-cli` unless upstream adds `.codex-plugin/plugin.json` at its plugin root.

## Upstream Sync

The sync workflow runs weekly and can also be started manually from GitHub Actions. It sparse-checks out `skills/playwright-cli`, `LICENSE`, and `README.md` from upstream, then opens a pull request with any vendored updates.

## Local Validation

```bash
python3 -m json.tool .claude-plugin/plugin.json
python3 -m json.tool .codex-plugin/plugin.json
```

If Claude Code is installed:

```bash
claude plugin validate .
```
