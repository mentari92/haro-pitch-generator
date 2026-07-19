# HARO Pitch Generator — Master PRD

> **Version:** 1.0  
> **Status:** Draft  
> **Target:** OpenAI Build Week 2026 — Track: Work & Productivity

---

## 1. Product Overview

### 1.1 Vision

HARO (Help A Reporter Out) adalah sumber backlink kualitas tertinggi untuk SEO — Forbes, Inc, Business Insider, TechCrunch. Tapi apply ke HARO itu manual dan makan waktu: baca query, riset angle, nulis pitch, kirim. Rata-rata orang cuma apply ke 5-10 query per minggu karena males.

**HARO Pitch Generator** automate proses ini. Paste query HARO, dapet 3 pitch siap kirim dalam 5 detik.

### 1.2 Target User

- SEO specialists yang daily pake HARO buat link building
- Digital PR professionals
- Content marketers yang butuh backlink
- Freelancer SEO yang manage multiple client

### 1.3 Problem Statement

| Masalah | Dampak |
|---------|--------|
| Nulis pitch manual makan 10-15 menit per query | Cuma bisa apply 5-10 query/hari |
| Banyak orang gak tau angle terbaik | Pitch ditolak journalist |
| Harus nulis ulang untuk tone beda | Repetitif dan membosankan |

### 1.4 Solution

Tool berbasis web yang:

1. Input: Paste HARO query + bio/expertise
2. Proses: GPT-4o analyze query + generate 3 pitch variants
3. Output: 3 pitch siap copy (Professional, Storytelling, Data-Driven)
4. Bonus: Relevance score, originalitas, stats tracker

---

## 2. Feature List

### P0 — Must Have (Build Week MVP)

| Fitur | Description |
|-------|-------------|
| Input HARO Query | Text area untuk paste query dari email |
| Input Bio/Expertise | Text area untuk background user |
| Generate 3 Pitches | GPT-4o generate 3 variant beda tone |
| Copy to Clipboard | One-click copy tiap pitch |
| Responsive UI | Bisa dipake di mobile/desktop |

### P1 — Nice to Have

| Fitur | Description |
|-------|-------------|
| Relevance Score | % match antara pitch dan query |
| Tone Selector | Pilih tone sebelum generate |
| Local Stats | Track jumlah pitch yang digenerate (localStorage) |
| Dark Mode | Toggle dark/light theme |

### P2 — Future

| Fitur | Description |
|-------|-------------|
| HARO Query Parser | Auto-parse query dari forwarded email |
| Pitch History | History semua pitch yang pernah digenerate |
| Export CSV | Export pitch ke CSV |
| Multi-language | Generate pitch dalam bahasa lain |

---

## 3. User Flow

```
User buka web
  → Paste HARO query
  → Paste bio/expertise (optional: target publication + tone)
  → Klik "Generate Pitches"
  → Loading state (5-10 detik)
  → Lihat 3 pitch:
      [Pitch 1: Professional] ★ Recommended
      [Pitch 2: Storytelling]
      [Pitch 3: Data-Driven]
  → Klik [Copy] pada pitch yang dipilih
  → Paste ke email → Send ke HARO ✅
```

---

## 4. Success Metrics

| Metric | Target |
|--------|--------|
| Waktu generate 3 pitch | < 10 detik |
| Copy rate | User copy minimal 1 pitch |
| Relevance accuracy | Pitch sesuai query > 80% |
| Page load time | < 3 detik |

---

## 5. Competitive Landscape

| Tool | Ada Fitur Ini? |
|------|---------------|
| ColdSEO | ❌ Prospecting + email, bukan HARO |
| LinkIntel | ❌ Link building agent, bukan HARO |
| RoastMyEmail | ❌ Roast email doang, gak generate |
| Mailento | ❌ Generate cold email dari URL, bukan HARO |
| **HARO Pitch Generator** | ✅ **First of its kind** |
