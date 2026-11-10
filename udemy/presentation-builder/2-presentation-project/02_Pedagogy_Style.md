# 02 — Pedagogy Style (How to teach with the engine)

Project: **Debuggeando Ideas** — technical teaching presentations.

## 0. How this file works with the Tech Engine

There are two complementary files. Read both before building any presentation.

| File | Answers | Never answers |
|---|---|---|
| `01_Tech_Engine.md` | HOW to build it: HTML, CSS, JS, components (section 7), template | What to teach or in which order |
| `02_Pedagogy_Style.md` (this file) | WHAT to put on each slide, WHY, and WHICH component to use | How to write the code of a component |

Rule of use:
1. Use this file to decide the **sequence of slides** and the **pedagogical purpose** of each one.
2. For each slide, pick the component from the mapping tables below. Component references like **[7.5]** point to section 7 of `01_Tech_Engine.md`.
3. Build the slide by copying that component exactly as defined in `01_Tech_Engine.md`.

If a pedagogical idea here seems to need a component that does not exist in `01_Tech_Engine.md`, do NOT invent one. Use the closest existing component and mention the gap to the instructor.

Subject-specific tool rules (e.g. "algorithms use GSAP, not Mermaid") live in `03_Course_Domains.md`. When both files apply, `03` decides the tool and this file decides how to use it.

---

## 1. Core principles (evidence-based)

Each principle has: the rule, why it works, and how it is implemented with the engine.

### P1. Dual coding — words + meaningful visuals
- **Rule:** Every concept is shown with a visual (diagram, icon, animation or analogy image) next to a minimal verbal/code form. Never text alone.
- **Why:** Verbal and visual information are processed through separate channels (Paivio); combining them improves understanding and recall. The benefit comes from *meaningful* visuals, not from adding pictures.
- **Implement:** Dual coding split **[7.9]**, Mermaid **[7.6]**, entity rows **[7.7]**, step animation **[7.10]**.

### P2. Coherence — no decorative content (avoid "seductive details")
- **Rule:** Every image, icon, animation and word must explain part of the concept. If removing an element does not hurt understanding, remove it.
- **Why:** Interesting but irrelevant material (decorative images, anecdotes, effects) consumes working memory and reduces learning.
- **Implement:**
  - AI analogy images **[7.9]** are only allowed when every main element of the image maps to a part of the concept (see section 4).
  - Icons **[7.7]** represent real entities of the system, never decoration.
  - No animations that do not represent a real change of state.

### P3. Cognitive load reduction — minimal text
- **Rule:** Max 3–4 bullets per slide, each max ~8 words. Keywords, not sentences. Zero paragraphs.
- **Why:** Working memory is very limited; the slide supports the speaker, it does not replace them.
- **Implement:** Bullets **[7.3]**, callouts **[7.8]**, slide header **[7.1]**.

### P4. Redundancy — don't show what you will say
- **Rule:** The slide holds the visual and the keywords; the full explanation is spoken. Put the spoken explanation in speaker notes, not on the slide.
- **Why:** Reading identical text on screen while hearing it overloads the same verbal channel and reduces learning.
- **Implement:** Speaker notes **[7.13]** on every content slide.

### P5. Split-attention & contiguity — explanation inside the visual
- **Rule:** Labels go ON the diagram (edge labels, node names) or IN the code (short comments on the key line). No footnotes, no legends far from the element, no "see previous slide".
- **Why:** Integrating text into diagrams reduces cognitive load and study time compared with separated text and graphics.
- **Implement:** Mermaid edge labels **[7.6]**, inline code comments in the macOS window **[7.5]**, `.anim-op` / `.anim-note` captions directly under the animation **[7.10]**.

### P6. Signaling — guide the eye
- **Rule:** In every slide, the ONE thing that matters right now is visually highlighted; the rest is neutral or dimmed.
- **Why:** Cues that highlight the essential material help learners select and organize it.
- **Implement (color semantics, always the same meaning):**
  - `#88C0D0` ice = active / focus / "look here"
  - `#8FBCBB` sage = correct / success / happy path
  - `#E3A89D` salmon = error / failure / removed / bad path
  - `#4C566A` structural = inactive / background context
- **Tools:** Line-by-line code highlighting with `data-line-numbers` **[7.5]**; colored edges with `linkStyle` **[7.6]**; color states in animations **[7.10]**; `tone-*` classes in text **[7.3]**.

