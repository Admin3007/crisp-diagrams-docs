---
title: Support
description: How to get help with Crisp Mermaid Diagrams for Confluence, what the response targets are, and what is in scope.
---

# Support

## Where to ask

**[Open an issue](https://github.com/Admin3007/crisp-diagrams-docs/issues)** — bugs, questions
and feature requests all go to the same tracker. It is public, so you can see what has already
been reported and whether a fix is on the way.

Read [Troubleshooting](guides/troubleshooting) first. It has a symptom index and covers the
common cases, including diagrams that will not render and syntax errors that are hard to read.

For a security vulnerability, follow [Security](security) instead — do not put exploitable
detail in a public issue.

---

## What to expect

| | Target |
|---|---|
| First response | 2 business days |
| Diagnosis, or a question back to you | 5 business days |
| Fix for a rendering bug | Next release |
| Fix for a critical or high security issue | Per Atlassian's [security bug fix policy](https://www.atlassian.com/trust/security/bug-fix-policy) |

**Business days are Monday to Friday, IST (UTC+05:30).** The tracker accepts reports at any
hour; the clock starts on the next business day.

This is a one-person project. There is no phone line and no 24-hour desk, and saying otherwise
would be a promise that could not be kept. What is promised above is what will actually happen.

---

## What helps a report get fixed faster

1. **The diagram source.** Paste the Mermaid text, not a screenshot of it. The text is what
   reproduces the bug.
2. **What you expected and what you got.** "The label is cut off on the right" beats "it looks
   wrong".
3. **Browser and theme.** Chrome or Firefox, light or dark, and whether your Confluence page
   was in dark mode.
4. **Whether it renders elsewhere.** Paste the same source into the
   [Mermaid live editor](https://mermaid.live). If it fails there too, it is a Mermaid syntax
   issue rather than an app bug, and [Troubleshooting](guides/troubleshooting) will get you
   there faster than an issue will.

---

## What is in scope

**In scope:** the macro failing to render, a diagram that renders differently from what the
Mermaid syntax specifies, export producing a broken SVG or PNG, zoom or pan misbehaving, theme
or dark-mode problems, the editor losing your source, and anything that looks like a security
problem.

**Out of scope:** teaching Mermaid syntax from scratch — the
[templates](templates) and [worked examples](examples/) exist for that — and diagram types
Mermaid itself does not support. If Mermaid cannot draw it, neither can this app.

---

## Before you file

The app requests no Atlassian API scopes and makes no external requests, so a large class of
problems can be ruled out immediately: it cannot be a permissions issue, and it cannot be an
outage of ours, because there is no server of ours to be down. If a diagram stopped rendering,
the cause is in the source, the browser, or the app's own code.

See [Security](security) for how to verify those claims yourself in about a minute.

---

## Related

- [Troubleshooting](guides/troubleshooting) — symptom index
- [Getting started](guides/getting-started)
- [Diagram templates](templates)
- [Security](security)
- [Privacy](privacy)
