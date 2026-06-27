---
title: Self-Hosted Services
nav_order: 5
---

# Self-Hosted Business Services ｜ 自架商業服務
{: .no_toc }

<details open markdown="block">
  <summary>On this page ｜ 本頁</summary>
- TOC
{:toc}
</details>

A fleet of off-the-shelf open-source platforms, self-hosted and integrated
instead of bought as SaaS. Each entry is *what kind of application* it is plus
*its stack and database*.

一整批 off-the-shelf 開源平台，選擇自架整合而非買 SaaS。每一筆都標明*它是什麼類型的
應用*，加上*它的技術棧與資料庫*。

## Services ｜ 服務一覽

| Service ｜ 服務 | Category ｜ 類型 | Stack / Database ｜ 技術棧／資料庫 |
|---|---|---|
| **Snipe-IT** | IT asset management ｜ IT 資產管理 | PHP (Laravel) · MySQL |
| **Moodle** | Learning management (LMS) ｜ 學習管理 | PHP · MySQL |
| **iTop** | IT service management (ITSM) ｜ IT 服務管理 | PHP · MySQL |
| **OpenProject** | Project management ｜ 專案管理 | Ruby on Rails · PostgreSQL |
| **Metabase** | Business intelligence / dashboards ｜ BI／儀表板 | JVM · MySQL (read-only reporting user) |
| **NocoDB** | Airtable-alternative / no-code DB ｜ Airtable 替代 | Node · PostgreSQL + MinIO (attachments) |
| **Nocobase** | Low-code application platform ｜ 低代碼平台 | Node · PostgreSQL |
| **InvenTree** | Parts inventory ｜ 零件庫存 | Python (Django) · SQLite |
| **Radicale** | CalDAV / CardDAV (calendars & contacts) ｜ 行事曆／聯絡人 | Python · file-based store |
| **RustDesk** | Self-hosted remote-desktop relay ｜ 自架遠端桌面中繼 | Rust (relay + rendezvous) |

## Patterns worth noting ｜ 值得一提的模式

- **Database by ecosystem.** The PHP/Laravel apps land on **MySQL**; the
  Rails/Node apps land on **PostgreSQL**; small single-user tools stay on
  **SQLite**. The database choice follows each app's native ecosystem rather
  than forcing one engine everywhere.
  <br>**資料庫看生態系。** PHP/Laravel 系落在 **MySQL**；Rails/Node 系落在
  **PostgreSQL**；小型單人工具用 **SQLite**。資料庫的選擇順著每個應用的原生生態系，
  而不是硬把所有東西塞進同一個引擎。
- **Object storage split.** The no-code DB keeps *metadata* in PostgreSQL but
  *attachments* in **MinIO** — so a complete restore means mirroring both, a
  detail that's easy to miss. ｜ **物件儲存分離。** 無代碼資料庫的*中繼資料*放
  PostgreSQL、*附件*放 **MinIO**——所以完整復原得同時鏡像兩邊，這個細節很容易漏掉。
- **Co-tenancy.** Several lightweight services (remote-desktop relay, inventory,
  CalDAV) share a single host to save resources. ｜ **共置。** 幾個輕量服務
  （遠端桌面中繼、庫存、CalDAV）共用一台主機以節省資源。
- **Staging mirrors.** Asset management runs a QA/staging twin alongside
  production for safe upgrades. ｜ **預備鏡像。** 資產管理在正式環境旁跑一套 QA／預備
  雙生環境，讓升級更安全。

How these are backed up is covered in [Data & Backup](data-and-backup.html);
how they're watched is in [Observability](observability.html).

它們怎麼備份見 [資料與備份](data-and-backup.html)；怎麼被監看見
[可觀測性](observability.html)。
