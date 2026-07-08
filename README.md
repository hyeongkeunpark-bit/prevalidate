# prevalidate

> **만들기 전에 아이템부터 점검**하는 Claude Code **스킬 2개**.
> 린캔버스(Lean Canvas)로 아이템이 **랜딩으로 검증 착수할 준비가 됐는지** 판정하고,
> 그 캔버스에서 테스트할 **키카피 N개**를 뽑아준다.
>
> 플러그인 아님 — 그냥 스킬 폴더 두 개. `~/.claude/skills/`에 복사하면 끝.

## 왜 만들었나
한 팀이 린캔버스의 **수요 칸을 '가상 사례'로 채워놓고** "다 채웠으니 검증됐다"고 착각한 채
랜딩페이지를 **12개** 만들었다. 그 수요 사례는 나중에 **가상 예시**로 판명됐고, 2개월이 날아갔다.
→ **칸을 다 채움 = "검증 완료"가 아니라 "랜딩으로 검증 착수할 준비 됨"** 임을 규율로 박제.

## 설치 (마켓·install 없음)
```bash
git clone https://github.com/hyeongkeunpark-bit/prevalidate
cp -r prevalidate/item-check prevalidate/key-copy prevalidate/landing ~/.claude/skills/
```
다음 세션부터 `/item-check`, `/key-copy`, `/landing` 으로 바로 사용.

## 스킬 3개

| 순서 | 스킬 | 하는 일 |
|---|---|---|
| ① | **item-check** | 린캔버스 9칸을 **표**로 채우기 → 빈 칸=갭 코칭 → **착수 준비 완료 / 조건부 / 아직 이르다** 판정. 칸마다 **내가 초안 낼 것 🤖 / 당신이 리서치할 것 🙋**(경쟁사 등)을 구분 — 모르는 건 지어내지 않고 짧은 리서치 힌트. 수요 칸 근거 태그 |
| ② | **key-copy** | 채운 캔버스(내용) × **레퍼런스 사이트별 보이스**(스타일)로 키카피 **N개**(기본 5). 캔버스가 갱신되면 다시 돌려 최신화 |
| ③ | **landing** | 캔버스+카피 → **실제 astrodeck 레포(MIT) 클론 → 데이터만 교체 → 빌드**로 랜딩 3룩(Startup·SaaS·Agency) 제시. 원본 룩·다크모드·인터랙션 그대로. 하나 고르지 않음 |

흐름 (한 루프로 돎):
```
아이디어
 └─ /item-check <아이템> → ideas/<slug>/lean-canvas.md  ←──┐ 표 채울 때마다
      └─ (준비됨) /key-copy <slug> → ideas/<slug>/key-copy.md ┘ 다시 돌려 카피 최신화
           └─ /landing <slug> → astrodeck 클론→데이터 교체→빌드→프리뷰 (+ ideas/<slug>/landing/)
```
> **아이디어별 폴더 `ideas/<slug>/`** 에 저장 — 여러 아이디어를 나란히 두고 비교. slug는 item-check가 정하고, 이후 스킬은 인자로 받거나 가장 최근 것을 이어받는다. (고정 파일명으로 덮어쓰지 않음)
> ③ landing은 실제 astrodeck 레포(MIT)를 클론해 **컴포넌트·스타일은 그대로 두고 데이터만 교체**한 뒤 `npm run build`→`preview`로 확인한다(원본 룩 100% 유지). 절차·컴포넌트 prop·함정은 `landing/reference/astrodeck-repo.md`에 박제. 네트워크/npm 불가 시엔 `astrodeck-templates.md` 요약으로 단일 HTML 재현(폴백).
- **item-check**: 경쟁사·차별점처럼 내가 모르는 니치 사실은 **지어내지 않고** "가서 이걸 확인하라" 힌트만.
- **key-copy**: "실제 사이트 4개 주고 우리 기획에 맞춰 새로 써줘 → 스타일 다양한 카피가 나와 좋았다"는 경험을 스킬화. 레퍼런스 사이트 N개의 보이스를 추출해 우리 메시지를 각 보이스로.

## 방법론
- **Lean Canvas (Ash Maurya)** — 정해진 9칸을 채운다. 빈 칸 = 부족한 점.
- **안전핀**: 수요 직결 칸(Problem·기존대안·Customer·UVP·Unfair Advantage)은 **[근거 있음 / 아직 가정]** 태그.
- **The Mom Test · RAT** — 별도 프로세스가 아니라 **칸을 채우는 도구**로만 스며든다.

## 캔버스 → 랜딩 매핑
| 캔버스 칸 | 랜딩 요소 |
|---|---|
| UVP + 하이레벨 컨셉 | Hero 헤드라인 = **키카피** |
| Problem + 기존 대안 | 문제 제기 섹션 |
| Solution | 작동 방식 / 쇼케이스 |
| Customer + 얼리어답터 | 타겟·톤 |
| Revenue | 가격·오퍼·CTA |
| Unfair Advantage | 차별점 배지 |
| Key Metrics | CTA가 잡을 검증 신호 |

## Companion 스킬 (별도 설치, 있으면 자동 재사용)
카피 크래프트는 검증된 범용 스킬에 **위임**한다(중복 구현 안 함):
- **`premium-marketing`** — 앵커링·넛지·상욕방보 등 전환/가격 카피. `key-copy`가 활용.
- **`brand-story`** — 정체성/서사 보이스. `key-copy`가 활용.

> 없어도 이 스킬 2개만으로 단독 동작. companion은 품질 부스터.

## 라이선스
[MIT](LICENSE) — 자유롭게 사용·수정·재배포 가능.
