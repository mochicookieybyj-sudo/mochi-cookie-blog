# GitHub Guide

## Repository

Expected repository name:

```text
mochi-cookie-blog
```

Expected SSH remote:

```text
git@github-mochi:mochicookieybyj-sudo/mochi-cookie-blog.git
```

Expected GitHub Pages URL:

```text
https://mochicookieybyj-sudo.github.io/mochi-cookie-blog/
```

## Authentication

Use GitHub SSH authentication for normal Git operations.

Important:

- This machine already has another GitHub account configured.
- Do not use the default `github.com` SSH host for this blog.
- Do not create remotes like `git@github.com:<account>/mochi-cookie-blog.git`.
- Use the dedicated blog account only after its SSH key is registered.

This project uses a dedicated SSH host alias:

```text
github-mochi
```

The matching private key is:

```text
~/.ssh/id_ed25519_mochi_cookie_blog
```

Repository remotes for this project must use:

```text
git@github-mochi:mochicookieybyj-sudo/mochi-cookie-blog.git
```

## Publishing Rule

Only publish posts after the user reviews the localhost preview.

## GitHub Pages

The site is stored in `site/`, so Pages is deployed through GitHub Actions.

Workflow:

```text
.github/workflows/pages.yml
```

Expected Pages source:

```text
GitHub Actions
```
