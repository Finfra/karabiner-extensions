---
name: README
description: "Extensions/n3sh/_doc 인덱스 — 도구가 열지 않는 사람용 문서. 규칙 서술·표기 SSOT·변경 이력"
date: 2026.08.08
arch: _doc_arch/extension-layout-design.md
---
# 역할

n3sh 폴더는 **역할 3분할**이다(2026-08-08).

| 폴더 | 역할 | 누가 읽나 |
| :--- | :--- | :--- |
| [layout/](../layout) | **입력** — 사람 정본 md | 도구(`md_to_json`·`keymap_build`·`validate_docs`) + 사람 |
| [core/](../core) | **출력** — 생성 JSON·스키마 | 도구 (직접 편집 금지) |
| `_doc/` (여기) | **문서** — 읽는 것이 전부 | 사람 |

> 판정 한 줄: **프로그램이 이 파일을 여는가.** 열면 `layout/`, 안 열면 `_doc/`.

경계를 이렇게 그은 이유는, 셋이 한 폴더에 있으면 **어느 것을 손으로 고쳐도 되는지가 폴더만 보고 판정되지 않기** 때문이다. 생성 JSON 옆에 있는 md 는 "생성물인가" 를 매번 확인하게 만들고, 서술 문서 옆에 있는 정본 표는 "고쳐도 되나" 를 망설이게 만든다.

# 목록

| 문서 | 내용 |
| :--- | :--- |
| [notation.md](notation.md) | **표기 SSOT** — 동시타 · 모디파이어 2표기 · 초성/종성 `~` 접두. 데이터 md 와 도구 주석이 전부 이 문서를 인용한다 |
| [rules_notes_intersection.md](rules_notes_intersection.md) | 양 배열 **공통 규칙 수집** + Numbers 원문 보존 절. SSOT 예외(배열별 문서와 중복 보유 — 갈라지면 배열별이 이긴다) |
| [n390/rules_notes.md](n390/rules_notes.md) | **390 적용 규칙** — 출력 꼬리·기호 대응·트리거 유일성·배열 차이 (전건 실측) |
| [final/rules_notes.md](final/rules_notes.md) | **최종식 적용 규칙** — 같은 구조. ⚠️ 미배포 배열이라 계산값이며 실기 미확인 |
| [n390/CHANGELOG.md](n390/CHANGELOG.md) · [final/CHANGELOG.md](final/CHANGELOG.md) | 배열별 변경 이력. 짝인 `VERSION` 은 [layout/](../layout) 에 남았다 — `emit.py` 가 rule description 에 각인하므로 도구가 읽는다 |
| [n390/fsnippet-한글속기.md](n390/fsnippet-한글속기.md) | fSnippet(prj9) `_한글속기` 스니펫 세트 — 두 글자 이상 축약 담당  |
| [n390/training.md](n390/training.md) | **390 매뉴얼 초안** — 단계별 타건 드릴과 연습 문장 |
| [n390/training_cheatsheet.md](n390/training_cheatsheet.md) | 매뉴얼과 짝인 **한 장 요약** — 초성 자판 지도와 1·2·3열 배치 |
| `_doc_base/training_for_nowage.md` | 옛 습관 교정표 — 재배치 **이전** 손버릇을 가진 사람 전용(범용 아님) |
| [final/training.md](final/training.md) | 최종식 매뉴얼 초안 + 암기 보조표 |

## ⚠️ 판정 기준의 예외 2건

둘 다 **도구가 읽는데도 `_doc/` 에 있다.** 위 판정 한 줄대로면 `layout/` 이어야 하지만, 각각 성격을 우선한 사용자 지시 배치다(2026-08-08).

| 파일 | 여는 도구 → 산출 | 왜 여기인가 |
| :--- | :--- | :--- |
| `n390/fsnippet-한글속기.md` | `md_to_json.py` → [fsnippet_snippets.json](../core/fsnippet_snippets.json) 126건 | n3sh 키보드 규칙이 아니라 **별개 제품(fSnippet)의 자료**. 전용 폴더는 2026-08-08 폐지 |
| `final/training.md` | `md_to_json.py` → [practice.json](../core/final/practice.json) 4건 · [memory_aid.json](../core/final/memory_aid.json) 15건 | **매뉴얼 계열**이라 `training*` 넷이 함께 문서로 묶였다. 그중 final 판만 표 2개를 품고 있다 |

* `n390/training*.md` 3종은 예외가 아니다 — `validate_docs.py` 가 **검사만** 하고 아무것도 생성하지 않는다
* 예외 2건도 **편집 절차는 `layout/` 의 md 와 똑같다** — 고친 뒤 `md_to_json.py build` → `check` 를 돌린다. 여기 있다고 해서 자유 문서가 아니다
* 판정 기준을 바꾼 것이 아니라 **두 건을 예외로 둔 것**이다. 다른 파일을 옮길 때 이 배치를 선례로 삼지 말 것

# 여기 두지 않는 것

| 대상 | 실제 위치 |
| :--- | :--- |
| 규칙표·staging·금지 정본 md | [layout/](../layout) — 인덱스 [layout/README.md](../layout/README.md) |
| 단계 정의 (`rules_step.md`) | [layout/n390/rules_step.md](../layout/n390/rules_step.md) — 설계 계열이라 `layout/` 에 남았다. `validate_docs.py` 가 연다 |
| 생성 JSON·스키마 | [core/](../core) |
| Extension 자체 설명 | [README.md](../README.md) · [info.md](../info.md) |

# 관련

* 폴더 판정 기준: `_doc_arch/extension-layout-design.md`
* 데이터 편집 규약: `.claude/rules/data-md-first-rules.md`
* 파이프라인 설계: `_doc_arch/data-pipeline-design.md`
