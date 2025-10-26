# Migration Guide

This guide helps you migrate your existing Reloaded MkDocs Theme setup to the latest version.

## Version 1.0.0 Migration

If you are upgrading from a version prior to 1.0.0, follow these steps:

### 1. Directory Structure Changes

**Before:**
```
project-root/
├── Images/
├── Pages/
├── Stylesheets/
├── docs/
└── mkdocs.yml
```

**After:**
```
project-root/
├── docs/
│   ├── Images/
│   ├── Pages/
│   │   └── private/
│   └── Stylesheets/
└── mkdocs.yml
```

**mkdocs.yml Changes:**

```diff
 extra_css:
-  - Reloaded/Stylesheets/extra.css
+  - Reloaded/docs/Stylesheets/extra.css

 nav:
-  - Home: Reloaded/Pages/index.md
-  - License: Reloaded/Pages/license.md
-  - How to Document: Reloaded/Pages/contributing.md
-  - Testing Zone: Reloaded/Pages/testing-zone.md
+  - Home: Reloaded/docs/Pages/index.md
+  - License: Reloaded/docs/Pages/license.md
+  - How to Document: Reloaded/docs/Pages/contributing.md
+  - Testing Zone: Reloaded/docs/Pages/testing-zone.md
```

**Actions Required:**

- Move `Images/`, `Pages/`, and `Stylesheets/` directories into `docs/`
- Update all file references in your markdown files

This was done in case of Windows users who don't have symlink access.

### 2. Updated Exclude Patterns

Theme-specific files have been moved to a `private` subdirectory. Update your exclude patterns to exclude the private folder:

**Actions Required:**

If using `mkdocs-exclude-unused-files`, update glob patterns:

```yaml
- exclude:
    glob:
      - Reloaded/docs/Pages/private/*
      - Reloaded/docs/*.txt
      - Reloaded/.gitignore
      - Reloaded/Readme.md
      - Reloaded/LICENSE
      - Reloaded/*.yml
      - Reloaded/*.py
      - Reloaded/venv/*
```

### 3. Image Format Migration

All PNG images in the theme have been converted to AVIF format for better compression.

**Actions Required:**

- If you reference any images from the theme template (e.g., Reloaded logo), you may need to change the file extension from `.png` to `.avif`
- Example: `../Images/Reloaded-Icon.png` → `../Images/Reloaded-Icon.avif`

### 4. Build System Enhancements

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

### 5. Setup Script Improvements

New automated setup script available.

**Actions Required:**

- Add `start_docs.py` from this repository to your root
- Update `.gitignore` to include:
  ```
  # MkDocs build output
  site/
  
  # Python virtual environments
  venv/
  ```

### 6. Version Tracking

Add version comment to your markdown files for future migrations:

```markdown
<!--- Reloaded.MkDocsMaterial.Themes.R2:1.0.0 --->
```







