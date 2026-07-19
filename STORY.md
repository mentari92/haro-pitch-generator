# HARO Pitch Generator — DevPost Submission Story

## 🎯 One-Liner

**An AI-powered web app that generates 3 HARO pitches in 5 seconds — built entirely with Codex CLI.**

---

## 💡 Inspiration

Every SEO professional knows the feeling. You open your inbox and see 15 new HARO queries from journalists at Forbes, Inc, and TechCrunch. You know each backlink is worth thousands. But writing personalized pitches takes 10-15 minutes each. By the time you finish the third one, you're exhausted. You close the tab and tell yourself you'll do the rest tomorrow.

I've been doing SEO for 5 years. I've helped 50+ sites rank on page 1. And I've lost count of how many HARO opportunities I've skipped because I "didn't have time."

HARO is the most underutilized backlink source in SEO — not because people don't want to apply, but because the manual work is too slow. I built this tool to solve my own problem: **turn 15 minutes of pitch writing into 5 seconds.**

---

## 🏗️ What It Does

HARO Pitch Generator is a single-page web app:

1. **Paste** a HARO query from your email
2. **Add** your bio and expertise
3. **Click** generate → GPT-4o analyzes the query + your background
4. **Get** 3 unique pitch variants (Professional, Storytelling, Data-Driven)
5. **Copy** the best one → paste into HARO → send ✅

No login. No subscription. No backend. Just you, your API key, and OpenAI.

---

## 🔧 How I Built It with Codex

This entire project was built using **Codex CLI**. Here's my workflow:

1. **Blueprint first** — I wrote detailed PRD and architecture documents in `docs/`
2. **Prompt engineering** — I gave Codex a structured prompt referencing the docs
3. **Iterative generation** — Codex built the complete `index.html` in under 10 minutes
4. **Polish** — I refined the UI, error handling, and demo mode

**Key Codex capabilities I used:**
- Context understanding from multiple markdown documents
- Tailwind CSS class generation
- OpenAI API integration with proper error handling
- localStorage persistence logic
- Responsive design across mobile + desktop

---

## 🎨 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | HTML + Tailwind CSS (CDN) |
| **Logic** | Vanilla JavaScript |
| **AI** | OpenAI GPT-4o (JSON mode) |
| **Storage** | Browser localStorage |
| **Deployment** | GitHub Pages |
| **Build Tool** | Codex CLI |

**Why this stack?** Zero build step, zero backend, zero cost to run. The entire application is a single HTML file. Deploy to GitHub Pages in one click. No servers, no databases, no monthly fees.

---

## 🏆 Track: Work & Productivity

HARO Pitch Generator makes outreach teams **10x more productive.** 

- **Before:** 5 HARO queries = 60-75 minutes of writing
- **After:** 5 HARO queries = 25 seconds of generating + 2 minutes of reviewing

For an SEO agency managing 10+ clients, that's **10+ hours saved per week** on pitch writing alone.

---

## 🌟 What Makes This Unique

- **First HARO-specific AI tool** — No existing tool automates HARO pitch generation
- **Zero infrastructure** — Single HTML file, no backend, free to host
- **Privacy-first** — Your API key stays in your browser, never sent to a server
- **Built with Codex** — The entire project, from docs to code, was created using Codex CLI

---

## 🔗 Links

- **GitHub:** https://github.com/mentari92/haro-pitch-generator
- **Live Demo:** https://mentari92.github.io/haro-pitch-generator
- **Demo Video:** [link to demo video]
