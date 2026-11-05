+++
title = "Why I chose Zola for this site"
description = "Notes on setting up a static site without a JavaScript build chain."
date = 2026-03-01
+++

I wanted a site to put up project notes and writeups without dealing with a heavy build setup.

A lot of modern web tools pull in hundreds of megabytes of dependencies in `node_modules` just to render plain Markdown files to HTML. Over time, dependencies drift, build scripts fail on newer Node versions, and keeping the site working becomes its own chore.

Zola is a single executable written in Rust. It takes a folder of Markdown files and Tera templates, and writes out static HTML and CSS.

A few things that made it practical for me:

* One binary to install, with no external package manager needed.
* Builds take less than a second.
* Syntax highlighting runs during the build, so pages do not need client-side highlighting scripts.
* The output is plain HTML, which deploys to GitHub Pages or Cloudflare Pages with zero hosting cost.
