# 포스팅 워크플로우 제안서

## 목적

여러 프로젝트/AI가 작성한 Markdown 문서를 이 블로그 프로젝트에서 안정적으로 수집, 정리, 링크 연결, 로컬 검수, 공개 배포할 수 있는 워크플로우를 정한다.

이번 제안의 핵심은 다음이다.

- 외부 프로젝트에서 작성된 md 파일을 어떻게 주고받을지 정한다.
- 포스팅용 md 파일명을 통일한다.
- 주제별 폴더 구조를 정한다.
- 여러 글 사이의 링크, 백링크, 시리즈 흐름을 관리한다.
- 공개 전 로컬 미리보기 검수 흐름과 연결한다.

## 기본 전제

- 이 블로그 프로젝트가 최종 편집/게시 허브 역할을 한다.
- 다른 프로젝트의 AI는 해당 프로젝트에서 있었던 일을 md 파일로 정리한다.
- 원본 md 파일은 보존하고, 공개용 md 파일은 별도로 만든다.
- 공개 전에는 반드시 로컬 Jekyll 미리보기에서 사용자가 직접 확인한다.
- 검수 통과 후에만 GitHub에 push한다.

## 주제 폴더

초기 주제는 두 개로 시작한다.

```text
homeassistant
elgato-stream-deck-plugin
```

추천 폴더 구조:

```text
inbox/
  ai-drafts/
    homeassistant/
    elgato-stream-deck-plugin/

content/
  posts/
    homeassistant/
    elgato-stream-deck-plugin/

content/
  assets/
    homeassistant/
    elgato-stream-deck-plugin/

site/
  _posts/
    homeassistant/
    elgato-stream-deck-plugin/

links/
  topics/
    homeassistant.md
    elgato-stream-deck-plugin.md
```

## md 파일 주고받는 방법

### 1차 방식: inbox 원본 수집

다른 프로젝트의 AI가 작성한 md 파일은 이 프로젝트의 `inbox/ai-drafts/{topic}/` 아래에 넣는다.

예:

```text
inbox/ai-drafts/homeassistant/2026-04-27-001-ha-dashboard-draft.md
inbox/ai-drafts/elgato-stream-deck-plugin/2026-04-27-001-plugin-architecture-draft.md
```

이 파일은 원본으로 취급한다.

원칙:

- 원본 draft는 가능한 한 수정하지 않는다.
- 공개용 문서는 `content/posts/{topic}/` 아래에 새로 만든다.
- 원본에서 빠진 메타데이터나 링크는 공개용 문서에서 보강한다.

### 예외 방식: 사용자가 직접 붙여넣기

사용자가 채팅으로 md 내용을 직접 전달하면, Codex가 해당 내용을 `inbox/ai-drafts/{topic}/`에 원본 파일로 저장한다.

이때 원본 파일명은 Codex가 규칙에 맞춰 생성한다.

## 파일명 양식

### 원본 draft 파일명

```text
YYYY-MM-DD-NNN-topic-short-title-draft.md
```

예:

```text
2026-04-27-001-homeassistant-dashboard-draft.md
2026-04-27-001-elgato-plugin-key-rendering-draft.md
```

규칙:

- `YYYY-MM-DD`: 작성 또는 수집 날짜
- `NNN`: 같은 날짜/주제 내 순번, 001부터 시작
- `topic`: 주제 식별자
- `short-title`: 영문 소문자 kebab-case 요약
- `draft`: 원본 초안 표시

### 공개용 post 파일명

```text
YYYY-MM-DD-NNN-topic-short-title.md
```

예:

```text
2026-04-27-001-homeassistant-dashboard.md
2026-04-27-001-elgato-stream-deck-plugin-key-rendering.md
```

### Jekyll 게시 파일명

Jekyll `_posts` 규칙을 따른다.

```text
YYYY-MM-DD-topic-short-title.md
```

예:

```text
2026-04-27-homeassistant-dashboard.md
2026-04-27-elgato-stream-deck-plugin-key-rendering.md
```

같은 날짜에 같은 short title이 겹칠 경우 뒤에 순번을 붙인다.

```text
2026-04-27-homeassistant-dashboard-002.md
```

## 주제 식별자

초기 주제 식별자는 다음으로 고정한다.

```text
homeassistant
elgato-stream-deck-plugin
```

파일명, 폴더명, frontmatter의 `topic`은 모두 긴 정식명을 사용한다.

이유:

- 주제가 늘어났을 때 약어 충돌을 줄인다.
- 외부 AI가 파일을 만들 때 판단할 여지를 줄인다.
- 링크와 백링크 경로를 예측하기 쉬워진다.

## 포스트 frontmatter 표준

공개용 문서에는 다음 frontmatter를 사용한다.

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

필드 의미:

- `topic`: 큰 주제 폴더와 동일한 값
- `tags`: 세부 키워드
- `series`: 시리즈 이름
- `series_order`: 시리즈 내 순서
- `source_project`: 원본 프로젝트명
- `source_ai`: 원본 작성 AI
- `source_draft`: 원본 draft 파일 경로
- `status`: `draft`, `review`, `ready`, `published`
- `related_posts`: 이 글에서 연결할 관련 포스트
- `backlinks`: 이 글을 참조하는 포스트

## 링크와 백링크 관리 규칙

### 기본 원칙

- 링크는 포스트 본문에 자연스럽게 넣는다.
- 백링크는 frontmatter와 `links/topics/*.md`에서 관리한다.
- 자동화 전까지는 수동 관리로 시작한다.
- 외부 AI는 확정 링크를 임의로 만들지 않고, 링크 후보를 별도 섹션에 정리한다.
- 최종 링크와 백링크 반영은 이 블로그 프로젝트의 Codex가 담당한다.

### topic index

주제별 링크 인덱스를 둔다.

```text
links/topics/homeassistant.md
links/topics/elgato-stream-deck-plugin.md
```

각 파일에는 다음 내용을 둔다.

```markdown
# Home Assistant

## Posts

- 2026-04-27: [글 제목](../../site/_posts/homeassistant/...)

## Series

- 시리즈명

## Backlink Notes

- A 글은 B 글에서 참조됨
```

### 내부 링크 작성 방식

게시가 확정된 글을 본문에서 링크할 때는 사이트 기준 절대 경로를 사용한다.

예:

```markdown
[Home Assistant 대시보드 정리]({{ "/2026/04/27/homeassistant-dashboard/" | relative_url }})
```

단, 외부 AI가 초안을 작성할 때는 Jekyll Liquid 링크를 직접 넣지 않는다.

외부 AI 초안에서는 다음 형식을 사용한다.

```markdown
[[관련: homeassistant-dashboard]]
[[관련: elgato-stream-deck-plugin-key-rendering]]
```

Codex가 공개용 포스트로 옮길 때 실제 링크로 변환한다.

### related_posts 작성 방식

frontmatter에는 포스트 경로 또는 slug를 넣는다.

추천:

```yaml
related_posts:
  - "homeassistant/homeassistant-dashboard"
```

Jekyll 렌더링 단계에서는 처음에는 자동 링크 렌더링까지 하지 않고, 본문 링크와 인덱스 파일로 관리한다.

포스트 수가 늘어나면 `related_posts`를 읽어 관련 글 목록을 자동 출력하는 layout 기능을 추가한다.

### 백링크 작성 방식

외부 AI 초안에서는 백링크를 직접 확정하지 않는다.

대신 문서 하단에 다음 섹션을 둔다.

```markdown
## 링크/백링크 후보

### 이 글이 참고하면 좋은 글

- 후보 slug 또는 설명

### 이 글을 나중에 참조할 수 있는 글

- 후보 slug 또는 설명
```

Codex는 공개용 문서로 정리할 때 다음을 수행한다.

1. 실제 존재하는 포스트와 후보를 대조한다.
2. 본문에 자연스러운 내부 링크를 추가한다.
3. 해당 주제의 `links/topics/{topic}.md`를 업데이트한다.
4. 필요한 경우 참조 대상 포스트의 `backlinks`를 갱신한다.

## 시리즈 관리

시리즈는 `content/series/{topic}/` 아래에 관리한다.

예:

```text
content/series/homeassistant/dashboard-build.md
content/series/elgato-stream-deck-plugin/plugin-development.md
```

시리즈 파일에는 다음 내용을 둔다.

```yaml
---
title: ""
topic: ""
description: ""
posts: []
---
```

초기에는 시리즈 없이 단일 포스트로 시작해도 된다.

## 포스팅 처리 흐름