### P7. Segmenting — one idea per slide, learner-paced
- **Rule:** One idea per slide. Big processes are split into consecutive slides. Everything advances by the instructor's click; nothing autoplays.
- **Why:** Learners understand better when material is presented in user-paced segments rather than as one continuous unit.
- **Implement:**
  - Diagrams with more than ~8 nodes → split into phases, one slide each (e.g. 1. Request & auth, 2. Processing, 3. Response). Each phase slide shows the same kicker with the phase number.
  - Fragments for progressive reveal **[7.3] [7.8]**.
  - Step animations, one state per click, reversible **[7.10]**.

### P8. Pre-training — names before mechanisms
- **Rule:** Before a complex diagram or animation, show a slide that introduces the main components (name + icon + one-line role).
- **Why:** Learners process a complex system better when they already know the names and roles of its parts.
- **Implement:** Entity row **[7.7]** with up to 5 entities, optionally with callouts **[7.8]**.

### P9. Worked examples → completion (faded guidance)
- **Rule:** Code is taught in two moves: (1) a fully worked example, explained line by line; (2) a similar example with a missing piece the students complete before the solution is revealed.
- **Why:** For novices, studying worked examples is more effective than solving problems from scratch; guidance is then gradually removed.
- **Implement:**
  - Worked example: macOS window with `data-line-numbers` steps **[7.5]**.
  - Completion problem: same component, with the missing part written as `/* ??? */` (or `# ???` in Python). The next slide shows the same window with the solution and the completed line highlighted.

### P10. Expertise reversal — adapt the scaffolding
- **Rule:** The more advanced the audience or module, the less scaffolding: fewer analogies, fewer pre-training slides, more direct code and diagrams.
- **Why:** Support that helps novices becomes redundant and harmful for experienced learners.
- **Implement:** Ask/assume the level from the instructor's request. Beginner → analogies + pre-training + worked examples. Advanced → skip analogies unless the concept is genuinely new.

### P11. Prediction before reveal (generative learning)
- **Rule:** Before each important step of an animation, diagram phase or highlighted code line, the instructor asks the class to predict what happens next.
- **Why:** Actively generating an answer before seeing it engages deeper processing than passive watching.
- **Implement:** In step animations **[7.10]** and code steps **[7.5]**, write the prediction question in speaker notes **[7.13]** (e.g. "Pregunta: ¿qué elemento sale cuando entra D?").

### P12. Retrieval practice with immediate feedback
- **Rule:** After each dense block (roughly every 8–12 content slides), insert one quiz. Optionally start a follow-up class with one recap quiz from the previous class.
- **Why:** Retrieval practice improves retention in real classrooms; multiple-choice questions have shown consistent benefits.
- **Implement:** Quiz **[7.11]**. Design rules in section 5.

---

## 2. Content type → component (decision table)

Use this table to pick the component for each slide.

| What you need to show | Component | Principles |
|---|---|---|
| Opening of the deck | Cover **[7.2]** | — |
| Why this topic matters / the problem | Entity row **[7.7]** + callouts **[7.8]** | P1, P7 |
| Names and roles of the parts of a system | Entity row **[7.7]** (pre-training) | P8 |
| Abstract concept with no obvious visual | Dual coding split **[7.9]** | P1, P2 |
| Architecture, flow between services, request lifecycle | Mermaid **[7.6]** (split into phases if > 8 nodes) | P5, P6, P7 |
| Algorithm or data structure changing state | Step animation **[7.10]** | P6, P7, P11 |
| How to implement it | macOS window with line steps **[7.5]** | P5, P6, P9 |
| Let students try | Completion problem in macOS window **[7.5]** | P9, P11 |
| Terminal command or output | macOS window, `language-bash` **[7.5]** | — |
| Check understanding | Quiz **[7.11]** | P12 |
| Close the topic | Takeaways grid **[7.12]** | P3 |

---

## 3. Standard lesson arc (default slide sequence)

Use this order by default. Skip steps that do not apply (e.g. no code in a pure architecture lesson). Mark skipped steps in the draft.

