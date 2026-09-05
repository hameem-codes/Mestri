# ◉ Mestri

### **A quiet signal for noisy AI infrastructure.**

Mestri is an **AI service monitoring platform** that tracks the health of major AI providers in one place — turning scattered status pages and incident feeds into a single, consistent signal.

<p align="center">

**[🌐 Live Dashboard](https://mestri.mestri.workers.dev/)** · **[💻 GitHub](https://github.com/sadiyasyed28/Mestri)**

</p>

---

## 👀 What is Mestri?

AI applications depend on a growing stack of external providers.

When one of them slows down, degrades, or goes offline, you need to know **what changed — and when**.

Mestri continuously collects provider status information and turns it into:

`STATUS` → `HISTORY` → `INCIDENTS` → `SIGNALS`

No jumping between a dozen status pages.

---

## ⚡ What it does

|    | Capability                                                                    |
| -- | ----------------------------------------------------------------------------- |
| 🟢 | **Live Provider Status** — Monitor operational, degraded, and outage states   |
| 📈 | **30-Day History** — Visualize provider health over time                      |
| 🚨 | **Incident Tracking** — Preserve incidents and their updates                  |
| 🔄 | **State Transitions** — Detect when a provider changes status                 |
| 🔔 | **Webhooks** — Push status-change events to your systems                      |
| 📡 | **RSS Feeds** — Subscribe to all incidents or a specific provider             |
| 🧩 | **Embeddable Status** — Drop a lightweight status indicator into another site |
| 🔌 | **JSON API** — Consume normalized status and incident data programmatically   |

---

## 🧠 The interesting part

Different providers expose status information in completely different ways.

Mestri normalizes them into one common model:

```text
 OpenAI ───────┐
 Anthropic ────┤
 xAI ──────────┤
 Google ───────┤
 Mistral ──────┤
 Cohere ───────┤
 Hugging Face ─┤
 Replicate ────┤
 DeepSeek ─────┤
 ElevenLabs ───┤
               ▼
        ┌───────────────┐
        │    MESTRI     │
        │  Normalize    │
        │  Store        │
        │  Detect       │
        │  Signal       │
        └───────┬───────┘
                ▼
      Dashboard / API / RSS
                │
                ▼
            Webhooks
```

Each provider can use its appropriate source adapter — including **Statuspage, RSS, Instatus, Google Cloud, or manual mode**.

---

## 🔎 Providers

Mestri currently has provider definitions for:

**OpenAI · Anthropic · xAI · Google · Mistral · Cohere · Hugging Face · Replicate · Groq · Perplexity · DeepSeek · ElevenLabs**.

Some providers use live feeds while others are explicitly marked **manual** when a browser-readable public feed isn't available.

---

## 🔄 How monitoring works

```text
        Provider Feed
             ↓
       Fetch Snapshot
             ↓
       Normalize Status
             ↓
       Compare Previous
             ↓
      ┌──────┴──────┐
      │             │
   No change      Changed
      │             │
      ↓             ↓
   Store          Record
   snapshot      transition
                    │
                    ↓
                Notify
```

The scheduled monitoring cycle checks active providers, persists successful snapshots, detects state transitions, and triggers subscribed webhook notifications when a change occurs.

---

## 🛠️ Built with

**Frontend**

`React 19` · `TypeScript` · `Vite` · `Tailwind CSS`

**Backend / Edge**

`Cloudflare Workers` · `Cloudflare D1` · `Wrangler`

**Tooling**

`Vitest` · `ESBuild` · `Prettier`

The project is packaged and run with **pnpm**.

---

## 📡 API at a glance

```http
GET  /api/status
GET  /api/incidents
GET  /api/incidents/:id
POST /api/notifications
```

There are also machine-readable content surfaces:

```http
GET /api/feeds/all.xml
GET /api/feeds/:provider.xml
GET /sitemap.xml
GET /robots.txt
```

And lightweight embeddable status pages:

```http
GET /embed/:provider
```

These routes are implemented directly by the Cloudflare Worker.

---

## 🔔 Notifications

Mestri supports subscriptions for provider events through:

**Webhook** → JSON payload delivered when provider status changes.

The worker validates webhook destinations and blocks unsafe targets such as localhost and private/internal IP ranges.

> Email subscriptions are represented in the system, but actual email delivery is currently a stub.

---

## 🚀 Run locally

```bash
git clone https://github.com/sadiyasyed28/Mestri.git
cd Mestri

pnpm install
pnpm dev
```

For the Cloudflare Worker:

```bash
pnpm worker:dev
```

Useful commands:

```bash
pnpm build
pnpm check
pnpm test
pnpm format
```

---

## 🌐 Try it

### Live

**https://mestri.mestri.workers.dev/**


---

## ✦ Philosophy

> **AI infrastructure shouldn't be a black box.**

Mestri is designed to make infrastructure health **visible, queryable, and easy to integrate** — whether you're looking at a dashboard, consuming an API, subscribing to an RSS feed, or wiring alerts into another system.

### One signal. Many providers. Less noise.


