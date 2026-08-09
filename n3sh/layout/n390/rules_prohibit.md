---
name: rules_prohibit
description: "세벌식 390 판 배정 금지 자리 SSOT — 의도적으로 비워 두기로 결정한 트리거와 그 사유 (prohibit.json 정본)"
date: 2026.08.05
rule: .claude/rules/data-md-first-rules.md
arch: _doc_arch/data-pipeline-design.md
generates: [Extensions/n3sh/core/n390/prohibit.json]
---
# 0. 개요

**배열: 390.** 의도적으로 **비워 두기로 결정한** 트리거다. "아직 안 정함"([staging.md](staging.md) `미정`)과 반드시 구분한다 — 여기 있는 자리는 **배정 금지**다.

* 데이터: [prohibit.json](../../core/n390/prohibit.json) — 총 6건 · 스키마: [prohibit.schema.json](../../core/schema/prohibit.schema.json)
* 유입: [staging.md](staging.md) 의 `금지` → 결정이 서면 이 파일로 승격. staging 은 전이 구역이라 나가지 않는 항목을 담지 않는다(2026-08-05 분리)
* 불변식: **`prohibit ∩ rules = ∅`** — 같은 (`c1`,`c2`,⌥,⇧,⌘) 조합이 [rules.md](rules.md) 에 활성으로 있으면 안 된다. `python3 tools/validate_cross.py` 가 검사한다

> `사유` 는 **필수**다. 근거 없는 금지는 나중에 되돌릴 수 없다 — 왜 막았는지 모르면 아무도 손대지 못하고, 그렇다고 신뢰할 수도 없다.
> 🔧 현재 2건이 `등록안됨` 인데 이는 **상태 서술이지 사유가 아니다**. 원 결정 근거를 확인해 채울 것.

> 셀 표기: `—` 는 빈 문자열, `␣` 는 공백 1칸. `c1`·`c2`(누르는 키)의 `␣` 는 **스페이스바 키**로 JSON 에 `_` 로 저장된다. 종성 자모는 `~` 접두([notation.md](../../_doc/notation.md)). 표를 고친 뒤 `python3 tools/md_to_json.py build`

# 1. 금지 표

<!-- data: prohibit.json -->

| c1  | c2  | h1  | h2  | ⌥   | ⇧   | ⌘   | txt | 기호 | sp  | 품사 | 사유                                              |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | ---- | ------------------------------------------------- |
| u   | ;   | ㄷ  | ㅂ  | —   | ✔   | —   | 다  | ?    | ✔   | e    | 등록안됨                                          |
| u   | ;   | ㄷ  | ㅂ  | —   | ✔   | ✔   | 다  | !    | ✔   | e    | 등록안됨                                          |
| k   | m   | ㄱ  | ㅎ  | —   | ✔   | ✔   | 고  | !    | ✔   | —    | OS 단축키 충돌 확인. 지정 금지                    |
| k   | m   | ㄱ  | ㅎ  | —   | —   | ✔   | 고  | —    | ✔   | —    | OS 단축키 충돌 확인. 지정 금지                    |
| m   | ;   | ㅎ  | ㅂ  | -   | -   | ✔   | 해  | —    | ✔   | e    | macOS 윈도우 최소화가 선점 → 구조적으로 발동 불가 |
| f   | v   | ㅏ  | ㅗ  | —   | —   | —   | —   | —    | —   | —    | 이중모음 ㅘ(ㅗ+ㅏ) 구성 —  배정 금지              |
