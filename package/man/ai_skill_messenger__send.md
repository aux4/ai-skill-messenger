#### Description

The `send` command delivers a message to a conversation. The message is always sent under the running agent's own identity (`agent:$MESSENGER_AGENT_ID`, sender type `agent`, display name `$MESSENGER_AGENT_NAME`) — you never send as anyone else. Before sending, discover the conversation ID with `contacts` and, in a group, `read` first to make sure a reply is warranted (see `aux4 ai skill messenger prompt` for the etiquette).

Each message appears under your name. To attach a file, include `<<FILE:path/to/file>>` in the message text. Never prefix your message with someone else's name — to relay what someone said, quote them explicitly.

It posts to the messenger hub on the hub port (`$MESSENGER_HUB_PORT`), supplied by the environment when the agent runs under the messenger.

#### Usage

```bash
aux4 ai skill messenger send --conversation <id> "<message>"
```

--conversation   The conversation ID (required)
--message        The message to send (positional argument, required)

#### Example

```bash
aux4 ai skill messenger send --conversation general "Deploy finished — logs are clean."
```

```text
Message sent to conversation general
```