```text
외부 AI가 md 작성
-> inbox/ai-drafts/{topic}/에 원본 저장
-> Codex가 공개용 content/posts/{topic}/ 문서 작성
-> frontmatter 보강
-> 관련 링크/백링크 후보 정리
-> site/_posts/{topic}/에 Jekyll 게시 파일 생성 또는 동기화
-> 로컬 Jekyll 미리보기 실행
-> 사용자가 localhost에서 확인
-> 수정 사항 반영
-> 승인 후 commit/push
-> GitHub Actions 배포 확인
```

## 외부 AI 문서 작성 가이드

각 프로젝트의 AI가 포스팅 후보 문서를 작성할 때 참고할 공통 규칙을 별도 문서로 제공한다.

예상 문서:

```text
docs/ai-draft-guide.md
```

이 문서에 포함할 내용:

- 이 블로그의 목적
- 주제 식별자 목록
- 파일명 양식
- 필수 frontmatter
- 필수 본문 섹션
- 링크/백링크 후보 작성법
- 이미지/첨부 파일 전달법
- 하면 안 되는 것

### 외부 AI용 파일명 규칙

외부 AI는 다음 형식으로 파일명을 만든다.

```text
YYYY-MM-DD-NNN-topic-short-title-draft.md
```

예:

```text
2026-04-27-001-homeassistant-dashboard-draft.md
2026-04-27-001-elgato-stream-deck-plugin-key-rendering-draft.md
```

### 외부 AI용 필수 frontmatter

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

### 외부 AI용 필수 본문 섹션

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

### 외부 AI가 하면 안 되는 것

- 공개용 파일 경로를 임의로 확정하지 않는다.
- 존재하지 않는 내부 링크를 실제 Markdown 링크처럼 만들지 않는다.
- 백링크를 확정된 사실처럼 쓰지 않는다.
- 원본 프로젝트의 민감한 정보, 토큰, 개인 경로를 포함하지 않는다.
- 이미지 파일을 본문에서 참조했다면 파일명과 위치를 함께 전달한다.

## Home Assistant 초기 운영안

폴더:

```text
inbox/ai-drafts/homeassistant/
content/posts/homeassistant/
content/assets/homeassistant/
site/_posts/homeassistant/
links/topics/homeassistant.md
```

추천 태그 후보:

- `homeassistant`
- `automation`
- `dashboard`
- `addon`
- `integration`
- `yaml`
- `mqtt`

## Elgato Stream Deck Plugin 초기 운영안

폴더:

```text
inbox/ai-drafts/elgato-stream-deck-plugin/
content/posts/elgato-stream-deck-plugin/
content/assets/elgato-stream-deck-plugin/
site/_posts/elgato-stream-deck-plugin/
links/topics/elgato-stream-deck-plugin.md
```

추천 태그 후보:

- `stream-deck`
- `elgato`
- `plugin`
- `nodejs`
- `typescript`
- `sdk`
- `ui`

## 구현 범위 초안

승인 후 다음을 구현한다.

1. 주제별 inbox/content/assets/site 폴더 생성
2. `links/topics/` 생성
3. 주제별 링크 인덱스 파일 생성
4. `docs/posting-workflow.md` 생성
5. `docs/ai-draft-guide.md` 생성
6. `docs/writing-guide.md`에 포스트 frontmatter 표준 반영
7. 샘플 draft 템플릿 생성
8. 샘플 publish-ready 템플릿 생성

## 구현 후 추가 사항

구현 진행 중 확인된 사항:

- 주제별 inbox/content/assets/site 폴더를 생성했다.
- `links/topics/`와 주제별 링크 인덱스를 생성했다.
- 외부 AI 전달용 `docs/ai-draft-guide.md`를 생성했다.
- 사용자가 파일을 어디에 옮겨야 하는지 정리한 `docs/file-transfer-guide.md`를 생성했다.
- 전체 포스팅 흐름 문서 `docs/posting-workflow.md`를 생성했다.
- `docs/writing-guide.md`에 확정된 topic/frontmatter/link 후보 규칙을 반영했다.
- `docs/templates/ai-draft-template.md`와 `docs/templates/publish-post-template.md`를 생성했다.

## 사용자 답변 필요 항목

현재 사용자 답변 필요 항목:

확정된 항목:

1. Home Assistant 주제 식별자와 파일명 표기: `homeassistant`
2. Elgato Stream Deck Plugin 주제 식별자와 파일명 표기: `elgato-stream-deck-plugin`
3. 공개 기준: GitHub에 push된 상태
4. 로컬 기준 공개/비공개 구분은 두지 않음
5. 외부 AI용 문서 작성 가이드 필요

현재 사용자 답변 필요 항목:

없음.
