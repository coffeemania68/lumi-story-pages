# 루미이야기 웹사이트 콘텐츠 운영 안내

**작성 기준일:** 2026-08-28  
**운영 저장소:** `coffeemania68/lumi-story-pages`  
**운영 주소:** <https://story.mypawstory.com/>  
**배포 방식:** GitHub Pages, `main` 브랜치 루트

## 1. 운영 원칙

루미이야기 웹사이트의 배포 기준은 GitHub 저장소 `coffeemania68/lumi-story-pages`의 `main` 브랜치입니다. Manus의 임시 주소인 `dreamhub-pe3mongt.manus.space`는 원본 저장소나 최종 배포 주소로 사용하지 않습니다. `dream.mypawstory.com`은 꿈해몽 앱·블로그 영역이므로 루미이야기 사이트 작업에서 수정하지 않습니다.

영어 콘텐츠는 자동 번역으로 만들거나 브라우저 번역 기능에 의존하지 않습니다. 한국어 원고와 사람이 검토한 영어 원고를 별도로 준비한 뒤, 사이트에 명시된 영어 경로 또는 사전 제작 영어 페이지로 직접 연결합니다. 현재 사이트의 EN 링크는 <https://dream.mypawstory.com/en/>인 사전 제작 영어 페이지를 가리키고 있습니다.

> **핵심 규칙:** 원고는 한국어와 영어를 따로 관리하고, `main`에 커밋한 결과만 운영 사이트에 배포합니다. 자동 번역 스크립트는 추가하지 않습니다.

## 2. 현재 저장소 구조

현재 저장소는 Manus에서 공개된 정적 사이트를 독립 배포할 수 있도록 복원한 스냅샷입니다. 따라서 일반적인 React 원본 프로젝트처럼 `src/`의 원고 파일만 수정하면 자동으로 빌드되는 구조가 아닙니다. 현재 운영 파일의 역할은 다음과 같습니다.

```text
lumi-story-pages/
├── index.html                         # 사이트 진입점
├── 404.html                           # GitHub Pages SPA fallback
├── CNAME                              # story.mypawstory.com
├── .nojekyll                          # 정적 자산 경로 보호
├── assets/
│   ├── index-*.js                     # 사이트 실행 번들 및 콘텐츠 데이터
│   └── index-*.css                    # 사이트 스타일 번들
├── manus-storage/                     # 공개 이미지·영상 자산
├── case-archive/index.html            # 사건 기록 목록 직접 접속용
├── lumi-in-motion/index.html          # Lumi in Motion 직접 접속용
├── privacy/index.html                 # 개인정보 페이지 직접 접속용
├── case-files/
│   └── <slug>/index.html              # 각 사건 기록 직접 접속용
├── .github/                           # 현재는 선택적 자동화 설정
├── README.md
└── LUMI_CONTENT_OPERATIONS.md
```

`assets/index-*.js` 안에 사건 데이터와 라우팅 데이터가 압축되어 있으므로, 현재 스냅샷에서 새 사건을 추가할 때 이 파일을 손으로 편집하는 것은 금지합니다. 원본 편집 프로젝트 또는 새 빌드 파이프라인을 먼저 확보해야 합니다.

## 3. 권장 콘텐츠 원본 구조

향후 유지보수를 위해 원고 원본은 배포 파일과 분리해 다음 구조로 관리하는 것을 권장합니다. 이 폴더 구조를 추가한다고 즉시 사이트에 반영되는 것은 아니며, 아래 원고를 읽어 정적 번들을 만드는 빌드 단계가 함께 필요합니다.

```text
content/
├── incidents/
│   ├── ko/
│   │   └── <slug>.md                  # 한국어 사건 기록
│   └── en/
│       └── <slug>.md                  # 검수 완료 영어 사건 기록
├── pages/
│   ├── ko/
│   │   └── <page-slug>.md             # 한국어 일반 페이지
│   └── en/
│       └── <page-slug>.md             # 검수 완료 영어 일반 페이지
├── data/
│   └── incidents.json                 # 목록·ID·이미지·날짜·태그 매핑
└── media/
    └── <slug>/                        # 원본 제작물, 배포 전 검수용
```

사건 기록 하나는 한국어와 영어 파일의 파일명(slug)을 반드시 동일하게 유지합니다. 예를 들어 `content/incidents/ko/lottery-detour.md`와 `content/incidents/en/lottery-detour.md`는 같은 사건의 양 언어 버전입니다. slug에는 영문 소문자, 숫자, 하이픈만 사용하고, 발행 후에는 변경하지 않습니다. URL이 바뀌어 기존 공유 링크가 끊기기 때문입니다.

사건 메타데이터는 다음과 같은 형태를 사용합니다.

```yaml
id: 11
slug: rainy-bus-stop
day: 2
series: "Lumi's day"
title_ko: "비 오는 버스 정류장"
title_en: "The Rainy Bus Stop"
status: draft
image: /manus-storage/rainy-bus-stop-hero.png
published_at: 2026-09-01
```

