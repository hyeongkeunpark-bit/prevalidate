---
name: landing
description: 채운 린캔버스 + 키카피를 바탕으로 검증용 랜딩페이지를 astrodeck 4종(Home·SaaS·Portfolio·Startup) 스타일로 각각 단일 HTML 샘플로 뽑는다. 하나를 고르지 않고 4개를 다 만들어 룩을 비교·선택하게 한다. "랜딩 만들어줘", "샘플 페이지 뽑아줘", "이 카피로 랜딩 4개" 류 요청에 사용. item-check·key-copy 다음 마지막 단계.
---

# landing — astrodeck 랜딩 4종 샘플 (단일 HTML)

캔버스·카피를 **astrodeck 랜딩 4종 룩**으로 각각 뽑아, 사용자가 **4가지를 보고 고르게** 한다.
(하나를 고르지 않음 — key-copy가 카피 N개 주듯, 랜딩도 4룩 제시)

## 전제
- `lean-canvas.md` + `key-copy.md`를 먼저 읽는다. 없으면 `/item-check` → `/key-copy` 먼저.
- item-check 판정이 ❌(아직 이르다)면 **랜딩 만들지 않는다.**
- 템플릿 구조·디자인토큰은 `reference/astrodeck-templates.md` 참조 (astrodeck MIT, 실제 빌드에서 추출).

## 출력 = 단일 HTML 4개
`landing-home.html` / `landing-saas.html` / `landing-portfolio.html` / `landing-startup.html`
- 전부 **self-contained 단일 HTML** (인라인 CSS, 외부 상대경로 에셋 없음 → 배포 초간단)
- 이미지는 **플레이스홀더 + `onerror` 폴백** (실제 이미지는 이후 채움)
- astrodeck 룩: **primary `#0066FF`, Geist 폰트(+system 폴백), shadcn 팔레트, 라이트 기본**
- 모바일 반응형. CTA는 캔버스의 Key Metrics가 잡을 **진짜 신호**를 향하게(허영 가입 아님)

## 4종 언제 쓰나 (참조자료에 상세)
| 파일 | 템플릿 | 어울리는 아이템 |
|---|---|---|
| landing-startup | Startup/Product Launch | **검증용 최적** — 경쟁 비교·얼리어답터 섹션이 캔버스와 1:1 |
| landing-saas | SaaS Landing | 구독형 B2B (가격 티어·로고클라우드·FAQ) |
| landing-portfolio | Portfolio/Agency | 서비스·에이전시 (클라이언트 로고·팀) |
| landing-home | Home | 일반/기본 (센터 히어로) |

## 순서
1. `lean-canvas.md`·`key-copy.md`·`reference/astrodeck-templates.md`를 읽는다.
2. 각 템플릿마다 단일 HTML 생성:
   - **구조**: 참조자료의 섹션 순서대로
   - **내용**: 캔버스→랜딩 매핑(UVP=히어로 헤드라인, Problem=문제섹션, Solution=기능, 기존대안=경쟁비교, Customer=얼리어답터/타겟, Revenue=가격·CTA)
   - **히어로 카피**: 그 템플릿 톤에 가장 맞는 **key-copy 변형**을 골라 넣는다(4샘플이 카피도 조금씩 다르게)
   - **디자인토큰**: 참조자료 값 그대로(제약으로)
   - 검증 안 된 수치·로고·후기는 `[플레이스홀더]`로 명시
3. **AI 슬롭 체크**: 보라 그라데이션 남발/이모지 아이콘/의미없는 3카드/과한 그림자/가짜 대시보드 금지.
4. 4개 파일 저장 → 사용자에게 "4룩 비교 후 택1" + "이미지·수치는 플레이스홀더" 고지.

## 다음
고른 1개의 이미지 슬롯 채우기 → (있으면) `landing-visuals` 스킬로 레퍼런스 보드→생성.
배포는 단일 HTML이라 어떤 정적 호스팅에도 바로 올라감.
