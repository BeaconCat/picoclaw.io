---
title: "PicoClaw v0.2.7 — Auth Overhaul, AI Runs More Reliably"
description: "Unified authentication across Launcher, Dashboard, and Gateway; AI execution pipeline rewritten; native Gemini provider; Feishu group chat, Android APK, and launcher sync update"
date: 2026-04-22
tags: ["Release", "New Features"]
lang: en
author: PicoClaw Team
slug: v027-release
---

**April 22, 2026**  The PicoClaw team is releasing v0.2.7

This version overhauls authentication across the board, rewrites the AI execution pipeline internally, and adds native Gemini support
Plus new features like Feishu group chat, Android APK, and more

---

## 1. UI Updates

### Tool Page Redesign

The old tool page is now split into two tabs: **"Tool Library"** and **"Web Search Settings"** — easier to find what you need

![Tool page redesign](../../../assets/blog/v027-release/toolspage.png)

### Code Highlighting

Code blocks in chat and skills now have **syntax highlighting** — much easier on the eyes

![Code highlighting](../../../assets/blog/v027-release/code.png)

### Other Improvements

- Disabled input boxes now tell you **why** they're disabled — no more mysterious grayed-out state
- Chat history restoration is more stable, attachment display fixed
- Channel configuration supports **list editing** — configuring multiple instances per channel is easier

![Other improvements](../../../assets/blog/v027-release/message.png)

---

## 2. Better Context Management

Last version added the Seahorse memory engine — this time we kept polishing

- **`/context` command** — check how many tokens the current conversation has used, plus a **usage ring indicator** on the UI so you always know your remaining quota
- **`/clear` upgrade** — now clears not just chat history but also Seahorse's short-term memory

![Clear command](../../../assets/blog/v027-release/clear.png)

- **`/btw` aside** — drop a side comment mid-conversation without derailing the AI's understanding of the main topic

![Btw command](../../../assets/blog/v027-release/btw.png)

---

## 3. Auth Overhaul

We unified and streamlined all authentication flows in this release

### Launcher Auth

Now follows a clean **login → initialize → logout** flow
Also supports **browserless OAuth login** — works on headless servers without a desktop

### Dashboard Auth

The web dashboard switched from Token-based auth to **password login** — just like any normal website

### Gateway Connection

Gateway verification simplified from requiring both PID and Token to just **Token** — much simpler configuration

---

## 4. AI Execution Pipeline Rewrite

Users won't notice any change, but this was a major engineering effort

The core AI execution logic used to be crammed into a single 4,000+ line file — now it's split into over a dozen small files, each handling one thing
The entire execution flow was reorganized for clarity

In short: **the way AI works hasn't changed, but the code is far more maintainable, and adding new features will be faster**

---

## 5. Native Gemini Support

Previously Gemini was supported through a compatibility layer — now it gets **native integration**

- **Thinking and response displayed separately** — you can now see what Gemini is "thinking" vs. what it "says"
- Pro model special requirements handled correctly
- Tool call IDs no longer get mixed up
- Documentation added

---

## 6. Platforms & Channels

**Feishu group chat** — group chat triggers now supported, with configurable random emoji reactions

**Android APK** — starting from this version, the Release page provides Android arm64 packages directly — no more building from source

**Launcher sync update (picoclaw_fui v0.1.3)** — the Flutter client is updated alongside the main release:

- Auth integration — embedded core upgraded to v0.26 nightly with auth login flow
- About page — version info display (App version + Core version), multi-language support
- Settings improvements — save confirmation dialog, language selector, auto-restart after save
- Storage permission fix — resolved Android Q+ SELinux errno 13 crash on some devices
- Light theme fix — settings text no longer invisible on light (Sakura) theme
- Log export — export button changed from icon-only to text button
- macOS WebView — native macOS WebView support, system tray close no longer exits
- CI/CD — nightly/testly auto-builds, APK auto-upload to VolcEngine TOS

**MCP tool hot reload** — previously MCP tools would disappear after config reload, now fixed

**Image send fix** — sending images to models that don't support them no longer freezes — automatically recovers and continues

---

## 7. Stability Fixes

**Tool calls no longer get mixed up** — tool call IDs in multi-turn conversations now stay consistent

**Scheduled tasks no longer interfere** — each scheduled task now runs in its own session, task A won't affect task B

**Network error fallback** — timeouts, connection failures, and other network issues now automatically try backup options

---

## 8. Engineering Improvements

- CI build tooling switched to pnpm/action-setup, install steps updated accordingly
- Release process split into tag creation and publish — more flexible
- Code directory restructured
- Documentation reorganized by type and language, session and routing docs added
- 15+ frontend/backend dependency upgrades (React 19.2.5, shadcn 4.2.0, SQLite 1.48.2, etc.)

---

## Summary

| Category | Update |
|----------|--------|
| 🎨 UI | Tool page redesign, code highlighting, disabled reason prompt |
| 🧠 Context | `/context` usage ring, `/clear` clears memory, `/btw` aside |
| 🔐 Auth overhaul | Launcher unified flow, Dashboard password login, Gateway Token-only |
| ⚙️ Internal rewrite | AI execution pipeline split and reorganized |
| 🤖 Gemini | Native support, thinking/response separated |
| 📱 Platforms | Android APK/launcher, Feishu group chat, MCP hot reload fix |
| 🔧 Stability | Tool call consistency, scheduled task isolation, image send fix |

The biggest changes in this version: **auth flows fully unified, AI execution engine split and reorganized, native Gemini support**
Login is smoother, AI runs more reliably, and the interface is better — in short, everything that needed fixing got fixed

---

*PicoClaw — Lightweight, cross-platform, fast*

Website: picoclaw.io

GitHub: github.com/sipeed/picoclaw

Docs: docs.picoclaw.io

Discord: discord.gg/V4sAZ9XWpN
