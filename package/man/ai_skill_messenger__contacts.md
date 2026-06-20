#### Description

The `contacts` command lists the conversations the agent currently belongs to, with their IDs. It is the discovery entry point: always use it to find a conversation's ID rather than assuming or hardcoding one. To message a specific person, combine it with `directory` (to resolve their member ID) and pick the conversation that includes them.

It queries the messenger hub for conversations whose members include the running agent (`agent:$MESSENGER_AGENT_ID`) on the hub port (`$MESSENGER_HUB_PORT`), both supplied by the environment when the agent runs under the messenger.

#### Usage

```bash
aux4 ai skill messenger contacts
```

#### Example

```bash
aux4 ai skill messenger contacts
```

```text
[{"id":"general","name":"General","members":["agent:1","user:42"]}]
```
