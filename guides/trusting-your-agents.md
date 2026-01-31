# Trusting Your Agents

## The Challenge

When Claude Code runs autonomously, how do you know it's doing things correctly? You can't watch every step.

## The Solution: Validation Hooks

Hooks are automatic checks that run during agent execution. They ensure quality without manual oversight.

```
Agent does work
      ↓
Hook automatically validates
      ↓
Issues caught immediately
      ↓
Agent fixes problems
      ↓
You get quality output
```

## Why This Matters

With validation hooks in place:

| Without Hooks | With Hooks |
|---------------|------------|
| Manual review required | Automatic validation |
| Issues found late | Issues caught immediately |
| Inconsistent quality | Consistent standards |
| More babysitting | Less terminal time |

## Hooks in Different Places

### Global Hooks (All Projects)
```
~/.claude/settings.json → hooks section
```

### Project Hooks (This Project)
```
.claude/settings.json → hooks section
```

### Frontmatter Hooks (Single Command/Agent)
```yaml
---
hooks:
  post_tool_use:
    - matcher: Bash
      command: python ./validator.py
---
```

## The Trust Pyramid

```
        /\
       /  \      Frontmatter hooks
      /    \     (specific validation)
     /------\
    /        \   Project hooks
   /          \  (project standards)
  /------------\
 /              \ Global hooks
/                \(universal protection)
------------------
```

## What to Validate

| Area | Hook Type | Example |
|------|-----------|---------|
| Tests | PostToolUse on Bash | Run tests after build |
| Security | PreToolUse on Bash | Block dangerous commands |
| Format | PostToolUse on Write | Validate file format |
| Screenshots | PostToolUse on Write | Log visual captures |

## Setting It Up

1. **Start with security** (Module 07 covers this)
2. **Add test validation** (this module's auto-test-runner)
3. **Add visual logging** (screenshot capture logging)

## Peace of Mind

Once hooks are configured:
- Agents validate their own work
- You don't have to micromanage
- Quality is consistent
- You can focus on higher-level tasks

**This is the power of validation hooks: Trust, but verify automatically.**
