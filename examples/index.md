---
title: Real-world examples
---

# Real-world examples

Diagrams for jobs that actually come up in Confluence. Every one is copy-paste ready and
**verified rendering in Crisp Diagrams** — all 19 Mermaid diagram types below were tested against
the shipping build.

Jump to: [Architecture](#system-architecture) · [Sequence](#api-request-flow) ·
[Decision](#incident-triage) · [Data model](#data-model) · [State](#content-lifecycle) ·
[Planning](#release-plan) · [C4](#c4-system-context) · [Everything else](#other-diagram-types)

---

## System architecture

The most common diagram in any engineering space: what talks to what.

```
flowchart LR
  U[Client] -->|HTTPS| G[API Gateway]
  G -->|verify token| A[Auth Service]
  G -->|place order| O[Orders Service]
  O -->|publish| Q[[Event Queue]]
  O -->|write| D[(Orders DB)]
  Q -->|consume| W[Fulfilment Worker]
  W -->|store label| S[(Object Store)]
  A -.->|read user| D
```

**Why it works:** every arrow is labelled, so the diagram says *what* flows, not just *that*
something flows. Unlabelled arrows are the most common way an architecture diagram becomes
useless six months later.

`[[double brackets]]` marks a queue, `[(rounded)]` marks a datastore, and `-.->` is a dashed line
for a secondary or read-only path.

---

## API request flow

For documenting an endpoint, an auth handshake, or a retry policy.

```
sequenceDiagram
  autonumber
  participant C as Client
  participant A as API
  participant D as Database
  C->>A: POST /orders
  A->>D: BEGIN TRANSACTION
  A->>D: INSERT order
  D-->>A: order_id
  A->>D: COMMIT
  A-->>C: 201 Created
  Note over C,A: Retries are idempotent<br/>via Idempotency-Key
```

**Why it works:** `autonumber` gives every step a reference number, so people can discuss "step 4"
in a comment. `Note over` captures the constraint that would otherwise live only in someone's head.

---

## Incident triage

A runbook people can actually follow at 3am.

```
flowchart TD
  A[Alert fires] --> B{Customer impact?}
  B -->|No| C[Log and review next standup]
  B -->|Yes| D{Known cause?}
  D -->|Yes| E[Apply documented fix]
  D -->|No| F[Page on-call lead]
  F --> G[Open incident channel]
  G --> H[Post status page update]
  E --> I{Resolved?}
  H --> I
  I -->|Yes| J[Write postmortem]
  I -->|No| F
  classDef urgent fill:#FFECEB,stroke:#C9372C,stroke-width:2px
  class F,G,H urgent
```

**Why it works:** decision diamonds map to the actual questions someone asks, and the loop from
"not resolved" back to escalation is explicit. The red `classDef` marks the steps with a clock on
them — the one place colour earns its keep.

---

## Data model

For a schema discussion that doesn't require opening the database.

```
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE_ITEM : contains
  PRODUCT ||--o{ LINE_ITEM : "appears in"
  CUSTOMER {
    uuid id PK
    string email UK
    string name
    timestamp created_at
  }
  ORDER {
    uuid id PK
    uuid customer_id FK
    string status
    decimal total
  }
  LINE_ITEM {
    uuid id PK
    int quantity
    decimal unit_price
  }
```

**Why it works:** `PK`, `FK` and `UK` markers mean reviewers can spot a missing index or a bad key
without asking. Cardinality (`||--o{`) is the part people argue about, so state it.

---

## Content lifecycle

Approval flows, document states, order status — anything with defined transitions.

```
stateDiagram-v2
  [*] --> Draft
  Draft --> InReview: submit
  InReview --> Draft: request changes
  InReview --> Approved: approve
  Approved --> Published: publish
  Published --> Archived: archive
  Archived --> [*]
  note right of InReview
    Two approvals required
    for regulated content
  end note
```

**Why it works:** transitions are labelled with the *action* that causes them, which is what a
reader needs. The note carries the business rule that a plain state diagram would lose.

---

## Release plan

```
gantt
  title Q4 delivery
  dateFormat YYYY-MM-DD
  axisFormat %b %d
  section Build
    Rendering engine   :done,    a1, 2026-09-01, 20d
    Editor + preview   :active,  a2, after a1, 14d
    Export pipeline    :         a3, after a2, 10d
  section Launch
    Beta with 5 teams  :         b1, after a3, 14d
    Marketplace review :crit,    b2, after b1, 7d
```

**Why it works:** `done` / `active` / `crit` give visual status without a legend. `after a1` means
the chart stays correct when a date slips — you change one date, not five.

---

## C4 system context

For architecture that has to survive a security review.

```
C4Context
  title System Context — Payments Platform
  Person(customer, "Customer", "Places orders")
  Person(agent, "Support Agent", "Handles disputes")
  System(shop, "Storefront", "Web and mobile ordering")
  System(pay, "Payments Service", "Authorises and captures")
  System_Ext(psp, "Payment Provider", "Third-party PSP")
  System_Ext(ledger, "Accounting System", "General ledger")
  Rel(customer, shop, "Browses and orders")
  Rel(shop, pay, "Requests payment")
  Rel(pay, psp, "Authorise / capture", "HTTPS")
  Rel(pay, ledger, "Posts journal entries", "Nightly")
  Rel(agent, pay, "Issues refunds")
```

**Why it works:** C4 distinguishes people, internal systems and external systems, which is exactly
the distinction a security reviewer cares about. `System_Ext` marks your trust boundary.

---

## Other diagram types

All of these render. Each is a minimal, working starting point.

### Class diagram
```
classDiagram
  class Order {
    +String id
    +Money total
    +submit() void
  }
  class Customer {
    +String email
  }
  Customer "1" --> "*" Order : places
```

### User journey
```
journey
  title Checkout experience
  section Browse
    View item: 5: Customer
    Add to cart: 4: Customer
  section Pay
    Enter card: 2: Customer
    Confirm: 4: Customer
```

### Pie chart
```
pie title Traffic sources
  "Organic" : 45
  "Direct" : 30
  "Referral" : 25
```

### Quadrant chart
```
quadrantChart
  title Effort vs impact
  x-axis Low Effort --> High Effort
  y-axis Low Impact --> High Impact
  quadrant-1 Do now
  quadrant-2 Plan
  quadrant-3 Drop
  quadrant-4 Quick wins
  Bundle formats: [0.6, 0.9]
  Dark mode polish: [0.2, 0.4]
```

### Git graph
```
gitGraph
  commit
  branch develop
  commit
  checkout main
  merge develop
  commit tag: "v1.0"
```

### Mindmap
```
mindmap
  root((Product))
    Discovery
      Interviews
      Surveys
    Delivery
      Build
      Ship
```

### Timeline
```
timeline
  title Roadmap
  2026 Q3 : Launch free
  2026 Q4 : Add formats
  2027 Q1 : Introduce pricing
```

### XY chart
```
xychart-beta
  title "Installs"
  x-axis [Jan, Feb, Mar, Apr]
  y-axis "Count" 0 --> 500
  line [50, 120, 260, 430]
```

### Requirement diagram
```
requirementDiagram
  requirement render_req {
    id: 1
    text: Diagrams must render as SVG
    risk: high
    verifymethod: test
  }
  element viewer {
    type: component
  }
  viewer - satisfies -> render_req
```

### Block, Sankey, Kanban, Architecture
```
block-beta
  columns 3
  A["Web"] B["API"] C["DB"]
  A --> B
  B --> C
```

```
sankey-beta

Visits,Signup,120
Visits,Bounce,380
Signup,Paid,25
```

```
kanban
  Todo
    [Write docs]
  Doing
    [Test diagrams]
  Done
    [Ship v1]
```

```
architecture-beta
  group api(cloud)[API]
  service db(database)[Database] in api
  service server(server)[Server] in api
  db:L -- R:server
```

---

## A note on colour

Crisp renders unstyled diagrams in a restrained neutral-blue palette that matches Confluence. That
is deliberate: **colour should mean something.** Reach for `classDef` when you want to mark the
critical path, a deprecated component, or a trust boundary — not to decorate every node.

```
classDef critical fill:#FFECEB,stroke:#C9372C,stroke-width:2px
classDef done     fill:#DDF3E4,stroke:#1F845A,stroke-width:2px
class NodeA,NodeB critical
class NodeC done
```

More on this in [Styling diagrams](../guides/styling).
