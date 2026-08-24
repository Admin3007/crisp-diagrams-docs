---
title: Confluence diagram templates
description: Copy-paste Mermaid templates for Confluence — architecture, sequence, ER, C4, Gantt, state and fourteen more.
---

# Diagram templates for Confluence

A starting point for every diagram type. Copy one, paste it into a Mermaid Diagram macro,
and edit it — or skip the copying and pick the same template from the
**Examples** menu inside the editor.

All 20 are the exact templates the app ships, generated from the same file, so this
page cannot drift from what you actually get.

> **To use one:** type `/mermaid` on any Confluence page, choose **Mermaid Diagram**,
> then pick from **Examples** in the editor footer. Loading an example offers an
> Undo, so it will not quietly overwrite work in progress.

---

## Jump to

[Flowchart](#flowchart) · [Service architecture](#service-architecture) · [Sequence diagram](#sequence-diagram) · [Class diagram](#class-diagram) · [State diagram](#state-diagram) · [Entity relationship](#entity-relationship) · [C4 system context](#c4-system-context) · [Gantt chart](#gantt-chart) · [User journey](#user-journey) · [Mindmap](#mindmap) · [Timeline](#timeline) · [Kanban board](#kanban-board) · [Git graph](#git-graph) · [Pie chart](#pie-chart) · [XY chart](#xy-chart) · [Quadrant chart](#quadrant-chart) · [Requirement diagram](#requirement-diagram) · [Block diagram](#block-diagram) · [Sankey diagram](#sankey-diagram) · [Architecture (beta)](#architecture-beta-)

---

## Flowchart

```
flowchart TD
  A[Request received] --> B{Valid?}
  B -->|Yes| C[Process]
  B -->|No| D[Reject with reason]
  C --> E[(Store result)]
  C --> F[Notify caller]
```

## Service architecture

```
flowchart LR
  subgraph Edge
    CDN[CDN] --> GW[API Gateway]
  end
  subgraph Services
    GW -->|verify| AUTH[Auth]
    GW -->|orders| ORD[Orders]
  end
  ORD -->|publish| Q[[Event bus]]
  Q -->|consume| W[Worker]
  ORD --> DB[(Orders DB)]
```

## Sequence diagram

```
sequenceDiagram
  autonumber
  participant C as Checkout
  participant P as Payments
  participant L as Ledger
  C->>P: POST /charge
  P->>L: reserve funds
  L-->>P: ok
  P-->>C: 201 Created
```

## Class diagram

```
classDiagram
  class Order {
    +String id
    +Money total
    +place() bool
  }
  class Customer {
    +String email
  }
  Customer "1" --> "*" Order : places
```

## State diagram

```
stateDiagram-v2
  [*] --> Draft
  Draft --> InReview: submit
  InReview --> Draft: changes requested
  InReview --> Approved: approve
  Approved --> Published: publish
  Published --> [*]
```

## Entity relationship

```
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE_ITEM : contains
  CUSTOMER {
    string email
    string name
  }
  ORDER {
    string id
    date placed_at
  }
```

## C4 system context

```
C4Context
  title Order platform — system context
  Person(cust, "Customer", "Places and tracks orders")
  System(shop, "Order platform", "Checkout and fulfilment")
  System_Ext(pay, "Payment provider", "Card capture")
  Rel(cust, shop, "Browses and orders", "HTTPS")
  Rel(shop, pay, "Captures payment", "REST")
```

## Gantt chart

```
gantt
  title Release plan
  dateFormat YYYY-MM-DD
  section Build
    Engine        :a1, 2026-09-01, 20d
    Interface     :after a1, 12d
  section Launch
    Beta          :2026-10-05, 10d
    General       :2026-10-20, 5d
```

## User journey

```
journey
  title Checkout
  section Browse
    View item: 5: Customer
    Add to cart: 4: Customer
  section Pay
    Enter card: 3: Customer
    Confirm: 5: Customer
```

## Mindmap

```
mindmap
  root((Product))
    Discovery
      Interviews
      Analytics
    Delivery
      Build
      Ship
    Support
```

## Timeline

```
timeline
  title Roadmap
  2026 Q3 : Launch
          : First customers
  2026 Q4 : More formats
  2027 Q1 : Team plan
```

## Kanban board

```
kanban
  Todo
    [Write the docs]
    [Design the icon]
  In progress
    [Cross-browser testing]
  Done
    [Ship v1]
```

## Git graph

```
gitGraph
  commit
  branch feature
  commit
  commit
  checkout main
  merge feature
  commit
```

## Pie chart

```
pie title Where installs come from
  "Marketplace search" : 45
  "In-product browse" : 30
  "Community" : 25
```

## XY chart

```
xychart-beta
  title "Installs by month"
  x-axis [Sep, Oct, Nov, Dec]
  y-axis "Installs" 0 --> 500
  line [40, 120, 280, 430]
```

## Quadrant chart

```
quadrantChart
  title Effort against impact
  x-axis Low effort --> High effort
  y-axis Low impact --> High impact
  Templates: [0.3, 0.8]
  Dark mode: [0.4, 0.5]
  Rewrite: [0.9, 0.6]
```

## Requirement diagram

```
requirementDiagram
  requirement crisp {
    id: 1
    text: Diagrams stay sharp at any zoom
    risk: high
    verifymethod: test
  }
  element viewer {
    type: component
  }
  viewer - satisfies -> crisp
```

## Block diagram

```
block-beta
  columns 3
  Web["Web app"] API["API"] DB[("Database")]
  space:3
  Cache["Cache"] Queue["Queue"] Store["Object store"]
```

## Sankey diagram

```
sankey-beta

Visitors,Listing page,600
Visitors,Bounce,400
Listing page,Install,180
Listing page,Left,420
```

## Architecture (beta)

```
architecture-beta
  group api(cloud)[API]
  service db(database)[Database] in api
  service srv(server)[Server] in api
  service disk(disk)[Storage] in api
  db:L -- R:srv
  srv:T -- B:disk
```

---

## Related

- [Getting started](guides/getting-started) — install to first diagram
- [Worked examples](examples/) — bigger diagrams, with notes on why they are built that way
- [Styling](guides/styling) — colour that carries meaning
- [Why diagrams go blurry](why-diagrams-blur)
