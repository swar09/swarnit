+++
title = "Why I Chose Zola for My Engineering Portfolio"
description = "How migrating away from heavy node-based frameworks to a single Rust binary gave me sub-second builds and zero maintenance overhead."
date = 2026-03-01
+++

Static site generators have come a long way. For years, the default choice for modern web portfolios was Gatsby, Next.js, or Astro. While those tools are great for dynamic web applications, using a massive JavaScript toolchain for a documentation or portfolio site often brings unnecessary complexity:

* Gigabytes of `node_modules`
* Frequent dependency churn and breaking package updates
* Heavy client-side JavaScript bundles for simple textual content

### The Elegance of Zola

[Zola](https://www.getzola.org/) is a single, self-contained binary written in Rust. It does not require installing Node.js, Python, or Ruby.

```bash
# Installing and serving a site with Zola
zola init my-portfolio
zola serve
```

### Key Advantages

1. **Lightning-Fast Builds**: Compiling 100+ pages of Markdown takes less than 50 milliseconds.
2. **Tera Templating**: Powerful layout inheritance inspired by Jinja2 and Django.
3. **Built-in Syntax Highlighting**: Powered by `syntect`, so no client-side `Prism.js` is needed.
4. **$0 Hosting**: Generates pure static HTML and CSS that deploys effortlessly to Cloudflare Pages or GitHub Pages.
