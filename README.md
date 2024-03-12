# Git 백과사전
- 지금까지 배운 모든 git명령어를 정리할 예정
- [옵션인자]: 생략 가능한 표현
- <필수인자>: 꼭 입력해야함
## 환경설정 관련

1. **git config**
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

1. **git add**
   - add는 새로 수정/생성한 파일을 특정 "스테이지"라는 공간에 위치시킨다.
   - 커밋을 통해 특정 버전을 생성하기 이전에, 어떤 파일들이 다른 버전을 구성할지 등록해 주는 것이다.
   - 경로내 모든 파일을 스테이징 하려면, `$ git add .` 과 같이 입력한다.
   ```sh
   $ git add [파일이름] 
   ```
2. **git commit**
   - commit은 스테이징된 파일을 기준으로 나의 로컬 저장소에 특정 "버전"을 생성한다.
   - 이는 즉시 원격저장소와의 동기화를 말하는 것은 아니며, 로컬 저장소에만 적용된다.
   ```sh
   $ git commit -m "커밋 메시지"
   ```
3. **git push**
   - push를 이용해 내가 가진 가장 최근 버전정보(commit)을 기준으로 원격저장소와 히스토리 내역, 파일 상태 등을 동기화한다.
   - 혼자 저장소를 사용한다면, `git push origin main(master)`가 가장 자주 사용하는 명령어가 될 것이다.
   ```sh
   $ git push <원격 저장소 별칭> <브랜치 이름>
   ```
   (번외)
   - 강제 푸시 옵션을 사용해 히스토리 내역이 맞지 않더라도 푸시할 수 있다. 이의 활용에 대해서는 후술한다.
   ```sh
   $ git push --force-with-lease
   ```
## 정보를 조회하는 명령어
1. **git log**
   - 이 명령어를 사용하여 commit 된 내역을 조회할 수 있다.
   - `oneline` 옵션은 로그를 한줄단위로 출력하도록 한다.
   - `graph` 옵션은 브랜치가 뻗어나가는 경로를 트리형태로 시각화해 볼 수 있도록 한다.
   - `nk` (k는 숫자) 최근 k개의 commit 내역을 볼 수 있도록 한다.
   - `decorate` 옵션은 각 브랜치가 어떤 commit을 가리키고 있는지 보여준다.
   ```sh
   $ git log [--oneline] [--graph] [--all] [-nk] [--decorate]
   --- example ---
   $ git log --oneline --graph --all --decorate -n4
   ```
2. **git status**
   - add 명령어를 통해 스테이징된 파일의 상태를 확인 할 수 있다.
   ```sh
   $ git status
   ```
## 브랜치 관련 명령어

1. **git branch**
   - 브랜치를 삭제/생성, 브랜치 정보조회를 할 수 있는 기본 명령어에 해당한다.
   - `-v` 옵션을 사용해 현재 원격 저장소에 어떤 브랜치가 있는지 조회할 수 있다.
   ```sh
   $ git branch -v
   ```
   - 특정 커밋에서 브랜치를 새로 생성하고 변경까지 가능한 명령어이다. `[커밋 체크섬]` 은 git commit을 통해서 최근 commit을 조회했을 때 얻을 수 있는 16진수 표현이 입력된다.
   - 일반적으로 6자를 적어준다.
   ```sh
   $ git branch -c <브랜치이름> [커밋 체크섬]
   ```
2. **git switch**
   - 해당 브랜치 이름에 해당하는 브랜치로 체크아웃 한다.
   ```sh
   $ git switch <브랜치이름>
   ```
3. **git rebase**
   - 대상 브랜치의 가장 최신 커밋을 기준으로 브랜치를 재배치한다.
   ```sh
   $ git rebase <대상 브랜치>
   ```
4. **git merge**
   - 현재 브랜치와 대상 브랜치에 대한 병합 커밋을 생성한다. 
    ```sh
    $ git merge <대상 브랜치>
    ```
  (참고) Fast Forward 병합과 Conflict가 포함된 병합
  - Fast Forward 병합은 두 코드가 충돌하는 부분이 없을 경우 git에서 자동으로 병합해주는 경우에 해당한다.
  - Conflict가 발생하는 경우 충돌이 발생한 커밋에 대해서 `변경사항 모두 수락`, `변경사항 둘 중 하나만 수락`과 같은 옵션이 존재하며, 사용자가 직접 대상 파일들을 수정해야한다. 
## 동기화 관련 명령어
1. **git fetch**
   - git fetch 명령어는 원격 저장소의 브랜치와 커밋들을 로컬 저장소와 동기화 한다.
   - 로컬저장소에 있는 파일과 직접 병합되지는 않는다. 이는 git pull과의 주요한 차이점이다.
    ```sh
    $ git fetch [원격 저장소 별명] [브랜치 이름]
    ```
2. **git pull**
   - 원격저장소의 변경사항을 로컬에 직접 반영한다. git fetch + git merge라고 볼 수 있다.
    ```sh
    $ git pull
    ```
## 커밋 되돌리기와 시간여행
1. **git revert**
    - git revert는 과거의 특정 커밋 체크섬을 이용해서 그 커밋에서 변경된 사항을 되돌린다.
    - amend와의 다른점은 revert는 되돌리고 난후 되돌렸다는 명시적인 커밋 메시지가 남게된다는 점이다.
    ```sh
    $ git revert [커밋 체크섬]
    ```
2. **git commit --amend**
   - 마지막 commit을 정정하는 방법이다.
   - 실수로 덜 수정한 파일이 있거나 할 때 또다른 커밋내역을 생성하지 않고 정정이 가능하다.
    ```sh
    $ git commit --amend 
    ```
    - 히스토리 내역이 조작되기 때문에 강제푸시를 진행해야 한다는 점 또한 명심하자.
    ```sh
    $ git push --force-with-lease
    ```
3. **git reset**
   - 리셋 명령어는 옵션에 따라 주의해서 사용해야 한다. 
   - 특정 커밋만을 되돌리는 revert와는 달리, 그 커밋아래에 딸린 자식 커밋도 모두 되돌린다.
    ```sh
    $ git reset [--mixed] [커밋 체크섬]
    ```
    - 커밋 내역을 삭제하지만, 로컬 변경사항은 유지하는 명령어이다.
    ```sh
    $ git reset [--hard] [커밋 체크섬]
    ```
    - 커밋 내역과 로컬변경사항까지 모두 되돌린다. 작성한 코드까지 모두 날아가게 되니 주의해 사용해야한다.
    - 이전 커밋 내역이 원격저장소에 push된 상태라면 강제푸시를 사용해야 한다.
    ```sh
    $ git push --force-with-lease
    ```

## 문제 상황 해결
- [병합 커밋을 남기지 않고 브랜치를 통합하는 방법](https://github.com/Rucious-Aladdin/hello-git-cli/blob/main/%EC%8B%9C%EB%82%98%EB%A6%AC%EC%98%A4%20%EC%B2%98%EC%B9%98%EC%99%80%20%EA%B3%A0%EA%B8%89%20%EA%B9%83%ED%97%88%EB%B8%8C%20%EA%B8%B0%EC%88%A0/3-way_merge_versus_rebase.md)