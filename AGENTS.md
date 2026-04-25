# Playwright CLI

Plugin-source wrapper for vendored Playwright CLI skills used by Claude Code and Codex.

## Repository Purpose

This repository is an Accelerate Data owned plugin wrapper around the upstream Microsoft Playwright CLI skill content. It is not the upstream npm package and must not republish the CLI runtime.

- Upstream source: `https://github.com/microsoft/playwright-cli`
- Vendored content: `skills/playwright-cli/`
- Upstream documentation snapshot: `UPSTREAM-README.md`
- Claude Code manifest: `.claude-plugin/plugin.json`
- Codex manifest: `.codex-plugin/plugin.json`

Marketplace entries should point to this wrapper repository, not directly to `microsoft/playwright-cli`, because the wrapper owns both plugin manifests and cross-agent guidance.

## Instruction Hierarchy

Use this precedence when maintaining agent guidance:

1. `AGENTS.md` - canonical, cross-agent repository guidance
2. Skill-local references under `skills/playwright-cli/references/`
3. Root plugin manifests for product-specific metadata

Do not add a separate Claude adapter unless the Claude runtime requires one for behavior that cannot live in the plugin manifest or `AGENTS.md`.

## Maintenance Rules

- Keep `.claude-plugin/plugin.json` and `.codex-plugin/plugin.json` aligned on name, version, repository, and license.
- Keep the Codex plugin category as `Coding`.
- Preserve the upstream skill directory layout under `skills/playwright-cli/`.
- Do not edit vendored skill content by hand unless the change is intentionally downstream-only and documented in this file.
- Prefer syncing from upstream with `.github/workflows/sync-upstream.yml`.

## Upstream Sync

The scheduled sync workflow runs weekly and can also be run manually. It sparse-checks out only:

- `skills/playwright-cli`
- `LICENSE`
- `README.md`

The workflow replaces `skills/playwright-cli/`, updates the root `LICENSE`, stores upstream `README.md` as `UPSTREAM-README.md`, and opens a pull request when changes are detected.

## Local Validation

After changing plugin metadata, run:

```bash
python3 -m json.tool .claude-plugin/plugin.json
python3 -m json.tool .codex-plugin/plugin.json
```

If Claude Code is available locally, also run:

```bash
claude plugin validate .
```

For Codex, verify the manifest is readable and category metadata stays in `.codex-plugin/plugin.json`.
