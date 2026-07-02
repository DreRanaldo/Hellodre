# SDMP — Software Dev Marketplace
## Product & Design Specification v1.0

> A marketplace that combines the best of **Upwork, Fiverr, GitHub, Jira, Trello, Slack, and Stripe** into one platform dedicated to software development — built on **milestone-based escrow** and **independent QA verification**.

**Companion mockups:** open [`mockups/index.html`](mockups/index.html) in a browser (all screens are self-contained HTML/CSS/JS, no build step, dark + light mode).

---

## 1. Vision & positioning

SDMP connects **clients** (businesses, entrepreneurs, startups, individuals) with **developers, UI/UX designers, QA testers, project managers, and DevOps engineers**. Its differentiators over generic freelance platforms:

1. **Escrow-first trust model** — money is deposited up front, locked with SDMP, and released only per approved milestone.
2. **Independent QA in the loop** — every milestone can be verified by a third-party tester before funds release.
3. **Real dev tooling built in** — Kanban workspace, Git integration, code snippets in chat, version history.

Design references: **Linear, Stripe, GitHub, Upwork, Vercel** — modern, minimal, professional, enterprise quality.

---

## 2. Design system

### 2.1 Brand colors

| Token | Hex | Usage |
|---|---|---|
| Primary | `#2563EB` | CTAs, links, active states |
| Secondary | `#4F46E5` | Gradients, secondary emphasis |
| Accent | `#06B6D4` | Highlights, AI features, info |
| Success | `#10B981` | Escrow released, QA pass, online |
| Warning | `#F59E0B` | In QA, pending, ratings stars |
| Danger | `#EF4444` | Disputes, errors, destructive actions |
| Background (light) | `#FFFFFF` | Light mode canvas |
| Background (dark) | `#0F172A` | Dark mode canvas |

Brand gradient: `linear-gradient(135°, #2563EB → #4F46E5 → #06B6D4)`.

### 2.2 Visual language

- **Themes:** full light + dark mode; toggle persisted per user, defaults to OS preference.
- **Corners:** rounded — 8 px (small controls), 12 px (buttons/inputs), 16 px (cards), 24 px (hero/feature cards).
- **Glassmorphism accents:** translucent panels (`backdrop-filter: blur(18px)`) for nav bars, hero cards, and AI panels — accents only, never body content.
- **Gradients:** brand gradient on primary CTAs, wallet card, avatars, hero text.
- **Motion:** 150 ms micro-interactions, 280 ms layout transitions, `cubic-bezier(.22,.68,.34,1)`; fade-up entrances, hover lift on cards. Respect `prefers-reduced-motion`.
- **Typography:** Inter (fallback: system sans); JetBrains Mono for code/amounts/IDs. Display headlines −3.5% letter-spacing, weight 800.
- **Responsive:** 1200 px max content width; breakpoints at 1024 px and 720 px; sidebar collapses to bottom tab bar on mobile.

### 2.3 Core components (see `mockups/assets/sdmp.css`)

Buttons (primary/secondary/ghost/success/danger × sm/md/lg) · cards (flat, hover-lift, glass) · badges & chips · avatars (with online dot, gradient fallbacks) · form fields · search bars · progress bars · tables · stat tiles · Kanban columns/cards · chat bubbles · milestone stepper · star ratings · theme toggle.

---

## 3. User types & permissions

| Capability | Client | Developer | Tester | Admin |
|---|---|---|---|---|
| Post projects, create milestones, upload requirements | ✅ | — | — | ✅ |
| Apply to projects / receive invitations | — | ✅ | ✅ | — |
| Submit work, track milestones, daily updates | — | ✅ | — | — |
| Test builds, file bug reports, pass/fail verdicts | — | — | ✅ | — |
| Approve work & release escrow | ✅ | — | — | ✅ (disputes) |
| Chat, video calls, screen share | ✅ | ✅ | ✅ | ✅ |
| Leave / receive reviews | ✅ | ✅ | ✅ | moderate |
| Approve users, KYC verification, ban users | — | — | — | ✅ |
| Manage escrow, freeze payments, resolve disputes | — | — | — | ✅ |
| Platform analytics, transactions, reports | own | own | own | ✅ all |

