---
marp: true
theme: default
paginate: true
style: |
  :root {
    --navy: #1d2138;
    --text-dark: #222741;
    --text-light: #eef0f6;
    --peri: #6d77c9;
    --peri-light: #9aa3e0;
    --tint: #edf0fa;
    --muted-dark: #6b7280;
    --muted-light: #a9aec7;
  }

  section {
    background-color: #ffffff;
    background-image: url('images/bg-band.svg');
    background-size: cover;
    background-position: center;
    color: var(--text-dark);
    font-family: 'Poppins', 'Avenir Next', 'Segoe UI', sans-serif;
    padding: 48px 248px 48px 64px;
  }

  h1 {
    font-size: 2.6em;
    color: var(--navy);
    line-height: 1.1;
    font-weight: 700;
  }

  h2 {
    font-size: 1.6em;
    color: var(--navy);
    font-weight: 700;
    margin-bottom: 24px;
  }

  h3 {
    color: var(--peri);
    font-size: 0.95em;
    text-transform: uppercase;
    letter-spacing: 2px;
    margin-bottom: 6px;
  }

  ul {
    list-style: none;
    padding: 0;
  }

  ul li {
    padding: 7px 0 7px 22px;
    color: var(--text-dark);
    position: relative;
    font-size: 0.95em;
  }

  ul li::before {
    content: '▸';
    color: var(--peri);
    position: absolute;
    left: 0;
  }

  strong { color: var(--navy); }

  code {
    background: var(--tint);
    color: var(--navy);
    padding: 2px 8px;
    border-radius: 4px;
  }

  blockquote {
    border-left: 4px solid var(--peri);
    background: var(--tint);
    padding: 16px 24px;
    margin: 16px 0;
    border-radius: 0 6px 6px 0;
    font-style: italic;
    color: var(--text-dark);
  }

  blockquote p { margin: 0; }

  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.9em;
    background: transparent;
  }

  th {
    background: var(--navy);
    color: #ffffff;
    padding: 10px 16px;
    text-align: left;
    font-weight: 600;
    border: none;
  }

  td {
    padding: 10px 16px;
    border: none;
    border-bottom: 1px solid #e2e4f0;
    color: var(--text-dark);
    background: #ffffff;
  }

  tr:nth-child(even) td { background: #f5f6fc; }

  section::after {
    position: absolute;
    top: 28px;
    right: 36px;
    bottom: auto;
    color: var(--peri-light);
    font-size: 0.75em;
    font-weight: 600;
  }

  section::before {
    content: '';
    position: absolute;
    bottom: 24px;
    right: 40px;
    width: 120px;
    height: 22px;
    background: url('images/codurance-logo-white.svg') no-repeat center / contain;
  }

  section.plain {
    background-image: none;
    padding: 48px 64px;
  }

  section.plain::before { display: none; }
  section.plain::after { color: var(--peri); }

  .flow {
    display: flex;
    gap: 6px;
    align-items: center;
    flex-wrap: wrap;
    margin: 20px 0;
  }

  .flow-step {
    background: var(--tint);
    border: 1.5px solid var(--peri);
    border-radius: 4px;
    padding: 8px 12px;
    font-size: 0.74em;
    color: var(--navy);
    font-weight: 500;
    white-space: nowrap;
  }

  .flow-arrow { color: var(--muted-dark); font-size: 1.1em; }

  section.highlight {
    background-color: var(--tint);
  }

  section.highlight blockquote { background: #ffffff; }

  section.title,
  section.divider,
  section.screenshot {
    background-color: var(--navy);
    background-image: url('images/bg-hex.svg');
    color: var(--text-light);
    padding: 48px 64px;
  }

  section.title strong,
  section.divider strong,
  section.screenshot strong { color: #ffffff; }

  section.title {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  section.title h1 {
    font-size: 3em;
    color: #ffffff;
  }

  section.title h2 { color: #ffffff; }
  section.title h3 { color: var(--peri-light); }
  section.title p { color: var(--muted-light); font-size: 1em; }

  section.divider {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  section.divider h1 {
    font-size: 1em;
    color: var(--peri-light);
    text-transform: uppercase;
    letter-spacing: 3px;
    margin-bottom: 8px;
  }

  section.divider h2 {
    font-size: 2.8em;
    color: #ffffff;
    margin: 0;
    font-weight: 700;
  }

  section.divider p { color: var(--muted-light); margin-top: 16px; }

  section.divider p strong {
    display: block;
    color: #ffffff;
    font-size: 1.7em;
    font-weight: 600;
    line-height: 1.35;
  }

  section.title blockquote {
    background: rgba(255,255,255,0.08);
    border-left: 4px solid var(--peri-light);
    color: rgba(255,255,255,0.9);
  }

  section.title blockquote p { color: rgba(255,255,255,0.9); }

  section.screenshot {
    padding: 40px 48px;
  }

  section.screenshot h2 {
    color: var(--peri-light);
  }

  section.screenshot p {
    color: var(--muted-light);
    font-size: 0.85em;
  }

  section.screenshot img {
    width: 100%;
    border-radius: 6px;
  }
---

<!-- _class: title -->

# Talk Title
# Goes Here

### Optional kicker line

<!--
Speaker note for the opening. One plain HTML comment per slide becomes the presenter note. Keep directive comments like _class on their own line, separate from notes.
-->

---

<!-- _class: highlight -->

## A Highlight Slide

- Use the highlight class for slides that set context or need emphasis
- It gets a pale tint instead of white

<br>

> Blockquotes render as a callout card.

<!--
Note for the highlight slide.
-->

---

<!-- _class: divider -->

## Section Name

<!--
Divider notes are a good place for the bridge sentence between sections.
-->

---

## A Content Slide

An intro sentence if the slide needs one.

- Keep to six bullets or fewer per slide
- **Bold** only the key term at the start of a bullet
- The navy band takes the right edge, so lines are shorter than full width

<!--
Note for the content slide. Written the way you'd say it out loud.
-->

---

## A Table Slide

| Column one | Column two |
|---|---|
| Row | Content |
| Row | Content |
| Row | Content |

<!--
Tables are pre-themed with a navy header. Keep the explicit cell backgrounds in the CSS; without them Marp's default theme turns cells grey.
-->

---

<!-- _class: plain -->

## A Full-Width Slide

<div class="flow">
  <div class="flow-step">Step one</div>
  <div class="flow-arrow">→</div>
  <div class="flow-step">Step two</div>
  <div class="flow-arrow">→</div>
  <div class="flow-step">Step three</div>
</div>

Use the plain class when content needs the whole slide width. The logo is hidden here because it is white.

<!--
Note for the flow slide. Check the rendered output; long flow rows wrap when they run out of width.
-->

---

<!-- _class: screenshot -->

## An Image Slide

A sentence introducing the image.

![w:1150](images/example-screenshot.png)

A sentence with the takeaway. Replace the image path with your own; dark screenshots blend best.

<!--
Note for the screenshot slide.
-->

---

<!-- _class: title -->

# Questions?

<!--
Closing note. Discussion starters can live here in case the room is quiet.
-->
