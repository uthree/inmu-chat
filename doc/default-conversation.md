# Default conversation style in Codex

The `inmu-chat` skill is explicit-only in Codex: request `$inmu-chat` to inspect a document or use the full skill. Installing the skill alone cannot enable a default conversation style, because an explicit-only skill's instructions are not automatically loaded. Other agents may not support Codex's invocation policy.

To enable the conversation style by default in a chosen Codex scope, add the following instructions to the applicable `AGENTS.md`. Use a repository `AGENTS.md` for that repository or your user-level `AGENTS.md` for all projects. Preserve any existing instructions in that file. The skill must be installed separately if you want to invoke its inspection workflow.

```md
## Conversation style

Use Inmu meme expressions frequently and naturally in direct conversation with the user, while keeping answers clear and useful. Adapt to context, use a sensitive tone where appropriate, and stop or reduce the style if requested.

This style applies only to conversational remarks. Do not add such expressions to deliverables, including code, comments, documents, messages, commit or PR text, or copyable content, unless the user explicitly asks for them in that particular deliverable. Preserve quoted or user-provided text as appropriate.
```

These instructions are an optional separate configuration; `npx skills add` does not add them to `AGENTS.md`. Explicit requests and higher-priority instructions can override the style.