A single account can hold multiple roles (e.g., developer who also hires); the dashboard adapts to the active role.

---

## 4. Information architecture

```
Marketing site          App (authenticated)                Admin
├─ Home (landing)       ├─ Dashboard (per-role)            ├─ Overview KPIs
├─ Find Talent          ├─ Projects                        ├─ Users & verifications
├─ Find Work            │   ├─ Post project (wizard)       ├─ Projects
├─ Browse Projects      │   ├─ Proposals & hiring          ├─ Escrow & transactions
├─ How It Works         │   └─ Workspace                   ├─ Disputes
├─ Pricing              │       ├─ Kanban board            ├─ Fraud & moderation
├─ FAQs                 │       ├─ Timeline & milestones   ├─ Featured listings
└─ Auth                 │       ├─ Files & versions        └─ Analytics & audit log
                        │       ├─ QA reports
                        │       └─ Git commits
                        ├─ Messages (real-time)
                        ├─ Wallet & escrow
                        ├─ Calendar / Tasks
                        ├─ Notifications
                        └─ Profile & settings
```

---

## 5. Screens

### 5.1 Landing page — `mockups/index.html`
Sections, in order: sticky glass nav · **Hero** ("Find Expert Developers. Build Amazing Software." + CTAs *Hire Developers / Find Work / Browse Projects*, live stats, floating escrow-card mock) · Trusted companies · Categories grid · Featured developers · Trending projects · How It Works (4 steps) · **Escrow Protection** feature panel with live milestone stepper · Success stories · Pricing (Starter/Pro/Enterprise) · FAQs · Gradient CTA banner · Footer.

### 5.2 Authentication
Email + password, OAuth (Google, GitHub, Microsoft, Apple), magic link. **2FA** (TOTP + SMS backup), forgot-password flow, device management. Signup asks role intent (hire / work / test) to tailor onboarding. KYC verification required before first withdrawal or "Verified" badge.

### 5.3 Dashboard — `mockups/dashboard.html`
Per-role widgets: stat tiles (active projects, escrow balance, released this month, approval speed) · active projects with progress · **"Needs your action"** rail (approve milestone, assign tester) · message previews · gradient wallet snapshot · recent-activity table. Developer variant swaps in earnings, proposals, and milestone deadlines; tester variant shows assignment queue and accuracy score.

### 5.4 Post a project — `mockups/post-project.html`
4-step wizard: **Basics → Details & budget → Milestones → Review & fund escrow.** Fields: title, description, budget range, deadline, tech-stack chips, attachments (drag-drop), optional repository & Figma links, priority, QA mode (auto-assign / choose / optional), visibility (**Public / Private / Invite only**). Inline **AI Project Estimator** panel: suggested budget, predicted timeline, risk analysis, suggested milestones, top developer matches.

### 5.5 Browse & search — `mockups/browse.html`
Tab chips: Developers / QA Testers / Designers / PMs / DevOps / Projects. Sticky filter rail: languages & frameworks, hourly rate, country, min rating, years of experience, availability, verified-only, top-rated-only. Result cards: avatar + online dot, badges (✓ Verified, 🏆 Top Rated, ⚡ Fast Delivery, 🎓 Expert), rating & review count, skills, rate, *View Profile* / *Invite* actions. Sort: best match, rating, rate, project count.

### 5.6 Developer profile — `mockups/profile.html`
Gradient cover · avatar + verification/achievement badges · gamification level & XP. Main column: About, skill bars (verified via assessments), portfolio grid, reviews with project/value context. Side rail: hourly rate, availability, response time, completed projects, on-time %, **QA first-pass rate**, links (GitHub with stars, LinkedIn, resume), certificates, achievements. CTAs: *Invite to Project*, *Message*.

