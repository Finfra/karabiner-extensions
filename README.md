---
name: Extensions
description: Builded Extension 5종의 폴더별 진입점 인덱스 — 이름·설명·배포 파일 링크
date: 2026.08.06
---

> 📦 **이 저장소는 파생본이다.** 정본은 비공개 작업 저장소(Karabiner-Elements 규칙 관리)에 있고,
> 여기 있는 것은 거기서 생성된 공개 사본이다 — `tools/build_public.py` 가 만든다.
> 본문에 백틱으로 적힌 경로(ex `data/rule_source.yaml`)는 **그 작업 저장소 안의 위치**이며
> 이 저장소에는 존재하지 않는다. 링크로 걸린 것만 여기서 열린다.


# 목적

이 프로젝트가 만든 Karabiner-Elements complex_modifications 규칙(**Builded Extension**)마다 폴더를 하나씩 두고, 그 규칙의 구현 파일·설정·데이터가 어디 있는지를 각 폴더 [README.md](.) 가 가리킨다.

기존에는 규칙별 구성·설계 파일이 `karabiner_json` · `data` · `_doc_base/builded_extensions` 세 곳에 흩어져 있었고, 그 흩어짐을 견딜 수 있었던 것은 `data` 를 통째로 쓰는 NowageShorthand 뿐이었다. 나머지 4종은 진입점이 없었다.

> ⚠️ **여기는 색인이지 정본이 아니다.** manipulator 수·규칙 내용·통계는 각 정보 파일의 `ke-sync` 관리 블록이 기계로 산출하는 것이 정본이다(`tools/ke_sync.py`). 이 폴더의 문서에 그 수치를 옮겨 적지 않는다 — 옮겨 적은 숫자는 반드시 낡는다(Issue22·Issue45 에서 실제로 겪음).

# Builded Extension 목록

| no  | 코드명        | 이름                                     | 설명                                                            | 배포 파일 (라이브에 올라가는 것)                                                             | 상태                      |
| --- | ------------- | :--------------------------------------- | :-------------------------------------------------------------- | :------------------------------------------------------------------------------------------- | :------------------------ |
| 1   | footPedal     | [FootPedal](footPedal/README.md)         | USB 3페달 풋스위치 — 편집·탐색·미디어 3계층 × 모디파이어 6층    | [footPedal/rule.json](footPedal/rule.json)                                                   | ✅ 라이브 · pqrs 공개 등록 |
| 2   | 12Key2Knob    | [12Key2Knob](12Key2Knob/README.md)       | 12키+2노브 매크로패드 — Keyboard Maestro 매크로 트리거          | [12Key2Knob/rule.json](12Key2Knob/rule.json)                                                 | ✅ 라이브 · 실사용 중      |
| 3   | remoteDesktop | [RemoteDesktop](remoteDesktop/README.md) | MS 원격 데스크톱 한정 alt↔command 스왑 + 한/영 전환             | [remoteDesktop/rule.json](remoteDesktop/rule.json)                                           | ✅ 라이브                  |
| 4   | n3sh          | [NowageShorthand](n3sh/README.md)        | n3sh 세벌식 390 속기 — 자모 조합으로 완성형 단어·구 산출        | ⚙️ 생성물 `Extensions/n3sh/build/n3sh-{390,final}.json` — 만드는 것은 `tools/gen_rules.py`   | ✅ 라이브 — 프로젝트 본체  |
| 5   | engCharOnKor  | [EngCharOnKor](engCharOnKor/README.md)   | 한글 모드에서 `Insert` 를 누른 동안만 영문 입력 (모드 전환 없이) | [engCharOnKor/rule.json](engCharOnKor/rule.json)                                             | ✅ 라이브 (2026-08-07)     |

