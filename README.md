# Orvanta CLI Quickstart

`orvanta` is the official command line interface for
[Orvanta](https://docs.orvanta.cloud) — a visual-first polyglot automation
platform for scripts, flows, triggers, schedules, resources, and apps. Use it
to authenticate against a workspace, scaffold local projects, sync
scripts/flows/apps between your filesystem and a workspace, and run or debug
jobs from your terminal.

## Install

```sh
npm install -g @orvanta/cli
orvanta --version
```

Upgrade later with `orvanta upgrade`.

## Connect to a workspace

```sh
orvanta workspace add
```

This walks you through adding a workspace profile — a `(name, remote URL,
workspace id, token)` tuple stored under your Orvanta config directory
(default `~/.config`, override with `OV_CONFIG_DIR`). You can have multiple
profiles and switch between them with `orvanta workspace switch <name>`.

A workspace token is created from the Orvanta UI under
`User Settings → Tokens`. For self-hosted instances, point the remote at your
own URL (e.g. `https://orvanta.example.com`).

## Initialize a project directory

```sh
orvanta init
```

`orvanta init` creates:

- a sync configuration file (which folders/types to track).
- `AGENTS.md` + `CLAUDE.md` — the agent prompt published in this repo.
- `.claude/skills/` — per-task guides used by AI coding assistants (Claude
  Code, Codex, Pi). These are the same `SKILL.md` files you'll find under
  `skills/` in this repo.

It also offers to bind a workspace profile to the current git branch and to
import git-sync settings from the backend if any are configured.

## Sync between local files and a workspace

```sh
orvanta sync pull     # workspace → local (writes flows, scripts, apps, etc.)
orvanta sync push     # local → workspace
```

Sync is idempotent and diff-aware: `orvanta sync push --dry-run` previews the
changes without applying them.

For individual entities you can also use the type-specific commands:

```sh
orvanta script push   path/to/script.ts
orvanta flow   push   path/to/flow.yaml
orvanta app    push   path/to/app.yaml
orvanta resource push path/to/resource.yaml
```

## Run, inspect, and debug jobs

```sh
orvanta script run u/me/my_script --data '{"foo": "bar"}'
orvanta flow   run u/me/my_flow   --data @inputs.json
orvanta job list --failed --limit 20
orvanta job get  <job_id>
orvanta job logs <job_id>
```

## Scaffold new entities

```sh
orvanta script new u/me/path --language bun
orvanta flow   new u/me/path --summary "..."
orvanta app    new u/me/path --summary "..." --framework svelte
```

These create the correct folder layout and a minimal spec file. Prefer them
over hand-creating the folders — they pick the right naming conventions for
your workspace.

## Triggers and schedules

Triggers (HTTP routes, WebSocket, Kafka, NATS, MQTT, SQS, GCP Pub/Sub, Azure
Event Hubs, Email, Postgres CDC) and cron schedules are tracked as YAML files
synced alongside your scripts and flows. See `skills/triggers/SKILL.md` and
`skills/schedules/SKILL.md` for the full schemas.

## Completion

```sh
source <(orvanta completions bash)        # bash, zsh: source <(orvanta completions zsh)
source (orvanta completions fish | psub)  # fish
```

## Reference

- `cli-commands.md` — every `orvanta` command and flag, generated from the
  source.
- `AGENTS.md` — the top-level prompt the CLI installs into each project (and
  the same instructions AI coding assistants follow when working in an
  Orvanta repo).
- `skills/<name>/SKILL.md` — one self-contained guide per common task.

### Skills index

- `skills/write-script-bash/SKILL.md`
- `skills/write-script-bigquery/SKILL.md`
- `skills/write-script-bun/SKILL.md`
- `skills/write-script-bunnative/SKILL.md`
- `skills/write-script-csharp/SKILL.md`
- `skills/write-script-deno/SKILL.md`
- `skills/write-script-duckdb/SKILL.md`
- `skills/write-script-go/SKILL.md`
- `skills/write-script-graphql/SKILL.md`
- `skills/write-script-java/SKILL.md`
- `skills/write-script-mssql/SKILL.md`
- `skills/write-script-mysql/SKILL.md`
- `skills/write-script-nativets/SKILL.md`
- `skills/write-script-php/SKILL.md`
- `skills/write-script-postgresql/SKILL.md`
- `skills/write-script-powershell/SKILL.md`
- `skills/write-script-python3/SKILL.md`
- `skills/write-script-rlang/SKILL.md`
- `skills/write-script-rust/SKILL.md`
- `skills/write-script-snowflake/SKILL.md`
- `skills/write-flow/SKILL.md`
- `skills/raw-app/SKILL.md`
- `skills/triggers/SKILL.md`
- `skills/schedules/SKILL.md`
- `skills/resources/SKILL.md`
- `skills/write-workflow-as-code/SKILL.md`
- `skills/cli-commands/SKILL.md`
- `skills/preview/SKILL.md`

## About this repo

Auto-generated mirror of the Orvanta CLI's bundled AI-agent guidance and
command reference, published for ingestion by docs aggregators such as
[context7](https://context7.com).

**Do not edit by hand.** This repo is regenerated from the Orvanta platform on
every release — edits here are overwritten. For documentation, issues, and
support, see [https://docs.orvanta.cloud](https://docs.orvanta.cloud).