### 5.7 Project workspace — `mockups/project.html`
Header: project meta, team (client/developer/tester), stack chips, repo & Figma links, escrow summary (released vs locked). Tabs: **Board · Timeline · Milestones · Files · QA Reports · Commits · Settings**.
- **Kanban:** Backlog → To Do → Doing → Testing → Completed; cards carry ticket ID, milestone tag, assignee, progress.
- **Milestones stepper:** per-milestone amount + state; current milestone shows *Approve & release* / *Request revision*.
- **QA panel:** tester identity, checks passed (e.g., 32/34), bug list with severity, session recording, performance score.
- **Commits:** recent Git activity (GitHub/GitLab/Bitbucket integrations).

### 5.8 Messaging — `mockups/messages.html`
Thread list with unread badges · conversation with day separators, read receipts (✓✓), **typing indicator**, code-snippet blocks, file/video attachments, voice notes, task mentions (`@task`), inline **milestone event cards** (e.g., "Milestone 2 submitted — Review"). Header actions: voice call, video call, screen share. All messages encrypted.

### 5.9 Wallet & escrow — `mockups/wallet.html`
Balance tiles: total (gradient), **locked in escrow**, releasable, available. Escrow-by-project table (total/released/locked/status) · payment methods (Stripe cards, PayPal, bank/ACH, Wise, optional crypto) · transaction history with type badges (Release, QA payout, Deposit, Refund, Fee) and invoice links · CSV export & tax reports · multi-currency.

### 5.10 Admin panel — `mockups/admin.html` (dark by default)
KPIs: platform revenue, escrow under management, active users, open disputes. Revenue/escrow chart · **verification queue** (KYC approve/reject) · **disputes table** with *Freeze funds / Propose split / Release* actions and SLA timer · fraud signals (blocked payments, duplicate identities, off-platform hints) · QA network health (turnaround, tester accuracy) · live **audit log**. Also: featured listings management, content moderation, ban controls.

---

## 6. Core flows

### 6.1 Client flow
1. Create project (wizard §5.4) → AI estimator suggests scope/budget/milestones.
2. Receive proposals → compare developers (experience, portfolio, reviews, price) side by side.
3. Hire → **deposit full amount into escrow** (funds locked with SDMP).
4. Track work in workspace; approve or reject each milestone after QA.
5. On completion: leave review, download deliverables, tax invoice generated.

### 6.2 Developer flow
1. Build profile: photo, bio, skills, languages/frameworks, certificates, portfolio, GitHub, LinkedIn, resume, hourly rate, availability.
2. Browse/search projects (filters: technology, budget, country, experience) or receive invitations.
3. Apply: cover letter + price + timeline + portfolio highlights.
4. When hired: project dashboard — tasks, milestones, file uploads, Git commits, progress tracking, **daily updates**, messaging.
5. Submit milestone → QA → client approval → **instant payout**.

### 6.3 Tester (QA) flow
1. Developer submits milestone → project **automatically enters Testing**.
2. Available testers notified; client **chooses a tester or auto-assigns**.
3. Tester receives requirements, acceptance checklist, test cases.
4. Tester submits: bug report (severity-tagged), screenshots, videos, performance report, **Pass/Fail verdict + QA score**.
5. **Fail** → developer revises (loop). **Pass** → client approves → escrow releases → **developer and tester paid automatically**.

### 6.4 Escrow state machine

```
                ┌────────────┐
   deposit ────▶│   FUNDED   │  (locked; developer cannot withdraw)
                └─────┬──────┘
            milestone submitted
                ┌─────▼──────┐   fail    ┌──────────┐
                │  IN QA     ├──────────▶│ REVISION │──┐
                └─────┬──────┘           └──────────┘  │ resubmit
              QA pass │                       ▲────────┘
                ┌─────▼──────┐  reject  ┌──────────┐  escalate  ┌─────────┐
                │ CLIENT     ├─────────▶│ REVISION │───────────▶│ DISPUTE │
                │ REVIEW     │          └──────────┘            └────┬────┘
                └─────┬──────┘                    admin: release / refund /
              approve │                           split / freeze / chargeback
                ┌─────▼──────┐
                │  RELEASED  │  (automatic payout: developer + tester fees)
                └────────────┘
```

