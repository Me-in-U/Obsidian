---
tags:
  - git
---
```git
git remote add origin https://lab.ssafy.com/me_in_u/git_train.git
```

| 단계                | 명령어                           | 설명                                                |
| ----------------- | ----------------------------- | ------------------------------------------------- |
| **1. 초기화**        | `git init`                    | 현재 디렉토리를 Git 로컬 저장소로 초기화. `.git` 폴더 생성.           |
| **2. 원격 연결**      | `git remote add origin <url>` | 원격 저장소(URL)를 로컬 저장소에 연결. `origin`은 기본 원격 이름.      |
| **3. 상태 확인**      | `git status`                  | 현재 디렉토리의 변경 사항 및 Staging Area 상태 확인.              |
| **4. 파일 추가**      | `git add <파일명>`               | 특정 파일을 Staging Area에 추가.                          |
|                   | `git add .`                   | 현재 디렉토리의 모든 파일을 Staging Area에 추가.                 |
| **5. 커밋**         | `git commit -m "메시지"`         | Staging Area의 파일을 로컬 저장소에 커밋하며, 메시지와 함께 저장.       |
| **6. 브랜치 설정**     | `git branch -M main`          | 현재 브랜치 이름을 `main`으로 변경 (Git 기본 브랜치).              |
| **7. 원격 브랜치 동기화** | `git push -u origin main`     | 로컬 `main` 브랜치를 원격 저장소 `origin/main`에 업로드 및 추적 설정. |


| 명령어                              | 설명                                  |
| -------------------------------- | ----------------------------------- |
| `git diff`                       | Working Directory와 Staging Area 비교. |
| `git diff --cached` , `--staged` | Staging Area와 마지막 커밋 비교.            |
| `git diff HEAD`                  | Working Directory 전체와 마지막 커밋 비교.    |
| `git diff file.txt`              | 특정 파일의 변경 사항 확인.                    |
| `git diff <commit1> <commit2>`   | 두 커밋 간의 변경 사항 비교.                   |
| `git diff main feature`          | 두 브랜치 간 변경 사항 비교.                   |
| `git diff --stat`                | 변경된 파일과 줄 수를 요약.                    |
| `git difftool`                   | GUI 도구로 변경 내용 확인.                   |
| `--stat` 옵션                      | 간략하게 표현                             |
git push origin master