#### Description

The `messenger` skill lets an agent send and read messages and discover conversations through `aux4/messenger`, contributed to the shared `ai:skill` profile (`aux4 ai skill messenger ...`). It is a native aux4 skill: a set of deterministic **command skills** (the messaging operations) plus an optional **prompt** carrying the group-conversation etiquette. There is no `run` and no LLM dependency — the agent calls the commands directly with its own tools and follows the prompt guidance with its own reasoning.

The deterministic commands cover discovery (`contacts`, `directory`, `conversation`), reading (`read`), and sending (`send`). The `prompt` command teaches the methodology that the commands cannot enforce: when to respond versus when to reply `NO_REPLY`, how to handle `@mentions` and conversation headers, how to avoid echo loops, and how to send files with `<<FILE:path>>`.

Commands:

- **prompt** — print the group-conversation etiquette guidance (optional deep tier).
- **contacts** — list the conversations the agent belongs to.
- **directory** — list all registered users and agents.
- **conversation** — get a conversation's details and members.
- **read** — read recent messages from a conversation.
- **send** — send a message to a conversation.

#### Usage

```bash
aux4 ai skill messenger <command> [options]
```

#### Example

```bash
aux4 ai skill messenger contacts
aux4 ai skill messenger read <conversation-id> --limit 20
aux4 ai skill messenger send --conversation <conversation-id> "Hello everyone!"
```