Supported operations: milestone releases, partial releases, full releases, refunds, chargebacks, dispute arbitration. Every transition is written to the immutable audit log.

---

## 7. Feature catalog

### Categories
Web Development · Mobile Apps · Desktop Applications · AI Development · Machine Learning · Game Development · Cybersecurity · Cloud Engineering · DevOps · Blockchain · Embedded Systems · UI/UX Design · API Development · Database Design · Automation · WordPress · Shopify · E-commerce · Testing/QA.

### Ratings & reputation
5-star system with written reviews, bidirectional (clients ↔ developers; testers rate projects). Achievement badges: **Verified Developer, Top Rated, Fast Delivery, Expert**. Reviews carry project value + date for credibility.

### Notifications
Real-time (in-app), email, SMS, push. Triggers: milestone approved, new messages, project invitations, escrow released, payment received, QA verdicts, dispute updates. Per-channel preferences.

### AI features
AI Project Estimator (budget/timeline/risk prediction) · developer suggestions/matching score · requirement generation · AI code review · AI bug detection · resume optimization · skill recommendations.

### Analytics
Per-user: developer earnings, completion rate, project success, client spending, average delivery time, bug rate, tester accuracy. Platform (admin): revenue, GMV, take rate, growth charts.

### Security
Encrypted messaging · KYC identity verification · 2FA · escrow protection · fraud detection (payment velocity, duplicate identity, off-platform-payment detection) · GDPR compliance (export/delete my data) · immutable audit logs · secure payments (PCI via Stripe) · role-based permissions.

### Gamification
XP + levels, achievements, leaderboards (global/country/category), daily streaks, top developers/testers showcases, verified badges.

### Mobile app
Native iOS + Android with full feature parity: offline notification queue, push notifications, biometric login (Face ID / fingerprint). Bottom tab bar: Home · Projects · Post/Apply · Messages · Wallet. Same design tokens.

### Revenue model
Platform service fee (10% Starter / 5% Pro) · premium subscriptions ($29/mo Pro; custom Enterprise) · featured listings · sponsored developers · featured projects · advertising · enterprise plans (SSO, SLAs, payroll) · verification fees.

---

## 8. Suggested technical architecture (for implementation handoff)

- **Frontend:** Next.js (React, TypeScript), Tailwind mapped to the tokens in §2; WebSockets for chat/presence; native apps in Flutter or Swift/Kotlin sharing the API.
- **Backend:** API gateway + services (Node.js/Go): identity & KYC, projects/matching, escrow ledger (double-entry, append-only), messaging, QA workflow, notifications, admin.
- **Payments:** Stripe (cards, Connect payouts) + PayPal/Wise adapters; escrow as internal ledger over PSP balances; webhooks drive state machine §6.4.
- **Data:** PostgreSQL (core), Redis (presence/queues), S3-compatible object storage (files/recordings), OpenSearch (search/filters).
- **Integrations:** GitHub/GitLab/Bitbucket OAuth apps (commits, PR links), Figma embeds, WebRTC (calls/screen share).
- **AI:** Claude API for estimator, requirement generation, code review, and matching-explanation features.

## 9. Future roadmap
Hackathons · developer teams · company accounts · AI pair programming · skill assessments · built-in IDE · code collaboration · video interviews · marketplace API · public developer rankings · freelancer insurance · global payroll.

---

*Deliverable: this spec + 8 linked hi-fi mockups constitute the v1 design handoff. Every screen participates in one continuous journey: post → hire → fund escrow → build → QA → approve → release → review.*
