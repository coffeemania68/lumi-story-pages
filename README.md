# 루미이야기 웹사이트 작업 허브

이 폴더는 루미이야기 웹사이트를 작업하는 사람과 에이전트가 가장 먼저 읽는 안내 폴더다. 실제 웹사이트 원본과 배포 파일은 GitHub에 있다.

## 바로가기

| 목적 | 주소 |
|---|---|
| GitHub 저장소 | [coffeemania68/lumi-story-pages](https://github.com/coffeemania68/lumi-story-pages) |
| 운영 사이트 | [story.mypawstory.com](https://story.mypawstory.com/) |
| GitHub Pages 기본 주소 | [coffeemania68.github.io/lumi-story-pages](https://coffeemania68.github.io/lumi-story-pages/) |
| 영어 사건 예시 | [English cafe field note](https://story.mypawstory.com/en/case-files/cafe-field-note/) |
| 한국어 사건 예시 | [Korean cafe field note](https://story.mypawstory.com/case-files/cafe-field-note/) |

## 작업 시작

Windows PowerShell에서는 다음처럼 작업 사본을 받는다.

```powershell
gh repo clone coffeemania68/lumi-story-pages
Set-Location .\lumi-story-pages
git checkout main
```

이 폴더의 `AGENTS.md`와 `LUMI_CONTENT_OPERATIONS.md`를 먼저 읽는다. 상세 운영 문서는 GitHub 저장소의 `LUMI_CONTENT_OPERATIONS.md`를 기준으로 한다.

## 중요한 경계

`dreamhub-pe3mongt.manus.space`는 더 이상 최종 주소나 배포 원본으로 사용하지 않는다. `dream.mypawstory.com`은 꿈해몽 앱이고, 블로그도 별도 서비스다. 루미이야기 웹사이트 수정은 반드시 `lumi-story-pages` 저장소에서만 한다.

영어 콘텐츠는 자동 번역으로 만들지 않는다. 한국어 원고와 사전에 준비한 영어 원고를 각각 관리하고, 영어 사건 경로는 `/en/case-files/<slug>/` 형식으로 만든다. 한국어와 영어 링크가 서로의 언어를 잃지 않도록 한다.

## 배포 확인

`main`에 푸시하면 GitHub Pages가 배포된다. 배포가 성공한 뒤 다음 주소를 확인한다.

```text
https://story.mypawstory.com/
https://story.mypawstory.com/en/
https://story.mypawstory.com/case-files/<slug>/
https://story.mypawstory.com/en/case-files/<slug>/
```

직접 주소로 새로고침했을 때 404가 없어야 하며, 한국어·영어 페이지의 제목과 본문이 각각 올바른지 확인한다. 새 글을 추가할 때에는 먼저 로컬 검수 후 커밋하고, GitHub Actions 또는 Pages 상태가 성공한 뒤 운영 주소를 확인한다.

## 저장소 상태

현재 저장소는 공개 GitHub 저장소이며 GitHub Pages와 사용자 지정 도메인 `story.mypawstory.com`을 사용한다. 외부 연결에 필요한 비밀값은 코드에 넣지 않는다.
