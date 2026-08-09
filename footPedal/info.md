---
name: info
description: "Builded Extension — Foot Pedal: USB 3페달 풋스위치, 모디파이어 6층 편집·탐색·미디어 매핑"
date: 2026-07-29
ke_sync:
  rule_description: "USB Foot Pedal (3 pedals). Pedal 1 (left, 'a') = editing: copy, control=cut, option=paste, shift=paste-without-formatting, command=undo, hyper=redo. Pedal 2 (middle, 'b') = navigation: page down, control=page up, option=end, shift=home, command=Mission Control, hyper=Launchpad. Pedal 3 (right, 'c') = media: play/pause, control=rewind, option=fast-forward, shift=mute, command=volume down, hyper=volume up. Requires a USB foot switch with vendor_id 6790 (0x1a86) / product_id 57382 (0xe026)."
  source_json: Extensions/footPedal/rule.json
---

# 개요

USB 풋페달(발로 밟는 스위치) 3개를 감지해, 페달마다 편집·탐색·미디어 계층을 배정하고 함께 누른 모디파이어로 층을 나누는 규칙. 라이브에서는 `Foot Pedal : v2026.07.26` 으로 올라가 있다.

> 📌 **명칭 통일 (2026-07-29)**: 이 규칙은 오래 `FootSwitch` 로 불렸다. 라이브·정본·pqrs 공개본이 모두 `foot_pedal` 계열 이름으로 수렴했으므로 문서도 **foot_pedal 로 통일**했다. 구세대 `FootSwitch`(Keyboard Maestro 경유, manipulator 20)는 별도 extension 이 아니라 **본 규칙의 이전 세대**이며, 아래 "이력" 절에 남긴다.

# 소스 위치

* 정본 JSON: [foot_pedal.json](rule.json) — rule 단위 원본(수정 금지)
* 구조화 분류 데이터: `data/rule_source.yaml` `만든_것` 섹션
* 계보: 구세대 `FootSwitch` rule 은 전체 config 백업 `karabiner_json/_orignal_do-not-update/all_setting/karabiner_2026.06.03_390.json` 의 `Default profile` 에 남아 있다
* 아티팩트 없음 — 원본이 이미 rule 단위라 추출본을 두지 않는다

# 의존성 (ke-sync 자동 생성)

<!-- ke-sync:begin -->
<!-- 이 블록은 tools/ke_sync.py 가 생성합니다. 직접 수정하면 다음 apply 때 덮어써집니다. -->

| 항목 | 값 |
| :--- | :--- |
| manipulator 총 수 | 18 |
| type 분포 | `basic` 18 |
| `device_if` 의존 | 18 |
| 대상 장치 | vendor_id `6790` / product_id `57382` |
| `shell_command` 의존 | 0 |
| 순수 키매핑 (장치·외부앱 비의존) | 0 |

* 원본: [rule.json](rule.json) → `(profile 없음 — rule 단위 원본)` → rule `USB Foot Pedal (3 pedals). Pedal 1 (left, 'a') = editing: copy, control=cut, option=paste, shift=paste-without-formatting, command=undo, hyper=redo. Pedal 2 (middle, 'b') = navigation: page down, control=page up, option=end, shift=home, command=Mission Control, hyper=Launchpad. Pedal 3 (right, 'c') = media: play/pause, control=rewind, option=fast-forward, shift=mute, command=volume down, hyper=volume up. Requires a USB foot switch with vendor_id 6790 (0x1a86) / product_id 57382 (0xe026).`
* 아티팩트: 없음 — 원본이 rule 단위라 추출본을 두지 않는다
* 원본 rule 다이제스트(sha256 앞 12): `0903db46e22b`
<!-- ke-sync:end -->

위 표는 `tools/ke_sync.py` 가 원본 JSON 에서 직접 계산한다. 사람이 손으로 옮겨 적던 시절 구세대 규칙의 manipulator 수를 22개로 잘못 기록했다가 아티팩트 추출 과정에서 20개로 정정한 전례가 있어, 이 수치들은 기계 산출로 넘겼다.