`status`는 `draft`, `review`, `published` 중 하나로 관리합니다. `published`가 아닌 사건은 목록 데이터와 배포 번들에 넣지 않습니다. 이미지 경로는 외부 Manus 임시 URL이 아니라 저장소 안의 `/manus-storage/` 경로를 사용합니다.

## 4. 새 사건 기록 추가 절차

### 4.1 원고와 영어 번역 준비

먼저 한국어 원고를 작성하고, 같은 slug를 사용하는 영어 원고를 별도로 작성합니다. 영어 원고는 자동 번역 결과를 그대로 사용하지 않고 제목, 본문, CTA, 메타 설명, 이미지 대체 텍스트를 사람이 검수합니다. 한국어와 영어 사이에 누락된 문단이나 링크가 없는지 확인합니다.

사건에는 제목, 짧은 소개, 본문, 태그, 이미지, 발행일, 목록에 표시할 순번을 포함합니다. 이미 발행된 사건의 `id`와 slug는 재사용하지 않습니다.

### 4.2 이미지와 동영상 저장

배포에 사용할 자산은 다음처럼 사건별로 이름을 고정합니다.

```text
manus-storage/
├── rainy-bus-stop-hero.png
├── rainy-bus-stop-study.png
└── rainy-bus-stop-reel.mp4
```

파일명에는 공백, 한글, 괄호, 임시 버전명(`final-final`)을 사용하지 않습니다. 공개 사이트에 필요하지 않은 원본 PSD, 편집 프로젝트, 개인 자료는 저장소에 올리지 않습니다.

### 4.3 사이트 데이터에 사건 추가

현재 저장소는 원본 소스가 아닌 정적 스냅샷이므로, 사건 데이터는 압축된 `assets/index-*.js`를 직접 수정하지 않습니다. 다음 중 하나를 먼저 수행해야 합니다.

1. Manus에서 편집 가능한 원본 코드 패키지를 확보하고 빌드합니다.
2. 별도 로컬 소스 프로젝트를 만들어 `content/`와 `data/`를 읽는 빌드 스크립트를 구성합니다.
3. 빌드 결과로 새 `assets/index-*.js`와 `index.html`을 생성한 뒤 저장소에 반영합니다.

원본 소스가 준비되기 전에는 새 사건의 원고와 자산만 `content/` 및 `manus-storage/`에 준비해 두고, 번들 파일에 손으로 데이터를 삽입하지 않습니다.

### 4.4 직접 접속용 route 파일 생성

GitHub Pages는 `/case-files/<slug>/` 요청에 대해 해당 폴더의 `index.html`이 있어야 200 응답을 반환합니다. 새 사건을 배포할 때는 빌드 결과의 `index.html`을 다음 위치에도 복사합니다.

```text
case-files/<slug>/index.html
```

목록 페이지, 사건 상세 페이지, 개인정보 페이지처럼 새 일반 경로를 추가할 때도 동일하게 경로 폴더 안에 `index.html`을 둡니다.

```text
new-page/index.html
```

또한 루트의 `404.html`은 유지합니다. 이 파일은 경로가 완전히 일치하지 않는 상황에서 SPA 화면을 복원하는 안전망이며, 삭제하면 직접 경로 접근 시 문제가 다시 발생할 수 있습니다.

## 5. 새 일반 페이지 추가 절차

새 페이지는 먼저 slug와 양 언어 콘텐츠를 확정합니다.

```text
content/pages/ko/about-lumi.md
content/pages/en/about-lumi.md
about-lumi/index.html
```

페이지가 사이트 메뉴에 노출되어야 한다면 원본 라우팅 데이터와 메뉴 데이터에 경로를 추가한 뒤 다시 빌드합니다. 단순히 폴더와 HTML만 만들면 메뉴에서 자동으로 나타나지 않습니다. 메뉴에 없는 랜딩 페이지라면 외부에서 직접 접근할 URL과 canonical URL을 함께 검수합니다.

`index.html`의 `<link rel="canonical">`, Open Graph URL, 이미지 경로가 새 사용자 지정 도메인인 `https://story.mypawstory.com/` 기준인지 확인합니다. Manus 임시 주소를 canonical이나 이미지 URL에 남기지 않습니다.

## 6. 로컬 검수

커밋하기 전에 저장소 루트에서 정적 서버를 실행해 새 경로를 확인합니다.

```bash
cd lumi-story-pages
python3 -m http.server 4173
```

브라우저에서 다음을 확인합니다.

```text
http://127.0.0.1:4173/
http://127.0.0.1:4173/case-archive/
http://127.0.0.1:4173/case-files/<slug>/
http://127.0.0.1:4173/<new-page>/
```

화면 검수에서는 제목과 본문 언어, 이미지 로딩, 모바일 레이아웃, 사건 목록에서 상세 페이지로 이동하는 링크, EN 링크의 목적지를 확인합니다. EN 링크가 자동 번역 URL이나 브라우저 번역 기능으로 바뀌지 않았는지 반드시 확인합니다.

## 7. GitHub 배포 절차

