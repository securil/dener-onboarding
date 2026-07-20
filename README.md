# Dener 온보딩 가이드 (랜딩페이지)

코인이 처음인 유저도 따라 할 수 있는 **Dener·총판 참여 매뉴얼** 랜딩페이지입니다.
거래소 가입 → MetaMask → .dex 도메인 구입 → 대표 도메인 등록 → MOL 구입·서임 → 총판(선택)의 6단계로 구성되어 있습니다.

## 파일 구성

| 파일 | 설명 |
|---|---|
| `dener-onboarding.html` | 문서형 랜딩페이지 (단일 파일, 외부 의존성 없음) |
| `dener-chat-guide.html` | 대화형(스토리 모드) 가이드 — 질문에 답하며 분기별로 안내받는 챗봇 형식 |
| `dener-onboarding.en.html` | 문서형 랜딩페이지 **영문판** |
| `dener-chat-guide.en.html` | 대화형 가이드 **영문판** |
| `README.md` | 이 문서 |

두 페이지는 서로 링크되어 있습니다(문서형 히어로의 "대화형 가이드로 시작" ↔ 대화형 상단의 "문서형 가이드"). 함께 배포하세요.

## 영문판(English version) 관리

- **한국어가 원본이고 영문은 번역본**입니다. 영문 푸터에 "if the two differ, the Korean version governs"를 명시했으므로 삭제하지 마세요.
- **언어 전환**: 문서형은 상단 내비게이션 우측의 `한국어 / EN` 토글, 대화형은 헤더의 `EN` / `한국어` 버튼으로 이동합니다. `<link rel="alternate" hreflang>`도 양쪽에 설정되어 있습니다.
- **내용을 수정하면 한국어·영문 두 파일을 모두 고쳐야 합니다.** 특히 수치(2,000만/3,000만 MOL, $620/$930, 기준가)는 반드시 함께 맞추세요.
- **참고 자료 모음**: 영문판은 한국어 블로그·유튜브를 제외하고 공식 영문 문서(MetaMask, Chainlist, Ledger)만 남겼습니다. 한국 거래소·트래블룰 자료는 `한국어` 태그를 달아 최소한만 유지하고, 전체 목록은 한국어 페이지로 링크합니다.
- **영상**: 6편 모두 한국어 음성입니다. 영문판에서는 각 영상 아래에 `🔊 Narration is in Korean` 안내와 영문 요약(기본 펼침)을 제공합니다.
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

**영문판 표현 대응표** — 영어에서는 일부 단어가 한국어보다 강한 금융상품 뉘앙스를 가지므로 아래 표기를 사용합니다.

| 한국어 | 영문 표기 | 사용하면 안 되는 영문 |
|---|---|---|
| 본드 (PV) | committed MOL (PV) | bond (채권으로 읽힘) |
| 코인 구입 | swap, join / participate in the ecosystem | buy, invest, purchase coins |
| 참여 준비 규모 | participation setup size | investment, capital, funds |
| 리워드 | rewards | earnings, income, returns, yield |
| 기준가 / 교환 비율 | reference rate / exchange ratio | price, valuation |
| 서임 | designation | — |
| 총판 | evangelist | distributor (판매 대리점으로 읽힘) |

수치 예시에는 영문에서도 "an example, not a guarantee"를 반드시 병기하세요.
수치 예시에는 반드시 "예시이며 보장되지 않음"을 병기하고, 푸터의 면책 문구를 삭제하지 마세요.

## 배포 전 확인 사항

- [ ] MOL 고정가 확정값 반영 (내부 문서 간 $0.000031 / $0.000036 불일치)
- [ ] .dex 도메인 등록비 실제 금액 확인 후 STEP 3에 명시
- [ ] 거래소별 BNB·POL 지원 및 개인지갑(트래블룰) 정책 최신화
- [ ] 영상 6편 제작·업로드 후 `data-video-id` 입력
- [ ] 총판 등록 문의 채널(punditcode@gmail.com) 유효성 확인

## 면책

본 페이지의 모든 정보는 참고용이며 투자 권유가 아닙니다. 정책·가격·절차는 변경될 수 있으며, 실제 서비스 화면의 표시값이 우선합니다.

## 관련 링크

[dexignation.com/ko](https://dexignation.com/ko) · [digmol.com](https://digmol.com) · [docs.dexignation.com](https://docs.dexignation.com) · [github.com/DEXignation](https://github.com/DEXignation) · [github.com/molepin](https://github.com/molepin)
