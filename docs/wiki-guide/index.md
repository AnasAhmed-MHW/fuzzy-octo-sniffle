---
title: Wiki Guide
layout: default
nav_order: 10
last_modified_date: 2025-01-20 12:00
---

# The Mediahub Wiki How-To  

This document provides basic guidance on how to contribute to the D&A Wiki and effectively use Markdown for documentation.  

---

## Setup  

For those with a developer background:  

This wiki uses the `Just the Docs` theme to generate a static website with [Jekyll](https://jekyllrb.com/). Jekyll enables you to create web pages using Markdown files, which are converted into HTML during the build process.  

All new documents should be added to the `/docs` folder to ensure they are included in the site build.  

### About the Theme  

The `Just the Docs` theme enhances Jekyll’s static site generator by adding useful features and clean styling. While this theme is currently in use, other Jekyll-compatible themes can be explored and used if necessary.  

### Workflow  

The site is deployed via the `main` branch. A deployment workflow is defined in `.github/workflows/pages.yml`, which automatically deploys the site whenever changes are merged into the `main` branch.  

### Customisation  

The theme is configured using the `_config.yml` file. While most settings have already been established, you can further customize the site by referring to the [Just the Docs configuration page](https://just-the-docs.com/docs/configuration/).  

There are additional features available, such as buttons and typography, that you may wish to explore for enhancing the wiki’s functionality and design.  

---

## Contributing to the Wiki  

Here are some resources to guide you in contributing effectively:  