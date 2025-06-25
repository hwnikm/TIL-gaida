# Git 정리

## 로컬저장소 세팅
`git init` => Git 저장소 초기화<br>
프로젝트용 디렉토리 안에서 실행하는 것을 권고
복구 원할시 `rm -r .git` => 해당 디렉토리를 git repository가 아닌 일반 폴더로 되돌리는 역할
모든 git 기록(commit history, branch 사라짐)

`git add <filename>` => 수정한 파일 커밋할 준비(스테이징)

`git commit -m` => 변경 사항 Git에 저장

`git status` => 현재 Git 상태 확인

`git log` => Git 기록 확인 (커밋내용)

## 로컬저장소와 원격저장소 연결
git remote add origin <URL>

# 로컬저장소 파일 push
git push origin main


## local => remote :: `push`
1. 작업 디렉토리 만들기 `mkdir`
2. Git 초기화 `git init` <br>
`.git` 폴더 생성 -> Git 리포지토리 
3. 파일 추가 및 수정
4. `git status` 확인
5. 스테이징(Staging) <br>
**untracked** 상태의 파일을 `git add <filename>`로 스테이징 => 스테이징 영역에 해당 파일이 올라감
6. 커밋(Commit) <br>
```git commit -m "blahblah"```
