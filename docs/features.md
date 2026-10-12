# Trifini features

Trifini organises life into four everyday domains (Mind, Body, Money, Habits) with an AI coach on top, and a wider set of life areas underneath. This page describes what each area does from a user's point of view.

## AI Life Coach

- **Daily rhythm.** A two-minute morning check-in (intention, energy, priorities) and a ninety-second evening reflection. Proactive, quiet-hours aware, and never nags twice.
- **Free to talk to.** The daily coach conversation is part of the free plan; it is the heart of the product, not a paywalled extra.
- **Knows your context.** Answers are enriched with your routines, streaks, reminders and relevant history retrieved from your own data.
- **Can act, with consent.** The coach can propose actions (log a mood, complete or reschedule a routine, create a reminder). Nothing executes without your approval, and every action is logged.
- **Multimodal input.** Type, speak, or attach an image.
- **Progressive unlock.** New users see a small starter surface (dashboard, routines, mood, chat); more of the product appears as they use it.
- **Multi-channel.** The same coach is available on web, the mobile app and Telegram.

## Mind

- 144-emotion grid for fast, nuanced mood logging
- Year-in-pixels view of the whole year at a glance
- Journal, gratitude log and stress tracking
- Morning intentions and evening reflections
- Insight and pattern views connecting mood to sleep, activity and spending
- Therapist-ready export
- Deeper "inner life" tooling: self-assessments, intelligence profile

## Body

- Sleep score from duration and quality, plus energy and stress
- Wearable and Google Fit integration
- Burnout-risk view and support resources
- Breathing exercises and focus sessions
- Physical and diet tracking

## Money

- Accounts, expenses and income
- Budgets with alerts
- Net worth over time, goals and a FIRE calculator
- Tax and financial-health insights
- CSV import and broker imports, live asset prices
- Recurring transactions and bills
- Family finance
- Mood-to-spending correlation (the cross-domain insight no single-purpose app can give)

## Habits and routines

- Routines, habits and one-off tasks in one place
- Habit-strength scoring that rewards consistency rather than only streak length
- Templates, groups and completion history
- Calendar integration and reminders with one-tap complete/skip buttons
- Focus (deep-work) sessions and personal experiments (try a change, measure the effect)

## Gamification

- XP and levels from completing routines, logging mood, tracking health and more
- Daily and weekly quests
- Weekly leagues from Bronze up to Diamond with promotion and demotion zones
- Streak freezes that protect a streak on a missed day
- Grace-period logging so a late entry still counts

## Social

- Friends and groups
- Celebrations of each other's milestones
- Reactions in the style of fitness-tracking apps
- Privacy-first: nothing is shared by default

## Automations

- If-this-then-that rules ("when I finish my morning routine, log my mood")
- Scheduling and cron-style recurrence
- Reminders delivered to web, mobile push or Telegram, with action buttons
- AI proposals that wait for your approval before running

## Memory powered by RAG

Trifini embeds your own entries (mood logs, journal, gratitude, behaviour signals) into a private vector index. When you talk to the coach, it retrieves the most relevant moments from your past, so it can say "in February you wrote that evening walks helped". Embeddings run on local models by default, so personal data does not need to leave the stack to be searchable. A weekly reflection job summarises patterns. See [architecture](architecture.md).

## Voice

Speech-to-text and text-to-speech across 12 languages, available in the chat experience and on mobile.

## Offline and sync

- Installable progressive web app with a service worker and offline page
- The Flutter app supports offline logging
- Multi-device sync uses conflict-free replicated data types (CRDTs), so edits made on a phone and a laptop merge cleanly

## 14 languages

The interface is localised in 14 languages, with English as the primary language.

## Robo Pet

A companion that mirrors your real life. A virtual pet lives on web and mobile (and as a floating widget); a physical desk robot is in development. Details in [robo-pet.md](robo-pet.md).

## Safety and trust

- Crisis-language screening on **every** free-text input (coach, journal, pet naming and more)
- Crisis resources are shown without blocking you from saving what you wrote
- Human alerting for high-risk signals
- Guardrails on both inputs and AI outputs
- A fail-closed policy engine decides whether any AI-initiated action is allowed
- Consent before actions, full data export, and a user-held delete key
- Safety features are never gated behind a paid plan

## Plans and billing

Free, Basic (₹99), Pro (₹299), Premium (₹499) and a Student Pro plan (₹49), priced in ₹ and inclusive of taxes, with a 7-day trial and roughly 40% off annual billing. Payments via Razorpay.

## Surfaces

| Surface | Notes |
|---|---|
| Web app | Dark mode by default, responsive, installable |
| Flutter app | Web first, Android second, iOS scaffolded; biometrics, deep links, push |
| Telegram bot | Conversational coach, reminder buttons, check-ins |
| Voice | Hands-free conversation |
| MCP server | Lets external AI agents read and act on a user's data with permission |
| Robo Pet | Virtual and physical companion |
