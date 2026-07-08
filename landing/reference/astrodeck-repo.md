# astrodeck 레포 직접 활용법 (primary 방식)

요약본을 손으로 재현하지 않고, **실제 astrodeck 레포를 클론 → 데이터만 교체 → 빌드**한다.
룩·인터랙션·다크모드·폰트를 원본 그대로 살린다.

- 레포: https://github.com/holger1411/astrodeck  (**MIT License** — 클론·수정·사용 자유)
- 스택: Astro. 템플릿 페이지는 **데이터 주도형** — 각 `.astro` 상단 프론트매터에 JS 객체(features/testimonials/faqs/tiers…)를 정의하고, 그걸 섹션 컴포넌트에 props로 넘긴다.
- **컴포넌트·스타일·CSS는 절대 건드리지 않는다. 데이터 배열과 히어로/CTA 카피만 우리 내용으로 교체.**

## 셋업 & 빌드 (캐시 재사용 — 반복 실행 빠름)
```bash
cd "<프로젝트 디렉토리>"                 # 사용자 cwd. .claude/skills 안이면 안 됨
[ -d astrodeck ] || git clone --depth 1 https://github.com/holger1411/astrodeck.git astrodeck  # 있으면 생략
cd astrodeck
[ -d node_modules ] || npm install --no-audit --no-fund   # 최초 1회만 (~549패키지)
# (여기서 templates/*.astro 데이터 교체 + 브랜딩 정리)
npm run build && npm run preview       # preview: http://localhost:4321/
```
- node 18+ 필요(검증: node 22 / npm 10).
- **캐시 포인트**: `astrodeck/` 재사용 → clone 생략, `node_modules` 재사용 → install 생략. 첫 실행만 무겁고(clone+install), 다음부터는 **빌드만(수 초)**. 아이디어 바뀌어도 데이터만 다시 교체 후 build.

## 랜딩용 템플릿 3개 (이 중 **1개만** 골라 교체·빌드)
3개가 유사해 전부 만들 필요 없다. 목적에 맞는 1개만(선택 기준 = landing SKILL.md "템플릿 선택").
`src/pages/templates/` 안:
- `startup.astro`  → **Startup룩** (검증용 최적: 경쟁비교+얼리어답터 포함)
- `saas.astro`     → **SaaS룩** (가격티어+FAQ)
- `portfolio.astro`→ **Agency룩** (스플릿히어로+교차블록+팀)
- `contact.astro`  → 문의폼 성격(랜딩 아님) — 기본은 건드리지 않음. 4번째가 필요하면 이걸로.
- ※ astrodeck엔 별도 "Home룩" 랜딩이 없다. `index.astro`는 astrodeck 자체 홍보 홈이라 랜딩용 아님.

## 캔버스 → 데이터 매핑
- UVP/키카피 → Hero* 의 `title`/`subtitle` (subtitle은 `<mark>강조</mark>` 지원)
- Solution → `features[]`
- 기존대안 → `comparisonColumns` + `comparisonFeatures` (startup)
- Problem → portfolio의 ContentBlock(tagline "Problem")
- Revenue → `tiers[]` (saas)
- Customer/얼리어답터 → Testimonials 톤·회사명
- Key Metrics 신호 → CTA `cta.label` (허영 아닌 진짜 커밋: 사전신청/문의)
- **미검증 수치·후기·로고·가격·팀 = 전부 `[플레이스홀더]`.** 있는 척 금지.

## 템플릿별 섹션 구성 (import 순서 = 페이지 순서)
- **startup**: HeroGradient → Features → Comparison → ContentBlock → Stats → Testimonials → FAQ → CTA
- **saas**: Hero → LogoCloud → Features → Stats → Pricing → Testimonials → FAQ → CTA
- **portfolio**: HeroSplit → LogoCloud → Stats → ContentBlock×2(Problem/Solution) → Team → Testimonials → Newsletter → CTA
- 섹션 배경 대비는 래퍼 `<div class="section-muted">` / `<div class="section-inverted">` 로 감싼다(원본 그대로 유지).

