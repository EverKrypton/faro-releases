# Faro

A terminal coding agent. Fast, cache-aware, and it tells you what it costs.

```
◆ Faro · cache-aware coding agent
› add a health route and a test
→ read src/server.ts
→ edit src/server.ts (1 replacement)
→ write test/health.test.ts
· ctx 12.4k/400.0k cache 94.2% in 812 cached 11.3k out 341 $0.0009 left $7.99
```

## Install

Requires **Node 20 or newer** (`node -v`).

```bash
npm install -g https://github.com/EverKrypton/faro-releases/releases/latest/download/faro-agent.tgz
faro --version
```

Windows: use WSL. Android/Termux: `pkg install nodejs-lts` first, then the same command.

## Get a key

```bash
faro signup you@example.com     # free key, activated immediately
```

Or, if you were given a key:

```bash
faro login FARO-XXXX-XXXX-XXXX-XXXX
```

You never need an API key. No provider account, no configuration file to edit.

## Use

```bash
cd ~/my-project
faro                                   # interactive
faro -p "fix the failing test" --yolo  # one-shot
faro usage                             # what you spent, from the server
faro models                            # available models
```

In a session:

| command | what it does |
|---|---|
| `/help` | commands |
| `/stats` | context, cache hit rate, spend |
| `/compact` | shrink the context, keeps the session |
| `/memory` | what the agent remembers about this project |
| `/new` | fresh session |
| `/model <id>` | switch model (warns: resets the cache) |
| `/undo` | drop the last turn |
| `/exit` | quit |

## What it does

- **Reads and edits code** with `read`, `write`, `edit`, `glob`, `grep`.
- **Runs commands** with `bash`, asking first unless you pass `--yolo`.
- **Remembers your project** across sessions — build commands, conventions, gotchas.
- **Delegates research** to subagents with their own context, so your session stays small.
- **Shows the cache hit rate and the cost of every turn.** Most agents hide this; it is the difference between a $12 month and a $200 month.

## Plans

| | free | pro |
|---|---|---|
| included usage | $0.20 / month | $8 / month, then top-ups |
| turns per message | 15 | 200 |
| context | 64k | 400k |
| subagents | — | yes |

`faro usage` shows exactly what is left. When the balance runs out the agent stops
instead of silently billing you.

## Troubleshooting

| symptom | fix |
|---|---|
| `no license on this machine` | `faro signup you@example.com` |
| `this build cannot be unlocked` | `faro login <key>` again |
| `license revoked` | ask for a new key |
| `insufficient balance` | `faro usage`, then top up or upgrade |
| `context ... exceeds the cap` | `/compact` or `faro --new` |
| `node: command not found` | install Node 20+ |
| install fails on Android | `pkg install nodejs-lts` first |

## Uninstall

```bash
npm uninstall -g faro-agent
rm -rf ~/.faro
```

## License

MIT. The client is provided as a compiled, sealed artifact; the source is not
distributed. Usage is metered by the Faro gateway, which is what the plans pay for.
