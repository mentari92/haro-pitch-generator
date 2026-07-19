# CODEX PROMPT: Build HARO Pitch Generator

## Copy prompt di bawah ini ke Codex (OpenAI)

---

```
You are building HARO Pitch Generator — a single-page web app that generates 3 HARO (Help A Reporter Out) pitches in under 8 seconds using OpenAI GPT-4o.

This project is submitted to OpenAI Build Week 2026 (Track: Work & Productivity). It must be polished, professional, and demonstrate what Codex can build.

## CONTEXT

Read these blueprint documents FIRST before writing any code:

1. docs/00-master-prd.md — Product Requirements (read this first for product context)
2. docs/01-architecture.md — System architecture

## CRITICAL REQUIREMENTS

1. SINGLE FILE: Everything (HTML + CSS + JS) goes into ONE file: index.html
2. NO BUILD STEP: Must work by opening index.html directly in a browser
3. NO BACKEND: All logic runs client-side
4. NO FRAMEWORKS: Vanilla JavaScript only
5. Tailwind CSS via CDN (https://cdn.tailwindcss.com)
6. Google Fonts: Inter (via CDN)
7. NO external dependencies besides Tailwind + Inter + OpenAI API

## WHAT TO BUILD

### File: index.html

A complete, polished, single-page web application with these sections:

---

### SECTION 0: <head> Setup
- Viewport meta tag for responsive
- Tailwind CSS CDN
- Inter font from Google Fonts
- Title: "HARO Pitch Generator"
- Dark theme by default (add dark class to html element)
- Smooth scroll behavior
- Meta description for SEO: "Generate 3 HARO pitches in 5 seconds using AI. Built for OpenAI Build Week 2026."

---

### SECTION 1: HEADER
- Left: 🔥 icon + "HARO Pitch Generator" title
- Right: Theme toggle button (🌙/☀️) + small badge "Built with Codex"
- Sticky header with blur backdrop
- Dark: bg-slate-900/80, Light: bg-white/80

### SECTION 2: API KEY INPUT (Collapsible)
- Small toggle: "🔑 API Settings"
- When expanded: password input for OpenAI API key
- Placeholder: "sk-..."
- Save button that stores to localStorage key: "haro_api_key"
- On page load: auto-load from localStorage
- Helper text: "Your key stays in your browser. Never sent to any server."

### SECTION 3: HERO
- Headline: "Your HARO Pitches, Written in Seconds"
- Subheadline: "Paste any HARO query. Get 3 unique pitch variants. Copy and send."
- Stats counter: "🔥 X pitches generated today" (from localStorage)
- Small note: "Built for OpenAI Build Week 2026"

### SECTION 4: INPUT FORM
Two textareas + one optional input + one button:

4a. "HARO Query" textarea
- 4 rows, full width
- Placeholder: "Paste the HARO / Connectively query here...

Example: Need quotes from SEO experts about the impact of Google's December 2025 Core Update on small businesses for a Forbes article."

4b. "Your Bio / Expertise" textarea
- 3 rows, full width
- Placeholder: "e.g. SEO specialist with 5 years experience. Helped 50+ sites recover from core updates. Featured in Search Engine Journal."

4c. "Target Publication (optional)" input
- 1 row
- Placeholder: "e.g. Forbes, Inc, TechCrunch"

4d. Generate button
- Full width, large, gradient background (blue to purple)
- Text: "🚀 Generate 3 Pitches"
- Disabled during loading
- Loading text: "⏳ Analyzing query and crafting pitches..."

### SECTION 5: SAMPLE QUERIES (Clickable)
Small section below the form with label: "💡 Try a sample query:"
3 clickable chips/badges:
1. "🔍 SEO Core Update" — fills query about Google December 2025 Core Update
2. "📱 SaaS Growth" — fills query about SaaS growth strategies
3. "🌐 Local SEO" — fills query about local SEO trends

On click: pre-fill the HARO Query textarea with the sample query text.

### SECTION 6: LOADING STATE
When generating, show 3 skeleton cards with shimmer animation:
- Each card: gray placeholder with animated pulse
- Text below: "Generating 3 pitches tailored to your expertise..."

### SECTION 7: RESULTS (3 Pitch Cards)
3 cards, stacked vertically, each with:

Card 1: Professional (blue accent)
- Badge: "📝 Professional ★ Best Match"
- Full pitch text (50-100 words, paragraph)
- Relevance score: horizontal progress bar
  - Label: "Relevance: 92%"
  - Bar: gradient blue, animated width
- "Why this works" — small collapsible section with explanation
- Button: "📋 Copy Pitch" (blue)
- Border left: blue-500, 4px

Card 2: Storytelling (purple accent)
- Badge: "📖 Storytelling"
- Same structure as Card 1 but purple theme
- Border left: purple-500, 4px

Card 3: Data-Driven (green accent)
- Badge: "📊 Data-Driven"
- Same structure but green theme
- Border left: green-500, 4px

Cards animate in sequentially with a staggered delay (first at 0ms, second at 150ms, third at 300ms).

### SECTION 8: HOW IT WORKS
4 steps in a grid (2x2 on mobile, 4 columns on desktop):
1. 📋 Paste query from your HARO email
2. 🤖 AI analyzes + generates 3 unique pitches
3. ⭐ Pick the best tone for your journalist
4. 🚀 Copy and send — backlink secured!

Each step: icon + title + short description, with subtle hover effect.

### SECTION 9: FOOTER
- Simple, centered
- "🔥 HARO Pitch Generator — Built with Codex for OpenAI Build Week 2026"
- GitHub link

---

## JAVASCRIPT LOGIC

### State Management
Use a simple state object:
```javascript
const state = {
  apiKey: localStorage.getItem('haro_api_key') || '',
  query: '',
  bio: '',
  publication: '',
  isLoading: false,
  results: null,
  error: null,
  theme: localStorage.getItem('haro_theme') || 'dark',
  stats: JSON.parse(localStorage.getItem('haro_stats') || '{"total":0,"today":0,"date":""}')
};
```

### Functions to implement:

1. `loadSampleQuery(type)` — pre-fills query textarea with sample
   - Sample 1 (SEO): "[FORBES] Need quotes from SEO experts about Google's December 2025 Core Update. How has it changed the landscape for small businesses? What specific strategies are working now? Deadline: 48 hours."
   - Sample 2 (SaaS): "[TECHCRUNCH] Looking for growth marketers to discuss how B2B SaaS companies can reduce dependency on paid ads. What organic channels are underutilized? Deadline: 72 hours."
   - Sample 3 (Local): "[BUSINESS INSIDER] Need insights on local SEO trends for 2026. How are small businesses adapting to AI search? What's working for local pack rankings? Deadline: 24 hours."

2. `saveApiKey()` — saves key to localStorage, shows success toast

3. `generatePitches()` — main function:
   - Validates query (min 10 chars), bio (min 10 chars), API key
   - Sets isLoading = true
   - Calls OpenAI API
   - On success: sets results, updates stats
   - On error: sets error message
   - Sets isLoading = false

4. `callOpenAI(query, bio, publication)` — the API call:
   ```javascript
   async function callOpenAI(query, bio, publication) {
     const response = await fetch('https://api.openai.com/v1/responses', {
       method: 'POST',
       headers: {
         'Content-Type': 'application/json',
         'Authorization': `Bearer ${state.apiKey}`
       },
       body: JSON.stringify({
         model: 'gpt-5.6-terra',
         reasoning: { effort: 'low' },
         input: [
           {
             role: 'developer',
             content: `You are an expert HARO pitch writer helping SEO professionals get quoted in top publications.

Generate 3 distinct HARO pitches.

RULES:
- Each pitch: 50-100 words, one paragraph
- Must be personalized to the query and the user's bio
- Pitch 1 (professional): Formal, authoritative, credible. Uses data and experience.
- Pitch 2 (storytelling): Narrative-driven, personal, engaging. Uses a story or case study.
- Pitch 3 (data_driven): Evidence-based, uses statistics, research findings, or specific numbers.
- relevance_score: 0-100, how well this pitch matches the query intent
- why_it_works: One sentence explaining why a journalist would pick this pitch

Output MUST match the provided JSON schema exactly.`
           },
           {
             role: 'user',
             content: `HARO Query: ${query}\n\nBio: ${bio}\n${publication ? `Target Publication: ${publication}` : ''}`
           }
         ],
         text: {
           format: {
             type: 'json_schema',
             schema: {
               type: 'object',
               properties: {
                 pitches: {
                   type: 'array',
                   items: {
                     type: 'object',
                     properties: {
                       tone: { type: 'string' },
                       pitch: { type: 'string' },
                       relevance_score: { type: 'number' },
                       why_it_works: { type: 'string' }
                     },
                     required: ['tone', 'pitch', 'relevance_score', 'why_it_works'],
                     additionalProperties: false
                   }
                 }
               },
               required: ['pitches'],
               additionalProperties: false
             }
           }
         }
       })
     });
     const data = await response.json();
     const output = data.output.find(o => o.role === 'assistant');
     const content = output.content.find(c => c.type === 'output_text');
     return JSON.parse(content.text);
   }
   ```

5. `copyPitch(text, buttonElement)` — copies text, shows "Copied!" for 2 seconds

6. `toggleTheme()` — toggles dark/light class, saves preference

7. `updateStatsDisplay()` — reads stats from localStorage, updates UI

8. `renderResults(pitches)` — creates HTML for pitch cards with animation

9. `renderSkeletons()` — shows 3 skeleton loading cards

10. `showError(message)` — shows error banner

### Error Handling
- API key missing: "Please enter your OpenAI API key in Settings"
- Query too short: "Query must be at least 10 characters"
- Bio too short: "Bio must be at least 10 characters"
- API error (401): "Invalid API key. Please check your key in Settings."
- API error (429): "Rate limited. Please wait a moment and try again."
- API error (other): "Something went wrong: [error message]"
- Network error: "Connection error. Please check your internet."

### localStorage Keys
- haro_api_key: string — the saved API key
- haro_theme: "dark" | "light" — theme preference
- haro_stats: { total: number, today: number, date: "YYYY-MM-DD" }

### Stats Logic
- On page load: check if stats.date matches today. If not, reset today to 0.
- On successful generation: increment total and today.
- Display: "🔥 X pitches generated today" in hero and footer.

---

## UI POLISH REQUIREMENTS

- Dark theme default: bg-slate-900, text-slate-100, cards bg-slate-800
- Light theme: bg-white, text-slate-900, cards bg-gray-50
- Smooth transitions on theme toggle (transition-colors)
- All textareas have: dark bg-slate-700, light bg-white, border, rounded-lg, focus ring
- Buttons have: hover scale effect, active press effect, transition-all
- Cards have: shadow, hover:shadow-lg, rounded-xl, transition-all
- Gradient generate button: bg-gradient-to-r from-blue-600 to-purple-600
- Relevance bar: gradient matching card theme
- Toast notification for "Copied!" — appears at bottom-right, fades out
- Loading skeleton: animate-pulse with rounded-lg gray blocks
- Staggered card animation: opacity-0 → opacity-100 with translate-y-0
- Scroll margin for sections
- Responsive: works on mobile (320px) to desktop (1920px)
- Max container width: 800px, centered
- Padding: p-4 on mobile, p-8 on desktop

---

## FINAL CHECKLIST

Before finishing, verify:
- [ ] File opens directly in browser and works
- [ ] Dark/light theme toggles smoothly
- [ ] Sample queries pre-fill the form
- [ ] API key saves to localStorage
- [ ] Generate button shows loading state
- [ ] 3 pitch cards display with staggered animation
- [ ] Copy button copies text and shows feedback
- [ ] Error messages display for all failure modes
- [ ] Stats persist and update correctly
- [ ] Responsive on mobile and desktop
- [ ] All links work (GitHub, etc.)
- [ ] No console errors
- [ ] Tailwind classes all load correctly

---

## OUTPUT

Create a SINGLE file: index.html

The file must be COMPLETE and PRODUCTION-READY. Every feature listed above must work. No TODOs, no placeholders.

Save it to the project root directory.
```

---

## Cara Pakai

1. Copy semua teks di atas (dari "---" pertama sampai akhir)
2. Buka Codex (OpenAI)
3. Paste prompt
4. Codex akan baca docs/ → generate `index.html`
5. Buka `index.html` di browser → coba demo mode
6. Masukkan OpenAI API key → generate beneran
7. Push ke GitHub + deploy GitHub Pages
8. Submit ke DevPost 🚀
