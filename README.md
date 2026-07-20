# Dener 온보딩 가이드 (랜딩페이지)

코인이 처음인 유저도 따라 할 수 있는 **Dener·총판 참여 매뉴얼** 랜딩페이지입니다.
거래소 가입 → MetaMask → .dex 도메인 구입 → 대표 도메인 등록 → MOL 구입·서임 → 총판(선택)의 6단계로 구성되어 있습니다.

## 파일 구성

| 파일 | 설명 |
|---|---|
| `dener-onboarding.html` | 문서형 랜딩페이지 (단일 파일, 외부 의존성 없음) |
| `dener-chat-guide.html` | 대화형(스토리 모드) 가이드 — 질문에 답하며 분기별로 안내받는 챗봇 형식 |
| `dener-onboarding.en.html` / `.ja.html` / `.zh-Hant.html` | 문서형 랜딩페이지 **영문 / 일본어 / 번체중문판** |
| `dener-chat-guide.en.html` / `.ja.html` / `.zh-Hant.html` | 대화형 가이드 **영문 / 일본어 / 번체중문판** |
| `README.md` | 이 문서 |

두 페이지는 서로 링크되어 있습니다(문서형 히어로의 "대화형 가이드로 시작" ↔ 대화형 상단의 "문서형 가이드"). 함께 배포하세요.

## 다국어판 관리 (EN / 日本語 / 繁體中文)

- **한국어가 원본이고 나머지는 번역본**입니다. 각 번역판 푸터에 "두 버전이 다르면 한국어판이 우선한다"를 명시했으므로 삭제하지 마세요.
- **언어 전환**: 8개 페이지 모두 `🌐` 드롭다운(`details.langmenu`)으로 4개 언어를 오갑니다. 문서형은 내비게이션 우측, 대화형은 헤더 버튼 줄에 있습니다. `<link rel="alternate" hreflang>`도 4개 언어 전부 설정되어 있습니다.
  - 문서형의 드롭다운은 `.nav-in`의 `overflow-x:auto`에 잘리므로 **`<nav>` 직속 자식**으로 두고 `position:absolute`로 배치했습니다. `.nav-in` 안으로 옮기지 마세요.
  - 언어를 추가하면 8개 파일의 `.langlist` 목록과 `hreflang` 블록을 **모두** 갱신해야 합니다.
- **내용을 수정하면 4개 언어 파일을 모두 고쳐야 합니다.** 특히 수치(2,000만/3,000만 MOL, $620/$930, 기준가)는 반드시 함께 맞추세요.
- **대화형 가이드의 `FLOW` 객체**는 4개 언어가 동일한 26개 노드·동일한 분기 구조를 유지합니다. 번역 시 노드 키와 선택지의 이동 대상 id는 절대 바꾸지 마세요. 검증용 스크립트:
  ```
  node -e 'const fs=require("fs");function flow(f){const m=fs.readFileSync(f,"utf8").match(/const FLOW = (\{[\s\S]*?\n\};)/);return eval("("+m[1].slice(0,-1)+")")}
  const en=flow("dener-chat-guide.en.html");for(const f of ["dener-chat-guide.html","dener-chat-guide.ja.html","dener-chat-guide.zh-Hant.html"]){const t=flow(f);
  console.log(f, JSON.stringify(Object.keys(en))===JSON.stringify(Object.keys(t))?"OK":"불일치")}'
  ```
- **참고 자료 모음**: 번역판은 한국어 블로그·유튜브를 제외하고 공식 영문 문서(MetaMask, Chainlist, Ledger)만 남겼습니다. 한국 거래소·트래블룰 자료는 `한국어` 태그를 달아 최소한만 유지하고, 전체 목록은 한국어 페이지로 링크합니다.
- **영상**: 6편 모두 한국어 음성입니다. 번역판에서는 각 영상 아래에 "음성은 한국어" 안내와 해당 언어 요약(기본 펼침)을 제공합니다.
- **중국어는 번체(zh-Hant) 단독**입니다. 대만·홍콩 독자 기준이며, 중국 본토는 가상자산 홍보가 금지되어 있어 간체판은 의도적으로 만들지 않았습니다. 간체 요구가 오면 규제 검토를 먼저 하세요.
- **`.gitignore`는 화이트리스트 방식**입니다. 새 파일을 추가하면 `!파일명`을 등록해야 배포됩니다.

## 배포 방법 (GitHub Pages)

1. 이 저장소에서 `dener-onboarding.html`을 `index.html`로 이름 변경(또는 복사)
2. GitHub 저장소 → **Settings → Pages** → Source를 `main` 브랜치 `/ (root)`로 설정
3. 몇 분 후 `https://<계정명>.github.io/<저장소명>/` 에서 접속 가능

커스텀 도메인을 쓰려면 Pages 설정의 Custom domain에 입력하고 DNS(CNAME)를 연결하세요.

## 영상 추가 방법

각 단계에는 16:9 영상 슬롯이 있습니다. 영상을 유튜브에 업로드한 뒤, HTML에서 해당 단계의 `video-box`에 영상 ID만 넣으면 자동으로 플레이어로 전환됩니다.

```html
<!-- 변경 전 -->
<div class="video-box" data-video-id="">
<!-- 변경 후 (예: https://youtu.be/AbCdEf12345) -->
<div class="video-box" data-video-id="AbCdEf12345">
```

