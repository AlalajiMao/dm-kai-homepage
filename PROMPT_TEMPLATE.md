# LeetCode Topic Page — Content Generation Prompt

> **Purpose:** Reusable prompt for generating a complete new algorithm/data structure topic
> for the `dm-kai-homepage` LeetCode notes site. Paste this prompt into Claude and fill in
> the `[PLACEHOLDERS]` before sending.

---

## How to Use

1. Copy the **Full Prompt** section below.
2. Replace every `[PLACEHOLDER]` with the target topic's details.
3. Send to Claude. It will produce two deliverables:
   - `leetcode/[topic-slug].html` — the topic overview page
   - `leetcode/problems/[id]-[slug].html` — one mock interview page per problem (start with 2)
4. Drop the files into the repo, add sidebar entries, push, done.

---

## Full Prompt

```
You are helping build a static GitHub Pages LeetCode review site at:
  https://alalajimao.github.io/dm-kai-homepage/leetcode/

Target topic: [TOPIC NAME]  (e.g. "Linked List", "Binary Search", "Sliding Window")
Topic slug:   [topic-slug]  (e.g. "linked-list", "binary-search")
Topic icon:   [EMOJI]       (e.g. 🔗, 🔍, 🪟)
Chinese name: [中文名]

The site uses a shared stylesheet at `leetcode/style.css`. All CSS classes are already
defined — do NOT add inline styles or new CSS unless strictly necessary.
Use the same sidebar, header, and layout pattern as `leetcode/stack.html`.

---

### DELIVERABLE 1 — Topic Overview Page
File: `leetcode/[topic-slug].html`

Build the page in this exact section order:

#### Section 1 · Introduction (英文 + 一句中文备注)
- One-paragraph plain-English explanation of what the data structure / technique is.
- Core operations with Python syntax (as a `.code-block` with manual syntax highlighting
  using the CSS classes: `.kw` `.fn` `.str` `.num` `.cm` `.var` `.bi`).
- Time/space complexity of core operations.
- One-sentence Chinese annotation for quick recall.

#### Section 2 · Problem Patterns
- 3–5 pattern cards using the `.pattern-grid` / `.pattern-card` layout.
- Each card must include:
  - `pattern-icon` (emoji)
  - `pattern-title` (English)
  - `pattern-zh` (Chinese name)
  - `pattern-desc` (2–3 sentence description of when/why this pattern applies)
  - `pattern-keywords`: 3–5 keyword chips using `.kchip` that serve as recognition triggers
    (exact phrases from problem statements that signal this pattern)

#### Section 3 · Deep Dives (one per pattern, in `<h2>` subsections)
Each deep dive must contain:
a. **Trigger callout** (`.callout-yellow`): exact keywords / phrases from problem descriptions
   that signal this pattern. Include Chinese translation.
b. **Core insight callout** (`.callout-blue`): the single most important observation that
   makes the efficient solution click. In English + one Chinese sentence.
c. **Core template pseudocode** (`.code-block`): language-agnostic pseudocode with syntax
   highlighting. Comments explain the WHY, not just the what.
d. **Interactive walkthrough** (vanilla JS, no frameworks): an animated step-by-step trace
   of the algorithm on a concrete example. Use the `.walkthrough` container.
   - For array/string problems: show a character/element row with `.cbox` highlighting.
   - For tree/graph problems: render an ASCII or SVG diagram updated per step.
   - Controls: Prev / Next / Auto / Reset buttons using `.btn` classes.
e. **Complexity summary** in a `.callout-green`.

#### Section 4 · Practice Problem List
Two tables (`<h3>` each): **Classic Problems** and **Recent Interview Picks (2023–2025)**.
Table columns: # | Problem (linked if page exists) | Difficulty tag | Pattern tag | Note
- Mark must-know problems with ⭐
- Mark recently trending problems with 🔥
- Link to problem pages that exist; use `#` placeholder for future ones.

---

### DELIVERABLE 2 — Mock Interview Pages
File: `leetcode/problems/[id]-[slug].html`  (generate for the 2 most important problems)

Each page follows a **6-stage interview dialogue** between Interviewer (IV) and Candidate (Me).
Use `.chat-bubble` / `.chat-bubble.cand` with `.btext.int-b` / `.btext.cand-b`.
Use `.thought` divs for internal reasoning the candidate verbalises.
Use `.stage-label` dividers between stages.

**Stage 1 — Problem Introduction**
IV presents the problem naturally, as a real interviewer would (no robotic recitation).
Include 1–2 intentional ambiguities the candidate should catch.

**Stage 2 — Clarifying Questions**
Candidate asks 3–4 targeted clarifications covering:
- Edge cases (empty input, single element, duplicates)
- Constraints (length, value range)
- Output format confirmation
IV answers concisely.

**Stage 3 — Approach Discussion**
Candidate verbally walks through:
1. Brute-force approach + its complexity (always state this first)
2. The key observation that leads to the optimal approach
3. The pattern/data structure chosen and why
IV may ask "can you do better?" to prompt the upgrade.
Use a `.thought` div to show the internal "aha moment".

