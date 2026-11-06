# MARCH 개발 흐름

| 브랜치 | 용도 |
| --- | --- |
| `main` | 기본 브랜치. 릴리스할 변경을 `dev`에서 PR로 가져옴 |
| `dev` | 통합 브랜치. 기능 PR을 모아 다음 릴리스를 준비 |
| `feat/<작업명>` | `dev`에서 분기하는 작업 브랜치 |

```bash
git fetch origin
git switch -c feat/archive-search origin/dev
# 변경하고 커밋한 후
git push -u origin feat/archive-search
```

1. 기능 PR은 `feat/* → dev`로 연다. 이슈나 요구사항, 바뀐 계약, 검증 결과를 PR에 적는다. 여러 작업 커밋은 필요하면 squash한다.
2. 릴리스 PR은 같은 저장소의 `dev → main`으로 연다. 변경 목록과 통합 검증 결과를 적고 merge commit으로 합친다.

`main`과 `dev`는 PR과 `verify` 통과, 대화 해결이 필요하다. 직접 push·강제 push·삭제를 제한한다. 1인 초기 운영을 위해 승인 인원 최소값은 0명이다. 현재 `verify`는 PR 경로, README, 변경 공백을 검사한다. 실행 코드 이전 시 BE의 API·DB, FE의 화면·상태, AI의 스키마·근거 검사를 각 저장소 CI에 연결한다.

GitHub Actions는 PR이 열리거나 업데이트될 때 테스트 병합 커밋을 `verify`로 검사한다. 브랜치 반영 후 또는 **Actions → CI → Run workflow**에서 실행하는 `smoke`는 저장소 기본 검사다.
