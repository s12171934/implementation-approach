---
title: implementation-approach
created: 2026-10-16
updated: 2026-10-16
tags: [domain/인공지능, area/ai에이전트, topic/오케스트레이션]
source: ai
---

# implementation-approach

> 구현 작업을 시작하기 전에, 그 작업을 에이전트에게 어떤 **구현 방식**으로 나눠 돌릴지 — 또는 방식 없이 진행할지 — 를 고르는 에이전트 스킬이다.
> 에이전트는 카탈로그를 읽고 권장안을 제시할 뿐이고, 결정은 언제나 사용자가 한다.

## 설치

에이전트 도구의 스킬 디렉터리에 clone 하거나, clone 한 곳을 스킬 디렉터리에 링크한다.

```bash
git clone https://github.com/s12171934/implementation-approach.git ~/.claude/skills/implementation-approach
# 또는: ln -s <clone 경로> ~/.claude/skills/implementation-approach
```

다른 스킬과의 연동(선택): `orca-work-placement`, `orca-orchestration-rules`, `claude-usage-check`, `gh-stack`, `vault-entry`, `vault-write-boundary`. 방식 문서가 이 스킬들을 이름으로 가리킨다.

## 구성

- `SKILL.md` — 진입점. 적용 조건, 카탈로그 찾기, 선택·선언 절차.
- `references/구현 방식 카탈로그.md` — 등록된 방식 목록과 선택 규칙, 방식 문서 양식 (SSOT).
- `references/티켓 체크박스 커밋 리뷰 방식.md` — 등록된 방식 「티켓 체크박스 커밋 리뷰」의 허브 문서.
- 그 방식이 돌리는 루프와 세부 규칙
    - `references/티켓 체크박스 커밋 리뷰 루프.md` — 루프의 순서와 목차
    - `references/티켓 체크박스 커밋 리뷰 배치 단위.md`
    - `references/티켓 체크박스 커밋 리뷰 에이전트 구성.md`
    - `references/티켓 체크박스 커밋 리뷰 사용량 게이트.md`
    - `references/티켓 체크박스 커밋 리뷰 라운드.md`
    - `references/티켓 체크박스 커밋 리뷰 커밋과 지라 갱신.md`
    - `references/티켓 체크박스 커밋 리뷰 볼트 기록 규격.md`
    - `references/구현 검증 결과 재사용.md`
    - `references/코디네이터 호출 규율.md`

## 공개 면

- 스킬 이름 `implementation-approach` 만 공개 면이다. `references/` 는 내부 전용이라 예고 없이 바뀔 수 있다.
- 개정 이력은 git 커밋이 갖는다.
