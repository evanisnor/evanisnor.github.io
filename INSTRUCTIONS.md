**Overview**
- **Purpose**: This document explains how to maintain the site dependencies and how to add new posts to this Jekyll-based site.
- **Do not edit**: The `/_site/` folder is generated. Do not edit files inside `_site` — change source files and rebuild.

**Maintaining Dependencies**
- **Ruby gems**: This project uses Bundler with a `Gemfile`/`Gemfile.lock`. Install or update gems using:

  - `gem install bundler` (if Bundler is missing or you need a newer Bundler)
  - `bundle install` (install gems from `Gemfile.lock` / `Gemfile`)

- **Update all gems**: To update all gems to the latest compatible versions, run:

  - `bundle update`

  Or to update a single gem (e.g., `jekyll`):

  - `bundle update jekyll`

- **Verify after updates**: After updating, always build and serve the site locally to check for regressions:

  - `bundle exec jekyll build`
  - `bundle exec jekyll serve`

  Open `http://localhost:4000` and check pages, styles, and JS behavior.

- **Commit changes**: If updating gems modifies `Gemfile` and `Gemfile.lock`, commit both files together:

  - `git add Gemfile Gemfile.lock`
  - `git commit -m "chore: update gems"`

- **Bundler versioning**: If the project expects a specific Bundler version, prefer using the same version locally. Example to install a specific bundler version:

  - `gem install bundler -v '2.4.13'`

- **JavaScript / vendor assets**: This repository stores JS assets under `assets/js/` and `assets/vendor/`. There is no npm/yarn config here.

  - To update a vendor JS file, replace the file in `assets/js/` or `assets/js/vendor/` and verify the site works.
  - If you introduce a JS package manager (npm/yarn), add a `package.json` and document how to build assets.

**Building & Testing Locally**
- **Install prerequisites**: Ensure Ruby and Bundler are installed (macOS: use a Ruby version manager or system Ruby). Then run:

  - `bundle install`

- **Build**: `bundle exec jekyll build` — output is placed in `_site/`.
- **Serve (development)**: `bundle exec jekyll serve` — serves at `http://localhost:4000` by default.
- **Drafts**: If you use drafts, preview with `bundle exec jekyll serve --drafts` after adding files to `_drafts/`.

**Adding New Posts**
- **Location & filename**: Create a new Markdown file in `_posts/` named with the date prefix: `YYYY-MM-DD-title.md`.

  - Example: `_posts/2025-11-23-my-new-post.md`

- **Minimal front matter**: At minimum include `layout`, `title`, and `date`. Example front matter:

  ```yaml
  ---
  layout: post
  title: "My new post"
  date: 2025-11-23 09:00:00 -0500
  categories: [blog]
  tags: [example, jekyll]
  excerpt: "A short summary of the post."
  ---
  ```

  - Make sure the `date` in the front matter corresponds to the filename date (Jekyll uses the filename date to set the post permalink unless overridden).

- **Content**: Write content below the front matter in Markdown. Use relative paths to images (see next bullet).
- **Images and assets**: Add images to `assets/images/` or a subfolder and reference them with a site-root-relative path, e.g. `/assets/images/my-image.jpg`.
- **Preview**: After adding the file, run `bundle exec jekyll serve` and go to `http://localhost:4000` to confirm the post appears and renders correctly.

**Publishing / Deployment**
- **GitHub Pages**: This site appears to be hosted via GitHub Pages. After verifying locally, push your branch and open a PR or push to `main` depending on your workflow.
- **Commit checklist**: When publishing a post or dependency change, typically commit:

  - The new post (e.g., `_posts/2025-11-23-my-new-post.md`)
  - Any updated assets you intentionally changed
  - `Gemfile` and `Gemfile.lock` if dependencies changed

- **Don't commit**: The generated `_site/` contents should not be committed (unless you have a specific reason).

**Notes & Tips**
- **Backups**: Before large dependency updates, create a branch so you can revert easily if a gem update breaks the build.
- **Troubleshooting**: If the site fails to build after updating gems:

  - Check the error message and stack trace from `bundle exec jekyll build`.
  - Try `bundle exec jekyll build --verbose` for more info.
  - Consider locking a gem to a previous version in `Gemfile` if an incompatibility is encountered.

- **Style & templates**: Site templates and includes live in the repository root and `_includes/`. Update those to change layout or header fragments.
