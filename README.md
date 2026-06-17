# dm-kai-homepage

Personal GitHub Pages site for interview prep notes. Live at: https://alalajimao.github.io/dm-kai-homepage/

## Project structure

```
dm-kai-homepage/
├── index.html              # Landing page — card grid linking to all sections
├── PROMPT_TEMPLATE.md      # Reusable Claude prompt for generating new LeetCode topic pages
│
├── leetcode/               # LeetCode topic notes section
│   ├── index.html          # Topic overview (pattern grid + progress table)
│   ├── style.css           # Shared stylesheet for ALL pages (leetcode + company-prep)
│   ├── stack.html          # Stack topic page (complete)
│   ├── linked-list.html    # Linked List topic page (complete)
│   └── problems/           # Individual mock interview pages
│       ├── 20-valid-parentheses.html
│       ├── 42-trapping-rain-water.html
│       ├── 84-largest-rectangle-in-histogram.html
│       ├── 155-min-stack.html
│       ├── 232-implement-queue-using-stacks.html
│       ├── 739-daily-temperatures.html
│       ├── ll-2-add-two-numbers.html
│       ├── ll-19-remove-nth-from-end.html
│       ├── ll-21-merge-two-sorted-lists.html
│       ├── ll-23-merge-k-sorted-lists.html
│       ├── ll-25-reverse-nodes-in-k-group.html
│       ├── ll-92-reverse-linked-list-ii.html
│       ├── ll-138-copy-list-with-random-pointer.html
│       ├── ll-141-linked-list-cycle.html
│       ├── ll-142-linked-list-cycle-ii.html
│       ├── ll-143-reorder-list.html
│       ├── ll-146-lru-cache.html
│       ├── ll-206-reverse-linked-list.html
│       ├── ll-234-palindrome-linked-list.html
│       ├── ll-876-middle-of-linked-list.html
│       └── ... (more stack/calculator problems)
│
└── company-prep/           # Company-specific interview prep section
    └── index.html          # Problem list filterable by company (Google/Meta/Amazon/etc.)
```

## Design system

All pages share `leetcode/style.css` (referenced as `../leetcode/style.css` from sub-directories).

**Color palette:** sage green theme — `--bg-primary: #f3f6f0`, `--blue: #3474b0`, `--green: #28784a`

**Layout:** fixed header + sidebar (sticky) + main content + optional right TOC rail

**Key CSS components** (all defined in style.css — do NOT add new classes inline):

| Component | Class |
|-----------|-------|
| Page layout | `.page-layout` → `.sidebar` + `.main-content` + `.toc-rail` |
| Callout boxes | `.callout .callout-blue/yellow/green` |
| Pattern cards | `.pattern-grid` → `.pattern-card` |
| Problem table | `.problem-table` with `.tag-easy/medium/hard`, `.tag-pattern` |
| Chat bubbles | `.chat-bubble` / `.chat-bubble.cand` with `.btext.int-b` / `.btext.cand-b` |
| Code blocks | `.code-block` + `.code-block-header` + syntax classes `.kw .fn .str .num .cm .var .bi` |
| Walkthrough | `.walkthrough` with `.cbox`, `.wt-row`, `.wt-col`, `.wt-msg` |
| Complexity grid | `.complexity-box` → `.cx-cell.hd` (3-column grid) |
| Progress tracker | `.prob-progress` + `.prob-progress-fill` + `.prob-check` |
| Stage labels | `.stage-label` + `.stage-dot` |

**Typography tiers:** responsive via CSS variables — Tier 1 (<1200px), Tier 2 (≥1200px), Tier 3 (≥1600px)

## Sections

### LeetCode Notes (`/leetcode/`)
Pattern-based topic pages. Each topic page has:
1. Introduction + core operations
2. Problem patterns (`.pattern-grid` cards with trigger keywords)
3. Deep dives with interactive walkthroughs (vanilla JS, no frameworks)
4. Practice problem table

Individual problem pages (`/leetcode/problems/`) are mock interview dialogues with 6 stages:
Stage 1 Problem intro → Stage 2 Clarifying questions → Stage 3 Approach discussion →
Stage 4 Pseudocode walkthrough → Stage 5 Complexity analysis → Stage 6 Follow-ups

Use `PROMPT_TEMPLATE.md` to generate new topic + problem pages with Claude.

**Completed topics:** Stack, Linked List

### Company Prep (`/company-prep/`)
Single-page app (vanilla JS, no build step). All problem data is embedded in the JS of
`company-prep/index.html` as a `PROBLEMS` array.

Features:
- Company filter (sidebar + card grid): Google, Meta, Amazon, Microsoft, Apple, ByteDance, Uber
- Problems sorted by reported frequency (High → Med) per company
- Checkbox progress tracking persisted to `localStorage`
- Links to existing mock interview pages where available

To add a new company: add its key to the `COMPANIES` array and add `freq` entries to relevant problems.
To add a new problem: append an object to the `PROBLEMS` array following the existing schema.

## Adding content

**New LeetCode topic page:** follow `PROMPT_TEMPLATE.md` — fill in the placeholders and send to Claude.

**New problem to Company Prep:** edit the `PROBLEMS` array in `company-prep/index.html`.

**New company to Company Prep:** add the company key to `COMPANIES`, add a sidebar item, a card, and
`freq` entries on relevant problems in `company-prep/index.html`.

## Tech stack

Pure static HTML/CSS/JS — no build tools, no frameworks, no dependencies.
Deploy: `git push` to `main` → GitHub Pages auto-publishes.