# 구조

페달 3개가 각각 평범한 `a`/`b`/`c` 키를 보내고, 키보드에서 함께 누른 모디파이어로 층을 나누는 설계다. 페달 1개당 6층(무·control·option·shift·command·hyper)이므로 3 × 6 = 18슬롯이다.

| 모디파이어 | `a`(페달1) — 편집  | `b`(페달2) — 탐색 | `c`(페달3) — 미디어 |
| :--------- | :----------------- | :---------------- | :------------------ |
| (없음)     | 복사               | page down         | 재생/일시정지       |
| control    | 잘라내기           | page up           | 되감기              |
| option     | 붙여넣기           | end               | 빨리감기            |
| shift      | 서식 없이 붙여넣기 | home              | 음소거              |
| command    | 실행 취소          | Mission Control   | 볼륨 down           |
| hyper      | 다시 실행          | Launchpad         | 볼륨 up             |

# 장비 정보 (2026-07-18)

## 장비사 3층 (2026-08-08 보강)

12Key2Knob 과 같은 사정이다 — 이 계열은 **단일 브랜드 제품이 아니라** 같은 컨트롤러·같은 USB 식별자를 쓰는 물량이 여러 이름으로 풀린다. 그래서 "제조사" 를 한 줄로 못 적고 아래 셋으로 나눈다.

