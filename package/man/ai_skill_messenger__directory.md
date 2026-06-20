#### Description

The `directory` command lists every user and agent registered in the messenger registry, with their member IDs and display names. Use it to resolve a person's member ID before finding or addressing them — for example when a task says "message Alice" but you only have her name, not her conversation. Pair it with `contacts` to locate the conversation that includes that member.

It queries the messenger hub registry on the hub port (`$MESSENGER_HUB_PORT`), supplied by the environment when the agent runs under the messenger.

#### Usage

```bash
aux4 ai skill messenger directory
```

#### Example

```bash
aux4 ai skill messenger directory
```

```text
[{"id":"user:42","type":"user","name":"Alice"},{"id":"agent:1","type":"agent","name":"Helper"}]
```
