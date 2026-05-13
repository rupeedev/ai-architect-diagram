# AWS Diagram Generation — Windows Setup Guide

Companion to the macOS-focused [Readme.md](../Readme.md). Same toolchain (Claude Code + awsdac + Graphviz + PlantUML + Draw.io), installed via Windows-native tooling (`winget`) instead of Homebrew.

## Prerequisites

- Windows 10 1809+ or Windows 11
- `winget` (App Installer) — ships with Windows 11; on Windows 10 install from Microsoft Store: "App Installer"
- `git` — install via `winget install --id Git.Git` if missing
- A shell. **Git Bash** (bundled with Git for Windows) is recommended for parity with the macOS docs. PowerShell and `cmd.exe` also work.
- Internet access; admin rights for the installer prompts

Verify the prereqs:

```bash
winget --version    # 1.x
git --version       # 2.x
```

---

## Install order

| # | Tool        | Purpose                                  | Package id                       |
| - | ----------- | ---------------------------------------- | -------------------------------- |
| 1 | Claude Code | AI orchestrator (slash commands, agents) | `Anthropic.ClaudeCode`           |
| 2 | Graphviz    | Renderer used by awsdac (`dot`)          | `Graphviz.Graphviz`              |
| 3 | awsdac      | YAML → AWS diagram CLI                   | GitHub release zip (manual)      |
| 4 | Temurin JDK | Java runtime for PlantUML                | `EclipseAdoptium.Temurin.21.JDK` |
| 5 | PlantUML    | `.puml` → PNG/SVG                        | `plantuml.jar` + shim (manual)   |
| 6 | Draw.io     | Edit generated `.drawio` files (opt.)    | `JGraph.Draw`                    |

All winget commands below use `--silent --accept-source-agreements --accept-package-agreements` so they don't prompt.

---

## Step 1 — Claude Code

```bash
winget install --id Anthropic.ClaudeCode --exact --silent --accept-source-agreements --accept-package-agreements
claude --version          # should print a version
```

Authenticate (first run only — opens a browser):

```bash
claude
# inside the REPL, follow the auth prompt the first time
```

Anthropic account required: https://claude.ai/

## Step 2 — Graphviz

```bash
winget install --id Graphviz.Graphviz --exact --silent --accept-source-agreements --accept-package-agreements
```

