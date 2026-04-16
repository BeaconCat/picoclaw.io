---
title: "PicoClaw v0.2.6 — AI Finally Has Memory, and Learned to Protect Itself"
description: "Long-term memory and the Seahorse short-term memory engine are here. LOCOMO benchmark hit rate up 3×. Process-level sandbox isolation added. WebSocket, gateway PID, and Docker deployment bugs fixed."
date: 2026-04-09
tags: ["Release", "New Features"]
lang: en
author: PicoClaw Team
slug: v026-release
---

**April 9, 2026**  The PicoClaw team is releasing v0.2.6

Two big changes in this version: AI finally **has memory**, and tool execution now runs inside a **sandbox**

Also includes fixes for the WebSocket connection issues from v0.2.5 and a round of stability improvements

---

## 1. Memory System

v0.2.6 adds full memory capabilities — AI no longer starts from zero every conversation

### Long-term Memory

AI decides on its own what's worth remembering — your name, preferences, project context — and writes it to a dedicated memory file

It's loaded automatically at the start of every conversation, so you never have to repeat yourself

There's also a **daily notes** feature: key interaction highlights are recorded each day, and the last 3 days of notes are automatically injected into context

### Short-term Memory (Seahorse Engine)

A brand-new context management engine built on SQLite + FTS5 full-text search:

- **Smart retrieval**: No more dumb truncation — relevant history is searched based on the current topic
- **Auto-compression**: When conversations get long, LLM-generated summaries preserve key information
- **Active recall**: AI can proactively search and expand past conversations
- **Pluggable design**: Implemented via the `ContextManager` interface — switch with one config line

### LOCOMO Benchmark Results

We evaluated memory quality using the [LOCOMO](https://snap-research.github.io/locomo/) academic benchmark (10 real long conversations, ~2,000 Q&A pairs):

| Mode | Evidence Hit Rate | LLM Judge Score |
|------|-------------------|-----------------|
| Traditional truncation | 23.8% | 0.66 |
| **Seahorse smart retrieval** | **70.0%** | **0.84** |

Seahorse's evidence hit rate is **3× higher** than the traditional approach — the advantage is especially clear when information spans multiple conversation turns

---

## 2. Process Sandbox Isolation

**Process isolation**: AI tool execution can now run inside a sandbox environment, no longer operating directly on your system — safer and more reassuring

One line: we put a "safety cage" around AI so it can't accidentally damage your environment while working

---

## 3. Tool & Capability Enhancements

**Hooks enhancement**: The hook system gains a `respond` action, plus complete documentation — custom workflows are now more flexible

**MCP large text storage**: Oversized text results are automatically stored as artifacts — no more blowing up the conversation window

**HTTP custom headers**: Model provider interfaces support injecting custom headers — easier enterprise integration

**write_file improvement**: Fixed nested JSON escape semantics and added tests — writing files is more reliable

---

## 4. Platforms & Channels

**Teams Webhook**: New Teams Webhook output channel — another option for enterprise users

**Feishu (Lark)**: Card and file replies now correctly carry context

**Model fallback**: `model_fallbacks` now uses an independent provider per candidate — if one fails, the next kicks in automatically

---

## 5. Bug Fixes

High-value fixes this release, targeting the core pain points from v0.2.5:

✅ **WebSocket connection failure** — WebSocket URL now derived from the browser address, no longer depends on backend config, finally resolves the connection nightmare since v0.2.5

✅ **WebUI unable to connect to gateway** — Fixed gateway connection issue on WebUI startup

✅ **Gateway PID handling** — Hardened PID liveness checks and WebSocket proxy state management — no more false process detection

✅ **Gateway PID file leftovers** — PID ownership is now verified and stale files cleaned up — restarts no longer get stuck

✅ **Docker startup** — Launcher now passes `-console` and opens networking — running in containers no longer a mystery

✅ **Duplicate `v` in CLI help** — `picoclaw --help` no longer shows `vv0.2.5`

✅ **FreeBSD/ARM compatibility** — Seahorse context manager disabled on unsupported platforms — no more crashes

✅ **exec terminal control characters** — Security-related fix, further hardening planned in upcoming releases

---

## 6. Dependency Updates

- `github.com/pion/rtp` upgraded to 1.10.1
- `modernc.org/sqlite` upgraded to 1.48.0

---

## Summary

| Category | Update |
|----------|--------|
| 🧠 Memory system | Long-term memory + Seahorse short-term engine + daily notes |
| 📊 Memory benchmark | LOCOMO: evidence hit rate 70%, Judge Score 0.84 |
| 🆕 Sandbox isolation | Process-level isolation, safer AI execution |
| 🔧 Tool enhancements | Hooks respond, MCP artifact, custom Headers |
| 💬 New channel | Teams Webhook |
| 🐛 Key fixes | WebSocket connection, gateway PID, Docker deployment |
| 🔩 Stability | 10+ bug fixes, FreeBSD/ARM compatibility improved |

This version marks the moment PicoClaw truly learned to "remember" —

Not just a jump in benchmark numbers, but the foundation for a continuous, memory-aware relationship between you and your AI

---

*PicoClaw — Lightweight, cross-platform, fast*

Website: picoclaw.io

GitHub: github.com/sipeed/picoclaw

Docs: docs.picoclaw.io

Discord: discord.gg/V4sAZ9XWpN
