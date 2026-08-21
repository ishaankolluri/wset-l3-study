# WSET L3 Quizlet — deck schema

Flashcard decks for self-study. Copy is original paraphrase, not textbook quotation.
No tracking, no login, no network. Progress lives in `localStorage` under `wset-l3-quizlet-v1`.

## File layout

```
quizlet/
  schema.md    this document
  decks.json   array of decks (source of truth for authors)
  index.html   standalone player; embeds the same array so file:// works
  README.md    how to open it
```

`index.html` must not rely on `fetch('./decks.json')`. Browsers block that under `file://`.
Embed via `<script type="application/json" id="decks-data">`.

## Deck object

| Field     | Type   | Rules |
|-----------|--------|--------|
| `id`      | string | Stable slug, e.g. `sat-core` |
| `title`   | string | Short deck title |
| `chapter` | number | WSET L3 chapter (start of a range is fine) |
| `section` | number | Section, or the end chapter when the deck spans chapters (e.g. 4–5) |
| `blurb`   | string | One line |
| `cards`   | array  | 12–16 term/definition cards |

Chapter tag in the player: single chapter shows `Ch. N`. A span (vine-climate, winery) shows `Ch. A–B`.

## Card object

| Field        | Type   | Rules |
|--------------|--------|--------|
| `id`         | string | Stable slug unique within the deck |
| `term`       | string | Front of the card; also the typed-answer key |
| `definition` | string | Back of the card; quiz stem |
| `hint`       | string | Optional. Shown on the flashcard back and after a missed type-in |

## Progress (`wset-l3-quizlet-v1`)

```
{
  "decks": {
    "<deckId>": {
      "cards": { "<cardId>": { "status": "known" | "learning" } },
      "lastQuiz": { "correct": 8, "total": 10, "at": 1710000000000 }
    }
  }
}
```

Mastery % on the home list is `known / cards.length`. Reset deck clears that deck's object.

## Player behaviour

1. Home: every deck as a row (title, count, chapter tag, mastery).
2. Flashcards: one card, tap or Space to flip term ↔ definition. Prev/Next. Know / Still learning. Keys: Space, ← →, K, L.
3. Quiz: 8–12 questions (or the whole deck if smaller). Mix of type-the-term and 4-choice MCQ with 3 distractors from the same deck. Score, missed list, retry missed.
4. No login, no network, no tracking.

## Seed pack (5 decks)

| id | chapter | title | cards |
|----|---------|--------|------:|
| `sat-core` | 1 | SAT core | 12 |
| `vine-climate` | 4–5 | Vine and climate | 13 |
| `vineyard` | 6 | Vineyard work | 12 |
| `winery` | 7–9 | Winery toolkit | 14 |
| `law` | 11 | Wine and the law | 12 |
