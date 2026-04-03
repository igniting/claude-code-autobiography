# Claude Code Autobiography

This is a static website built with Hugo that presents the autobiography of Claude Code in a good format.

## Building the Site

1. Install Hugo (extended version recommended for better theme support):
   ```bash
   # On Ubuntu/Debian
   sudo apt update && sudo apt install hugo

   # Or using snap
   snap install hugo --channel=extended

   # Or using Docker
   docker run --rm -v $(pwd):/src klakegg/hugo:ext
   ```

2. Build the site:
   ```bash
   hugo
   ```

   This will generate the static files in the `public/` directory.

3. Serve locally for preview:
   ```bash
   hugo server
   ```

   Visit `http://localhost:1313` to view the site.

## Publishing to GitHub Pages

1. Enable GitHub Pages in your repository settings:
   - Go to Settings > Pages
   - Set Source to "GitHub Actions" or "Deploy from a branch"
   - If using a branch, create a `gh-pages` branch with the built site

2. For automated deployment with GitHub Actions, create `.github/workflows/deploy.yml`:

   ```yaml
   name: Deploy Hugo site to Pages

   on:
     push:
       branches: [ main ]
     pull_request:
       branches: [ main ]

   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
           with:
             submodules: true
             fetch-depth: 0

         - name: Setup Hugo
           uses: peaceiris/actions-hugo@v2
           with:
             hugo-version: 'latest'
             extended: true

         - name: Build
           run: hugo --minify

         - name: Deploy
           uses: peaceiris/actions-gh-pages@v3
           if: github.ref == 'refs/heads/main'
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: ./public
   ```

3. Push the changes and the site will be available at `https://igniting.github.io/claude-code-autobiography/`

## Content

The autobiography is formatted as a single-page book using Hugo's book theme structure. The content is sourced from `story.md` and presented in a clean, readable format suitable for long-form reading.