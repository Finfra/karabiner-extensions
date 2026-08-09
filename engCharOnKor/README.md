---
name: README
description: EngCharOnKor 진입점 — 한글 모드에서 Insert 를 누른 동안만 영문을 치는 규칙 (2026-08-07 라이브)
date: 2026.08.07
---

# 목적

> 🏷️ **영문 몇 글자 치려고 한글 치다 한/영 전환하고, 영문 타이핑하고, 다시 한/영 전환하고 — 그 왕복 없이. `Insert` 를 모디파이어처럼 누른 채 영문을 친다.**

한글 입력 모드에서 영문 한두 글자를 치려고 **한/영 전환 → 영문 입력 → 한/영 전환**을 왕복하는 것은 비효율이다. `Insert` 를 **누르고 있는 동안만** 영문이 나가면 그 왕복이 사라진다.

> ✅ **2026-08-07 라이브 반영.** 트리거 후보 7종을 실기로 걸러 `Insert` 홀드 레이어(G)를 채택했다. manipulator **30건**(레이어 2 + 대문자 토글 2 + 알파벳 26)으로 알파벳 + 숫자 + 기호를 덮는다.

# 쓰는 법

| 동작                           | 결과                                                           |
| :----------------------------- | :------------------------------------------------------------- |
| `Insert` 누른 채 글자          | 영문 소문자. 몇 글자든 연속 (`Insert` 누른 채 `a p i` → `api`) |
| `Insert` 누른 채 **`Home` 탭** | **대문자 토글** — 이어서 `a p i` → `API`. 다시 탭하면 소문자로 |
| `Insert`+`⇧`+글자              | 대문자 (한 글자짜리엔 이쪽도 됨)                               |
| `Insert` 뗌                    | 한글 복귀 + 대문자 상태 자동 해제                              |
| 조합중(`아`)에 `Insert`+글자   | 앞 글자가 확정되고 이어 붙는다 (`아a`)                         |
| 영문 모드에서 `Insert`         | 규칙 미발동 — 본래 동작                                        |

⚠️ `insert` 를 **내보내는** 물리 키는 키보드마다 다르다. 안 먹으면 `open -a "Karabiner-EventViewer"` 로 실제 `key_code` 를 먼저 확인할 것.

# 파일

| 구분                | 경로                                                                             | 상태                                 |
| :------------------ | :------------------------------------------------------------------------------- | :----------------------------------- |
| 정본 JSON           | [rule.json](rule.json)                                                           | ✅ 라이브                             |
| 정보 파일 (ke_sync) | [info.md](info.md)                                                               | ✅                                    |
| 설계 SSOT           | `_doc_arch/eng-char-on-kor-design.md` | ✅                                    |
| 분류 등록           | `data/rule_source.yaml` `만든_것`                   | ✅ (2026-08-07 `참고_발견` 에서 이관) |
| 후보 시험 이력      | [forTest/](forTest) · 기각분 [forTest/z_old/](forTest/z_old)                   | 📕 보존                               |
| 공개본 (선택)       | `pqrs_submission/json/nowage_eng_char_on_kor.json`                               | 🚧 미정                               |

* 초안 `karabiner_json/_orignal_do-not-update/z_backup/한글모드에서functionKey로%20영문입력/karabiner_forFunctionChar_inKorMode.json` 은 **수정 금지 영역**이라 그대로 보존한다. 정본은 그것을 고친 게 아니라 새로 작성했다

# 왜 `Insert` 인가 — 6종을 버린 끝

트리거 후보 7종 중 6종이 기각됐다. 사유 전문은 [forTest/z_old/README.md](forTest/z_old/README.md).

| 기각                  | 사유 요약                                          |
| :-------------------- | :------------------------------------------------- |
| 오른쪽 ⌘ / ⌘⇧         | 사용 중 · ⇧ 는 대문자용이라 트리거 금지            |
| 오른쪽 ⌥              | device 단 리매핑으로 **complex 규칙에 도달 안 함** |
| 한/영 홀드 / 모아치기 | 가장 많이 치는 키의 감각 변화 · 한 번에 한 글자    |
| `fn` 홀드             | `fn`+F키·방향키가 한글 모드 동안 전부 죽음         |

