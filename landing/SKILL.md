---
name: landing
description: 채운 린캔버스 + 키카피를 바탕으로 검증용 랜딩을 우리 랜딩 베이스 레포(prevalidate-landing, astrodeck MIT 포크 — 신청폼·구글시트 연동 내장)로 뽑는다. 클론→데이터만 교체→빌드로 원본 룩 그대로. Startup·SaaS·Agency 중 목적에 맞는 1개를 골라 1장만 만든다(사용자 지정 가능). 채팅엔 프리뷰 주소 + 짧은 안내만. "랜딩 만들어줘", "샘플 페이지 뽑아줘" 류 요청에 사용. item-check·key-copy 다음 마지막 단계.
---

# landing — 우리 랜딩 베이스 레포로 검증용 랜딩

## 규율 (겉으로 설명하지 말고 그냥 적용)
- **요약본을 손으로 재현하지 않는다.** 우리 랜딩 베이스(`prevalidate-landing`, astrodeck MIT 포크)를 클론해 **컴포넌트·스타일 그대로 두고 데이터만 교체** → 빌드. **신청 폼·구글시트 연동이 이미 내장**(CTA는 전부 `#signup` 폼으로 연결됨).
- Startup·SaaS·Agency 중 **목적에 맞는 1개만** 골라 1장 만든다(3개가 비슷해 다 만들 필요 없음). 사용자가 지정하면 그걸로, 아니면 캔버스로 골라 **왜 골랐는지 한 줄** 밝힌다.
- 미검증 수치·후기·로고·가격·팀 = 전부 `[플레이스홀더]`. 있는 척 금지.
- **채팅 출력은 짧게** — 프리뷰 주소 표 + 한 줄 안내. 방법론 설명 금지.
- 상세 절차·컴포넌트 prop·함정은 `reference/astrodeck-repo.md` 참조(이게 메인).

## 전제 (어느 아이디어인지 먼저)
- `ideas/<slug>/lean-canvas.md` + `ideas/<slug>/key-copy.md` 를 읽는다. slug는 인자로 주면 그걸, 없으면 **가장 최근 수정된 `ideas/*/lean-canvas.md`**. 여러 개고 애매하면 물어본다.
- `ideas/`·`prevalidate-landing/`는 **사용자 작업 폴더(cwd)** 기준. `pwd`로 확인 — cwd가 `.claude/skills` 안이면 스킬 폴더이니 거기 쓰지 말고 프로젝트 경로를 물어라. **스킬 폴더 안에 클론·산출물을 만들지 않는다.**
- 없으면 `/item-check`→`/key-copy` 먼저.
- 판정 **❌면 기본은 안 만든다.** 단 ❌ 사유가 "수요 미검증"이고 사용자가 **가짜문(신청 측정)** 목적이면, CTA를 커밋형(예: "먼저 써보기 신청"/"도입 상담 신청")으로 두고 "수요 측정용"임을 명시하고 만든다.

## 템플릿 선택 (캔버스로 1개만)
- **Startup** 〔기본·검증용〕 — 신규 아이템 첫 검증. 경쟁비교+얼리어답터가 캔버스와 1:1. **애매하면 이걸로.**
- **SaaS** — Revenue가 구독 **가격 티어** 중심 + 기능/가격 비교가 핵심 셀링인 경우.
- **Agency(portfolio)** — 서비스·에이전시·수주형(프로젝트 기반), 팀·클라이언트가 신뢰 요소인 경우.

## 순서
1. **캔버스+카피 읽기 + 템플릿 1개 + 히어로 키카피 1개 선택**
   - 룩: 위 기준으로 하나 결정(사용자 지정 우선).
   - **히어로 카피(=랜딩 메인 하이라이트)**: `key-copy.md` N개 중 **정확히 1개**를 골라 **Hero title**(가장 큰 헤드라인)로 쓴다. 사용자가 번호 지정 시 그것, 아니면 **고른 룩에 맞는 스타일**을 자동 선택(예: SaaS→간결·스펙형, Startup→문제 직격). subtitle은 UVP 보조 문구 + `<mark>`로 핵심구 강조.
   - **룩·카피 왜 골랐는지 한 줄** 준비(둘 다 나중에 밝힘).
