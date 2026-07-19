# HARO Pitch Generator — Master PRD

> **Version:** 2.0  
> **Status:** Ready for Codex  
> **Target:** OpenAI Build Week 2026 — Track: Work & Productivity  
> **Built with:** Codex + OpenAI GPT-4o

---

## 1. Inspiration (Build Week Story)

### The Problem

Every SEO professional knows HARO (Help A Reporter Out). It's the best source of high-quality backlinks — Forbes, Inc, Business Insider, TechCrunch. A single HARO backlink can be worth $5,000-$10,000 in SEO value.

But there's a reason most people don't apply consistently: **it's tedious.** Every day, 50+ HARO queries land in your inbox. For each one, you need to:
1. Read the query
2. Research the journalist and publication
3. Figure out your angle
4. Write a personalized pitch
5. Proofread and send

That's **10-15 minutes per query.** Most people give up after 5 queries. They're leaving thousands of dollars in backlink value on the table.

### Why I Built This

I've been doing SEO for 5+ years. I've helped 50+ sites rank on page 1 of Google. And I've lost count of how many HARO queries I skipped because I "didn't have time."

I built HARO Pitch Generator using Codex because **I wanted a tool that I would actually use every day.** Not another SaaS platform with a $79/month subscription. Just something simple: paste a query, get 3 pitch options, copy the best one, send it. Done in 5 seconds.

### Why Codex?

I built this entire project using **Codex CLI** — OpenAI's coding agent. Codex helped me:
- Design the UI with Tailwind CSS
- Structure the OpenAI API integration
- Handle edge cases and error states
- Generate polished, production-ready code

This project is a testament to how **Codex turns a 1-week project into a 4-hour build.**

---

## 2. Product Overview

### Vision

Make HARO link building accessible to everyone. Not just SEO agencies with dedicated outreach teams, but freelancers, founders, and content marketers who need backlinks but don't have hours to spend on pitches.

### Target User

- **SEO specialists** — daily HARO users looking to 10x their output
- **Digital PR professionals** — need to respond to journalist queries fast
- **SaaS founders** — bootstrapping organic growth without a big team
- **Freelancers** — managing multiple client backlink campaigns

### Problem Statement

| Problem | Impact | Current Solution |
|---------|--------|-----------------|
| Manual pitch writing takes 10-15 min/query | Only 5-10 queries/day possible | None (HARO is underserved) |
| Most people don't know the best angle | Pitches get rejected | Trial and error |
| Different journalists want different tones | Wasting time rewriting | Manual effort |

### Solution

A single-page web app powered by OpenAI GPT-4o that:
1. Takes a HARO query + your bio
2. Analyzes the journalist's intent and your expertise
3. Generates 3 pitch variants (Professional, Storytelling, Data-Driven)
4. Each with relevance scoring and "why this works" explanation
5. One-click copy — paste and send

---

## 3. Key Features

### P0 — Must Have (Build Week MVP)

| Feature | Description | Why It Matters |
|---------|-------------|----------------|
| HARO Query Input | Paste any HARO/Connectively query | Core functionality |
| Bio/Expertise Input | Your background and credentials | Personalization |
| 3 Pitch Generation | Professional, Storytelling, Data-Driven | Different journalist preferences |
| Relevance Score | 0-100% match indicator | Helps user choose best pitch |
| One-Click Copy | Copy any pitch to clipboard | Speed — send in seconds |
| API Key Management | Save to localStorage, no backend needed | Privacy + simplicity |
| Demo Mode | Sample query included on first visit | Try without setup |

### P1 — Polish (For Submission Impact)

| Feature | Description |
|---------|-------------|
| Dark/Light Theme | Toggle with smooth transition |
| Local Stats | Track today's generated pitches |
| Sample HARO Query | Pre-filled example for instant demo |
| Responsive Design | Mobile + desktop |
| Loading Skeleton | Animated placeholder during generation |
| Error Handling | Clear messages for API errors, rate limits |

### P2 — Future

| Feature | Description |
|---------|-------------|
| Pitch History | Searchable history of all generated pitches |
| Export CSV | Download pitch log for tracking |
| HARO Query Parser | Auto-extract key info from forwarded email |
| Multi-Language | Generate pitches in any language |

---

## 4. User Flow

```
┌─────────────────────────────────────────────────────────┐
│  FIRST VISIT:                                           │
│                                                         │
│  1. See landing page with problem statement              │
│  2. Pre-filled sample HARO query for instant demo        │
│  3. Enter your OpenAI API key                            │
│  4. Click generate → see results in 5 seconds            │
│                                                         │
│  DAILY USE:                                             │
│                                                         │
│  1. Open web app (API key already saved)                 │
│  2. Copy HARO query from email                          │
│  3. Paste into tool                                     │
│  4. Click generate                                      │
│  5. Review 3 pitches → pick best one → copy → send      │
│  6. Total time: ~15 seconds per query                   │
└─────────────────────────────────────────────────────────┘
```

---

## 5. Success Metrics for Build Week

| Metric | Target | How to Measure |
|--------|--------|----------------|
| Generation speed | < 8 seconds | Timing in demo video |
| Pitch quality | 3 usable pitches per query | Judge reads output |
| UI polish | Professional, responsive | Judge visual inspection |
| Codex integration | Built entirely with Codex | Git history shows Codex commits |
| Demo readiness | Works on first try | Demo video + live URL |

---

## 6. Why This Wins (For Judges)

| Judge Perspective | Why This Project Stands Out |
|------------------|---------------------------|
| **Product & Platform** | Solves a real, underserved problem. HARO is a $0 market — no tool exists. |
| **Technical** | Clean architecture: no backend, no build step, pure browser + API. |
| **Business Impact** | Every HARO backlink = $5K-$10K value. This tool pays for itself in one use. |
| **Codex Showcase** | Built from scratch with Codex CLI. Blueprint + prompt → production code. |
| **Track Fit** | Work & Productivity: makes outreach teams 10x faster. |

---

## 7. Competitive Landscape

| Tool | Our Differentiator |
|------|-------------------|
| ColdSEO | Prospecting + outreach, NOT HARO-specific |
| LinkIntel | Backlink outreach agent, NOT HARO-specific |
| RoastMyEmail | Email critique only, doesn't generate |
| Mailento | Cold emails from URL, not HARO queries |
| **HARO Pitch Generator** | **First HARO-specific AI pitch tool** |
