---
name: codurance-deck
description: Create, edit, and build Codurance-branded slide decks with Marp, including turning existing content (a document, notes, a brief) into a full deck. Use when the user wants to make a presentation or slide deck, convert a write-up into slides, apply Codurance branding to slides, add speaker notes, regenerate slides.html or a PDF from a Marp markdown deck, or review a deck via CR comments.
---

# Codurance Marp Decks

Build presentations as Marp markdown with the bundled Codurance theme. The markdown file is the source of truth; `slides.html` and the PDF are generated from it.

## Starting a new deck

1. Copy `assets/template.md` (relative to this skill) to `<deck-name>.md` in the user's working directory.
2. Create an `images/` folder next to it and copy in `assets/bg-band.svg`, `assets/bg-hex.svg`, and `assets/codurance-logo-white.svg`. The theme CSS references these relatively.
3. Replace the example slides with the user's content, keeping one example of each class for reference until the deck has real slides of that type.

Sharing note: `slides.html` needs the `images/` folder beside it; the PDF is self-contained. Recommend the PDF for sharing.

## Creating a deck from existing content

Users can feed in source material of any shape: a structured write-up, loose meeting notes, bullet points, or plain prose telling a story. Build the deck from it rather than from scratch:

1. Read all the source material first.
2. Interview the user before planning anything. A few pointed questions, asked properly (AskUserQuestion where available), not a checkbox exercise:
   - Who exactly is the audience, and what do they already know? ("Everyone" is not an answer; push for the real room.)
   - What is the occasion and how long is the talk?
   - What is the one thing they want the room to take away?
   - What in the source should be left out, softened, or is sensitive (names, clients, numbers)?
   - Is there a story or order they want told? If the source is a narrative, confirm the arc with them; never impose a sequence or intentionality the author didn't state.
   Follow up on vague answers before moving on.
3. Propose an outline before writing slides: the sections (which become `divider` slides) and one line per planned slide. Get the user's agreement, then build.
4. Split content between slide and note: slides carry the skeleton (a headline, a few bullets, a table, or one visual); the speaker note carries the substance from the source in spoken form. Do not paste paragraphs from the source onto slides.
5. Use only facts from the source. Do not invent examples, numbers, sequence, or intentionality that are not there; if something needed for the story is missing, ask.
6. Rough sizing: a 10-minute talk is around 10-14 slides including dividers; 30 minutes around 20-28.

## Writing style: ask first

Before drafting any slide or note content for a new deck, ask the user whether to apply the bundled defaults in `STYLE.md` (read it, then apply) or their own style rules. If they give their own rules, follow those instead and do not mix in the defaults. Do not skip this question.

## Slide classes

| Class | Look | Use for |
|---|---|---|
| (none) | White, navy band on the right | Standard content slides |
| `plain` | White, full width, no band or logo | Wide diagrams, flows, big tables |
| `divider` | Dark navy, hexagons | Section breaks; `##` renders large white |
| `title` | Dark navy, hexagons, vertically centred | Opening and closing slides |
| `highlight` | Pale tint, band kept | Context-setting or emphasis slides |
| `screenshot` | Dark navy, full width | Full-width images; dark screenshots blend best |

Set a class with a directive comment at the top of the slide: `<!-- _class: divider -->`.

## Layout rules

- Six bullets maximum on a content slide; the band leaves roughly 970px of usable width, so lines wrap sooner than full-slide designs.
- Anything wide (tables, `.flow` rows) must be checked in the rendered output for wrapping or overflow. Shrink `.flow-step` font-size or move the slide to `plain` if a flow row wraps.
- Do not remove the explicit `th`/`td` background colours from the CSS. Marp's default theme gives tables a white background, and translucent or missing cell backgrounds render as washed-out grey.
- The page number renders top-right (on the band) and the white logo bottom-right automatically; `plain` hides the logo because it would be invisible on white.
- Dark image slides: pass width like `![w:1150](images/foo.png)`.

## Speaker notes

- One plain HTML comment per slide is that slide's presenter note. Keep it separate from directive comments.
- Write notes as a talk track: spoken sentences the presenter could deliver, plus any delivery cues. Cues and discussion prompts belong in notes, never on the slide.
- Presenter view: open `slides.html` and press `P`, or open `slides.html?view=presenter`. A second normal browser window stays in sync for the audience screen.

## Build and verify

```
npx -y @marp-team/marp-cli <deck>.md -o slides.html
npx -y @marp-team/marp-cli <deck>.md -o <deck>.pdf --allow-local-files
```

After any content or CSS change, render PNGs to a scratch directory and visually inspect every changed slide before declaring the work done:

```
npx -y @marp-team/marp-cli <deck>.md --images png --allow-local-files -o <scratch-dir>/deck.png
```

Check for: text overflowing or wrapping oddly, tables clipping, content colliding with the band, and that slide count and note count still match (`grep -o '<svg data-marpit-svg' slides.html | wc -l` and `grep -o 'class="bespoke-marp-note"' slides.html | wc -l`).

## Review loop

Deck owners annotate the markdown with `<!-- CR: their comment -->` next to the thing the comment is about. When asked to process review comments: `grep -n 'CR:'` to collect them all, apply each change, delete the marker as you go, regenerate all outputs, and verify zero `CR:` markers remain.
