---
name: README
description: 12Key2Knob 진입점 — 12키+2노브 매크로패드 전용 Keyboard Maestro 매크로 트리거 규칙
date: 2026.08.08
---

# 개요

12키 + 2노브 매크로패드를 감지해 각 키·노브를 개인 Keyboard Maestro 매크로 호출로 연결하는 규칙. rule 표시명은 `12Key2Knob : v2024.03.10` 이다.

manipulator 대부분이 `shell_command` 로 Keyboard Maestro Engine 에 매크로 이름을 넘기는 구조라, **하드웨어와 개인 매크로 라이브러리 양쪽에 100% 의존**한다. 순수 키매핑은 0건이다.

> 📌 **명칭 통일 (2026-08-08)**: 코드명 `nowageCustom` · 표시명 `12key+2knobe` · 정본 description `Nowage Custom : Combo V2024.03.10` 로 갈려 있던 세 이름을 **장치 이름 `12Key2Knob` 하나**로 모았다. 옛 이름을 만나면 [Extensions.md](../README.md) 의 경로 이전 대응표를 본다.

# 파일 위치

| 구분                   | 경로                                                                                            |
| :--------------------- | :---------------------------------------------------------------------------------------------- |
| **배포 파일 (= 정본)** | [rule.json](rule.json)       |
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

# ⚠️ 매크로는 이 저장소에 포함되지 않는다

**이 규칙만으로는 동작하지 않는다.** manipulator 62건이 전부 `shell_command` 로 Keyboard Maestro Engine 에 **매크로 이름을 넘기는** 구조이고, 그 매크로 본체는 여기 없다.

* 가져다 쓰려면 같은 이름의 매크로 62종을 **직접 만들어야** 한다 — 이름 목록은 [정보 파일](info.md) 과 아래 명령으로 얻는다:
    ```bash
    grep -o 'do script \\"[^\\]*\\"' rule.json | sed 's/do script \\"//;s/\\"//' | sort -u
    ```
* 이름이 하나라도 어긋나면 그 키는 **조용히 아무 일도 하지 않는다**(Karabiner 는 매크로 부재를 알리지 않는다). 특히 노브 계열은 언더스코어가 3개다 — `12Key2Knob___knob1_push`
* 매크로가 빠진 이유는 **개인 작업 흐름에 밀착**돼 있어서다. 파일·폴더 경로가 그대로 박혀 있어 남에게는 의미가 없고, 그대로 내면 개인정보가 샌다
* ⚠️ **[FootPedal](../footPedal/README.md) 식 해법은 성립하지 않는다** — 그쪽은 Keyboard Maestro 의존을 순수 키 동작으로 걷어내 pqrs 에 공개했지만(PR #1982), 여기서는 **매크로 호출 자체가 기능**이라 걷어내면 남는 것이 없다

# 공개 상태

| 대상 | 상태 |
| :--- | :--- |
| **GitHub** | ✅ 공개 — [finfra/karabiner-extensions](https://github.com/Finfra/karabiner-extensions) (2026-08-09, Issue89) |
| **pqrs 등록** | ⏸️ **미룸** — 매크로 없이는 남의 환경에서 동작하지 않아 등록 기준을 못 채운다. *하지 않기로 한 것이 아니라 지금은 안 하는 것* |

> 📌 **판정 정정 (2026-08-09)**: 이 절은 오래 *"공개하지 않는다 — 예정 없음"* 으로 적혀 있었다. 실제 판단은 **pqrs 등록을 미룬다**였고 GitHub 공개는 거부한 적이 없다. `data/rule_source.yaml` 의 `공개_대상` 한 필드가 **두 종류의 공개**(pqrs 등록 / GitHub 공개)를 겸해 생긴 혼동이다.

* 참고: 하드웨어·외부앱 의존 자체는 pqrs 결격 사유가 아니다(device-specific 그룹 36건 확인, 2026-07-18). 걸리는 것은 **매크로 부재**다

# 관련 이슈

Issue2(분류) · Issue1(공개 검토 — 보류) · Issue3(정보 파일) · Issue4(ke-sync) · Issue24(정본 재지정, 아티팩트 제거)
