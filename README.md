
# Mediahub Wiki README

This is a Jekyll-based website template using the [Just the Docs](https://just-the-docs.github.io/just-the-docs/) theme. It is designed to be easily deployed on [GitHub Pages](https://docs.github.com/en/pages). The site is automatically deployed from the `main` branch using a GitHub Actions workflow. Other branches will not be published live.

---

## Table of Contents
- [Mediahub Wiki README](#mediahub-wiki-readme)
  - [Table of Contents](#table-of-contents)
  - [Deploying Locally](#deploying-locally)
  - [Making Changes to the Configuration](#making-changes-to-the-configuration)
  - [Workflow](#workflow)
  - [Resources](#resources)

---

## Deploying Locally

To run this site locally, you’ll need to have Ruby and Bundler installed. Follow these steps:

1. **Install Ruby**: Ensure Ruby is installed on your system. You can check by running:
   ```bash
   ruby -v
   ```
   If Ruby is not installed, follow the [official Ruby installation guide](https://www.ruby-lang.org/en/documentation/installation/).

2. **Install Bundler**: Bundler is used to manage Ruby gems. Install it by running:
   ```bash
   gem install bundler
   ```

3. **Clone the Repository**: Clone this repository to your local machine:
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

4. **Install Dependencies**: Use Bundler to install the required gems:
   ```bash
   bundle install
   ```

5. **Build and Serve the Site**: Start the Jekyll server to preview the site locally:
   ```bash
   bundle exec jekyll build
   bundle exec jekyll serve
   ```
   The site will be available at `http://localhost:4000`.

6. **Make Changes**: Edit files in your local repository. The site will automatically rebuild, and you can preview changes in real-time.

---

## Making Changes to the Configuration

The site’s configuration is managed in the `_config.yml` file. You can customise settings such as the site title, description, and theme options. Refer to the [Just the Docs configuration documentation](https://just-the-docs.com/docs/configuration/) for detailed guidance.

---

## Workflow

The site is deployed using GitHub Pages. A GitHub Actions workflow is defined in `.github/workflows/pages.yml`. This workflow automatically builds and deploys the site whenever changes are pushed to the `main` branch.

To deploy to a different platform, you can modify the workflow or build the site locally and upload the `_site` directory to your preferred hosting service.


---

## Resources

- [Just the Docs Documentation](https://just-the-docs.github.io/just-the-docs/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [GitHub Pages / Actions Workflow](https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/)
- [Just the Docs Template Repository](https://github.com/just-the-docs/just-the-docs-template)

