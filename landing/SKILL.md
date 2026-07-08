---
name: landing
description: 채운 린캔버스 + 키카피를 바탕으로 검증용 랜딩을 astrodeck 4종(Startup·SaaS·Portfolio·Home) 스타일로 각각 단일 HTML 샘플로 뽑는다. 하나 고르지 않고 4룩 제시. 채팅엔 파일 4개 + 짧은 안내만. "랜딩 만들어줘", "샘플 페이지 뽑아줘" 류 요청에 사용. item-check·key-copy 다음 마지막 단계.
---

# landing — astrodeck 랜딩 4종 샘플 (단일 HTML)

## 규율 (겉으로 설명하지 말고 그냥 적용)
- 캔버스+카피 → astrodeck **4룩 각각 단일 HTML**. 하나 안 고르고 4개 제시(고르는 건 사용자).
- 전부 **self-contained 단일 HTML** — 인라인 CSS, 외부 상대경로 에셋 X, 이미지=플레이스홀더+`onerror` 폴백.
- 룩·토큰은 `reference/astrodeck-templates.md` 참조(primary #0066FF·Geist·shadcn, 라이트 기본).
- **채팅 출력은 짧게** — 파일 만들고 4줄 요약 + 한 줄 안내. 방법론 설명 금지.

## 전제
- `lean-canvas.md` + `key-copy.md` 읽기. 없으면 `/item-check`→`/key-copy` 먼저. 판정 ❌면 안 만듦.

## 만들 것 — 파일 4개
`landing-startup.html` / `landing-saas.html` / `landing-portfolio.html` / `landing-home.html`
- 구조: 참조자료의 템플릿별 섹션 순서.
- 내용: 캔버스→랜딩 매핑(UVP=히어로 헤드라인, Problem=문제섹션, Solution=기능, 기존대안=경쟁비교, Customer=타겟·얼리, Revenue=가격·CTA).
- 히어로 카피: 그 템플릿 톤에 맞는 **key-copy 변형**을 골라 넣어 4샘플이 카피도 조금씩 다르게.
- 미검증 수치·로고·후기는 `[플레이스홀더]`.
- AI 슬롭 금지(보라 그라데이션 남발·이모지 아이콘·의미없는 3카드·가짜 대시보드).

## 채팅 출력 형식 (짧게)
```
✅ 랜딩 4종 생성 (단일 HTML)
- landing-startup    Startup룩 — 경쟁비교·얼리어답터 (검증용 추천)
- landing-saas       SaaS룩 — 가격티어·FAQ
- landing-portfolio  Agency룩 — 목업·팀
- landing-home       기본룩 — 센터 히어로
→ 4개 열어보고 택1. 이미지·수치는 플레이스홀더(교체 필요).
```

## 다음
고른 1개 이미지 채우기 → (있으면) `landing-visuals`. 단일 HTML이라 어떤 정적 호스팅에도 바로 배포.
