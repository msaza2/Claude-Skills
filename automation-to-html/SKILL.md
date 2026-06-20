---
name: automation-to-html
description: Use when the user wants a self-contained, visual HTML page that explains or visualizes an engineering workflow, automation, pipeline, data flow, or codebase — e.g. "build an HTML for this automation", "visualize this workflow", "make a workflow explainer", or turning a system's code/docs into a single-file, diagram-style reference.
---

# Automation to HTML

## Overview

Produce **one self-contained `.html` file** that explains **what an engineering workflow does and why it matters** — for the non-expert operator who owns it. It works for *any* workflow you build (an automation, a data transform, a service/API, a scheduled job, a monitor, a script, a library). The output is a **plain-language explainer with light, beautiful structure. It is NOT a code walkthrough.**

The owner often vibe-coded the system and does not want to track its churny internals. The implementation is subject to change; the purpose is not. Explain the purpose.

## The altitude rule (most important thing in this skill)

Write at the altitude of a **smart operator who has never read the code.** For every sentence, ask: *Would this make sense to the owner who only knows what the automation is for?* If it only makes sense to someone who read the source, **rewrite it in plain terms or cut it.**

**KEEP — what actually matters to the operator** (include the ones this workflow actually has — not every workflow has every item):
- **A plain-English summary of the whole thing.** Lead with this. It is the heart of the page.
- **How it gets access / signs in** (authentication), conceptually — including any **human-in-the-loop** step (e.g. a texted 2FA code).
- **What it's looking for vs. what it skips/ignores/filters** — the business rules (e.g. keep real, in-scope records; drop test, duplicate, or out-of-scope ones).
- **The meaningful checks and decisions, in business terms** (e.g. "an AI model double-checks each record for likely duplicates").
- **Where the results go and the KEY pieces of info it saves**, each explained in plain language (name → who the record is about; date; amount) — not a dump of field codes.
- **How it's tested / how you know it works** (unit tests, a safe "pretend" server, a dry-run mode that changes nothing, a verified live run).
- **The essentials it needs** (credentials/secrets), named **generally**: "the data-source login", "the CRM key & secret", "the texting bot". Not the config mechanics.
- **Concrete evidence** — a verified run with real numbers/ids, if it exists.