## 컴포넌트 props 치트시트 (src/components/sections/)
```
HeroGradient  { badge?, title, subtitle, primaryCta:{href,label}, secondaryCta?:{href,label} }
Hero          { badge:"true", title, subtitle, primaryCta, secondaryCta }
HeroSplit     { tagline, title, subtitle, primaryCta, secondaryCta }
Features      { title, subtitle, features:[{title, description, icon}] }
                 icon ∈ zap | shield | chart | users | globe | lock
Comparison    { title, subtitle,
                 columns:[{name, highlighted?}],
                 features:[{name, values:[...]}] }   // values 순서=columns 순서, bool 또는 문자열
ContentBlock  { tagline, title, description, imageSide:'left'|'right', features:[string] }
Stats         { title?, subtitle?, stats:[{value, label, description}] }
Pricing       { title, subtitle,
                 tiers:[{name, price, description, features:[string], cta:{href,label}, highlighted?}] }
Testimonials  { title, testimonials:[{quote, author, role, company}] }
FAQ           { title, subtitle, faqs:[{question, answer}] }
CTA           { title, description, cta:{href,label} }
LogoCloud     { title }
Team          { title, subtitle, members:[{name, role, bio, social:{twitter?,linkedin?,github?}}] }
Newsletter    { title, description, placeholder, buttonText }
```
- subtitle/description에 `<mark>` 로 핵심구 강조 가능(Hero류).
- CTA href는 검증 링크(사전신청 폼/문의) 또는 `#`.

## 브랜딩 정리 (3파일 — 데이터 교체와 함께 매번, 3룩 공용이라 1회면 전부 반영)
astrodeck엔 중앙 config가 없어 브랜딩이 하드코딩. 안 고치면 "AstroDeck" 데모처럼 보임.
서비스명 = 캔버스 하이레벨 컨셉의 브랜드(예: "리핏"). 없으면 `[서비스명]` 플레이스홀더.
1. **`src/components/Logo.astro`** — 맨 아래 워드마크 `{showText && <span …>AstroDeck</span>}` 의 **"AstroDeck" → 서비스명**. (SVG 카드덱 아이콘은 그대로 두거나 실로고 있으면 교체)
2. **`src/components/Header.astro`** — `navItems` 배열을 **랜딩 앵커**로 교체:
   `const navItems = [{ href: '#features', label: '기능' }, { href: '#pricing', label: '가격' }, { href: '#cta', label: '사전신청' }];`
   (해당 앵커 id가 페이지에 없으면 있는 섹션 id에 맞추거나 항목 뺀다.)
3. **`src/components/Footer.astro`** — `footerLinks` 를 최소화(랜딩 앵커만) + `"Open-source Astro.js starter kit…"` 태그라인 → **서비스 한 줄 소개**, `"AstroDeck"` 헤딩 → 서비스명.

## 함정 (겪은 것)
1. **빌드 산출물은 절대경로(`/…`)로 에셋 참조** → `dist/**/index.html` 을 file:// 로 직접 열면 CSS 깨짐.
   반드시 `npm run preview`(localhost:4321) 로 확인. 정적 호스팅 배포는 정상.
   프리뷰 주소: `http://localhost:4321/templates/{startup|saas|portfolio}/`
2. **브랜딩은 중앙 config가 없다** → 위 "브랜딩 정리" 3파일을 반드시 실행.
3. guard-conventions 훅 + `npm run check:kpis` 가 있지만 데이터만 바꾸면 빌드 통과.
4. `git clone` 시 `.git` 이 딸려온다. 우리 프로젝트에 커밋할 거면 `astrodeck/.git` 정리 고려.

## 폴백 (네트워크/npm 불가 시)
클론·빌드가 막히면 `astrodeck-templates.md` 의 토큰·섹션 요약으로 **단일 self-contained HTML** 4종을 손으로 재현(구 방식). 룩 재현도이지 원본은 아님 → 가능하면 레포 방식 우선.
