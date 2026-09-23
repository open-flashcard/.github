## Open Flashcard Standard

**An open JSON format for flashcards.** A deck is one file: you can write it by hand, diff it in git, validate it
strictly, and open it in any app that implements the format.

```json
{
  "openflashcard": "1.0.0",
  "id": "urn:ofc:deck:you/hello",
  "name": "My First Deck",
  "lang": "en",
  "cards": [
    {
      "front": [{ "type": "cloze", "text": "The {{mitochondria}} is the powerhouse of the cell." }]
    },
    {
      "front": [{ "type": "text", "text": "mariposa", "lang": "es", "speech": { "rate": 0.8 } }],
      "back": [{ "type": "text", "text": "butterfly" }]
    }
  ]
}
```

A card is a piece of paper. It has a **front**, and it may have a **back**, a **hint**, and **notes**. Each side is
a list of content blocks, in any order and any mix: text, Markdown, LaTeX, code, Mermaid diagrams, images, audio,
video, embeds, lists, multiple choice, cloze, and links.

### Projects

| | |
|---|---|
| [**schema**](https://github.com/open-flashcard/schema) | The specification, the JSON Schema (draft 2020-12), example decks, and a language-neutral conformance suite |
| [**skills**](https://github.com/open-flashcard/skills) | Agent skills for writing, validating, converting (Anki, Quizlet, CSV), and reviewing decks with Claude or any agent that supports Agent Skills |
| [**web**](https://github.com/open-flashcard/web) | A local-first study app and the reference renderer, with FSRS scheduling and no account or backend |

### Get started

- **Read the spec:** [`schema.md`](https://github.com/open-flashcard/schema/blob/main/versions/v1.0.0/schema.md)
- **Validate a deck:** `npx -p ajv-cli -p ajv-formats ajv validate --spec=draft2020 -c ajv-formats -s schema.json -d your-deck.ofc.json`
- **Make decks with Claude Code:** `/plugin marketplace add open-flashcard/skills`, then
  `/plugin install ofc@open-flashcard`
- **Study a deck:** run [web](https://github.com/open-flashcard/web) and drop in a `.ofc.json` file

### Principles

- **Content only.** Scheduling, review history, and learner progress stay out of the deck, so a published deck means
  the same thing to every reader and reveals nothing about the person who studied it.
- **Strictly validatable.** A deck either conforms or it doesn't; implementations have no grey area to resolve
  differently.
- **Every renderer renders everything.** A conforming app supports every built-in block, so a deck that works in one
  app works in all of them.
- **Accessible by design.** Images require `alt` text, embeds require a fallback, and language is tagged per block.

Contributions, questions, and implementations in other languages are welcome. Open an issue in the relevant
repository. Everything here is MIT or Apache-2.0 licensed.
