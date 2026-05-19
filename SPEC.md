# Agent-Ready Specification

**Version:** 1.0 — initiated April 2026, last updated May 2026.
**License:** CC0 1.0 Universal — public domain.
**Maintainer:** [Fiperly](https://www.fiperly.de) (initiator, not gatekeeper).

A website is Agent-Ready when it satisfies the twelve mandatory points below. The three recommendations are 2026 best practice but not required for the badge.

---

## Twelve mandatory points

A site is Agent-Ready when all twelve are satisfied.

### Discoverability

1. **`/llms.txt`** is in the site root, under 500 lines, in markdown, and describes the site's purpose, primary pages, contact, and citation policy. Follows the [llms.txt proposal](https://llmstxt.org/) by Jeremy Howard (fast.ai), September 2024.

2. **`/robots.txt`** explicitly allows the major AI crawlers. As of May 2026 these include, at minimum: `ClaudeBot`, `Claude-User`, `Claude-SearchBot`, `claude-code` (Anthropic four-bot system), `GPTBot`, `ChatGPT-User`, `OAI-SearchBot` (OpenAI), `PerplexityBot`, `Perplexity-User`, `Google-Extended`, `Google-Agent`, `Applebot`, `Applebot-Extended`, `MistralAI-User`, `DuckAssistBot`, `Meta-ExternalAgent`, `Meta-WebIndexer`, `Amazonbot`, `CCBot`, `Bytespider`. See [`examples/robots.txt`](examples/robots.txt).

3. **`/sitemap.xml`** exists and lists every public URL with a `lastmod` date.

### Structured data

4. **JSON-LD** with `Organization` and `WebSite` types is present in the `<head>` of every page. See [`examples/jsonld-organization.html`](examples/jsonld-organization.html).

5. **Articles and guides** additionally carry `Article` or `TechArticle` JSON-LD with `author`, `datePublished`, and `dateModified`.

6. **FAQ sections** are marked up with `FAQPage` JSON-LD. See [`examples/jsonld-faq.html`](examples/jsonld-faq.html).

### Semantic HTML

7. **Heading hierarchy** is clean — exactly one `<h1>` per page, no level skipping (no `<h2>` followed directly by `<h4>`).

8. **Semantic tags** are used in place of generic `<div>` containers: `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<header>`, `<footer>`.

9. **Images** carry descriptive `alt` attributes. No empty alt on content images, no filename-as-alt, no keyword stuffing.

10. **Link anchors** describe their destination ("to the pricing page") rather than positional fillers ("click here", "more").

### Render quality

11. **Static HTML** is the primary delivery: the page's substantive content is in the initial HTML response, not exclusively JavaScript-rendered. Single-page applications must server-side render or pre-render the content that LLM agents need to read.

12. **Canonical URL, meta description, and Open Graph data** are individually set per page (no template defaults across the whole site).

---

## Three 2026 recommendations (not required for the badge)

### A. `/llms-full.txt` — full-text variant

The next layer beyond `llms.txt`. Same markdown shape, but instead of navigational links, the consolidated full text of the site's key pages in a single file. LLM agents fetch the full brand context in one request rather than parsing dozens of HTML pages. Particularly valuable for brand landing pages, documentation, and marketing hubs of manageable size. See [llmstxt.org](https://llmstxt.org/) for the latest format guidance.

### B. Anthropic's four-bot system

As of May 2026, Anthropic operates four separate crawlers with distinct user-agent strings and distinct purposes:

- `ClaudeBot` — model training corpus.
- `Claude-User` — fetches initiated by user prompts in the Claude product.
- `Claude-SearchBot` — Claude's web search index.
- `claude-code` — the Claude Code CLI's web access.

All four should appear as separate `User-agent:` blocks in `/robots.txt` so they can be allowed or denied independently.

### C. Search-bots vs. training-bots — a strategic choice

A 2026 question every site owner answers in their `robots.txt`:

- **Allow training bots** (`ClaudeBot`, `GPTBot`, `CCBot`, `Google-Extended`) if you want your content to influence the next generation of models.
- **Allow retrieval bots** (`Claude-SearchBot`, `OAI-SearchBot`, `PerplexityBot`, `ChatGPT-User`, `Claude-User`) if you want to appear in live AI answers.
- **Block training, allow retrieval** if you have paid content you do not want absorbed into training corpora but still want cited live.

Both strategies are legitimate. Make the choice deliberately and document it as a comment in `/robots.txt`.

---

## Platform map (May 2026)

A summary of what each major AI-answer platform actually weights. The honest version of "what works for which engine."

| Platform | Strongest signal | Crawler(s) in robots.txt | `llms.txt` relevant? |
|---|---|---|---|
| **Anthropic Claude** | Clear structure, clean sources, technical depth, primary data. | `ClaudeBot`, `Claude-User`, `Claude-SearchBot`, `claude-code` | Yes — Anthropic recommends it. |
| **OpenAI ChatGPT** | Fact density, comparison pages, Bing index in the background. | `GPTBot`, `OAI-SearchBot`, `ChatGPT-User` | Weaker but read. |
| **Perplexity** | Freshness (60–90 days), Q&A structure, external mentions (Reddit, Wikipedia). | `PerplexityBot`, `Perplexity-User` | Weak — other signals dominate. |
| **Google AI Overviews** | E-E-A-T, classic top-10 SEO, schema markup, atomic answers. | `Google-Extended`, `Google-Agent` | Officially ignored. |
| **Meta AI** | Open Graph tags, Meta crawler allowed, consistency with Facebook/Instagram presence. | `Meta-ExternalAgent`, `Meta-WebIndexer` | Unclear. |
| **xAI Grok** | Presence on X (Twitter): posts, discussions, real-time mentions. | None significant — Grok has no strong public web crawler. | Not relevant. |
| **Mistral** | Structured data, clear hierarchy, multilingual. | `MistralAI-User` | Read. |
| **Apple Intelligence** | Classic SEO, clean meta tags, clear hierarchy. | `Applebot`, `Applebot-Extended` | Unclear. |

The single most consequential measure from this table: explicitly allow every relevant AI crawler in `robots.txt`. Many sites accidentally block them via default Cloudflare or hosting-provider rules and disappear from AI answers entirely.

---

## How to test your implementation

1. **Google Rich Results Test** — paste any page URL: <https://search.google.com/test/rich-results>. Confirms the JSON-LD parses.
2. **`view-source:`** in any browser — quick visual check of semantic tags and JSON-LD presence.
3. **Live citation test** — ask ChatGPT, Claude, or Perplexity a question that your site uniquely answers. If they cite you, the implementation works for that engine. Repeat over weeks — citation behavior is non-deterministic and lags indexing.
4. **`curl https://yourdomain.com/llms.txt`** — confirm the file is reachable and serves as `text/plain` or `text/markdown`.
5. **`curl -A "ClaudeBot" https://yourdomain.com/`** — confirm the page renders correctly for a specific bot user-agent (sometimes hosts return blank or error pages to bots they don't recognize).

---

## Reference: the RAG path

Why all of this matters. An LLM-based answer engine fetches your page through roughly this sequence (Retrieval-Augmented Generation, RAG):

1. **Discovery** — engine finds the page via search index, `llms.txt`, prior citation, or direct user link.
2. **Fetch** — page is retrieved, ideally as static HTML. JS-only sites are often invisible to the fetch step.
3. **Parse** — engine extracts headings, paragraphs, lists, tables, structured data. The clearer the HTML, the more reliable the parse.
4. **Chunk and embed** — text is split into semantic units and embedded into a vector space for relevance scoring against the user's question.
5. **Cite** — relevant chunks land in the generated answer, usually with the source URL.

Agent-Ready targets steps 2 through 5. A clean implementation is fetched reliably, parsed correctly, chunked precisely, and cited frequently.

---

## Changelog

- **April 2026** — version 1.0 published by Fiperly.
- **May 2026** — added recommendations A, B, C; expanded platform map with Anthropic four-bot system and Meta-WebIndexer.
