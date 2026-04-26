# Writing Guide

## Topics

Current topic identifiers:

```text
homeassistant
elgato-stream-deck-plugin
```

Use these exact values in filenames, folders, and frontmatter.

## Source Draft Minimum Format

```yaml
---
title: ""
date: "YYYY-MM-DD"
topic: ""
source_project: ""
source_ai: ""
status: "draft"
tags: []
summary: ""
---
```

Required body sections:

- 요약
- 작업 배경
- 진행한 작업
- 결정 사항
- 문제점과 해결
- 남은 일
- 링크/백링크 후보
- 참고 자료

## Publish-Ready Post Metadata

```yaml
---
layout: post
title: ""
description: ""
date: "YYYY-MM-DD"
updated: "YYYY-MM-DD"
topic: ""
tags: []
series: ""
series_order:
source_project: ""
source_ai: ""
source_draft: ""
status: "review"
related_posts: []
backlinks: []
---
```

## Link Notes

External AI drafts should use candidate notation instead of final Markdown links:

```markdown
[[관련: homeassistant-dashboard-overview]]
```

Codex converts candidates into final links during publish preparation.
