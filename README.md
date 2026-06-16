# 개발 블로그 (Hugo + PaperMod)

GitHub Pages 로 배포되는 정적 개발 블로그입니다.
대표 토픽: **폴리스너츠 한글화** (카테고리).

## 구조

```
hugo.toml                         사이트 설정
content/
  posts/                          블로그 글 (카테고리/태그로 분류)
    hello.md                      블로그 시작 글 (카테고리: 잡담)
    download.md / about.md / changelog.md / license.md   (카테고리: 폴리스너츠 한글화)
  categories/폴리스너츠-한글화/_index.md   카테고리 소개 페이지
  search.md                       검색 페이지
themes/PaperMod                   테마 (git submodule)
.github/workflows/hugo.yml        push → 빌드 → Pages 자동 배포
```

## 처음 배포하기

1. **public GitHub 저장소 생성** 후 이 폴더를 push
   ```bash
   git remote add origin https://github.com/<유저명>/<저장소명>.git
   git add -A && git commit -m "init: Hugo 블로그"
   git push -u origin main
   ```
2. GitHub 저장소 → **Settings → Pages → Build and deployment → Source: GitHub Actions**
3. push 하면 Actions 가 자동 빌드·배포 → `https://<유저명>.github.io/<저장소명>/`

> `hugo.toml` 의 `baseURL`·`title`·`socialIcons`·Releases 링크를 본인 것으로 바꾸세요.
> (Actions 빌드 시 baseURL 은 Pages 주소로 자동 주입되지만, 로컬 미리보기·RSS 위해 채워두면 좋습니다.)

## 글 추가

`content/posts/` 에 마크다운 파일을 만들고 front matter 에 `categories`/`tags` 를 지정하면 됩니다.

```markdown
---
title: "글 제목"
date: 2026-06-17
categories: ["폴리스너츠 한글화"]   # 같은 토픽으로 묶임
tags: ["태그1", "태그2"]
---
```

## 로컬 미리보기 (선택)

Hugo extended 설치 후:
```bash
hugo server -D     # http://localhost:1313
```
설치: `choco install hugo-extended` (Windows) 또는 `go install` / 공식 릴리스 바이너리.
