# astrodeck 랜딩 4종 참조자료

출처: astrodeck (https://www.astrodeck.dev, **MIT License**). 아래 디자인토큰은 실제 빌드본 CSS에서 추출.
이 파일만으로 astrodeck 셋업 없이 단일 HTML로 룩을 재현할 수 있게 정리함.

## 디자인 토큰 (shadcn 스타일, 라이트 기본 + 다크 옵션)

```
--color-primary:        #0066FF   /* 브랜드/CTA. astrodeck 원본 #06f */
--font-sans:            "Geist", ui-sans-serif, system-ui, sans-serif   /* Geist 없으면 시스템 폴백 */
--font-mono:            "Geist Mono", ui-monospace, SFMono-Regular, Menlo, monospace

/* 라이트 */
--color-background:     oklch(100% 0 0)      /* ≈ #ffffff */
--color-foreground:     oklch(9.8% .0016 286.75)  /* near-black */
--color-card:           oklch(100% 0 0)
--color-muted:          oklch(96.1% .0011 286.75)  /* 연회색 배경 */
--color-muted-foreground: oklch(40% .0018 286.75)
--color-border:         oklch(91.4% .009 286.75)
--radius:               ~0.5rem (rounded-lg)

/* 다크 (옵션) */
--color-background:     oklch(9.8% .0016 286.75)
--color-foreground:     oklch(98% 0 0)
--color-border:         oklch(25% 0 0)
```
- 그림자는 약하게(shadcn 톤), 큰 헤드라인 + 타이트한 자간, 단색 위주. 과한 글로우/그라데이션 금지.
- Geist는 CDN 링크 대신 **시스템 폴백 스택**으로 두면 단일 HTML 자체완결 유지(폰트 완벽 재현이 필요하면 CDN 1줄 허용).

## 4종 섹션 구조 + 캔버스 매핑

### ① Startup / Product Launch  〔검증용 최적〕
gradient-glow hero → feature grid → **competitor comparison** → deep-dive content → **early adopter testimonials** → FAQ → CTA
- hero = UVP(키카피) / feature grid = Solution / competitor comparison = **기존 대안** / early adopter = **Customer(얼리어답터)** / FAQ·CTA = Revenue·Key Metrics
- 린캔버스와 거의 1:1 → 기본 추천.

### ② SaaS Landing  〔구독형 B2B〕
hero → logo cloud → features → stats → pricing tiers → testimonials → FAQ → CTA
- hero = UVP / features = Solution / pricing tiers = Revenue / logo·testimonials = 사회적 증거(플레이스홀더)

### ③ Portfolio / Agency  〔서비스·에이전시〕
split hero(+목업) → client logos → alternating content blocks → team profiles → testimonials → newsletter
- split hero = UVP+비주얼 / content blocks = Solution/Problem / team = 신뢰 / newsletter = CTA(신호)

### ④ Home  〔일반/기본〕
centered hero(+grid 패턴) → feature grid → showcase → pricing → testimonials → CTA
- 가장 범용. 성격이 안 잡히면 이걸로.

## 공통 규칙
- 전부 **단일 self-contained HTML**, 이미지=플레이스홀더+onerror 폴백.
- CTA는 캔버스 Key Metrics가 잡을 **진짜 커밋 신호**를 향하게(무료 가입 허영 금지).
- 미검증 수치·로고·후기는 `[플레이스홀더]` 표기(있는 척 금지).
