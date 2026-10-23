# DMWipe

![platform](https://img.shields.io/badge/platform-Vencord-8A2BE2?style=flat-square)
![type](https://img.shields.io/badge/type-plugins/userplugins-blue?style=flat-square)
![version](https://img.shields.io/badge/version-1.2.0-green?style=flat-square)
![license](https://img.shields.io/badge/license-GPL--3.0--or--later-lightgrey?style=flat-square)

Bulk-delete every message in a Discord DM or group DM. Paces itself off Discord's own rate limit
headers, keeps whatever you tell it to keep, backs up before it deletes, and never lets a single
failed request end the run.

---

## Contents

- [Features](#features)
- [Install](#install)
- [Quick start](#quick-start)
- [Commands](#commands)
- [Context menu](#context-menu)
- [Status card](#status-card)
- [Pausing and cancelling](#pausing-and-cancelling)
- [Settings](#settings)
- [Filters](#filters)
- [How it works](#how-it-works)
- [Crash reports](#crash-reports)
- [Stats and the queue](#stats-and-the-queue)
- [Performance notes](#performance-notes)
- [Troubleshooting](#troubleshooting)
- [Limitations](#limitations)
- [License](#license)

---

## Features

**Deleting**

- Deletes every message in a DM, at any age. Yours, theirs, or a mix, your choice.
- Works in group DMs as well as 1:1 DMs.
- Individual REST deletes, so the two week bulk-delete window never applies.
- Uses the bulk endpoint automatically where Discord allows it, 100 messages per request.

**Pacing**

- Reads `X-RateLimit-Limit`, `X-RateLimit-Remaining` and `X-RateLimit-Reset-After` from every
  response and paces to exactly what your bucket allows. No guessing, no oscillation.
- Honours the server's own `retry_after` on every 429.
- Adjustable concurrency for pipelining, with a global rate limiter so raising it can never
  overshoot.

**Resilience**

- A failed request can never end a run. Passes restart themselves and keep sweeping until a full
  pass finds nothing left.
- Resume offer if your client dies mid-run.
- Crash reports filed automatically when a run ends abnormally, plus a manual send.

**Control**

- Live progress card with a bar, percentage, rate, elapsed time and ETA.
- Pause, resume and cancel from the chat, a notification, the context menu, or a command.
- Dry run mode that scans and reports without deleting anything.
- Filters: keep pinned, newest N, last N days, links, attachments, reactions, bot messages, or a
  regex.
- JSON backup to clipboard or file before anything is deleted.
- Multi-channel wipe queue.
- Lifetime stats with a per-run history.

---
## Local Installation

1. Clone Vencord and install dependencies.

   ```sh
   git clone https://github.com/Vendicated/Vencord
   cd Vencord
   pnpm install

<img width="1306" height="216" alt="image" src="https://github.com/user-attachments/assets/ac65b315-8b08-4f46-b614-50a66ad0fe72" />
<img width="386" height="108" alt="image" src="https://github.com/user-attachments/assets/a96855e0-b773-4ead-98c3-69b0fb5b5200" />
