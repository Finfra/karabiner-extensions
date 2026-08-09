---
name: README
description: 12Key2Knob 진입점 — 12키+2노브 매크로패드 전용 Keyboard Maestro 매크로 트리거 규칙
date: 2026.08.08
---

# 개요

12키 + 2노브 매크로패드를 감지해 각 키·노브를 개인 Keyboard Maestro 매크로 호출로 연결하는 규칙. rule 표시명은 `12Key2Knob : v2024.03.10` 이다.

manipulator 대부분이 `shell_command` 로 Keyboard Maestro Engine 에 매크로 이름을 넘기는 구조라, **하드웨어와 개인 매크로 라이브러리 양쪽에 100% 의존**한다. 순수 키매핑은 0건이다.

> 📌 **명칭 통일 (2026-08-08)**: 코드명 `nowageCustom` · 표시명 `12key+2knobe` · 정본 description `Nowage Custom : Combo V2024.03.10` 로 갈려 있던 세 이름을 **장치 이름 `12Key2Knob` 하나**로 모았다. 옛 이름을 만나면 `Extensions.md` 의 경로 이전 대응표를 본다.

# 파일 위치

| 구분                   | 경로                                                                                            |
| :--------------------- | :---------------------------------------------------------------------------------------------- |
| **배포 파일 (= 정본)** | [rule.json](rule.json)       |
| **매크로 export**      | [KeyboardMaestro_exports/12Key2Knob_Macros.kmmacros](KeyboardMaestro_exports/12Key2Knob_Macros.kmmacros) — 이름 뼈대 19종(아래 절) |
| 라이브 스냅샷          | `karabiner_json/_indivisual/snapshot/12Key2Knob.json` |
| 정보 파일 (ke_sync)    | [info.md](info.md) |
| 분류·공개 판정 (yaml)  | `data/rule_source.yaml` `만든_것`                                  |
| 장치 식별자 (json)     | `data/devices.json` `id: macropad_12key2knob`                |
| 장치 설명 문서         | `data/devices.md`                                                        |

> manipulator 수·`shell_command` 의존 건수는 [정보 파일](info.md)의 `ke-sync` 관리 블록이 정본이다.

# 장비

