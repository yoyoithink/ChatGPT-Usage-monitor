ChatGPT Model Usage Monitor (Tampermonkey)

A Tampermonkey userscript that monitors ChatGPT model usage by intercepting ChatGPT web requests and maintaining bucketed usage counts (GPT-5.x Auto/Instant, GPT-5.x Thinking, GPT-5.x Thinking Mini, GPT-4.x, o3, o4-mini).

Note
This is a local, unofficial counter based on browser-observed requests.
It is not an official quota source and is for reference only.

Features
Core

Bucketed counters with progress bars and warning / danger thresholds.

Rolling vs. calendar windows per bucket (e.g. 3-hour rolling, daily, weekly).

Status tracking: dispatched / completed / failed
(counts are recorded at dispatch time).

Analytics dashboard:

7-day / 30-day overview

Daily usage trend

Bucket distribution

Daily breakdown table

Import / Export usage data (JSON).

Clear all locally stored data.

Theme-aligned UI using ChatGPT CSS tokens (dark mode supported).

i18n: English / Chinese, auto-following ChatGPT UI language.

Quality of Life

Inline mode
Inserts a “Usage” button next to the model switcher (when detected).

Floating mode
Draggable and resizable floating panel when no anchor is found.

Keyboard shortcuts

Ctrl / Cmd + I: toggle panel

Esc: close panel

Installation
Option A — Install from a userscript site (recommended)

Install Tampermonkey.

Open the script page (e.g. Greasy Fork).

Click Install.

Option B — Manual installation

Install Tampermonkey.

Create a new userscript.

Paste the full script code.

Save and open https://chatgpt.com/.

Usage

Open https://chatgpt.com/.

Click Usage:

Inline mode: button appears near the model selector.

Floating mode: minimized pill can be expanded.

Tabs:

Usage: live counters and reset timers

Analytics: 7d / 30d overview and breakdown

Debug: request event logs (optional)

Tampermonkey Menu Commands

Reset position

Export usage data

Import usage data

Clear usage data

Buckets & Model Mapping

Observed model / model_slug values are mapped into buckets via
MODEL_BUCKET_MAP.

Default buckets

GPT-5.x Auto / Instant

GPT-5.x Thinking

GPT-5.x Thinking Mini

GPT-4.x

o3

o4-mini

You can extend mappings by adding model identifiers to
MODEL_BUCKET_MAP.

Data & Storage

Stored locally only via Tampermonkey storage (GM_getValue / GM_setValue)

Retention: 45 days (older records are pruned)

Export format: JSON snapshot of internal state

Privacy

No data is uploaded.

All logs remain on your device.

The script intercepts fetch calls only to read metadata needed for counting.

If you are uncomfortable with request interception, do not install this script.

Compatibility

Site: https://chatgpt.com/*

Requires: Tampermonkey (or compatible manager)

ChatGPT UI changes frequently; selectors may require updates.

FAQ
Why does the count differ from my actual quota?

This is an unofficial local estimate. Retries, cancellations, failures, or UI/backend changes can cause discrepancies.

Are failed messages counted?

Yes. Requests are counted at dispatch time; status is updated later if possible.

How do I reset the panel position?

Use the Tampermonkey menu → Reset position.

Development

Single userscript file.

Main components:

UI & theming

Storage & migration

Bucket logic & analytics

fetch interception with idempotency handling

License

MIT License.

Disclaimer

This project is not affiliated with OpenAI.
All statistics are best-effort estimates based on observed browser requests.
Use at your own risk.
