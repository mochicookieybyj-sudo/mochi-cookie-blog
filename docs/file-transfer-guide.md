# File Transfer Guide

이 문서는 사용자가 다른 프로젝트/AI에게서 받은 포스팅 후보 파일을 이 블로그 프로젝트에 옮기는 방법을 정리한다.

## 기본 원칙

- 받은 원본 md 파일은 `inbox/ai-drafts/{topic}/`에 둔다.
- 받은 이미지와 첨부 파일은 `inbox/assets/{topic}/`에 둔다.
- 원본 파일은 가능한 한 수정하지 않는다.
- 공개용 최종 글은 Codex가 `site/_posts/{topic}/`에 만든다.
- 공개 기준은 GitHub에 push된 상태다.

## 주제별 위치

### Home Assistant

원본 md:

```text
inbox/ai-drafts/homeassistant/
```

원본 첨부 파일:

```text
inbox/assets/homeassistant/
```

공개용 Jekyll post:

```text
site/_posts/homeassistant/
```

정리된 공개 후보 원문:

```text
content/posts/homeassistant/
```

### Elgato Stream Deck Plugin

원본 md:

```text
inbox/ai-drafts/elgato-stream-deck-plugin/
```

원본 첨부 파일:

```text
inbox/assets/elgato-stream-deck-plugin/
```

공개용 Jekyll post:

```text
site/_posts/elgato-stream-deck-plugin/
```

정리된 공개 후보 원문:

```text
content/posts/elgato-stream-deck-plugin/
```

## 사용자가 파일을 옮기는 순서

1. 파일의 주제를 확인한다.
2. md 파일명을 확인한다.
3. md 파일을 `inbox/ai-drafts/{topic}/`에 넣는다.
4. 이미지나 첨부 파일이 있으면 `inbox/assets/{topic}/`에 넣는다.
5. Codex에게 어떤 파일을 포스팅 후보로 처리할지 알려준다.

예:

```text
inbox/ai-drafts/homeassistant/2026-04-27-001-homeassistant-dashboard-draft.md
inbox/assets/homeassistant/2026-04-27-homeassistant-dashboard-card-layout.png
```

그 다음 Codex에게 이렇게 요청한다.

```text
homeassistant 초안 2026-04-27-001-homeassistant-dashboard-draft.md 포스팅용으로 정리해줘
```

## 채팅으로 내용을 전달하는 경우

파일을 직접 옮기기 어렵다면 md 내용을 채팅에 붙여넣는다.

이때 같이 알려줄 것:

- 주제: `homeassistant` 또는 `elgato-stream-deck-plugin`
- 원하는 short-title
- 첨부 파일 유무

Codex가 규칙에 맞는 원본 draft 파일을 `inbox/ai-drafts/{topic}/`에 생성한다.

## 파일명 확인 기준

원본 draft:

```text
YYYY-MM-DD-NNN-topic-short-title-draft.md
```

좋은 예:

```text
2026-04-27-001-homeassistant-dashboard-draft.md
2026-04-27-001-elgato-stream-deck-plugin-key-rendering-draft.md
```

피해야 할 예:

```text
ha.md
streamdeck.md
draft.md
작업정리.md
```

## Codex가 처리하는 일

Codex는 원본 draft를 받은 뒤 다음을 처리한다.

1. frontmatter 확인
2. 민감 정보 확인
3. 공개용 문서 정리
4. 링크/백링크 후보 검토
5. `links/topics/{topic}.md` 업데이트
6. `site/_posts/{topic}/`에 Jekyll post 생성
7. 로컬 미리보기 실행
8. 사용자의 검수 피드백 반영
9. 승인 후 commit/push

## 링크와 백링크 처리 기준

사용자는 초안 파일을 옮길 때 링크를 직접 정리하지 않아도 된다.

다만 외부 AI가 만든 초안에는 아래 섹션이 있어야 한다.

```markdown
## 링크/백링크 후보

### 이 글이 참고하면 좋은 글

### 이 글을 나중에 참조할 수 있는 글
```

이 후보를 바탕으로 Codex가 최종 링크와 백링크를 정리한다.
