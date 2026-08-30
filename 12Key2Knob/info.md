---
name: info
description: "Builded Extension — 12Key2Knob: 12키+2노브 매크로패드 + Keyboard Maestro 매크로 트리거"
date: 2026.08.08
ke_sync:
  rule_description: "12Key2Knob : https://github.com/Finfra/karabiner-extensions v2024.03.10"
  source_json: Extensions/12Key2Knob/rule.json
---

# 개요

`12Key2Knob`이라는 12키+노브 2개짜리 매크로패드 장치를 감지해서, 키·노브 조합별로 Keyboard Maestro 매크로를 실행하는 규칙. Karabiner-Elements complex_modifications description: `12Key2Knob : v2024.03.10`.

> 📌 **명칭 통일 (2026-08-08)**: 이 규칙은 오래 `NowageCustom`·`Nowage Custom : Combo V2024.03.10`·`12key+2knobe` 세 이름으로 갈려 불렸다. `Nowage Custom` 은 무엇을 하는 규칙인지 말해 주지 않고 `12key+2knobe` 는 오타(`knobe`)였다. **장치 이름 `12Key2Knob` 하나로 통일**한다 — 폴더명·표시명·스냅샷 파일명이 모두 같은 값이다. 옛 이름은 오라클 백업(`_orignal_do-not-update/`)에만 남으며 그쪽은 수정 금지 영역이다.

# 소스 위치

* 정본 JSON: [Extensions/12Key2Knob/rule.json](rule.json) — rule 단위 원본. `description: "12Key2Knob : v2024.03.10"`
* **매크로 export**: [KeyboardMaestro_exports/12Key2Knob_Macros.kmmacros](KeyboardMaestro_exports/12Key2Knob_Macros.kmmacros) — Keyboard Maestro 매크로 19종(그룹 `9.6.1_12Key2Knob_`). 규칙이 부르는 62개 중 **이름 일치 14건**이며 그 14건의 본문은 비어 있는 뼈대다(액션 분포 — Comment 15 · IfThenElse 4 · ExecuteMacro 1). 동작이 든 것은 규칙이 **부르지 않는** 노브 회전 4종뿐이다. 상세·주의 2건: [README.md](README.md) "이름 뼈대이지 완성품이 아니다"
* 구조화 분류 데이터: `data/rule_source.yaml` `만든_것` 섹션
* 계보: 전체 config 백업 `karabiner_json/_orignal_do-not-update/all_setting/karabiner_2026.06.03_390.json` 의 같은 rule 에서 유래. 2026-07-26 부터 `ke_sync` 는 위 rule 단위 원본을 직접 참조한다
* 아티팩트 없음 — 원본이 이미 rule 단위라 추출본을 두지 않는다. 구 `artifact/nowage-custom.json` 은 manipulator 전건 동일한 중복본이었다

# 의존성 (ke-sync 자동 생성)

<!-- ke-sync:begin -->
<!-- 이 블록은 tools/ke_sync.py 가 생성합니다. 직접 수정하면 다음 apply 때 덮어써집니다. -->

| 항목 | 값 |
| :--- | :--- |
| manipulator 총 수 | 66 |
| type 분포 | `basic` 66 |
| `device_if` 의존 | 66 |
| 대상 장치 | vendor_id `4489` / product_id `34960` |
| `shell_command` 의존 | 62 |
| 순수 키매핑 (장치·외부앱 비의존) | 0 |

* 원본: [rule.json](rule.json) → `(profile 없음 — rule 단위 원본)` → rule `12Key2Knob : https://github.com/Finfra/karabiner-extensions v2024.03.10`
* 아티팩트: 없음 — 원본이 rule 단위라 추출본을 두지 않는다
* 원본 rule 다이제스트(sha256 앞 12): `e6cd4c51327d`
<!-- ke-sync:end -->

위 표는 `tools/ke_sync.py` 가 원본 JSON 에서 직접 계산한다.

해석: 대상 장치는 12키+2노브 매크로패드이며, 12키(`f1`~`f12`) 단독 / Control·Option·Shift 조합 / 노브 6동작(숫자 `1`~`6` — 회전 up·down·누름)까지 세분화된 식별자(`12Key2Knob_a`, `12Key2Knob_a_with_ct`, `12Key2Knob__knob1__d` 등)로 매핑이 나뉜다. `shell_command` 항목은 Keyboard Maestro 매크로 호출이고, 순수 키매핑이 0개라 원본 그대로는 타인 환경에서 재현되지 않는다.

# 장비 정보 (2026-08-08)

12키(3×4) + 노브 2개짜리 **범용 CH57x 매크로패드**다. 단일 브랜드 제품이 아니라 같은 펌웨어·같은 USB 식별자를 쓰는 OEM 물량이 여러 판매자 이름으로 풀린 계열이라, "제조사" 는 아래 셋을 구분해야 한다.

