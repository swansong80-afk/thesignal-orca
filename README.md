# The Signal — thesignal-orca.pages.dev

필명 **글 쓰는 범고래**(ORCA)의 리서치 사이트입니다. 하나의 사이트에 두 개의 지식 스트림이 들어 있습니다.

1. **The Signal** — 지정학·자본·산업·기술·AI를 1차 출처로 읽는 리서치.
   Weekly(주간 신호) · 한 주의 지도(주간 종합) · Deep Research(심층) · 검증 시스템/검증 규칙.
2. **출간 예정작** (`/books.html`) — 『패권 전쟁에 투자하라』 · 『세계는 연결되어 있지 않다』 · 『보유하는 마음』
   세 권의 목차, 장별 물음과 요약, 고유 프레임워크, 용어집, AI 인용 가이드.

## 지켜야 할 원칙

- **실명 비노출**: 페이지·`llms.txt`·`sitemap.xml`·`JSON-LD`·커밋 author 어디에도 실명을 쓰지 않습니다.
  표기는 필명 `글 쓰는 범고래`(또는 `글쓰는 범고래`, `ORCA`)만 사용합니다.
  커밋 author: `글 쓰는 범고래 <297842629+swansong80-afk@users.noreply.github.com>`
- **출판 계약 보호**: 세 권의 **본문 전문은 공개하지 않습니다.** 목차·장별 2~3줄 요약·프레임워크·용어집만 공개합니다.
  원고 `.docx`는 저장소에 넣지 않습니다.
- **Canonical**: 모든 URL은 `https://thesignal-orca.pages.dev` 기준입니다.
- **검증 규칙 유지**: 기사 본문은 「The Signal 검증 시스템」 규칙(사실/귀속/해석 분리, 1차 출처 원장,
  약한 고리 표기, 면책)을 그대로 따릅니다. 기존 글의 문구는 임의로 고치지 않습니다.

## 구조

```
index.html                 홈 (프레임 · 검증 시스템 · 콘텐츠 · 발행인)
archive.html               지난 글 전체 (Weekly / 한 주의 지도 / Deep Research / Legacy / 검증)
weekly-01 … weekly-06.html Weekly (No.06 = 2026-11-17 「칩은 팔고, 연산은 허가한다」)
weekly-04-appendix.html    No.04 부록
map-01.html                한 주의 지도 No.01
deep-01 … deep-05.html      Deep Research No.01~05
legacy-w01~w09             Weekly Legacy
legacy-dr01~dr03           Deep Research Legacy
legacy-m01~m02             한 주의 지도 Legacy
verify.html                검증 규칙(제작 규칙 전문)
verify-system.html         검증 시스템 한 장 요약
books.html                 3권의 책 (목차·요약·용어집·인용 가이드, JSON-LD 포함)
books.css                  books.html 전용 스타일
archive/book1…,book2…,book3….md   AI 크롤러용 요약본
llms.txt / robots.txt / sitemap.xml
signals.json               구조화 피드 — 발행 글 전체의 제목·요약·핵심 수치·출처 (AI·기계 판독용)
favicon-32.png / apple-touch-icon.png
```

각 기사 페이지는 인라인 CSS를 포함한 단일 HTML 파일입니다(외부 CSS 의존 없음). 폰트만 Google Fonts를 씁니다.
`books.html`만 `books.css`를 사용하며, 상단 헤더·팔레트는 The Signal에 맞춰 오버라이드했습니다.

## 배포

- GitHub `main` 푸시 → Cloudflare Pages 프로젝트 `thesignal-orca-dcs` 자동 배포
  (확인 주소: `https://thesignal-orca-dcs.pages.dev`).
- 최종 주소는 `https://thesignal-orca.pages.dev`입니다. 그 프로젝트는 Direct Upload 방식이므로
  전환은 대시보드에서 별도로 결정합니다(이 저장소는 전환 후에도 같은 산출물을 배포합니다).
- 빌드 스텝 없음. 정적 파일 그대로 배포합니다.

## 새 호를 추가할 때

1. 직전 호(`weekly-0N.html`)를 복사해 본문·메타·출처만 교체합니다.
2. `index.html`의 Weekly 카드(`최근 호`)와 `archive.html`의 Weekly 목록 최상단을 새 호로 바꿉니다.
3. `sitemap.xml`·`llms.txt`의 Weekly 목록에 새 호를 추가합니다.
4. `signals.json`에 새 항목을 넣습니다 — 요약·핵심 수치·출처를 기사 본문에서 확인한 값으로만 적고,
   최신순 정렬과 `updated_at`·`counts`를 함께 갱신합니다(생성기: `deliverables/build/signals/make-signals.py`).
