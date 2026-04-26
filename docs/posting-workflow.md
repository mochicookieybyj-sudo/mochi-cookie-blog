# Posting Workflow

## Overview

```text
external AI draft
-> inbox/ai-drafts/{topic}/
-> Codex editorial pass
-> content/posts/{topic}/
-> site/_posts/{topic}/
-> local Jekyll preview
-> user review
-> commit and push
-> GitHub Pages deploy
```

## Topics

```text
homeassistant
elgato-stream-deck-plugin
```

## Draft Intake

Original drafts go here:

```text
inbox/ai-drafts/{topic}/
```

Original assets go here:

```text
inbox/assets/{topic}/
```

## Publish Preparation

Codex creates cleaned publish candidates here:

```text
content/posts/{topic}/
```

Jekyll posts go here:

```text
site/_posts/{topic}/
```

## Review

Run local preview from `site/`:

```text
bundle exec jekyll serve --baseurl=
```

Review at:

```text
http://127.0.0.1:4000/
```

Only push after the user approves the local preview.
