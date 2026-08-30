---
name: README
description: FootPedal 진입점 — USB 3페달 풋스위치 편집·탐색·미디어 계층 규칙. pqrs 공개 등록 완료본
date: 2026.08.06
---

# 개요

USB 풋페달(발로 밟는 스위치) 3개를 감지해 페달마다 계층을 배정하고, 키보드에서 함께 누른 모디파이어로 층을 나누는 규칙. 라이브 rule 이름은 `Foot Pedal : v2026.07.26` 이다.

페달 3개가 각각 평범한 `a`/`b`/`c` 를 보내고, 페달 1개당 6층(무·control·option·shift·command·hyper)으로 갈린다.

| 모디파이어 | `a`(페달1) — 편집  | `b`(페달2) — 탐색 | `c`(페달3) — 미디어 |
| :--------- | :----------------- | :---------------- | :------------------ |
| (없음)     | 복사               | page down         | 재생/일시정지       |
| control    | 잘라내기           | page up           | 되감기              |
| option     | 붙여넣기           | end               | 빨리감기            |
| shift      | 서식 없이 붙여넣기 | home              | 음소거              |
| command    | 실행 취소          | Mission Control   | 볼륨 down           |
| hyper      | 다시 실행          | Launchpad         | 볼륨 up             |

**4종 중 유일하게 공개본과 개인 정본이 일치한다** — 공개용으로 순수 키 동작으로 재작성한 규칙을 그대로 개인 환경에도 올렸기 때문이다.

# 파일 위치

| 구분                    | 경로                                                                                          |
| :---------------------- | :-------------------------------------------------------------------------------------------- |
| **배포 파일 (= 정본)**  | [rule.json](rule.json)       |
| 라이브 스냅샷           | `karabiner_json/_indivisual/snapshot/foot_pedal.json` |
| 정보 파일 (ke_sync)     | [info.md](info.md) |
| 분류·공개 판정 (yaml)   | `data/rule_source.yaml` `만든_것` 첫 항목                        |
| 장치 식별자 (json)      | `data/devices.json` `id: foot_pedal`                       |
| 장치 설명 문서          | `data/devices.md`                                                      |
| **공개본 JSON**         | `pqrs_submission/json/nowage_foot_pedal.json` |
| 공개본 부가 설명 HTML   | `pqrs_submission/extra_descriptions/nowage_foot_pedal.html` |
| 구세대 규칙 (미배포)    | `karabiner_json/_orignal_do-not-update/all_setting/karabiner_2026.06.03_390.json` `Default profile` 의 `FootSwitch ` |

> manipulator 수·`device_if` 의존 건수 등 통계는 [정보 파일](info.md)의 `ke-sync` 관리 블록이 정본이다. 손으로 옮겨 적던 시절 22 → 20 오기가 실제로 있었다.

# 장비

* `vendor_id 6790`(`0x1a86`) · `product_id 57382`(`0xe026`)
* 장비사는 **3층으로 갈린다** — 칩·VID 등록자 **WCH**([wch-ic.com](https://www.wch-ic.com/)) · 완제품 브랜드 **PCsensor**(RDing Tech, [pcsensor.com 풋스위치](https://pcsensor.com/product-category/foot-switch/) — 유력하나 미확정) · 판매자는 같은 물건을 자기 이름으로 파는 리브랜딩 다수
* 후보 제품 **FS23-PM / FS3_P 계열 USB Triple Foot Switch** — 구조는 일치하나 VID/PID 를 판매 페이지에서 확인할 수 없어 **동일 제품 여부 미확정**
* 사진·구매 링크·브랜드 확정 절차(페달 연결 후 `ioreg` 문자열 서술자 확인): [정보 파일 "장비 정보" 절](info.md)

# 공개

* ✅ **pqrs 등록 완료** — PR [#1982](https://github.com/pqrs-org/KE-complex_modifications/pull/1982) merge(commit `42db4a4`, 2026-07-19)
* 사이트 노출 (Maintained by @nowage) — 사이트는 SPA 라 규칙별 고정 페이지가 없다. **JSON 주소가 가장 정확한 지목**이다
    - 규칙 파일: <https://ke-complex-modifications.pqrs.org/json/nowage_foot_pedal.json>
    - 부가 설명: <https://ke-complex-modifications.pqrs.org/extra_descriptions/nowage_foot_pedal.html>
    - 사이트에서 찾기: <https://ke-complex-modifications.pqrs.org/?q=nowage_foot_pedal>
* 제출 절차: `pqrs_submission/README.md`

# 이력

구세대 `FootSwitch ` 는 같은 페달 장치를 쓰되 모든 동작을 개인 Keyboard Maestro 매크로 호출(`shell_command`)로 처리했다. 두 세대의 manipulator 교집합은 **0** — 이름만 바뀐 것이 아니라 구현이 통째로 교체됐고, 그 재작성이 pqrs 공개의 직접 조건이었다. 상세 비교표: [정보 파일 "이력" 절](info.md)

