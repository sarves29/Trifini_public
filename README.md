<p align="center">
  <img src="assets/brand/trifini-emblem.png" alt="Trifini logo" width="220">
</p>

<h1 align="center">Trifini</h1>

<h3 align="center">The AI life coach that actually knows you.</h3>

<p align="center">
  <a href="https://trifini.com"><b>trifini.com</b></a> &nbsp;|&nbsp;
  <a href="docs/features.md">Features</a> &nbsp;|&nbsp;
  <a href="docs/architecture.md">Architecture</a> &nbsp;|&nbsp;
  <a href="docs/robo-pet.md">Robo Pet</a> &nbsp;|&nbsp;
  <a href="docs/roadmap.md">Roadmap</a>
</p>

> **Showcase repository.** Trifini's source code is private. This repository documents the product, its architecture and the engineering behind it. It was designed, built and shipped end to end by one engineer, [Sarvesvara Ramar](#built-by).

---

## What is Trifini?

Everyone has access to an AI that can give advice. Almost nobody has one that knows *them*.

Trifini is a **personal life operating system built around an AI coach**. You talk to it for two minutes in the morning and about ninety seconds at night. It remembers your moods, money, habits and sleep, and because all of that lives in one place it notices what separate apps and generic chatbots cannot: that spending climbs when work stress does, that Thursdays are always hard, that you are closer to a goal than it feels.

It replaces a drawer full of disconnected apps (budgeting, habit tracking, mood journal, sleep tracker, to-do and automation tools, a chatbot) with a single product on a shared data model, a shared event bus and a shared memory layer.

- **Coach first.** The AI coach is the narrator; every module feeds it or expresses it.
- **Four domains, one thread.** Mind, Body, Money, Habits, all in one conversation.
- **India first, globally usable.** Priced in ₹, GST-aware billing, localised in 14 languages.
- **Private by design.** Local-model option for embeddings and inference, consent before any AI action, user-held delete and export.
- **Safety is never paywalled.** Crisis screening runs on every free-text surface.
- **A companion, not just an app.** A virtual pet on web and mobile, and a physical desk robot in development.