* `vendor_id 4489`(`0x1189`) · `product_id 34960`(`0x8890`) — 12키(3×4) + 노브 2개 매크로패드
* 단일 브랜드 제품이 아니라 **범용 CH57x 매크로패드** 계열이다. 칩 제조사 **WCH**([wch-ic.com](https://www.wch-ic.com/)) · VID `0x1189` 등록자 **Trisat Industrial**(이 계열 공용 VID) · 완제품은 무명 OEM 다수 — 셋의 구분과 사진·판매·설정도구 링크는 [정보 파일 "장비 정보" 절](info.md)
* ✅ **실사용 중** — 2026-08-07 `ioreg` 로 연결 확인(`wch.cn` / `CH57x`). 위 식별자가 실제 하드웨어와 일치한다
* ⚠️ **라이브 `devices` 엔트리는 0 건이지만 미연결이 아니다.** 그 값은 *설정을 손댄 적 있는 장치*를 세는 것이라 연결 여부와 무관하다 — 판정은 `ioreg` 로만 한다(`data/devices.md` "연결 판정" 절). 이 오독 때문에 오랫동안 "미연결·실동작 미검증" 으로 잘못 적혀 있었다
* `identifier_description` 이 manipulator 마다 `12Key2Knob_{키}[_with_{수식키}]` 형태로 다르다

# ⚠️ Keyboard Maestro 가 필요하다 — 매크로 export 동봉 (부분)

**이 규칙만으로는 동작하지 않는다.** manipulator 62건이 전부 `shell_command` 로 Keyboard Maestro Engine 에 **매크로 이름을 넘기는** 구조다. 순수 키매핑은 0건이다.

동봉 파일: [KeyboardMaestro_exports/12Key2Knob_Macros.kmmacros](KeyboardMaestro_exports/12Key2Knob_Macros.kmmacros) — Keyboard Maestro 의 **File → Import Macros…** 로 불러온다 (2026-08-09 추가).

## ⚠️ 이름 뼈대이지 완성품이 아니다

실측(2026-08-09) 기준으로 export 는 규칙이 부르는 이름의 **일부만** 담고 있고, 담긴 것도 대부분 본문이 비어 있다.

| 항목                     | 값 |
| :----------------------- | -: |
| 규칙이 호출하는 이름     | 62 |
| export 에 들어 있는 매크로 | 19 |
| **이름이 일치하는 것**   | **14** |
| 그중 동작 본문이 든 것   | 0 |

* 일치 14건 = 12키 무수식 `12Key2Knob_a`~`_l` + 노브 푸시 2종. **나머지 48건은 export 에 없다** — 전부 `{기본이름}_with_{ctl|opt|shift|cmd|alt}` 수식키 변형이다
* 일치분은 **Comment 액션 하나뿐인 빈 매크로**다. 이름만 존재해 호출이 실패하지 않게 할 뿐, 무엇을 할지는 받은 사람이 채운다
    - 예외 1건 — `12Key2Knob_d` 는 Comment 뒤에 `ExecuteMacro` 가 붙어 있고 그 대상 UID(`A4B71B72…`)가 이 export 에 없다. **비활성(disabled) 상태**라 실행되지는 않는다. 살려 쓸 것이 아니면 지워도 무방
* 실제 AppleScript 가 든 것은 규칙이 **부르지 않는** 노브 회전 4종(`___knob{1,2}__{left,right}`)뿐이다 — Keynote 최전면일 때 **선택 객체의 크기를 1.1배씩 조절**하고(knob1 = 폭 · knob2 = 높이 · left 축소 · right 확대), 그 밖의 앱에서는 방향키를 보낸다. 규칙 쪽은 회전 무수식을 직접 키로 처리하므로 이 4종은 KM 안에서만 쓰인다
    - **넷 다 조건 액션이 비활성 상태로 들어 있다.** 켜기 전에는 아무 일도 하지 않는다 — 어떻게 쓰는지 보여 주는 예시이지 완성품이 아니다
    - ⚠️ **`___knob1__left` 는 켜기 전에 한 줄 고쳐야 한다** — 폭만 계산해 놓고(`newWidth`) 정의하지 않은 `newHeight` 로 높이를 설정하는 줄이 남아 있다. 그 줄을 지우면 된다. 나머지 3종은 그대로 동작한다
* KM 트리거(단축키)는 전건 비어 있다. **정상이다** — 규칙이 `osascript` 로 이름을 직접 부르므로 KM 쪽 단축키가 필요 없다

## 왜 비어 있나 — 그래도 왜 내는가

12키의 실제 동작은 **개인 작업 흐름에 밀착**돼 있다(특정 파일·폴더를 여는 등). 그대로 내면 남에게 의미가 없고 개인 경로가 샌다. 그래서 **이름 뼈대만** 낸다.

받는 쪽 이득은 **이름을 새로 짓지 않아도 된다**는 것이다. 이름이 하나라도 어긋나면 그 키는 **조용히 아무 일도 하지 않는다** — Karabiner 도 KM 도 매크로 부재를 알리지 않는다. 특히 노브 계열은 언더스코어가 3개라(`12Key2Knob___knob1_push`) 손으로 적으면 틀리기 쉽다.

빠진 48종을 마저 만들려면 이름 목록을 규칙에서 직접 뽑는다:

```bash
grep -o 'do script \\"[^\\]*\\"' rule.json | sed 's/do script \\"//;s/\\"//' | sort -u
```

* ⚠️ **[FootPedal](../footPedal/README.md) 식 해법은 성립하지 않는다** — 그쪽은 Keyboard Maestro 의존을 순수 키 동작으로 걷어내 pqrs 에 공개했지만(PR #1982), 여기서는 **매크로 호출 자체가 기능**이라 걷어내면 남는 것이 없다

# 공개 상태

| 대상 | 상태 |
| :--- | :--- |
| **GitHub** | ✅ 공개 — [finfra/karabiner-extensions](https://github.com/Finfra/karabiner-extensions) (2026-08-09, Issue89) |
| **pqrs 등록** | ⏸️ **미룸** — 동봉 export 는 이름 뼈대뿐이라(본문 비어 있음) 남의 환경에서 곧바로 동작하지 않는다. 등록 기준을 아직 못 채운다. *하지 않기로 한 것이 아니라 지금은 안 하는 것* |

> 📌 **판정 정정 (2026-08-09)**: 이 절은 오래 *"공개하지 않는다 — 예정 없음"* 으로 적혀 있었다. 실제 판단은 **pqrs 등록을 미룬다**였고 GitHub 공개는 거부한 적이 없다. `data/rule_source.yaml` 의 `공개_대상` 한 필드가 **두 종류의 공개**(pqrs 등록 / GitHub 공개)를 겸해 생긴 혼동이다.

* 참고: 하드웨어·외부앱 의존 자체는 pqrs 결격 사유가 아니다(device-specific 그룹 36건 확인, 2026-07-18). 걸리는 것은 **매크로 부재**다

# 관련 이슈

Issue2(분류) · Issue1(공개 검토 — 보류) · Issue3(정보 파일) · Issue4(ke-sync) · Issue24(정본 재지정, 아티팩트 제거)
