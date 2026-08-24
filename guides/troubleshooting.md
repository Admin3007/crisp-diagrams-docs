---
title: Troubleshooting
---

# Troubleshooting

---

## "Syntax error" with a line number

The editor validates as you type and tells you the exact line and character.

Most common causes:

**Unclosed bracket.** `A[Start` instead of `A[Start]`. The caret in the error points at where the
parser gave up, which is usually just after the real mistake.

**Wrong arrow for the diagram type.** Flowcharts use `-->`, sequence diagrams use `->>`, class
diagrams use `-->` with different semantics. Copying an arrow between diagram types is a frequent
trap.

**Special characters in labels.** Parentheses, quotes and `#` inside a label confuse the parser.
Wrap the label in quotes:

```
A["Order (pending)"]
```

**A stray blank first line.** The diagram type must be the first non-empty line.

---

## Diagram is smaller than I expected

Crisp deliberately **never scales a diagram above its natural size**. A small three-node flowchart
on a wide page renders at its real size rather than being blown up until the boxes look like
buttons.

If you want it larger, **zoom in** — the output is vector, so it stays perfectly sharp at any
magnification. Use **+** on the hover toolbar, `Ctrl`/`Cmd` + scroll, or **⤢** for full screen.

To genuinely make the diagram bigger rather than just magnified, add content or change direction —
`flowchart LR` (left to right) uses horizontal space that `flowchart TD` (top down) leaves empty.

---

## Diagram is very tall and pushes content down

Crisp caps the rendered height so one diagram can't swallow the whole page. If your diagram is
taller than the cap, it fits to the visible area and you pan or full-screen it.

For genuinely large diagrams, consider:

- Switching `TD` to `LR` — wide beats tall on a page
- Splitting into two diagrams with a shared entry point
- Using `subgraph` to group related nodes so the layout engine can compact them

---

## Labels overlap the connector lines

Crisp draws every edge label on an opaque, bordered chip specifically so the line passes cleanly
behind the text. If labels still look crowded, the diagram is usually too dense for its direction —
try `LR` instead of `TD`, or shorten the labels.

---

## My colours aren't applying

`classDef` must come **after** the nodes it targets are defined, and `class` must reference node
IDs, not labels:

```
flowchart LR
  A[Start] --> B[End]
  classDef done fill:#DDF3E4,stroke:#1F845A,stroke-width:2px
  class A,B done
```

`class A,B done` — not `class Start,End done`.

---

## Dark mode looks wrong

Set **Theme → Match Confluence** in the editor. That is the default and follows each reader's own
Confluence appearance setting, so the diagram is correct for everyone.

If you hard-code **Light** or **Dark**, readers on the opposite setting will see a diagram that
doesn't match the page around it.

If you set explicit colours with `classDef`, those win over the theme in both modes — which is
usually what you want for semantic colour, but means you should pick shades that work on both a
white and a dark background.

---

## The diagram didn't appear at all

**Check the macro is configured.** A freshly inserted macro with no source shows *"No diagram
yet"* with a prompt to edit it. That is expected, not a failure.

**Reload the page.** Confluence caches macro output aggressively.

**Check the source parses.** Open the editor — the badge tells you immediately.

---

## Export produced an image with no text

This was a real bug in earlier builds and is fixed. Crisp now converts every label to a true SVG
text element before export, so downloaded SVG and PNG files carry their labels in any viewer, not
just a browser.

If you see it, you are on an old cached build — reload the page.

---

## Does it work offline?

Yes, after the page has loaded once. Everything runs in your browser and the app makes no external
network requests. You can disconnect from the internet and the diagram will still render, zoom and
export.

That is also how you can verify the privacy claim yourself — see [Privacy](../privacy).

---

## Still stuck?

Open an issue at
[github.com/Admin3007/crisp-diagrams-docs/issues](https://github.com/Admin3007/crisp-diagrams-docs/issues).

Include the diagram source that reproduces it — that is almost always enough to diagnose it.
