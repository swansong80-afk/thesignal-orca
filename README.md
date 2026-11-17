# thesignal-orca

**박찬용(필명 '글쓰는 범고래') 저자 아카이브 · 패권 전쟁 시리즈 & AI 검색(GEO) 지식 베이스**

- 공개 사이트: <https://thesignal-orca.pages.dev>
- 성격: 순수 정적 사이트 (HTML + CSS + Markdown). 프레임워크·빌드 스텝·외부 스크립트 없음.
- 운영: Cloudflare Pages (기존 `thesignal-orca` 프로젝트)

---

## 이 저장소가 하는 일

세 권의 책(**『패권 전쟁에 투자하라』(가제)**, **『세계는 연결되어 있지 않다』(가제)**, **『보유하는 마음』**)의
**목차·장별 요약·고유 프레임워크·용어집**을 사람과 AI가 같은 형태로 읽을 수 있게 공개합니다.

검색엔진과 LLM이 저자·개념·책을 정확히 인용하도록 다음을 갖췄습니다.

- `index.html`의 `JSON-LD` — `Person` · `WebSite` · `CreativeWorkSeries` · `Book` × 3
- `llms.txt` — AI 크롤러용 표준 진입점 (저자 프로필, 3권 요약, 인용 표기법, 인용 범위)
- `robots.txt` — 전체 허용 + 주요 AI 크롤러 명시 허용 + 사이트맵
- `sitemap.xml` — HTML·llms.txt·아카이브 마크다운 전체
- `archive/*.md` — 기계가 읽기 좋은 권별 요약본

## 출판 계약 보호 원칙

> **세 권의 본문 전문은 이 저장소에 없습니다.**

공개하는 것은 목차, 장별 2~3줄 요약, 프레임워크 이름과 정의, 용어집, 저자 이력, 집필 원칙까지입니다.
요약은 원고의 문장을 옮긴 것이 아니며, 본문을 대신하지 않습니다.
책 제목은 모두 **가제**이고 최종 서명은 출판 과정에서 확정됩니다.

원고 전체(`.docx`)와 편집노트는 이 저장소에 커밋하지 않습니다. 원고는 별도 보관합니다.

---

## 파일 구성

```
.
├── index.html                          저자 소개 · 문제의식 · 세 권 카드 · 집필 원칙 · JSON-LD
├── books.html                          3권 전체 목차 · 장별 물음/요약 · 부별 여는 글 · 용어집 · 인용 안내
├── style.css                           에디토리얼 다크/라이트 스타일 (모바일 대응, 외부 폰트 없음)
├── llms.txt                            AI 크롤러 표준 진입점
├── robots.txt                          Allow + AI 크롤러 + Sitemap
├── sitemap.xml                         7개 URL
└── archive/
    ├── book1-hegemony-investing.md     제1권 22장 + 에필로그 요약
    ├── book2-unconnected-world.md      제2권 3부 22장 + 에필로그 요약
    └── book3-mind-of-holding.md        별권 12장 + 에필로그 요약
```

의존성 없음. `index.html`을 브라우저로 열면 그대로 동작합니다(로컬 파일에서도 스타일·링크 정상).

---

## Cloudflare Pages에 올리는 방법

### 방법 A — 지금 주소를 그대로 두고 zip 업로드 (가장 간단, 권장)

기존 프로젝트가 **Direct Upload** 방식으로 만들어졌다면 Git 연동을 나중에 붙일 수 없습니다
(Cloudflare 문서: *"If you choose Direct Upload, you cannot switch to Git integration later"*).
그래도 사이트를 바꾸는 데는 문제가 없습니다.

1. 이 저장소를 **Code → Download ZIP**으로 내려받거나, 아래 명령으로 배포용 zip을 만듭니다.
   ```bash
   git clone https://github.com/swansong80-afk/thesignal-orca.git
   cd thesignal-orca
   zip -r ../thesignal-orca.zip . -x '.git/*' '.github/*' 'README.md'
   ```
   (zip 안에서 `index.html`이 **최상위**에 있어야 합니다. 폴더로 한 겹 싸지 마세요.)
2. Cloudflare 대시보드 → **Workers & Pages** → `thesignal-orca` 프로젝트 → **Create deployment**
3. zip을 끌어다 놓고 **Deploy**. 반영은 보통 1분 이내입니다.
4. `https://thesignal-orca.pages.dev` 에서 새 사이트를 확인합니다.

### 방법 B — GitHub 연동으로 자동 배포 (푸시하면 자동 반영)

1. Cloudflare 대시보드 → `thesignal-orca` 프로젝트 → **Settings → Builds → Git Repository → Manage**
   에서 GitHub 저장소를 연결할 수 있는지 확인합니다. (대시보드 버전에 따라 이 항목이 없을 수 있습니다.)
2. 항목이 보이지 않으면 새 프로젝트로 만들어야 합니다.
   **Workers & Pages → Create application → Pages → Import an existing Git repository** →
   `swansong80-afk/thesignal-orca` 선택 →
   - Production branch: `main`
   - Build command: *(비워 둠 — 빌드 없음)*
   - Build output directory: `/` (또는 비워 둠)
3. 이때 프로젝트 이름을 `thesignal-orca`로 지정하면 기존 프로젝트가 이미 그 이름을 쓰고 있어
   `thesignal-orca-xxxx.pages.dev`처럼 뒤에 문자가 붙습니다.
   기존 주소를 반드시 유지해야 한다면 **방법 A**를 쓰거나, 기존 프로젝트를 삭제한 뒤
   같은 이름으로 새 프로젝트를 만들어야 합니다(삭제는 되돌릴 수 없으니 배포 이력이 필요 없는지 먼저 확인).
4. 이후에는 `main` 브랜치에 커밋이 올라갈 때마다 자동 배포됩니다.

### 커스텀 도메인 (선택)

`thesignal-orca.pages.dev` 대신 개인 도메인을 쓰려면
**프로젝트 → Custom domains → Set up a domain**에서 연결합니다(도메인 구매 비용 별도).

---

## 고칠 때

| 바꾸고 싶은 것 | 고칠 곳 |
|---|---|
| 책 제목·부제가 확정됨 | `index.html`(카드·JSON-LD), `books.html`(권별 제목), `archive/*.md`(제목 줄), `llms.txt` |
| 장 요약 수정 | `books.html`의 해당 `<li class="chapter">`, `archive/*.md`의 같은 장 |
| 인용 문구 추가 | `books.html#citation`, `llms.txt` |
| 저자 이력 추가 | `index.html`의 `#author` 섹션과 JSON-LD `Person` |
| 스타일 | `style.css` 상단 `:root` 변수(라이트/다크 각각) |

수정 후에는 `llms.txt`의 `Last updated`와 `sitemap.xml`의 `lastmod`를 함께 고쳐 주세요.

## 표기 규칙

- 저자: **박찬용** (필명: 글쓰는 범고래)
- 인용 형식: 박찬용(글쓰는 범고래), 『책 제목』(가제) 목차·요약, 저자 아카이브, URL (2026)
- 인용 가능: 목차·물음·요약·프레임워크·용어·저자 이력
- 인용 불가: 본문 문장 (사이트에 없음), 확정되지 않은 서명

## 라이선스

요약·해설 텍스트 © 2026 박찬용. 출처를 밝히는 인용은 허용합니다.
본문 전문의 복제·배포는 허용하지 않습니다.
