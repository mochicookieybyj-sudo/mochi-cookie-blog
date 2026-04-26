# AI Draft Guide

이 문서는 각 프로젝트의 AI에게 전달할 포스팅 초안 작성 규칙이다.

## 역할

각 프로젝트의 AI는 해당 프로젝트에서 있었던 작업을 블로그 후보 문서로 정리한다.

AI가 할 일:

- 원본 작업 내용을 Markdown으로 정리한다.
- 파일명 규칙을 지킨다.
- 필수 frontmatter를 채운다.
- 링크와 백링크는 확정하지 않고 후보로 남긴다.
- 이미지나 첨부 파일이 있으면 함께 전달한다.

AI가 하지 않을 일:

- 공개용 최종 경로를 확정하지 않는다.
- GitHub Pages URL을 임의로 만들지 않는다.
- 존재하지 않는 내부 링크를 일반 Markdown 링크처럼 쓰지 않는다.
- 백링크를 확정된 사실처럼 쓰지 않는다.
- 토큰, 비밀번호, 개인 경로, 비공개 주소를 포함하지 않는다.

## 주제 식별자

현재 사용 가능한 주제는 다음 두 개다.

```text
homeassistant
elgato-stream-deck-plugin
```

파일명, frontmatter의 `topic`, 첨부 파일 폴더명에는 위 값을 그대로 사용한다.

## 파일명 규칙

초안 파일명은 다음 형식을 사용한다.

```text
YYYY-MM-DD-NNN-topic-short-title-draft.md
```

예:

```text
2026-04-27-001-homeassistant-dashboard-draft.md
2026-04-27-001-elgato-stream-deck-plugin-key-rendering-draft.md
```

규칙:

- `YYYY-MM-DD`: 초안을 작성한 날짜
- `NNN`: 같은 날짜/주제 내 순번, 001부터 시작
- `topic`: `homeassistant` 또는 `elgato-stream-deck-plugin`
- `short-title`: 영문 소문자 kebab-case
- 마지막은 반드시 `draft.md`

## 필수 Frontmatter

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

예:

```yaml
---
title: "Home Assistant 대시보드 카드 정리"
date: "2026-04-27"
topic: "homeassistant"
source_project: "homeassistant-dashboard"
source_ai: "Codex"
status: "draft"
tags:
  - homeassistant
  - dashboard
summary: "대시보드 카드 구조를 정리하고 다음 개선 방향을 기록했다."
---
```

## 필수 본문 섹션

아래 섹션을 순서대로 작성한다.

```markdown
## 요약

## 작업 배경

## 진행한 작업

## 결정 사항

## 문제점과 해결

## 남은 일

## 링크/백링크 후보

### 이 글이 참고하면 좋은 글

### 이 글을 나중에 참조할 수 있는 글

## 참고 자료
```

내용이 없으면 `없음`이라고 적는다.

## 링크와 백링크 후보 작성법

초안 작성 AI는 내부 링크를 확정하지 않는다.

대신 다음처럼 후보를 남긴다.

```markdown
## 링크/백링크 후보

### 이 글이 참고하면 좋은 글

- homeassistant-dashboard-overview: 대시보드 전체 구조 설명이 있으면 연결
- elgato-stream-deck-plugin-action-model: 액션 모델 비교용

### 이 글을 나중에 참조할 수 있는 글

- homeassistant-automation-refactor: 자동화 리팩터링 글에서 참조 가능
```

본문 중간에 관련 글을 표시하고 싶으면 다음 형식을 사용한다.

```markdown
[[관련: homeassistant-dashboard-overview]]
[[관련: elgato-stream-deck-plugin-action-model]]
```

최종 Markdown 링크 변환은 블로그 프로젝트의 Codex가 담당한다.

## 이미지와 첨부 파일

이미지나 첨부 파일이 있으면 초안과 함께 전달한다.

첨부 파일명은 다음 형식을 권장한다.

```text
YYYY-MM-DD-topic-short-title-asset-name.ext
```

예:

```text
2026-04-27-homeassistant-dashboard-card-layout.png
```

본문에는 임시 표기로 남긴다.

```markdown
[이미지: 2026-04-27-homeassistant-dashboard-card-layout.png]
```

최종 이미지 경로 변환은 블로그 프로젝트의 Codex가 담당한다.

## 마무리 체크리스트

- 파일명이 규칙을 따른다.
- `topic`이 정확하다.
- frontmatter가 있다.
- 필수 본문 섹션이 모두 있다.
- 링크는 후보로 남겼다.
- 민감한 정보가 없다.
- 첨부 파일이 있으면 파일명을 본문에 적었다.
