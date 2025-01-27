---
title: Wiki Structure
parent: Wiki Guide
nav_order: 2
last_modified_date: 2025-01-20 12:00
---

# The Wiki Structure and How It Works

This guide explains the structure of the Wiki repository and provides best practices for organising and maintaining it effectively.

---

## Current Wiki Structure

Below is an example of how the current Wiki repository is organised:

```plaintext
❯ tree -L 3
.
├── Gemfile
├── Gemfile.lock
├── LICENSE
├── MediahubLogo-Dark.webp
├── README.md
├── _config.yml
├── docs
│   ├── analyst
│   │   ├── cognito.md
│   │   ├── geo-holdout.md
│   │   ├── index.md
│   │   ├── powerbi.md
│   │   ├── radar-files.md
│   │   └── taxonomy-help.md
│   ├── getting-started.md
│   ├── governance.md
│   ├── mac-setup.md
│   └── wiki-guide
│       ├── callouts.md
│       ├── contributing-guide.md
│       ├── index.md
│       ├── markdown.md
│       └── wiki-structure.md
└── index.md
```

---

## How to Contribute to the Wiki

Contributions to the Wiki involve editing or adding files within the `docs` folder. Follow these best practices to maintain consistency and usability.

{: .warning}
> Avoid modifying `Gemfile` or `_config.yml` unless necessary and tested locally. Changes to these files can affect the overall structure and functionality.

### Organising Content

1. **Use Logical Folders**  
   Group related files into subfolders (e.g., `adverity`, `engineering`, `pulse`). Each folder should include an `index.md` file as the main entry point. This file is displayed when users click on the folder in the navigation sidebar.

2. **Clear File Names**  
   Use descriptive and concise names for files (e.g., `data-mapping.md`, `pull-requests.md`) to make the content easily identifiable.

3. **Markdown Guidelines**  
   - Follow the [Markdown Guide](docs/wiki-guide/markdown.md).  
   - Use [callouts](docs/wiki-guide/callouts.md) to emphasise important points.

---

## Navigation Structure

### Setting `nav_order`

To determine the order of pages in the navigation sidebar, use the `nav_order` attribute in the front matter of each file. Pages with lower values appear first.

Example:  
```yaml
---
title: Getting Started
nav_order: 2
last_modified_date: 2023-11-20 12:00
---
```

{: .tip}
> Assign unique `nav_order` values for each file. If two files share the same value, their order may change unpredictably upon rendering.

---

### Creating Multi-Level Navigation

To create a hierarchy in the navigation sidebar, use the `parent` attribute in the front matter.

#### Parent Page Example:
```yaml
---
title: Wiki Guide
layout: default
nav_order: 10
last_modified_date: 2025-01-20 12:00
---
```

#### Child Page Example:
```yaml
---
title: Markdown Guide
parent: Wiki Guide
nav_order: 3
last_modified_date: 2025-01-20 12:00
---
```

{: .important}
> Ensure the `parent` value matches the `title` of the corresponding `index.md` file in the folder.

---

## Best Practices for Structuring the Wiki

1. **Maintain Consistency**  
   - Use consistent naming and file structures across all sections.  
   - Ensure all folders include an `index.md` file summarising the content.

2. **Organise Logically**  
   - Regularly review the structure to ensure it remains clear and scalable as content grows.

3. **Update Metadata**  
   - Include `last_modified_date` in the front matter to track updates.

4. **Avoid Redundancy**  
   - Consolidate related content instead of duplicating information across files.

---

## Reference Materials

For detailed documentation and additional features, refer to the [Just the Docs guide](https://just-the-docs.github.io/just-the-docs/).
