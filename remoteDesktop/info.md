---
name: info
description: "Builded Extension — Remote Desktop: MS RDC 한정 alt↔command 스왑 + keypad_comma 한/영 전환"
date: 2026.07.29
ke_sync:
  rule_description: "Remote Desktop에서 left_alt를 left_command로, left_command를 left_alt로 매핑"
  source_json: Extensions/remoteDesktop/rule.json
---

# 개요

Microsoft Remote Desktop(RDC) 앱이 최전면일 때만 발동하는 규칙. Windows 원격 데스크톱 환경에서 macOS 수정자 배치를 Windows 관습에 맞추고(`left_alt` ↔ `left_command` 양방향 스왑), 세벌식 사용자가 쓰는 한/영 전환키(`keypad_comma`)를 Windows 쪽 전환 조합인 `shift + spacebar` 로 바꿔 보낸다. 원본 Karabiner-Elements complex_modifications description: `Remote Desktop에서 left_alt를 left_command로, left_command를 left_alt로 매핑`.

# 소스 위치

* 정본 JSON: [remote_desktop.json](rule.json) — rule 단위 원본(수정 금지)
* 구조화 분류 데이터: `data/rule_source.yaml` `만든_것` 섹션
* 계보: 전체 config 백업 `karabiner_json/_orignal_do-not-update/all_setting/karabiner_2026.06.03_390.json` 의 같은 rule 에서 유래
* 아티팩트 없음 — 원본이 이미 rule 단위라 추출본을 두지 않는다

# 자작 판정 근거 (2026-07-29 정정)

이 규칙은 2026-07-18 최초 분류에서 pqrs 공개 규칙 [Virtual Machine and Remote Desktop - Swap Command / Alt](https://ke-complex-modifications.pqrs.org/json/virtual_machine_alt.json) 를 그대로 받은 것으로 잘못 분류돼 있었다. 사용자 확인과 JSON 대조로 자작임이 확정됐다.

| 항목 | pqrs `virtual_machine_alt.json` | 본 규칙 |
| :--- | :--- | :--- |
| 적용 대상 앱 | VMware·Parallels·RDC 등 가상머신 계열 다수 | `com.microsoft.rdc`, `com.microsoft.rdc.macos` 2종 한정 |
| manipulator 수 | 2 (alt↔command 스왑) | 3 |
| 세 번째 manipulator | 없음 | `keypad_comma` → `shift + spacebar` (한/영 전환) |

수정자 스왑이라는 아이디어 자체는 널리 쓰이는 관용 패턴이라 겹쳐 보이지만, 대상 앱을 RDC 로 좁힌 점과 원본에 존재하지 않는 한/영 전환 매핑이 붙은 점이 자작임을 가른다. FootSwitch 가 2026-07-18 에 같은 이유(공개 예제와 스타일이 겹쳐 오분류)로 정정된 것과 동일한 사례다.

# 의존성 (ke-sync 자동 생성)

<!-- ke-sync:begin -->
<!-- 이 블록은 tools/ke_sync.py 가 생성합니다. 직접 수정하면 다음 apply 때 덮어써집니다. -->

| 항목 | 값 |
| :--- | :--- |
| manipulator 총 수 | 3 |
| type 분포 | `basic` 3 |
| `device_if` 의존 | 0 |
| 대상 장치 | 없음 (하드웨어 비의존) |
| `shell_command` 의존 | 0 |
| 순수 키매핑 (장치·외부앱 비의존) | 3 |

* 원본: [rule.json](rule.json) → `(profile 없음 — rule 단위 원본)` → rule `Remote Desktop에서 left_alt를 left_command로, left_command를 left_alt로 매핑`
* 아티팩트: 없음 — 원본이 rule 단위라 추출본을 두지 않는다
* 원본 rule 다이제스트(sha256 앞 12): `cef53c76a5b9`
<!-- ke-sync:end -->

위 표는 `tools/ke_sync.py` 가 원본 JSON 에서 직접 계산한다.

해석: `device_if` 가 없어 특정 하드웨어에 묶이지 않고, `shell_command` 도 없어 외부 앱 매크로에 의존하지 않는다. 조건은 `frontmost_application_if` 하나뿐이라 다른 사용자 환경에서도 그대로 동작한다 — 이 폴더의 다른 Builded Extension 3종과 달리 순수 키매핑으로만 구성된다.

# 공개 상태

| 대상 | 상태 |
| :--- | :--- |
| **GitHub** | ✅ 공개 — [finfra/karabiner-extensions](https://github.com/Finfra/karabiner-extensions) (2026-08-09) |
| **pqrs 등록** | ⏸️ **미룸** — 아래 사유 |

* pqrs 를 미루는 이유는 결격이 아니다. 하드웨어·매크로 의존이 없다는 점에서 다른 3종보다 사정이 좋다 — 다만 pqrs 에 이미 alt↔command 스왑 계열이 다수 등록돼 있어 차별점이 `keypad_comma` 한/영 전환 하나뿐이고, 그 매핑은 세벌식 + Windows 원격이라는 좁은 조합 전용이다. 등록 여부는 재개 시 함께 판단한다
* 📌 **정정 (2026-08-09)**: 이 절은 *"비공개 (현재 공개 대상 아님)"* 으로 적혀 있었으나, 이 폴더는 `tools/build_public.py` 가 공개 트리에 통째로 복사하므로 **push 되는 순간 이미 공개**였다. 보류는 pqrs 축의 판단이다
* 라이브 상태: ✅ `Remote Desktop : v2026.07.26` (manipulator 3)

