---
title: Moving from PlantUML to Mermaid in Confluence
description: An honest comparison of PlantUML and Mermaid for Confluence, with a syntax mapping for the common diagram types.
---

# Moving from PlantUML to Mermaid

If your team already writes PlantUML, switching is a real decision with real costs. This
page is meant to help you make it accurately, including the cases where you should not.

---

## The honest summary

**PlantUML is more capable.** It has been around longer, covers more diagram types, and
handles some things Mermaid simply cannot. If you depend on those, stay where you are.

**Mermaid is easier to host.** It runs in a browser. PlantUML is a Java application that
renders on a server, which is why PlantUML apps for Confluence either ship a server
dependency or send your diagram to one.

That single architectural difference drives most of what follows.

### Stay with PlantUML if you need

- **Deployment, timing, object, or use-case diagrams** — Mermaid has no equivalent
- **Salt wireframes** or **Ditaa** ASCII conversion
- **`!include` across files**, shared macro libraries, or a preprocessor
- **Very fine layout control** — PlantUML's `together`, `hidden` links and directional
  hints are more expressive than anything Mermaid offers
- **An existing library of hundreds of diagrams.** Migration is not free, and "it renders"
  is not the same as "it looks right"

### Mermaid is the better fit if

- Your diagrams are **flowcharts, sequence, class, state, ER, Gantt or C4** — the common
  cases, all well covered
- You want **no server**, no Java, and no diagram content leaving Atlassian
- You want a **live preview while you type** rather than save-and-check
- You care that the output is **vector**, not a rendered image

---

## Syntax mapping

The good news for the common types: the concepts map almost one to one.

### Sequence diagrams

**PlantUML**

```
@startuml
Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response
Alice -> Bob: Another request
@enduml
```

**Mermaid**

```
sequenceDiagram
  Alice->>Bob: Authentication Request
  Bob-->>Alice: Authentication Response
  Alice->>Bob: Another request
```

| PlantUML | Mermaid | Note |
|---|---|---|
| `@startuml` / `@enduml` | *(omitted)* | The macro is the boundary |
| `->` | `->>` | Solid arrow |
| `-->` | `-->>` | Dashed arrow |
| `participant X as Y` | `participant X as Y` | Identical |
| `activate` / `deactivate` | `activate` / `deactivate` | Identical |
| `note left of X` | `Note left of X` | Capital N in Mermaid |
| `autonumber` | `autonumber` | Identical |

### Class diagrams

**PlantUML**

```
@startuml
class Order {
  +String id
  +total() float
}
Customer "1" --> "*" Order : places
@enduml
```

**Mermaid**

```
classDiagram
  class Order {
    +String id
    +total() float
  }
  Customer "1" --> "*" Order : places
```

Visibility markers (`+`, `-`, `#`) work the same. Relationship arrows differ slightly:
Mermaid uses `<|--` for inheritance, `*--` for composition, `o--` for aggregation — the
same UML vocabulary, spelled marginally differently.

### Flowcharts and activity diagrams

This is where the two genuinely diverge. PlantUML activity diagrams use a start/stop
keyword flow; Mermaid uses an explicit node-and-edge graph.

**PlantUML**

```
@startuml
start
if (valid?) then (yes)
  :Process;
else (no)
  :Reject;
endif
stop
@enduml
```

**Mermaid**

```
flowchart TD
  A([Start]) --> B{Valid?}
  B -->|yes| C[Process]
  B -->|no| D[Reject]
  C --> E([Stop])
  D --> E
```

Mermaid is more verbose here because you name every node. In exchange you can style and
reference those nodes individually, which PlantUML's activity syntax does not let you do.

### Entity relationship

**PlantUML** uses `entity` blocks with `||--o{` crow's feet. **Mermaid's** `erDiagram` uses
the *same* crow's-foot notation:

```
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE_ITEM : contains
```

If you know PlantUML's ER notation you already know Mermaid's.

### C4

Both support C4. PlantUML uses the `C4-PlantUML` include library; Mermaid has C4 built in
with near-identical macros — `Person()`, `System()`, `Rel()`, `System_Ext()`. Diagrams
usually port with only the `!include` line removed.

---

## What to expect when you migrate

**Layout will change.** Both tools lay out automatically, and they disagree. A diagram that
was carefully arranged in PlantUML will come out differently. Budget time to re-tune, and
convert your most-viewed diagrams first so you find the sharp edges early.

**Some things need rethinking, not translating.** Anything relying on `!include`, macros or
the preprocessor has no direct equivalent. Inline it or drop it.

**Test the awkward ones first.** Migrate your largest and your ugliest diagram before
committing. If those two survive, the rest will.

---

## Trying it

Type `/mermaid` on any Confluence page. The **Examples** menu has a starting point for each
of the nineteen types, so you can paste a PlantUML diagram beside a Mermaid one and compare
before deciding anything.

[Get started](guides/getting-started) · [Diagram templates](templates) ·
[Worked examples](examples/)

---

## Related

- [Why Confluence diagrams go blurry](why-diagrams-blur)
- [Mermaid without a third-party account](no-account-required)
- [Troubleshooting](guides/troubleshooting)
