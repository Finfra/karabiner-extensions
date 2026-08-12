---
name: README
description: "Karabiner-Elements complex_modifications 규칙 5종 — 공개 진입점"
date: 2026.08.09
---
[![en](https://img.shields.io/badge/lang-en-blue.svg)](README_en.md)

# Karabiner-Elements Extensions

macOS 키보드 커스터마이저 [Karabiner-Elements](https://karabiner-elements.pqrs.org/) 의 `complex_modifications` 규칙 다섯 개다. 규칙마다 폴더 하나를 쓰고, 그 안에 **바로 쓸 수 있는 JSON**(`rule.json`)과 **무엇을 하는 규칙인지 설명하는 문서**가 함께 있다.

10년 넘게 개인 환경에서 굴려 온 것들이라 만듦새가 고르지 않다. 둘은 그대로 가져다 쓸 수 있는 순수 키 리매핑이고, 나머지 셋은 특정 하드웨어나 외부 앱을 전제한다 — **어느 쪽인지 표에 먼저 적었다.** 조건을 안 갖춘 규칙은 설치해도 조용히 아무 일도 하지 않는데, 그건 고장과 구분이 안 되기 때문이다.

# 규칙 5종

| 규칙 | 무엇을 하나 | 필요한 것 |
| :--- | :--- | :--- |
| [RemoteDesktop](remoteDesktop/README.md) | MS 원격 데스크톱이 앞에 있을 때만 `alt` ↔ `command` 를 맞바꾼다 | **없음** — 순수 키 리매핑 |
| [EngCharOnKor](engCharOnKor/README.md) | 한글 입력 상태에서 `Insert` 를 **누르고 있는 동안만** 영문이 나온다. 입력기를 전환하지 않는다 | `insert` 를 내보내는 키 · 한글 IME |
| [FootPedal](footPedal/README.md) | USB 3페달 풋스위치 — 편집·탐색·미디어 3계층 × 모디파이어 6층 | 3페달 USB 풋스위치 |
| [NowageShorthand (n3sh)](n3sh/README.md) | 세벌식 390 속기 — 자모 조합을 완성형 단어·구로 펼친다 <br>📖 [문서 사이트](https://finfra.github.io/karabiner-extensions/) | 한글 IME · 세벌식 390 배열 |
| [12Key2Knob](12Key2Knob/README.md) | 12키+2노브 매크로패드를 Keyboard Maestro 매크로 트리거로 쓴다 | 그 매크로패드 **+ 직접 만든 매크로 62종** ⚠️ |

## 처음이라면

**[RemoteDesktop](remoteDesktop/README.md)** 이 가장 짧고 조건이 없다. Karabiner 규칙이 어떻게 생겼는지 보기에 좋다.

**[EngCharOnKor](engCharOnKor/README.md)** 는 한글을 쓰는 사람에게 실익이 크다. 한/영 전환 없이 잠깐 영문을 치는 동작인데, 입력기를 바꾸지 않으므로 **전환 단축키가 무엇이든 무관**하다.

**[n3sh](https://finfra.github.io/karabiner-extensions/)** 는 셋 중 유일하게 **배워야** 쓸 수 있다 — 254 규칙이라 설치해서 바로 되는 분량이 아니다. 그래서 문서 사이트를 따로 두었고, 설치 파일도 거기서 받는다. 세벌식 390 배열을 쓰지 않는다면 해당 없다.

# 설치

1. Karabiner-Elements → **Complex Modifications → Add rule**
2. 또는 `rule.json` 을 `~/.config/karabiner/assets/complex_modifications/` 에 넣고 UI 에서 활성화
3. 목록에 안 보이면 Karabiner-Elements 재시작

⚠️ **장치 전용 규칙은 그 장치가 연결돼야 반응한다.** `vendor_id`/`product_id` 로 매칭하므로, 장치가 없으면 규칙이 켜져 있어도 아무 일도 일어나지 않는다 — 설치 실패와 똑같아 보인다.

# 무엇이 들어 있고 무엇이 없나

| 있다 | 없다 |
| :--- | :--- |
| `rule.json` — 실제로 올라가는 규칙 | n3sh 를 생성하는 빌드 도구 |
| `info.md` — 설명·유래 | 12Key2Knob 의 Keyboard Maestro 매크로 |
| `README.md` — 규칙별 진입점 | 라이브 설정 백업·대조 스냅샷 |
| n3sh 의 규칙표(`layout/`)·생성 데이터(`core/`)·서술(`_doc/`) | 개인 경로가 담긴 것 일체 |

⚠️ **12Key2Knob 은 그대로는 동작하지 않는다.** manipulator 가 하는 일이 Keyboard Maestro 에 **매크로 이름을 넘기는 것**뿐이고, 매크로 본체는 개인 작업 흐름에 밀착돼 있어 공개하지 않았다. 쓰려면 같은 이름의 매크로 62종을 직접 만들어야 한다 — 이름 목록과 주의점은 [그 README](12Key2Knob/README.md) 에 있다.

# pqrs 공개 등록

공식 규칙 저장소 [ke-complex-modifications.pqrs.org](https://ke-complex-modifications.pqrs.org/) 는 **규칙 1건 단위**로 등록받는다. 다섯을 한자리에 모아 보여 줄 곳이 없어서 이 저장소가 있다.

| 규칙 | 등록 상태 |
| :--- | :--- |
| FootPedal | ✅ 등록됨 — *USB Foot Pedal (3 pedals)*, PR [#1982](https://github.com/pqrs-org/KE-complex_modifications/pull/1982) |
| EngCharOnKor | 🚧 제출본 준비 완료, PR 예정 |
| 12Key2Knob | ⏸️ 미룸 — 매크로 없이는 남의 환경에서 동작하지 않는다 |
| RemoteDesktop | ⏸️ 미룸 — `alt`↔`command` 스왑은 이미 여럿 등록돼 있다 |
| n3sh | 🚧 제출 예정 — 이 저장소의 문서가 서면서 가능해졌다(2026-08-10 전환). **390 판만** 낸다 |

* n3sh 의 **최종식(final) 배열**은 위 표에 없다 — 390 제출 후 **쓰겠다는 요청이 있을 때만** 별도 프로젝트로 독립시켜 공개한다. 쓰는 사람이 확인되지 않은 배열을 먼저 내지 않는다

# 폴더 구조

```
.
├── README.md · README_en.md   # 이 문서
└── {코드명}/
    ├── README.md              # 규칙 진입점 — 개요·파일 위치·상태
    ├── info.md                # 설명과 유래
    ├── rule.json              # 올리는 규칙
    └── layout/ core/ _doc/    # 규칙 전용 자산 (n3sh 만 해당)
```

폴더명은 규칙 코드명 그대로다. `12Key2Knob` 이 숫자로 시작하는 건 정렬 번호가 아니라 **장치 이름 자체**여서다.

# 이 저장소에 대해

정본은 비공개 작업 저장소에 있고 여기 있는 것은 거기서 **생성된 사본**이다. 본문에 백틱으로 적힌 경로(ex `data/rule_source.yaml`)는 그 작업 저장소 안의 위치이며 여기엔 없다 — 링크로 걸린 것만 열린다.

규칙을 실제로 쓸지 판단하려면 각 폴더의 `README.md` 부터 보는 편이 빠르다. **그 규칙이 당신 환경에 무엇을 전제하는지**가 거기 적혀 있고, 대개 그것이 될지 안 될지를 가른다.
