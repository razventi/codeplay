# 개발 블로그 (Hugo + Stack)

GitHub Pages 로 배포되는 정적 개발 블로그입니다.
대표 토픽: **폴리스너츠 한글화** (카테고리).

- 테마: [Stack](https://github.com/CaiJimmy/hugo-theme-stack) (git submodule)
- 빌드: Hugo extended 0.163.2 (GitHub Actions)
- 사이트: https://razventi.github.io/dev_odyssey/

## 구조

```
hugo.toml                         사이트 설정 (Stack)
content/
  posts/                          블로그 글 (mainSections = ["posts"])
    hello.md                      블로그 시작 글 (카테고리: 잡담)
    download.md / about.md / changelog.md / license.md   (카테고리: 폴리스너츠 한글화)
  categories/폴리스너츠-한글화/_index.md   카테고리 소개 페이지(설명·배경색)
  page/search/index.md            검색 페이지 (Stack layout: search)
static/downloads/                 배포 패치 zip
layouts/_markup/render-link.html  내부 링크에 baseURL 하위경로 보정 훅
themes/hugo-theme-stack           테마 (git submodule)
.github/workflows/hugo.yml        push → 빌드 → Pages 자동 배포
```

## 글 추가

`content/posts/` 에 마크다운 파일을 만들고 front matter 에 `categories`/`tags` 를 지정합니다.

```markdown
---
title: "글 제목"
date: 2026-06-17
categories: ["폴리스너츠 한글화"]   # 같은 토픽으로 묶임
tags: ["태그1", "태그2"]
# image: "cover.jpg"               # (선택) 표지 이미지
---
```

푸시하면 1~2분 뒤 사이트에 자동 반영됩니다.

```bash
git add -A && git commit -m "새 글: 제목" && git push
```

## 메뉴 · 링크 주의사항 (Stack + 프로젝트 하위경로)

- 사이트가 `/dev_odyssey/` 하위경로에 배포되므로, **좌측 메뉴는 `pageRef`** 로 지정해야
  하위경로가 정확히 붙습니다(Stack 은 메뉴 `.URL` 을 그대로 출력함).
- 본문 마크다운의 루트상대 링크(`/posts/...`, `/downloads/...`)는
  `layouts/_markup/render-link.html` 훅이 자동으로 하위경로를 보정합니다.

## 로컬 미리보기 (선택)

Hugo extended(≥0.157) 설치 후:
```bash
hugo server -D     # http://localhost:1313
```
설치: `choco install hugo-extended` (Windows) 또는 공식 릴리스 바이너리.