* **배포 파일**은 `~/.config/karabiner/karabiner.json` 에 실제로 올라가는 소스다. 넷은 rule 단위 원본이 곧 배포본이고, **n3sh 만 생성 산출물**이다
* ⚠️ **n3sh 칸만 링크가 아닌 이유** — `Extensions/n3sh/build/` 는 `.gitignore` 대상이라 clone 직후에는 **존재하지 않는다.** 추적되는 색인이 untracked 생성물로 링크를 보내면 남의 저장소에서 죽은 링크가 되고, 로컬에는 파일이 있어 링크 검사도 그것을 잡지 못한다. 그래서 경로는 평문으로 적고 링크는 **그것을 만드는 도구**로 보낸다
* 공개(pqrs 등록) 여부는 각 폴더 README 의 "공개" 절 참조. 현재 등록된 것은 FootPedal 1건

# 폴더 구조 규약

```
Extensions/
├── Extensions.md          # 본 문서 — 전체 색인
└── {코드명}/
    ├── README.md          # 그 규칙의 진입점: 개요 + 파일 위치표 + 상태
    └── core/ · layout/ · _doc/   # 그 규칙 전용 자산 (현재 n3sh 만 보유)
```

* **폴더명 = 위 목록표의 코드명 그대로**(기본 camelCase, ex: `n3sh`). 목록표 **코드명** 컬럼이 정본이며, 폴더명을 바꾸면 목록표도 같은 커밋에서 바꾼다
    - 예외: **장치 이름이 숫자로 시작하면 그 이름을 그대로 쓴다** — `12Key2Knob`. 읽는 사람이 아는 이름은 장치 이름이지 그것을 camelCase 로 비튼 형태가 아니다(2026-08-08 개명. 구 `nowageCustom`)
* ❌ **번호 접두를 붙이지 않는다** — 여기서 말하는 번호 접두는 `01_`·`2-` 같은 **정렬용 접두**다. `12Key2Knob` 의 `12` 는 정렬 번호가 아니라 장치 이름의 일부라 해당 없다. 규칙별 자산 폴더와 1:1 로 맞추려면 이름이 코드명 하나로 고정돼야 하고, 정렬 순서는 목록표의 `no` 가 갖는다
* 규칙 전용 데이터가 생기면 그 폴더 아래 두고 README 파일 위치표에 등록한다. 현재 그런 규칙은 n3sh 하나다(2026-08-06 Issue84 로 `data` 에서 이관)
* ⚠️ **도구는 내리지 않는다** — 공통이든 특정 규칙 전용이든 코드는 전부 `tools` 다. 공통 도구 3종은 애초에 어느 Extension 폴더에도 못 들어가고, 둘로 쪼개면 도구를 찾는 자리가 두 곳이 된다

# 공통 자산

모든 Builded Extension 이 함께 쓰는 것들. 규칙별 폴더에 복제하지 않는다.

> 📦 `rule.json`(rule 단위 정본)과 `info.md`(`ke_sync` 결속)는 2026-08-06(Issue84)부터 **각 Extension 폴더**에 있다 — 더 이상 공통 자산이 아니다.

| 자산                                                                                | 역할                                                     |
| :---------------------------------------------------------------------------------- | :------------------------------------------------------- |
| `karabiner_json/_indivisual/snapshot`     | 라이브에서 뜬 대조용 스냅샷                              |
| `karabiner_json/_orignal_do-not-update` | 전체 config 백업 (수정 금지)                             |
| `data/rule_source.yaml`                                   | 받은 것 / 만든 것 분류 + 공개 판정 SSOT                  |
| `data/devices.json`                                           | 장치 식별자(vendor_id·product_id) 정본                   |
| `tools/ke_sync.py`                                   | md ↔ JSON 드리프트 검출 (`/ke-sync`)                     |
| `tools/ke_deploy.py`                               | 라이브 config 와 의미 diff + 안전 적용 (`/ke-deploy`)    |
| `tools/ke_formatter.py`                         | manipulator 1건 = 1행 한 줄 포맷터                       |
| `pqrs_submission`                                             | pqrs 공개 등록본·제출 절차                               |

