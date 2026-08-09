---
name: rules_prohibit
description: "세벌식 최종식 판 배정 금지 자리 SSOT — 의도적으로 비워 두기로 결정한 트리거와 그 사유 (prohibit.json 정본)"
date: 2026.08.05
rule: .claude/rules/data-md-first-rules.md
arch: _doc_arch/data-pipeline-design.md
generates: [Extensions/n3sh/core/final/prohibit.json]
---
# 0. 개요

**배열: 최종식.** 의도적으로 **비워 두기로 결정한** 트리거다. "아직 안 정함"([staging.md](staging.md) `미정`)과 반드시 구분한다 — 여기 있는 자리는 **배정 금지**다.

* 데이터: [prohibit.json](../../core/final/prohibit.json) — 총 3건 · 스키마: [prohibit.schema.json](../../core/schema/prohibit.schema.json)
* 유입: [staging.md](staging.md) 의 `금지` → 결정이 서면 이 파일로 승격 (2026-08-05 분리)
* 불변식: **`prohibit ∩ rules = ∅`** — `python3 tools/validate_cross.py` 가 검사한다
* ⚠️ **최종식 판정은 미시작**이다 — 아래 3건은 390 분리 시점(2026-08-02)의 사본이며 최종식 기준으로 재검토된 적이 없다. 이관 중 `m+;`+⇧⌘ 1건은 **거짓 금지**로 판정돼 제거했다(2026-08-05 — rules 에 `해!` 가 활성. 390 도 같은 트리거에서 같은 사유로 제거)

> `사유` 는 **필수**다. 🔧 현재 2건이 `등록안됨` 으로, 이는 상태 서술이지 사유가 아니다 — 재검토 시 함께 채울 것.

> 셀 표기: `—` 는 빈 문자열, `␣` 는 공백 1칸. `c1`·`c2`(누르는 키)의 `␣` 는 **스페이스바 키**로 JSON 에 `_` 로 저장된다. 종성 자모는 `~` 접두([notation.md](../../_doc/notation.md)).

# 1. 금지 표

<!-- data: prohibit.json -->

| c1  | c2  | h1  | h2  | ⌥   | ⇧   | ⌘   | txt | 기호 | sp  | 품사 | 사유                                                                                            |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | ---- | ----------------------------------------------------------------------------------------------- |
| u   | ;   | ㄷ  | ㅂ  | —   | ✔   | —   | 다  | !    | ✔   | e    | 등록안됨                                                                                        |
| u   | ;   | ㄷ  | ㅂ  | —   | ✔   | ✔   | 다  | ?    | ✔   | e    | 등록안됨                                                                                        |
| m   | ;   | ㅎ  | ㅂ  | -   | -   | ✔   | 해  | —    | ✔   | e    | ⌘+m 이 먼저 눌리면 macOS 윈도우 최소화가 선점 → 구조적으로 발동 불가 (rules `x`=✔ 와 같은 결정) |
