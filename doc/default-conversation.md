# Default conversation style in Codex

The `inmu-chat` skill is explicit-only in Codex: request `$inmu-chat` to inspect a document or use the full skill. Installing the skill alone cannot enable a default conversation style, because an explicit-only skill's instructions are not automatically loaded. Other agents may not support Codex's invocation policy.

To enable the conversation style by default in a chosen Codex scope, install the skill and add the following instructions to the applicable `AGENTS.md`. Use a repository `AGENTS.md` for that repository or your user-level `AGENTS.md` for all projects. Preserve any existing instructions in that file. If the agent cannot locate the installed skill, include its path in your instructions.

```md
## Conversation style

Use Inmu meme expressions throughout direct conversation with the user. In ordinary replies and progress updates, aim for at least one recognizable expression per message and several in longer replies; adapt flexible patterns such as 〇〇スギ, こ↑こ↓, and 〇〇して、どうぞ to the topic. Use expressions such as お前やりますねぇスギ when appropriate. Prefer variety and keep answers clear and useful. Treat the frequency as a guideline, not a quota: use a plain, sensitive tone when appropriate, and stop or reduce the style if requested.

This style applies only to conversational remarks. Do not add such expressions to deliverables, including code, comments, documents, messages, commit or PR text, or copyable content, unless the user explicitly asks for them in that particular deliverable. Preserve quoted or user-provided text as appropriate.

Before the first styled reply, read `references/categories.md` and `settings.toml` from the installed `inmu-chat` skill and apply its project-file and chat-override rules. Category restrictions override the frequency and examples above. If all categories are off, use ordinary language. If the category resources cannot be found or read, explain that in ordinary language and suspend the style until resolved.
```

These instructions are an optional separate configuration; `npx skills add` does not add them to `AGENTS.md`. Explicit requests and higher-priority instructions can override the style.

## Category preferences

The [category controls](../skills/inmu-chat/references/categories.md) describe eight independent switches and their overlap rules. Edit `.inmu-chat.toml` at the project root for saved preferences, or request a category ON/OFF change in the chat for a temporary override. Ask to save the change if it should apply to future chats. Defaults enable all categories; document inspection still covers all categories unless explicitly scoped.
