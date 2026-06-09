# claude-skills

Two [Claude](https://claude.com/claude-code) skills for turning things into **beautiful, self-contained HTML explainers** — one `.html` file, inline CSS/JS, no external dependencies, renders fully offline.

Both share the same calm visual system: a warm "paper" light theme with a warm-dark toggle, tuned for low-strain reading, with a sticky table of contents, scroll-spy, and a tidy component kit.

## Skills

### `html-for-general`
Turn any **non-code subject** — a video, article, paper, talk, report, dataset, product, concept, or decision — into one self-contained `.html` explainer written for a smart reader who's new to it. It distills the material to its essence (lead with the gist, keep what matters, cut the filler) rather than transcribing it. Ships with `template.html`, the full component kit and visual system.

> e.g. *"make an HTML explaining this video"*, *"turn this article into a visual explainer"*

### `automation-to-html`
Turn an **engineering workflow you own** — an automation, pipeline, data transform, service/API, scheduled job, or script — into a plain-language, single-file HTML explainer of *what it does and why it matters*. It's deliberately **not** a code walkthrough: it explains the system at the altitude of the person who owns it, not the person who wrote every line. Shares the visual system from `html-for-general`.

> e.g. *"build an HTML for this automation"*, *"visualize this workflow"*

## Non-negotiables (both skills)

- **Self-contained** — one `.html`, zero external requests. Inline `<style>`, inline `<script>`, inline SVG. System fonts only — no CDN, no web fonts, no remote images.
- **Grounded** — every claim traces to the real source; nothing invented.
- **Calm & scannable** — strong hierarchy, generous spacing, accessible contrast.
- **Degrades gracefully** — content is visible without JavaScript; JS only adds polish.

## Install

Copy the skill folders into your Claude skills directory:

```
~/.claude/skills/html-for-general/
~/.claude/skills/automation-to-html/
```

On Windows that's `%USERPROFILE%\.claude\skills\...`.

Then just ask Claude in natural language (see the examples above) and it will pick up the matching skill.

## License

[MIT](LICENSE) — free to use, change, and share.
