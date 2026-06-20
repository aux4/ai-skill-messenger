#### Description

The `read` command returns the most recent messages from a conversation, newest activity included. Use it to catch up **before** you speak — especially in a group, so you understand the tone and topic and don't repeat what was already said. Reading first is how you "read the room": decide whether the conversation needs you at all, and address the actual question rather than just acknowledging.

It queries the messenger hub on the hub port (`$MESSENGER_HUB_PORT`), supplied by the environment when the agent runs under the messenger.

#### Usage

```bash
aux4 ai skill messenger read <id> [--limit <n>]
```

--conversation   The conversation ID (positional argument, required)
--limit          Maximum number of messages to retrieve (default: `10`)

#### Example

```bash
aux4 ai skill messenger read general --limit 20
```

```text
[{"sender":"Alice","content":"Has anyone seen the deploy logs?"}, ...]
```
