# CODEX PROMPT: Build HARO Pitch Generator

## Copy prompt di bawah ini ke Codex

---

```
You are building HARO Pitch Generator — an AI-powered tool that generates HARO (Help A Reporter Out) pitches in seconds using OpenAI GPT-4o.

## CONTEXT

Read these blueprint documents FIRST before writing any code:

1. docs/00-master-prd.md — Product Requirements Document
2. docs/01-architecture.md — System architecture

## TECH STACK

- **Frontend:** Single HTML file + Tailwind CSS (CDN) + Vanilla JavaScript
- **AI:** OpenAI GPT-4o API (chat completions, JSON response format)
- **Storage:** Browser localStorage
- **No backend, no build step, no frameworks**

## WHAT TO BUILD

### File Structure

```
/haro-pitch-generator
├── index.html     ← Single file: HTML + CSS + JS inline
├── docs/          ← Blueprint docs (already created)
├── CODEX-PROMPT.md ← This file
└── README.md      ← Cara pakai
```

### index.html — Tampilan

Buat halaman web 1 file dengan Tailwind CSS CDN. Tampilan dark theme by default.

**Header:**
- Logo/icon 🔥 kecil + judul "HARO Pitch Generator"
- Subtitle: "Generate 3 HARO pitches in 5 seconds"
- Small badge: "Built for OpenAI Build Week 2026"

**Section 1: Input Form**

Dua textarea dengan label:
1. "HARO Query" — placeholder: "Paste the HARO/Connectively query here..."
2. "Your Bio / Expertise" — placeholder: "e.g. SEO specialist, 5 years experience, helped 50+ sites rank page 1"

Satu text input opsional:
3. "Target Publication" — placeholder: "e.g. Forbes, Inc, TechCrunch (optional)"

Satu tombol generate: 🚀 Generate 3 Pitches

**Section 2: Loading State**
- Skeleton cards (3 cards with shimmer animation)
- Text: "Analyzing query and crafting pitches..."

**Section 3: Results (3 Pitch Cards)**

Hasilkan 3 card, masing-masing dengan:
- Label tone: "📝 Professional" / "📖 Storytelling" / "📊 Data-Driven"
- Yang pertama ada badge ★ Recommended
- Full pitch text (paragraph length, 50-100 words)
- Relevance score bar (progress bar visual)
- "Why this works" short explanation
- Tombol [📋 Copy Pitch] — copy to clipboard
- Masing-masing card beda warna accent: Professional=blue, Storytelling=purple, Data-Driven=green

**Section 4: Stats Footer**
- "Today: X pitches generated"
- Simple, di footer

### index.html — Logic

**Form Handling:**
- Validate: query minimal 10 karakter, bio minimal 10 karakter
- Show error message kalau kosong
- Disable button selama loading

**OpenAI API Call:**
```javascript
const response = await fetch("https://api.openai.com/v1/chat/completions", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": `Bearer ${apiKey}`
  },
  body: JSON.stringify({
    model: "gpt-4o",
    messages: [
      {
        role: "system",
        content: `You are an expert HARO pitch writer. Generate 3 HARO pitches in JSON format.
        
Rules:
- Each pitch must be 50-100 words
- Must be personalized to the query and bio
- Pitch 1: Professional tone (formal, credible, authoritative)
- Pitch 2: Storytelling tone (narrative, personal experience, engaging)
- Pitch 3: Data-driven tone (statistics, research, facts)
- Relevance score: 0-100 based on how well the pitch matches the query
- why_it_works: explain briefly why this pitch would catch a journalist's attention

Output ONLY valid JSON with this structure:
{
  "pitches": [
    {"tone": "professional", "pitch": "...", "relevance_score": 92, "why_it_works": "..."},
    {"tone": "storytelling", "pitch": "...", "relevance_score": 85, "why_it_works": "..."},
    {"tone": "data_driven", "pitch": "...", "relevance_score": 78, "why_it_works": "..."}
  ]
}`
      },
      {
        role: "user",
        content: `HARO Query: ${query}\n\nBio: ${bio}\n\nTarget Publication: ${publication || "Not specified"}`
      }
    ],
    temperature: 0.7,
    response_format: { type: "json_object" }
  })
});
```

**API Key Input:**
- Input field di bagian atas untuk OpenAI API key
- Label: "OpenAI API Key"
- Type: password (hidden)
- Simpan ke localStorage setelah pertama kali diisi
- Auto-load dari localStorage kalau sudah ada
- Bisa di-reset

**Copy to Clipboard:**
```javascript
await navigator.clipboard.writeText(pitchText);
// Show "Copied!" feedback on button for 2 seconds
```

**localStorage Stats:**
- Key: `haro_stats`
- Value: `{ totalGenerated: number, todayDate: string, todayCount: number }`
- Increment setiap kali generate sukses
- Reset todayCount kalau date beda

**Dark Mode:**
- Default dark theme
- Toggle button di header (🌙/☀️)
- Smooth transition

**Error Handling:**
- API error: tampilkan alert merah dengan pesan error
- Network error: "Connection error. Please check your internet."
- Rate limit: "Too many requests. Please wait a moment."

## UI/UX DETAILS

- Gunakan gradient halus di background (dark: slate-900 ke slate-800, light: white ke gray-50)
- Card shadow + hover effect
- Smooth transitions semua elemen
- Responsive: mobile-first, max-width container 800px
- Font: Inter (Google Fonts)
- Icon: Gunakan Unicode/emoji, jangan library icon

## OUTPUT

Buat file `index.html` LENGKAP — semua CSS inline di <style>, semua JS inline di <script>.

File harus bisa langsung dibuka di browser dan jalan.
```

---

## Cara Pakai

1. Copy prompt di atas
2. Buka Codex (OpenAI)
3. Paste prompt
4. Codex akan baca docs/00-master-prd.md dan docs/01-architecture.md
5. Codex akan generate `index.html`
6. Buka index.html di browser
7. Masukkan OpenAI API key
8. Selesai! 🚀

## Persiapan Sebelum Coding

- OpenAI API key (bikin di platform.openai.com)
- GitHub repo (buat baru)
- Siapkan kopi ☕