Live at **[trifini.com](https://trifini.com)**.

## Screenshots

Dark theme (the product default). A [light theme](assets/screenshots/light/) is available too.

| | |
|---|---|
| ![Dashboard](assets/screenshots/dark/dashboard.png)<br>**Dashboard**: balance score, streaks, schedule and quick logging | ![AI Coach](assets/screenshots/dark/ai-coach-chat.png)<br>**AI Coach**: personalised routine and savings guidance |
| ![Mind](assets/screenshots/dark/mood.png)<br>**Mind**: mood tracking with year-in-pixels | ![Body](assets/screenshots/dark/health-sleep.png)<br>**Body**: sleep quality, stress, energy and breathing tools |
| ![Money](assets/screenshots/dark/finance.png)<br>**Money**: net worth, budgets, accounts and smart insights | ![Habits and routines](assets/screenshots/dark/habits-routines.png)<br>**Habits and routines**: streaks and completion tracking |
| ![Quests, XP and leagues](assets/screenshots/dark/gamification.png)<br>**Quests, XP and leagues**: levels, daily and weekly quests, weekly leagues | ![Robo Pet](assets/screenshots/dark/robo-pet.png)<br>**Robo Pet**: a companion that mirrors your real life |
| ![Plans](assets/screenshots/dark/pricing.png)<br>**Plans**: Free to Premium, plus a Student plan | ![Mobile](assets/screenshots/dark/mobile-dashboard.png)<br>**Mobile**: responsive dashboard |

<details>
<summary>Light theme gallery</summary>

![Dashboard (light)](assets/screenshots/light/dashboard.png)
![AI Coach (light)](assets/screenshots/light/ai-coach-chat.png)
![Mind (light)](assets/screenshots/light/mood.png)
![Body (light)](assets/screenshots/light/health-sleep.png)
![Money (light)](assets/screenshots/light/finance.png)
![Habits and routines (light)](assets/screenshots/light/habits-routines.png)
![Quests, XP and leagues (light)](assets/screenshots/light/gamification.png)
![Robo Pet (light)](assets/screenshots/light/robo-pet.png)
![Plans (light)](assets/screenshots/light/pricing.png)
![Mobile (light)](assets/screenshots/light/mobile-dashboard.png)

</details>

*Screenshots are from a demo account with sample data.*

## Feature tour

Full detail in [docs/features.md](docs/features.md).

| Area | Highlights |
|---|---|
| **AI Life Coach** | Proactive morning and evening check-ins, free-tier daily conversation, personas, context-aware answers that can also *take actions* (log a mood, complete a routine) with consent |
| **Mind** | 144-emotion grid, year-in-pixels, journal, gratitude, stress tracking, morning intentions and evening reflections, therapist-ready export |
| **Body** | Sleep score, energy, wearables and Google Fit integration, burnout-risk view, breathing exercises, diet and physical tracking |
| **Money** | Accounts, budgets, net worth, goals, FIRE calculator, tax insights, CSV import, broker imports, live prices, family finance, mood-to-spending correlation |
| **Habits and routines** | Routines, habits and tasks with a habit-strength algorithm, templates, groups, completion history |
| **Gamification** | XP and levels, daily and weekly quests, Duolingo-style leagues (Bronze to Diamond), purchasable streak freezes, grace-period logging |
| **Social** | Friends, groups, celebrations, Strava-style reactions |
| **Automations** | If-this-then-that rules, scheduling, reminders with one-tap buttons, AI *proposals* the user approves before anything runs |
| **Memory (RAG)** | The coach retrieves from *your own* history using vector search, so advice cites what actually worked for you |
| **Voice** | Speech-to-text and text-to-speech across 12 languages |
| **Offline and sync** | Installable web app, offline mode, conflict-free multi-device sync (CRDT) |
| **14 languages** | Fully localised interface |
| **Robo Pet** | Virtual pet whose mood, energy and bond reflect your real habits; a physical desk companion on a custom SG2002-based board in development. See [docs/robo-pet.md](docs/robo-pet.md) |
| **Safety** | Crisis-language screening on every free-text input, resources surfaced without blocking the user, human alerting, guardrails on every AI response |
| **Channels** | Web, Flutter app (web and Android), Telegram bot, voice, MCP server for external AI agents |

## Architecture at a glance

```mermaid
flowchart LR
    subgraph Clients
        W[Web app]
        F[Flutter app<br/>web + Android]
        T[Telegram bot]
        V[Voice]
        R[Robo Pet<br/>virtual + physical]
        M[MCP server]
    end

    subgraph Backend["Django backend"]
        API[REST + WebSocket APIs]
        AREAS[Life-area modules<br/>mood, health, finance, habits, ...]
        ENG[Engines<br/>automation, reminders, gamification, social]
        INTEL[Intelligence<br/>coach, RAG, observations, proposals]
        SAFE[Safety + policy layer]
    end

    subgraph Data
        PG[(PostgreSQL<br/>+ pgvector)]
        RD[(Redis<br/>cache, queues, channels)]
    end

    subgraph AI["AI providers"]
        CL[Cloud LLMs]
        OL[Local models<br/>Ollama]
    end

    Clients --> API
    API --> SAFE --> INTEL
    INTEL <--> AI
    INTEL <--> PG
    AREAS <--> PG
    ENG <--> RD
    AREAS -- events --> INTEL
    INTEL -- proposals --> ENG
    ENG -- actions --> AREAS
```

Deeper walkthrough: [docs/architecture.md](docs/architecture.md).

## Tech stack

| Layer | Technology |
|---|---|
| Backend | Python, Django, Django REST, Channels (ASGI/WebSockets), Celery |
| Database | PostgreSQL with pgvector for semantic memory |
| Cache / queues | Redis |
| Web | Server-rendered Django templates, PWA with service worker, offline support |
| Mobile and app | Flutter (web first, Android second, iOS scaffolded), ~90K lines of Dart |
| AI | Provider factory with complexity-based routing across cloud LLMs, with a fully local path via Ollama; local embedding models |
| Voice | Whisper (speech-to-text), ElevenLabs (text-to-speech) |
| Payments | Razorpay subscriptions, GST-aware invoicing |
| Messaging | Telegram bot, web push and mobile push |
| Feature management | GrowthBook feature flags and kill switches |
| Agent interop | Model Context Protocol (MCP) server |
| Hardware | Custom SG2002-based PCB for the desk companion, enclosure design, embedded firmware |
| Quality | Playwright end-to-end tests, Lighthouse and axe audits, mypy, pre-commit hooks, CI pipelines |

## Plans

All prices in ₹ and inclusive of taxes. Annual billing saves roughly 40%.

| Plan | Price | What you get |
|---|---|---|
| **Free** | ₹0 | 5 routines, 3 reminders/day, AI chat (10/day), mood journal |
| **Basic** | ₹99 / month | 10 routines, 20 reminders/day, AI chat (20/day), data export |
| **Pro** (most popular) | ₹299 / month | Unlimited routines and reminders, AI chat (100/day), AI reports, analytics, data export |
| **Premium** | ₹499 / month | Everything in Pro plus Robot Companion, Watch app and unlimited AI |
| **Student Pro** | ₹49 / month | All Pro features at 83% off with a college ID |

## Engineering highlights

Trifini is a production system, not a prototype.

- **Scale of the codebase:** 38 Django apps, roughly 280 data models and ~890 URL endpoints, ~250K lines of Python and ~90K lines of Dart.
- **Test depth:** 2,500+ automated tests across unit, API, end-to-end (Playwright) and mobile layers.
- **Compliance matrix:** a 142-column "every rule x every module" scoreboard tracks engineering standards (error contracts, observability events, feature gating, accessibility, performance budgets, resilience). Gates are enforced, not decorative.
- **CI and pre-push gates:** type-checking, leak scanning, linting, coverage and audit gates run before code ships.
- **Consistent contracts:** one uniform error envelope across every module, one event bus (`emit-on-every-action`) feeding the intelligence layer, one canonical write path shared by the UI and the AI.
- **Resilience:** retries and circuit breakers around every external call; provider fallbacks so the coach degrades gracefully.
- **Safety by construction:** a fail-closed policy engine gates anything the AI tries to *do*, and crisis screening is a shared invariant across all free-text surfaces.
- **Performance work:** font subsetting, bundled assets, cache-aware static delivery, Lighthouse-driven tuning.
- **An AI agent organisation runs operations:** a coordinated team of AI agents (chief of staff, team leads, workers) handles routine engineering, QA, SEO, analytics and marketing tasks under human approval and a hard usage budget, with an auto-heal pipeline that detects bugs and proposes validated patches using a local model.
- **Solo-built:** one engineer owned product, design, backend, mobile, infrastructure, hardware direction and quality.

## Built by

**Sarvesvara Ramar** - Founder and sole engineer of Trifini.

- LinkedIn: [linkedin.com/in/sarvesvara-r-b2b310249](https://www.linkedin.com/in/sarvesvara-r-b2b310249/)
- Email: [sarvesvarasar@gmail.com](mailto:sarvesvarasar@gmail.com)
- Product: [trifini.com](https://trifini.com)

Open to conversations about roles, collaboration and partnerships.

---

<sub>Source code is private. This repository documents the product and its architecture. Documentation and assets are provided under the terms in [LICENSE](LICENSE).</sub>
