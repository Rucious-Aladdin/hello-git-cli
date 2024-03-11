# Git 백과사전
- 지금까지 배운 모든 git명령어를 정리할 예정
- [옵션인자]: 생략 가능한 표현
- <필수인자>: 꼭 입력해야함
## 환경설정 관련

1. **git config 관련 명령어**
- 처음 github에 계정 정보를 등록하거나, 계정정보를 갱신해야할 때 사용한다.
```sh
$ git config --global user.name <username>
$ git config --global user.email <useremail>
```
- 삭제시 `--unset` 옵션을 넣어서 계정정보의 갱신이 가능하다.
```sh
$ git config --global [--unset] user.name <user.name>
$ git config --global [--unset] user.email <user.email>
```
- `--list` 옵션과 `$ grep user` 를 파이프라인으로 이용하여 현재 등록된 계정 정보의 조회가 가능하다.
```sh
$ git config --global --list | grep user
```
- (번외)CLI환경에서 가시성을 개선하는 명령어
```sh
$ git config --global color.ui auto
```

## 저장소를 처음 시작할 때의 명령어
1.  **git init**
- 로컬 저장소의 현재 디렉토리를 git 저장소로 초기화한다. 
- 현재 디렉토리 내에 `.git/` 폴더가 생성되면 성공이다.
```sh
$ git init
$ ls -al
```
2. **git clone**
- 특정 계정에 있는 레포지토리를 복제하는 명령어이다. github에 접속하여 code아래의 url을 복사하여 붙여넣는다.
- `[디렉토리 경로]`내에 "."을 입력하면 하위폴더가 생기는 것 없이 레포지토리의 전체 내용을 깔끔히 복사할 수 있다.
```sh
$ git clone <저장소 URL> [디렉토리 경로]
```
## 로컬 저장소와 원격 저장소 연결하기
1. **git remote**
- 로컬 저장소에 연결할 원격 저장소 주소를 설정해준다. 
- 또한 `[별칭]` 인자에 원격저장소의 이름을 지정할 수 있는데, 관례적으로 origin(또는 master)을 사용한다.
```sh
$ git remote add <별칭> <원격 저장소 URL>
```
2. **git branch**
- 일단 git을 사용하기 위해서는, 브랜치를 설정해주어야 한다.
- `-M` 인자는 `--move --force` 의 줄임말이다. 이름이 똑같은 브랜치가 존재하더라도 덮어씌우고 브랜치를 생성한다.
- `<브랜치 이름>` 처음 만드는 branch면 main을 사용하면 된다.
- 그외 브랜치에 대한 자세한 내용은 후술한다.
```sh
$ git branch [-M] <브랜치 이름>
``` 

## add, commit, push
- add는 새로 수정/생성한 파일을 특정 "스테이지"라는 공간에 위치시킨다.
- 커밋을 통해 특정 버전을 생성하기 이전에, 어떤 파일들이 다른 버전을 구성할지 등록해 주는 것이다.
- 경로내 모든 파일을 스테이징 하려면, `$ git add .` 과 같이 입력한다.
```sh
$ git add [파일이름] 
```
- commit은 스테이징된 파일을 기준으로 나의 로컬 저장소에 특정 "버전"을 생성한다.
- 이는 즉시 원격저장소와의 동기화를 말하는 것은 아니며, 로컬 저장소에만 적용된다.
```sh
$ git commit -m "커밋 메시지"
```
- push를 이용해 내가 가진 가장 최근 버전정보(commit)을 기준으로 원격저장소와 히스토리 내역, 파일 상태 등을 동기화한다.
- 혼자 저장소를 사용한다면, `git push origin main(master)`가 가장 자주 사용하는 명령어가 될 것이다.
```sh
$ git push <원격 저장소 별칭> <브랜치 이름>
```

## 정보를 조회하는 명령어
