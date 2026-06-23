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
| `#private/chenzhiqiang` | Account credentials, login info, API tokens, system access |
| `#private/clinic` | Medical info — clinic addresses, treatments, medications, health checkups |
| `#private/life` | Personal life notes — home appliances, daily living, household info |
| `#private/resources` | Personal files and shared resources — Baidu pan links, download codes, shared docs |
| `#private/travel` | Travel info — airline accounts, bookings, destination guides. Sub-tag by country e.g. `#private/travel/thailand` |
| `#private/visa` | Visa application requirements, procedures, documents checklist |
| `#private/グルメ` | Restaurant and food recommendations (mainly Japan) |
| `#work` | Any professional/work-related content — use as parent tag for all job-related memos |
| `#work/rakuten` | Rakuten-specific work content — nested under `#work` |
| `#reading` | Book notes, article summaries, quotes worth keeping |
| `#workflow` | Repeatable processes, personal rules, how-to notes for recurring tasks |
| `#journal` | Diary entries, personal reflections, daily logs (replaces `#writing` for clarity) |

### Tag Decision Guide

```
Is it a credential or account?        → #private/chenzhiqiang
Is it medical/clinic/health info?     → #private/clinic
Is it a visa application/procedure?   → #private/visa
Is it travel info or booking?         → #private/travel (or #private/travel/<country>)
Is it a personal file/download link?  → #private/resources
Is it a restaurant/food rec in Japan? → #private/グルメ
Is it other personal life info?       → #private/life
Is it a diary/daily reflection?       → #journal
Is it about natural language study?   → #language
Is it CS/programming knowledge?       → #cs
Is it any work-related content?       → #work
Is it specifically Rakuten-related?   → #work/rakuten
Is it a work process/rule?            → #work/rakuten #workflow
Is it a book/article/quote?           → #reading
Is it a personal process or rule?     → #workflow
Is it personal but not a credential?  → #private
```

Multiple tags are fine when content genuinely spans categories.

### Tag Notes

- `#language` = natural language study only. Programming → `#cs`.
- `#journal` replaces `#writing` — clearer that it means diary, not writing craft or docs.
- `#work/rakuten` and `#private/chenzhiqiang` — always nested, never space-separated.
- Future companies: just add `#work/new_company` alongside existing `#work/rakuten` memos.

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
#private/chenzhiqiang
```

**Workflow:**
```
When publishing to PyPI:
1. rm -rf dist/ build/
2. python -m build
3. twine upload dist/*
#work/rakuten #workflow
```

## Behavior

- When the user says "memo this" or similar, infer the right tags from context — don't ask unless ambiguous.
- For credentials or sensitive info, always add `#private/chenzhiqiang` without being prompted.
- When creating a memo, confirm with the slug so the user can reference it later.
- When searching, show slug + date + a short preview so the user can pick the right one to update or delete.
