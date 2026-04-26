# GitHub 블로그 관리 구조 제안서

## 목적

이 프로젝트를 GitHub 기반 블로그 운영 허브로 구성한다.

핵심 목표는 다음과 같다.

- 여러 프로젝트/AI가 작성한 초안 md 파일을 안전하게 수집한다.
- 공개 전 localhost에서 포스트 렌더링과 링크를 검수한다.
- 검수 통과 후에만 GitHub 공개 위치로 반영한다.
- 관련 포스팅 링크, 백링크, 태그, 시리즈 정보를 이 프로젝트에서 최종 정리한다.
- 구현 요청은 항상 이 제안서 문서를 먼저 거친다.

## 운영 원칙 반영

### 제안서 우선

사용자가 기능 구현을 요청하면 즉시 구현하지 않고, 먼저 날짜-시간으로 시작하는 제안서 파일을 작성한다.

예상 파일명 형식:

```text
YYYY-MM-DD-HHmm-topic-proposal.md
```

예:

```text
2026-04-27-0027-github-blog-structure-proposal.md
```

### 같은 제안서 유지

하나의 구현 흐름에서는 하나의 제안서를 계속 수정한다.

- 사용자 수정 요청: 같은 제안서 내용만 갱신
- 구현 승인: 같은 제안서를 기준으로 구현
- 구현 후 문제/아쉬움/추가 요청: 같은 제안서에 `구현 후 추가 사항` 항목 추가
- 최종 완료 선언: 파일명 앞에 `[완료]` 추가
- 사용자의 답변이나 판단이 필요한 항목은 항상 제안서 맨 아래에 배치
- 제안서에는 설계 결정과 운영 방향만 작성하고, 명령 실행 순서 같은 구현 절차는 승인 후 작업 중에 처리

예:

```text
[완료]2026-04-27-0027-github-blog-structure-proposal.md
```

## 추천 폴더 구조

```text
mochi-cookie-blog/
  proposals/
    active/
    completed/

  AGENTS.md
  PROJECT_CONTEXT.md

  inbox/
    ai-drafts/
    assets/

  content/
    posts/
    series/
    pages/
    assets/

  links/
    backlink-index.md
    series-index.md
    tag-index.md

  site/
    // localhost 미리보기용 블로그 앱

  scripts/
    validate-posts/
    publish/

  docs/
    workflow.md
    writing-guide.md
    github-guide.md
```

## 폴더별 역할

### AGENTS.md

새 세션의 AI가 가장 먼저 읽어야 하는 프로젝트 작업 지침이다.

이 파일에는 다음 내용을 저장한다.

- 구현 요청을 받으면 먼저 제안서를 작성한다.
- 사용자 승인 전에는 실제 구현을 하지 않는다.
- 제안서는 하나의 구현 흐름에서 계속 같은 파일을 수정한다.
- 사용자 답변 필요 항목은 항상 제안서 맨 아래에 둔다.
- 최종 완료 선언을 받으면 제안서 파일명 앞에 `[완료]`를 붙인다.
- 다른 프로젝트/AI가 보낸 md 초안은 원본과 공개용 문서를 분리한다.
- 공개 전 localhost 검수를 통과한 포스트만 GitHub 공개 대상으로 삼는다.

### PROJECT_CONTEXT.md

프로젝트의 현재 상태와 운영 목적을 요약하는 문서다.

이 파일에는 다음 내용을 저장한다.

- 이 프로젝트의 역할
- 현재 폴더 구조
- GitHub/repo 연결 상태
- 블로그 프레임워크 선택 상태
- 로컬 테스트 방식
- 포스트 처리 흐름
- 아직 결정되지 않은 사항

새 세션에서는 `AGENTS.md`를 먼저 읽고, 이어서 `PROJECT_CONTEXT.md`를 읽은 뒤 작업한다.

### proposals

구현/운영 변경 제안서를 관리한다.

- `active/`: 진행 중인 제안서
- `completed/`: 완료된 제안서

