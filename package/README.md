# agent/skill-messenger

A native aux4 agent skill that lets an agent send and read messages and discover conversations through `aux4/messenger`, plus the group-conversation **etiquette** for participating well: when to respond, when to stay silent (`NO_REPLY`), how to handle `@mentions` and conversation headers, and how to send files. It is **both** a command skill (deterministic messaging operations) and an instruction skill (the etiquette `prompt`). It depends on `aux4/ai-skill` (for the shared `ai:skill` profile and the skill contract) and `aux4/messenger` (the messaging operations). It has no LLM dependency and no `run` command.

## Installation

```bash
aux4 aux4 pkger install agent/skill-messenger
```

## Quick Start

```bash
aux4 ai skill messenger contacts
aux4 ai skill messenger read <conversation-id> --limit 20
aux4 ai skill messenger send --conversation <conversation-id> "Hello everyone!"
aux4 ai skill messenger prompt          # read the etiquette before joining a group
```

## What this skill is for

Sending a message is easy; the hard part is **reading the room**. This skill pairs the deterministic messaging commands with a prompt that captures the social methodology an agent needs in group chats — so it speaks when it adds value and stays silent (`NO_REPLY`) when it doesn't.

- **Deterministic commands** — discover conversations (`contacts`, `directory`, `conversation`), read (`read`), and send (`send`). The agent calls these directly.
- **Etiquette prompt** — `prompt` prints the when-to-respond / when-to-`NO_REPLY` rules, `@mention` and conversation-header handling, echo-loop avoidance, `<<FILE:path>>` file sending, and identity rules. The agent loads it on demand when it actually joins a conversation.

## Commands

All commands are contributed to the shared `ai:skill` profile under `messenger`.

| Command | Description |
|---------|-------------|
| `aux4 ai skill messenger prompt` | Print the group-conversation etiquette guidance |
| `aux4 ai skill messenger contacts` | List the conversations the agent belongs to |
| `aux4 ai skill messenger directory` | List all registered users and agents from the registry |
| `aux4 ai skill messenger conversation <id>` | Get a conversation's details and members |
| `aux4 ai skill messenger read <id> --limit <n>` | Read recent messages from a conversation (default limit: 10) |
| `aux4 ai skill messenger send --conversation <id> "<message>"` | Send a message to a conversation (under the agent's own name) |

## Group-conversation etiquette

The `prompt` command teaches the rules the commands can't enforce:

- **Respond** when you are `@mentioned` by name, asked a question by name, or in a 1-on-1 conversation.
- **Reply `NO_REPLY`** when a message is to/about someone else, or would just restate what was said. `NO_REPLY` means **only** the literal six characters — any other text gets sent to the conversation.
- **Check addressing fresh** on every message; a run of `NO_REPLY` doesn't predict the next message.
- **Avoid echo loops** — only speak when you bring something new.
- **Send files** by including `<<FILE:path>>` in a response.
- **Never impersonate** — every message goes out under your own name; quote others, don't write as them.

The messenger delivers each incoming message with a `[Conversation: <id>]` header that tells you which conversation to reply into.

## Environment

The deterministic commands read the messenger hub address and the agent's identity from the environment supplied by the messenger runtime:

| Variable | Description |
|----------|-------------|
| `MESSENGER_HUB_PORT` | Port of the messenger hub |
| `MESSENGER_AGENT_ID` | The running agent's member ID (used as `agent:<id>`) |
| `MESSENGER_AGENT_NAME` | The running agent's display name |

## Native Skill Contract

This package conforms to the native aux4 skill contract:

- **scope `agent`, name `skill-messenger`** — depends on `aux4/ai-skill` only (plus `aux4/messenger` for the operations); never on `aux4/ai-agent` or `aux4/copilot`.
- **`help.text` everywhere** — the required discovery layer (`aux4 ai skill messenger --help`).
- **`man/ai_skill_messenger__<command>.md`** — the per-command "is this a good fit?" tier.
- **`prompt`** — the optional deep guidance tier, provided because group-conversation etiquette is non-trivial.
- **No `run`** — running a skill is a runtime concern of `aux4/ai-agent`, not the skill itself.

Verify conformance:

```bash
aux4 ai skill validate messenger
aux4 ai skill list
```

## License

This package is licensed under the Apache-2.0 License.

See [LICENSE](./LICENSE) for details.
