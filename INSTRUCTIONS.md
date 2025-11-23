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

  **Overview**
  - **Purpose**: Quick guide for maintaining dependencies and adding posts for this Jekyll site.
  - **Note**: Do not edit the generated `_site/` directory — change source files and rebuild.

  **Prerequisites**
  - **Ruby & rbenv**: Use the project Ruby (`rbenv` recommended). Confirm with `ruby -v` and `rbenv global`.
  - **Bundler 2+**: This repo requires Bundler 2+. Install a specific Bundler if needed:

    - `gem install bundler -v '2.4.13'`

  - **Homebrew OpenSSL (macOS)**: If you experience SSL errors, install `openssl@3` and point Ruby to it when building Ruby.

  **Dependencies**
  - **Install**: `bundle install`
  - **Update gems**: `bundle update` or `bundle update <gemname>`
  - **Update Bundler in the lockfile**: If `Gemfile.lock` requires a newer Bundler, run:

    - `bundle _2.4.13_ update --bundler` (use the version you installed)

  - **Commit**: Commit both `Gemfile` and `Gemfile.lock` together after updates:

    - `git add Gemfile Gemfile.lock`
    - `git commit -m "chore: update gems"`

  **SSL / Remote theme issues (common)**
  - If Jekyll fails with `certificate verify failed (unable to get certificate CRL)`, two practical fixes:

    1) Avoid remote fetches by installing the theme gem locally (preferred):

       - Add `gem "minimal-mistakes-jekyll", "~> 4.24"` to `Gemfile` and replace `remote_theme:` with `theme:` in `_config.yml`.
       - Run `bundle install` and build normally.

    2) Temporary SSL workaround (diagnostic):

       - Export macOS system certs: `security find-certificate -a -p /Library/Keychains/System.keychain /System/Library/Keychains/SystemRootCertificates.keychain > /tmp/cacert.pem`
       - `export SSL_CERT_FILE=/tmp/cacert.pem` then run `bundle exec jekyll doctor`.

    3) Robust fix: rebuild Ruby linked to Homebrew OpenSSL:

       - `RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl@3)" rbenv install <version> --force`

  **Build & Preview**
  - Build: `bundle exec jekyll build` (output in `_site/`)
  - Serve: `bundle exec jekyll serve` (preview at `http://localhost:4000`)
  - Drafts: `bundle exec jekyll serve --drafts`

  **Adding a Post**
  - Create a file in `_posts/` named `YYYY-MM-DD-title.md` (e.g. `_posts/2025-11-23-my-new-post.md`).
  - Minimal front matter:

    ```yaml
    ---
    layout: post
    title: "My new post"
    date: 2025-11-23 09:00:00 -0500
    ---
    ```

  - Add content below front matter in Markdown. Reference images with site-root paths like `/assets/images/...`.
  - Preview locally with `bundle exec jekyll serve` and verify the post displays.

  **Publishing**
  - After verification, commit new posts and any updated `Gemfile`/`Gemfile.lock`, then push and open a PR or merge to `main` per your workflow.
  - Do not commit `_site/`.

  **Quick Troubleshooting**
  - `bundle exec jekyll doctor` for diagnostics.
  - Use `bundle exec jekyll build --verbose` to see build errors.
  - If SSL or gem conflicts persist, paste the error output and I'll help debug.

  ---
  Concise maintenance instructions for this repository.
