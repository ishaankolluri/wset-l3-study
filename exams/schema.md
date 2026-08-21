# WSET L3 practice theory papers — JSON schema

Original Unit 1 practice papers. Not textbook quotation and not PassWSET copy.
Part 1 is a 50-item multiple-choice paper (timed). Part 2 is four short-written questions (untimed, self-marked).

## File layout

```
quizlet-site/
  exam.html          standalone exam player (fetch JSON over https)
  exams/
    schema.md        this document
    paper-01.json … paper-10.json
  index.html         flashcard player; header link to exam.html
```

`exam.html` may `fetch('./exams/paper-0N.json')` on Pages. Papers are not embedded.

## Paper object

| Field | Type | Rules |
|-------|------|--------|
| `id` | string | `paper-01` … `paper-10` |
| `title` | string | `Practice paper N` |
| `duration_minutes` | number | `60` — countdown for Part 1 MCQ only |
| `pass_mark_percent` | number | `55` (28/50 on MCQ; same bar on written in the real exam) |
| `mcq` | array | Exactly 50 items |
| `written` | array | Exactly 4 questions, 25 marks each (100 total) |

## MCQ item

| Field | Type | Rules |
|-------|------|--------|
| `id` | string | `q01` … `q50` |
| `topic` | string | One of the five buckets below |
| `q` | string | Stem. Original wording. One correct answer. |
| `choices` | array | Exactly 4 strings, labelled `A …` `B …` `C …` `D …` |
| `answer` | string | Must equal one of `choices` exactly |
| `why` | string | One-line justification for study review |

### Topic buckets (every paper, this mix)

| `topic` | Count | Meaning |
|---------|------:|---------|
| `vineyard-winery` | 8 | Vine, climate, vineyard, yield, canopy, white/red/rosé making, MLF, oak, SO2, maceration (LO1 factors, not a named region) |
| `still` | 28 | Still wines of the world, including PDO/PGI/label law tied to still wine |
| `sparkling` | 5 | Sparkling methods, regions, styles, dosage |
| `fortified` | 5 | Sherry, Port, VDN, Madeira, Rutherglen Muscat |
| `advice` | 4 | SAT, faults, quality/readiness, storage, service, food and wine |

Player shuffles choice **order** on load and re-letters A–D. Grade by the answer **text** after the letter, not by letter. Grade only on Finish (or when the 60-minute clock hits zero). Written is not on that clock.

## Written question

| Field | Type | Rules |
|-------|------|--------|
| `id` | string | `w1` … `w4` |
| `title` | string | Short heading |
| `marks` | number | `25` |
| `parts` | array | Sub-parts; their `marks` sum to 25 |

### Written part

| Field | Type | Rules |
|-------|------|--------|
| `prompt` | string | What the candidate should answer |
| `marks` | number | Shown on the paper |
| `points` | array | Mark-scheme bullets (not shown until toggled) |

Typical shape: w1–w2 still-wine regions in depth (vineyard and winery folded in); w3 sparkling; w4 fortified **or** food/service with a region. Across the four questions aim near 70 marks LO2 (still / factors), 20 marks LO3+LO4 (sparkling + fortified), 10 marks LO5 (storage/service/food). Vary the split by paper.

## Player behaviour

1. Home: list of 10 papers.
2. Part 1: all 50 MCQs on one scrolling sheet, radio choices, pinned countdown, one Finish control. Refuse Finish while any item is blank. Shuffle options on load. No per-item grade while the sheet is open.
3. After submit or timeout: score / 50, 55% pass line, weak-area breakdown by the five buckets, then optional review of items.
4. Part 2: written questions with mark allocations and a Show mark scheme toggle. Not auto-graded. Not timed.
5. Back to list.
