---
title: Security
description: Security posture and vulnerability disclosure policy for Crisp Diagrams for Confluence.
---

# Security

## Reporting a vulnerability

Open a report at
[github.com/Admin3007/crisp-diagrams-docs/issues](https://github.com/Admin3007/crisp-diagrams-docs/issues).

If the issue would put users at risk once public, mark it clearly at the top and keep the
detail minimal — a private channel will be arranged before you send anything further.

**What to expect:**

| | Target |
|---|---|
| Acknowledgement | 2 business days |
| Initial assessment and severity | 5 business days |
| Fix for a critical or high issue | Per Atlassian's [security bug fix policy](https://www.atlassian.com/trust/security/bug-fix-policy) |
| Public disclosure | After a fix ships, credited unless you prefer otherwise |

Reports made in good faith will not be pursued. There is no bounty — this is a one-person
project — but every report will be answered.

---

## Security posture

The honest summary is that the app's attack surface is unusually small, and that is by
construction rather than by discipline.

### It requests no permissions

The Forge manifest declares `scopes: []`. The app has **no access to any Atlassian API** —
it cannot read your pages, your spaces, your user directory or anything else. There is no
`asUser()` or `asApp()` call anywhere in it, because there is nothing for it to call.

### It makes no external requests

The manifest declares no `remotes` and no `external` permissions, which Forge enforces
rather than merely records. The Mermaid rendering engine is bundled into the app rather
than fetched from a CDN.

It carries Atlassian's **Runs on Atlassian** badge, granted only to apps that use
exclusively Atlassian-hosted compute and storage and do not egress data.

You can confirm both claims yourself: open your browser's Network tab and reload a page
containing a diagram — every request goes to your own domain — or disconnect from the
internet and watch the diagram still render, zoom and export.

### It collects no credentials

No passwords, no API tokens, no personal access tokens, no OAuth secrets. There is no
account, so there is nothing to authenticate to and nothing to store.

### Where your data lives

Diagram source is stored as plain text in the macro on your own Confluence page. It is
versioned, restored and exported with that page. There is no external database.

---

## Untrusted input

Diagram source is written by anyone who can edit a page and rendered for everyone who can
read it. That is a privilege boundary, and it is treated as one.

- Mermaid runs with `securityLevel: 'strict'`, which sanitises labels through DOMPurify
- HTML labels are disabled globally, so a tag in a label becomes inert text rather than
  markup
- Any surviving `foreignObject` is converted to a plain SVG `<text>` element
- Error messages are HTML-escaped before display

Every release is tested against a hostile-input suite covering script tags, event-handler
attributes, `javascript:` URLs, injected `foreignObject`, remote image references,
entity-encoded payloads, a 100,000-character label, deeply nested subgraphs, null bytes,
right-to-left override characters, and markup inside an error message.

The remote-image case matters most: if a page editor could smuggle a tracking pixel into a
label, this app would become a per-viewer beacon and the zero-egress claim would be false.
It cannot — the tag is reduced to text and no element fetches anything.

---

## Dependencies

The app bundles its rendering libraries so that nothing is fetched at runtime. That means
their licences and their vulnerabilities are ours to carry.

- Every bundled package is listed with its licence at
  [Third-party notices](third-party-notices) — 154 packages
- Dependencies are audited on every release. **Current status: 0 known vulnerabilities**
- Mermaid and its tree are kept current; a security advisory against any bundled package
  is treated as a release blocker

---

## Reporting something that is not a vulnerability

For bugs, questions and feature requests, the same
[issue tracker](https://github.com/Admin3007/crisp-diagrams-docs/issues) is the right
place. See [Troubleshooting](guides/troubleshooting) first — it covers the common cases.
