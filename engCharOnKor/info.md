---
name: info
description: "Builded Extension — Eng Char on Kor: 한글 모드에서 Insert 를 누른 동안만 영문 입력, 떼면 한글 복귀"
date: 2026.08.07
ke_sync:
  rule_description: "Eng Char on Kor : v2026.08.07"
  source_json: Extensions/engCharOnKor/rule.json
---

# 개요

한글 입력 모드를 유지한 채 **`Insert` 를 누르고 있는 동안만** 영문을 치는 규칙. 떼면 한글로 돌아온다. 한/영 전환 → 영문 입력 → 한/영 재전환의 왕복을 없애는 것이 목적이다.

영문 몇 글자를 끼워 넣을 때마다 왕복하던 것이 **키 하나를 누르고 있는 것**으로 바뀐다. 대문자는 홀드 중 `Home` 을 **탭**해서 토글한다(설계 요점 4).

# 소스 위치

* 정본 JSON: [rule.json](rule.json) — rule 단위 원본
* 구조화 분류 데이터: `data/rule_source.yaml` `만든_것` 섹션
* 설계 SSOT: `_doc_arch/eng-char-on-kor-design.md`
* 계보: 초안 `karabiner_json/_orignal_do-not-update/z_backup/한글모드에서functionKey로%20영문입력/karabiner_forFunctionChar_inKorMode.json` (`fn`+알파벳 52행, 결함 5건으로 로드 불가). 정본은 그 초안을 고친 것이 아니라 **새로 작성**했다
* 후보 시험 이력: [forTest/](forTest) — 채택된 G(Insert 홀드) · 기각된 A~F [z_old/](forTest/z_old)

# 동작

| 동작 | 결과 |
| :--- | :--- |
| `Insert` 누름 (한글 모드) | 조합중 글자 확정 → 영문 입력소스로 전환 → `keyboardLayoutSettingIsEng = 1` |
| 누른 채 아무 글자 | 영문 소문자 |
| 누른 채 **`Home` 탭** | **대문자 켬/끔 토글** (변수 `engCharUpper`) |
| 누른 채 `⇧`+글자 | 대문자 (여전히 됨 — 한 글자짜리엔 이쪽이 빠를 수 있다) |
| `Insert` 뗌 | 한글 복귀 → `keyboardLayoutSettingIsEng = 0` + **대문자 상태 해제** |
| `Insert` (영문 모드) | 규칙 미발동 — `Insert` 본래 동작 |
| `Home` (레이어 밖) | 규칙 미발동 — `Home` 본래 동작 |

# 설계 요점 4가지

네 가지가 이 규칙의 전부다. 각각 실기에서 실패를 겪고 들어온 것이라 **지우면 그 실패가 돌아온다**.

## 1. 홀드 레이어 — 입력소스 전환이 시퀀스당 1회

키마다 영문↔한글을 왕복하지 않는다. `Insert` 를 누를 때 한 번, 뗄 때 한 번뿐이다. 그래서 글자 수가 늘어도 비동기 경합이 늘지 않고, 연속 영문(`API`)이 자연스럽다.

부수 효과로 **소문자는 글자별 manipulator 가 필요 없다** — 누른 순간 이미 영문 입력소스라 매핑이 없는 키도 영문으로 나간다. 숫자·기호가 manipulator 0건으로 덮이는 것이 그 덕이다. (대문자는 사정이 다르다 — 설계 요점 4 참조)

## 2. space + backspace 선행 — 조합중 글자 살리기

한글은 다음 글자의 초성이 와야 앞 글자가 확정된다. `아` 를 친 직후(조합중)에 입력소스를 바꾸면 IME 가 그 조합을 **커밋하지 않고 버린다** — `아` 가 사라지고 영문만 남았다.

`spacebar`(조합 확정 + 공백) → `delete_or_backspace`(그 공백 제거) 를 전환보다 **먼저** 보내 해결한다. 조합중이 아니면 순 효과 0.

⚠️ **Karabiner 에는 IME 조합 상태를 볼 조건이 없다**(지원 조건 7종에 preedit 개념 없음). 그래서 조건부가 아니라 **무조건** 보낸다 — Keyboard Maestro 에서 쓰던 방식과 같다.

## 3. 레이어 키 2분기 — 모디파이어 소비

`Insert` manipulator 가 둘인 이유는 하나다. `⇧space` 가 이 환경의 **한/영 전환 단축키**라, 우리가 보내는 `spacebar` 에 눌린 ⇧ 가 얹히면 전환이 한 번 더 일어나 꼬인다.

| # | `from.modifiers` | 역할 |
| :- | :--- | :--- |
| 1 | `{"mandatory": ["any"]}` | 눌린 모디파이어를 **소비** → space 는 언제나 맨 space |
| 2 | (없음) | 모디파이어 없이 눌린 경우 |

`mandatory` 소비는 **그 manipulator 의 출력에서만** 일어난다. 물리 ⇧ 는 계속 눌린 상태라 뒤따르는 글자는 정상적으로 대문자가 된다.

* ⇧ 만이 아니라 `any` 로 잡았다 — `⌘space`·`⌃space`·`⌥space` 도 전부 입력소스 전환 계열 단축키다
* ❌ **레이어 키를 `optional: ["any"]` 로 되돌리지 말 것** — 그 순간 3번 실패가 재발한다

## 4. 레이어 안에서만 `Home` 을 가로챈다 — 대문자 토글

`⇧`+`Insert`+글자는 **오른손이 Insert 를 잡은 채 ⇧ 까지 눌러야** 해서 대문자 입력 효율이 안 났다(2026-08-07 사용자 지적).

