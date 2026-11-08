---
tags: [parked, developer-tools, rust, profiling, systems]
aliases: [Perfx, Function Profiler, Performance Tool, Rust Profiler]
created: 2026-06-27
status: parked
---

# Perfx — Function Performance Profiler in Rust

> **Status:** 📋 Parked. Learning project. Build when ready.
> **Platform:** CLI (Linux, macOS, Windows)
> **Stack:** Rust
> **Effort:** ~45 hours

---

## The Story

You worked with gprof. It's outdated, inaccurate, and painful. You want a modern function profiler written in Rust that works with any codebase, any language.

**Perfx is that tool.**

**Inspired by:**
- perf (Linux kernel profiler — powerful but complex)
- gprof (outdated, "exists for historical reasons")
- flamegraph (visual profiling, works with perf)
- criterion (Rust benchmarking library)

---

## The Problem

**Existing tools fail because:**
- gprof is outdated, inaccurate, no hardware counters
- perf is Linux-only, steep learning curve
- Valgrind/Callgrind has 20-50x slowdown
- Intel VTune is commercial, expensive
- No modern, cross-platform, language-agnostic profiler

**What you want:**
- Function-level profiling (any language)
- Cross-platform (Linux, macOS, Windows)
- Modern CLI with TUI
- Flamegraph generation (no external tools)
- History + diff (track performance over time)

---

## The Solution

**Perfx = Modern function profiler in Rust**

1. **Record** — Sample any running process (perf_event_open on Linux)
2. **Symbol resolution** — Parse ELF/Mach-O/PE binaries
3. **Report** — Flat profile (function, time %, call count)
4. **Flamegraph** — Generate interactive SVG (no external tools)
5. **History** — Save profiling runs, compare over time

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    PERFX                                     │
│                                                              │
│  ┌────────────────────────────────────────────────────────┐ │
│  │  CLI + TUI                                             │ │
│  │  - perfx record ./myapp                                │ │
│  │  - perfx report                                        │ │
│  │  - perfx flamegraph                                    │ │
│  │  - perfx diff run1.perfx run2.perfx                    │ │
│  └──────────────────────┬─────────────────────────────────┘ │
│                         │                                    │
│  ┌──────────────────────┴─────────────────────────────────┐ │
│  │  RUST CORE                                             │ │
│  │  - Sampling engine (perf_event_open)                   │ │
│  │  - Symbol resolver (gimli, goblin, pelite)            │ │
│  │  - Flamegraph generator (inferno)                      │ │
│  │  - History store (SQLite)                              │ │
│  └──────────────────────────────────────────────────────  │ │
└─────────────────────────────────────────────────────────────┘
```

---

## Features

### P0 — V1: Core Profiler (~20h)

1. **Record** — Sample any running process
2. **Symbol resolution** — Parse ELF/Mach-O/PE binaries
3. **Report** — Flat profile (function, time %, call count)
4. **Flamegraph** — Generate interactive SVG
5. **History** — Save profiling runs

### P1 — V2: Intelligence (~15h)

6. **Diff** — Compare two runs, highlight regressions
7. **Hot path detection** — Top 3 bottlenecks
8. **Source annotation** — Hot spots (if debug info available)
9. **TUI** — Terminal UI for interactive exploration

### P2 — V3: Polish (~10h)

10. **Cross-platform** — Linux, macOS, Windows
11. **Export** — JSON, CSV, Markdown
12. **CI integration** — Fail build if performance regresses

---

## Key Decisions

| Decision | Choice | Why |
|----------|--------|-----|
| Language | Rust | Fast, small binary, systems programming |
| Syscalls | perf_event_open (Linux) | Hardware performance counters |
| Binary parsing | gimli (ELF), goblin (Mach-O), pelite (PE) | Cross-platform |
| Flamegraph | inferno | Rust flamegraph library |
| TUI | ratatui | Modern terminal UI |

---

## Monetization

**None.** Open source learning project.

---

## Worth Assessment

| Dimension | Score | Notes |
|-----------|-------|-------|
| Portfolio value | 7/10 | Rust systems programming |
| Learning value | 9/10 | Deep Rust, OS internals, binary formats |
| Market/user value | 3/10 | Niche, gprof users, students |
| Personal value | 6/10 | You'll use it for learning Rust |

---

## Dependencies

- **None** — Standalone tool

---

## Quality Markers

- [ ] Record works on Linux
- [ ] Symbol resolution works
- [ ] Flamegraph generation works
- [ ] History + diff works
- [ ] Cross-platform (Linux, macOS, Windows)

---

**Parked. Build when you want to learn Rust deeply, Master.**
