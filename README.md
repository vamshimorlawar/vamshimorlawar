<h1 align="center">Vamshikiran Morlawar</h1>

<p align="center">
  <b>Full-stack engineer.</b> I ship small products end to end — build it, publish it, take the support emails, charge for it.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/India-FF9933?style=flat-square&logo=googlemaps&logoColor=white" alt="India">
  <img src="https://img.shields.io/badge/IIT%20Kanpur-004C8C?style=flat-square&logo=graduation-cap&logoColor=white" alt="IIT Kanpur">
  <img src="https://img.shields.io/badge/Open%20to-Full--stack%20%26%20Backend%20roles-2ea44f?style=flat-square" alt="Open to roles">
  <a href="mailto:vamshimorlawar@gmail.com"><img src="https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white" alt="Email"></a>
</p>

---

## 🚀 Shipped

Three products live and downloadable, built solo — store listings, privacy policies, payments and releases included.

<table>
<tr>
<td width="33%" valign="top">

### 🖥️ [DeskPilot](https://deskpilot-site.vercel.app/)

**Local AI agents for your filesystem**

Point it at a messy folder — it proposes a structure, you approve, it moves the files. One-click undo.

Runs on local `llama3.2` via Ollama. Nothing leaves your machine.

<img src="https://img.shields.io/badge/Tauri_2-24C8DB?style=flat-square&logo=tauri&logoColor=white"> <img src="https://img.shields.io/badge/Rust-000?style=flat-square&logo=rust"> <img src="https://img.shields.io/badge/Ollama-000?style=flat-square&logo=ollama&logoColor=white">

[Download](https://deskpilot-site.vercel.app/) · [Source](https://github.com/vamshimorlawar/deskpilot)

</td>
<td width="33%" valign="top">

### 📔 [My Diary](https://chromewebstore.google.com/detail/my-diary/nfdcipolchlmlipikekpbbmpdpienajm)

**Save what you read, with its source**

Select text anywhere, right-click, saved — with page title, URL, tags and your notes.

Free tier plus a paid Pro tier with Gumroad licence activation.

<img src="https://img.shields.io/badge/Chrome-4285F4?style=flat-square&logo=googlechrome&logoColor=white"> <img src="https://img.shields.io/badge/MV3-green?style=flat-square"> <img src="https://img.shields.io/badge/Gumroad-FF90E8?style=flat-square&logo=gumroad&logoColor=black">

[Install](https://chromewebstore.google.com/detail/my-diary/nfdcipolchlmlipikekpbbmpdpienajm) · [Source](https://github.com/vamshimorlawar/my-diary-extension)

</td>
<td width="33%" valign="top">

### ✍️ [Rephrase It](https://chromewebstore.google.com/detail/rephrase-it/cfpjlmhgebbmimbdkljdmoohcpnfoojk)

**Rewrite any text in 10 tones**

Select, right-click, pick a tone. Works in inputs and content-editable fields.

No backend. Your Gemini key stays in local storage.

<img src="https://img.shields.io/badge/Chrome-4285F4?style=flat-square&logo=googlechrome&logoColor=white"> <img src="https://img.shields.io/badge/Gemini-8E75B2?style=flat-square&logo=googlegemini&logoColor=white"> <img src="https://img.shields.io/badge/No_backend-555?style=flat-square">

[Install](https://chromewebstore.google.com/detail/rephrase-it/cfpjlmhgebbmimbdkljdmoohcpnfoojk) · [Source](https://github.com/vamshimorlawar/rephrase-extension)

</td>
</tr>
</table>

---

## 🔨 Currently building

### [bsewatch](https://github.com/vamshimorlawar/bsewatch) — BSE filings, the moment they land

<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white"> <img src="https://img.shields.io/badge/mypy-strict-blue?style=flat-square"> <img src="https://img.shields.io/badge/tests-91-2ea44f?style=flat-square"> <img src="https://img.shields.io/badge/ruff-clean-D7FF64?style=flat-square&logo=ruff&logoColor=black">

The hard part isn't scraping. It's staying alive against an undocumented API under a shared rate limit.

```mermaid
flowchart LR
    BSE[("BSE API<br/>~15 req/s shared")]

    subgraph engine ["Engine"]
        direction TB
        POLL["Poll<br/><i>interval scales with<br/>watchlist size</i>"]
        CB{"429?"}
        COOL["Global cooldown<br/><i>halt the whole tick</i>"]
        BREAK["Circuit breaker<br/><i>per scrip</i>"]
    end

    DEDUP[("INSERT OR IGNORE<br/>on (scrip, news_id)")]
    OUTBOX[("Transactional outbox<br/><i>retry + dead-letter</i>")]
    OUT["Telegram · Webhook · Console"]

    BSE --> POLL
    POLL --> CB
    CB -->|yes| COOL
    CB -->|"scrip fails 3x"| BREAK
    CB -->|ok| DEDUP
    DEDUP -->|"new only"| OUTBOX
    OUTBOX --> OUT

    style BSE fill:#1f6feb,stroke:#1f6feb,color:#fff
    style DEDUP fill:#8250df,stroke:#8250df,color:#fff
    style OUTBOX fill:#8250df,stroke:#8250df,color:#fff
    style COOL fill:#cf222e,stroke:#cf222e,color:#fff
    style BREAK fill:#bc4c00,stroke:#bc4c00,color:#fff
    style OUT fill:#1a7f37,stroke:#1a7f37,color:#fff
```

| Problem | Approach |
|---|---|
| Shared rate limit | Tick interval derived from watchlist size, not hardcoded |
| One bad symbol | Per-scrip circuit breaker after N consecutive failures |
| `429` — the problem is us | Halt the entire tick, start a global cooldown |
| Telegram goes down | Transactional outbox; filings are never lost to a delivery failure |
| Two ticks race | Dedup by primary key, not `SELECT`-then-`INSERT` |
| Fixed interval is a fingerprint | Off-hours polling jittered within a range |

Design rationale and the end-to-end latency budget: [ARCHITECTURE.md](https://github.com/vamshimorlawar/bsewatch/blob/main/ARCHITECTURE.md)

---

## 📊 By the numbers

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/stats-dark.svg">
    <img src="assets/stats-light.svg" alt="411 contributions in the past year, 3 products shipped and live, 47 repositories, 91 tests in bsewatch" width="100%">
  </picture>
</p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/languages-dark.svg">
    <img src="assets/languages-light.svg" alt="Language distribution across 47 repositories: TypeScript 49.5%, Python 16.0%, CSS 13.4%, HTML 8.3%, JavaScript 6.9%, TeX 3.1%, PHP 2.3%, Kotlin 0.5%" width="100%">
  </picture>
</p>

---

## 🧰 Stack

**Languages**

<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"> <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white"> <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black"> <img src="https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white"> <img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white"> <img src="https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white">

**Backend & data**

<img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white"> <img src="https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white"> <img src="https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white"> <img src="https://img.shields.io/badge/Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=white"> <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white"> <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white"> <img src="https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white">

**Frontend & desktop**

<img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black"> <img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white"> <img src="https://img.shields.io/badge/Tailwind-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white"> <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white"> <img src="https://img.shields.io/badge/Tauri-24C8DB?style=for-the-badge&logo=tauri&logoColor=white">

**Tooling**

<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white"> <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white"> <img src="https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white"> <img src="https://img.shields.io/badge/LaTeX-008080?style=for-the-badge&logo=latex&logoColor=white">

---

<p align="center">
  <a href="mailto:vamshimorlawar@gmail.com"><img src="https://img.shields.io/badge/Get%20in%20touch-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
</p>
