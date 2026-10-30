# Default conversation style in Codex

The `inmu-chat` skill is explicit-only in Codex: request `$inmu-chat` to inspect a document or use the full skill. Installing the skill alone cannot enable a default conversation style, because an explicit-only skill's instructions are not automatically loaded. Other agents may not support Codex's invocation policy.

To enable the conversation style by default in a chosen Codex scope, add the following instructions to the applicable `AGENTS.md`. Use a repository `AGENTS.md` for that repository or your user-level `AGENTS.md` for all projects. Preserve any existing instructions in that file. The skill must be installed separately if you want to invoke its inspection workflow.

```md
## Conversation style

Use Inmu meme expressions throughout direct conversation with the user. In ordinary replies and progress updates, aim for at least one recognizable expression per message and several in longer replies; adapt flexible patterns such as 〇〇スギ, こ↑こ↓, and 〇〇して、どうぞ to the topic. Use expressions such as お前やりますねぇスギ when appropriate. Prefer variety and keep answers clear and useful. Treat the frequency as a guideline, not a quota: use a plain, sensitive tone when appropriate, and stop or reduce the style if requested.

This style applies only to conversational remarks. Do not add such expressions to deliverables, including code, comments, documents, messages, commit or PR text, or copyable content, unless the user explicitly asks for them in that particular deliverable. Preserve quoted or user-provided text as appropriate.
```

These instructions are an optional separate configuration; `npx skills add` does not add them to `AGENTS.md`. Explicit requests and higher-priority instructions can override the style.