| 층                       | 실체                                                                                            | 근거                                                                                |
| :----------------------- | :---------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------- |
| **칩 제조사**            | 난징 QinHeng Microelectronics (**WCH**, [wch-ic.com](https://www.wch-ic.com/)) — `CH57x` 시리즈 | 2026-08-07 `ioreg` 실측이 `wch.cn` / `CH57x` 를 그대로 보고했다                     |
| **USB vendor_id 등록자** | `0x1189` = **Trisat Industrial Co., Ltd.**                                                      | USB ID 목록. ⚠️ 이 계열 매크로패드가 **공용으로 쓰는 VID** 이지 실제 조립사가 아니다 |
| **완제품 판매자**        | AliExpress·Amazon 등의 무명 OEM 다수                                                            | 아래 판매 링크                                                                      |

* **USB 식별자**: `vendor_id 4489`(`0x1189`) / `product_id 34960`(`0x8890`). 장치 식별자 정본은 `data/devices.json`(설명: `data/devices.md`)
* **장비 사진·형태**: 3×4 키 + 노브 2개. 같은 계열 전체를 사진과 함께 정리한 곳이 [ch57x-keyboard-tool 저장소](https://github.com/kriomant/ch57x-keyboard-tool) 다 — README 에 배열별(3×4+2노브 포함) 실물 사진이 있다
* **판매 링크(동형 제품)**: [AliExpress — 12 Key 2 Knob Macropad](https://www.aliexpress.com/item/1005005992174580.html) · [Bluetooth 판](https://www.aliexpress.com/item/1005009937927521.html). ⚠️ VID/PID 를 판매 페이지가 노출하지 않아 **완전 동일 제품 여부는 미확정** — 판정은 `ioreg` 의 `1189/8890` 로만 한다
* **키 재정의 도구(참고)**: 이 계열은 번들 Windows 전용 설정 앱 대신 오픈소스로 프로그래밍할 수 있다 — [ch57x-keyboard-tool](https://github.com/kriomant/ch57x-keyboard-tool)(`1189:8890` 명시 지원, macOS 가능) · [VMacropad](https://github.com/visiuun/VMacropad)
    - ⚠️ **이 규칙은 패드가 보내는 키에 의존한다.** 현재 12키는 `f1`~`f12`(×4층 = 48건), 노브 6동작은 숫자 `1`~`6`(18건)을 보내는 것을 전제로 짜여 있다. 2023년 백업(`karabiner_json/_orignal_do-not-update/z_backup/old_history/karabiner-for속기_2023.05.17.json`)에서는 같은 패드가 `a`~`l` 을 보내고 있었으므로, 그 사이에 **패드 자체의 키 배정이 한 번 바뀌었다**. 패드를 초기화하거나 다른 개체로 교체하면 이 규칙은 통째로 안 먹는다 — 그때 배정을 되돌리는 수단이 위 도구다

# 공개 상태

| 대상 | 상태 |
| :--- | :--- |
| **GitHub** | ✅ 공개 — [finfra/karabiner-extensions](https://github.com/Finfra/karabiner-extensions) (2026-08-09) |
| **pqrs 등록** | 🚧 **준비 완료 · 미제출** (2026-08-11) — 산출물 3종 완비(`pqrs_submission/json/nowage_12key2knob.json` · `pqrs_submission/extra_descriptions/nowage_12key2knob.html` · groups_entry) · lint ok · 정본과 66건 전건 동일. PR 만 남았고 **제출 여부는 사용자 판단** |

> 📌 **방침 철회 (2026-08-09)**: 이 절은 *"공개하지 않는다 — 예정 없음"* 으로 적혀 있었다. 이 폴더는 `tools/build_public.py` 가 통째로 공개 트리에 복사하므로 **push 되는 순간 이미 공개**이며, 비공개 방침은 사실과 어긋난 채 남아 있었다. 철회하고 두 축으로 갈라 적는다 — 근본 원인은 `data/rule_source.yaml` 의 `공개_대상` 한 필드가 **pqrs 등록**과 **GitHub 공개**를 겸한 것이다.

* ✅ **미룸 철회 (2026-08-11)** — 구 사유는 *"매크로 본문이 비어 있어 등록 기준을 못 채운다"* 였으나, upstream [hub16-launchapps.json](https://github.com/pqrs-org/KE-complex_modifications/blob/main/public/json/hub16-launchapps.json) 이 `device_if` + `shell_command` 매크로패드 규칙을 **`(template)`** 로 같은 `device-specific` 그룹에 등록해 둔 것이 확인됐다. 받는 사람이 내용을 채우는 형태는 이미 허용된다
    - ⚠️ **잔여 리스크**: hub16 은 `open '/Applications/X.app'` 이라 KM 없이 즉시 동작하지만 본 규칙은 KM(유료) + 매크로 62종 없이는 **아무 일도 하지 않는다**. 리뷰어가 결격으로 볼 여지가 남아, 공개본 설명 첫 절이 이를 정면으로 밝히고 시작한다
* ⚠️ **[FootPedal](../footPedal/info.md) 식 해법은 pqrs 축에서 성립하지 않는다.** FootPedal 은 Keyboard Maestro 의존을 순수 키 동작으로 걷어내 등록했지만(PR #1982), 본 규칙은 **매크로 호출 자체가 기능**이라 걷어내면 남는 것이 없다 — 그래서 **재작성 없이 정본 그대로** 낸다(드리프트 0)
* ✅ **매크로 export 동봉 (2026-08-09)** — 구 방침은 *"export 원본은 개인 경로가 박혀 있어 공개 트리 밖에 둔다"* 였다. 실제로 내보낸 파일을 전수 스캔한 결과 **개인 경로·계정·실명·메일 0건**이었다(본문이 비어 있는 뼈대라 경로가 애초에 없다). 방침을 철회하고 [KeyboardMaestro_exports/](KeyboardMaestro_exports) 에 동봉한다 — 보관소였던 `_doc_base/km_macros/12Key2Knob/README.md` 는 이제 익명화 절차 문서만 남는다
* ⚠️ **개인 동작이 든 매크로를 추가로 내려면 익명화가 선행 조건**이다 — 경로는 지우지 말고 `/Users/{yourname}` 로 예제화하고, `build_public.py` → `validate_public.py` **exit 0** 을 확인한 뒤 push 한다
* 판정 근거: `data/rule_source.yaml` `pqrs_보류_사유`

