---
name: implementation-approach
description: >-
  Picks which implementation orchestration approach — if any — a coding task should follow.
  Load it at the start of an implementation task (writing or changing code), before the work
  is dispatched, and whenever the user points at it or names an approach document. It defines
  no approach of its own: it reads the catalog bundled with this skill
  (`references/구현 방식 카탈로그.md`) and returns exactly one registered approach or the
  explicit "선택하지 않음" outcome for work that does not need one. The agent never settles
  this alone — it proposes a recommendation and the user picks before any work starts. Not for
  research, Q&A, document work, or read-only analysis.
---

# 구현 방식 선택 (implementation-approach)

> 구현 오케스트레이션 **방식 문서 묶음의 선택기**다. 방식 자체는 여기 적지 않는다.
> 방식 목록·선택 규칙·각 문서의 양식은 이 스킬에 함께 있는 `references/구현 방식 카탈로그.md` 가 SSOT다.
> 이 파일은 그 카탈로그로 가는 포인터이며, 규칙을 복제하지 않는다.

## 1. 적용 조건 — 구현 작업일 때

- 코드를 만들거나 고치는 **구현 작업**에서 로드한다. 착수 전에 방식을 정하는 것이 이 스킬의 자리다.
- 사용자가 이 스킬·카탈로그·개별 방식 문서를 지목하면 작업 종류와 무관하게 로드한다. 지목이 우선한다.
- 대상이 아닌 일 — 조사·질문 답변·문서 작업·읽기 전용 분석·단순 명령 실행.
- **로드가 곧 방식 적용은 아니다.** §3 의 결과에는 "선택하지 않음"이 있고, 그것도 정상적인 결론이다.
- **방식은 에이전트가 확정하지 않는다.** §3 대로 사용자의 선택을 받은 뒤에야 구현에 착수한다.
- 방식을 적용하든 하지 않든 결론은 §4 대로 한 줄 밝힌다. 조용히 넘어가지 않는다.

## 2. 카탈로그 찾기

- 카탈로그와 방식 문서는 이 스킬 디렉터리의 `references/` 에 있다. 이 `SKILL.md` 는 도구 스킬 경로에 심볼릭링크로 걸려 있을 수 있으므로 실제 경로를 해석해서 찾는다.

```bash
skill_file="<이 SKILL.md 가 로드된 경로>"
skill_dir="$(cd "$(dirname "$(readlink -f "$skill_file")")" && pwd -P)"
catalog="$skill_dir/references/구현 방식 카탈로그.md"
```

- `readlink -f` 가 없는 환경이면 `python3 -c 'import os,sys;print(os.path.realpath(sys.argv[1]))' "$skill_file"`.
- 방식 문서 안에서 다른 방식 문서를 제목으로 가리키는 링크는 같은 `references/` 안의 `<제목>.md` 파일을 뜻한다.
- 카탈로그를 못 읽는 표면(파일시스템 접근 없음, 링크 끊김)이면 **방식을 추측하지 않고** 사용자에게 카탈로그 내용을 요청한다.

## 3. 방식 고르기 — 결정은 사용자가 한다

1. 카탈로그의 "선택 규칙"과 "방식 목록"을 읽는다.
2. 이번 작업에 맞는 방식을 **하나**로 좁히거나, 맞는 방식이 없으면 **선택하지 않음**으로 좁힌다. 여기까지가 에이전트의 몫이다.
3. 좁힌 결과를 **권장안으로 제시하고 사용자의 선택을 받는다.** 에이전트가 혼자 확정해 착수하지 않는다 — 선택하지 않음도 마찬가지로 확인을 받는다. 단 하나의 예외는 어느 방식의 전제도 성립할 수 없음이 명백한 경우로, 그 기준과 선언 형식은 카탈로그 "선택 규칙"의 생략 항목이 정한다. 제시 형식(권장안 이유·`선택하지 않음` 포함)도 카탈로그 "선택 규칙"이 SSOT다.
4. 사용자가 이미 방식을 이름으로 지목했으면 그것이 곧 선택이다. 다시 묻지 않는다.
5. 후보가 둘 이상이면 우열을 매기지 말고 나란히 올려 사용자에게 묻는다. 조건이 겹쳤다는 것은 카탈로그가 갱신되어야 한다는 신호이므로 그 사실도 함께 알린다.
6. 사용자가 고른 것이 결론이다. 권장안과 달라도 그대로 따른다.
7. 선택하지 않음으로 결론 나면 방식 없이 평소대로 구현한다. 억지로 끼워 맞추지 않는다.
8. 방식으로 결론 나면 그 문서를 열어 전문을 읽는다 — 카탈로그의 한 줄 설명만 보고 실행하지 않는다.
9. 두 방식을 섞지 않는다. 섞어야 할 것 같으면 그것은 카탈로그에 없는 새 방식이라는 신호다.

## 4. 확인받고, 선언하고, 실행

- **사용자의 선택 전에는 구현에 착수하지 않는다.** 방식이 명백해 보여도 선택 단계를 건너뛰지 않는다 (§3-3 의 생략 예외만 빼고).
- 선택이 끝났으면 실행 전에 한 줄로 밝힌다 — `적용 방식 · 방식 문서 · 고른 이유`.
- 선택하지 않음이면 그것도 한 줄로 밝힌다 — `방식 없이 진행 · 그렇게 판단한 이유`.
- 그 지시가 덮는 범위에 한해 방식 문서를 따른다. 범위를 넘겨 확장하지 않는다.
- 방식 문서가 현실과 어긋나면 임의로 바꿔 실행하지 말고, 어긋난 지점을 보고한 뒤 카탈로그 갱신 여부를 사용자에게 확인한다.

## 5. 다른 룰과의 관계

- 이 스킬은 아래 규칙들을 대체하지 않고 그 위에 얹힌다.
- 워크트리 배치·탭 명명·모델 선택·목표 확정 — `orca-work-placement` 스킬.
- 감독형 오케스트레이션 진입 조건과 코디네이터 의무 — `orca-orchestration-rules` 스킬.
- 볼트 세션이 외부 저장소를 고칠 때의 경계 — `vault-write-boundary` 스킬.
- 볼트 진입과 노트 형식 — `vault-entry` 스킬.
- 명령어와 플래그는 항상 버전 매칭 가이드에서 읽는다. 이 스킬과 방식 문서 어디에도 명령 표면을 옮겨 적지 않는다.
