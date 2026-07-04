# Tokyo Debunker — SSR 카드 랭킹 아카이브 (Darkwick Archive)

게임 *Tokyo Debunker* 의 **SSR 캐릭터 카드 147종**을 정리한 위키 + 랭킹 시스템입니다.
TU · MP · Speed 전투 메커니즘을 기반으로 각 카드를 정량 분석해 순위를 매깁니다.

**단일 HTML + 로컬 이미지**로 구성되어 있어 별도 빌드·서버 없이 그대로 열리며, GitHub Pages에 바로 배포됩니다.

## 기능

- **147개 SSR 카드** 그리드 — 티어 배지(S/A/B/C/D) + 랭크 점수 표시
- **필터**: 검색(카드명·캐릭터·스킬), 하우스(8개), 카드 타입 색상(Red/Green/Blue), 스킬 타입(P.ATK/S.ATK)
- **정렬**: 랭크 점수 / 속도 / 카드명 / 캐릭터
- **카드 상세**: `캐릭터: 카드명` 형식, 카드 타입, 스킬 타입, 유니크/액티브/패시브 스킬, 전투 판정 리드아웃(진입 지연·MP 게이지·행동 지연), 랭크 점수 분해
- **랭킹 가중치 슬라이더**: 공격 효율 / 순간 화력 / 진입 속도 / MP 경제 / 유틸리티 5축 실시간 조정

## 전투 판정 모델

- **진입 지연** = `ceil((Speed − 100) / 10)` — 낮을수록 먼저 행동
- **행동 지연** = `ceil((스킬 TU − 100) / 10)` — 스킬 사용 후 다음 행동까지 밀리는 정도
- **MP** = 5에서 시작, 0~10 범위(음수 불가), 스킬 사용 시 증감
- **광역(All) 스킬**은 3체 조우 기준으로 대상 수를 계산

랭크 점수는 5개 축(공격 효율·순간 화력·진입 속도·MP 경제·유틸리티)을 전체 카드 풀에서 0~100으로
정규화한 뒤 가중 평균한 값입니다. 가중치는 화면에서 즉시 조정 가능합니다.

## GitHub Pages 배포

1. 이 폴더 전체를 새 GitHub 레포지토리에 push 합니다 (`index.html`이 레포 루트에 오도록).
   ```bash
   git init
   git add .
   git commit -m "Tokyo Debunker SSR card archive"
   git branch -M main
   git remote add origin https://github.com/<사용자명>/<레포명>.git
   git push -u origin main
   ```
2. 레포 **Settings → Pages** 로 이동
3. **Source** 를 `Deploy from a branch`, **Branch** 를 `main` / `/ (root)` 로 설정 후 저장
4. 잠시 뒤 `https://<사용자명>.github.io/<레포명>/` 에서 공개됩니다

> `/docs` 폴더로 배포하려면 이 폴더의 파일들을 레포의 `docs/` 안에 넣고 Pages Source에서 `/docs` 를 선택하세요.

## 데이터 출처 및 참고

- 데이터는 Tokyo Debunker 커뮤니티 위키(Fandom, CC BY-SA)의 구조화 정보(스킬·TU·MP·Speed 등)를
  수집해 구성했습니다. 카드 표기는 `캐릭터: 카드명` 형식으로 재구성했습니다.
- 원본에 스탯이 비어 있는 일부 카드는 Speed를 중앙값으로 보정했으며, 상세 화면에 "추정"으로 표시됩니다.
- 이미지는 원본 위키 CDN의 핫링크 차단을 피하기 위해 로컬(`images/`)로 내려받아 560px 폭 WebP로 최적화했습니다.
- 랭크 점수는 위에 정의된 모델에 따른 추정치이며, 실제 게임 밸런스와 다를 수 있습니다.

## 파일 구조

```
.
├── index.html        # 앱 전체 (HTML + CSS + JS + 카드 데이터 인라인)
├── images/           # 147개 카드 이미지 (WebP)
├── .nojekyll         # GitHub Pages Jekyll 처리 비활성화
└── README.md
```
