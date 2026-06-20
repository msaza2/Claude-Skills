---
name: html-for-general
description: Use when turning any non-code subject into one self-contained, beautiful HTML explainer — a watched/downloaded video or its transcript, an article, paper, talk, report, dataset, product, concept, process, or decision. Triggers include "make an HTML explaining this video / article / topic", "turn this into a visual explainer", or right after using the watch skill on a video. For an engineering workflow, automation, pipeline, or codebase you own, use automation-to-html instead.
---

# HTML for General

## Overview

Produce **one self-contained `.html` file** that explains **any subject** clearly and beautifully — for a smart reader who is new to it. A watched video, an article or paper, a talk, a report, a dataset, a product, a concept, a decision: distill it into a calm, scannable, single-file page.

Same look and quality as the `automation-to-html` skill — it shares that visual system — but it is **subject-agnostic**, not tied to software. (For engineering workflows / automations / codebases you own, use **automation-to-html**; it's tuned to explain systems without the code.)

## The altitude rule (most important thing in this skill)

Write for a **smart reader who has NOT seen the source.** **Distill — don't transcribe.** Your job is to surface the *ideas and what matters*, not to reproduce the material.

- **Lead with the gist** — a flowing, plain-language summary of the whole thing. It's the heart of the page.
- **Keep:** the main ideas/arguments/steps; the *why it matters*; concrete examples and evidence; key numbers; notable quotes or moments; practical takeaways / what to do; who it's for; honest caveats.
- **Cut:** filler, tangents, repetition, throat-clearing, ads/sponsor breaks, minute-by-minute play-by-play, and anything a reader wouldn't remember tomorrow. A tight page that captures the substance beats a long one that mirrors the runtime.
- For a **video/talk**: don't just timestamp everything — pull out the through-line and the few moments that carry it. (A short chapter list is fine; a transcript is not.)

## Chunk it — no walls of text (second most important)

Distilling is not enough — even distilled content reads as a blob if it's delivered as long flowing paragraphs. **Prose is for the through-line; structure is for the details.** The reader should be able to *scan* any section and get it; flowing paragraphs are the exception, not the default.

**Hard density limits — treat these as lint rules:**

- **A paragraph is at most 3 sentences / ~60 words.** If it runs longer, it contains more than one idea — split it or convert it to a component.
- **The gist is a true summary, not the findings squeezed into prose.** At most 2–3 *short* paragraphs (~50 words each) giving the through-line. Per-topic verdicts, numbers, and qualifiers belong in their own sections — the gist links the story together, it doesn't carry the data.
- **The "bolded label" test:** if you find yourself writing paragraphs that open with a bold topic label (`Hosting: …`, `Pricing: …`), that is a list wearing a paragraph costume. Convert it — one `.save-row` per topic (topic → one-line verdict), or `.info` cards, or `.stages`. The detail each paragraph was carrying moves into that topic's own section.
- **At most ~2 numbers per sentence.** Three or more numbers in one breath means the content is a dataset, not prose — move it to `.vstats`, a table, or `.save-row`s, and keep only the headline figure in the sentence.
- **At most one parenthetical or qualifier per sentence.** Stacked parentheses and em-dash asides are how walls of text form. Spin the qualifier into its own short sentence, a `.callout`, or a footnote-style gloss — or cut it.
- **Bullets are 1–2 sentences.** A bullet with 3+ sentences and multiple bolded sub-points is a paragraph hiding in a list — split it into separate bullets or promote it to its own card.
- **Callouts are ≤ ~50 words.** A callout is a sticky note, not a sidebar essay.

**The squint test (run it before calling the page done):** scroll the page squinting so you can't read the words, only see the shapes. Every section should show visible *structure* — rows, cards, numbers, splits. Any screen-tall block of uniform gray text fails; restructure it.

## Ground it — and stay honest

- **Work from the real source, never your assumptions.** For a **video**, use the **watch** skill — it gives you the transcript plus sampled frames; base everything on that. For an article/page, read or fetch it; for a file, read it.
- **Don't invent.** Every claim, number, name, and quote must trace to the source. If the source is unclear or you're inferring, say so plainly ("the talk implies…", "roughly").
- **Mind the medium's gaps:** `watch` *samples* frames, so purely visual details, on-screen text, or fast demos may be partial — don't over-claim what you couldn't verify. Transcripts can mishear names/terms; sanity-check before stating them as fact.

## Audience: explain, don't assume (jargon)

The reader is sharp but **not** an expert in the subject's domain.
- **Keep general terms** as-is.
- **Explain or replace domain jargon:** replace a niche/product-specific name with a general one when it carries the meaning; **gloss** a term the first time it matters (e.g. "a *webhook* — an automatic message one app sends another when something happens").
- When in doubt, gloss it. If several domain terms survive, add a small **"In plain terms"** glossary near the top (the template's `.gloss` rows).

## Non-negotiables

- **Self-contained.** One `.html`, **zero external requests.** Inline `<style>`, inline `<script>`, inline SVG. System font stacks only — **no CDN, no web fonts, no remote images.** Must render fully offline. If a source image is genuinely essential (e.g. one key video frame), embed it as a `base64` data URI — but default to none; prefer text + inline SVG.
- **Grounded in reality.** Real content from the real source — never invented.
- **Structured & scannable.** Clear sections, strong hierarchy, generous spacing.
- **Beautiful & calm.** Use the shipped visual system as-is; don't restyle it.
- **Degrades gracefully.** Content visible without JS; JS only adds polish (scroll-spy, theme toggle, reveal).

## Structure — let the subject choose its sections

**No fixed section list. Build from what the subject actually is — use your judgment.**

**Always include (the core):**
1. **Hero** — title + one plain sentence on what it is and why it's worth the time.
2. **The gist** *(centerpiece)* — the plain-English through-line, 2–3 *short* paragraphs max. Never skip it; never let it swell into the whole report (see the chunking rules). If the subject has per-topic verdicts, follow the short prose with one `.save-row` per topic (topic → one-line verdict) instead of more paragraphs.
3. **The main content** — the substance, broken into a few sections that fit (key points, the argument, chapters, the process…).

**Then add only what genuinely applies** — and **invent sections freely**, named in the reader's terms. Common shapes: *Key points · How it works / The argument · Chapters or timeline · Examples & evidence · Pros & cons / trade-offs · Who it's for / when to use · Background & context · Notable quotes · Key numbers · Takeaways / what to do · Caveats & limits · Glossary · Sources.*

**Order & restraint:** lead with the gist, then order by what most helps understanding. Drop sections that don't earn their place — a focused 5-section page beats a padded one.

## Visual system — use the shipped kit

**Copy `template.html` from this skill's folder and fill it in.** It carries the calm palette (a warm cream "paper" theme as default + a warm-dark toggle, tuned for low-strain reading) and the full component kit, all self-contained. Keep its `<style>` and `<script>` verbatim; keep only the sections you need; update the `<title>`, brand, and TOC. Don't restyle — the calm look is the point.

**Hero scale guardrail:** keep the hero title at the template's normal reading scale. Do not replace `.hero h1` with `vw`, `vh`, or `clamp()` font-size rules, and do not force a narrow hero title width such as `10ch`-`14ch`. If the title wraps into stacked billboard words, shorten the `<h1>` and move detail into the lede or chips. Desktop hero titles should stay around 40-46px, mobile around 32-34px, with the next content visible in a normal first viewport.

**Visual QA gate:** before handing it off, look at the actual rendered page through Playwright, Chrome, the browser-control skill, or an equivalent real browser. Do not rely on static HTML inspection alone. Check desktop and mobile viewports, light and dark themes, hero title size, TOC behavior, console errors, horizontal overflow, and whether the first screen looks normal. Use screenshots or measured DOM values from the actual rendered page. If no browser path is available, say visual QA was not run and do not claim the page looks normal.

**Pick the component that fits the content shape:**

| Content shape | Component (class) |
|---|---|
| The flowing summary + inline glossary | `.summary-card` + `.gloss` |
| Ordered points / steps / chapters | `.stages` (numbered rail) |
| A set of parallel items (features, examples, who-it's-for) | `.info-grid` / `.info` cards |
| Any two-sided split (pros/cons, do/don't, before/after, myth/fact) | `.keepskip` / `.ks` |
| Paired rows (term → meaning, topic → verdict, Q → A) | `.save-row` |
| Key numbers / evidence dashboard | `.verified` / `.vstats` |
| A note, caveat, or pulled-out takeaway | `.callout` |
| A set of sources / links / related items | `.sys-grid` / `.sys` |
| Quick facts or tags in the hero | `.chips`, `.stat-strip` |
| Recurring colored meanings (use only if helpful) | `.tag` + a `.legend` |

## Build process

1. **Get the source.** Video → run the **watch** skill (transcript + frames). Article/page → read or fetch it. File → read it. Concept with no single source → research it. Capture: the one-line purpose, the gist, the main points, examples/numbers/quotes worth keeping, the jargon list (term → plain meaning), and any caveats.
2. **Distill to operator/reader altitude** — apply the altitude rule; cut the filler.
3. **Generate the single HTML** — copy `template.html`, choose the sections that fit (table above), fill them, delete the rest, wire the TOC.
4. **Verify before claiming done.** Confirm **no external requests** in the markup; then perform the **Visual QA gate** in a real browser (Playwright, Chrome, browser-control, or equivalent) before handing it off. Check desktop and mobile, both themes, TOC anchors, console errors, horizontal overflow, and hero scale. Run the **squint test** and the density limits from the chunking section — any paragraph over ~60 words, any bolded-label paragraph train, any number-stuffed sentence gets restructured before you ship.

## Relationship to automation-to-html

- **automation-to-html** → an engineering workflow, automation, pipeline, or codebase *you built/own* (explains the system without its internals).
- **html-for-general** *(this skill)* → everything else — content you consume or a topic you're explaining (video, article, paper, talk, concept, decision…).
- They **share the same visual system**, so outputs look like siblings.

## Common mistakes

- **Transcribing instead of distilling** — mirroring the runtime/length instead of surfacing the ideas. Cut hard.
- **The gist as a wall of text** — multi-topic 100+ word paragraphs with bolded topic labels and 5+ numbers each, all inside one card. That's the report crammed into prose; the gist is the through-line, and the data lives in structured sections.
- **Dense prose anywhere** — long paragraphs, 3-sentence bullets, sidebar-essay callouts. Apply the density limits; if a section fails the squint test, restructure it.
- **Inventing** beyond the source, or stating sampled/uncertain detail as fact.
- **Timestamp dumps** for videos instead of a real through-line.
- Any **external dependency** (CDN, web font, remote image); hiding primary content behind JS.
- **Restyling** the kit or going low-contrast — keep the calm palette as shipped.
- **Oversized hero titles** — never use viewport-scaled `h1` font sizes or very narrow `ch` widths that make the header dominate the page.
- Leaving **domain jargon** unexplained.
- Forcing a fixed section set — only the core (hero + gist + main content) is constant; everything else is by judgment.
