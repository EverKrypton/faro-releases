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

Faro updates itself: when a new release is out, launching it shows a small dialog
with **Cancel** and **Update**. Update installs in place and restarts — sessions and
memory stay.

```bash
npm install -g https://github.com/EverKrypton/faro-releases/releases/latest/download/faro-agent.tgz
faro --version
```

The download is a sealed binary. It does nothing until you activate a key — there
is no usable code inside before that.

Windows: use WSL. Android/Termux: `pkg install nodejs-lts` first, then the same command.

## Get a key

```bash
faro signup you@example.com     # free key, activated immediately
```

You will see exactly what the free plan gives you:

```
✓ free key created for you@example.com

  Free plan · you@example.com
  included  $0.20 of model usage per month
  limits    15 turns per message · 64k context · no subagents
  nothing is charged. when the allowance is used up, faro stops and tells you.

  upgrade: faro upgrade (card or crypto, activates on you@example.com)
```

Or, if you were given a key:

```bash
faro login FARO-XXXX-XXXX-XXXX-XXXX
```

You never need an API key. No provider account, no configuration file to edit.

## When the free allowance runs out

Nothing breaks and nothing is charged. The session is saved and you get:

```
  You are out of included usage.

  the free allowance for this month is spent. the session is saved, nothing is lost.

  keep going
    faro upgrade        pro: $12/mo · $99/yr · $249 lifetime
    faro usage          see exactly what was spent

  pro activates on you@example.com — the same key keeps working, usage is not reset.
```

## Upgrade

```bash
faro upgrade              # opens a crypto/card checkout for your account
faro upgrade --wait <id>  # waits until the payment lands, then confirms
```

The upgrade applies to **the same key and the same email** — no new key, no
re-login, and your spend history stays intact. Card and crypto (USDT, BTC, ETH,
USDC, LTC, TRX) go through the same checkout page.

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
| `/undo` | revert the last turn, including file edits |
| `/init` | write an `AGENTS.md` for this repo |
| `/upgrade` | start a checkout without leaving the session |
| `/update` | check for a new release and install it |
| `/exit` | quit |

Ctrl+C cancels a running answer without closing the session. Ctrl+C twice on an
empty prompt quits.

## What it does

- **Reads and edits code** with `read`, `write`, `edit`, `glob`, `grep`.
- **Runs commands** with `bash`. Safe commands (`git status`, `git diff`, `ls`, `cat`)
  run without asking; anything else asks once, and `--yolo` skips the question.
- **Searches the web** with `web_search`, reads pages with `fetch`, produces cited
  briefings with `research`, and audits a page with `seo`.
- **Remembers your project** across sessions — build commands, conventions, gotchas.
- **Follows your `AGENTS.md`** if the repo has one. `/init` writes it for you.
- **Delegates research** to subagents with their own context, so your session stays small.
- **Undo puts the files back**, not just the conversation. `/undo` reverts the edits.
- **Shows the cache hit rate and the cost of every turn** in the status bar, always
  visible at the bottom. Most agents hide this; it is the difference between a $5
  month and a $200 month.

## Plans

| | free | starter | pro |
|---|---|---|---|
| price | $0 | $5 / mo | $12 / mo · $99 / yr · $249 lifetime |
| included usage | $0.20 / month | $6 / month | $8 / month, then top-ups |
| turns per message | 15 | 120 | 200 |
| context | 64k | 200k | 400k |
| subagents | — | yes | yes |

Usage is metered, not "unlimited": every token costs real money, so a plan includes a
fixed amount of model usage and then asks you to top up. Nothing is charged without
your action, and nothing is silently throttled — when you run out, Faro stops and
says so.

`faro usage` shows exactly what is left. When the balance runs out the agent stops
instead of silently billing you.

## Troubleshooting

| symptom | fix |
|---|---|
| `no license on this machine` | `faro signup you@example.com` |
| `this build cannot be unlocked` | `faro login <key>` again |
| stuck on a long answer | Ctrl+C cancels it, the session stays alive |
| `license revoked` | ask for a new key |
| `insufficient balance` | `faro upgrade`, or `faro usage` to see the spend |
| `context ... exceeds the cap` | `/compact` or `faro --new` |
| `node: command not found` | install Node 20+ |
| install fails on Android | `pkg install nodejs-lts` first |

## Uninstall

```bash
npm uninstall -g faro-agent
rm -rf ~/.faro
```

## Privacy

Faro sends your conversation to the Faro gateway, which forwards it to a model and
records token counts for billing. It does not record your code or your prompts.
The client never reveals which model or provider serves a request.

## License

MIT. The client is provided as a compiled, sealed artifact; the source is not
distributed. Usage is metered by the Faro gateway, which is what the plans pay for.
