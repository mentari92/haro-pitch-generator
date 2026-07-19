# HARO Pitch Generator — Architecture

> **Version:** 2.0  
> **Stack:** Single HTML file + Tailwind CSS (CDN) + OpenAI GPT-4o API  
> **Built with:** Codex CLI

---

## 1. System Architecture

Single-page application. Zero backend. Zero build step. Everything runs in the browser.

```
┌──────────────────────────────────────────────────────────────┐
│                        Browser                                │
│                                                               │
│   ┌──────────────────────────────────────────────────────┐   │
│   │                   index.html                          │   │
│   │                                                       │   │
│   │  ┌─────────────┐   ┌─────────────────────────────┐   │   │
│   │  │ Tailwind CDN │   │     JavaScript (Vanilla)     │   │   │
│   │  │  (styling)   │   │                             │   │   │
│   │  └─────────────┘   │  • UI State Management      │   │   │
│   │                     │  • OpenAI API Integration   │   │   │
│   │                     │  • localStorage Persistence │   │   │
│   │                     │  • Clipboard API            │   │   │
│   │                     │  • Theme Toggle             │   │   │
│   │                     │  • Demo Mode                │   │   │
│   │                     └──────────┬──────────────────┘   │   │
│   └────────────────────────────────┼──────────────────────┘   │
└────────────────────────────────────┼──────────────────────────┘
                                     │
                                     ▼
                    ┌──────────────────────────────┐
                    │     OpenAI GPT-4o API         │
                    │     (Chat Completions)        │
                    │                              │
                    │  Input: HARO query + bio     │
                    │  Output: 3 pitches (JSON)    │
                    └──────────────────────────────┘
```

## 2. Tech Stack

| Layer | Choice | Why |
|-------|--------|-----|
| **Frontend** | HTML + Tailwind CSS 3.x CDN | Zero build, instant setup |
| **Typography** | Inter (Google Fonts) | Clean, modern, readable |
| **Icons** | Unicode/Emoji | No icon library dependency |
| **Logic** | Vanilla JavaScript (ES6+) | No framework overhead |
| **AI** | OpenAI GPT-4o (JSON mode) | Reliable structured output |
| **Storage** | Browser localStorage | API key + stats persistence |
| **Deployment** | GitHub Pages | Free, instant, no config |

## 3. OpenAI API Integration

### Request

```javascript
// POST https://api.openai.com/v1/responses
{
  "model": "gpt-5.6-terra",
  "reasoning": { "effort": "low" },
  "input": [
    {
      "role": "developer",
      "content": "You are an expert HARO pitch writer..."
    },
    {
      "role": "user",
      "content": "Query: [paste from HARO email]\nBio: [user expertise]\nPublication: [target outlet]"
    }
  ],
  "text": {
    "format": {
      "type": "json_schema",
      "schema": {
        "type": "object",
        "properties": {
          "pitches": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "tone": { "type": "string" },
                "pitch": { "type": "string" },
                "relevance_score": { "type": "number" },
                "why_it_works": { "type": "string" }
              },
              "required": ["tone", "pitch", "relevance_score", "why_it_works"],
              "additionalProperties": false
            }
          }
        },
        "required": ["pitches"],
        "additionalProperties": false
      }
    }
  }
}
```

### Response (JSON)

```json
{
  "pitches": [
    {
      "tone": "professional",
      "pitch": "As an SEO specialist who has helped 50+ sites recover from Google core updates...",
      "relevance_score": 92,
      "why_it_works": "This pitch positions you as a credible authority with specific, verifiable results."
    },
    {
      "tone": "storytelling",
      "label": "Storytelling",
      "pitch": "I'll never forget the panic when a client's traffic dropped 80% overnight...",
      "relevance_score": 85,
      "why_it_works": "Journalists love narratives. This hooks them with a relatable scenario."
    },
    {
      "tone": "data_driven",
      "label": "Data-Driven",
      "pitch": "After analyzing 500 sites affected by the December 2025 update...",
      "relevance_score": 78,
      "why_it_works": "Data-backed pitches are 2x more likely to get quoted."
    }
  ]
}
```

## 4. File Structure

