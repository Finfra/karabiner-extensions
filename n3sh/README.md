---
name: README
description: NowageShorthand(n3sh) 진입점 — 이 프로젝트의 본체이자 유일하게 데이터 파이프라인 전체를 쓰는 Extension
date: 2026.08.06
---

> 🌐 **pqrs 공개 등록** (PR #2001 · 2026-08-30) — [커뮤니티 카탈로그]([https://ke-complex-modifications.pqrs.org/?q=nowage_n3sh_390](https://ke-complex-modifications.pqrs.org/?q=n3sh))에 올라가 있다.

> 📖 **배우려면 → [n3sh 문서 사이트](https://finfra.github.io/karabiner-extensions/)**
> 설치 → 치트시트 → 6단계 드릴 → 규칙표 순으로 읽게 되어 있고, **바로 넣을 수 있는 규칙 파일**을 거기서 받는다.
> 아래는 규칙 자체의 설명이고, 이 폴더의 나머지는 저장소 작업자를 위한 것이다.

# 무엇을 하는 규칙인가

세벌식 390 자판에서 **자모 2개를 동시에 누르면 완성형 한 글자가 한 번에 나오게 한다.** 자주 나오는 글자를 2타로 줄인다. 250여가지 규칙이 들어 있다.

| 누르면    | 나온다 | 일반 타건        |
| :-------- | :----- | :--------------- |
| `j` + `h` | 을␣    | 4타 (ㅇ ㅡ ㄹ ␣) |
| `y` + `u` | 를␣    | 4타              |
| `h` + `l` | 는␣    | 4타              |
| `k` + `m` | 고␣    | 3타 (ㄱ ㅗ ␣)    |
| `j` + `i` | 있     | 3타 (ㅇ ㅣ ㅆ)   |

* **조사·어미는 뒤 공백까지 함께 나온다**(`sp`) — 그래서 `을`·`는`·`를` 의 일반 타건은 자모 3타에 스페이스를 더해 4타다. `있` 처럼 공백이 안 붙는 규칙은 3타
* **순서는 무관하다** — 모아치기(동시타)라 `j`+`h` 든 `h`+`j` 든 같다. 문서의 열 순서는 읽기 편의일 뿐
* 모디파이어(`⇧`·`⌘`·`⌥`)로 층을 나눠 같은 자리에 다른 글자를 얹는다
* 나오는 것은 대부분 **한 글자**다 — 조사·어미·받침 있는 글자. 여러 글자가 나오는 규칙은 2건뿐이라 "단어를 펼치는" 도구는 아니다

## 쓰려면 무엇이 필요한가

| 조건                | 비고                                                                                                                    |
| :------------------ | :---------------------------------------------------------------------------------------------------------------------- |
| **세벌식 390 배열** | 두벌식에서는 동작하지 않는다. 자모의 물리 위치가 규칙의 전제다                                                          |
| **한글 입력 상태**  | `keyboardLayoutSettingIsEng == 0` 일 때만 발동한다                                                                      |
| ⚠️**외우는 시간**    | 254개는 설치해서 바로 쓰는 분량이 아니다.[학습 단계](layout/n390/rules_step.md)가 예비·1~6단계 커리큘럼으로 나뉘어 있다 |

> 10년 넘게 개인 환경에서 굴려 온 체계다. 조사·어미부터 익히면(2단계) 나머지를 몰라도 이득이 나오게 단계를 짰다.

# 이 폴더의 구조 (저장소 작업자용)

라이브 rule 이름은 `n3sh(Nowage ShortHand for 3set 390) : v2026.08.30` 이다 — 버전은 [layout/n390/VERSION](layout/n390/VERSION) 이 SSOT 이고 `emit.rule_description` 이 각인한다(옮겨 적은 값은 낡으므로 그 파일을 본다).

**이 Extension 만 전용 데이터를 갖는다.** 사람 정본 md 는 [layout/](layout), 생성 JSON·스키마는 [core/](core), 도구가 열지 않는 문서는 [_doc/](_doc), 포매터 정렬 원형은 [z_done/forTest/](z_done/forTest) 에 **아카이브**돼 있다(소비처 0건, 2026-08-08). 나머지 4종은 rule JSON 과 정보 md 뿐이다.

> 📦 **역할 3분할** (2026-08-08) — `layout/`(입력) · `core/`(출력) · `_doc/`(문서). 판정 한 줄: **프로그램이 이 파일을 여는가.** 열면 `layout/`, 안 열면 `_doc/`. 전에는 셋이 `data/` 한 폴더에 섞여 있어 폴더만 보고는 손으로 고쳐도 되는지 알 수 없었다.

> 📌 본 문서는 **링크 모음**이다. 규칙 내용·건수·설계 근거는 링크 대상이 정본이며 여기에 옮겨 적지 않는다 — 옮겨 적은 숫자는 반드시 낡는다.

# 어디를 봐야 하나

| 알고 싶은 것                       | 문서                                                                            |
| :--------------------------------- | :------------------------------------------------------------------------------ |
| 데이터 문서 전체 색인              | [layout/README.md](layout/README.md)                                            |
| 규칙 정본 (390 / 최종식)           | [n390/rules.md](layout/n390/rules.md) · [final/rules.md](layout/final/rules.md) |
| 현행 규칙 서술                     | [n390/rules_notes.md](_doc/n390/rules_notes.md)                                 |
| 학습 단계 정의                     | [n390/rules_step.md](layout/n390/rules_step.md)                                 |
| 대기 중인 규칙 (추가·수정·미정)    | [n390/staging.md](layout/n390/staging.md)                                       |
| 비워 두기로 한 자리                | [n390/rules_prohibit.md](layout/n390/rules_prohibit.md)                         |
| 표기 규약 (`—`·`␣`·`~` 등)         | [notation.md](_doc/notation.md)                                                 |
| 자판 배열                          | [keymap.md](layout/keymap.md)                                                   |
| 파이프라인 설계 (md → JSON → rule) | `_doc_arch/data-pipeline-design.md`              |
| 데이터 편집 규약                   | `.claude/rules/data-md-first-rules.md`            |
| 규칙 정보 파일 (ke_sync 결속)      | [nowage-shorthand.md](info.md)                                                  |

# 파일 위치

| 구분                           | 경로                                                                                                                  |      편집      |
| :----------------------------- | :-------------------------------------------------------------------------------------------------------------------- | :------------: |
| 사람 정본 (md — 도구가 읽는다) | [layout/](layout) — 배열별 `n390/` · `final/`                                                                        |       ✅        |
| 문서 (도구가 열지 않는다)      | [_doc/](_doc) — 색인 [_doc/README.md](_doc/README.md)                                                                |       ✅        |
| 데이터 (생성 JSON)             | [core/](core)                                                                                                        |    ❌ 생성물    |
| 스키마                         | [core/schema/](core/schema)                                                                                          |       ✅        |
| 포매터 정렬 원형               | [z_done/forTest/](z_done/forTest) — before/after 픽스처                                                              |   📦 아카이브   |
| 파이프라인 도구                | `tools` — **Extension 밖**(코드는 인스턴스를 따라가지 않는다)                                          |       ✅        |
| **배포 파일**                  | ⚙️`build/n3sh-{390,final}.json` — gitignore 라 clone 직후엔 없다. 만드는 것은 `tools/gen_rules.py` |    ❌ 생성물    |
| rule 단위 원본                 | [rule.json](rule.json) — 2022 오라클 스냅샷(227)                                                                      | 📦**수정 금지** |

> ⚠️ **이 규칙만 `rule.json` 이 라이브가 아니다.** 라이브는 `build/` 생성 산출물이고(`b869835` 에서 배포 소스를 재지정), `rule.json` 은 2026-06-03 오라클에서 뜬 **227 스냅샷**이다. 나머지 4종은 `rule.json` 이 곧 라이브라 편집 대상이지만 여기서는 아니다.
>
> 그래서 `tools/gen_indivisual.py` 가 n3sh 만 `compare_org: False` 로 회귀 대조에서 **명시적으로 제외**한다 — 대조하면 영구 NG 다. 라이브 정합은 `ke_deploy diff` 가 본다. 이 불일치는 몰라서 남은 것이 아니라 **알고 제외한 것**이며, 발단은 조사였다.

> 📦 데이터가 `data/` 에서 이 폴더로 온 것은 2026-08-06이다. 공유 자산(`rule_source.yaml`·`devices.*`)은 여전히 `data` 에 있다 — 소비자가 여럿이기 때문이다. 판정 기준: `_doc_arch/extension-layout-design.md`

# 주요 명령

```bash
python3 tools/md_to_json.py build     # md → JSON 재생성
python3 tools/md_to_json.py check     # md ↔ JSON 정합 (exit 0 이어야 함)
python3 tools/gen_rules.py            # 규칙 → Karabiner JSON 생성 + 오라클 대조
python3 tools/validate_schema.py      # 스키마 검증
python3 tools/validate_cross.py       # 파일 사이의 모순 검출
python3 tools/validate_docs.py        # 파급 문서의 기계적 주장 대조
python3 tools/verify_layout.py        # 폴더 구조 — 옛 경로·링크·build 해시
/ke-deploy                                 # 라이브 반영 (백업·lint·확인 게이트)
```

* 위 명령은 **저장소 루트에서** 실행한다(경로가 루트 기준)

# 공개

| 대상                   | 상태                                                                                                                                                             |
| :--------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **GitHub**             | ✅ 공개 —[finfra/karabiner-extensions](https://github.com/Finfra/karabiner-extensions) (2026-08-09)                                                      |
| **pqrs 등록 (390)**    | ✅ **등록 완료** (2026-08-30, PR [#2001](https://github.com/pqrs-org/KE-complex_modifications/pull/2001)) — `international` 그룹. 주소는 이 문서 상단 |
| **pqrs 등록 (최종식)** | ⏸️ **요청이 있을 때만** — 390 이 등록됐으니 조건은 이제 *쓰겠다는 사람이 나타나는 것* 하나다. 그때 **별도 프로젝트로 독립시켜** 공개한다                          |

* **최종식(final)을 함께 내지 않는 이유** — 배열 사용자가 소수라 수요가 확인되지 않은 채로 내면 유지 부담만 남는다. 390 과 한 규칙에 묶어 내는 것도 하지 않는다 — 배열이 다르면 눌리는 키가 다르고, 한 항목이 두 배열을 겸하면 어느 쪽 사용자에게도 맞지 않는다. 요청이 오면 이 저장소에서 떼어 **독립 프로젝트**로 세운다
* **왜 그동안 내지 않았는가** — 받아 줄 문서가 없었다. n3sh 는 세벌식 390 자판과 254 규칙을 전제하는 대규모 규칙이라, 등록 페이지 한 칸으로는 쓰는 사람이 *무엇을 눌러야 하는지* 알 수 없고 물어볼 곳도 고칠 곳도 없었다
* **왜 이제 냈는가** — 로 공개 저장소와 문서 트리가 섰다. 자판·학습 단계·규칙표를 GitHub 문서가 받으므로 `extra_descriptions` 는 요약과 링크만 담으면 됐다
* **등록 후 이름 정리** (2026-08-30, PR [#2002](https://github.com/pqrs-org/KE-complex_modifications/pull/2002) 심사 중) — 받는 사람의 Complex Modifications 목록에 뜨는 것은 rule `description` 한 줄뿐인데 거기에 설명문을 넣어 문단이 펼쳐졌다. 이름·출처·버전만 담는 한 줄로 바꿨고, 설명은 `extra_descriptions` 가 맡는다
* ⚠️ 구조상의 결격은 **아니었다** — 이 규칙도 `rules` 1건(manipulator 227개)이라 pqrs 에 등록된 [FootPedal](../footPedal/README.md)(1건·18개)과 같은 형태다. 종전 "1건 단위 체계에 맞지 않는다" 는 서술은 사실이 아니라 지어낸 것이었다(2026-08-09 정정)
* 판정 근거: `data/rule_source.yaml` `만든_것` · 관련 이슈 · ·
