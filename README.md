# ChatGPT Model Usage Monitor (Tampermonkey) / ChatGPT 使用量监控（油猴脚本）

A Tampermonkey userscript that monitors ChatGPT **model usage** by intercepting ChatGPT web requests and maintaining **bucketed counts** (GPT-5.x Auto/Instant, GPT-5.x Thinking, GPT-5.x Thinking Mini, GPT-4.x, o3, o4-mini).  
一个 Tampermonkey 用户脚本，通过拦截 ChatGPT 网页端请求统计**各模型用量**，并按“桶”展示（GPT-5.x Auto/Instant、GPT-5.x Thinking、GPT-5.x Thinking Mini、GPT-4.x、o3、o4-mini）。

> Note: This is a **local** counter based on requests observed in your browser. It is **not** an official quota source.  
> 注意：本脚本基于浏览器侧观测到的请求进行本地计数，**不是官方额度来源**，仅供参考。

---

## Features / 功能

### Core / 核心能力
- **Bucketed counters** with progress indicators (warning/danger thresholds).  
  **按桶计数**并提供进度条与告警阈值显示。
- **Rolling vs calendar windows** per bucket (3h rolling / daily / weekly calendar windows).  
  支持**滚动窗口**与**自然日/自然周**窗口展示（不同桶不同窗口策略）。
- **Status tracking**: dispatched / completed / failed (counts are recorded at dispatch).  
  记录请求状态（dispatched/completed/failed），并在 **dispatch 时计数**（失败/取消也会计入尝试次数）。
- **Analytics dashboard**: 7d / 30d overview, daily trend, bucket distribution, daily breakdown table.  
  **分析面板**：7/30 天概览、每日趋势、桶分布、每日明细表格。
- **Import/Export** usage data to JSON; **Clear** all local data.  
  支持**导入/导出 JSON**、一键**清空数据**。
- **Theme-aligned UI**: uses ChatGPT CSS tokens; supports dark mode.  
  UI 尽量对齐 ChatGPT 主题 Token，并支持深色模式。
- **i18n**: English / 中文, with auto-following ChatGPT language.  
  支持英文/中文，并可自动跟随 ChatGPT 页面语言。

### Quality-of-life / 体验优化
- **Inline mode**: if a model switcher button is found, a “Usage/用量” trigger is inserted near it and opens a popover.  
  **内联模式**：检测到模型切换按钮时，在其旁边插入“用量/Usage”按钮，弹出浮层面板。
- **Floating mode**: if no anchor is found, a draggable/resizable floating panel is shown.  
  **悬浮模式**：找不到锚点时，展示可拖拽/可缩放的悬浮面板。
- **Keyboard shortcuts**: `Ctrl/Cmd + I` toggle, `Esc` close.  
  快捷键：`Ctrl/Cmd + I` 开关面板，`Esc` 关闭。

---

## Installation / 安装

### Option A: Install from a userscript site (recommended) / 从脚本平台安装（推荐）
1. Install **Tampermonkey** in your browser.
2. Open the script page (e.g., Greasy Fork).
3. Click **Install**.

### Option B: Install manually / 手动安装
1. Install **Tampermonkey**.
2. Create a new script.
3. Paste the full userscript code.
4. Save and open `https://chatgpt.com/`.

---

## Usage / 使用方法

- Open `https://chatgpt.com/`.
- Click **Usage / 用量**:
  - In **inline mode**, the button appears next to the model switcher.
  - In **floating mode**, a minimized pill appears and can be expanded.
- Switch tabs:
  - **Usage / 用量**: live counters per bucket and reset timers.
  - **Analytics / 分析**: 7d / 30d overview and breakdown.
  - **Debug / 调试**: event logs (optional toggle).

### Menu commands (Tampermonkey) / 油猴菜单命令
- Reset position
- Export usage data
- Import usage data
- Clear usage data

---

## Buckets & Model Mapping / 桶与模型映射

The script maps observed `model` / `model_slug` to buckets using a predefined list (see `MODEL_BUCKET_MAP`).  
脚本将请求体中的 `model` / `model_slug` 映射到桶（详见 `MODEL_BUCKET_MAP`）。

Default buckets / 默认桶：
- GPT-5.x Auto/Instant
- GPT-5.x Thinking
- GPT-5.x Thinking Mini
- GPT-4.x
- o3
- o4-mini

> You can extend the mapping by adding new model identifiers into the corresponding list in `MODEL_BUCKET_MAP`.  
> 你可以通过修改 `MODEL_BUCKET_MAP` 为某个桶添加新的模型标识。

---

## Data & Storage / 数据与存储

- Data is stored **locally** via Tampermonkey storage (`GM_setValue` / `GM_getValue`).
- Retention: **45 days** (old records are periodically pruned).
- Export format: JSON snapshot of the internal state.

---

## Privacy / 隐私声明

- No data is uploaded by this script.
- All usage logs remain on your device (Tampermonkey storage).
- The script intercepts `fetch` calls in the page context to observe request metadata needed for counting.

> If you are uncomfortable with request interception, do not install this script.  
> 如果你不接受对页面请求的拦截统计，请不要安装此脚本。

---

## Compatibility / 兼容性

- Site: `https://chatgpt.com/*`
- Requires: Tampermonkey (or compatible userscript manager)
- The ChatGPT web app changes frequently; selectors may need updates.

---

## FAQ / 常见问题

### 1) Why does the count differ from actual quota? / 为什么统计与实际额度不一致？
This is an **unofficial** local counter. Retries, failures, cancellations, or backend changes may cause mismatches.  
这是**非官方**本地计数。重试、失败、取消、以及 ChatGPT 前端/后端变化都可能导致偏差。

### 2) Does it count failed messages? / 失败也计数吗？
Yes. A request is recorded at **dispatch** time; status is later updated to completed/failed when possible.  
是的。脚本在 **dispatch** 时就计数，并在后续根据响应更新状态。

### 3) How do I reset the UI position? / 如何重置位置？
Use Tampermonkey menu: **Reset position**.  
在油猴菜单中选择 **Reset position**。

---

## Development / 开发

- This project is a single userscript file.
- Main sections:
  - UI & styling (ChatGPT theme tokens)
  - Storage & migration
  - Bucket logic & analytics
  - `fetch` proxy interception and idempotency tracking

---

## License / 许可证

MIT License.

---

## Disclaimer / 免责声明

This project is not affiliated with OpenAI.  
This script provides best-effort estimates based on observed web requests. Use at your own risk.  
本项目与 OpenAI 无关；统计结果基于浏览器侧观测请求，仅为尽力估算，使用风险自担。