초기에는 루트에 제안서를 둘 수도 있지만, 제안서가 많아질 것을 고려하면 `proposals/active`와 `proposals/completed`로 분리하는 편이 좋다.

### inbox

다른 프로젝트의 AI가 작성한 md 파일을 임시로 받는 곳이다.

- `inbox/ai-drafts/`: 원본 초안
- `inbox/assets/`: 외부 프로젝트에서 전달된 이미지, 첨부 파일

이 폴더의 파일은 원본성을 보존하고, 실제 공개용 문서는 `content/posts`로 옮겨 정리한다.

### content

실제 블로그 콘텐츠의 원천이다.

- `content/posts/`: 공개 대상 포스트
- `content/series/`: 시리즈 설명 및 순서 관리
- `content/pages/`: 소개, 프로젝트 목록 같은 고정 페이지
- `content/assets/`: 공개 콘텐츠에 쓰이는 이미지와 자료

### links

포스트 간 연결 정보를 관리한다.

- `backlink-index.md`: 포스트별 역참조
- `series-index.md`: 시리즈별 포스트 순서
- `tag-index.md`: 태그별 포스트 목록

초기에는 수동 관리로 시작하고, 포스트 수가 늘어나면 스크립트로 자동 생성하는 방식을 추천한다.

### site

localhost 미리보기용 블로그 앱을 둔다.

추천 후보:

1. Jekyll
2. Hugo
3. Astro
4. VitePress
5. Next.js

현재 목적에는 Jekyll을 1순위로 추천한다.

이유:

- GitHub Pages가 공식적으로 Jekyll 기반 흐름을 지원한다.
- GitHub 블로그 운영 사례에서 가장 흔한 선택지 중 하나다.
- Markdown, frontmatter, `_posts` 구조가 블로그 운영에 적합하다.
- GitHub Actions를 통해 빌드/배포 자동화를 구성하기 좋다.

주의점:

- Jekyll은 Ruby 기반이라 Windows 로컬 환경에서는 RubyInstaller 또는 WSL 설정이 필요할 수 있다.
- 로컬 설치 부담이 커지면 Docker 또는 GitHub Actions 기반 빌드 검증으로 보완한다.

### scripts

검수와 배포 보조 스크립트를 둔다.

초기 후보:

- 포스트 frontmatter 검사
- 내부 링크 검사
- 이미지 경로 검사
- 공개 전 빌드 테스트
- `inbox` 초안을 `content/posts` 형식으로 변환

### docs

프로젝트 운영 문서를 둔다.

- `workflow.md`: 전체 작업 흐름
- `writing-guide.md`: 포스트 작성 규칙
- `github-guide.md`: GitHub push, branch, PR, publish 규칙

## 제안하는 GitHub 운영 방식

### 브랜치

```text
main
draft
publish
```

- `main`: 관리 기준 브랜치
- `draft`: 초안 정리 및 검수 브랜치
- `publish`: 공개 배포용 브랜치

단순하게 시작하려면 `main` 하나로 시작하고, 공개 자동화가 생긴 뒤 브랜치를 나누는 것도 가능하다.

### 공개 방식

초기 추천:

```text
GitHub repo + GitHub Pages
```

이 방식이면 별도 서버 없이 정적 블로그를 공개할 수 있다.

단, 블로그 프레임워크를 무엇으로 할지 정한 뒤 GitHub Pages 설정을 맞추는 편이 좋다.

## 포스트 처리 흐름

```text
외부 AI가 md 작성
-> inbox/ai-drafts 에 수집
-> 내용/메타데이터/링크 검토
-> content/posts 로 공개용 문서 생성
-> localhost 미리보기
-> 링크/백링크/이미지 검수
-> GitHub push
-> 공개 확인
```

## 포스트 기본 메타데이터 초안

```yaml
---
title: ""
description: ""
date: "YYYY-MM-DD"
updated: "YYYY-MM-DD"
tags: []
series: ""
source_project: ""
source_ai: ""
status: "draft"
---
```