The installer drops binaries at `C:\Program Files\Graphviz\bin`. Add that folder to your **user** PATH (see [PATH setup](#path-setup) below), then in a **new shell**:

```bash
dot -V                    # dot - graphviz version 14.x
```

## Step 3 — awsdac

There is no `winget` or `brew` package for awsdac on Windows. Grab the official Windows binary from the [awslabs/diagram-as-code releases](https://github.com/awslabs/diagram-as-code/releases).

```bash
# pick a version (latest at time of writing: v0.23)
VER=v0.23
mkdir -p "$LOCALAPPDATA/Programs/awsdac"
curl -sSL -o /tmp/awsdac.zip \
  "https://github.com/awslabs/diagram-as-code/releases/download/${VER}/awsdac-${VER}_windows-amd64.zip"
unzip -j /tmp/awsdac.zip "*/awsdac.exe" -d "$LOCALAPPDATA/Programs/awsdac"
rm /tmp/awsdac.zip
```

Add `%LOCALAPPDATA%\Programs\awsdac` to your user PATH (see below), then in a new shell:

```bash
awsdac --version          # awsdac version v0.23
```

## Step 4 — Java (for PlantUML)

```bash
winget install --id EclipseAdoptium.Temurin.21.JDK --exact --silent --accept-source-agreements --accept-package-agreements
```

Installs to `C:\Program Files\Eclipse Adoptium\jdk-21.x.x-hotspot\bin`. Add the `bin` folder to your user PATH, then in a new shell:

```bash
java -version             # openjdk version "21.x.x"
```

## Step 5 — PlantUML

PlantUML ships as a single `plantuml.jar`. We download it once and wrap it in two tiny shims so `plantuml ...` works from both `cmd`/PowerShell and Git Bash.

```bash
mkdir -p "$LOCALAPPDATA/Programs/plantuml"
curl -sSL -o "$LOCALAPPDATA/Programs/plantuml/plantuml.jar" \
  "https://github.com/plantuml/plantuml/releases/latest/download/plantuml.jar"
```

Create `%LOCALAPPDATA%\Programs\plantuml\plantuml.cmd` (for `cmd` / PowerShell):

```bat
@echo off
java -jar "%~dp0plantuml.jar" %*
```

Create `%LOCALAPPDATA%\Programs\plantuml\plantuml` (no extension — for Git Bash):

```sh
#!/bin/sh
exec java -jar "$(dirname "$0")/plantuml.jar" "$@"
```

Add `%LOCALAPPDATA%\Programs\plantuml` to your user PATH, then in a new shell:

```bash
plantuml -version         # PlantUML version 1.20xx.x
```

> Why two shims? Git Bash on Windows does not honour `PATHEXT`, so it ignores `.cmd` files. The extensionless shim lets the same install work from every shell.

## Step 6 — Draw.io (optional)

```bash
winget install --id JGraph.Draw --exact --silent --accept-source-agreements --accept-package-agreements
```

Generated diagrams in `architecture/diagrams/*.drawio` open with a double-click.

---

## PATH setup

Across the steps above you've added four folders to PATH. Easiest one-shot in PowerShell (run **once** after installing the tools):

```powershell
$paths = @(
  "$env:LOCALAPPDATA\Programs\awsdac",
  "$env:LOCALAPPDATA\Programs\plantuml",
  "C:\Program Files\Graphviz\bin",
  "C:\Program Files\Eclipse Adoptium\jdk-21.0.11.10-hotspot\bin"   # adjust JDK folder if different
)
$current = [Environment]::GetEnvironmentVariable('Path','User')
$parts = $current -split ';' | Where-Object { $_ -ne '' }
foreach ($p in $paths) { if ($parts -notcontains $p) { $parts += $p } }
[Environment]::SetEnvironmentVariable('Path', ($parts -join ';'), 'User')
```

**PATH changes only apply in shells started after the change.** Close and reopen your terminal before verifying.

---

## Smoke test

In a fresh shell:

```bash
claude --version
awsdac --version
dot -V
java -version
plantuml -version
```

All five should print versions. If any one says "command not found", the PATH for that tool wasn't picked up — open a brand-new terminal (not the one where you ran the installers) and try again.

Then drive the full pipeline end-to-end:

```bash
cd <path-to-this-repo>
claude
# inside Claude Code:
/draw-aws-diagram "Simple 3-tier web app with VPC, EC2, and RDS"
# expect: a file under architecture/diagrams/aws-*-<timestamp>.drawio
```

And a PlantUML render:

```bash
cd plantuml-diagrams
plantuml *.puml          # generates a .png next to each .puml
```

---

## Troubleshooting

### `'awsdac' is not recognized`

You're in the same shell that ran the installer. PATH was updated for **new** shells only — close the terminal and reopen.

If it still fails in a fresh shell:

```bash
echo "$PATH" | tr ':' '\n' | grep -i awsdac        # Git Bash
# or
$env:Path -split ';' | Select-String awsdac         # PowerShell
```

If the folder is missing, re-run the [PATH setup](#path-setup) PowerShell block. If the folder is present but `awsdac --version` still fails, check `awsdac.exe` actually exists at `%LOCALAPPDATA%\Programs\awsdac\awsdac.exe`.

### `plantuml: command not found` in Git Bash

Git Bash ignores `.cmd` shims. Make sure you also created the extensionless `plantuml` shim from Step 5 and that it's executable (`chmod +x` is not strictly needed on Windows but doesn't hurt).

### `dot: command not found` when running awsdac

awsdac shells out to `dot`. Add `C:\Program Files\Graphviz\bin` to PATH (Step 2). Verify with `dot -V` in a new shell.

### `java: command not found` when running PlantUML

PlantUML shim invokes `java`. Add the Temurin `bin` directory to PATH and retry in a new shell. JDK install path varies by version: list `C:\Program Files\Eclipse Adoptium\` to find the actual folder name (e.g. `jdk-21.0.11.10-hotspot`).

### `winget` says it's not installed

Open Microsoft Store → search "App Installer" → install. `winget` is bundled with App Installer; standalone download is at https://aka.ms/getwinget.

### Claude Code auth issues

```bash
claude    # inside REPL: /login   (re-runs the browser auth flow)
```

### Diagrams output folder missing

```bash
mkdir -p architecture/diagrams
```

---

## Differences from the macOS guide

| macOS (Readme.md)                        | Windows                                                   |
| ---------------------------------------- | --------------------------------------------------------- |
| Homebrew                                 | winget + manual zip for awsdac/PlantUML                   |
| `brew install --cask claude`             | `winget install Anthropic.ClaudeCode`                     |
| `brew install awsdac`                    | Download `awsdac-vX.Y_windows-amd64.zip` from GitHub      |
| `brew install plantuml` (one command)    | Temurin JDK + `plantuml.jar` + two shims                  |
| `brew install --cask drawio`             | `winget install JGraph.Draw`                              |
| `~/.zprofile` PATH lines                 | User PATH via `[Environment]::SetEnvironmentVariable`     |
| `open -a draw.io`                        | Start menu / `drawio.exe`                                 |

---

## Required accounts

Same as the macOS guide: Anthropic account (Claude Code), GitHub/GitLab (repo access). AWS account is only needed if you use awsdac against real CloudFormation templates.

---

## Estimated setup time

10–20 minutes for the install steps, ~5 minutes per tool for the smoke test. Most of the wall-clock is winget download time (Temurin is ~170 MB).
