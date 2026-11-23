# 01 — Tech Engine (HTML / CSS / JavaScript)

Project: **Debuggeando Ideas** — technical teaching presentations.

## 0. Scope of this file

This file defines ONLY the technical layer: how to build the presentation file with HTML, CSS and JavaScript.

- It does NOT define what to teach, how many slides to make, or how to write content. Those rules live in other project files (workflow, pedagogy, course domains). Follow them for content; follow THIS file for code.
- It is model-agnostic. Any AI model (Claude, ChatGPT, Gemini) must produce the same visual result by following it literally.
- When this file and your own design ideas disagree, this file wins. Do not "improve", restyle or modernize anything.
- Companion files: `02_Pedagogy_Style.md` decides WHICH component each slide uses and why; `03_Course_Domains.md` decides WHAT is taught and which tool each subject uses. Both reference components of this file by number, e.g. **[7.5]**.

---

## 1. Hard rules (non-negotiable)

1. Output is ONE standalone file named `index.html`. No external local CSS/JS files. No Node.js, npm, bundlers or build steps.
2. Libraries are loaded ONLY from the CDN URLs in section 5, with EXACTLY those versions. Never change a version, never add another library.
3. Start from the Base Template (section 6) copied verbatim. Only replace `[DECK_TITLE]`, the slides inside `<div class="slides">`, and the `ANIMATIONS` registry entries (section 7.10).
4. Use ONLY the components in section 7. Do not invent new class names, layouts or inline styles, except the inline `style` shown in a component snippet.
5. Use ONLY the color tokens in section 2. Never introduce new colors.
6. All user-facing text (titles, bullets, captions, quiz, notes) is in Spanish. Class names, ids and code identifiers stay in English.
7. Never use uppercase titles via CSS. Never use emojis as icons; use the icon system (section 7.7).
8. Every code block is inside a macOS window (section 7.5). Every code block uses Atom One Dark through Reveal's highlight plugin.
9. Inside `<code>` blocks, escape `<` as `&lt;`, `>` as `&gt;` and `&` as `&amp;`.
10. Do not use `localStorage`, `fetch`, frameworks (React, Vue, Tailwind, jQuery) or ES modules.

---

## 2. Color tokens (Nordic Dark)

Declared once in `:root` (already in the template). Reference them with `var(--name)` in CSS. Use the raw hex only inside JavaScript (Mermaid config, GSAP).

| Token | Hex | Use |
|---|---|---|
| `--bg-color` | `#292F3A` | Global background, Mermaid node fill, dark text on light buttons |
| `--text-color` | `#E5E9F0` | Main text, titles |
| `--struct-color` | `#4C566A` | Borders, inactive states, muted text, inline-code background, default animated nodes |
| `--accent-ice` | `#88C0D0` | Primary accent: cover title, kicker, inline-code text, progress bar, active/focused element |
| `--accent-sage` | `#8FBCBB` | Success: correct answer, HIT, successful connection, "good" path |
| `--accent-salmon` | `#E3A89D` | Error / alert: wrong answer, MISS, failure, eviction, "bad" path |
| `--accent-forest` | `#86A67C` | Secondary (bosque): the practical side, what we do in the course (callouts about the project, the practical takeaway card) |
| `--accent-bark` | `#F5E1CE` | Secondary (tronco): the real-world object of an analogy (carta, laptop, cable…) |

Color roles (Nordic landscape), always the same meaning:
- Ice = technical concept and focus. Snow/grey (`--text-color`, `#C4CBD8`) = text.
- Bark = real-world side of an analogy; in a mapping bullet write `<bark>objeto</bark> = <ice>concepto</ice>`.
- Forest = practical / course-specific emphasis.
- Sage and salmon = ONLY success and error. Forest and bark never mean success or error.
- Secondary colors are occasional: max 1–2 elements per slide, and only in text (`tone-*`) or takeaway icons. Never in Mermaid, code or animations.

Fixed secondary shades (do not use elsewhere):
- `#C4CBD8` — subtitle (`h3`) and secondary text.
- `#262B35` — analogy image frame background.
- macOS window and memory cells only: `#1e222a` body, `#2a303c` header, `#1a1e25` header border, `#8a93a5` filename, dots `#FF5F56`, `#FFBD2E`, `#27C93F`.

---

## 3. Typography

- **Poppins** (400, 600, 700): titles, theory text, bullets, diagram labels, filenames.
- **JetBrains Mono** (400, 700): code, inline code, kickers, quiz buttons, animation captions, slide number.
- Both are loaded from Google Fonts in the template. Do not load other fonts.

Size scale on the 1920×1080 canvas (already set by the template; do not override per slide):
- Body: 44px · `h1`: 2.6em · `h2`: 1.6em · `h3`: 1.05em (weight 400).
- Code: 26px · kicker: 22px.

---

## 4. Canvas and Reveal.js configuration

- Reveal.js **4.3.1**, base theme `night` (fully overridden by the template CSS).
- Canvas: **1920×1080 (16:9 Full HD)**, `margin: 0.06`, `center: true`.
- `transition: 'fade'`, `hash: true`, `slideNumber: 'c/t'`, `controls: true`, `progress: true`.
- Plugins: `RevealHighlight` (code) and `RevealNotes` (speaker view, key **S**).
- Progress bar: 3px, ice blue. Controls: 50% opacity, ice blue on hover.
- Personal logo: fixed top-left, 82×82px, circular crop, 80% opacity (100% on hover). It hides itself automatically if the file is missing.

---

## 5. Dependencies (exact CDN URLs)

In `<head>`:
```
https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Poppins:wght@400;600;700&display=swap
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/reset.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/reveal.min.css
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/theme/night.min.css
https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/styles/atom-one-dark.min.css
https://cdn.jsdelivr.net/npm/@phosphor-icons/web@2.1.2/src/regular/style.css
```

