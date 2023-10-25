# Welcome to Cheatsheets

This site was made with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) based on [mkdocs.org](https://www.mkdocs.org) and hosted on [Github Pages](https://docs.github.com/en/pages)

## Set up Github Pages

The source directory can either be at the root `/` or a `docs/` directory.

1. Create a new repository and setup the local git configuration as usual.
- Edit the Markdown files as wanted.
- Create a github workflow under `.github/workflows/ci.yml` and add the following [basic configuration](#workflow-configuration).
- Now, a push on the `main` branch will execute this workflow and publish this site.
- To get the public URL, go to the `settings` tab and under **"Code and automation"** section of the sidebar click on **Pages**.
- Under **"Build and deployment"**, under **"Source"**, select **Deploy from a branch**.
- Under **"Build and deployment"**, under **Branch**, select the dropdown menu and select the `gh-pages` branch and click on **Save**.
- Optionally, use the folder dropdown menu to select a folder for your publishing source. (e.g. `/`or `docs/`)
- Now the site should be available on : `https://<github-account>.github.io/<your-repo>/` or go to the **Actions** tab, under **ci** click on the workflow (with a green check) and then click on **deploy** (with a green check) and then expand the **Run mkdocs gh-deploy --force** step to see the public URL.

## Workflow configuration

```yaml
name: ci 
on:
  push:
    branches:
      - master 
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - uses: actions/cache@v2
        with:
          key: ${{ github.ref }}
          path: .cache
      - run: pip install mkdocs-material
      - run: pip install pillow cairosvg
      - run: mkdocs gh-deploy --force
```

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

```
mkdocs.yml    # The configuration file.
docs/
    index.md  # The documentation homepage.
    ...       # Other markdown pages, images and other files.
```