`status` 후보:

- `draft`: 초안
- `review`: 로컬 검수 중
- `ready`: 공개 준비 완료
- `published`: 공개 완료

## 추천 결정안

현재 단계에서는 다음을 추천한다.

1. 세션 일관성 지침: `AGENTS.md`와 `PROJECT_CONTEXT.md`를 먼저 생성
2. 블로그 프레임워크: Jekyll
3. 제안서 위치: `proposals/active`
4. 공개 방식: GitHub Pages
5. 초기 브랜치: `main` 단일 브랜치
6. 포스트 상태 관리: frontmatter의 `status` 필드 사용
7. 로컬 검수: `bundle exec jekyll serve`, `bundle exec jekyll build`, 사용자 직접 검수 순서로 진행
8. GitHub repo 이름: `mochi-cookie-blog`
9. 외부 AI md 최소 형식: 제목, 작성일, 원본 프로젝트, 작성 AI, 본문 요약, 작업 내용, 결과, 이슈/아쉬운점, 참고 링크 포함
10. GitHub Pages 공개 URL 형식: 프로젝트 사이트 방식

```text
https://계정명.github.io/mochi-cookie-blog/
```

## GitHub 권한 준비

실제 GitHub repo 생성, push, GitHub Pages 설정을 진행하려면 로컬 환경에서 GitHub 인증이 필요하다.

권한 확보 방식:

GitHub SSH 설정을 사용한다.

선택 이유:

- 이후 `git push`, `git pull`을 안정적으로 처리할 수 있다.
- GitHub 계정 권한과 로컬 Git 작업을 분리해서 관리하기 좋다.
- 한 번 설정하면 이 프로젝트뿐 아니라 같은 계정의 다른 repo 작업에도 재사용할 수 있다.

예상 remote 형식:

```text
git@github.com:계정명/mochi-cookie-blog.git
```

필요 권한:

- repo 생성 권한
- repo push 권한
- GitHub Pages 설정 권한
- GitHub Actions 사용 권한

## 구현 범위 초안

사용자가 승인하면 다음 순서로 구현한다.

1. `AGENTS.md` 생성
2. `PROJECT_CONTEXT.md` 생성
3. 기본 폴더 구조 생성
4. 현재 제안서를 `proposals/active`로 이동
5. Git 저장소 초기화
6. Jekyll 기반 `site` 생성
7. `content/posts` 샘플 포스트 1개 생성
8. localhost 미리보기 명령 구성
9. GitHub SSH 방식으로 repo 연결 준비

## 구현 후 추가 사항

구현 진행 중 확인된 사항:

