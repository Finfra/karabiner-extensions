---
name: README
description: RemoteDesktop 진입점 — MS 원격 데스크톱 한정 alt↔command 스왑 + keypad_comma 한/영 전환
date: 2026.08.06
---

# 개요

Microsoft 원격 데스크톱(RDC) 앱에서만 `left_alt` ↔ `left_command` 를 서로 바꾸고, 추가로 `keypad_comma` 를 `shift + spacebar`(Windows 한/영 전환)로 보내는 규칙. 라이브 rule 이름은 `Remote Desktop : v2026.07.26` 이다.

macOS 와 Windows 의 수식키 위치 차이 때문에 원격 세션에서 복사·붙여넣기 손버릇이 어긋나는 문제를 앱 한정으로 교정한다.

# 자작 판정 근거

 최초 분류가 이 규칙을 pqrs [virtual_machine_alt.json](https://ke-complex-modifications.pqrs.org/json/virtual_machine_alt.json) 에서 받은 것으로 **잘못 판정해** `_doc_base/builded_extensions` 에서 누락돼 있었다. 2026-07-29 대조로 자작임이 확정됐다.

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

| 대상 | 상태 |
| :--- | :--- |
| **GitHub** | ✅ 공개 — [finfra/karabiner-extensions](https://github.com/Finfra/karabiner-extensions) (2026-08-09) |
| **pqrs 등록** | 🚧 **준비 완료 · 미제출** (2026-08-11) — 산출물 3종 완비 · lint ok · 정본과 3건 전건 동일. 대상 그룹 **`application-specific`** |

* 기술적으로는 가장 공개하기 쉬운 규칙이다. `device_if` 0 · `shell_command` 0 으로 **5종 중 유일하게 하드웨어·외부앱 비의존 순수 키매핑**이다
* ✅ **보류 철회 (2026-08-11)** — 구 사유는 *"차별점이 좁다"* 였는데 이는 결격이 아니라 **수요 판단**이었다. 실측 대조 결과 upstream `application-specific` 의 원격 데스크톱·가상머신 계열 6건은 전부 모디파이어 재배치이고 **한/영 전환을 포함한 것은 없다** — 대조표: `pqrs_submission/README.md` `nowage_remote_desktop.json` 절
* ⚠️ **공개본은 문안을 새로 썼다** — 정본 `title`·`description` 이 한글이라 앞 3건 중 유일하게 영문화가 필요했다. manipulator 는 전건 동일하다

> 💡 [EngCharOnKor](../engCharOnKor/README.md) 도 한/영 전환을 다루지만 **묶지 않기로 했다**(2026-08-08,  쟁점 ⑥) — 트리거·목적·조건이 전혀 다르고, 묶으면 RDC 를 안 쓰는 사용자가 불필요한 규칙까지 받는다. 각각 별도 등록한다.

