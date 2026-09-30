# Git 병합 체크리스트

## 1. 브랜치 상태 확인

```bash
git status
git branch
```

커밋하지 않은 변경 사항이 있다면 먼저 정리합니다.

## 2. 병합 대상 브랜치로 이동

```bash
git switch main
```

병합 결과를 받을 브랜치로 이동합니다. 보통 `main` 또는 `develop`이 대상 브랜치입니다.

## 3. 최신 내용 가져오기

```bash
git pull origin main
```

원격 저장소의 최신 커밋을 반영해 불필요한 충돌 가능성을 줄입니다.

## 4. 작업 브랜치 병합

```bash
git merge feature/login
```

Git은 두 브랜치의 변경 이력을 비교합니다.

- **Fast-forward**: 대상 브랜치에 별도 작업이 없어 포인터만 앞으로 이동
- **3-way merge**: 두 브랜치에 각각 커밋이 있어 병합 커밋 생성
- **충돌 발생**: 같은 부분을 다르게 수정해 직접 해결 필요

## 5. 충돌 해결

충돌 파일을 수정한 뒤 다음 명령으로 해결 사실을 알립니다.

```bash
git add <해결한-파일>
git commit
```

병합을 취소하려면 다음을 실행합니다.

```bash
git merge --abort
```

## 6. 결과 확인 및 공유

```bash
git log --oneline --graph --decorate --all
git push origin main
```

병합 후에는 테스트를 실행하고, 그래프에서 원하는 이력이 만들어졌는지 확인합니다.