---
title: How to use Mermaid diagrams in Confluence Cloud
description: Every way to get Mermaid diagrams onto a Confluence Cloud page in 2026, from pasted images to free and paid apps, and how to choose between them.
---

# How to use Mermaid diagrams in Confluence Cloud

You write Mermaid in GitHub, GitLab or your docs repo, and you want the same diagrams on Confluence pages.
At the time of writing (October 2026), Confluence Cloud doesn't render Mermaid on its own: put the
source in a code block and readers see the text, not the diagram. Here are the ways around that, with
their trade-offs.

> We make Crisp Mermaid Diagrams, one of the options below. We've tried to describe every option fairly;
> check the current Marketplace listings too, because apps change.

---

## Option 1: paste an image

Draw the diagram in the [Mermaid Live Editor](https://mermaid.live), export a PNG or SVG, and attach it to the page.

- **Good:** nothing to install, works on any Confluence.
- **Bad:** the diagram is frozen. Every change means re-exporting and re-uploading, and the source lives
  somewhere else, so nobody else can edit it. PNGs also [go blurry when readers zoom](why-diagrams-blur).

Fine for a diagram that will never change; painful for living documentation.

## Option 2: the free Atlassian Labs viewer

Atlassian Labs publishes a free *Mermaid diagrams viewer* app. You write Mermaid in a code block, then insert
the viewer macro, which renders the code block above it.

- **Good:** free, installed on thousands of sites.
- **Bad:** its author describes it as an internal side project without the support of official Atlassian
  products, it's rated about 3 out of 5 on the Marketplace, and the code block and macro are two separate
  pieces that can get separated when a page is edited.

## Option 3: a Marketplace app

Search the Atlassian Marketplace for *Mermaid* and you'll find dozens of apps. They differ in four ways that
matter more than the feature lists:

1. **Vector or image.** Some apps save a picture of your diagram; others draw it fresh as SVG each time
   the page loads. SVG stays sharp at any zoom and in PDF exports. See [why diagrams go blurry](why-diagrams-blur).
2. **Account required or not.** Some apps need everyone who edits a diagram to sign up with the app's own
   service. See [can I use Mermaid without a third-party account?](no-account-required)
3. **Where diagram content goes.** Apps marked *Runs on Atlassian* keep data on Atlassian's platform; others
   send it to the vendor's servers to render. Matters for security reviews.
4. **Price.** Most are free for sites up to 10 users, then charged per user per month through Atlassian.

## Option 4: Crisp Mermaid Diagrams (ours)

What we built it to do differently:

- Renders **true SVG**, so diagrams stay sharp at any zoom and export at full resolution.
- **Live preview** beside the source while you edit, with errors that name the line and point at the character.
- Full page width, pan, zoom and full screen, plus SVG or PNG download.
- **No account** for anyone, and no requests outside Atlassian: Mermaid is bundled into the app.
- Nineteen diagram types with ready-made [templates](templates).

What it doesn't do: it's for Confluence Cloud only (not Jira, not Data Center), and it's a young app with
far fewer installs than the established ones.

[Get started](guides/getting-started) · [Marketplace listing](https://marketplace.atlassian.com/apps/331634655)

---

## Which should you pick?

| If you... | Choose |
|---|---|
| need one diagram that will never change | a pasted SVG image |
| want free and can live with an unsupported app | the Atlassian Labs viewer |
| need diagrams that stay editable, sharp when zoomed, with no extra accounts | an SVG-rendering app that Runs on Atlassian, such as Crisp |
| already use a vendor's own Mermaid editor across tools | that vendor's Confluence app |

## Moving diagrams you already have

- **From GitHub/GitLab Markdown:** copy the text inside the ` ```mermaid ` block; it works unchanged.
- **From a PNG on the page:** if you still have the source, paste it into the macro and delete the image.
- **From PlantUML:** see [moving from PlantUML](plantuml-to-mermaid).
