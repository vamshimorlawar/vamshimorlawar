### Vamshikiran Morlawar

Full-stack engineer. I ship small products end to end — build it, publish it, take the support emails, charge for it.

India · IIT Kanpur · Open to full-stack and backend roles

---

### Shipped

Three products live and downloadable, built solo — including the store listings, privacy policies, payments and release process.

#### [DeskPilot](https://deskpilot-site.vercel.app/) · macOS · [source](https://github.com/vamshimorlawar/deskpilot)
Local AI agents that clean up your filesystem. Point it at a messy folder and it proposes a structure, you approve it, and it moves the files — with one-click undo. Runs entirely on a local `llama3.2` via Ollama, so nothing leaves the machine and there's no subscription.

Built with Tauri 2 (Rust + React). Every filesystem mutation goes through a **plan → approve → execute → undo** cycle rather than acting directly, because an AI agent that reorganises your Documents folder needs to be reversible before it needs to be clever.

#### [My Diary](https://chromewebstore.google.com/detail/my-diary/nfdcipolchlmlipikekpbbmpdpienajm) · Chrome · [source](https://github.com/vamshimorlawar/my-diary-extension)
Save text snippets from any page with their source, notes and tags. Free tier plus a paid Pro tier with license-key activation through Gumroad.

#### [Rephrase It](https://chromewebstore.google.com/detail/rephrase-it/cfpjlmhgebbmimbdkljdmoohcpnfoojk) · Chrome · [source](https://github.com/vamshimorlawar/rephrase-extension)
Rewrite selected text in 10 tones using Gemini. The API key stays in local storage — no backend, no data collection, no account.

---

### Currently building

**[bsewatch](https://github.com/vamshimorlawar/bsewatch)** — a Python library and CLI that watches BSE corporate filings and alerts you the moment a company you follow announces something.

The hard part isn't the scraping, it's staying alive against an undocumented API under a shared rate limit:

- Tick interval scales with watchlist size to stay inside BSE's request budget
- Per-scrip circuit breaker for one bad symbol; global cooldown when a `429` means the problem is us
- Transactional outbox, so a Telegram outage can never lose an announcement
- Jittered off-hours polling — a fixed interval is a fingerprint
- Dedup enforced by the primary key rather than a read-then-write race

Design rationale and the end-to-end latency budget are in [ARCHITECTURE.md](https://github.com/vamshimorlawar/bsewatch/blob/main/ARCHITECTURE.md).

---

### Stack

**Languages** · Python · TypeScript · JavaScript · Rust · Java · Kotlin
**Backend** · Flask · Node · Express · Prisma · Ktor · SQLite · MySQL · Postgres
**Frontend** · React · Vite · Tailwind · shadcn/ui · Chrome Extensions (MV3)
**Desktop & infra** · Tauri · Ollama · Docker · GitHub Actions

---

[Email](mailto:vamshimorlawar@gmail.com)
