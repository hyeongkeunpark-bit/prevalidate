# prevalidate

> **만들기 전에 아이템부터 점검**하는 Claude Code 스킬 묶음.
> 린캔버스(Lean Canvas)로 아이템이 **랜딩으로 검증 착수할 준비가 됐는지** 판정하고, 그 캔버스에서 테스트할 **키카피 N개**를 뽑아준다.

## 왜 만들었나
한 팀이 린캔버스의 **수요 칸을 '가상 사례'로 채워놓고** "다 채웠으니 검증됐다"고 착각한 채
랜딩페이지를 **12개** 만들었다. 그 수요 사례는 나중에 **가상 예시**로 판명됐고, 2개월이 날아갔다.
→ **칸을 다 채움 = "검증 완료"가 아니라 "랜딩으로 검증 착수할 준비 됨"** 임을 규율로 박제.

## 방법론
- **Lean Canvas (Ash Maurya)** — 정해진 9칸을 채운다. 빈 칸 = 부족한 점.
- **안전핀**: 수요 직결 4칸(Problem·Customer·UVP·Unfair Advantage)은 **[근거 있음 / 아직 가정]** 태그.
  가정만으로 채운 건 검증된 게 아니다 — 랜딩으로 확인할 대상.
- **The Mom Test · RAT** — 별도 프로세스가 아니라 **칸을 채우는 도구**로만 스며든다.
  (근거 만들 땐 Mom Test식 과거 행동 질문 / 어느 빈칸부터는 RAT = 가장 위험한 칸 먼저)

## 스킬 2개

| 순서 | 스킬 | 하는 일 |
|---|---|---|
| ① | **item-check** | 린캔버스 9칸 채우기 → 빈 칸=갭 코칭 → **착수 준비 완료 / 조건부 / 아직 이르다** 판정. 수요 칸 근거 태그 |
| ② | **key-copy** | 채운 캔버스의 **UVP·Problem 칸**에서 키카피 **N개**(기본 5). 앵글별 변형 |

흐름:
```
아이디어
 └─ /item-check → lean-canvas.md  (9칸 채움? 빈칸=갭. 착수 준비 판정)
      └─ (준비됨) /key-copy → key-copy.md  (UVP·Problem 기반 키카피 N개)
           └─ fast-landing-validator 로 랜딩 제작  ← lean-canvas.md 그대로 입력
```

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

## Companion 스킬 (독립 스킬 — 별도 설치, 있으면 자동 재사용)
카피 크래프트는 검증된 범용 스킬에 **위임**한다(중복 구현 안 함):
- **`premium-marketing`** — 앵커링·넛지·상욕방보 등 전환/가격 카피. `key-copy`가 활용.
- **`brand-story`** — 정체성/서사 앵글. `key-copy`가 활용.

> 없어도 이 플러그인 2개만으로 단독 동작. companion은 품질 부스터.

## 설치
```bash
# 플러그인으로
git clone https://github.com/hyeongkeunpark-bit/prevalidate
claude --plugin-dir ./prevalidate
# 또는 스킬만 낱개로
cp -r prevalidate/skills/* ~/.claude/skills/
```

## 라이선스
[MIT](LICENSE) — 자유롭게 사용·수정·재배포 가능.