해법은 **키를 빼앗지 않는 것**이다. `Home` manipulator 는 `variable_if keyboardLayoutSettingIsEng == 1` 조건이 붙어 **Insert 를 누르고 있을 때만** 발동한다. 레이어 밖에서 `Home` 은 100% 평소대로다 — 영구히 희생되는 키가 **0** 이다.

| | |
| :--- | :--- |
| 조작 | `Insert` 홀드 → `Home` **탭** → 글자들 → (`Home` 탭으로 해제) → `Insert` 뗌 |
| 수단 | 변수 `engCharUpper` 토글 + 알파벳 26 manipulator 가 `modifiers: ["left_shift"]` 를 붙여 송출 |
| 이득 | 3키 홀드 → **1키 홀드 + 1탭**. `API`·`URL` 같은 연속 대문자에 특히 유리 |

* 트리거로 `Home` 을 고른 근거: Insert 바로 **오른쪽 이웃**이고, 레이어 중에 커서를 줄 앞으로 보낼 일이 없다. 전수 조사 결과 이 프로필에 **영구로 내줄 수 있는 빈 키가 없었고**(nav 클러스터 전부 사용 중, 완전히 빈 키는 숫자패드뿐), 그래서 "빼앗지 않고 레이어 안에서만 빌린다"로 방향을 틀었다
* ⚠️ **`engCharUpper` 는 진입·이탈 양쪽에서 0 으로 리셋한다.** 한쪽만 두면 대문자 상태가 다음 레이어 진입까지 새어 나간다

### ❌ `sticky_modifier` 는 안 된다 (2026-08-07 실측)

처음엔 `{"sticky_modifier": {"left_shift": "toggle"}}` 로 만들었다. 문법상 유효하고 lint 도 통과하지만, 실기에서 **첫 글자만 대문자가 되고 두 번째부터 소문자**로 돌아왔다 — Karabiner 의 sticky modifier 는 이름과 달리 **one-shot** 이라 다음 키 하나에만 붙고 스스로 풀린다.

그래서 **변수 + 글자별 manipulator** 로 바꿨다. 이 규칙이 자랑하던 "글자별 manipulator 0건"을 여기서 포기한다 — 알파벳 26건이 늘지만, 연속 대문자가 실제로 동작하는 쪽이 옳다. 설계 요점 1의 "매핑 없는 키도 영문으로 나간다"는 **소문자에 한해** 여전히 유효하다(숫자·기호는 manipulator 없이 그대로 나간다).

* ⚠️ **다시 `sticky_modifier` 로 되돌리지 말 것.** lint 를 통과해서 옳아 보이지만 실기에서 한 글자만 먹는다

# 왜 `insert` 인가

트리거 후보 6종(오른쪽 ⌘·⌘⇧·오른쪽 ⌥·한/영 홀드·한/영 모아치기·`fn`)이 전부 기각된 끝에 남은 키다. 사유는 [forTest/z_old/README.md](forTest/z_old/README.md).

| 근거 | 실측 |
| :--- | :--- |
| 기존 규칙 점유 0 | n3sh 254행 · FootPedal · 12Key2Knob · RemoteDesktop 전수 `insert` 0건 |
| macOS 기본 기능 없음 | 잃는 기능이 없다 (`fn` 안은 `fn`+F키·방향키를 통째로 희생해야 했다) |
| device 리매핑 없음 | `insert` 를 `from` 으로 쓰는 simple_modification 0 — complex 규칙에 그대로 도달 |
| 한/영 키 무간섭 | 가장 많이 치는 키의 감각이 그대로 |

# n3sh 와의 관계

홀드 중 `keyboardLayoutSettingIsEng = 1` 로 올린다. [n3sh](../n3sh/README.md) 254 manipulator **전부**가 `variable_if keyboardLayoutSettingIsEng == 0` 을 조건으로 달고 있어, **영문 레이어 동안 n3sh 가 통째로 잠긴다.**

이 변수는 n3sh 에 처음부터 있었으나 **어디서도 1로 세팅되지 않던** 미배선 off 스위치였다(2026-08-07 실측, `set_variable` 0건). 본 규칙이 그 스위치의 첫 사용처다.

# 공개

`device_if` 0 · `shell_command` 0 인 순수 키매핑이라 [FootPedal](../footPedal/README.md) 과 같은 경로로 pqrs 등록이 가능하다. 다만 한국어 입력소스 전용이라 대상이 좁고, `⇧space` 전환키 전제가 환경 의존이다 — [RemoteDesktop](../remoteDesktop/README.md) 과 묶는 안이 검토 중이다.

# 의존성 (ke-sync 자동 생성)

<!-- ke-sync:begin -->
<!-- 이 블록은 tools/ke_sync.py 가 생성합니다. 직접 수정하면 다음 apply 때 덮어써집니다. -->

| 항목 | 값 |
| :--- | :--- |
| manipulator 총 수 | 30 |
| type 분포 | `basic` 30 |
| `device_if` 의존 | 0 |
| 대상 장치 | 없음 (하드웨어 비의존) |
| `shell_command` 의존 | 0 |
| 순수 키매핑 (장치·외부앱 비의존) | 30 |

* 원본: [rule.json](rule.json) → `(profile 없음 — rule 단위 원본)` → rule `Eng Char on Kor : v2026.08.07`
* 아티팩트: 없음 — 원본이 rule 단위라 추출본을 두지 않는다
* 원본 rule 다이제스트(sha256 앞 12): `82f1a68f05cd`
<!-- ke-sync:end -->
