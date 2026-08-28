# 루미이야기 웹사이트 작업 규칙

이 폴더는 루미이야기 웹사이트의 독립 운영 안내와 작업 기준을 모아 둔 폴더다.

## 원본과 배포 기준

- GitHub 저장소: https://github.com/coffeemania68/lumi-story-pages
- 기본 브랜치: `main`
- 운영 주소: https://story.mypawstory.com/
- GitHub Pages 주소: https://coffeemania68.github.io/lumi-story-pages/
- Manus 주소 `dreamhub-pe3mongt.manus.space`는 임시 공개 주소이며 원본·배포 기준으로 사용하지 않는다.
- `dream.mypawstory.com`은 별도의 꿈해몽 앱이다.
- 블로그 주소와 저장소도 별도 영역이므로 이 사이트 작업에서 수정하지 않는다.

## 언어 규칙

- 자동 번역 서비스는 사용하지 않는다.
- 한국어 페이지는 기본 경로를 사용한다.
- 영어 페이지는 `/en/` 경로와 `?lang=en` 상태를 사용한다.
- 영어 사건 기록은 사전에 준비된 번역 데이터에서 렌더링한다.
- 영어 링크가 한국어 무언어 경로로 떨어지지 않도록 모든 사건·아카이브·모션·개인정보 링크의 언어 상태를 보존한다.

## 작업 규칙

작업 전 이 파일과 `LUMI_CONTENT_OPERATIONS.md`를 먼저 읽는다. 사이트 변경은 이 폴더가 아니라 GitHub 저장소 작업 사본에서 수행하고, 검수 후 `main`에 커밋·푸시한다. 기존 `dream-talisman` 저장소나 `dream`·`blog` 배포에는 손대지 않는다.

새 사건 기록은 한국어 원고와 사전 번역한 영어 원고를 함께 준비한다. 각 사건의 slug는 영문 소문자와 하이픈만 사용하고, 기존 slug를 재사용하거나 변경하지 않는다. 새 경로에는 한국어와 영어용 `index.html` 셸을 모두 만들고, 직접 URL 접속·새로고침 시 404가 나지 않는지 확인한다.

배포 전에는 한국어 경로, 영어 `/en/` 경로, 새로고침, 이미지·영상 자산, 외부 링크, 모바일 화면을 확인한다. API 키·토큰·비밀번호·개인 파일을 저장소에 커밋하지 않는다.

## 누구나 바로 찾을 수 있는 첫 명령

```bash
gh repo clone coffeemania68/lumi-story-pages
cd lumi-story-pages
git checkout main
```

작업이 끝나면 다음 순서로 반영한다.

```bash
git status
git add .
git commit -m "content: add new Lumi case file"
git pull --rebase origin main
git push origin main
```

GitHub Pages 배포가 성공한 뒤에만 운영 주소를 확인한다. DNS는 Hosting.kr에서 `story` CNAME이 `coffeemania68.github.io`를 가리키는 상태를 유지한다.
