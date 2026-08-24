---
title: Getting started
---

# Getting started

Five minutes from installing to your first diagram on a page.

---

## 1. Install

Find **Crisp Diagrams** on the Atlassian Marketplace and install it into your Confluence Cloud site.
You need Confluence admin rights to install an app, but **anyone can use it once installed** — there
is no per-user setup, no account, and nothing to sign into.

## 2. Insert the macro

On any Confluence page, in the editor:

- Type `/mermaid` and pick **Mermaid Diagram**, or
- Click **+** in the toolbar, search for *Mermaid*, and select it

The editor opens automatically the first time.

## 3. Write your diagram

You get a split view: **Mermaid source** on the left, **live preview** on the right. The preview
updates as you type — no save-and-check loop.

Start with something simple:

```
flowchart LR
  A[Request] --> B{Cache hit?}
  B -->|Yes| C[(Cache)]
  B -->|No| D[Origin]
```

The badge at the top right of the editor shows **Valid** while your syntax parses, and **Syntax
error** with the exact line number when it doesn't.

## 4. Save

Click **Save**. The dialog closes and your diagram appears on the page.

## 5. Use it

Hover over any diagram to reveal the toolbar:

| Control | What it does |
|---|---|
| **−** / **+** | Zoom out / in |
| **Reset** | Fit the diagram back to the page width |
| **⤢** | Full screen |
| **SVG** | Download as vector — sharp at any size |
| **PNG** | Download as a 3× raster image |

You can also **drag to pan** and **Ctrl/Cmd + scroll to zoom** directly on the diagram.

> Plain scrolling deliberately scrolls the page rather than zooming the diagram — so a diagram in
> the middle of a long page never traps your scroll.

---

## Editing later

Select the macro on the page and choose **Edit**. The same split editor opens with your source
intact.

## Changing the theme

The **Theme** control in the editor has three options:

- **Match Confluence** *(default)* — follows your Confluence light/dark setting automatically
- **Light** — always light
- **Dark** — always dark

Most of the time you want *Match Confluence*, so the diagram looks right for every reader
regardless of their own theme preference.

---

## Next

- [Real-world examples](../examples/) — copy-paste diagrams for common documentation jobs
- [Styling diagrams](styling) — colour, emphasis, and when to use it
- [Troubleshooting](troubleshooting) — when something doesn't render