| 층 | 실체 | 근거 |
| :--- | :--- | :--- |
| **칩·VID 등록자** | 난징 QinHeng Microelectronics (**WCH**, [wch-ic.com](https://www.wch-ic.com/)) — `vendor_id 0x1a86` 이 WCH 정식 등록 VID | USB ID 목록. 저가형 풋스위치·매크로 장치가 이 컨트롤러를 널리 쓴다 |
| **완제품 브랜드(유력)** | **PCsensor**(RDing Tech, [pcsensor.com](https://pcsensor.com/product-category/foot-switch/)) — 풋스위치 전문 제조사. FS 시리즈(FS23·FS3_P 등)가 이 계열 | `1a86:e026` 이 PCsensor 계열 설정 도구 [rgerganov/footswitch](https://github.com/rgerganov/footswitch) 의 지원 목록에 명시돼 있다. 다만 그 문서는 **VID/PID 만 적고 브랜드명을 붙이지 않는다** |
| **판매자** | AliExpress·Amazon 의 리브랜딩 다수(Nancie·LNIMI·Ctzrzyt 등이 같은 `FS3-P` 를 자기 이름으로 판다) | 아래 판매 링크 |

* USB 식별자: `vendor_id 6790`(`0x1a86`) / `product_id 57382`(`0xe026`). 정본은 `data/devices.json`(설명: `data/devices.md`)
* 후보 제품: **FS23-PM / FS3_P 계열 USB Triple Foot Switch** — 3페달 USB HID. 제조사 공식 페이지 [PCsensor USB Foot Switch Triple Pedals FS23](https://pcsensor.com/product-category/foot-switch/) 에 실물 사진이 있다
* 구매 링크(동형): https://www.aliexpress.com/item/1005010759334987.html (2026-07-18 확인 시점 ₩30,600, 평점 5.0/7리뷰, 144 sold)
* 설정 도구(참고): [rgerganov/footswitch](https://github.com/rgerganov/footswitch) — `1a86:e026` 지원. ⚠️ **본 규칙은 쓰지 않는다.** 페달이 보내는 `a`/`b`/`c` 를 그대로 두고 해석은 Karabiner 가 맡는 설계라, 펌웨어를 건드리면 오히려 규칙이 깨진다

### ⚠️ 아직 미검증인 것 — 브랜드 확정

* **PCsensor 는 "유력" 이지 확정이 아니다.** 근거가 서드파티 도구의 지원 목록 한 줄뿐이고, AliExpress 는 VID/PID 를 스펙에 노출하지 않아 판매 페이지로는 대조할 수 없다
* 확정하는 방법은 하나 — **페달을 꽂고 USB 문자열 서술자를 읽는다.** 이 계열은 보통 `iManufacturer = PCsensor` / `iProduct = FootSwitch` 로 나온다
    ```bash
    # 페달을 연결한 뒤 실행. Manufacturer/Product 문자열이 브랜드의 유일한 1차 근거다
    ioreg -c IOHIDDevice -r -l | grep -E '"(Product|Manufacturer|VendorID|ProductID)" =' | grep -B3 -A1 57382
    ```
* 2026-08-08 실행 시점에는 페달이 **연결돼 있지 않아 확인 못 했다**(같은 명령으로 매크로패드는 `wch.cn`/`CH57x` 가 그대로 나왔다). 다음에 꽂을 때 이 절을 갱신한다 🔧

# 공개 상태

* **공개 등록 완료 (2026-07-19)** — PR [#1982](https://github.com/pqrs-org/KE-complex_modifications/pull/1982) merge(commit `42db4a4`) 후 [ke-complex-modifications.pqrs.org](https://ke-complex-modifications.pqrs.org/?q=foot%20pedal) 에 **USB Foot Pedal (3 pedals) - Editing / Navigation / Media layers** (Maintained by @nowage) 로 노출 중
* 공개본 `pqrs_submission/json/nowage_foot_pedal.json` 과 정본 [foot_pedal.json](rule.json) 은 **manipulator 전건 동일**하다(2026-07-29 실측). 공개용으로 재작성한 규칙을 그대로 개인 환경에도 올린 결과다
* 요구 장비는 `pqrs_submission/extra_descriptions/nowage_foot_pedal.html` 에 명시했고 `karabiner_cli --lint-complex-modifications` 를 통과했다. 제출 절차·현황: `pqrs_submission/README.md`

# 이력 — 구세대 `FootSwitch` (Keyboard Maestro 경유, 미배포)

2026-07 이전 세대는 같은 페달 장치를 쓰되 **모든 동작을 개인 Keyboard Maestro 매크로 호출로 처리**했다. 지금은 라이브에 없다.

| 항목        | 구세대 `FootSwitch `                                                    | 현행 `Foot Pedal : v2026.07.26`      |
| :---------- | :---------------------------------------------------------------------- | :----------------------------------- |
| manipulator | 20 (18슬롯 + Lock/Unlock 2)                                             | 18                                   |
| 구현 방식   | `shell_command` 20건 — `osascript … "Keyboard Maestro Engine" … do script` | 순수 키 동작 (외부 앱 의존 0)        |
| 매크로 이름 | `FootSwitch__a`, `FootSwitch__a_c`, `FootSwitch__Unlock` 등             | 해당 없음                            |
| 위치        | 전체 config 백업 `all_setting/karabiner_2026.06.03_390.json` `Default profile` | `_indivisual/org/foot_pedal.json` |
| 배포        | ❌ 대체됨                                                                | ✅ 라이브                             |

* 두 세대의 manipulator 교집합은 **0** 이다. 이름만 바뀐 것이 아니라 구현이 통째로 교체됐다.
* 구세대는 개인 매크로 이름에 100% 의존해 타인 환경에서 아무것도 동작하지 않았고, 그 점이 pqrs 공개를 위해 순수 키 동작으로 재작성한 직접 이유였다. 개인 전용 `FootSwitch__Unlock`·`FootSwitch__Lock` 2개는 그때 제외돼 20 → 18 이 됐다.
* 구세대 추출 아티팩트 `artifact/footswitch.json` 은 2026-07-29 제거했다. 정본이 전체 config 백업에 그대로 남아 있어 언제든 다시 뽑을 수 있고, 현행 규칙과 무관한 사본을 유지하면 드리프트 대상만 늘어난다. 복구가 필요하면 git 이력에서 꺼낸다.

