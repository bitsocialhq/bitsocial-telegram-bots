# Hooks Setup

## Overview

Both `.cursor/` and `.codex/` contain hooks that run automatically during AI-assisted development. They are mirrored — changes to one should be applied to both.

## Hook Configuration

Defined in `.cursor/hooks.json` (and `.codex/hooks.json`):

```json
{
  "version": 1,
  "hooks": {
    "afterFileEdit": [
      { "command": ".cursor/hooks/format.sh", "timeout": 10 },
      { "command": ".cursor/hooks/yarn-install.sh", "timeout": 120 }
    ],
    "stop": [
      { "command": ".cursor/hooks/verify.sh", "timeout": 60 }
    ]
  }
}
```

## Hooks

### format.sh (afterFileEdit)

Auto-formats `.js`, `.ts`, and `.mjs` files using Prettier after AI edits.

### yarn-install.sh (afterFileEdit)

Runs `yarn install` when `package.json` is modified, to keep the lockfile in sync.

### verify.sh (stop)

Runs `yarn build` when the agent session ends, to catch compilation errors.

## Maintenance

When updating hooks:

1. Edit the file in `.cursor/hooks/`
2. Copy the updated file to `.codex/hooks/`
3. If changing `hooks.json`, copy that too
