# chub — Claude Code Plugin

A Claude Code plugin for [Context Hub (chub)](https://github.com/andrewyng/context-hub). Gives Claude access to curated, versioned API docs so it uses current APIs instead of hallucinating from training data.

## Install

Paste these into Claude Code:

```
/plugin marketplace add naga-k/chub-claude-plugin
/plugin install chub@chub-claude-plugin
/reload-plugins
```

The plugin automatically installs and updates the chub CLI and doc registry on each session start — no manual setup needed.

### Manual (without marketplace)

```bash
mkdir -p ~/.claude/skills/get-api-docs
curl -o ~/.claude/skills/get-api-docs/SKILL.md https://raw.githubusercontent.com/naga-k/chub-claude-plugin/main/skills/get-api-docs/SKILL.md
```

Note: manual install doesn't include auto-install/update hooks. You'll need to install chub yourself: `npm install -g @aisuite/chub`

## What it does

When Claude needs to write code against an external API (OpenAI, Stripe, Anthropic, etc.), this skill tells it to fetch the current docs from chub first — instead of guessing from training data.

Claude will:
1. Search for the right docs (`chub search`)
2. Fetch the current version (`chub get <id> --lang py`)
3. Write code using the fetched docs
4. Annotate any gaps it discovers for future sessions
5. Rate the docs so maintainers can improve them

**On each session start**, the plugin:
- Installs or upgrades the chub CLI to the latest version
- Refreshes the doc registry (`chub update`) so you always have the latest docs

## License

MIT
