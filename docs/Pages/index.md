---
hide:
  - toc
---

<div align="center">
	<h1>The Reloaded MkDocs Theme</h1>
	<img src="../Images/Reloaded-Icon.png" width="150" align="center" />
	<br/> <br/>
    A Theme for MkDocs Material.
    <br/>
    That resembles the look of <i>Reloaded</i>.
</div>

## About

This it the NexusMods theme for Material-MkDocs, inspired by the look of [Reloaded-II](https://reloaded-project.github.io/Reloaded-II/).

The overall wiki theme should look fairly close to the actual launcher appearance.

## Setup From Scratch

- Add [this repository](https://github.com/Reloaded-Project/Reloaded.MkDocsMaterial.Themes.R2) as submodule to `docs/Reloaded`.
- Save the following configuration as `mkdocs.yml` in your repository root.

```yaml
site_name: Reloaded MkDocs Theme
site_url: https://github.com/Reloaded-Project/Reloaded.MkDocsMaterial.Themes.R2

repo_name: Reloaded-Project/Reloaded.MkDocsMaterial.Themes.R2
repo_url: https://github.com/Reloaded-Project/Reloaded.MkDocsMaterial.Themes.R2

extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/Reloaded-Project
    - icon: fontawesome/brands/twitter
      link: https://twitter.com/thesewer56?lang=en-GB

extra_css:
  - Reloaded/docs/Stylesheets/extra.css

markdown_extensions:
  - admonition
  - tables
  - pymdownx.details
  - pymdownx.highlight
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
  - pymdownx.tasklist
  - def_list
  - meta
  - md_in_html
  - attr_list
  - footnotes
  - pymdownx.tabbed:
      alternate_style: true
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg

theme:
  name: material
  palette:
    scheme: reloaded-slate
  features:
    - navigation.instant

plugins:
  - search
  - exclude-unused-files:
      file_types_to_check: [ "psd", "7z", "kra" ]
      file_types_override_mode: append
      enabled: true
  - minify:
      minify_html: true
      minify_js: true
      minify_css: true
      htmlmin_opts:
      remove_comments: true
      cache_safe: true
  - exclude:
      # Exclude the Theme's own files.
      glob:
        - Reloaded/docs/Pages/index.md
        - Reloaded/docs/Pages/testing-zone.md
        - Reloaded/.gitignore
        - Reloaded/Readme.md
        - Reloaded/LICENSE
        - Reloaded/*.yml
        - Reloaded/*.py
        - Reloaded/venv/*

nav:
  - Home: index.md
```

- Add a GitHub Actions workload in `.github/workflows/DeployMkDocs.yml`.

```yaml
name: MkDocs Build and Deploy

on:
  workflow_dispatch:
  push:
    branches: [ main ]
    paths:
      - "mkdocs.yml"
      - "docs/**"
  pull_request:
    branches: [ main ]
    paths:
      - "mkdocs.yml"
      - "docs/**"

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pages: write
      id-token: write
    steps:
      - name: Deploy MkDocs
        uses: Reloaded-Project/devops-mkdocs@v1
        with:
          requirements: ./docs/requirements.txt
          publish-to-pages: ${{ github.event_name == 'push' }}
          checkout-current-repo: true
```

- Copy `docs/requirements.txt` from this repository to your repository.

- Push to GitHub, this should produce a GitHub Pages site.

Your page should then be live.

!!! tip

    Refer to [Contributing](contributing.md#website-live-preview) for instructions on how to locally edit and modify the wiki.

!!! note

    For Reloaded3 theme use `reloaded3-slate` instead of `reloaded-slate`.

!!! note

    If you run into issues deploying, make sure `Settings->Pages` has `Build and Deployment` source set as `GitHub Actions`.

## Extra

!!! info

    Most documentation pages will also include additional plugins; some which are used in the pages here.
    Here is a sample complete mkdocs.yml you can copy to your project for reference.

## Technical Questions

If you have questions/bug reports/etc. feel free to [Open an Issue](https://github.com/Reloaded-Project/Reloaded.MkDocsMaterial.Themes.R2/issues/new).

Happy Documenting ❤️