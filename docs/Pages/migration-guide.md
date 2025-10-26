# Migration Guide

This guide helps you migrate your existing Reloaded MkDocs Theme setup to the latest version.

## Version 1.0.0 Migration

!!! info "If you are upgrading from a version prior to 1.0.0, follow these steps"

The theme now uses a vendoring approach instead of submodules. You now copy the necessary files directly instead of managing submodules. 

**Setup:**

- Copy the contents of the `copy-me` folder from this repository to your project root
- Skip .gitignore and mkdocs.yml if already present, and do updates below instead

The `copy-me` folder already contains the correct configuration with updated paths.

**Actions Required:**

- Update your `mkdocs.yml` with the changes shown above

### 1. Referencing Theme Documentation

If you need to reference pages from this theme's documentation (such as contributing guidelines or examples), please use the direct URLs instead of local file references.

**mkdocs.yml Changes:**

```diff
 nav:
-  - How to Document: Reloaded/Pages/contributing.md
-  - Testing Zone: Reloaded/Pages/testing-zone.md
+  - How to Document: https://reloaded-project.github.io/Reloaded.MkDocsMaterial.Themes.R2/Pages/contributing.html
+  - Testing Zone: https://reloaded-project.github.io/Reloaded.MkDocsMaterial.Themes.R2/Pages/testing-zone.html
```

Previously this was done via submodule, but turned out unnecessary.

### 2. Updated Exclude Patterns

With the vendoring approach, exclude patterns are no longer needed for the Reloaded folder since the files are now part of your project.

**mkdocs.yml Changes:**

```diff
 plugins:
   - exclude:
       glob:
-        - Reloaded/docs/Pages/private/*
-        - Reloaded/docs/*.txt
-        - Reloaded/.gitignore
-        - Reloaded/Readme.md
-        - Reloaded/LICENSE
-        - Reloaded/*.yml
-        - Reloaded/*.py
-        - Reloaded/venv/*
```

### 3. Image References

Since the files are now vendored, you may need to move them out to your own `docs` folder.

**Actions Required:**

- Move any images from the vendored theme files to your `docs/Images/` folder
- Update image references in your markdown files to use the new paths

**Example Changes:**

```diff
- ![Reloaded Icon](Reloaded/Images/Reloaded-Icon.avif)
+ ![Reloaded Icon](Images/Reloaded-Icon.avif)
```

### 4. Image Format Migration

All PNG images in the theme have been converted to AVIF format for better compression.

**Actions Required:**

- If you reference any images from the theme template (e.g., Reloaded logo), you may need to change the file extension from `.png` to `.avif`
- Example: `../Images/Reloaded-Icon.png` → `../Images/Reloaded-Icon.avif`

### 5. Build System Enhancements

Added minification plugin for optimized builds.

**Actions Required:**

- Add to `docs/requirements.txt`:
  ```
  mkdocs-minify-plugin
  ```

- Add to `mkdocs.yml` plugins section:
```yaml
plugins:
  - offline
  - search
  - minify:
      minify_html: true
      minify_js: true
      minify_css: true
      htmlmin_opts:
        remove_comments: true
      cache_safe: true
```

### 6. Setup Script Improvements

New automated setup script available.

**Actions Required:**

- Add `start_docs.py` from the `copy-me` folder to your root
- Update `.gitignore` to include:
  ```
  # MkDocs build output
  site/
  
  # Python virtual environments
  venv/
  ```

### 7. Version Tracking

Version information is now stored in `version.txt` files in the `vendor` folder for
future migration.