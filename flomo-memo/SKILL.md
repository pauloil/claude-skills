---
name: flomo-memo
description: Use when the user wants to save, search, update, or delete a flomo memo — or when something worth remembering comes up in conversation (a decision, insight, link, note, credential, or task). Also triggers when the user says "memo this", "save to flomo", "write a note", "record this", or asks to look something up in their notes. Always apply the tag rules below when writing memos.
---

# Flomo Memo Skill

## Available MCP Tools

Use the `flo` MCP server tools:

| Tool | When to use |
|---|---|
| `create_memo` | Save a new note |
| `list_memos` | Browse recent memos |
| `search_memos` | Find memos by keyword |
| `update_memo` | Edit an existing memo (needs slug) |
| `delete_memo` | Remove a memo (needs slug) |

## Tag Rules

Always add at least one tag. Tags go inline in the memo content using `#tag` syntax.

### Tag Reference

| Tag | Use for |
|---|---|
| `#cs` | CS knowledge: algorithms, systems, tools, code concepts, programming languages |
| `#language` | **Natural language study only** — English, Japanese, etc. Programming language notes → `#cs` |
| `#private` | Personal notes not meant to be shared |
| `#private` `#chenzhiqiang` | Account credentials, login info, API tokens, system access — always use BOTH tags |
| `#work` | Any professional/work-related content — use as parent tag for all job-related memos |
| `#work` `#rakuten` | Rakuten-specific work content — always pair with `#work` |
| `#reading` | Book notes, article summaries, quotes worth keeping |
| `#workflow` | Repeatable processes, personal rules, how-to notes for recurring tasks |
| `#journal` | Diary entries, personal reflections, daily logs (replaces `#writing` for clarity) |

### Tag Decision Guide

```
Is it a credential or account?        → #private #chenzhiqiang
Is it a diary/daily reflection?       → #journal
Is it about natural language study?   → #language
Is it CS/programming knowledge?       → #cs
Is it any work-related content?       → #work
Is it specifically Rakuten-related?   → #work #rakuten
Is it a work process/rule?            → #work #rakuten #workflow
Is it a book/article/quote?           → #reading
Is it a personal process or rule?     → #workflow
Is it personal but not a credential?  → #private
```

Multiple tags are fine when content genuinely spans categories.

### Tag Notes

- `#language` = natural language study only. Programming → `#cs`.
- `#journal` replaces `#writing` — clearer that it means diary, not writing craft or docs.
- `#work` is the parent for all job content. `#rakuten` is always paired with `#work`.
- This makes future company changes easy: just add `#work #new_company` alongside `#work #rakuten`.
- `#chenzhiqiang` is always paired with `#private` — never used alone.

## Memo Format

Keep memos concise. Prefer plain text with `#tags` at the end or inline.

**Plain note:**
```
今天学到了 X。用途是 Y。 #cs
```

**Credential (always use both tags):**
```
Service: GitHub
User: pauloil
Note: use pauloil29@yahoo.co.jp for commits
#private #chenzhiqiang
```

**Workflow:**
```
When publishing to PyPI:
1. rm -rf dist/ build/
2. python -m build
3. twine upload dist/*
#work #rakuten #workflow
```

## Behavior

- When the user says "memo this" or similar, infer the right tags from context — don't ask unless ambiguous.
- For credentials or sensitive info, always add `#private #chenzhiqiang` without being prompted.
- When creating a memo, confirm with the slug so the user can reference it later.
- When searching, show slug + date + a short preview so the user can pick the right one to update or delete.
