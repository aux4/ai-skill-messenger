# ai skill messenger

Tests for the migrated `agent/skill-messenger` package. This skill is **both** a command
skill (deterministic messaging operations from `aux4/messenger`) and an instruction skill
(the group-conversation etiquette `prompt`). The deterministic `send`/`read`/etc. need a
live messenger hub, so they are exercised via `--help` (signatures) rather than execution.

These assume the package is installed locally so the shared `ai:skill` profile and the
`aux4 ai skill validate`/`list` framework commands can discover it:

```bash
aux4 aux4 releaser install --dir packages/ai/ai-skill-messenger/package --noBuild true
```

## prompt

### should output the messenger skill guidance

```execute
aux4 ai skill messenger prompt
```

```expect:partial
# Messenger Skill
```

### should reference the native ai skill messenger command path

```execute
aux4 ai skill messenger prompt
```

```expect:partial
aux4 ai skill messenger send
```

### should carry the group-conversation etiquette

```execute
aux4 ai skill messenger prompt
```

```expect:partial
Group conversations — read the room
```

### should carry the NO_REPLY rule

```execute
aux4 ai skill messenger prompt
```

```expect:partial
The NO_REPLY rule
```

### should explain NO_REPLY is the literal text only

```execute
aux4 ai skill messenger prompt
```

```expect:partial
the literal six characters `NO_REPLY`
```

### should document @mention handling

```execute
aux4 ai skill messenger prompt
```

```expect:partial
@mentioned by name
```

### should document the conversation header

```execute
aux4 ai skill messenger prompt | grep -c "Conversation: <id>" || true
```

```expect:partial
1
```

### should document file sending

```execute
aux4 ai skill messenger prompt
```

```expect:partial
<<FILE:path/to/file>>
```

### should include the rules section

```execute
aux4 ai skill messenger prompt
```

```expect:partial
## Rules
```

### should NOT reference the old copilot skills path

```execute
aux4 ai skill messenger prompt | grep -c "copilot skills messenger" || true
```

```expect
0
```

## command help

### contacts should describe discovering IDs

```execute
aux4 ai skill messenger contacts --help
```

```expect:partial
List conversations the agent belongs to
```

### read should show conversation and limit parameters

```execute
aux4 ai skill messenger read --help
```

```expect:partial
The conversation ID
```

### read should default limit to 10

```execute
aux4 ai skill messenger read --help
```

```expect:partial
10
```

### send should show the message parameter

```execute
aux4 ai skill messenger send --help
```

```expect:partial
The message to send
```

### conversation should show the conversation parameter

```execute
aux4 ai skill messenger conversation --help
```

```expect:partial
The conversation ID
```

### directory should describe the registry

```execute
aux4 ai skill messenger directory --help
```

```expect:partial
registry
```

## native skill contract

### should be registered under the ai:skill profile

```execute
aux4 ai skill messenger --help
```

```expect:partial
read the room
```

### validate should pass

```execute
aux4 ai skill validate messenger
```

```expect:partial
conforms to the native skill contract
```

### list should show messenger

```execute
aux4 ai skill list
```

```expect:partial
messenger
```

### should NOT expose a run command

```execute
aux4 ai skill messenger --help | grep -c "  run" || true
```

```expect
0
```

### should NOT delegate to ai agent ask

```execute
grep -c "ai agent ask" ../.aux4 || true
```

```expect
0
```

### should NOT carry a copilot model-intent command

```execute
grep -c "preferred model intent" ../.aux4 || true
```

```expect
0
```