**Stage 4 — Pseudocode Walkthrough**
Candidate presents pseudocode (not full code yet) and manually traces it on the
example from the problem statement. Steps should be explicit:
  "i=0, val=X → [action]. Stack: [state]"
IV asks at least one targeted question about a specific line or edge case.

**Stage 5 — Complexity Analysis**
Candidate gives time and space complexity with clear justification.
If there is a non-obvious amortised argument (e.g. each element pushed/popped once),
spell it out explicitly.
Use the `.complexity-box` grid component.

**Stage 6 — Follow-up Questions**
IV asks 2–3 follow-ups from this list (pick the most relevant):
- Variation: what if the array is circular / sorted / has duplicates?
- Extension: how would you modify for the "previous" version instead of "next"?
- Relation: how does this problem relate to [harder problem in the same family]?
- Optimisation: can you reduce space to O(1)?
- Generalisation: what if the constraint changes from > to >=?
Candidate answers each concisely but completely.

At the end of the page, include:
- Full Python solution in a `.code-block` with syntax highlighting.
- A `.callout-green` "Key Interview Tips" list (4–6 bullets): concrete reminders
  a candidate should internalise before the real interview.
- A "Next problem →" link.

---

### Style Rules (apply to both deliverables)
- Language: English throughout. Add a single Chinese sentence in italic or muted colour
  for key concepts only — not every paragraph.
- Code: Python 3 pseudocode in deep dives, full Python 3 in solution sections.
  Use manual syntax highlighting classes (.kw .fn .str .num .cm .var .bi).
- No external JS libraries. Vanilla JS only for animations.
- Sidebar: copy the sidebar structure from `stack.html` exactly; mark the new topic as
  `.active` and keep all other topics as they are.
- All paths are relative: CSS is `../style.css` from problem pages, `style.css` from topic pages.
- Problem difficulty tags: `.tag-easy` / `.tag-medium` / `.tag-hard`.
- Do not add new CSS classes. Use only classes already defined in `style.css`.

---

### Topic-specific inputs (fill these in)

TOPIC: [TOPIC NAME]
PATTERNS (list 3–5):
  1. [Pattern name] — [trigger keywords] — [core insight in one sentence]
  2. ...

PROBLEMS FOR DEEP DIVE MOCK INTERVIEWS (pick 2):
  Problem A: LC #[id] [name] ([difficulty]) — Pattern: [pattern]
  Problem B: LC #[id] [name] ([difficulty]) — Pattern: [pattern]

PRACTICE PROBLEM LIST:
  Classic (must-know):
    - LC #[id] [name] ([difficulty]) — [pattern] — [brief note]
    - ...
  Recent picks (2023–2025):
    - LC #[id] [name] ([difficulty]) — [pattern] — [brief note]
    - ...
```

---

## Quick Reference — CSS Components

| Component | HTML pattern |
|-----------|-------------|
| Callout box | `<div class="callout callout-blue/yellow/green"><div class="callout-label">TITLE</div>…</div>` |
| Code block with header | `<div class="code-block"><div class="code-block-header">…</div><pre><code>…</code></pre></div>` |
| Pattern grid | `<div class="pattern-grid"><div class="pattern-card">…</div></div>` |
| Problem table | `<table class="problem-table"><thead>…</thead><tbody>…</tbody></table>` |
| Difficulty tag | `<span class="tag tag-easy/medium/hard">Easy</span>` |
| Pattern tag | `<span class="tag tag-pattern">…</span>` |
| Chat bubble (IV) | `<div class="chat-bubble"><div class="avatar av-int">IV</div><div class="bubble-wrap"><div class="bubble-name">Interviewer</div><div class="btext int-b">…</div></div></div>` |
| Chat bubble (Me) | `<div class="chat-bubble cand"><div class="avatar av-cand">Me</div><div class="bubble-wrap"><div class="bubble-name">Candidate</div><div class="btext cand-b">…</div></div></div>` |
| Internal thought | `<div class="thought">…</div>` |
| Stage label | `<div class="stage-label"><span class="stage-dot"></span> Stage N — Title</div>` |
| Complexity grid | `<div class="complexity-box"><div class="cx-cell hd">…</div>…</div>` (3-column grid) |
| Walkthrough container | `<div class="walkthrough"><div class="walkthrough-title">…</div>…<div class="walkthrough-controls">…buttons…</div></div>` |

---

## Completed Topics

| Topic | File | Problems with pages | Status |
|-------|------|--------------------|----|
| Stack | `leetcode/stack.html` | #20, #739 | ✅ Done |

## Planned Topics (suggested order)

1. **Linked List** — Two pointers, fast/slow, reversal, merge
2. **Binary Search** — Classic, search space reduction, rotated array
3. **Sliding Window** — Fixed window, variable window, character frequency
4. **Trees (DFS/BFS)** — Pre/in/post order, level order, path problems
5. **Dynamic Programming** — 1D, 2D, interval, knapsack
6. **Two Pointers** — Sorted array, opposite ends, partition
7. **Graphs** — BFS shortest path, DFS connected components, topological sort
8. **Heap / Priority Queue** — Top-K, merge K sorted, median stream
