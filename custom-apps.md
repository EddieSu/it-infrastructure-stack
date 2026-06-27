---
title: Custom-Built Applications
nav_order: 4
---

# Custom-Built Applications ｜ 自寫應用
{: .no_toc }

<details open markdown="block">
  <summary>On this page ｜ 本頁</summary>
- TOC
{:toc}
</details>

In-house software, built from scratch to run the infrastructure itself — the
parts where off-the-shelf tools didn't fit.

為了維運這座基礎架構而從零打造的自寫軟體——那些 off-the-shelf 工具搆不到的地方。

## Server Fleet Admin Platform ｜ 伺服器車隊維運平台

A web app to operate a fleet of Linux servers over SSH: server inventory,
asset & change logs, SSH-key provisioning, and backup orchestration — a single
pane of glass for one admin running many machines.

一個透過 SSH 操作整支 Linux 伺服器車隊的 Web app：伺服器清單、資產與異動日誌、
SSH 金鑰佈署、備份編排——讓一位管理員用單一面板掌握多台機器。

- **Backend** ｜ 後端: FastAPI (Python 3.12, async), SQLAlchemy 2.0,
  asyncssh (pooled SSH connections), APScheduler, Alembic
- **Frontend** ｜ 前端: Next.js 16, React 19, TypeScript, Tailwind v4, shadcn/ui
- **Data** ｜ 資料: SQLite for dynamic state + YAML for static SSH config
  (a deliberate hybrid config model) ｜ SQLite 存動態狀態 + YAML 存靜態 SSH 設定
  （刻意的混合設定模型）
- **Delivery** ｜ 交付: `git push` → post-receive hook → `docker compose`
  build & deploy

> **Pattern ｜ 模式:** an async SSH connection *pool* keeps long-lived sessions
> to each host, so fleet-wide operations and scheduled jobs run without
> re-handshaking every time. ｜ 用非同步 SSH *連線池*對每台主機維持長連線，
> 讓全車隊操作與排程工作不必每次重新握手。

## Deployment Status HUD ｜ 部署狀態 HUD

A single-binary **Go** service that renders a live deployment "video wall": a
status matrix across the DEV → DEV2 → PROD chain plus TCP liveness probes. Zero
external dependencies; an always-on-top pinned card gives at-a-glance state
without watching a terminal.

一支單一 binary 的 **Go** 服務，呈現即時的部署「監控牆」：一張橫跨 DEV → DEV2 → PROD
的狀態矩陣，外加 TCP 存活探測。零外部相依；一張置頂釘選卡片讓你一眼掌握狀態，不必盯著
終端機。

- **Why Go** ｜ 為何用 Go: one static binary, no runtime to install, trivial to
  drop onto any host. ｜ 一支靜態 binary、不必裝 runtime、丟到任何主機都簡單。
- Deploy scripts report in with one line: `report --project … --status …`.
  <br>部署腳本一行回報：`report --project … --status …`。

## Notification Bridges ｜ 通知橋接

Small **Python** glue services that turn platform events into phone push:

幾支小型 **Python** 黏合服務，把平台事件轉成手機推播：

- a **chat → push** bridge (long-polls a chat events API, forwards mentions &
  DMs) ｜ **聊天 → 推播**橋（long-poll 聊天事件 API，轉發提及與私訊）
- a **wiki change-log** poller (new wiki docs → a team channel) ｜ **wiki 變更
  日誌**輪詢器（新文件 → 團隊頻道）
- a **backup-status** bridge (APScheduler reads backup summaries on a schedule)
  ｜ **備份狀態**橋（APScheduler 定時讀備份摘要）

> **Pattern ｜ 模式:** events in, push out. Each bridge is tiny, single-purpose,
> and runs beside the other containers on the build host. ｜ 事件進、推播出。
> 每支橋都很小、單一職責，與其他容器並列跑在 build 主機上。

## Manufacturing OT Platform ｜ 製造 OT 平台

A shop-floor operational-technology web platform for the factory floor.

一個給廠房現場用的製造端（OT）作業平台。

- **Stack** ｜ 技術棧: Payload CMS (headless, Node) + Next.js front end + PostgreSQL
- **Runtime** ｜ 執行: Docker behind Traefik, on a KVM virtual machine
- **Lifecycle** ｜ 生命週期: promoted through the DEV → DEV2 → PROD chain

> Described by architecture and application type only — no brand, no URL.
> 僅以架構與應用類型描述——不含品牌、不含網址。

## Internal Process Tooling ｜ 內部流程工具

Lightweight **Streamlit** (Python) tools for data import and automation against
internal admin APIs — quick to build, easy to hand to a non-developer.

輕量的 **Streamlit**（Python）工具，用於資料匯入與針對內部 admin API 的自動化——
做得快、也容易交給非開發者使用。