현재 배포는 `main` 브랜치에 push하면 GitHub Pages가 자동으로 빌드하는 방식입니다. 기본 배포 순서는 다음과 같습니다.

```bash
git status
git diff --check
git add content/ manus-storage/ case-files/ <new-page>/ assets/ index.html 404.html
git commit -m "content: add <slug> incident"
git pull --rebase origin main
git push origin main
```

사용하지 않는 파일을 정리할 때도 `CNAME`, `404.html`, `.nojekyll`, `assets/`, `manus-storage/`를 삭제하지 않습니다. push 직후 GitHub Actions의 `pages build and deployment` 실행이 `success`가 될 때까지 배포 완료로 간주하지 않습니다.

GitHub 저장소 주소는 <https://github.com/coffeemania68/lumi-story-pages>이며, Pages 설정은 `Settings → Pages`에서 확인합니다. Source는 `Deploy from a branch`, Branch는 `main`, 폴더는 `/ (root)`로 유지합니다. Custom domain은 `story.mypawstory.com`으로 유지하고, `Enforce HTTPS`를 활성화된 상태로 보존합니다.

## 8. 배포 후 검증

배포가 성공한 뒤 다음 URL을 확인합니다.

```bash
curl -I https://story.mypawstory.com/
curl -I https://story.mypawstory.com/case-archive/
curl -I https://story.mypawstory.com/case-files/<slug>/
curl -I https://story.mypawstory.com/<new-page>/
```

새 경로는 200 응답이어야 합니다. 404가 나오면 먼저 해당 폴더의 `index.html` 존재 여부와 파일명이 정확한지 확인합니다. 응답 본문이 사이트 HTML이어도 상태 코드가 404라면 경로 폴더 방식이 빠진 것이므로 `404.html`만 추가하는 것으로 끝내지 말고 해당 경로의 `index.html`을 생성합니다.

HTTPS 인증서, canonical URL, 이미지, 사건 목록, 사건 상세 화면을 확인합니다. 기존 주소가 정상인지도 함께 확인합니다.

```text
https://dream.mypawstory.com/
https://dream.mypawstory.com/en/
```

이 두 주소는 별도 꿈해몽 앱·블로그 영역이므로 루미이야기 배포에서 내용을 덮어쓰거나 DNS를 변경하지 않습니다.

## 9. 링크 검수 원칙

외부 링크는 새 글에 넣기 전에 최종 URL을 확정하고 리디렉션을 따라가며 확인합니다. 소셜 사이트는 로그인 화면으로 리디렉션될 수 있으므로, 로그인 리디렉션을 곧바로 404로 판단하지 않습니다. 반대로 사이트 내부 경로는 브라우저에서 200으로 직접 열려야 합니다.

번들 내부의 `api.manus.im`, Google Fonts의 루트 주소, 라이브러리 오류 문서 주소는 실제 사용자 버튼 링크가 아닐 수 있으므로, 링크 감사에서는 사용자에게 노출되는 `href`, `window.open`, 메뉴 경로를 우선 검사합니다.

## 10. 롤백과 장애 대응

배포 직후 문제가 생기면 먼저 GitHub Actions 실행 결과와 직전 커밋을 확인합니다. 새 콘텐츠만 되돌릴 때는 해당 커밋을 revert하고 다시 push합니다. `CNAME`이나 DNS를 먼저 삭제하지 않습니다. DNS 삭제는 사이트를 완전히 끊을 수 있으므로, 코드와 Pages 배포 상태를 먼저 복구합니다.

운영 중인 원칙은 다음과 같습니다.

> `main`은 검수 완료 배포본입니다. 원고 작성 중인 파일은 `draft`로 표시하고, 영어 번역 검수와 실제 경로 검증이 끝난 뒤에만 `published`로 전환합니다.

## 11. 앞으로의 권장 개선

현재 정적 스냅샷은 안정적인 배포에는 사용할 수 있지만, 새 사건을 자주 추가하기에는 원본 데이터와 빌드 과정이 부족합니다. 다음 단계에서는 `content/`의 한국어·영어 원고와 `data/incidents.json`을 읽어 라우트별 HTML과 자산을 자동 생성하는 별도 빌드 파이프라인을 만드는 것이 좋습니다. 그 파이프라인이 준비되면 새 글 추가는 원고 파일과 이미지 추가, 로컬 검수, `main` push만으로 단순화됩니다.

그때에도 자동 번역은 사용하지 않습니다. 한국어 원고와 사전 제작 영어 원고를 입력으로 삼고, 번역 누락 검사를 실패시키는 검수 단계를 둡니다. 모든 배포는 `story.mypawstory.com`에서 확인하고, `dream` 앱·블로그 저장소와 DNS는 별도 운영 영역으로 유지합니다.

## 참고 링크

- [루미이야기 GitHub 저장소](https://github.com/coffeemania68/lumi-story-pages)
- [루미이야기 운영 주소](https://story.mypawstory.com/)
- [GitHub Pages 공식 문서](https://docs.github.com/en/pages)
- [GitHub Pages custom domain 문제 해결](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages)
