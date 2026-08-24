---
title: Why Confluence diagrams go blurry
description: Why Mermaid diagrams in Confluence turn to mush when you zoom in, what causes it, and how to fix it.
---

# Why your Confluence diagram is blurry

You wrote a clean architecture diagram. On the page it looks fine. You zoom in to read a
label and the text turns to mush.

That is not your diagram. It is how the app stored it.

---

## The cause: a picture of a diagram, not the diagram

Most Confluence Mermaid apps render your text once, on a server or at save time, and store
the result as a **PNG** — a grid of coloured pixels at one fixed size.

A PNG has no idea what a letter is. It only knows that pixel 412 was dark grey. Ask the
browser to display it at twice the size and it has to invent the pixels in between, which is
why edges go soft and small text becomes an unreadable smear.

It gets worse in three ordinary situations:

- **A high-DPI screen.** A MacBook or a 4K monitor draws roughly twice as many physical
  pixels per CSS pixel. A raster diagram sized for a standard display is already being
  stretched before you touch the zoom.
- **Browser zoom.** Anyone reading at 125% — very common — is seeing an upscaled image.
- **Exports and print.** PDF and print run at a much higher resolution than a screen, so a
  raster diagram that looked acceptable on the page comes out visibly soft on paper.

None of this is a rendering bug. It is a storage decision that cannot be undone later.

---

## The fix: store the diagram, not a picture of it

**SVG** — Scalable Vector Graphics — stores the diagram as instructions: *a rectangle here,
a line from this point to that one, the word "Gateway" in this font at this size.*

The browser redraws it at whatever size it is asked for. At 400% the text is still text,
rendered fresh, using the same font engine that draws the rest of your page. There is no
resolution to run out of, because there was never a grid of pixels to begin with.

Three consequences that matter day to day:

| | Raster (PNG) | Vector (SVG) |
|---|---|---|
| Zoom to read a label | Blurs | Stays sharp |
| High-DPI screen | Soft | Sharp |
| Print or PDF | Soft | Sharp |
| Find text on the page | Impossible | The labels are real text |
| File size, large diagram | Grows with pixels | Grows with shapes |

---

## How to check which one you have

You do not need to take anyone's word for it.

1. Open a page with a diagram on it.
2. Zoom your browser to 300% (<kbd>Ctrl</kbd>/<kbd>Cmd</kbd> and <kbd>+</kbd>).
3. Look at the smallest label.

Crisp text means vector. Soft, fuzzy edges mean a stored image.

For a second opinion, right-click the diagram. If the menu offers **"Save image as…"** you
are looking at a raster image. A vector diagram has no single image to save.

---

## What Crisp Diagrams does

It renders **real SVG in your browser**, every time the page loads. Nothing is stored as a
picture, so there is no resolution to run out of:

- Zoom to 400% and every line is still a line
- Sharp on any screen, at any browser zoom, in print
- Downloads as SVG with labels intact — or as PNG at 3× if you need a raster to paste
  somewhere
- The rendering happens in your browser, so **no request leaves your Atlassian domain**

[Get started](guides/getting-started) · [See worked examples](examples/) ·
[Diagram templates](templates)

---

## Related

- [My diagram is not rendering](guides/troubleshooting) — when nothing appears at all
- [Mermaid in Confluence without an account](no-account-required) — if you have hit a
  third-party sign-up wall
- [Moving from PlantUML](plantuml-to-mermaid) — syntax mapping and honest trade-offs