각 슬롯 아래 접이식 **"영상 제작 가이드(촬영 콘티)"**에 녹화할 화면 순서·러닝타임·모자이크 포인트가 정리되어 있습니다.

## 참고 자료(외부 링크) 관리 정책

- STEP 1·2의 "참고 자료 모음"은 **2026년 7월 조사 기준**으로 선별한 외부 블로그·유튜브·공식 가이드입니다.
- 외부 콘텐츠는 게시자 사정으로 변경·삭제될 수 있으므로 **분기 1회 링크 점검**을 권장합니다.
- 거래소 절차(가입·계좌 연결·트래블룰)는 수시로 바뀝니다. 외부 자료와 실제 화면이 다르면 **각 거래소 공식 고객센터가 우선**입니다.
- 링크 추가 기준: ① 공식 문서 우선 ② 스크린샷/단계 구분이 명확한 것 ③ 최신 UI 기준.

## 용어(표현) 정책 — 법적 리스크 예방

페이지 전반에 다음 완곡 표현 원칙을 적용했습니다. 수정·추가 시에도 유지하세요.

| 피해야 할 표현 | 사용 표현 |
|---|---|
| 코인 구입/구매 | MOL 스왑, 생태계 참여 |
| 투자, 초기 자금 | 참여 준비 규모, 본드 규모 |
| 수익, 수당 | 리워드, 보상 |
| 원금 회수, 손익분기 | 참여 규모 상당의 리워드 누적 (예시·보장 아님 병기) |
| 매출 | 참여 금액, 스왑 금액 |
| 가격 | 교환 비율, 기준가 |

추가 금지 표현(앱 심사·금융규제 관점): APR·APY·이자·배당·Yield·Staking·예치·Investment·Passive Income·Earn BNB.

**다국어 표현 대응표** — 직역하면 금융상품 뉘앙스가 강해지는 단어가 있어 아래 표기를 사용합니다.

| 한국어 | English | 日本語 | 繁體中文 | 쓰면 안 되는 표현 |
|---|---|---|---|---|
| 본드 (PV) | committed MOL (PV) | コミット済みMOL（PV） | 承諾持有的 MOL（PV） | bond, 債券, 質押 |
| 코인 구입 | swap / participate in the ecosystem | MOLスワップ / エコシステムへの参加 | MOL 兌換 / 參與生態系 | buy, 購入, 購買, invest |
| 참여 준비 규모 | participation setup size | 参加準備規模 | 參與準備規模 | investment, 投資額, 本金, 元本 |
| 리워드 | rewards | リワード | 獎勵 | earnings, 収益, 収益率, 分紅, 利潤 |
| 기준가 / 교환 비율 | reference rate / exchange ratio | 基準レート / 交換比率 | 基準匯率 / 兌換比率 | price, 価格, 價格, 行情 |
| 서임 | designation | 叙任 | 敘任 | — |
| 총판 | evangelist | エバンジェリスト | 佈道者 | distributor, 代理店, 經銷商, 代理商 |

공통 금지어: APR · APY · 이자(利息) · 배당(配当/分紅) · Yield(利回り/收益率/年化) · Staking(ステーキング/質押) · 예치(預入/存入) · Passive Income(不労所得/被動收入) · 理財

수치 예시에는 각 언어로 보장 부인을 반드시 병기하세요 — EN `an example, not a guarantee` / JA `例であり、保証されるものではありません` / ZH `僅為示例，不構成任何保證`.

**예외 — 면책 문구**: 푸터 면책 조항에서는 `투자/investment/投資` 를 **부정문으로** 반드시 사용합니다(「투자 권유가 아닙니다」/「not investment advice」/「投資を勧誘するものではありません」/「並不構成投資建議」). 이 단어를 피하면 면책의 법적 효력이 약해집니다. 본문 홍보 문구에서만 금지입니다.
수치 예시에는 반드시 "예시이며 보장되지 않음"을 병기하고, 푸터의 면책 문구를 삭제하지 마세요.

## 배포 전 확인 사항

- [x] MOL 고정가 확정값 반영 — **$0.000036 확정** (2026-07-21). 파생 달러 수치 전부 재계산 완료: 본드 $720/$1,080, 추가 $360, 1대 예시 $7,200, 준비 규모 $750~900 / $1,100~1,300. 4개 언어 8개 파일 동기화됨. 값 재변경 시 8개 파일을 함께 고칠 것.
- [ ] .dex 도메인 등록비 실제 금액 확인 후 STEP 3에 명시
- [ ] 거래소별 BNB·POL 지원 및 개인지갑(트래블룰) 정책 최신화
- [ ] 영상 6편 제작·업로드 후 `data-video-id` 입력
- [ ] 총판 등록 문의 채널(punditcode@gmail.com) 유효성 확인

## 면책

본 페이지의 모든 정보는 참고용이며 투자 권유가 아닙니다. 정책·가격·절차는 변경될 수 있으며, 실제 서비스 화면의 표시값이 우선합니다.

## 관련 링크

[dexignation.com/ko](https://dexignation.com/ko) · [digmol.com](https://digmol.com) · [docs.dexignation.com](https://docs.dexignation.com) · [github.com/DEXignation](https://github.com/DEXignation) · [github.com/molepin](https://github.com/molepin)
