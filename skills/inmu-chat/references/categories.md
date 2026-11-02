# Conversation category controls

These settings control which expressions the assistant deliberately uses in conversation. The agent reads TOML as instructions; there is no runtime output filter. Ordinary words used with their literal meaning, user quotations, and evidence necessary for an inspection are not prohibited by a conversation toggle. The deliverable boundary in [the skill](../SKILL.md) still applies.

## Categories

Category labels select vocabulary, not definitive historical provenance. Section labels in the phrase tables identify membership:

| ID | Recognized request labels | Vocabulary |
| --- | --- | --- |
| `core` | core, basic, 基本, 本編 | Main phrase table, except entries assigned to a dedicated category below |
| `takuya` | takuya, タクヤ, タクヤさん, KBTIT | Performances and related wording in the dedicated related-table section |
| `second_tier` | second-tier, 二軍, 二軍淫夢 | Related performers in the dedicated section |
| `cookie` | cookie, クッキー, クッキー☆ | Voice-drama and livestream entries in the dedicated section |
| `ai` | AI, AI拓也, AI系 | AI-related derivatives in the dedicated section |
| `chimera` | chimera, キメラ, キメラ語録, 改変 | Chimera and adapted wording, including newly improvised combinations |
| `inmu_king` | INMU KING, インムキング | Entries in the song/adaptations section |
| `copypasta` | copypasta, コピペ, FF外 | Entries in the community copypasta section |

The main [phrase table](phrases.md) defaults to `core`. When an expression is also listed in a dedicated section of [related phrases](related-phrases.md), use the dedicated category instead of `core`, including variants and shortened forms of that entry. For example, the repeated KBTIT entries use `takuya`, and the repeated GO and MYN entries use `second_tier`. A disabled category cannot be bypassed by selecting a duplicate from the main table.

If an expression belongs to more than one dedicated category, all must be enabled. Known references in the entry's background also count: a chimera identified as used in INMU KING needs both `chimera` and `inmu_king`. All adapted patterns require `chimera`, including adapted variants embedded in the main table. Recognizable adaptations additionally require the categories of their source components. Disabling `chimera` still allows unchanged expressions from enabled source categories. If membership is uncertain, choose a clearly enabled expression or ordinary language rather than guessing that a disabled source is allowed.

## Loading and precedence

Resolve settings in this order, with later values overriding earlier values per category:

1. Read the installed skill's [settings.toml](../settings.toml). All eight categories default to `true` when a key is absent. If this required resource is missing or unreadable, explain the problem in ordinary language and suspend the style until resolved.
2. Read `.inmu-chat.toml` at the current Git repository root, or at the current working directory outside a Git repository. Do not search parent directories for additional settings. Missing keys inherit the defaults.
3. Apply the user's current-chat category requests, using the most recent request for each category. An explicit instruction to stop the style disables all categories; a sensitive context can also require ordinary language.

Re-resolve file settings on a new skill activation, a change of project, or a request to reload them. Retain chat overrides until the user resets them or the chat ends. A request to reset category preferences clears chat overrides and reloads file settings; it does not delete saved preferences. Resetting saved preferences requires an explicit request.

Use TOML booleans `true` and `false` in a `[categories]` table. Unknown category keys, non-boolean values, malformed TOML, or an existing file that cannot be read are configuration errors. Explain the file and problem in ordinary language and suspend styled replies until corrected or the user explicitly requests ignoring that file. Do not silently fall back to all enabled. Other top-level tables are outside this configuration's scope and can be preserved.

## Chat requests and saving

Accept category IDs and the request labels above. Enabling or disabling a named category changes only that category; an "only" request disables all others. "All on" and "all off" set all eight. Ask which category was intended when a label is unknown or ambiguous, and keep the existing selection while clarifying. Check the resulting selection before acknowledging the request. On a status request, list each category's effective ON/OFF value and whether it comes from defaults, project settings, or a chat override.

Requests apply to this chat without writing files. When the user explicitly asks to save a selection, create or update the project's `.inmu-chat.toml`, preserving unrelated settings and comments. Save only the requested category changes; an "only" or "all" selection writes all eight. A request to save the current selection also writes all eight effective values. Explain the saved path and scope. Do not modify the installed defaults unless the user asks to change those defaults. Project settings survive new chats, but updates to an installed skill may replace edits made inside its directory.

To persist a selection, edit the project's `.inmu-chat.toml`, for example:

```toml
[categories]
cookie = false
ai = false
```

The other categories inherit the installed defaults. To enable just one category, set its value to `true` and the other seven to `false`.

## Inspection and default conversation style

Conversation settings do not narrow a document inspection. Inspect all categories unless the user explicitly limits inspection scope. A report may quote a disabled expression as necessary evidence; do not add it to the surrounding conversational prose. A category-scoped inspection must identify that scope and its limits.

Codex's explicit-only invocation policy is unchanged. A separate default-style instruction in `AGENTS.md` must explicitly load this file and the installed skill's `settings.toml` before the first styled reply to use category filtering without invoking the skill. That instruction must make category restrictions take precedence over its frequency guidance and examples, use ordinary language when all categories are off, and suspend the style if the category resources cannot be found or read.

## Manual behavior checks

These are review scenarios, not measured model results or deterministic enforcement tests:

| Setup or request | Expected behavior |
| --- | --- |
| No project file or chat override | All eight categories enabled |
| Project disables `cookie`; chat enables `ai` | `cookie` stays off; `ai` is on; the other six inherit defaults |
| Disable `takuya` while `core` stays on | Repeated KBTIT entries in the main table and recognizable derivatives are unavailable |
| Disable `core`; leave `takuya` enabled | Dedicated performance entries remain available, including duplicates in the main table |
| Disable `chimera`; leave `core` enabled | Unchanged core expressions remain available; improvised adaptations do not |
| Enable `chimera` but disable `inmu_king` | A chimera explicitly associated with the song remains unavailable |
| Only `cookie` enabled | All seven other categories disabled; acknowledgement uses only permitted vocabulary or ordinary language |
| All off, followed by a normal coding request | Ordinary conversation, including progress updates; no forced expression |
| All off, followed by a broad inspection | Both phrase tables checked; necessary quotations allowed in the report |
| Project has a misspelled key, a string boolean, malformed TOML, or a read error | Explain the configuration error and use ordinary language |
| Chat-only toggle, then a new chat | Reload saved settings; do not claim the previous toggle was saved |
| Save one category with unrelated TOML content present | Update that category, preserving other values and comments |
| Reset chat preferences after a saved project override | Clear chat overrides and keep the saved project selection |
