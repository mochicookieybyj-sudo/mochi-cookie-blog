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
- Dedicated blog GitHub account status: connected
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

Ruby 3.3 with MSYS2 DevKit is installed locally at `C:\Ruby33-x64`.

Run the preview locally:

```text
cd site
bundle install
bundle exec jekyll serve --baseurl=
```

Preview URL:

```text
http://127.0.0.1:4000/
```

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

- Initial GitHub blog setup is complete.
- Use local Jekyll preview before publishing feature or post changes.
- Active next topic: blog design refresh proposal in `proposals/active/`.
