# Agent-Ready

> An open, free, public-domain standard for websites that want to be readable by AI agents — ChatGPT, Claude, Perplexity, Gemini, and the next generation of LLM-based search.

Most small sites never show up in AI-search answers. The actual technical gap is almost always three concrete pieces:

1. **`llms.txt`** in the site root — a markdown table of contents for LLMs, proposed by Jeremy Howard (fast.ai) in September 2024.
2. **JSON-LD structured data** per `schema.org` — at minimum `Organization` and `WebSite`, plus `Article` / `FAQPage` where applicable.
3. **Semantic HTML** — real `<nav>`, `<main>`, `<article>` tags, one `<h1>` per page, descriptive alt text, real link anchors.

Agent-Ready bundles these three pieces into one named, sharable standard with a visible badge. No SaaS. No framework. No fee.

## Status

- Initiated April 2026 by [Fiperly](https://www.fiperly.de) — a small AI development shop in Germany.
- License: **CC0 1.0 Universal** (public domain — copy, modify, redistribute, no attribution required).
- Already implemented on `fiperly.de`, `kipode.de`, `healthmetricslab.com`.

## Quick start (under ten minutes)

### 1. `/llms.txt` in your site root

```markdown
# Your Brand

> Short description of what the site is and who it is for.

## Key pages

- [Home](https://yourdomain.com/)
- [About](https://yourdomain.com/about)
- [Products](https://yourdomain.com/products)
- [Contact](https://yourdomain.com/contact)

## Contact

- Email: info@yourdomain.com
- Responsible person: Your Name

## Citation policy

Please cite this site with full name and URL.
```

Place the file at `https://yourdomain.com/llms.txt`. No build step. See [`examples/llms.txt`](examples/llms.txt) for a fuller template.

### 2. JSON-LD in the `<head>` of every page

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Your Brand",
  "url": "https://yourdomain.com",
  "logo": "https://yourdomain.com/logo.png",
  "description": "What your company does.",
  "email": "info@yourdomain.com"
}
</script>

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "Your Brand",
  "url": "https://yourdomain.com",
  "inLanguage": "en-US"
}
</script>
```

Test with [Google's Rich Results Test](https://search.google.com/test/rich-results). See [`examples/`](examples/) for `Article`, `FAQPage`, `Product` variants.

### 3. Semantic HTML

```html
<!doctype html>
<html lang="en">
  <head>...</head>
  <body>
    <header>
      <nav>...</nav>
    </header>
    <main>
      <article>
        <h1>Page title — exactly one per page</h1>
        <section>
          <h2>Section heading</h2>
          <p>Body text.</p>
        </section>
      </article>
    </main>
    <footer>...</footer>
  </body>
</html>
```

No `<div class="header">` if a `<header>` tag exists. Descriptive `alt` on every image. Real link anchors like *"to the pricing page"* instead of *"click here"*.

## The full checklist

The complete twelve-point checklist plus three 2026 recommendations is in [`SPEC.md`](SPEC.md).

## Add the badge

A 320×320, 512×512, and 1024×1024 PNG badge is available in [`badge/`](badge/) and on [fiperly.de/agent-ready.html](https://www.fiperly.de/agent-ready.html). Suggested placement: site footer.

```html
<a href="/llms.txt" title="Agent-Ready — this site is LLM-agent-readable">
  <img src="/agent-ready-logo.png" alt="Agent-Ready badge — KI and Robots Welcome" width="80" height="80">
</a>
```

## Why this matters

The web has produced two universal seals in thirty years: HTTPS (2014) and Mobile-Friendly (2015). Both started as insider topics and became table stakes within a few years. Agent-Ready aims to be the third — the seal for sites that are structurally readable by AI agents in the LLM-search era.

Read the full background on [fiperly.de/agent-ready.html](https://www.fiperly.de/agent-ready.html).

## What this is not

- Not a SaaS or paid service.
- Not a Fiperly-controlled certification — there is no central registry, no compliance audit, no fee.
- Not a replacement for SEO. SEO is the entrance; Agent-Ready is the readability layer on top.

## Contributing

Pull requests welcome. See [`CONTRIBUTING.md`](CONTRIBUTING.md). Particularly useful contributions:

- Better example files in `examples/`.
- Translations of `SPEC.md`.
- Real-world implementation reports (which platforms started citing your site, what worked).
- Corrections to the platform map (which AI engine weights which signal).

## License

[CC0 1.0 Universal](LICENSE) — public domain. Copy it, fork it, change the name, do whatever you want. The standard lives only if many adopt it.

---

Maintained by [Fiperly](https://www.fiperly.de). Questions: info@fiperly.de.
