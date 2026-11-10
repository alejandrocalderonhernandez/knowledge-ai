<!-- role: manifest | scope: framework | version: 1.0 -->
<!-- audience: AI first, human second | read before any kata file -->

# AI Kata Framework — Manifest v1

## 0. Purpose and scope

The AI Kata Framework is a way for a **human and an AI to build projects together** with a fixed method: which documents exist, who writes each one, in which order they are read, and how a concrete deliverable comes out of them.

**v1 solves four problems only:**

1. Understanding the human: collecting inputs, asking only what is missing, never inventing.
2. Static files: rules and builders that do not change between projects.
3. Output files: dynamic documents generated from rules + human inputs.
4. Project prompt: the instruction that binds the files together inside a chat project.

Everything else is out of scope (see section 13).

## 1. Core formula

```
Rules (HOW) + Context (WHAT) + Brief (THIS TIME) = Deliverable
```

- Change project → regenerate the context; rules stay.
- Change rules → context stays; deliverables improve.
- Change the ask → only the brief changes.

## 2. Terms

| Term | Definition |
|---|---|
| Kata | A reusable domain workflow: its rules, its builders and the deliverables it produces (e.g. "technical presentations"). |
| Framework | The method shared by all katas. This file. |
| Rule file | Static. Says HOW to produce or teach something. Constant across projects. |
| Builder | Static. Rules to GENERATE one dynamic file from human inputs. |
| Input | Raw material from the human: PRD, syllabus, notes, guides. Any format. |
| Context file | Dynamic. Output of a builder. Says WHAT one project is about. |
| Brief | Ephemeral. Sent in chat. Says WHAT this deliverable covers and how deep. Not stored. |
| Deliverable | The final product (a deck, a doc, code). |
| Project prompt | The instructions of a chat project. Tells the AI which files exist and how to combine them. |
| Stage | Stage 1 = build the context. Stage 2 = use it to produce deliverables. |

## 3. File taxonomy

| Type | Audience | Static / dynamic | Written by | Example |
|---|---|---|---|---|
| README | Human | Static per folder | Human (AI may draft) | `README.md` |
| Manifest | AI + human | Static | Human + AI | `MANIFEST.md` (this file) |
| Rule file | AI | Static | Human + AI, versioned | `01_Tech_Engine.md` |
| Builder | AI | Static | Human + AI, versioned | `course-context-builder.md` |
| Input | AI | Per project | Human | `course-business.md` |
| Context file | AI | Dynamic | AI via builder | `03_Course_Context.md` |
| Project prompt | AI | Per project | AI via template (section 10) | Project instructions |
| Brief | AI | Ephemeral | Human, in chat | "Presentation for E10 RAG" |

**Rule of audiences:** `README.md` is the only file written for humans. It is short. Every other file is written for the AI: strict structure, fixed fields, one line per fact.

## 4. Naming and ordering

- **Numeric prefixes** set reading order and priority: folders and files start with `01_`, `02_`, `03_`…
- Lower number = read first. Constant files get low numbers; dynamic files come after the rules they depend on.
- Every folder has one `README.md` (human) and may have one `MANIFEST.md` (AI).
- Builders are named `<output>-builder.md` (e.g. `course-context-builder.md`).
- Versions live in Git (tags, commits). File names do not carry versions; the role header does.
- Structure and field names in English. Content that reaches the final audience in the deliverable language.

### Role header (required in every AI file)

```
<!-- role: <rule|builder|output|manifest> | stage: <n of m> | output: <file> -->
<!-- read with: <files this one depends on> -->
```

## 5. Stages

| Stage | Inputs | Process | Output |
|---|---|---|---|
| 1 — Build | Builder + human inputs | Builder workflow (section 7) | Context file |
| 2 — Use | Rule files + context file + brief | Project prompt (section 10) | Deliverable |

Stage 1 runs once per project (and again when the project changes). Stage 2 runs once per deliverable.

## 6. Priority and conflicts

| Question | Source of truth |
|---|---|
| Project facts, names, versions, IDs | Context file |
| Topic, depth, focus of this deliverable | Brief |
| Sequencing and method | Domain rule file (e.g. pedagogy) |
| Construction and components | Technical rule file (e.g. engine) |

- If two sources contradict, the AI says so **in one line before the draft** and does not resolve it silently.
- A brief never overrides project facts; it may only narrow them.

## 7. Builder contract

Every builder must contain these sections, in this order:

