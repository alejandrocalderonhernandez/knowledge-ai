# 03 — Course Domains (What to teach and with which tools)

Project: **Debuggeando Ideas** — technical teaching presentations.

## 0. How this file works with the other files

| File | Answers |
|---|---|
| `00_Orchestrator_Flow.md` | The workflow (Phase 1 draft → approval → Phase 2 HTML) |
| `01_Tech_Engine.md` | HOW to build each component in HTML/CSS/JS |
| `02_Pedagogy_Style.md` | HOW to teach: slide sequence, principles, which component for which purpose |
| `03_Course_Domains.md` (this file) | WHAT to teach: topics, scope, correct technical facts, sources, and which tool each subject uses |

Priority when files overlap:
- **Technical facts and scope** → this file wins. Do not add topics outside the defined scope; do not contradict the "Key facts" section.
- **Which visual tool to use for a subject** → this file (section 1) wins.
- **How to sequence and present it** → `02_Pedagogy_Style.md`.
- **How to code it** → `01_Tech_Engine.md`.

If a fact needed for the lesson is NOT in this file and NOT in the listed sources, do not invent it: mark it in the draft as `[VERIFY]` for the instructor.

---

## 1. Domain tool rules (apply to every course)

| Domain | Examples | Main tool | Forbidden |
|---|---|---|---|
| Architecture & system design | Microservices, networks, auth flows, caching layers | Mermaid **[7.6]** (split into phases if > 8 nodes) | GSAP for flows |
| Algorithms & data structures | LeetCode, Min-Heap, sorting, graphs, linked lists | Step animation GSAP **[7.10]** | Mermaid |
| Language fundamentals & memory | Pointers, references, value vs reference, stack/heap | Step animation GSAP **[7.10]** as a memory diagram + code **[7.5]** | Mermaid for memory |
| Backend programming | Java, Spring, Python, Go services | macOS code windows **[7.5]** with line steps; quick transitions to code | Long theory before code |

Component numbers in **[ ]** refer to section 7 of `01_Tech_Engine.md`.

---

## 2. Active course

### 2.1 Course card

| Field | Value |
|---|---|
| Course | Fundamentos de Go |
| Topic of this deck | Apuntadores (punteros) en Go |
| Domain | Language fundamentals & memory |
| Level | Beginner (knows Go variables, functions and structs; never used pointers) |
| Language of slides | Spanish |
| Language of code | Go (current stable version), highlighted with `class="language-go"` |
| Target length | 10–14 slides, ~30 minutes |
| PRD | None for this course |

### 2.2 Learning objectives

By the end of the deck the student can:
1. Explain what a pointer is: a value that holds the memory address of another value.
2. Read and write the syntax `*T` (type), `&x` (address-of) and `*p` (dereference) without confusing the two uses of `*`.
3. Predict the output of a program that modifies a variable through a pointer.
4. Explain why a function needs a pointer parameter to modify the caller's variable (Go passes everything by value).
5. Recognize the zero value `nil` and what happens when a `nil` pointer is dereferenced.

### 2.3 Scope

**In scope:**
- Pointer type `*T`, operators `&` and `*`.
- Zero value `nil` and nil dereference panic.
- Modifying a variable through a pointer.
- Pass by value vs passing a pointer to a function.
- Pointers to structs and the shortcut `p.Campo` instead of `(*p).Campo`.
- `new(T)` as an alternative way to get a pointer (one slide max).

**Out of scope (do NOT include):**
- `unsafe` package and `uintptr`.
- Escape analysis details and garbage collector internals (at most one sentence in speaker notes).
- Slices, maps and channels internals (headers, backing arrays).
- Method receivers in depth (value vs pointer receivers). Can be mentioned as "próximo tema" in takeaways.
- Concurrency and pointers.

### 2.4 Key facts (source of truth — do not contradict)

1. A pointer holds the memory address of a value.
2. The type `*T` is a pointer to a value of type `T`. Its zero value is `nil`.
3. `&x` produces a pointer to `x`.
4. `*p` accesses (reads or writes) the value the pointer points to. This is called dereferencing.
5. `*` has two roles: in a **type** (`var p *int`) it means "pointer to"; in an **expression** (`*p = 20`) it means "the value at that address".
6. Go has **no pointer arithmetic** (unlike C). `p++` on a pointer does not compile.
7. Go passes all arguments **by value**. Passing a pointer copies the address, so the function can modify the original value through it.
8. For a pointer to a struct, `p.X` is allowed as a shortcut for `(*p).X`.
9. Dereferencing a `nil` pointer compiles but causes a **runtime panic** (`invalid memory address or nil pointer dereference`).
10. Returning a pointer to a local variable from a function is safe in Go; the compiler keeps the value alive (unlike C).
11. `new(T)` allocates a zero value of type `T` and returns a `*T`.

### 2.5 Common misconceptions (use as quiz distractors)

| Misconception | Correct idea |
|---|---|
| "Go pasa los valores por referencia" | Go always passes by value; a pointer is a copied address |
| "`*` siempre significa desreferenciar" | In a type, `*int` means "pointer to int" |
| "Puedo hacer `p++` para avanzar al siguiente valor" | Go has no pointer arithmetic |
| "Desreferenciar `nil` da error de compilación" | It compiles; it panics at runtime |
| "Retornar un puntero a una variable local es peligroso" | It is safe in Go |
| "`p` y `*p` son lo mismo" | `p` is the address; `*p` is the value stored there |