```
haro-pitch-generator/
├── index.html              ← Single file app (HTML + CSS + JS)
├── docs/
│   ├── 00-master-prd.md    ← Product Requirements
│   └── 01-architecture.md  ← Architecture (this file)
├── CODEX-PROMPT.md         ← The prompt given to Codex
├── STORY.md                ← DevPost submission story
└── README.md               ← Quick start guide
```

## 5. UI Component Tree

```
┌── App Container
│   ├── Header
│   │   ├── Logo + Title
│   │   ├── Theme Toggle (🌙/☀️)
│   │   └── Build Week Badge
│   ├── API Key Input (collapsible)
│   │   ├── Password Input
│   │   └── Save button
│   ├── Hero Section
│   │   ├── Headline
│   │   ├── Subheadline
│   │   └── Stats counter
│   ├── Input Form
│   │   ├── HARO Query Textarea
│   │   ├── Bio Textarea
│   │   ├── Optional: Publication Input
│   │   └── Generate Button
│   ├── Loading State
│   │   └── 3 Skeleton Cards
│   ├── Results Section
│   │   ├── Pitch Card 1 (Professional ★)
│   │   │   ├── Tone Badge
│   │   │   ├── Pitch Text
│   │   │   ├── Relevance Score Bar
│   │   │   ├── "Why This Works" Tooltip
│   │   │   └── Copy Button
│   │   ├── Pitch Card 2 (Storytelling)
│   │   │   └── (same structure)
│   │   └── Pitch Card 3 (Data-Driven)
│   │       └── (same structure)
│   ├── Sample HARO Queries Section
│   │   └── Clickable example queries
│   ├── How It Works Section
│   │   ├── Step 1: Paste
│   │   ├── Step 2: Generate
│   │   ├── Step 3: Copy
│   │   └── Step 4: Send
│   └── Footer
│       ├── Stats
│       ├── GitHub Link
│       └── Built with Codex badge
```

## 6. Data Flow

```
1. Page Load
   → Check localStorage for saved API key → prefill if exists
   → Check localStorage for today's stats → display counter
   → Pre-fill sample HARO query for demo (first visit)

2. User Clicks "Generate"
   → Validate inputs (query >= 10 chars, bio >= 10 chars, API key present)
   → Show loading state (3 skeleton cards with shimmer)
   → Disable button + show spinner
   → Call OpenAI API
   → On success: render 3 pitch cards
   → On error: show error message with actionable feedback
   → Increment stats in localStorage

3. User Clicks "Copy"
   → navigator.clipboard.writeText(pitchText)
   → Show "Copied!" feedback on button (2 seconds)
   → Brief toast notification

4. Theme Toggle
   → Toggle dark/light class on <html>
   → Save preference to localStorage
   → Smooth CSS transition
```

## 7. UI States

### Initial State (First Visit)
- Hero section with headline + explanation
- Pre-filled sample query for instant demo
- API key input (empty, with instructions)
- Stats: "0 pitches generated today"

### Ready State (API Key Saved)
- Form ready with saved key
- Sample query still visible
- Stats: "X pitches generated today"

### Loading State
- Generate button: spinner + "Analyzing query..."
- 3 skeleton cards with shimmer animation
- All inputs disabled

### Success State
- 3 pitch cards animate in (staggered)
- Copy buttons ready on each card
- Stats updated

### Error State
- Error banner: "API Error: [specific message]"
- Inputs re-enabled
- Retry possible

### Empty State
- Default form with placeholder text
- Helper text: "Tip: Be specific about your expertise"
- Sample query clickable to pre-fill

## 8. Performance Budget

| Metric | Target |
|--------|--------|
| HTML file size | < 50 KB |
| API response time | < 8 seconds |
| Time to interactive | < 3 seconds |
| Lighthouse score | > 90 (best practices) |

## 9. Key Design Decisions

| Decision | Rationale |
|----------|-----------|
| Single HTML file | Zero build step, instant deploy to GitHub Pages |
| API key in browser | No backend needed, user owns their key |
| JSON response format | Structured, parseable, easy to render |
| localStorage | Persists across sessions, no server needed |
| Tailwind CDN | Styling without build step, 90KB gzipped |
| No framework | Vanilla JS is faster, simpler, more maintainable |
| Unicode icons | Zero external dependencies |
