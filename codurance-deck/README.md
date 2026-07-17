# codurance-deck

A Claude Code skill for building Codurance-branded presentations with [Marp](https://marp.app/). Slides are written as markdown; HTML (with presenter view and speaker notes) and PDF are generated from it.

## What's inside

- `SKILL.md` — the skill instructions Claude follows
- `STYLE.md` — default writing-style rules (Claude asks whether to use these or your own)
- `assets/template.md` — starter deck with the full Codurance theme and one example slide per layout
- `assets/bg-band.svg`, `assets/bg-hex.svg`, `assets/codurance-logo-white.svg` — brand graphics the theme uses

## Install

Copy this folder into your personal Claude Code skills directory:

```
cp -r codurance-deck ~/.claude/skills/codurance-deck
```

Or into a project's `.claude/skills/` to share it with everyone working in that repo.

## Use

Start a new Claude Code session and ask for a deck, e.g. "create a Codurance-branded presentation about X" — the skill triggers on presentation/deck requests. Claude will set up the markdown, ask about writing style, build `slides.html` and a PDF, and visually verify the slides render correctly.

Best results come from feeding it content: point Claude at a write-up, notes, or a brief ("turn ~/notes/retro.md into a deck for the team, 15 minutes"). It will ask about audience and length, propose an outline for your approval, then put the skeleton on the slides and the substance in your speaker notes — using only what's in your source material.

Reviewing a draft: open the deck's `.md`, add comments like `<!-- CR: reword this, too formal -->` next to anything you want changed, then ask Claude to go through them.

Presenting: open `slides.html`, press `P` for presenter view (current slide, next slide, your notes, timer). Requires `npx` (Node) available; Marp CLI downloads on first use.
