---
title: Repositrory Best Practices
parent: Engineering Standards
nav_oder: 3
last_modified_date: 2025-01-20 12:00
---

# Repository Design

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## Organise the Repository

A consistent and clear repository structure helps team members understand the project’s purpose and locate files efficiently. Below is an example structure for organising a Python project.

### Folder Structure

```plaintext
~/project_name
.
├── .github
│   └── workflows
│       └── pre-commit.yml
├── .gitignore
├── CHANGELOG.md
├── README.md
├── pyproject.toml
├── requirements.txt
├── data
│   └── __init__.py
├── docs
├── tests
│   ├── __init__.py
│   ├── test_main.py
│   └── test_utils.py
└── src (source folder)
    ├── __init__.py
    ├── configs
    │   ├── __init__.py
    │   └── config.py
    ├── constants
    │   ├── __init__.py
    │   └── constants.py
    ├── main.py
    └── utils.py
```

#### Key Folders

- **`src/`**: Main application source code, often named `src`, `app`, or aligned with the project name (e.g., `project_name`).
- **`tests/`**: Houses all tests. Its structure mirrors the source folder for easier maintenance.
- **`docs/`**: Contains all project documentation. Each subdirectory can have its own README.md for added clarity.

### Root Directory Files

- **`README.md`**: Provides an overview, setup instructions, and usage examples.
- **`CHANGELOG.md`**: Tracks changes like new features, fixes, and breaking updates.
- **`requirements.txt`**: Lists Python dependencies; update with `pip freeze > requirements.txt`.
- **`pyproject.toml`**: Centralised configuration for tools such as `mypy`, `flake8`, and `interrogate`.
- **`.gitignore`**: Specifies files and folders Git should ignore.

---

## Automated Testing & CI/CD

Automated testing and CI/CD pipelines ensure code quality and streamline deployment.

### General Guidelines

- **Testing**: Place unit and integration tests in the `tests/` directory. Ensure the test structure mirrors the source code.
- **CI/CD**: Use GitHub Actions to automate testing, linting, and deployment.

### Example CI/CD Workflow

Create `.github/workflows/pre-commit.yml` for automated testing and checks:

```yaml
name: Pre-commit

on:
  push

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up Python 3.11
      uses: actions/setup-python@v3
      with:
        python-version: "3.11"

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install flake8 pytest interrogate mypy
    
    - name: Check docstring coverage with interrogate
      run: |
        interrogate -v .

    - name: Type checking with mypy
      run: |
        mypy .

    - name: Run tests with pytest
      run: |
        pytest -vvv
```

### Tool Configuration in .toml files

Example `pyproject.toml` file:

```toml
[tool.interrogate]
style = "sphinx"
verbose = 2
fail-under = 95
ignore-init-module = true
ignore-magic = true
exclude = ["tests"]

[tool.mypy]
python_version = "3.11"
exclude = ["docs"]

[tool.flake8]
max-line-length = 88
ignore = E203, W503
```

---

Here’s an improved and more cohesive version of the **Documentation Guidelines** section:  

---

## Documentation Guidelines

Clear and well-structured documentation ensures that users and contributors can quickly understand, set up, and use the project. Below are the recommended practices:  

### README.md

The `README.md` serves as the entry point for anyone exploring the project. Keep it concise yet comprehensive, and include the following:  
- **Overview**: Provide a brief description of the project’s purpose and its key features.  
- **Installation**: List step-by-step instructions for installing dependencies and setting up the project.  
- **Usage**: Include examples of key commands or workflows to help users get started quickly.  

### Detailed Documentation in docs folder

For more complex projects, maintain detailed documentation within a dedicated `docs/` folder. Structure this documentation into sections such as:  
- **API Documentation**: Describe available endpoints, methods, and expected inputs/outputs.  
- **Deployment Guidelines**: Provide instructions for deploying the project to different environments (e.g., staging, production).  
- **Architecture Overview**: Offer insights into the project's design, such as module relationships or critical workflows.  

### Additional Key Files

- **`CONTRIBUTING.md`**: Provide guidelines for contributors, including:  
  - How to set up the development environment.  
  - Coding standards and style requirements.  
  - Instructions for submitting pull requests (PRs).  
  - Any special considerations or processes, such as running tests before submitting changes.  

