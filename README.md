# chub — Claude Code Plugin

A Claude Code plugin for [Context Hub (chub)](https://github.com/andrewyng/context-hub). Gives Claude access to curated, versioned API docs so it uses current APIs instead of hallucinating from training data.

## Install

Paste into Claude Code:

```
/plugin marketplace add naga-k/chub-claude-plugin
/plugin install chub@chub-claude-plugin
/reload-plugins
```

That's it. No manual CLI setup — the plugin uses `npx` to run chub on demand and refreshes the doc registry on each session start.

## What it does

When Claude needs to write code against an external API (OpenAI, Stripe, Anthropic, etc.), this skill tells it to fetch the current docs from chub first — instead of guessing from training data.

Claude will:
1. Search for the right docs (`npx --yes @aisuite/chub search`)
2. Fetch the current version (`npx --yes @aisuite/chub get <id> --lang py`)
3. Write code using the fetched docs
4. Annotate any gaps it discovers for future sessions
5. Rate the docs so maintainers can improve them

**On each session start**, the plugin refreshes the doc registry so you always have the latest docs.

## How it works

- Uses `npx` to run chub — no global install needed, works in all scopes (user, project, local)
- `SessionStart` hook runs `npx --yes @aisuite/chub update` to refresh the registry
- The skill instructs Claude to use `npx --yes @aisuite/chub` for all commands
- First run downloads and caches chub automatically, subsequent runs use the cache

## Requirements

- Node.js with `npx` available (comes with npm 5.2+)

## License

MIT
