---
name: info
description: "Builded Extension — NowageShorthand: n3sh(세벌속기) 본체, 프로젝트 핵심 시스템"
date: 2026-07-18
ke_sync:
  rule_description: "Nowage Shorthand for 3set 390 : Combo V2022.08.01"
  source_json: Extensions/n3sh/rule.json
---

# 개요

n3sh(세벌식 390 속기 자동화) 본체. 세벌식 390 자판에서 c1(첫 입력키)·c2(둘째 입력키)·품사·복잡글자 조합에 따라 완성형 한글 단어·구를 산출하는, 이 프로젝트의 핵심 산출물. 원본 Karabiner-Elements complex_modifications description: `Nowage Shorthand for 3set 390 : Combo V2022.08.01`.

# 소스 위치

* 정본 JSON: [Extensions/n3sh/rule.json](rule.json) — rule 단위 원본(수정 금지, manipulator 227). `description: "Nowage Shorthand for 3set 390 : Combo V2022.08.01"`
* 계보: 전체 config 백업 `karabiner_json/_orignal_do-not-update/all_setting/karabiner_2026.06.03_390.json` 의 같은 rule 에서 유래. 2026-07-26 부터 `ke_sync` 는 rule 단위 원본을 직접 참조한다
* 구조화 분류 데이터: `data/rule_source.yaml` `만든_것` 섹션
* 원천 규칙표(Numbers): 관리자 로컬의 iCloud Numbers 문서 `HotKeyForJmac_n3sh.numbers` (2026-08-02 `HotKeyForJmac.numbers`에서 n3sh 관련 정보·`자판`·`AlfredSnippet`·`속기` 탭 분리 이동. 상세: `_doc_base/background/README.md`) — ⚠️ 이 파일은 저장소에 없다. 데이터 정본은 [layout/](layout) 의 md 다
* 아티팩트 없음 — 원본이 이미 rule 단위라 추출본을 두지 않는다. 구 `artifact/nowage-shorthand.json` 은 manipulator 전건 동일한 중복본이었다
* ⚠️ manipulator 수 주의: 오라클·정본 227 / 라이브·build 228

# 의존성 (ke-sync 자동 생성)

<!-- ke-sync:begin -->
<!-- 이 블록은 tools/ke_sync.py 가 생성합니다. 직접 수정하면 다음 apply 때 덮어써집니다. -->

| 항목 | 값 |
| :--- | :--- |
| manipulator 총 수 | 227 |
| type 분포 | `basic` 227 |
| `device_if` 의존 | 0 |
| 대상 장치 | 없음 (하드웨어 비의존) |
| `shell_command` 의존 | 0 |
| 순수 키매핑 (장치·외부앱 비의존) | 227 |

* 원본: [rule.json](rule.json) → `(profile 없음 — rule 단위 원본)` → rule `Nowage Shorthand for 3set 390 : Combo V2022.08.01`
* 아티팩트: 없음 — 원본이 rule 단위라 추출본을 두지 않는다
* 원본 rule 다이제스트(sha256 앞 12): `2b31692b6921`
<!-- ke-sync:end -->

위 표는 `tools/ke_sync.py` 가 원본 JSON 에서 직접 계산한다.

해석: 하드웨어에 묶인 다른 Builded Extension(FootPedal, 12Key2Knob)과 달리 장치·외부 앱 의존이 전혀 없다. 대신 세벌식 390 자판이라는 특정 배열을 전제로 한 대규모 조합 규칙이라 그 자체로 복잡도가 매우 높고, 이것이 로드맵 4~6단계(구조화·생성기·배열 분기)가 필요한 이유다.

# 공개 상태

| 대상 | 상태 |
| :--- | :--- |
| **GitHub** | ✅ 공개 — [finfra/karabiner-extensions](https://github.com/Finfra/karabiner-extensions) (2026-08-09) |
| **pqrs 등록** | ⏸️ **계획 없음** — 규칙 1건 단위 등록 체계에 맞지 않는다. GitHub 공개로 방향이 정해져 있다(2026-07-19) |

> 📌 **경위**: 이 절은 오래 *"비공개 확정 — 애초부터 비공개가 목적"* 으로 적혀 있었다. 그 판단은 2026-07-19 에서 **완성 후 GitHub 공개**로 이미 뒤집혔고, 로 완성을 기다리지 않고 [Extensions/](..) 통째 공개에 실렸다. 남아 있던 문장이 낡은 것이다.

