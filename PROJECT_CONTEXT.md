# Project Context

## Role

This project manages a GitHub-based blog. It receives Markdown drafts from other project-specific AI sessions, turns them into publish-ready posts, validates them locally, and then publishes through GitHub.

## Current Decisions

- Session instruction file: `AGENTS.md`
- Project context file: `PROJECT_CONTEXT.md`
- Proposal location: `proposals/active/`
- Completed proposal location: `proposals/completed/`
- Blog framework: Jekyll
- GitHub repository name: `mochi-cookie-blog`
- Dedicated blog GitHub account: `mochicookieybyj-sudo`
- GitHub connection method: SSH
- GitHub SSH host alias: `github-mochi`
- Important GitHub caution: the machine already has another GitHub account configured for a different purpose. Do not use that account for this blog.
- Dedicated blog GitHub account status: not connected yet
- GitHub Pages URL style: project site
- Expected public URL: `https://mochicookieybyj-sudo.github.io/mochi-cookie-blog/`
- Final post review: user manually reviews localhost preview
- GitHub Pages deployment: GitHub Actions workflow builds `site/` and deploys to Pages

## Current Structure

```text
proposals/
  active/
  completed/
inbox/
  ai-drafts/
  assets/
content/
  posts/
  series/
  pages/
  assets/
links/
site/
scripts/
docs/
```

## Local Preview

The preview site is a Jekyll site in `site/`.

Ruby and Bundler are required to run the preview locally:

```text
cd site
bundle install
bundle exec jekyll serve
```

At the time this file was created, Ruby was not available in the local shell.

## Draft Intake Standard

External AI draft files should include:

- Title
- Date
- Source project
- Source AI
- Summary
- Work log
- Result
- Issues or limitations
- Reference links

## Next Known Work

- Register `~/.ssh/id_ed25519_mochi_cookie_blog.pub` in the dedicated GitHub account.
- SSH authentication through `github-mochi` is working.
- GitHub repository is connected and `main` has been pushed.
- Enable GitHub Pages with GitHub Actions if the repository setting is not automatically enabled.
- Install Ruby/Bundler or choose an alternate Jekyll preview runtime for local previews.
- Validate the first localhost preview.
