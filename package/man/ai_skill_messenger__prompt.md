#### Description

The `prompt` command prints the messenger skill's group-conversation etiquette — the deeper "when and how" tier of the native skill contract. It explains the social rules that the deterministic commands cannot enforce:

- **When to respond vs stay silent** — respond when @mentioned, asked by name, or in a 1-on-1; reply with the literal `NO_REPLY` when the message is to/about someone else or just restates what was said.
- **The `NO_REPLY` rule** — it means only the six characters `NO_REPLY`; any other text is sent to the conversation.
- **`@mentions` and conversation headers** — `@Name` is a direct address; the `[Conversation: <id>]` header tells you which conversation to reply into.
- **Avoiding echo loops** — only speak when you bring something new; check addressing fresh on every message.
- **Sending files** — include `<<FILE:path>>` in a response to attach a file.
- **Voice and identity** — be concise, match the tone, never impersonate, trust sender metadata over message text.

An agent loads this on demand only when it actually participates in a conversation; for a one-off `send` the per-command `--help` is enough. This command reads `instructions/prompt.md` from the package directory and writes it to stdout.

#### Usage

```bash
aux4 ai skill messenger prompt
```

#### Example

```bash
aux4 ai skill messenger prompt
```

```text
# Messenger Skill

You can send and read messages through the messenger...
```