### 2.6 Code conventions for this topic

- Every complete example is runnable: `package main`, `import "fmt"`, `func main()`.
- Use simple names: `x`, `p`, `edad`, `persona`. Spanish names for variables are allowed; Go keywords stay in English.
- Print with `fmt.Println`. Show the expected output in a separate macOS window **[7.5]** with `language-bash`, title `Terminal — zsh`, and the command `go run main.go`.
- Max ~15 lines per code window.
- Completion problems (see `02_Pedagogy_Style.md`, P9) mark the gap with `/* ??? */`.

Reference snippet (correct, use as base):

```go
package main

import "fmt"

func duplicar(n *int) {
    *n = *n * 2
}

func main() {
    x := 10
    p := &x
    *p = 20
    duplicar(&x)
    fmt.Println(x) // 40
}
```

### 2.7 Visual conventions for this topic

Memory is shown with a GSAP step animation **[7.10]** ("memory boxes"):
- Each variable is a box with three parts: **name** (top), **value** (center, large), **address** (bottom, small, JetBrains Mono).
- A pointer box shows an address as its value, and an arrow or highlight connects it to the box it points to.
- Addresses are illustrative (e.g. `0xc000012080`). Say in speaker notes that real addresses change on every run.
- Colors: `#88C0D0` the box currently being read or written; `#8FBCBB` the value after a successful change; `#E3A89D` `nil` / panic; `#4C566A` inactive boxes.

Suggested animation states for the core example:
1. Empty memory.
2. `x := 10` → box `x` with value `10`.
3. `p := &x` → box `p` with value `0xc000012080` (the address of `x`), linked to `x`.
4. `*p = 20` → `p` highlighted, then `x` changes to `20`.
5. `duplicar(&x)` → copy of the address enters the function; `x` changes to `40`.

### 2.8 Suggested analogy (optional, beginners)

- **Scene:** a hotel. The room is the value; the room number written on a card is the pointer.
- **Mapping:** room = variable value · room number = address · card with the number = pointer · going to the room = dereference.
- **Limits (speaker notes):** a real pointer has a type (it can only point to one kind of "room"), and Go does not let you "walk to the next room" (no pointer arithmetic).

### 2.9 Suggested slide outline

Follows the lesson arc of `02_Pedagogy_Style.md` (section 3).

| # | Purpose | Component | Content |
|---|---|---|---|
| 1 | Cover | [7.2] | Apuntadores en Go |
| 2 | Hook | [7.5] | Function that tries to modify a value and fails (pass by value) |
| 3 | Pre-training | [7.7] | Variable, dirección, apuntador (icons + one-line role) |
| 4 | Concept | [7.9] | Hotel analogy |
| 5 | Syntax | [7.5] | `*T`, `&x`, `*p` with line steps |
| 6 | Mechanism | [7.10] | Memory boxes animation (states 1–4) |
| 7 | Worked example | [7.5] | `duplicar(n *int)` full code, line steps |
| 8 | Mechanism | [7.10] | Animation of `duplicar(&x)` (state 5) |
| 9 | Completion problem | [7.5] | Function with `/* ??? */`, then solution slide |
| 10 | Edge case | [7.5] + [7.8] | `nil` pointer and runtime panic |
| 11 | Quiz | [7.11] | Predict the output, misconception distractors |
| 12 | Takeaways | [7.12] | 3 ideas |

### 2.10 Sources (official)

- A Tour of Go — Pointers: https://go.dev/tour/moretypes/1
- A Tour of Go — Pointers to structs: https://go.dev/tour/moretypes/4
- The Go Programming Language Specification — Address operators: https://go.dev/ref/spec#Address_operators
- Effective Go — Pointers vs. Values: https://go.dev/doc/effective_go#pointers_vs_values
- Go FAQ — "When are function parameters passed by value?": https://go.dev/doc/faq#pass_by_value
- Go FAQ — "How do I know whether a variable is allocated on the heap or the stack?": https://go.dev/doc/faq#stack_or_heap

Only these sources may be used to justify technical facts in this deck.

---

## 3. PRD (optional)

A course may link a PRD (product requirements document) when the lessons build a real project (e.g. "an API that…"). When present, the PRD defines the project's features and the deck must use code consistent with it.

**This course has no PRD.** Examples are standalone and only illustrate the concept.

---

## 4. Template to add a new course

Copy section 2 and fill in:

```markdown
## N. Course: [name]

### N.1 Course card
| Field | Value |
|---|---|
| Course | |
| Topic of this deck | |
| Domain | [one of the domains in section 1] |
| Level | |
| Language of slides | Spanish |
| Language of code | |
| Target length | |
| PRD | [link or "None"] |

### N.2 Learning objectives
### N.3 Scope (in / out)
### N.4 Key facts (source of truth)
### N.5 Common misconceptions
### N.6 Code conventions
### N.7 Visual conventions
### N.8 Suggested analogy (optional)
### N.9 Suggested slide outline
### N.10 Sources (official)
```

