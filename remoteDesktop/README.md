---
name: README
description: RemoteDesktop 진입점 — MS 원격 데스크톱 한정 alt↔command 스왑 + keypad_comma 한/영 전환
date: 2026.08.06
---

# 개요

Microsoft 원격 데스크톱(RDC) 앱에서만 `left_alt` ↔ `left_command` 를 서로 바꾸고, 추가로 `keypad_comma` 를 `shift + spacebar`(Windows 한/영 전환)로 보내는 규칙. 라이브 rule 이름은 `Remote Desktop : v2026.07.26` 이다.

macOS 와 Windows 의 수식키 위치 차이 때문에 원격 세션에서 복사·붙여넣기 손버릇이 어긋나는 문제를 앱 한정으로 교정한다.

# 자작 판정 근거

Issue2 최초 분류가 이 규칙을 pqrs [virtual_machine_alt.json](https://ke-complex-modifications.pqrs.org/json/virtual_machine_alt.json) 에서 받은 것으로 **잘못 판정해** `_doc_base/builded_extensions` 에서 누락돼 있었다. 2026-07-29 대조로 자작임이 확정됐다.

| 항목                | pqrs `virtual_machine_alt.json`        | 본 규칙                                          |
| :------------------ | :-------------------------------------- | :----------------------------------------------- |
| 적용 대상 앱        | VMware·Parallels·RDC 등 가상머신 계열   | `com.microsoft.rdc`·`com.microsoft.rdc.macos` 2종 한정 |
| manipulator 수      | 2 (alt↔command 스왑)                    | 3                                                |
| 세 번째 manipulator | 없음                                    | `keypad_comma` → `shift + spacebar` (한/영 전환) |

# 파일 위치

| 구분                   | 경로                                                                                              |
| :--------------------- | :------------------------------------------------------------------------------------------------ |
| **배포 파일 (= 정본)** | [rule.json](rule.json)   |
| 라이브 스냅샷          | `karabiner_json/_indivisual/snapshot/remote_desktop.json` |
| 정보 파일 (ke_sync)    | [info.md](info.md) |
| 분류·공개 판정 (yaml)  | `data/rule_source.yaml` `만든_것`                                    |
| 오분류 경위            | `_doc_base/background/rule-classification.md` 검증 상태 절 |

> manipulator 통계는 [정보 파일](info.md)의 `ke-sync` 관리 블록이 정본이다.

# 공개

* ⏸ **보류** — 기술적으로는 가장 공개하기 쉬운 규칙이다. `device_if` 0 · `shell_command` 0 으로 **4종 중 유일하게 하드웨어·외부앱 비의존 순수 키매핑**이다
* 보류 사유: alt↔command 스왑 계열은 pqrs 에 이미 다수 등록돼 있고, 차별점인 `keypad_comma` 한/영 전환이 **세벌식 + Windows 원격**이라는 좁은 조합 전용이라 수요가 불확실

> 💡 [EngCharOnKor](../engCharOnKor/README.md) 도 한/영 전환을 다룬다. 그쪽이 완성되면 "한국어 입력 + macOS/Windows 혼용" 묶음으로 함께 공개하는 편이 개별 등록보다 설득력이 있다 — 공개 재검토 시 같이 볼 것.

# 관련 이슈

Issue2(분류 — 최초 오판정) · Issue1(공개 검토 — 보류) · Issue24(정본 재지정)