- **`CHANGELOG.md`**: Maintain a log of significant changes, including:  
  - New features, bug fixes, and updates for each release.  
  - Clear versioning to track changes (e.g., using Semantic Versioning: `MAJOR.MINOR.PATCH`).  
  - Automation tools like `git-changelog` or manually formatted logs to ensure accuracy.  

---

### Automating the Changelog with git-changelog

`git-changelog` is a Python library designed to generate changelogs directly from Git commit history. It helps streamline release management by automating the changelog creation process, ensuring consistency and reducing manual effort.

#### Installation

You can install `git-changelog` using pip:

```bash
pip install git-changelog
```

#### Configuration in `pyproject.toml`

To configure `git-changelog`, you can define its behavior in the `pyproject.toml` file. Below is an example:

```toml
[tool.git-changelog]
style = "angular"  # Define the commit message convention
repository = "."  # Path to the Git repository
output_file = "CHANGELOG.md"  # Output file for the changelog
unreleased = true  # Include unreleased changes in the changelog
sections = { Features = "feat", Fixes = "fix", Documentation = "docs" }
```

---

#### Customising "Sections"

The `sections` option defines how commits are categorised in the changelog. Each key is the section header (e.g., "Features"), and each value is a keyword used to identify commits that belong to that section.

- **Example of Sections**:
  ```toml
  sections = {
      Features = "feat",
      Fixes = "fix",
      Performance = "perf",
      Refactoring = "refactor",
      Documentation = "docs",
      Tests = "test",
      Build = "build",
      CI = "ci",
      Chores = "chore"
  }
  ```

- **Customising Sections**:
  - Add new categories relevant to your project, such as `Security` for vulnerability fixes or `UI Updates` for frontend changes.
  - Use multiple keywords per category if needed:
    ```toml
    sections = {
        Features = ["feat", "feature"],
        Fixes = ["fix", "bugfix"],
        Documentation = ["docs", "doc"]
    }
    ```
  - Rename headers to better suit your team’s terminology:
    ```toml
    sections = {
        "New Features" = "feat",
        "Bug Fixes" = "fix",
        "Internal Changes" = ["chore", "refactor"]
    }
    ```

---

### Versioning with CHANGELOG

- **Use Semantic Versioning**:
  - Format: `MAJOR.MINOR.PATCH`.
    - **MAJOR**: Breaking changes.
    - **MINOR**: New features, no breaking changes.
    - **PATCH**: Bug fixes, small improvements.
- Include:
  - New features.
  - Fixes and updates.
  - Deprecations or breaking changes.
- Tools:
  - Use `git-changelog` or other tools to automate changelog updates.

---

#### Best Practices for Customising Sections

1. **Align with Commit Message Standards**:
   - Use a conventional commit style, like **Conventional Commits** or **Angular Commit Guidelines**, to make it easier to categorize commits.
   - Example commit messages:
     ```
     feat: add user authentication
     fix: resolve payment gateway issue
     docs: update API usage in README.md
     ```

2. **Keep Sections Relevant**:
   - Ensure sections are meaningful for end users and contributors. Avoid overly granular categories unless they provide value.

3. **Order Sections Logically**:
   - Prioritize user-facing changes (e.g., Features, Fixes) before internal updates (e.g., Tests, CI).

4. **Use Plural Headers**:
   - Use plural forms like "Features" or "Fixes" to group multiple entries intuitively.

---

#### Additional Configuration Options

Beyond `sections`, `git-changelog` offers various customisation options to fine-tune your changelog generation:

- **Header Customisation**:
  - Modify the changelog title or date format.
    ```toml
    title = "Project Changelog"
    date_format = "%Y-%m-%d"
    ```

- **Template**:
  - Use custom Jinja2 templates to control the changelog’s format:
    ```toml
    template = "custom_template.j2"
    ```

- **Tag Matching**:
  - Define how Git tags are interpreted to group commits by version:
    ```toml
    tag_filter = "^v"  # Match tags starting with "v"
    ```

- **Commit Exclusion**:
  - Exclude specific commits or categories from the changelog:
    ```toml
    exclude_commits = ["ci", "chore"]
    ```

- **Release Highlights**:
  - Use an additional `highlights` section to summarise key changes for each release.

---

#### Sample Workflow

1. Ensure your team follows a structured commit message style.
2. Add `git-changelog` configuration to your `pyproject.toml`.
3. Run the tool to generate the changelog:
   ```bash
   git-changelog --output CHANGELOG.md
   ```
4. Review and include the changelog in your version control system.
5. Automate the changelog process in your CI/CD pipeline.