Before `</body>`, in this exact order:
```
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/reveal.min.js
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/plugin/highlight/highlight.min.js
https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/plugin/notes/notes.min.js
https://cdn.jsdelivr.net/npm/mermaid@10.8.0/dist/mermaid.min.js
https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js
https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js
```

Brand icons (no script needed, loaded as images): `https://cdn.simpleicons.org/<slug>/<HEX_WITHOUT_#>`

---

## 6. Base Template (copy verbatim)

Replace only: `[DECK_TITLE]`, the content of `<div class="slides">`, and the `ANIMATIONS` registry entries. Everything else stays byte-for-byte identical.

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[DECK_TITLE] - Debuggeando Ideas</title>

    <!-- Fonts: Poppins (theory) + JetBrains Mono (code) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">

    <!-- Reveal.js -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/reset.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/reveal.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/theme/night.min.css">

    <!-- Code: Atom One Dark -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/styles/atom-one-dark.min.css">

    <!-- Icons: Phosphor (concepts). Simple Icons (brands) are loaded as <img> -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@phosphor-icons/web@2.1.2/src/regular/style.css">

    <style>
        /* ===== NORDIC PALETTE ===== */
        :root {
            --bg-color: #292F3A;
            --text-color: #E5E9F0;
            --struct-color: #4C566A;
            --accent-ice: #88C0D0;
            --accent-sage: #8FBCBB;
            --accent-salmon: #E3A89D;
            --accent-forest: #86A67C;
            --accent-bark: #F5E1CE;

            /* Reveal theme variables (1920x1080 canvas) */
            --r-background-color: var(--bg-color);
            --r-main-font: 'Poppins', sans-serif;
            --r-main-font-size: 44px;
            --r-main-color: var(--text-color);
            --r-heading-font: 'Poppins', sans-serif;
            --r-heading-color: var(--text-color);
            --r-heading-font-weight: 700;
            --r-heading-text-transform: none;
            --r-heading-letter-spacing: -0.01em;
            --r-heading1-size: 2.6em;
            --r-heading2-size: 1.6em;
            --r-heading3-size: 1.05em;
            --r-code-font: 'JetBrains Mono', monospace;
            --r-link-color: var(--accent-ice);
            --r-selection-background-color: var(--accent-ice);
        }

        .reveal {
            font-family: 'Poppins', sans-serif;
            color: var(--text-color);
            background-color: var(--bg-color);
        }
        .reveal h1, .reveal h2, .reveal h3, .reveal h4 {
            font-family: 'Poppins', sans-serif;
            font-weight: 700;
            color: var(--text-color);
            text-transform: none;
            text-shadow: none;
        }
        .reveal h3 { font-weight: 400; color: #C4CBD8; }

        /* ===== TEXT HELPERS ===== */
        .kicker {
            font-family: 'JetBrains Mono', monospace;
            font-size: 22px;
            letter-spacing: 0.12em;
            color: var(--accent-ice);
            margin: 0 0 12px 0 !important;
        }
        .inline-code {
            font-family: 'JetBrains Mono', monospace;
            background-color: var(--struct-color);
            padding: 2px 12px;
            border-radius: 6px;
            color: var(--accent-ice);
            font-size: 0.85em;
        }
        .muted { color: var(--struct-color); }
        .tone-ice { color: var(--accent-ice); }
        .tone-sage { color: var(--accent-sage); }
        .tone-alert { color: var(--accent-salmon); }
        .tone-forest { color: var(--accent-forest); }
        .tone-bark { color: var(--accent-bark); }

        .reveal ul.bullets { list-style: none; margin: 0; padding: 0; }
        .reveal ul.bullets li {
            position: relative;
            padding-left: 44px;
            margin-bottom: 28px;
            line-height: 1.4;
        }
        .reveal ul.bullets li::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0.55em;
            width: 14px;
            height: 14px;
            border-radius: 3px;
            background: var(--accent-ice);
        }

        /* ===== FIXED LOGO ===== */
        .brand-logo {
            position: fixed;
            top: 20px;
            left: 20px;
            z-index: 9999;
            opacity: 0.8;
            transition: opacity 0.3s;
        }
        .brand-logo:hover { opacity: 1; }
        .brand-logo img { display: block; border-radius: 50%; object-fit: cover; }

        /* ===== MINIMAL REVEAL UI ===== */
        .reveal .progress { height: 3px; color: var(--accent-ice); }
        .reveal .controls { color: var(--struct-color); opacity: 0.5; transition: opacity 0.3s; }
        .reveal .controls:hover { opacity: 1; color: var(--accent-ice); }
        .reveal .slide-number {
            font-family: 'JetBrains Mono', monospace;
            background: transparent;
            color: var(--struct-color);
            font-size: 14px;
        }

        /* ===== MACOS CODE WINDOW ===== */
        .mac-window {
            background-color: #1e222a;
            border-radius: 14px;
            box-shadow: 0 30px 60px rgba(0,0,0,0.45);
            border: 1px solid var(--struct-color);
            margin: 30px auto 0;
            width: 100%;
            max-width: 1400px;
            overflow: hidden;
            text-align: left;
        }
        .mac-header {
            background-color: #2a303c;
            padding: 16px 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            border-bottom: 1px solid #1a1e25;
        }
        .mac-dot { width: 16px; height: 16px; border-radius: 50%; }
        .mac-dot.close { background-color: #FF5F56; }
        .mac-dot.min   { background-color: #FFBD2E; }
        .mac-dot.max   { background-color: #27C93F; }
        .mac-title {
            margin-left: auto;
            margin-right: auto;
            color: #8a93a5;
            font-family: 'Poppins', sans-serif;
            font-size: 18px;
            padding-right: 70px;
        }
        .reveal .mac-window pre { margin: 0; box-shadow: none; width: 100%; font-size: 26px; }
        .reveal .mac-window code {
            font-family: 'JetBrains Mono', monospace;
            padding: 30px 36px;
            line-height: 1.55;
            max-height: 720px;
        }
        .reveal .mac-window .hljs-ln-numbers { color: var(--struct-color); }

        /* ===== MERMAID DIAGRAMS ===== */
        .diagram-box {
            max-width: 1500px;
            margin: 30px auto 0;
            padding: 40px;
            border-radius: 14px;
            border: 1px dashed var(--struct-color);
        }
        .diagram-box .mermaid { display: flex; justify-content: center; }

        /* ===== ICONS & ENTITIES ===== */
        .flow-row {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 50px;
            margin: 50px 0 40px;
        }
        .entity { display: flex; flex-direction: column; align-items: center; gap: 18px; font-size: 28px; }
        .entity-icon {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            border: 2px solid var(--struct-color);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 72px;
            color: var(--accent-ice);
        }
        .entity-icon.success { border-color: var(--accent-sage); color: var(--accent-sage); }
        .entity-icon.alert { border-color: var(--accent-salmon); color: var(--accent-salmon); }
        .reveal .entity-icon img { width: 76px; height: 76px; margin: 0; }
        .flow-arrow { font-size: 56px; color: var(--struct-color); }

        .callouts { display: flex; flex-direction: column; gap: 18px; align-items: center; font-size: 34px; }
        .callouts i { margin-right: 14px; vertical-align: -4px; }

        /* ===== DUAL CODING (ANALOGY SPLIT) ===== */
        .analogy-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 90px;
            align-items: center;
            text-align: left;
        }
        .analogy-visual {
            aspect-ratio: 4 / 3;
            border-radius: 18px;
            overflow: hidden;
            border: 1px solid var(--struct-color);
            background: #262B35;
        }
        .reveal .analogy-visual img { width: 100%; height: 100%; max-width: 100%; max-height: 100%; object-fit: cover; margin: 0; }
        .ai-placeholder {
            display: none;
            height: 100%;
            box-sizing: border-box;
            padding: 50px;
            flex-direction: column;
            justify-content: center;
            gap: 22px;
            border: 2px dashed var(--struct-color);
            border-radius: 18px;
        }
        .analogy-visual.is-empty img { display: none; }
        .analogy-visual.is-empty .ai-placeholder { display: flex; }
        .ai-placeholder .ph { font-size: 64px; color: var(--accent-ice); }
        .ai-placeholder .label {
            font-family: 'JetBrains Mono', monospace;
            font-size: 20px;
            color: var(--accent-ice);
            letter-spacing: 0.1em;
        }
        .ai-placeholder .prompt { font-size: 26px; line-height: 1.5; color: #C4CBD8; }
        .ai-placeholder .path { font-family: 'JetBrains Mono', monospace; font-size: 18px; color: var(--struct-color); }

        /* ===== STEP ANIMATIONS (GSAP) ===== */
        .anim-stage { margin-top: 50px; }
        .anim-axis {
            display: flex;
            justify-content: space-between;
            margin: 0 auto 18px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 20px;
            color: var(--struct-color);
        }
        .anim-track { position: relative; margin: 0 auto; }
        .anim-slot, .anim-node {
            position: absolute;
            top: 0;
            border-radius: 16px;
            box-sizing: border-box;
        }
        .anim-slot { border: 2px dashed var(--struct-color); }
        .anim-node {
            left: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: 'JetBrains Mono', monospace;
            font-weight: 700;
            background: var(--struct-color);
            color: var(--text-color);
            border: 3px solid transparent;
            opacity: 0;
        }
        .anim-caption {
            margin-top: 60px;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 28px;
            font-size: 32px;
        }
        .anim-op {
            font-family: 'JetBrains Mono', monospace;
            background: #1e222a;
            border: 1px solid var(--struct-color);
            border-radius: 10px;
            padding: 10px 24px;
            color: var(--accent-ice);
        }
        .anim-step { font-family: 'JetBrains Mono', monospace; font-size: 20px; color: var(--struct-color); margin-top: 24px; }
        .reveal .fragment.step-trigger { display: none; }

        /* Memory cells (variables & pointers) */
        .mem-cell {
            position: absolute;
            top: 0;
            width: 320px;
            height: 220px;
            box-sizing: border-box;
            padding: 20px 0;
            border: 3px solid var(--struct-color);
            border-radius: 16px;
            background: #1e222a;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: space-between;
            opacity: 0;
        }
        .mem-name { font-family: 'JetBrains Mono', monospace; font-size: 28px; color: var(--accent-ice); }
        .mem-value { font-family: 'JetBrains Mono', monospace; font-size: 56px; font-weight: 700; color: var(--text-color); }
        .mem-value.is-addr { font-size: 30px; }
        .mem-addr { font-family: 'JetBrains Mono', monospace; font-size: 18px; color: var(--struct-color); }
        .mem-link {
            position: absolute;
            height: 4px;
            background: var(--accent-ice);
            border-radius: 2px;
            opacity: 0;
        }
        .mem-link.to-left { transform-origin: right center; }
        .mem-link.to-right { transform-origin: left center; }
        .mem-link.to-left::before, .mem-link.to-right::after {
            content: '';
            position: absolute;
            top: -8px;
            border-top: 10px solid transparent;
            border-bottom: 10px solid transparent;
        }
        .mem-link.to-left::before { left: -14px; border-right: 16px solid var(--accent-ice); }
        .mem-link.to-right::after { right: -14px; border-left: 16px solid var(--accent-ice); }

        /* ===== QUIZ ===== */
        .quiz-container { margin-top: 50px; display: flex; flex-direction: column; gap: 22px; align-items: center; }
        .quiz-btn {
            background-color: var(--struct-color);
            color: var(--text-color);
            border: 2px solid transparent;
            padding: 24px 40px;
            border-radius: 12px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 30px;
            cursor: pointer;
            width: 70%;
            transition: all 0.3s ease;
        }
        .quiz-btn:hover { border-color: var(--accent-ice); transform: translateY(-2px); }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }
        .shake-animation {
            animation: shake 0.4s cubic-bezier(.36,.07,.19,.97) both;
            background-color: var(--accent-salmon) !important;
            color: var(--bg-color) !important;
        }
        .correct-animation {
            background-color: var(--accent-sage) !important;
            color: var(--bg-color) !important;
            transform: scale(1.05);
            border-color: transparent !important;
        }

        /* ===== TAKEAWAYS GRID ===== */
        .takeaways {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 40px;
            margin-top: 60px;
            text-align: left;
        }
        .takeaway {
            border: 1px solid var(--struct-color);
            border-radius: 16px;
            padding: 44px 36px;
            font-size: 32px;
            line-height: 1.4;
        }
        .takeaway .ph { display: block; font-size: 60px; color: var(--accent-ice); margin-bottom: 22px; }
        .takeaway.sage .ph { color: var(--accent-sage); }
        .takeaway.forest .ph { color: var(--accent-forest); }
        .takeaway.bark .ph { color: var(--accent-bark); }
    </style>
</head>
<body>

    <a href="#" class="brand-logo">
        <img src="/Users/alejandrocalderon/Pictures/Debuggeando%20Ideas/Logo-V2.png" alt="Debuggeando Ideas" width="82" height="82"
             onerror="this.parentElement.style.display='none'">
    </a>

    <div class="reveal">
        <div class="slides">

            <!-- [SLIDES GO HERE — use only the components from section 7] -->

        </div>
    </div>

    <!-- Dependencies (order matters) -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/reveal.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/plugin/highlight/highlight.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.3.1/plugin/notes/notes.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/mermaid@10.8.0/dist/mermaid.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>

    <script>
        /* ========== 1. REVEAL.JS (16:9 FULL HD) ========== */
        Reveal.initialize({
            width: 1920,
            height: 1080,
            margin: 0.06,
            controls: true,
            progress: true,
            center: true,
            hash: true,
            slideNumber: 'c/t',
            transition: 'fade',
            plugins: [ RevealHighlight, RevealNotes ]
        });

        /* ========== 2. MERMAID (NORDIC PALETTE) ========== */
        mermaid.initialize({
            startOnLoad: false,
            theme: 'base',
            htmlLabels: false,
            flowchart: { htmlLabels: false, padding: 20, nodeSpacing: 60, rankSpacing: 70 },
            themeVariables: {
                primaryColor: '#292F3A',
                primaryTextColor: '#E5E9F0',
                primaryBorderColor: '#88C0D0',
                lineColor: '#8FBCBB',
                secondaryColor: '#4C566A',
                tertiaryColor: '#292F3A',
                edgeLabelBackground: '#292F3A',
                fontFamily: 'Poppins',
                fontSize: '24px'
            }
        });

        // Wait for Poppins before measuring text (prevents clipped labels)
        const fontsReady = Promise.all([
            document.fonts.load('400 24px Poppins'),
            document.fonts.ready
        ]);

        // Diagrams render only when their slide becomes visible
        function renderMermaid(slide) {
            const pending = Array.from(slide.querySelectorAll('.mermaid:not([data-processed]):not([data-queued])'));
            if (!pending.length) return;
            pending.forEach(el => el.setAttribute('data-queued', 'true'));
            fontsReady.then(() => mermaid.run({ nodes: pending }));
        }

        /* ========== 3. STEP ANIMATIONS (GSAP) ========== */
        // Registry: one entry per animated slide. Key = the slide's data-anim value.
        // Each entry: { render(slide, step, instant) } — see section 7.10.
        const ANIMATIONS = {
            // [ANIMATIONS GO HERE]
        };

        function currentStep(slide) {
            return slide.querySelectorAll('.step-trigger.visible').length;
        }

        function runAnimation(slide, instant) {
            const anim = ANIMATIONS[slide.dataset.anim];
            if (!anim) return;
            const step = currentStep(slide);
            anim.render(slide, step, instant);
            const counter = slide.querySelector('.anim-step');
            const total = slide.querySelectorAll('.step-trigger').length;
            if (counter) counter.textContent = 'Paso ' + step + ' / ' + total;
        }

        function onSlide(slide) {
            renderMermaid(slide);
            runAnimation(slide, true);
        }

        Reveal.on('ready', e => onSlide(e.currentSlide));
        Reveal.on('slidechanged', e => onSlide(e.currentSlide));
        Reveal.on('fragmentshown', e => {
            if (e.fragment.classList.contains('step-trigger')) runAnimation(Reveal.getCurrentSlide(), false);
        });
        Reveal.on('fragmenthidden', e => {
            if (e.fragment.classList.contains('step-trigger')) runAnimation(Reveal.getCurrentSlide(), false);
        });

        /* ========== 4. QUIZ ========== */
        function handleQuiz(button, isCorrect) {
            const buttons = button.parentElement.querySelectorAll('.quiz-btn');
            buttons.forEach(btn => {
                btn.classList.remove('shake-animation', 'correct-animation');
                btn.style.opacity = '1';
            });

            if (isCorrect) {
                button.classList.add('correct-animation');
                buttons.forEach(btn => {
                    if (btn !== button) btn.style.opacity = '0.3';
                });
                confetti({
                    particleCount: 150,
                    spread: 70,
                    origin: { y: 0.6 },
                    colors: ['#88C0D0', '#8FBCBB', '#E5E9F0']
                });
            } else {
                button.classList.add('shake-animation');
                setTimeout(() => {
                    button.classList.remove('shake-animation');
                }, 400);
            }
        }
    </script>
</body>
</html>
```

---

## 7. Component library

Every slide is a `<section>`. Build slides ONLY by combining these components.

### 7.1 Slide header (kicker + title)

Use on every content slide. The kicker is a short section label in Spanish, uppercase text typed literally.

```html
<p class="kicker">02 · NOMBRE DE LA SECCIÓN</p>
<h2>Título corto de la diapositiva</h2>
```

### 7.2 Cover slide

```html
<section>
    <p class="kicker">ÁREA · SUBÁREA</p>
    <h1 style="color: var(--accent-ice);">Título del tema</h1>
    <h3>Subtítulo en una línea</h3>
    <p class="muted" style="font-size: 26px; margin-top: 70px;">Debuggeando Ideas</p>
</section>
```

Never show module numbers on the cover or anywhere in the deck.

### 7.3 Bullets

```html
<ul class="bullets">
    <li>Idea corta</li>
    <li>Otra idea con <span class="tone-alert">énfasis de alerta</span></li>
</ul>
```

To reveal bullets one by one, add `class="fragment fade-up"` to each `<li>`.

Emphasis classes: `tone-ice`, `tone-sage`, `tone-alert`, `tone-forest`, `tone-bark`, `muted`, and `<strong>`. Use `tone-forest` / `tone-bark` only per the color roles in section 2.

### 7.4 Inline code (inside text or titles)

```html
<span class="inline-code">@RestController</span>
```

### 7.5 macOS code window

```html
<div class="mac-window">
    <div class="mac-header">
        <div class="mac-dot close"></div>
        <div class="mac-dot min"></div>
        <div class="mac-dot max"></div>
        <div class="mac-title">NombreArchivo.java</div>
    </div>
    <pre><code class="language-java" data-trim data-noescape>
// code here (escape &lt; &gt; &amp;)
    </code></pre>
</div>
```

Rules:
- `class="language-xxx"` must match the language: `java`, `python`, `go`, `javascript`, `typescript`, `sql`, `yaml`, `json`, `bash`, `xml`, `dockerfile`.
- Terminal output uses `language-bash` and the title `Terminal — zsh`.
- `.mac-title` is the real filename the code would live in.
- Maximum ~18 lines per window. Split longer code into several slides.
- Completion problems (see `02_Pedagogy_Style.md`, P9): mark the missing part with `/* ??? */` (use `# ???` in Python and Bash). The next slide repeats the same window with the solution and uses `data-line-numbers` to highlight the completed line.
- Step-by-step line highlighting (each click highlights the next group): add `data-line-numbers`. The first `|` shows the full code, then one group per click:
  ```html
  <pre><code class="language-java" data-trim data-noescape data-line-numbers="|6|10-13">
  ```

### 7.6 Mermaid diagram

```html
<div class="diagram-box">
    <div class="mermaid">
flowchart LR
    C([Cliente]) --> A[API]
    A --> R{¿En caché?}
    R -- HIT --> OK[Respuesta]
    R -- MISS --> DB[(PostgreSQL)]
    linkStyle 2 stroke:#8FBCBB,stroke-width:3px
    linkStyle 3 stroke:#E3A89D,stroke-width:3px
    </div>
</div>
```

Rules:
- Write the diagram text starting at column 0 inside `.mermaid` (no indentation on the first line), as shown.
- Supported types: `flowchart LR` / `flowchart TD`, `sequenceDiagram`, `classDiagram`, `stateDiagram-v2`, `erDiagram`.
- Node labels: max ~4 words. No HTML tags, no `<br>`, no markdown inside labels.
- Wrap labels with special characters (parentheses, colons, slashes) in double quotes: `A["GET /api/users"]`.
- Max ~8 nodes per diagram. If bigger, split into several slides.
- Semantic edge colors with `linkStyle <index>` (index = order the edges are written, starting at 0):
  - success / happy path → `stroke:#8FBCBB,stroke-width:3px`
  - error / failure path → `stroke:#E3A89D,stroke-width:3px`
  - highlighted / active → `stroke:#88C0D0,stroke-width:3px`
- Focal highlighting (flowchart only): by default every node has an ice border. To focus on the active nodes, dim the rest with `classDef` (node ids, comma-separated, no spaces):
  ```
  classDef dim stroke:#4C566A
  classDef active stroke:#88C0D0,stroke-width:3px
  class A,R active
  class C,DB,OK dim
  ```
  Only border colors change; node text stays white. Use it in phased diagrams: each phase slide repeats the same diagram and only that phase's nodes stay ice. `sequenceDiagram` does not support `classDef`: split long sequences into phase slides instead.
- Never set `startOnLoad`, never call `mermaid.init` or `mermaid.run` yourself; the template renders diagrams when their slide opens.

### 7.7 Icons and entity rows

Two icon sources:
- **Phosphor** (concepts, actions, generic objects): `<i class="ph ph-<name>"></i>`. Examples: `ph-user`, `ph-database`, `ph-cloud`, `ph-lightning`, `ph-lock`, `ph-arrow-right`, `ph-code`, `ph-cpu`, `ph-hard-drives`, `ph-warning`, `ph-check-circle`, `ph-x-circle`. Only the regular weight is loaded; do not use `ph-bold`, `ph-fill`, etc.
- **Simple Icons** (brands and technologies): `<img src="https://cdn.simpleicons.org/<slug>/<HEX>" alt="Nombre">`. The color is always a palette hex without `#`: `88C0D0` (default), `8FBCBB` (success) or `E3A89D` (alert). Examples of slugs: `springboot`, `postgresql`, `docker`, `redis`, `python`, `kubernetes`, `mongodb`. If a brand slug may not exist, use a Phosphor icon instead.

Never draw a technology or entity (database, server, Docker, bank) as a plain text box; use an icon.

Entity row (horizontal flow of icons):

```html
<div class="flow-row">
    <div class="entity">
        <div class="entity-icon"><i class="ph ph-user"></i></div>
        <span>Usuario</span>
    </div>
    <i class="ph ph-arrow-right flow-arrow"></i>
    <div class="entity">
        <div class="entity-icon"><img src="https://cdn.simpleicons.org/springboot/88C0D0" alt="Spring Boot"></div>
        <span>API</span>
    </div>
    <i class="ph ph-arrow-right flow-arrow"></i>
    <div class="entity">
        <div class="entity-icon alert"><img src="https://cdn.simpleicons.org/postgresql/E3A89D" alt="PostgreSQL"></div>
        <span>PostgreSQL</span>
    </div>
</div>
```

`.entity-icon` modifiers: none (ice), `success` (sage), `alert` (salmon). Max 5 entities per row.

### 7.8 Callouts (one-line statements revealed by click)

```html
<div class="callouts">
    <p class="fragment fade-up"><i class="ph ph-repeat tone-ice"></i>Primera afirmación</p>
    <p class="fragment fade-up tone-alert"><i class="ph ph-warning"></i>Problema o costo</p>
    <p class="fragment fade-up tone-ice"><i class="ph ph-lightbulb"></i>Idea o solución</p>
</div>
```

### 7.9 Dual coding split (theory + AI analogy image)

Left column: theory (header + bullets) OR a code window OR a diagram. Right column: AI-generated analogy image.

```html
<section>
    <div class="analogy-container">
        <div>
            <p class="kicker">02 · LA ANALOGÍA</p>
            <h2>Título de la analogía</h2>
            <ul class="bullets">
                <li><span class="tone-bark">Objeto real</span> = <span class="tone-ice">concepto</span></li>
                <li><span class="tone-bark">Otro objeto</span> = <span class="tone-ice">otra pieza</span></li>
            </ul>
        </div>
        <div class="analogy-visual">
            <img src="img/[slug].png" alt="Descripción breve de la imagen"
                 onerror="this.parentElement.classList.add('is-empty')">
            <div class="ai-placeholder">
                <i class="ph ph-image"></i>
                <span class="label">IMAGEN IA PENDIENTE</span>
                <p class="prompt">[Prompt en español para generar la imagen: estilo minimalista, tonos azul grisáceo nórdico, describe la escena concreta de la analogía.]</p>
                <span class="path">img/[slug].png</span>
            </div>
        </div>
    </div>
</section>
```

Rules:
- Images live in an `img/` folder next to `index.html`. `[slug]` is lowercase-kebab-case, e.g. `img/lru-escritorio.png`.
- The same `[slug]` appears in the `src` and in `.path`.
- If the image file does not exist yet, the slide automatically shows the prompt instead. Never omit the placeholder.
- Image aspect ratio: 4:3.
- Mapping bullets: the real-world object in `tone-bark`, the concept in `tone-ice`.

### 7.10 Step animation (GSAP, click-driven)

For algorithms, data structures and memory models (variables, pointers, references): elements move one logical step per click (→ / click forward, ← back). No autoplay, ever.

Two kinds of elements, same engine:
- **Block nodes** `.anim-node` — arrays, lists, queues, heaps (example below).
- **Memory cells** `.mem-cell` — variables and pointers with name, value and address (section 7.10b).

**HTML** — the slide has `data-anim="<id>"`, a stage, and N invisible `step-trigger` fragments (N = number of steps after the initial state):

```html
<section data-anim="lru">
    <p class="kicker">04 · EL ALGORITMO</p>
    <h2>LRU paso a paso</h2>

    <div class="anim-stage">
        <div class="anim-axis" style="width: 900px;"><span>← más reciente</span><span>menos reciente →</span></div>
        <div class="anim-track" style="width: 900px; height: 200px;">
            <div class="anim-slot" style="left: 0px;   width: 240px; height: 200px;"></div>
            <div class="anim-slot" style="left: 330px; width: 240px; height: 200px;"></div>
            <div class="anim-slot" style="left: 660px; width: 240px; height: 200px;"></div>
            <div class="anim-node" data-key="A" style="width: 240px; height: 200px; font-size: 80px;">A</div>
            <div class="anim-node" data-key="B" style="width: 240px; height: 200px; font-size: 80px;">B</div>
            <div class="anim-node" data-key="C" style="width: 240px; height: 200px; font-size: 80px;">C</div>
            <div class="anim-node" data-key="D" style="width: 240px; height: 200px; font-size: 80px;">D</div>
        </div>
        <div class="anim-caption">
            <span class="anim-op">—</span>
            <span class="anim-note"></span>
        </div>
        <div class="anim-step"></div>
    </div>

    <!-- One invisible trigger per step -->
    <span class="fragment step-trigger"></span>
    <span class="fragment step-trigger"></span>
    <span class="fragment step-trigger"></span>
    <span class="fragment step-trigger"></span>
    <span class="fragment step-trigger"></span>
</section>
```

Geometry (`width`, `height`, `left`, `font-size`) is set inline per animation, because it depends on the data. Everything else comes from the template classes.

**JavaScript** — add one entry to the `ANIMATIONS` registry in the template:

```js
const ANIMATIONS = {
    lru: (() => {
        // states[0] = initial state; states.length - 1 = number of step-trigger fragments
        const states = [
            { list: [],              op: 'cache(3)', note: 'Caché vacía, capacidad 3' },
            { list: ['A'],           op: 'put(A)',   note: 'Entra al frente' },
            { list: ['B', 'A'],      op: 'put(B)',   note: 'Entra al frente, A se recorre' },
            { list: ['C', 'B', 'A'], op: 'put(C)',   note: 'La caché está llena' },
            { list: ['A', 'C', 'B'], op: 'get(A)',   note: 'HIT: A vuelve al frente', hit: 'A' },
            { list: ['D', 'A', 'C'], op: 'put(D)',   note: 'Se expulsa B, el menos usado', evicted: 'B' }
        ];
        const SLOT_X = [0, 330, 660];

        return {
            render(slide, step, instant) {
                const state = states[step];
                const prev = states[Math.max(step - 1, 0)];
                const d = instant ? 0 : 0.6;

                slide.querySelectorAll('.anim-node').forEach(node => {
                    const key = node.dataset.key;
                    const idx = state.list.indexOf(key);
                    gsap.killTweensOf(node);

                    if (idx >= 0) {
                        const isHit = state.hit === key;
                        gsap.to(node, {
                            x: SLOT_X[idx], y: 0, opacity: 1,
                            backgroundColor: isHit ? '#8FBCBB' : '#4C566A',
                            color: isHit ? '#292F3A' : '#E5E9F0',
                            borderColor: idx === 0 && !isHit ? '#88C0D0' : 'rgba(0,0,0,0)',
                            duration: d, ease: 'power2.inOut'
                        });
                    } else if (state.evicted === key) {
                        gsap.set(node, { x: SLOT_X[prev.list.indexOf(key)], y: 0, opacity: 1 });
                        gsap.timeline()
                            .to(node, { backgroundColor: '#E3A89D', color: '#292F3A', duration: instant ? 0 : 0.3 })
                            .to(node, { y: 160, opacity: 0, duration: d, ease: 'power2.in' }, instant ? 0 : '+=0.3');
                    } else {
                        gsap.to(node, { y: -120, opacity: 0, duration: d, ease: 'power2.out' });
                    }
                });

                slide.querySelector('.anim-op').textContent = state.op;
                const note = slide.querySelector('.anim-note');
                note.textContent = state.note;
                note.style.color = state.evicted ? '#E3A89D' : (state.hit ? '#8FBCBB' : '#E5E9F0');
            }
        };
    })()
};
```

Contract for every animation (mandatory):
1. **State-based, not sequence-based.** Define an array of `states`. `render(slide, step, instant)` draws `states[step]` completely from scratch. It must never depend on what was drawn before. This is what makes going backwards (←) work.
2. `states.length - 1` must equal the number of `<span class="fragment step-trigger">` in the slide.
3. Call `gsap.killTweensOf(node)` before animating each element.
4. When `instant` is `true`, all durations are `0` (used when jumping into the slide).
5. Animate only `x`, `y`, `opacity`, `scale`, `backgroundColor`, `color`, `borderColor`. Use only palette hex values.
6. Color meaning: `#4C566A` default node, `#88C0D0` active/focused/pointer, `#8FBCBB` correct/found/hit/value just changed, `#E3A89D` removed/error/compared-and-rejected/`nil`/panic.
7. Write the current operation in `.anim-op` (code-like, e.g. `swap(i, j)`, `heapify(2)`) and a one-line Spanish explanation in `.anim-note`. The template fills `.anim-step` automatically.
8. Each animated slide has its own `data-anim` id and its own registry entry. Never share DOM ids between slides; always query inside `slide`.

### 7.10b Memory cells (variables and pointers)

Same engine and same contract as 7.10. Use for language fundamentals: values, addresses, pointers, references.

Each cell has a name (top), a value (center) and an address (bottom). A pointer cell shows an address as its value (`is-addr` makes it fit) and a `.mem-link` arrow points to the target cell. Addresses are illustrative; say so in speaker notes.

**HTML** (cell width is fixed at 320px; place cells with `left`, and size the arrow to fill the gap between them):

```html
<section data-anim="punteros">
    <p class="kicker">03 · EN MEMORIA</p>
    <h2>Un apuntador guarda una dirección</h2>

    <div class="anim-stage">
        <div class="anim-track" style="width: 840px; height: 220px;">
            <div class="mem-cell" data-key="x" style="left: 0px;">
                <span class="mem-name">x</span>
                <span class="mem-value">—</span>
                <span class="mem-addr">0xc000012080</span>
            </div>
            <div class="mem-link to-left" style="left: 336px; top: 108px; width: 184px;"></div>
            <div class="mem-cell" data-key="p" style="left: 520px;">
                <span class="mem-name">p</span>
                <span class="mem-value is-addr">—</span>
                <span class="mem-addr">0xc000014090</span>
            </div>
        </div>
        <div class="anim-caption">
            <span class="anim-op">—</span>
            <span class="anim-note"></span>
        </div>
        <div class="anim-step"></div>
    </div>

    <span class="fragment step-trigger"></span>
    <span class="fragment step-trigger"></span>
    <span class="fragment step-trigger"></span>
    <aside class="notes">Las direcciones son ilustrativas: cambian en cada ejecución. Antes de cada clic, pregunta qué valor tendrá x.</aside>
</section>
```

Arrow direction: `to-left` when the pointer cell is to the right of its target (arrowhead on the left end), `to-right` otherwise. The arrow grows from the pointer toward the target.

**JavaScript** (registry entry):

```js
const ANIMATIONS = {
    punteros: (() => {
        const states = [
            { cells: {},                                   link: false, op: '—',       note: 'Memoria vacía' },
            { cells: { x: '10' },                          link: false, op: 'x := 10', note: 'Se reserva x con el valor 10', focus: 'x' },
            { cells: { x: '10', p: '0xc000012080' },       link: true,  op: 'p := &x', note: 'p guarda la dirección de x', focus: 'p' },
            { cells: { x: '20', p: '0xc000012080' },       link: true,  op: '*p = 20', note: 'Se escribe en x a través de p', focus: 'p', changed: 'x' }
        ];

        return {
            render(slide, step, instant) {
                const s = states[step];
                const d = instant ? 0 : 0.5;

                slide.querySelectorAll('.mem-cell').forEach(cell => {
                    const key = cell.dataset.key;
                    const val = s.cells[key];
                    gsap.killTweensOf(cell);

                    if (val === undefined) {
                        gsap.to(cell, { opacity: 0, y: -40, duration: d });
                        return;
                    }
                    const valueEl = cell.querySelector('.mem-value');
                    valueEl.textContent = val;
                    const border = s.nil === key ? '#E3A89D'
                                 : s.changed === key ? '#8FBCBB'
                                 : s.focus === key ? '#88C0D0' : '#4C566A';
                    gsap.to(cell, { opacity: 1, y: 0, borderColor: border, duration: d, ease: 'power2.out' });
                    if (s.changed === key && !instant) {
                        gsap.fromTo(valueEl, { scale: 1.4 }, { scale: 1, duration: 0.5, ease: 'back.out(2)' });
                    }
                });

                slide.querySelectorAll('.mem-link').forEach(link => {
                    gsap.killTweensOf(link);
                    gsap.to(link, { opacity: s.link ? 1 : 0, scaleX: s.link ? 1 : 0, duration: d });
                });

                slide.querySelector('.anim-op').textContent = s.op;
                const note = slide.querySelector('.anim-note');
                note.textContent = s.note;
                note.style.color = s.nil ? '#E3A89D' : (s.changed ? '#8FBCBB' : '#E5E9F0');
            }
        };
    })()
};
```

State fields: `cells` (key → displayed value; missing key = cell hidden), `link` (arrow visible), `focus` (ice border), `changed` (sage border + pop), `nil` (salmon border, for `nil` values and panics), `op`, `note`. For more than one pointer, give each `.mem-link` a `data-key` and turn `link` into an object (`{ p: true, q: false }`).

### 7.11 Quiz

```html
<section>
    <p class="kicker">EVALUACIÓN RÁPIDA</p>
    <h2>Pregunta corta</h2>
    <p>Contexto opcional con <span class="inline-code">código</span>.</p>
    <div class="quiz-container">
        <button class="quiz-btn" onclick="handleQuiz(this, false)">Opción incorrecta</button>
        <button class="quiz-btn" onclick="handleQuiz(this, true)">Opción correcta</button>
        <button class="quiz-btn" onclick="handleQuiz(this, false)">Opción incorrecta</button>
    </div>
</section>
```

Rules: 3 or 4 options, exactly one with `true`, and do not always put the correct one in the same position. Behavior (already implemented): correct → sage + scale + palette confetti + other options fade to 30%; wrong → salmon + shake, then resets so the student can retry.

### 7.12 Takeaways grid (summary)

```html
<section>
    <p class="kicker">RESUMEN</p>
    <h2>Tres ideas para llevarte</h2>
    <div class="takeaways">
        <div class="takeaway"><i class="ph ph-lightning"></i>Idea clave 1</div>
        <div class="takeaway bark"><i class="ph ph-clock-counter-clockwise"></i>Idea clave 2</div>
        <div class="takeaway forest"><i class="ph ph-code"></i>Idea clave 3</div>
    </div>
</section>
```

Exactly 3 cards. Default palette: first card ice (no modifier), second `bark`, third `forest` (the most practical idea). `sage` stays available but is not the default.

### 7.13 Speaker notes

**Required on every content slide** (everything except the cover), at the end of the `<section>`. Visible only in speaker view (key **S**). `02_Pedagogy_Style.md` defines what goes in them: what to say, the prediction question before each step, where an analogy breaks, and why each quiz distractor is wrong.

```html
<aside class="notes">Qué decir o preguntar en esta diapositiva.</aside>
```

---

## 8. Final checklist (verify before delivering)

- [ ] One `index.html`; the template's `<head>`, CSS, logo block, CDN scripts and JS sections are unchanged.
- [ ] Only components from section 7; no new classes, colors, fonts or libraries.
- [ ] Every code block: inside `.mac-window`, correct `language-xxx`, `data-trim data-noescape`, `<` `>` `&` escaped.
- [ ] Every Mermaid diagram: inside `.diagram-box`, first line at column 0, short plain labels, ≤ 8 nodes.
- [ ] Every animated slide: `data-anim` id matches an `ANIMATIONS` key; step-trigger count = `states.length - 1`; `render` is state-based.
- [ ] Every analogy image: `img/<slug>.png` with the placeholder and Spanish prompt included.
- [ ] Every quiz: exactly one `handleQuiz(this, true)`.
- [ ] Every content slide has `<aside class="notes">`.
- [ ] Memory and pointer animations use `.mem-cell` (7.10b); arrays and lists use `.anim-node` (7.10).
- [ ] Completion problems mark the gap with `/* ??? */` and are followed by a solution slide.
- [ ] Focal Mermaid highlighting uses only the `dim` / `active` classDefs from 7.6.
- [ ] Forest and bark used only per section 2 roles (max 1–2 per slide, never for success/error).
- [ ] No module number anywhere.
- [ ] All visible text is in Spanish; no emojis.