# 경로 이전 대응표 (2026-08-06 Issue84 · 2026-08-08 Issue87)

완료된 이슈 기록·아카이브(`_doc_work/z_done/`)·오라클은 **그 시점의 사실**이라 고치지 않았다. 거기서 옛 경로를 만나면 아래로 읽는다.

| 옛 경로 | 현재 |
| :--- | :--- |
| `data/core/**` | `Extensions/n3sh/core/**` |
| `data/layout/**` | `Extensions/n3sh/layout/**` (Issue84 로 `Extensions/n3sh/data/layout/` → Issue87 로 한 겹 승격) |
| `Extensions/n3sh/data/layout/**` | `Extensions/n3sh/layout/**` |
| `data/fsnippet/` · `Extensions/n3sh/data/fsnippet/` | `Extensions/n3sh/_doc/n390/` |
| `…/layout/{n390,final}/rules_notes.md` | `Extensions/n3sh/_doc/{n390,final}/rules_notes.md` |
| `…/layout/{n390,final}/CHANGELOG.md` | `Extensions/n3sh/_doc/{n390,final}/CHANGELOG.md` |
| `…/layout/rules_notes_intersection.md` | `Extensions/n3sh/_doc/rules_notes_intersection.md` |
| `…/layout/notation.md` | `Extensions/n3sh/_doc/notation.md` |
| `data/forTest/` | `Extensions/n3sh/z_done/forTest/` |
| `data/core/devices.json` | `data/devices.json` (공유라 잔류) |
| `data/core/schema/devices.schema.json` | `data/schema/devices.schema.json` |
| `data/tools/**` | `tools/**` |
| `karabiner_json/_indivisual/org/{name}.json` | `Extensions/{코드명}/rule.json` |
| `_doc_base/builded_extensions/{name}.md` | `Extensions/{코드명}/info.md` |
| `Extensions/README.md` | `Extensions/Extensions.md` |
| `Extensions/nowageCustom/**` | `Extensions/12Key2Knob/**` (2026-08-08 명칭 통일) |
| `_indivisual/snapshot/12key2knobe.json` | `_indivisual/snapshot/12Key2Knob.json` |
| rule 표시명 `12key+2knobe : v2024.03.10` · 정본 description `Nowage Custom : Combo V2024.03.10` | `12Key2Knob : v2024.03.10` |

* 이동 판정 기준·불변식: `_doc_arch/extension-layout-design.md`
* 이동하지 **않은** 것: `karabiner_json/_indivisual/snapshot/` · `_orignal_do-not-update/`(오라클) · `Extensions/n3sh/build/`(생성 산출물)

# 신규 Extension 추가 절차

1. `Extensions/{코드명}/README.md` — 본 폴더 규약대로 진입점 작성 (목록표에는 마지막 `no` +1 로 행 추가)
2. `karabiner_json/_indivisual/org/{name}.json` — rule 단위 정본 (`{"title":…, "rules":[{"description":…, "manipulators":[…]}]}`)
3. `_doc_base/builded_extensions/{kebab-name}.md` — frontmatter `ke_sync.rule_description`(원문 그대로) + `source_json`
4. `data/rule_source.yaml` `만든_것` 에 항목 추가
5. `_doc_base/builded_extensions/README.md` 경로표·목록표 갱신 + 본 문서 목록표에 행 추가
6. `python3 tools/ke_sync.py apply` → `check` 가 exit 0 인지 확인
7. 라이브 반영은 `/ke-deploy` (백업·lint·확인 게이트 경유)

공개까지 갈 경우 `pqrs_submission/json/nowage_{name}.json` + `extra_descriptions/*.html` + `karabiner_cli --lint-complex-modifications` 통과. 절차: `pqrs_submission/README.md`

# 관련

* 규칙 정보 파일 인덱스: `_doc_base/builded_extensions/README.md`
* 분류 배경: `_doc_base/background/rule-classification.md`
* 프로젝트 개요: `CLAUDE.md` · 이슈: `Issue.md`
