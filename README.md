# CV SCOUT — AI CV Evaluator + Interview Simulator

> Bilingual (RO/EN), dark editorial, single-file React. Evaluates a CV with category scores,
> section feedback, rewrite suggestions and a job-match, then runs an adaptive interview
> simulation — all **with zero cost** wherever it's deployed.

🔗 **Live demo:** `https://laurandreea10.github.io/cv-scout/` · 👤 **Author:** [LaurAndreea10](https://github.com/LaurAndreea10)

---

## 🇷🇴 Română

### Ce face

Încarci un CV (PDF, imagine sau text lipit) și primești o analiză onestă: scor general, scoruri pe 5 categorii (impact, claritate, ATS, structură, relevanță), feedback secțiune-cu-secțiune și rescrieri concrete în format *Înainte → După*. Opțional, lipești un anunț de job pentru o comparație CV ↔ cerințe cu cuvinte-cheie găsite și lipsă. Apoi exersezi un **interviu adaptiv** de 5 întrebări, cu răspunsuri model sugerate și feedback final. Totul bilingv RO/EN și cu istoric persistent.

### Decizii tehnice (Problemă → Decizie → Rezultat)

**1. Cost zero, oriunde**
- **Problemă:** aplicația folosește AI, iar un apel API expus pe GitHub Pages ar însemna o cheie publică și costuri reale pentru oricine o folosește.
- **Decizie:** detectare automată a mediului. În Claude.ai se folosește API-ul real (gestionat de platformă, fără cheie); oriunde altundeva se trece pe un **motor local euristic** care rulează 100% în browser. Nicio cheie nu e scrisă vreodată în cod.
- **Rezultat:** demo complet funcțional pe GitHub Pages, fără card, fără cheie expusă, fără factură. O pastilă în header arată mereu modul activ (LIVE AI / LOCAL).

**2. Citirea PDF-urilor fără server**
- **Problemă:** extragerea textului dintr-un PDF cere de obicei un backend — incompatibil cu GitHub Pages și cu „cost zero".
- **Decizie:** `pdf.js` încărcat la cerere de la CDN, extrage textul direct în browser.
- **Rezultat:** PDF-urile reale sunt analizate local, gratuit. PDF-urile scanate (doar imagine) sunt detectate și utilizatorul e ghidat să lipească textul.

**3. Comutare RO/EN fără regenerare**
- **Problemă:** întrebările de interviu generate o singură dată rămâneau în limba inițială la schimbarea toggle-ului.
- **Decizie:** fiecare întrebare e stocată ca *descriptor independent de limbă* (ambele variante în modul live; index în banca bilingvă în modul local), iar textul afișat se derivă din limba curentă.
- **Rezultat:** comutarea RO/EN re-traduce instant întrebările, istoricul, feedback-ul și recomandările, fără apeluri suplimentare.

**4. Istoric persistent cross-environment**
- **Problemă:** `localStorage` e interzis în artifacts, iar `window.storage` nu există pe GitHub Pages.
- **Decizie:** un strat de stocare care alege automat `window.storage` (Claude.ai) → `localStorage` (Pages) → memorie (fallback), totul cu try/catch.
- **Rezultat:** istoricul persistă în orice mediu, fără server.

### Stack
React · pdf.js · CSS pur (fără librării de animație) · single-file · Anthropic API (în modul live)

---

## 🇬🇧 English

### What it does

Upload a CV (PDF, image, or pasted text) and get an honest read: an overall score, 5 category scores (impact, clarity, ATS, structure, relevance), section-by-section feedback, and concrete *Before → After* rewrites. Optionally paste a job post for a CV ↔ requirements comparison with matched and missing keywords. Then practice an **adaptive 5-question interview** with suggested model answers and final feedback. Fully bilingual RO/EN, with persistent history.

### Technical decisions (Problem → Decision → Result)

**1. Zero cost, anywhere**
- **Problem:** the app uses AI, and an API call exposed on GitHub Pages would mean a public key and real costs for anyone using it.
- **Decision:** automatic environment detection. Inside Claude.ai it uses the real API (platform-managed, no key); anywhere else it falls back to a **local heuristic engine** running 100% in the browser. No key is ever written into the code.
- **Result:** a fully working demo on GitHub Pages — no card, no exposed key, no invoice. A header pill always shows the active mode (LIVE AI / LOCAL).

**2. Reading PDFs without a server**
- **Problem:** extracting text from a PDF usually needs a backend — incompatible with GitHub Pages and with "zero cost".
- **Decision:** `pdf.js` loaded on demand from a CDN, extracting text directly in the browser.
- **Result:** real PDFs are analyzed locally, for free. Scanned (image-only) PDFs are detected and the user is guided to paste the text instead.

**3. RO/EN switching without regeneration**
- **Problem:** interview questions generated once stayed in their original language when the toggle was flipped.
- **Decision:** each question is stored as a *language-independent descriptor* (both variants in live mode; an index into the bilingual bank in local mode), and the displayed text is derived from the current language.
- **Result:** flipping RO/EN instantly re-translates questions, history, feedback and tips — with no extra calls.

**4. Cross-environment persistent history**
- **Problem:** `localStorage` is blocked in artifacts, and `window.storage` doesn't exist on GitHub Pages.
- **Decision:** a storage layer that automatically picks `window.storage` (Claude.ai) → `localStorage` (Pages) → in-memory (fallback), all wrapped in try/catch.
- **Result:** history persists in any environment, with no server.

### Stack
React · pdf.js · pure CSS (no animation libraries) · single-file · Anthropic API (in live mode)

---

## 🚀 Deploy

1. Push to a GitHub repo.
2. Settings → Pages → deploy from branch (`main` / root or `/docs`).
3. The app auto-detects it's outside Claude.ai and runs in **LOCAL** mode — no API key needed.

> Note: PDF reading uses `pdf.js` from a CDN, so it requires an internet connection. Pasted text works fully offline.
