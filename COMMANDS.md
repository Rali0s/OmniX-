# OMNIX CLI Reference

`omnix` is an operator-focused command-line interface for analysis, build assistance, case memory, incident review, tool routing, traffic inspection, and legacy source inspection.

## Basic Usage

```bash
omnix --version
omnix <command> [options]
```

## Core Commands

### Ask

Ask OMNIX a direct question or request assistance.

```bash
omnix ask <prompt> [--assist] [--compact|--verbose]
```

Useful options:

```bash
--source-map file
--memory-root dir
--lang-confirm auto|yes|no
--build-dir dir
--target name
--build-type type
--install-prefix dir
--recipe id
--ref git-ref
--clean
--build-only
--no-install
--offline
--local-only
```

---

### Ingest

Ingest a file path, source, log, or command output into OMNIX.

```bash
omnix ingest <path|command> [--compact|--verbose] [--memory-root dir] [--source-map file]
```

---

### Analyze

Analyze a case, source file, log, or other input.

```bash
omnix analyze <case|source> [--compact|--verbose] [--memory-root dir] [--source-map file]
```

---

### Decide

Generate or inspect a decision path for a case or source.

```bash
omnix decide <case|source> [--compact|--verbose] [--memory-root dir] [--source-map file]
```

Decision feedback:

```bash
omnix decide feedback <case-id> <decision-id> <helpful|not-helpful> [--note text] [--memory-root dir]
omnix decide outcome <case-id> <decision-id> <success|failed|partial> [--note text] [--memory-root dir]
```

---

## Case Management

Use this subsystem to track investigations, preserve reasoning chains, and export/import case bundles.

```bash
omnix case <id|source> [--assist] [--compact|--verbose] [--memory-root dir] [--source-map file]
omnix case list [--compact|--verbose] [--memory-root dir] [--source-map file]
omnix case search <term> [--compact|--verbose] [--memory-root dir] [--source-map file]
omnix case timeline <id|source> [--compact|--verbose] [--memory-root dir]
omnix case export <id|source> [--out file] [--memory-root dir]
omnix case import <bundle.json> [--memory-root dir]
```

---

## Incident Management

Use incident commands for operational review, triage, and report generation.

```bash
omnix incident list [--compact|--verbose] [--memory-root dir]
omnix incident <id> [--assist] [--compact|--verbose] [--memory-root dir]
omnix incident report <id> [--assist] [--compact|--verbose] [--out file] [--memory-root dir]
```

---

## Defensive Diagnostics

```bash
omnix defend diag <cpu|memory|logs|pid|port> [target] [--compact|--verbose] [--memory-root dir]
```

Diagnostic targets include:

- `cpu`
- `memory`
- `logs`
- `pid`
- `port`

---

## Code Understanding

### Define

```bash
omnix define <symbol-or-term> [file] [--compact|--verbose] [--memory-root dir] [--lang-confirm auto|yes|no]
```

### Explain

```bash
omnix explain <command-or-symbol> [file] [--compact|--verbose] [--memory-root dir] [--lang-confirm auto|yes|no]
```

### Review

```bash
omnix review <path-or-module> [--assist] [--compact|--verbose] [--memory-root dir]
```

### Patch Proposal

```bash
omnix patch-proposal <path-or-module> [--assist] [--compact|--verbose] [--memory-root dir]
```

---

## Build System Assistance

### Build

```bash
omnix build <project-or-path> [--assist] [--compact|--verbose] [--source-map file] [--memory-root dir] [--build-dir dir] [--target name] [--build-type type] [--install-prefix dir] [--recipe id] [--ref git-ref] [--clean] [--build-only] [--no-install] [--offline] [--local-only]
```

### Recipe Authoring

```bash
omnix recipe author <source-path> [--assist] [--compact|--verbose] [--source-map file] [--memory-root dir] [--build-dir dir] [--target name] [--build-type type] [--install-prefix dir] [--clean] [--build-only] [--no-install]
```

### Preflight

```bash
omnix preflight <project-or-path> [--assist] [--compact|--verbose] [--memory-root dir] [--target name] [--install-prefix dir] [--recipe id] [--ref git-ref] [--offline] [--local-only]
```

### Doctor

