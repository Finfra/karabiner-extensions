---
name: CHANGELOG
description: "n3sh 최종식 판 배포 이력 — VERSION 갱신 시 한 줄씩 추가"
date: 2026.08.02
---
# n3sh-final 배포 이력

* 2026.07.26 — 생성 기준선 (`build/n3sh-final.json`, 최종식 오라클 대조 기준 — Issue11 이중 산출 검증)
* 2026.08.02 — Intersection 방식 전환: 배열별 rules.md 완전 정본화(final 230행 — 역사 기준·keymap 학습 소스). 빌드 산출 불변(228 manip)
* 2026.08.02 — Issue36 `기호` 열 라벨 스왑 60건(`⇧`↔`⇧⌘` 의 `!`/`?`). **최종식 실출력은 실측 미확보** — `기호` 가 keymap tail 복합키의 일부이고 본 판이 두 배열의 학습 소스라, n390 만 고치면 조회가 깨져(생성실패 45건) 함께 스왑한 것이다. 키열 불변으로 빌드 산출 228 manip 유지
