# Codex Working Guide

This repository is the GitHub blog management hub for the mochi-cookie blog.

## First Read Order

At the start of a new session, read these files first:

1. `AGENTS.md`
2. `PROJECT_CONTEXT.md`
3. Active proposal files in `proposals/active/`

## Core Rule

When the user asks to implement a feature or workflow change, do not implement it immediately.

Create or update a proposal first. Implement only after the user explicitly approves implementation.

## Proposal Rules

- Proposal filenames start with `YYYY-MM-DD-HHmm`.
- One implementation flow uses one proposal file.
- User revision requests update the same proposal.
- Post-implementation issues or follow-up requests are added to the same proposal under `구현 후 추가 사항`.
- When the user declares the flow complete, add `[완료]` to the beginning of the proposal filename.
- Put user-answer-needed items at the very bottom of the proposal.
- Keep proposals focused on design decisions and operating direction. Handle command-by-command execution during implementation.

## Blog Workflow

- External AI drafts go into `inbox/ai-drafts/`.
- Preserve source drafts; create publish-ready posts separately.
- Publish-ready content lives under `content/`.
- The Jekyll preview site lives under `site/`.
- Only posts reviewed by the user in localhost preview should be pushed for public publishing.

## GitHub

- Use SSH remotes for GitHub.
- Do not use the default `github.com` SSH host for this blog.
- Do not reuse the existing GitHub account already configured on this machine.
- Wait until the dedicated blog GitHub account has the `id_ed25519_mochi_cookie_blog.pub` key registered.
- Use only the `github-mochi` SSH host alias for this blog repository.
- Expected repository name: `mochi-cookie-blog`.
- Dedicated blog GitHub account: `mochicookieybyj-sudo`.
- Expected GitHub Pages style: project site.
- Expected public URL: `https://mochicookieybyj-sudo.github.io/mochi-cookie-blog/`.