```bash
omnix doctor <project-or-path> [--compact|--verbose] [--memory-root dir] [--recipe id] [--offline] [--local-only]
```

### Provider Probe

```bash
omnix provider probe [--compact|--verbose] [--memory-root dir]
```

---

## Persona Mode

Switch the operating tone or reasoning posture.

```bash
omnix persona mode <premise|cynic|professional|neutral> [--compact|--verbose] [--memory-root dir]
```

Available modes:

- `premise`
- `cynic`
- `professional`
- `neutral`

---

## Traffic View

### Live Port Capture

```bash
omnix tview port <port> [--interface name] [--count n] [--seconds n] [--payload-bytes n] [--out file.jsonl] [--compact|--verbose] [--memory-root dir]
```

### PCAP Analysis

```bash
omnix tview pcap <file> [--port n] [--payload-bytes n] [--out file.jsonl] [--compact|--verbose] [--memory-root dir]
```

### Traffic View Doctor

```bash
omnix tview doctor [--compact|--verbose] [--memory-root dir]
```

---

## Interactive Shell

```bash
omnix shell [--source-map file] [--memory-root dir] [--assist] [--compact|--verbose]
```

---

## Memory System

Inspect stored memory domains:

```bash
omnix memory [history|prefs|definitions|language|security|uac|cases|runs|tze|legacy|persona|operator|assist] [--compact|--verbose] [--memory-root dir]
```

Prune memory:

```bash
omnix memory prune [--keep n] [--important-only] [--memory-root dir]
```

---

## TZE Run Tracking

```bash
omnix tze runs [--compact|--verbose] [--memory-root dir]
omnix tze latest [--compact|--verbose] [--memory-root dir]
omnix tze replay <run-id> [--compact|--verbose] [--memory-root dir]
omnix tze chain <run-id|latest> [--compact|--verbose] [--memory-root dir]
```

### Diffing Runs

```bash
omnix tze diff <left-run-id> <right-run-id> [--compact|--verbose] [--memory-root dir]
omnix tze diff-latest [--compact|--verbose] [--important-only] [--memory-root dir]
```

### Explaining Changes

```bash
omnix tze explain-change <left-run-id> <right-run-id> [--assist] [--compact|--verbose] [--memory-root dir]
omnix tze explain-change-latest [--assist] [--compact|--verbose] [--important-only] [--memory-root dir]
```

### Reporting and Export

```bash
omnix tze report <run-id> [--assist] [--compact|--verbose] [--out file] [--memory-root dir]
omnix tze diff-report <left-run-id> <right-run-id> [--out file] [--memory-root dir]
omnix tze export <run-id|latest> [--out file] [--memory-root dir]
omnix tze import <bundle.json> [--memory-root dir]
```

### Pruning and Marking Runs

```bash
omnix tze prune [--keep n] [--important-only] [--memory-root dir]
omnix tze mark <run-id> <helpful|not-helpful> [--note text] [--memory-root dir]
```

---

## Tool System

List available tools:

```bash
omnix tool list [--compact|--verbose] [--memory-root dir]
```

Locate a tool:

```bash
omnix tool locate <name> [--compact|--verbose] [--memory-root dir]
```

Diagnose a tool:

```bash
omnix tool doctor <name> [--compact|--verbose] [--memory-root dir]
```

Invoke a tool:

```bash
omnix tool <name> -- <args...> [--compact|--verbose] [--memory-root dir]
```

Built-in analyst modules:

- `inspect-log`
- `inspect-build`
- `inspect-host`
- `report-case`
- `text-pipeline`

---

## Legacy Utilities

```bash
omnix legacy coverage [file]
omnix legacy report [file]
omnix map <file>
omnix search <symbol> [file]
omnix emit-cpp <file> [output-dir]
omnix build-cmake [source-dir] [--target name] [--clean] [--build-dir dir] [--build-type type]
```

---

## Global Options

Most commands support:

```bash
--compact
--verbose
--memory-root dir
--source-map file
```

Build-related commands may also support:

```bash
--build-dir dir
--target name
--build-type type
--install-prefix dir
--recipe id
--ref git-ref
--clean
--build-only
--no-install
--offline
--local-only
```

Language-aware commands may support:

```bash
--lang-confirm auto|yes|no
```

---