`insert` 는 **기존 규칙 점유 0 · macOS 기본 기능 없음 · device 리매핑 없음** 이라 잃는 것이 없다.

> 🔑 **교훈**: `simple_modifications` 가 `complex_modifications` 보다 먼저 적용된다. 트리거 키를 고르기 전에 라이브 device 리매핑을 반드시 먼저 읽을 것 — 안 읽어서 후보 3종을 통째로 날렸다.

# 설계 요점 (지우면 실패가 돌아온다)

네 가지 다 실기 실패를 겪고 들어왔다. 근거는 `_doc_arch/eng-char-on-kor-design.md`.

1. **홀드 레이어** — 입력소스 전환이 글자당이 아니라 **시퀀스당 1회**. 그래서 글자별 manipulator 가 0 건이다
2. **space+backspace 선행** — 조합중 글자가 버려지는 것을 막는다. Karabiner 에 조합 상태 조건이 **없어서**(지원 조건 7종에 preedit 없음) 무조건 실행이 유일한 길이다
3. **레이어 키 2분기** — `⇧space` 가 한/영 전환 단축키라, `mandatory:["any"]` 로 모디파이어를 소비해야 대문자가 꼬이지 않는다. ❌ `optional:["any"]` 한 건으로 합치지 말 것
4. **레이어 안에서만 `Home` 가로채기** — `variable_if` 로 레이어 중에만 발동해 대문자를 토글한다. 3키 홀드를 1키 홀드+1탭으로 줄인다. ❌ `sticky_modifier` 로 되돌리지 말 것 — lint 는 통과하지만 실기에서 **첫 글자만** 대문자가 된다(one-shot)

# n3sh 와의 관계

홀드 중 `keyboardLayoutSettingIsEng = 1` → [n3sh](../n3sh/README.md) 254행이 통째로 잠긴다. n3sh 에 처음부터 있었으나 **아무도 켜지 않던** off 스위치의 첫 사용처다.

# 공개

**pqrs 등록 대상으로 확정**(2026-08-08 재판정 — 판정 SSOT `data/rule_source.yaml`). `device_if` 0 · `shell_command` 0 인 순수 키매핑이라 [FootPedal](../footPedal/README.md) 과 같은 경로로 간다. 대상 그룹은 **`international`**(Language Specific) — FootPedal 의 `device-specific` 과 다르다.

⚠️ **구 보류 사유 `⇧space` 전환키 의존은 사실이 아니었다.** 입력소스 전환은 `select_input_source` 로 하지 `⇧space` 를 보내지 않고, `space`+`backspace` 는 전환이 아니라 **조합중 글자 커밋용**이다. `⇧space` 는 2026-08-07 2차 실기의 **누출 사고**였고 설계 요점 3(`mandatory:["any"]` 2분기)이 **이미 차단**했다 — 고쳐 놓고 그 위험을 보류 사유로 들고 있었던 것이다.

[RemoteDesktop](../remoteDesktop/README.md) 과 **묶지 않는다**(쟁점 ⑥ 종결) — 트리거·목적·조건이 전혀 달라, 묶으면 RDC 를 안 쓰는 사용자가 불필요한 규칙까지 받는다.

**남에게 요구하는 환경** (`extra_descriptions` 에 그대로 적을 것):

| # | 조건 |
| :-- | :--- |
| A | `insert` 를 내보내는 물리 키가 있고 다른 규칙에 점유되지 않을 것 |
| B | **레이어 중** `home` 이 다른 용도로 쓰이지 않을 것 — 레이어 밖 `home` 은 100% 평소대로다 |
| C | 입력소스가 `^ko$` / `^en$` 로 식별될 것 (macOS 표준) |
| D | 한글 IME 가 `space` 로 조합을 커밋할 것 |

`⇧space`·`⌘space` 등 한/영 전환 단축키가 무엇이든 **무관**하다.

# 관련

* 신규 Extension 추가 절차: [Extensions.md](../README.md)
* 분류 배경: `_doc_base/background/rule-classification.md`
* 이슈: **Issue85**(완료 2026-08-07) · **Issue85_1**(후보 시험)
