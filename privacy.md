# Privacy Policy — Crisp Diagrams for Confluence

**Last updated:** 23 August 2026

## The short version

Crisp Diagrams runs entirely inside Atlassian. It makes **no external network requests**, stores
**no data outside your Atlassian site**, and requires **no third-party account**.

We do not receive your diagrams, your page content, or your personal information — not because we
promise not to look, but because the app never sends them anywhere.

## What data the app handles

| Data | Where it is stored | Who can access it |
|---|---|---|
| Your Mermaid diagram source | The macro configuration on your Confluence page | Anyone with permission to view that page |
| Your display preferences (theme) | The same macro configuration | Same |

That is the complete list.

## What the app does not do

- It does not transmit data to the developer or to any third party.
- It does not use analytics, tracking pixels, cookies, or fingerprinting.
- It does not load code, fonts, or images from external servers or CDNs.
- It does not require an account, login, or registration of any kind.
- It does not store data on developer-controlled infrastructure. There is none.

## Runs on Atlassian

Crisp Diagrams carries Atlassian's [**Runs on Atlassian**](https://www.atlassian.com/blog/developer/runs-on-atlassian-gives-partners-a-new-way-to-showcase-strict-data-protections)
badge. Atlassian grants this only to apps that:

- use exclusively Atlassian-hosted compute and storage,
- support the same data residency as the host product, and
- do not egress data.

Eligibility is verified automatically by Atlassian, not self-declared.

## Verify it yourself

You do not have to take our word for any of this:

1. Open a Confluence page containing a Crisp diagram.
2. Open your browser's developer tools and select the **Network** tab.
3. Reload the page and watch the requests.

No request leaves your Atlassian domain. You can also disconnect from the internet after the page
has loaded and the diagram will still render and zoom, because all processing happens in your
browser.

## Data processing and residency

All processing happens client-side, in your browser, on your device. Because no data reaches
developer infrastructure, there is no cross-border transfer, no sub-processor, and no retention
period to disclose.

Your diagram source lives in Confluence and is governed by
[Atlassian's own privacy policy](https://www.atlassian.com/legal/privacy-policy) and your
organisation's Confluence data-residency settings.

## Your rights

Because the developer holds no personal data about you, there is nothing for us to access,
correct, export, or delete. To remove diagram content, edit or delete the macro or the page in
Confluence, or uninstall the app.

## Children's privacy

The app is a business tool, is not directed at children, and collects no data from anyone.

## Changes to this policy

If the app ever changes in a way that affects data handling, this policy will be updated before
that change ships, and the "last updated" date above will change. Any future feature that would
require sending data anywhere will be **opt-in and clearly disclosed**, never silent.

## Contact

Questions about this policy: open an issue on the support page listed on the app's Marketplace
listing.

## Third-party code

Crisp Diagrams bundles its rendering libraries into the app rather than loading
them from a CDN. That is what makes zero data egress possible, and it means their
licences ship with the app. The complete list of bundled packages, versions and
licence texts is published at
[Third-party notices](third-party-notices).

## Security

The app's security posture, and how to report a vulnerability, are documented at
[Security](security).
