---
name: landing
description: 채운 린캔버스 + 키카피를 바탕으로 검증용 랜딩을 실제 astrodeck 레포(MIT)로 뽑는다. 레포 클론→데이터만 교체→빌드로 원본 룩 그대로. Startup·SaaS·Agency 3룩 제시(하나 안 고름). 채팅엔 프리뷰 주소 + 짧은 안내만. "랜딩 만들어줘", "샘플 페이지 뽑아줘" 류 요청에 사용. item-check·key-copy 다음 마지막 단계.
---

# landing — 실제 astrodeck 레포로 검증용 랜딩

## 규율 (겉으로 설명하지 말고 그냥 적용)
- **요약본을 손으로 재현하지 않는다.** 실제 astrodeck 레포를 클론(MIT)해서 **컴포넌트·스타일 그대로 두고 데이터만 교체** → 빌드. 원본 룩·다크모드·인터랙션 100% 유지.
- 3룩(Startup·SaaS·Agency) 각각 채워 제시. **하나 안 고른다**(고르는 건 사용자).
- 미검증 수치·후기·로고·가격·팀 = 전부 `[플레이스홀더]`. 있는 척 금지.
- **채팅 출력은 짧게** — 프리뷰 주소 표 + 한 줄 안내. 방법론 설명 금지.
- 상세 절차·컴포넌트 prop·함정은 `reference/astrodeck-repo.md` 참조(이게 메인).

## 전제
- `lean-canvas.md` + `key-copy.md` 읽기. 없으면 `/item-check`→`/key-copy` 먼저. 판정 ❌면 안 만듦.

## 순서
1. **캔버스+카피 읽기** → 룩별 히어로 카피(key-copy 변형)와 데이터 초안 준비.
2. **레포 준비** (`reference/astrodeck-repo.md` 셋업 블록 그대로):
   `git clone --depth 1 https://github.com/holger1411/astrodeck.git astrodeck` → `cd astrodeck` → `npm install`.
   (이미 `astrodeck/` 있으면 재사용.)
3. **데이터 교체** — `src/pages/templates/` 의 `startup.astro`·`saas.astro`·`portfolio.astro` 상단 JS 객체와 히어로/CTA 카피를 우리 내용으로. 컴포넌트·CSS는 손대지 않음.
   - 매핑·prop 치트시트는 참조파일 참고. 캔버스→데이터: UVP=Hero title/subtitle, Solution=features, 기존대안=Comparison, Problem=ContentBlock, Revenue=tiers, 얼리어답터=Testimonials, 신호=CTA label.
4. **빌드 & 프리뷰** — `npm run build` → `npm run preview`(백그라운드). 주소: `http://localhost:4321/templates/{startup|saas|portfolio}/`.
   - ⚠️ 빌드본은 절대경로라 file:// 직접 열기 X → 반드시 프리뷰 서버로.
5. 렌더 확인(우리 카피가 dist에 들어갔는지 grep) 후 채팅 출력.

## 채팅 출력 형식 (짧게)
```
✅ 실제 astrodeck 레포로 랜딩 3룩 생성 (데이터만 교체, 원본 룩 유지)
프리뷰 서버 실행 중:
- Startup (검증용 추천)  http://localhost:4321/templates/startup/
- SaaS                   http://localhost:4321/templates/saas/
- Agency                 http://localhost:4321/templates/portfolio/
→ 3개 열어보고 택1. 수치·후기·로고·가격은 [플레이스홀더](교체 필요).
참고: 헤더/푸터는 astrodeck 기본 브랜딩 — 실서비스면 로고/네비 정리 필요.
```

## 다음
고른 1룩 → 브랜딩(로고/네비/푸터) 정리 + 이미지·문구 다듬기 → (있으면) `landing-visuals`.
Astro 정적 빌드라 `dist/` 를 어떤 정적 호스팅에도 바로 배포.

## 폴백
네트워크/npm 불가 시에만: `reference/astrodeck-templates.md` 요약으로 단일 self-contained HTML 재현(구 방식, 룩 재현도).
