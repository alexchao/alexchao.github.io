# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is Alex Chao's personal blog built with Hugo and the PaperMod theme. The site is deployed automatically to GitHub Pages and uses GoatCounter for analytics.

## Common Commands

### Development
- `hugo server` - Start local development server with live reload
- `hugo server -D` - Start server including draft posts
- `hugo` - Build the site (outputs to `public/` directory)
- `hugo --gc --minify` - Build with garbage collection and minification (production build)

### Content Management
- `hugo new posts/post-name.md` - Create a new blog post
- `hugo new content/page-name.md` - Create a new page

## Architecture

### Site Structure
- **config.toml**: Main Hugo configuration with PaperMod theme settings, menu structure, and site parameters
- **content/**: All site content organized by type
  - `posts/`: Blog posts (main content area)
  - `about.md`, `archive.md`, `music.md`: Static pages accessible via main navigation
- **layouts/**: Custom layout overrides
  - `shortcodes/audio.html`: Custom shortcode for embedding audio players
  - `partials/extend_head.html`: Adds GoatCounter analytics in production
- **static/**: Static assets (CNAME file for GitHub Pages custom domain)
- **themes/PaperMod/**: Hugo PaperMod theme (git submodule)

### Content Organization
- Posts use Hugo's front matter with `title`, `date`, and `draft` fields
- Images are hosted on AWS S3 (`alexchao-blog-media.s3.amazonaws.com`)
- Posts include `<!--more-->` comment to define excerpt breaks
- Content covers software engineering, music, and personal topics

### Deployment
- Automatic deployment via GitHub Actions (`.github/workflows/hugo.yaml`)
- Builds on push to main branch using Hugo v0.127.0
- Deploys to GitHub Pages with custom domain
- Production builds include garbage collection and minification
- GoatCounter analytics enabled only in production environment

### Theme Customization
- Uses PaperMod theme with custom overrides
- Analytics integration via `extend_head.html` partial
- Custom audio shortcode for music-related posts
- Light theme as default with theme toggle disabled