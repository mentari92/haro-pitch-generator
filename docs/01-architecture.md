# HARO Pitch Generator — Architecture

> **Version:** 1.0  
> **Stack:** Single HTML file + Tailwind CSS + OpenAI API

---

## 1. System Architecture

Ini adalah **single-page application (SPA)** tanpa backend. Semua logic jalan di browser.

```
┌─────────────────────────────────────────────────────────┐
│                    Browser                               │
│                                                          │
│  ┌──────────────────────────────────────────────────┐   │
│  │              index.html                           │   │
│  │                                                    │   │
│  │  ┌─────────────┐  ┌──────────────────────────┐   │   │
│  │  │ Tailwind CSS │  │     JavaScript Logic      │   │   │
│  │  │  (CDN)       │  │                          │   │   │
│  │  └─────────────┘  │  • Form handling          │   │   │
│  │                    │  • OpenAI API call        │   │   │
│  │                    │  • Copy to clipboard     │   │   │
│  │                    │  • localStorage stats    │   │   │
│  │                    │  • Dark mode toggle      │   │   │
│  │                    └──────────┬───────────────┘   │   │
│  └───────────────────────────────┼───────────────────┘   │
└──────────────────────────────────┼───────────────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────┐
                    │     OpenAI API            │
                    │     (GPT-4o)              │
                    │                          │
                    │  Input: query + bio      │
                    │  Output: 3 pitch JSON    │
                    └──────────────────────────┘
```

## 2. Tech Stack

| Layer | Technology | Alasan |
|-------|-----------|--------|
| Frontend | HTML + Tailwind CSS (CDN) | Zero build step, 1 file |
| Logic | Vanilla JavaScript | No framework needed |
| AI | OpenAI GPT-4o API | Generate pitch berkualitas |
| Storage | localStorage (browser) | Stats tracking |
| Deployment | GitHub Pages / Vercel | Free hosting |

## 3. API Integration

### OpenAI API

**Endpoint:** `https://api.openai.com/v1/chat/completions`

**Request:**
```json
{
  "model": "gpt-4o",
  "messages": [
    {
      "role": "system",
      "content": "You are an expert HARO pitch writer..."
    },
    {
      "role": "user",
      "content": "Query: [query dari user]\nBio: [bio dari user]"
    }
  ],
  "temperature": 0.7,
  "response_format": { "type": "json_object" }
}
```

**Response:**
```json
{
  "pitches": [
    {
      "tone": "professional",
      "pitch": "Full pitch text...",
      "relevance_score": 92,
      "why_it_works": "Alasan kenapa pitch ini bagus"
    },
    {
      "tone": "storytelling",
      "pitch": "...",
      "relevance_score": 85,
      "why_it_works": "..."
    },
    {
      "tone": "data_driven",
      "pitch": "...",
      "relevance_score": 78,
      "why_it_works": "..."
    }
  ]
}
```

## 4. File Structure

```
/haro-pitch-generator
├── index.html            ← Single file aplikasi (HTML + CSS + JS inline)
├── docs/
│   ├── 00-master-prd.md  ← Product requirements
│   └── 01-architecture.md ← Architecture (file ini)
├── CODEX-PROMPT.md       ← Prompt untuk Codex
└── README.md             ← Cara pake
```

## 5. Data Flow

```
1. User input query + bio → form
2. JavaScript validate input → error handling
3. Show loading state → spinner
4. Fetch POST ke OpenAI API → streaming response
5. Parse JSON response → extract 3 pitches
6. Render pitches ke UI → cards dengan copy button
7. User klik copy → clipboard API
8. Increment stats → localStorage
```

## 6. UI States

| State | Component | Description |
|-------|-----------|-------------|
| **Initial** | Form | Input fields + generate button |
| **Loading** | Skeleton/Spinner | "Generating pitches..." |
| **Success** | Pitch Cards | 3 cards with copy buttons |
| **Error** | Alert | "API error: please check your key" |
| **Empty** | Form | Default state dengan placeholder |

## 7. Key Design Decisions

| Decision | Rationale |
|----------|-----------|
| Single file HTML | Mudah di-deploy, gak perlu build step |
| API key dari user | Gak perlu backend, privacy first |
| JSON response format | Mudah di-render ke UI |
| localStorage | Gak perlu database, tracking basic |
| Tailwind CDN | Cepet, gak perlu install |