2. **레포 준비 (캐시 재사용)** — cwd에서: `prevalidate-landing/` 있으면 **clone 생략**, `node_modules` 있으면 **install 생략**. 최초만 clone+install, 이후엔 빌드만(수 초).
   `[ -d prevalidate-landing ] || git clone --depth 1 https://github.com/hyeongkeunpark-bit/prevalidate-landing.git` → `cd prevalidate-landing` → `[ -d node_modules ] || npm install`.
3. **데이터 교체 (고른 1개만)** — `src/pages/templates/<선택>.astro` 상단 JS 객체와 히어로/CTA 카피를 우리 내용으로. 컴포넌트·CSS는 안 건드림. **나머지 2개 템플릿·신청 폼(Signup)은 손대지 않는다**(CTA는 이미 `#signup`로 연결됨).
   - 매핑·prop 치트시트는 참조파일. **Hero title = 선택한 키카피**(지정/자동), subtitle = UVP 보조 문구. Solution=features, 기존대안=Comparison, Problem=ContentBlock, Revenue=tiers, 얼리어답터=Testimonials.
   - **CTA 라벨** (hero primaryCta · 최종 CTA · `<Signup title=… buttonText=… />` 를 **일치**시킴): 아이템에 맞게 — **B2B·영업형 → "도입 상담 신청"**, **셀프서브 제품 → "먼저 써보기 신청"**. 약한 "문의하기/신청하기" 단독은 쓰지 말 것.
3b. **브랜딩 정리 (서비스명 자동 확정)** — 캔버스에 브랜드명 있으면 그것, **없으면 컨셉에서 짧은 임시 서비스명 1개를 생성**(예: 재방문 알림→"펫리마인드"). 그 이름으로 **`[서비스명]`·"AstroDeck" 을 전부 치환**(Logo·Footer·`<title>`·CTA 카피 등 모든 위치 — 남기지 말 것). 네비는 랜딩 앵커로. (헤더 GitHub 버튼은 포크에서 이미 제거됨.) **생성한 이름은 출력에서 밝힘.**
3c. **신청 저장 연결** — 사용자에게 구글 Apps Script 웹앱 URL을 묻는다. 있으면 `.env` 에 `PUBLIC_SIGNUP_ENDPOINT=<URL>` 기록. 없으면 `google-sheet/SETUP.md`(5분 세팅) 안내 후 그대로 진행 — 폼은 동작하되 저장 안 됨.
4. **빌드 & 프리뷰** — `npm run build` → `npm run preview`(백그라운드). 주소: `http://localhost:4321/templates/<선택>/`.
   - ⚠️ 빌드본은 절대경로라 file:// 직접 열기 X → 반드시 프리뷰 서버로.
5. 렌더 확인(우리 카피가 dist에 들어갔는지 grep). 빌드본 `dist/templates/<선택>/` 을
   `ideas/<slug>/landing/` 으로 복사해 보존. 그 후 채팅 출력.

## 채팅 출력 형식 (짧게)
```
✅ <선택>룩으로 검증용 랜딩 생성 (데이터만 교체, 원본 룩 유지)
프리뷰: http://localhost:4321/templates/<선택>/
왜 이 룩: <한 줄 이유>
서비스명: <생성/사용한 이름>  (바꾸려면 말하세요)
히어로 카피: #<N> <스타일>  (다른 카피로 바꾸려면 번호만 말하세요)
CTA: <라벨>
신청 저장: #signup 폼 → 구글시트  [연결됨 / 미설정 시 google-sheet/SETUP.md 5분]
→ 수치·후기·로고·가격은 [플레이스홀더](교체 필요). 다른 룩 원하면 말해주세요.
```

## 다음
고른 1룩 → 실로고·이미지·문구 다듬기 → (있으면) `landing-visuals`.
Astro 정적 빌드라 `dist/` 를 어떤 정적 호스팅에도 바로 배포.

## 폴백
네트워크/npm 불가 시에만: `reference/astrodeck-templates.md` 요약으로 단일 self-contained HTML 재현(구 방식, 룩 재현도).
