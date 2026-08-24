---
title: Styling diagrams
---

# Styling diagrams

Crisp renders unstyled diagrams in a restrained neutral-blue palette that matches Confluence, in
both light and dark mode. You don't have to style anything for a diagram to look finished.

When you *do* reach for colour, the guidance below keeps it meaning something.

---

## The rule

**Colour should carry information.** A diagram where every node is a different colour communicates
nothing; a diagram where two nodes are red communicates "look here".

Reserve colour for:

- The critical path
- Deprecated or to-be-removed components
- Trust boundaries and external systems
- Status — done, in progress, blocked

Not for: making it look nicer. The default palette already handles that.

---

## classDef

Define a class, then apply it to node IDs:

```
flowchart LR
  A[Ingest] --> B[Transform]
  B --> C[Publish]
  B --> D[Legacy export]

  classDef deprecated fill:#FFECEB,stroke:#C9372C,stroke-width:2px
  class D deprecated
```

Two rules that catch people out:

1. `classDef` must appear **after** the nodes exist
2. `class` takes **node IDs**, not labels — `class D deprecated`, not `class "Legacy export" ...`

---

## A palette that works in both themes

If you set explicit colours, they override the theme — so pick shades legible on both a white and a
dark page. These are Atlassian's semantic colours and are safe in both:

```
classDef success  fill:#DDF3E4,stroke:#1F845A,stroke-width:2px
classDef warning  fill:#FFF7D6,stroke:#946F00,stroke-width:2px
classDef danger   fill:#FFECEB,stroke:#C9372C,stroke-width:2px
classDef info     fill:#E9F2FE,stroke:#1868DB,stroke-width:2px
classDef muted    fill:#F1F2F4,stroke:#8590A2,stroke-width:2px
```

Light fills with a saturated border read well on either background. Dark fills do not — a
`fill:#1F845A` node becomes unreadable on a dark page.

---

## Grouping with subgraph

For anything with more than about eight nodes, grouping does more for legibility than colour:

```
flowchart LR
  subgraph Edge
    LB[Load Balancer]
  end
  subgraph Application
    A1[API 1]
    A2[API 2]
  end
  subgraph Data
    C[(Cache)]
    D[(Primary DB)]
  end
  LB --> A1
  LB --> A2
  A1 --> C
  A2 --> C
  C --> D
```

Subgraphs also help the layout engine compact the diagram, so it renders shorter.

---

## Node shapes carry meaning too

Shape is free information — use it before you use colour:

| Syntax | Shape | Conventional use |
|---|---|---|
| `A[Text]` | Rectangle | Process, service |
| `A(Text)` | Rounded | Start / end |
| `A([Text])` | Stadium | Entry point |
| `A[[Text]]` | Subroutine | Queue, job |
| `A[(Text)]` | Cylinder | Datastore |
| `A{Text}` | Diamond | Decision |
| `A{{Text}}` | Hexagon | Preparation |
| `A>Text]` | Flag | Note, annotation |

---

## Line styles

```
A --> B      solid — primary flow
A -.-> B     dotted — secondary, async, or read-only
A ==> B      thick — emphasised path
A --- B      solid, no arrow — association
```

A dotted line for async or read-only paths is one of the highest-value conventions you can adopt;
it removes a whole class of "does this call block?" questions.

---

## Direction

`flowchart LR` (left to right) almost always beats `TD` (top down) on a Confluence page. Pages are
wider than they are tall, `LR` uses the space you have, and the diagram renders larger as a result.

Use `TD` for decision trees and approval flows, where the top-down reading order matches how
someone actually follows the process.