**OMIT or heavily demote — churny internals the operator does not care about:**
- **Libraries, frameworks, packages, binaries, dependencies — by name.** (They change. They're irrelevant to the owner.)
- **Schemas, data types, validation mechanics** (e.g. "validates with a Zod schema — URLs, positive ints, booleans"). The operator cares *that* it needs a password, not *how* the password is validated.
- **Internal code architecture, dependency-injection wiring, class/file names, design patterns.**
- **Exhaustive field-code tables, low-level fallback/plumbing logic, env-var schema tables, scheduler/cron plumbing** — unless the owner specifically asked.
- Anything whose honest summary is "this is *how the code is built*" rather than "this is *what it does*."

Name a specific file, class, or tool **only** when it genuinely helps the owner recognize or locate something they care about (e.g. the login method). Default to plain description. When the owner mentioned a tool themselves (e.g. "Playwright" for login), it's fine to keep — it's part of *how it signs in*, which they care about.

## Voice (the target)

Lead with a flowing, plain summary the owner could have written themselves. Example — a generic ingest→filter→sync automation, in the owner's own words:

> "It signs into a data source with a saved login and a browser, then pulls down the new records — each with its key details. It exports that list and filters out the ones that don't qualify — duplicates, test entries, anything out of scope — so only the real, usable ones remain. An AI model double-checks that screening, then it organizes every field and saves each record into the CRM in the CRM's format."

Match that altitude and tone. Supporting sections may go a little deeper, but never lose this voice.

## Audience: explain, don't assume (jargon)

The reader is technically sharp but **not** an expert in the system's subject-matter domain.

- **Keep general tech terms** as-is: API, CRM, email, login, CSV, file, queue. Fair game.
- **Explain or replace domain/industry jargon:**
  1. **Replace** a product- or industry-specific name with a general term when a generic one carries the meaning. *a specific product name → "the CRM".*
  2. **Gloss** the term the first time it matters. *"SKU" → "the code that identifies a specific product."*
- When in doubt, **gloss it.** If several domain terms survive, add a small **"In plain terms"** glossary near the top.
- During exploration, **collect a jargon list** (term → plain meaning) so nothing slips through unexplained.

## Non-negotiables

- **Self-contained.** One `.html`, zero external requests. Inline `<style>`, inline `<script>`, inline SVG. System font stacks only — **no CDN, no web fonts, no remote images.** Must render fully offline.
- **Grounded in reality.** Read the actual source and docs. Every behavior, business rule, field, and credential you mention must be real — never invented. Explore before you generate. (Grounded ≠ low-altitude: be accurate, but report it in plain terms.)
- **Structured & scannable.** Clear sections, strong hierarchy, generous spacing.
- **Beautiful.** Restrained palette, consistent visual language, simple diagrams — not a wall of text.
- **Degrades gracefully.** Content visible without JS; JS only adds polish (scroll-spy, theme toggle, reveal).

## Structure — let the workflow choose its sections

**There is no fixed section list. Build the page from what is actually true about *this* workflow — use your judgment.** An ingest→filter→sync automation, for instance, tends to have "keeps vs. skips," "how it signs in," and so on. A transform, a monitor, a generator, an API, a scheduled job, or a library will each want a different shape. Match the structure to the thing — don't pour every workflow into one mold.

**Always include (the core — true of almost any workflow):**
1. **Hero** — name + one-sentence plain-language purpose.
2. **In plain English** *(centerpiece)* — the flowing summary in the owner's voice. This is the heart; never skip it.
3. **How it works** — the main flow as a few big plain-language steps (or, if it isn't sequential, its key moving parts).

**Then add only the sections that genuinely apply** — pick from this menu, skip the rest:
- **What it keeps vs. skips / decides** — *if* it filters, screens, validates, or applies business rules.
- **How it signs in / gets access** — *if* it authenticates or needs permission, including any human-in-the-loop step.
- **What it produces / saves** — *if* it writes records, files, messages, or output. Key pieces in plain meaning; note nothing useful is discarded.
- **What it reads / takes in** — *if* its inputs (data, files, events) are worth naming.
- **When it runs** — *if* it's scheduled or event-triggered.
- **How it's tested / how you know it works** — *if* there are tests, a dry-run, a fake environment, or a verified run.
- **What it needs** — *if* it requires credentials, config, or setup. Named generally; no schema mechanics.
- **Systems it connects to** — *if* it touches external services. A simple touchpoint map, not an architecture diagram.
- **Failure & recovery / limits** — *if* how it handles errors, retries, or its boundaries matter to the owner.
- **Verified run / evidence** — *if* real confirmation exists (numbers, ids), as a small dashboard.

**Invent sections when the workflow calls for them**, named in the owner's terms — e.g. a data transform → *Inputs → Transformations → Outputs*; a monitor/alerter → *What it watches → When it alerts → Who it tells*; a generator → *What goes in → What comes out*; an API/service → *What you can ask it → What it answers*.

**Order & restraint:** lead with the summary, then order by what most helps understanding. A focused 4-section page that fits beats a padded 10-section one. Never add a section just because another workflow had it — and never force "keeps vs. skips" onto something that doesn't filter. Omit anything that would only carry internals (architecture/DI diagrams, env-var schema tables, dependency lists) unless the owner asks.

## Visual system

**Calm by default.** The palette is tuned for long, low-strain reading and a learning mood, grounded in reading-ergonomics and color-psychology research. A warm "paper"/cream light theme is the **default**; a gentle warm-dark is the toggle. The rules behind it:

- **Warm, not white or black.** Never a pure-white (`#fff`) page or pure-black (`#000`) text — both glare and cause "halation" (a glow/blur around text, worst for the ~half of people with astigmatism). Use a cream/paper background and a very dark *warm gray* for text.
- **High but not maximal contrast.** Aim body text ~12–16:1 — comfortably past WCAG AA (4.5:1), at/above AAA (7:1), but pulled back from the harsh 21:1 of black-on-white. Never fix harshness by going low-contrast; that strains too.
- **Calm canvas, small accent (≈60/30/10).** Most of the page is a low-saturation warm neutral; a calm muted tone supports it; only a tiny single accent carries action. **Saturation and brightness drive arousal — desaturate everything large**, save chroma for small accents.
- **Cool, muted accents.** A muted **teal** is the default accent (with a dusty-blue support tone); every semantic color is softened/desaturated yet kept in a distinct hue family (sage *keep*, taupe *skip*, plum *human*, blue *external*, green *check*, amber *rerun*, teal *data*). Pair color with a text/icon label — contrast math doesn't guarantee color-blind distinguishability. Reserve any warmer/higher-energy tone (the amber) for a rare, intentional signal only.
- **Light default for sustained reading**; keep a warm-dark theme for low light — off-white text on warm charcoal, never `#fff` on `#000`.
- **Restraint.** Gentle reveal only; generous whitespace; reading measure ~64–70ch; comfortable body size (~15.5px+), line-height ~1.6.

**Drop-in token palette** (CSS custom properties; cream light is the default — set `<html ... data-theme="light">`). Copy verbatim:

```css
/* warm-dark (fallback base / toggle) — warm near-black, off-white text, desaturated accents */
:root{
  --bg:#1c1a17; --bg-1:#211e1a; --bg-2:#26231e; --surface:#26231e; --surface-solid:#2f2b24;
  --border:#3b362d; --hair:#322e27;
  --text:#e9e2d4; --muted:#b3ab9b; --faint:#847c6d;
  --accent:#79b6ae; --accent-2:#8fb3cc; --accent-ink:#1c1a17;
  --rail:linear-gradient(180deg,#79b6ae55,#8fb3cc55 40%,#847c6d33 80%,#1c1a1700);
  --shadow:0 1px 2px #00000050, 0 12px 30px -12px #00000080;
  --c-keep:#8fb58e; --c-skip:#aba191; --c-human:#c79cba; --c-external:#8fb3cc;
  --c-check:#86be8e; --c-rerun:#d6a659; --c-data:#79b6ae;
}
/* warm "paper" cream — the default view (set on <html>) */
html[data-theme="light"]{
  --bg:#faf6ee; --bg-1:#f6f1e7; --bg-2:#f1ebde; --surface:#fffdf8; --surface-solid:#f3eee2;
  --border:#ddd5c4; --hair:#ebe5d8;
  --text:#23211c; --muted:#5c564c; --faint:#857c6e;
  --accent:#2e6e68; --accent-2:#3d6585; --accent-ink:#faf6ee;
  --rail:linear-gradient(180deg,#2e6e6855,#3d658555 40%,#857c6e33 80%,#faf6ee00);
  --shadow:0 1px 2px #4a44320f, 0 10px 30px -14px #4a443233;
  --c-keep:#4a6f4e; --c-skip:#6b6258; --c-human:#7a4a6b; --c-external:#3d6585;
  --c-check:#3f7350; --c-rerun:#8a5a1e; --c-data:#2e6e68;
}
```
*(Body text ~14.9:1 light / ~13.5:1 dark — AAA; every accent and all seven semantic colors verified ≥ AA 4.5:1 on their own background. `faint` is the only sub-4.5 token — restrict it to large/de-emphasized labels, never small body copy.)*
*Evidence anchors:* warm sepia/paper (Kindle `#FBF0D9`) lowers effective screen radiance vs. white; the CMU/ASSETS reading study found warm backgrounds improved reading speed; NN/g warns low-contrast also strains; the Salford HEAD classroom study found learning peaks at *moderate* stimulation (muted neutral canvas + a small accent), with oversaturation hurting focus.

- **Semantic tags (a menu, not a requirement)** — a small set of reusable colored chips for recurring meanings; use the ones that fit *this* workflow and add your own, with a small legend. Common ones: `keep` / `skip`, `human-in-loop`, `external system`, `automated check`, `safe to re-run`. A workflow that doesn't filter won't use keep/skip; reserve the warm accent for genuine alerts. Always pair color with a text/icon label.
- **Navigation:** sticky left TOC with scroll-spy active state; smooth scroll; collapses under ~980px.
- **Components:** cards with hairline borders + subtle shadows; a simple numbered step flow; inline stroke SVG icons (24×24, `currentColor`); reveal-on-scroll via IntersectionObserver (default-visible fallback).
- **Type:** system sans stack for prose, system mono stack only where a real identifier genuinely helps.
- **Hero scale guardrail:** keep the hero title at normal reading scale. Do not use viewport-scaled `h1` rules such as `vw`, `vh`, or `clamp()` for the hero title, and do not force a narrow title width such as `10ch`-`14ch`. If the title wraps into stacked billboard words, shorten the `<h1>` and move detail into the lede or chips. Desktop hero titles should sit around 40-46px, mobile around 32-34px.
- **Visual QA gate:** before handing it off, look at the actual rendered page through Playwright, Chrome, the browser-control skill, or an equivalent real browser. Static HTML inspection is not enough. Check desktop and mobile viewports, light and dark themes, hero title size, TOC behavior, console errors, horizontal overflow, and whether the first screen looks normal. Use screenshots or measured DOM values from the actual rendered page. If no browser path is available, say visual QA was not run and do not claim the page looks normal.

## Build process

1. **Explore the real system** — read the code and docs; for anything non-trivial, fan out parallel readers (the Workflow tool). Capture the **plain map**: the one-line purpose, the flowing summary, the big steps — then *whichever of these the workflow actually has*: how it authenticates, what it filters/decides, what it reads and produces, when it runs, how it's tested, the credentials it needs (named generally), the external systems, any verified run — **plus the jargon list (term → plain meaning).** Note anything important none of these capture; that becomes its own section.
2. **Translate everything to operator altitude** — drop the internals per the altitude rule.
3. **Generate the single HTML** following the visual system. Apply the audience + altitude rules to every line.
4. **Verify before claiming done.** Confirm **no external requests** in the markup; then perform the **Visual QA gate** in a real browser (Playwright, Chrome, browser-control, or equivalent) before handing it off. Check desktop and mobile, both themes, TOC anchors, console errors, horizontal overflow, and hero scale. Screenshot or record measured DOM values from the actual rendered page; if browser QA cannot run, say so plainly.

## Reference exemplar

The **`template.html` component kit** from the sibling `html-for-general` skill (it shares this exact visual system) is the **quality bar and starting point** — copy its CSS tokens, calm theme, typography, cards, step rail, and overall polish *verbatim*; that's what carries the look and articulation. Treat any one page's **section lineup as an example, not a mold**: an ingest→filter→sync automation has keeps/skips, sign-in, etc., but yours may not. Reuse the *craft*; choose *sections* per the Structure rule above.

## Common mistakes

- **Deep-diving the code** instead of explaining what the automation does. The owner doesn't read the source.
- Naming **libraries, binaries, schemas, classes, or dependencies** the owner doesn't care about (subject to change).
- Dumping **field-code tables** instead of plain meaning ("cust_id → the customer it refers to").
- Leading with **architecture or config** instead of the plain summary.
- Surfacing **validation/plumbing detail** ("Zod schema, URL/int/boolean checks") when the operator only needs "it requires a password."
- **Forcing a sample section set** onto a workflow it doesn't fit — e.g. inventing a "keeps vs. skips" when nothing is filtered, or "how it signs in" when it touches nothing external. Let the workflow choose its sections; the core (hero + plain summary + how it works) is the only constant.
- **Oversized hero titles** — never use viewport-scaled `h1` font sizes or very narrow `ch` widths that make the header dominate the page.
- Inventing behavior; any external dependency (CDN, fonts, remote image); hiding primary content behind JS; leaving domain jargon unexplained.