1. **Cover** **[7.2]**
2. **Hook — the problem** **[7.7] + [7.8]**: what goes wrong without this concept.
3. **Pre-training** **[7.7]**: names and roles of the parts (beginners).
4. **Concept / analogy** **[7.9]**: only if the concept is abstract (see section 4).
5. **Mechanism** **[7.6]** or **[7.10]**: how it works, step by step.
6. **Implementation — worked example** **[7.5]**: full code, line by line.
7. **Completion problem** **[7.5]**: students fill the gap, then reveal.
8. **Quiz** **[7.11]**.
9. **Takeaways** **[7.12]**: exactly 3 ideas.

For long topics, repeat steps 4–8 per sub-topic, then one final takeaways slide.

---

## 4. Analogy rules (for **[7.9]**)

An analogy image is a teaching tool, not decoration (P2). Use one only when ALL of these are true:
1. The concept is abstract (no natural diagram: e.g. embeddings, cache eviction, concurrency).
2. A real-world scene exists where each main element maps to a part of the concept.
3. The mapping can be stated in 2–3 bullets on the left side.

Writing the analogy:
- **Left side (theory):** header + 2–3 bullets that state the mapping explicitly (e.g. "Escritorio = caché", "Estante = base de datos").
- **Right side (image):** AI-generated image. The prompt (Spanish) describes a concrete scene, minimal style, Nordic blue-gray tones, and includes every mapped element. No text inside the image.
- **Limits:** In speaker notes, state where the analogy breaks (e.g. "En la caché real no hay 'polvo': el criterio es el último acceso, no el tiempo en el escritorio").
- Max one analogy per sub-topic. Never two analogies for the same concept.

---

## 5. Quiz design rules (for **[7.11]**)

- 1 question, 3 options (4 max), exactly one correct.
- The question checks the concept just taught, ideally applying it to a new case (not repeating a sentence from a slide).
- Wrong options are **real misconceptions**, not absurd answers. Example: for LRU, "se expulsa el más antiguo en entrar" is a good distractor because it confuses LRU with FIFO.
- Vary the position of the correct option across quizzes.
- Speaker notes explain why each wrong option is wrong.

---

## 6. Writing rules for slide content

- All visible text in Spanish, professional and conversational ("tú"), never academic.
- Titles: max ~7 words. Prefer a short statement that says the point (e.g. "LRU expulsa lo menos usado") over a generic label ("Funcionamiento de LRU").
- Kicker: section number + short label, e.g. `03 · ARQUITECTURA`.
- Bullets: max 3–4, max ~8 words each, no final period.
- Code: max ~18 lines per window; comments in Spanish only on key lines.
- Diagrams: max ~8 nodes; labels max ~4 words.
- No emojis, no exclamation marks, no filler phrases ("Como podemos ver…").
- Do not state unverified numbers (latencies, percentages) as facts. If a number is illustrative, say so in speaker notes.

---

## 7. Phase 1 draft format (Markdown, before HTML)

The draft must already show which component each slide uses, so the instructor can approve the pedagogy before any HTML is generated. Use this template per slide:

```markdown
### Slide N — [Título]
- **Purpose:** [Hook | Pre-training | Concept | Mechanism | Worked example | Completion | Quiz | Takeaways]
- **Component:** [7.x name]
- **Kicker:** 0N · ETIQUETA
- **On screen:** [bullets / callouts / labels, max 3–4]
- **Code:** [file name + code, or "—"]
- **Diagram / animation:** [Mermaid text, or list of animation states, or "—"]
- **Analogy image:** [prompt + slug, or "—"]
- **Quiz:** [question, options, correct one, why distractors are wrong, or "—"]
- **Speaker notes:** [what to say, prediction question, where the analogy breaks]
```

---

## 8. Pedagogical checklist (verify in the draft AND in the final HTML)

- [ ] Every slide has one clear purpose from the lesson arc and one component from the decision table.
- [ ] No slide has more than 3–4 short bullets; no paragraphs.
- [ ] Every visual explains something; nothing is decorative.
- [ ] Every analogy has an explicit mapping and its limits in speaker notes.
- [ ] Diagrams > 8 nodes were split into phases.
- [ ] Every animation and code walkthrough advances by click, with prediction questions in notes.
- [ ] Code is taught as worked example → completion problem (when the lesson includes code).
- [ ] At least one quiz per dense block, with misconception-based distractors.
- [ ] The deck ends with exactly 3 takeaways.
- [ ] Color meaning is consistent: ice = focus, sage = success, salmon = error, structural = context.