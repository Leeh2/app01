# Git 병합을 이해하는 짧은 이야기

지수는 `main` 브랜치에서 서비스 코드를 안정적으로 운영하고 있습니다. 로그인 기능을 추가하기 위해 작업 공간을 따로 만들었습니다.

```bash
git switch main
git switch -c feature/login
```

## 두 갈래의 작업

`feature/login`에서 로그인 화면을 완성하고 커밋합니다.

```bash
git add .
git commit -m "Add login feature"
```

이 순간 Git에는 두 흐름이 생깁니다. `main`은 운영 코드에 머물고, `feature/login`은 새로운 기능을 앞서 진행합니다. 브랜치는 파일을 복사한 공간이라기보다 커밋을 가리키는 이름에 가깝습니다.

## 다시 한 줄로 합치기

기능을 검토한 뒤 지수는 결과를 `main`에 합칩니다.

```bash
git switch main
git merge feature/login
```

변경 내용이 겹치지 않으면 Git이 자동으로 병합합니다. 두 브랜치가 갈라진 뒤 `main`에 별도 커밋이 없었다면 `main` 포인터만 기능 커밋까지 이동하는 fast-forward가 일어날 수 있습니다. 양쪽 모두 새 커밋을 만들었다면 Git은 두 흐름을 연결하는 병합 커밋을 만들 수 있습니다.

## 같은 장소를 고쳤다면

지수와 동료가 같은 줄을 서로 다르게 수정했다면 Git은 어느 변경을 선택할지 결정하지 못합니다. 이 상태를 충돌이라고 합니다. 충돌 표시가 있는 파일에서 최종 내용을 직접 선택하고 다음처럼 마무리합니다.

```bash
git add <수정한-파일>
git commit -m "Resolve merge conflict"
```

아직 결정할 수 없다면 병합을 취소하고 원래 상태로 돌아갈 수 있습니다.

```bash
git merge --abort
```

## 이야기의 결말

병합은 파일을 무작정 합치는 명령이 아니라, 서로 다른 커밋 흐름을 현재 브랜치의 역사로 연결하는 작업입니다. 병합 뒤에는 테스트와 로그를 확인합니다.

```bash
git log --oneline --graph --decorate --all
```