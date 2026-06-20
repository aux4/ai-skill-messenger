#### Description

The `conversation` command returns the details and members of a single conversation by ID. Use it to see who is in a conversation before sending — for example to know whether you are in a 1-on-1 (always respond) or a group (read the room first), and to know the names you might be addressed by. The conversation ID comes from `contacts`; never hardcode it.

It queries the messenger hub on the hub port (`$MESSENGER_HUB_PORT`), supplied by the environment when the agent runs under the messenger.

#### Usage

```bash
aux4 ai skill messenger conversation <id>
```

--conversation   The conversation ID (positional argument, required)

#### Example

```bash
aux4 ai skill messenger conversation general
```

```text
{"id":"general","name":"General","members":[{"id":"user:42","name":"Alice"},{"id":"agent:1","name":"Helper"}]}
```
