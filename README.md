# WSET L3 Study

Flashcards, a term-first quiz, and ten original Unit 1 practice theory papers. Study copy is original, not a textbook dump and not a commercial bank.

**Live:** https://wset-l3-study.pages.dev

## Run locally

Open `index.html` in a browser for flashcards (decks are embedded).

Practice exams (`exam.html`) fetch `./exams/paper-0N.json`, so they need a local server or the Pages URL:

```
python3 -m http.server 8080
```

Then open http://localhost:8080/exam.html

## Deploy

```
npx wrangler pages deploy . --project-name wset-l3-study
```

## Contents

- `index.html` — flashcard / quiz player
- `exam.html` — timed 50-question MCQ sheet (60 min, 55% pass) plus untimed written Part 2
- `exams/paper-01.json` … `paper-10.json` — ten original papers
- `exams/schema.md` — paper JSON format
- `decks.json` — five flashcard decks
- `schema.md` — card format
- `wrangler.jsonc` — Pages assets config
