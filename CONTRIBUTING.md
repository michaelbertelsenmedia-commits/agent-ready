# Contributing to Agent-Ready

Agent-Ready is public domain. Anyone can use it, copy it, modify it, fork it, or rename it. Contributions back to this repository are welcome but never required.

## What is most useful

**Better example files** in `examples/`. Especially:
- Implementations of `Article`, `Product`, `Event`, `HowTo`, `Recipe` JSON-LD with realistic content.
- A clean static HTML page that scores 100/100 on Lighthouse SEO and accessibility.
- A working `robots.txt` for a specific stack (Cloudflare, Vercel, Netlify, classic Apache, nginx) that handles common pitfalls.

**Translations** of `README.md` and `SPEC.md`. Place translated files in `translations/<lang>/` — for example `translations/de/SPEC.md`.

**Implementation reports.** A short note describing your site, when you implemented Agent-Ready, and what you observed in AI-search citations afterwards. Open an issue with the `report` label. Honest negative reports ("implemented it, saw nothing change") are as valuable as positive ones.

**Platform-map corrections.** If you have hard evidence that the table in `SPEC.md` is wrong about how a specific platform weights `llms.txt` or a particular schema type, open an issue with the `platform-map` label and link to the evidence.

## What is not in scope

- Promotional content for specific SEO or GEO services.
- Disputes over copyright on the badge image (it is public domain — copy it).
- Demands that a specific commercial product be added to the platform map. Each platform in the map has its own crawler and public documentation; the map describes signals, not vendor preferences.

## Pull-request process

1. Fork the repository.
2. Create a topic branch: `git checkout -b examples/article-json-ld`.
3. Make your change. Keep it small and focused — one idea per PR.
4. Open the pull request against `main` with a short description of what you changed and why.
5. A maintainer will merge or comment within a week. If you do not hear back, ping the PR with a polite comment.

## Issue process

For questions, ideas, or non-code contributions, open an issue. Use one of the labels:

- `question` — you want clarification on the spec.
- `improvement` — you have an idea for a better example or wording.
- `platform-map` — you have evidence about how a specific AI engine behaves.
- `report` — implementation report from your own site.

## Style

- English for the canonical files. Translations go in `translations/<lang>/`.
- Plain markdown, no exotic formatting.
- No emoji in spec files. Emojis in issue discussions are fine.
- No trademark or company-promo language in shared files.

## Code of conduct

Be honest, be specific, be brief. Disagreements are welcome when they are substantive. Personal attacks, ad hominem arguments, and bad-faith framing get the comment hidden and the participant blocked from the repository.

## License

By submitting a contribution to this repository, you agree that your contribution is also released under [CC0 1.0 Universal](LICENSE) — public domain. There is no separate contributor license agreement.
