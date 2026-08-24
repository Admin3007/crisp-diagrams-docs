---
title: Crisp Diagrams
---

# Crisp Diagrams for Confluence

**Mermaid diagrams that stay sharp.** True SVG, full page width, live preview while you type.
No account. Nothing leaves Atlassian.

[Get started](guides/getting-started) · [Templates](templates) · [Real-world examples](examples/) ·
[Styling](guides/styling) · [Troubleshooting](guides/troubleshooting)

---

## The problem it solves

Most Confluence Mermaid apps save your diagram as a small raster image. Zoom in to read a label and
it turns to mush. One of the two most-installed apps in this category is rated **2.9/5**, and the
reviews say why:

> *"The generated diagrams are tiny and blurry, and therefore useless."*

> *"It only stores very small PNG images… This would be completely fixed if they stored diagrams as
> SVGs."*

Crisp renders **real vector graphics**. Zoom to 400% and every line is still a line.

---

## What it does

| | |
|---|---|
| **True SVG output** | Never a rasterised screenshot. Crisp at any zoom. |
| **Full page width** | No artificial size ceiling. |
| **Zoom, pan, full screen** | Large architecture diagrams stay usable. |
| **Live preview** | See the diagram as you type, side by side with the source. |
| **Precise errors** | The exact line and character — not "something went wrong". |
| **Proper dark mode** | Follows your Confluence theme instead of pasting a white box on a dark page. |
| **`classDef` works** | Your colours render the way you wrote them. |
| **SVG + PNG download** | Labels included, in any viewer — not just a browser. |
| **19 diagram types** | Every type below is tested against the shipping build. |

Flowchart · Sequence · Class · State · ER · Journey · Gantt · Pie · Quadrant · Requirement ·
Git graph · C4 · Mindmap · Timeline · XY chart · Block · Sankey · Kanban · Architecture

---

## No account. Ever.

Some Mermaid apps require **every person on your team** to create and log into a third-party account
before they can draw a box. The single most-upvoted review in this category is someone giving up
because of exactly that.

Crisp doesn't. Install it and it works, for everyone, immediately.

---

## Your data never leaves Atlassian

Crisp carries Atlassian's **Runs on Atlassian** badge. Atlassian grants it only to apps that use
exclusively Atlassian-hosted compute and storage and **do not egress data**. It is verified by
Atlassian, not self-declared.

Concretely:

- **Zero external network requests.** Mermaid is bundled into the app, not loaded from a CDN.
- **No analytics, no tracking, no cookies, no fingerprinting.**
- **No third-party account**, so there is no third party.
- Your diagram source is stored in the macro on your own Confluence page.

### Verify it yourself

You don't have to take our word for any of this:

1. Open a page with a Crisp diagram
2. Open your browser's developer tools → **Network** tab
3. Reload and watch

No request leaves your Atlassian domain. Then **disconnect from the internet** — the diagram still
renders, zooms and exports, because all of it runs in your browser.

---

## Free

Crisp Diagrams is free. No trial, no seat limit, no feature gate.

---

## Links

- [Getting started](guides/getting-started)
- [Real-world examples](examples/)
- [Styling diagrams](guides/styling)
- [Troubleshooting](guides/troubleshooting)
- [Privacy policy](privacy)
- [End user terms](terms)
- [Support — open an issue](https://github.com/Admin3007/crisp-diagrams-docs/issues)

---

## Common questions

- [Why do my Confluence diagrams go blurry?](why-diagrams-blur) — what raster storage costs you, and how to tell which kind you have
- [Can I use Mermaid without a third-party account?](no-account-required) — why some apps demand a sign-up, and how to verify one does not
- [How do I move from PlantUML?](plantuml-to-mermaid) — syntax mapping, and the cases where you should stay put
- [Where are the diagram templates?](templates) — a starting point for all nineteen types
- [My diagram is not rendering](guides/troubleshooting) — symptom index and fixes
- [Security and vulnerability reporting](security) — posture, and how to report an issue
