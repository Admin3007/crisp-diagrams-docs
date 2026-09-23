---
title: Mermaid in Confluence without a third-party account
description: How to use Mermaid diagrams in Confluence without every reader having to sign up for a separate service.
---

# Mermaid in Confluence, without a third-party account

You installed a Mermaid app. You wrote a diagram. Then a colleague opened the page and was
asked to **create an account with a company they have never heard of** before they could see
a box with an arrow in it.

That is a real pattern in this category, and it is worth understanding before you pick a
tool — because it is not something you can turn off later.

---

## Why some apps ask for a sign-up

Apps that require an account are usually doing the rendering **on their own servers**. Your
diagram text is sent out of Atlassian, drawn somewhere else, and sent back as an image.

Once that is the architecture, an account follows almost inevitably: the vendor needs to
know who is calling, meter it, and bill it. The sign-up is not a marketing choice bolted on
top; it is a consequence of where the drawing happens.

That architecture has three costs your team pays:

1. **Everyone who reads the page needs an account**, not just the person who wrote the
   diagram. On a documentation page read by fifty people, that is fifty sign-ups.
2. **Your diagram content leaves Atlassian.** For some teams that alone ends the
   conversation, whatever the vendor's policy says.
3. **The diagram depends on somebody else's uptime.** If their service is down or your
   network blocks it, your page has a hole in it.

---

## The alternative: render in the browser

If the rendering happens **in the reader's own browser**, none of that applies. There is no
server to authenticate to, nothing to meter, and no request to make.

That is how Crisp Diagrams works:

- **No account, for anyone.** Install it once and it works for everybody on the site
  immediately — authors and readers alike. There is no seat to assign, no invite, no
  separate login.
- **No third party.** The Mermaid rendering engine is bundled into the app rather than
  fetched from a CDN, so there is no external service in the path at all.
- **No data leaves Atlassian.** The app requests **no Atlassian API scopes** and makes no
  external network calls. It carries Atlassian's **Runs on Atlassian** badge, granted only
  to apps that use exclusively Atlassian-hosted compute and storage and do not egress data.

---

## Verify it yourself

Do not take the claim on trust. Two checks, neither of which needs any special access:

**Network tab.** Open your browser's developer tools, go to the Network tab, and reload a
page containing a diagram. Every request should be to your own `*.atlassian.net` domain.
There is no third-party host to find.

**Pull the plug.** Disconnect from the internet and open a cached page. The diagram still
renders, still zooms, and still exports — because all of that is running locally.

If an app passes both of those, it genuinely cannot be phoning home.

---

## Where your diagram is stored

In the macro on your own Confluence page, as plain text.

That has a few pleasant consequences that are easy to overlook:

- It is **versioned with the page**. Page history shows diagram changes like any other edit.
- It is **restored with the page** if someone reverts.
- It is **included in your site export**. Your diagrams are not stranded in a vendor's
  database.
- It is **searchable**, because it is text on your page rather than an opaque blob.

---

## Getting started

Type `/mermaid` on any Confluence page and pick **Mermaid Diagram**. Choose a starting point
from the **Examples** menu — there is one for each of the nineteen diagram types — and edit
it.

[Get started](guides/getting-started) · [Diagram templates](templates) ·
[Why diagrams go blurry](why-diagrams-blur)