1. Role header.
2. **What you are doing:** one job, one output file, and what is out of its scope.
3. **File map:** table with every file of the kata, its role, whether it changes per project, and whether the AI has it now.
4. **How the output is used:** who reads it in Stage 2 and for what.
5. **Workflow** (standard, below).
6. **Interface contracts:** the minimum the builder must know about other files (IDs only).
7. **Content rules:** size budget, forbidden content, language, `[VERIFY]` policy.
8. **Output template:** the exact skeleton of the generated file.
9. **Self-check:** checklist run before delivering.

### Standard workflow

| Step | Rule |
|---|---|
| 1. Acknowledge | Human's language, max 3 lines: ready, waiting for inputs. |
| 2. Receive | Inputs may span several messages. Do not generate until the human says so ("listo", "genera"). |
| 3. Gap check | Max 5 numbered one-line questions, only for REQUIRED fields that cannot be derived. Everything else → `[VERIFY]`. |
| 4. Generate | Use the output template exactly. |
| 5. Report | Max 5 lines: size, number of `[VERIFY]`, new items added, what was left out and why. |

## 8. Content rules (all AI files)

- **Summary, not manual.** One line per item. No paragraphs where a table fits.
- **Size budget** declared by each builder (reference: context files 8–15 KB). Over budget → cut explanations, keep names and facts.
- **Never invent.** Every fact comes from the inputs or an official source. If unsure → append `[VERIFY]` and list it in the file's "Open items".
- **Exact names.** Versions, classes, endpoints, ports and IDs are copied exactly as in the inputs.
- **No leakage between layers.** A context file holds no method; a rule file holds no project facts; a brief holds no rules.
- **Interface contracts.** A file only references IDs defined by another file (e.g. component `7.6`). Never invent IDs.

## 9. Human–AI protocol

- The human owns decisions; the AI owns structure and consistency.
- The AI asks only what changes the result, and at most 5 questions at once.
- The AI marks assumptions instead of stopping on them.
- The AI reports briefly and does not recap its steps.
- Feedback from the human is folded back into the rule or builder file, then versioned in Git. Lessons live in files, not in chat history.

## 10. Project prompt

The project prompt is the instruction of a chat project (Stage 2). It is short and points to files; it does not repeat their content.

### Template

```
You work inside the AI Kata Framework, kata: <kata name>.
Files: <01_...> (HOW to build) · <02_...> (HOW to <method>) · <03_...> (WHAT the project is).
For each request I send a brief: <brief fields>.
Priority: facts → 03 · scope → brief · method → 02 · construction → 01.
If the brief contradicts 03, say it in one line before the draft.
Never invent facts; mark doubts with [VERIFY].
Reply in <deck language>. Deliver: <deliverable format>.
```

## 11. Surfaces

| Surface | Used for | Reads |
|---|---|---|
| Chat project | Iterating with the human: Stage 1 and Stage 2 | Same files, uploaded as project knowledge |
| Claude Code | Executing: generating files, versioning, automation | Same files, from the repo |

Both surfaces read the **same files**. Context is never kept only in a chat; if it matters, it goes into a file.
v1 defines the chat project flow. Claude Code skills and agents are planned for v2 (section 13).

## 12. Reference kata — Technical presentations (Debuggeando Ideas)

| File | Type | Stage |
|---|---|---|
| `01_Tech_Engine.md` | Rule — HOW to build the HTML (components 7.x) | 2 |
| `02_Pedagogy_Style.md` | Rule — HOW to teach (principles, lesson arc) | 2 |
| `course-context-builder.md` | Builder → `03_Course_Context.md` | 1 |
| `course-business.md`, `course-technical.md` | Inputs (first project: *Java + IA: agentes, RAG y MCP en local*) | 1 |
| `03_Course_Context.md` | Context file | 2 |
| Brief in chat | Topic, depth, analogies, focus | 2 |

## 13. Out of scope for v1 (open problems)

1. Repository layout for framework, katas and projects.
2. Mapping katas to Claude Code skills (`SKILL.md`) and agents.
3. Portability to other agents (Codex, Antigravity) via `AGENTS.md` and `.agents/skills/`.
4. Versioning policy: semver for rules and builders, changelog format.
5. Validation: automatic checks of role headers, size budgets and `[VERIFY]` lists.
6. A builder that creates new katas (a "kata builder").
7. Feedback loop: how deliverable reviews update rule files.

## 14. Self-check for a new kata

- [ ] Has a `README.md` for humans, short.
- [ ] Every AI file starts with a role header.
- [ ] Rule files contain no project facts.
- [ ] Each dynamic file has exactly one builder.
- [ ] Builders follow the contract of section 7.
- [ ] Priority table (section 6) is filled for the kata.
- [ ] A project prompt exists, built from the template in section 10.
- [ ] Files are numbered in reading order.