- Git 저장소를 초기화했다.
- 세션 일관성 파일 `AGENTS.md`를 생성했다.
- 프로젝트 상태 파일 `PROJECT_CONTEXT.md`를 생성했다.
- 기본 폴더 구조를 생성했다.
- Jekyll 최소 사이트 구조를 `site/` 아래에 생성했다.
- 로컬 환경에 Ruby/Bundler가 아직 설치되어 있지 않아 Jekyll 로컬 실행은 보류 상태다.
- 기존 SSH 키는 다른 계정용으로 보고 건드리지 않았다.
- 전용 GitHub 계정용 SSH 키 `~/.ssh/id_ed25519_mochi_cookie_blog`를 생성했다.
- SSH config에 전용 Host alias `github-mochi`를 추가했다.
- 이 PC에는 다른 용도의 GitHub 계정이 이미 설정되어 있으므로, 블로그 repo에는 기본 `github.com` SSH host를 사용하지 않는다.
- 블로그 repo remote는 반드시 `git@github-mochi:mochicookieybyj-sudo/mochi-cookie-blog.git` 형식을 사용한다.
- GitHub SSH 연결 테스트 결과 `mochicookieybyj-sudo` 계정으로 인증 성공했다.
- 로컬 첫 커밋 `09ae455 Initial blog management scaffold`를 생성했다.
- 기본 브랜치를 `main`으로 변경했다.
- `origin` remote를 `git@github-mochi:mochicookieybyj-sudo/mochi-cookie-blog.git`로 설정했다.
- `gh auth login`은 브라우저 인증 대기 중 타임아웃되어 완료되지 않았다.
- `git push -u origin main` 결과 GitHub에 `mochi-cookie-blog` repo가 아직 없어 `Repository not found`로 실패했다.
- 사용자가 GitHub 웹에서 public repo `mochi-cookie-blog`를 생성했다.
- 이후 `git push -u origin main`이 성공했고, 로컬 `main`이 `origin/main`을 추적하도록 설정됐다.
- `site/` 폴더를 GitHub Pages로 배포하기 위해 GitHub Actions workflow `.github/workflows/pages.yml`을 추가했다.
- 첫 Pages workflow는 `Setup Pages` 단계에서 실패했다.
- `site/`는 baseurl을 직접 지정하므로 `actions/configure-pages` 단계를 제거해 재시도하도록 수정했다.
- 수정 후 GitHub Actions build/deploy가 모두 성공했다.
- `https://mochicookieybyj-sudo.github.io/mochi-cookie-blog/` 접속 확인 결과 `200 OK` 응답을 받았다.
- 사용자가 공개 전 직접 확인할 수 있도록 표준 Jekyll 로컬 미리보기 방식을 선택했다.
- Ruby 3.3 with MSYS2 DevKit을 설치했다.
- Windows Jekyll timezone 의존성 문제를 해결하기 위해 `site/Gemfile`에 `tzinfo`, `tzinfo-data`를 추가했다.
- `bundle install`이 성공했다.
- `bundle exec jekyll build --baseurl=` 로컬 빌드가 성공했다.
- `bundle exec jekyll serve --baseurl= --host 127.0.0.1 --port 4000` 서버 실행 후 `http://127.0.0.1:4000/` 접속 확인 결과 `200 OK` 응답을 받았다.

로컬 미리보기 방식:

- 공개 전 사용자가 직접 화면과 동작을 확인할 수 있도록 표준 Jekyll 로컬 미리보기를 사용한다.
- Windows 환경에 Ruby와 Bundler를 설치한 뒤 `site/` 폴더에서 Jekyll 서버를 실행한다.
- 로컬 미리보기 주소는 `http://localhost:4000`을 기본으로 사용한다.
- GitHub Pages의 `baseurl` 때문에 로컬 실행 시에는 `--baseurl ""` 옵션을 사용한다.
- 포스트나 기능을 공개하기 전에는 로컬 미리보기에서 먼저 확인하고, 통과한 변경만 GitHub에 push한다.

예상 검수 흐름:

1. `site/`에서 Jekyll 로컬 서버 실행
2. `http://localhost:4000`에서 사용자가 직접 확인
3. 문제가 있으면 로컬에서 수정
4. 미리보기 통과 후 commit
5. GitHub push
6. GitHub Actions 배포 결과 확인

## 사용자 답변 필요 항목

현재 확정된 항목:

1. 새 세션 지침 파일명: `AGENTS.md`
2. 프로젝트 상태 요약 파일명: `PROJECT_CONTEXT.md`
3. 블로그 프레임워크: Jekyll
4. 제안서 위치: `proposals/active`
5. GitHub repo 이름: `mochi-cookie-blog`
6. 포스트 공개 전 검수 기준: 사용자가 직접 localhost에서 최종 검수
7. 외부 AI md 최소 형식: Codex가 정한 표준 형식 사용
8. GitHub Pages 공개 URL 형식: `https://계정명.github.io/mochi-cookie-blog/`
9. GitHub 연결 방식: SSH
10. 로컬 미리보기: Ruby/Bundler 기반 Jekyll 로컬 서버 사용

현재 사용자 답변 필요 항목:

없음.
