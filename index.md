---
title: Home
nav_order: 1
description: Overview of a one-person-operated, self-hosted enterprise IT infrastructure.
---

# Self-Hosted Enterprise IT Infrastructure
{: .no_toc }
## 自架企業 IT 基礎架構
{: .no_toc .text-delta }

A single-handedly built and operated IT infrastructure for a manufacturing
enterprise — from the virtualization layer up through application hosting,
self-hosted business services, backup, observability, and an on-prem AI/RAG
stack.

一座由一人從零打造並維運的企業 IT 基礎架構（製造業）——從虛擬化層，往上到應用主機、
自架商業服務、備份、可觀測性，以及地端 AI/RAG 棧。

This site is a **technology-selection showcase**: for each part of the stack,
*what kind of system it is* and *what architecture / technology combination
powers it* — with no internal addresses, hostnames, or product branding.

本站是一份**技術選型展示**：針對每一塊，講清楚*它是什麼類型的系統*、以及*用了什麼
架構／技術組合*——不揭露任何內部位址、主機名或產品品牌。

---

## At a glance ｜ 規模一覽
{: .no_toc }

- **2** Proxmox VE nodes (KVM + LXC), one with GPU passthrough for AI inference
  <br>**2** 台 Proxmox VE（KVM + LXC），其中一台 GPU passthrough 供 AI 推論
- **~10** Dockerized application & service hosts
  <br>約 **10** 台容器化的應用／服務主機
- **3** Synology NAS units (backup destination + capacity)
  <br>**3** 台 Synology NAS（備份目的地 + 容量）
- **12+** self-hosted business services (asset mgmt, LMS, ITSM, BI, PM, low-code…)
  <br>**12+** 個自架商業服務（資產管理、LMS、ITSM、BI、專案管理、低代碼…）
- **Dual monitoring** — active polling + passive dead-man's-switch, pushed to phone
  <br>**雙層監控**——主動輪詢 + 被動 dead-man's-switch，推播到手機
- **On-prem RAG** — self-hosted embedding + vector search + local & API LLMs
  <br>**地端 RAG**——自架 embedding + 向量檢索 + 本地與 API LLM

---

## Platform pillars ｜ 平台支柱
{: .no_toc }

| Pillar ｜ 支柱 | Technology ｜ 技術 |
|---|---|
| Virtualization ｜ 虛擬化 | Proxmox VE 9.2 (KVM VMs + LXC), ZFS, GPU passthrough |
| Containerization ｜ 容器化 | Docker / Compose, Traefik reverse proxy, Watchtower, Portainer |
| Custom tooling ｜ 自寫工具 | FastAPI + Next.js fleet-admin app, Go status HUD, Python bridges |
| Data ｜ 資料 | PostgreSQL · MySQL · SQLite |
| Backup ｜ 備份 | Per-service dump orchestration → Synology, dead-man's-switch verified |
| Observability ｜ 可觀測性 | Nagios (active) + Healthchecks (passive) + ntfy + Zulip + Cloudflare Tunnel |
| AI / RAG | Onyx, Vespa / OpenSearch, Ollama, Claude API |

---

## Technology → where it's used ｜ 技術用在哪
{: .no_toc }

A cross-reference of the recurring technologies and the categories that lean on
them. ｜ 一張交叉表，列出反覆出現的技術、以及哪些類別倚賴它。

| Technology ｜ 技術 | Used in ｜ 用在 |
|---|---|
| Docker / Compose | nearly every application & service host ｜ 幾乎每台應用／服務主機 |
| Proxmox VE (KVM + LXC) | the virtualization layer, 2 nodes ｜ 虛擬化層，2 節點 |
| PostgreSQL | OT platform, project mgmt, low-code, Airtable-alternative, RAG ｜ OT 平台、專案管理、低代碼、Airtable 替代、RAG |
| MySQL | asset management, LMS, ITSM, BI ｜ 資產管理、LMS、ITSM、BI |
| SQLite | fleet-admin app, inventory, monitoring ｜ 維運平台、庫存、監控 |
| Next.js / React | OT platform, fleet-admin UI ｜ OT 平台、維運平台 UI |
| FastAPI (Python) | fleet-admin backend, automation tooling ｜ 維運後端、自動化工具 |
| Go | deployment status HUD ｜ 部署狀態 HUD |
| Traefik / Watchtower | reverse proxy & auto-update for containers ｜ 容器反代與自動更新 |
| Synology DSM | backup storage (NAS) ｜ 備份儲存（NAS） |
| Nagios / Healthchecks / ntfy / Zulip | observability & alerting ｜ 監控與告警 |
| Postfix (LXC) | SMTP relay ｜ 郵件中繼 |
| Onyx / Vespa / OpenSearch / Ollama | self-hosted RAG / AI inference ｜ 自架 RAG／AI 推論 |
| Cloudflare Tunnel | secure push ingress ｜ 安全推播入口 |

---

Use the navigation on the left to explore each layer of the stack.
左側導覽可逐層瀏覽整座技術棧。

*Built & operated by **Eddie Su**.*
