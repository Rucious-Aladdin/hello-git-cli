# 3-way merge와 rebase를 이용한 브랜치 병합

## 3-way merge 병합
- 특정 commit을 기준으로 2개의 서로 다른 브랜치가 생겼을 때, 병합 명령어를 이용하여 병합 커밋을 생성하여 브랜치를 하나로 통일한다.
```sh
$ git merge [브랜치 이름]
```
- 예를 들어, 현재 main 브랜치에 있고 feature 브랜치와 병합하고자 한다면, 
```sh
$ git merge feature
```
와 같은 형식으로 기술한다. 병합 충돌 현상이 발생할 시에는 vscode/vim editor를 이용해 충돌현상을 해결하고, 
```sh
$ git add .
$ git commit
```
을 순차적으로 실행해 병합을 마칠 수 있다.
## rebase 기반 병합
- 하나의 브랜치로 통합된다는 점은 3-way merge와 공통적인 특징이지만, 커밋을 떼와서 연결하기 때문에 잔 가지가 생기지 않고 히스토리 내역이 깔끔하게 병합된다는 점이 장점이다.
- 워크플로우는 다음과 같다.
1. 병합할 브랜치로 이동
   ```sh
   $ git switch <병합할 브랜치>
   ```
2. 리베이스 명령어 실행
    ```sh
    $ git rebase <기준 브랜치>
    ```
3. 충돌 발생시 해결
   - 텍스트 에디터 툴을 이용해 충돌이 있다면 해결해준다.
4. 리베이스 이어서 진행
    ```sh
    $ git rebase --continue
    ```
5. 기준 브랜치로 이동
   ```sh
   $ git switch <기준 브랜치>
   ```
6. 브랜치 병합 수행
   ```sh
   $ git merge <병합할 브랜치>
    ```
- 복잡하니 예를들어서 생각해보자. 마지막 기준이 될 브랜치가 main이고, 병합할 브랜치의 이름이 feature 라고 가정한다면, 다음과 같은 순서로 명령어를 입력한다.
    ```sh
    $ git switch feature
    $ git rebase main
    ## 충돌 해결후에,
    $ git rebase --continue
    $ git switch main
    $ git merge feature
    ```
- 이과정을 마치고 나면, main 브랜치로 병합된 것을 확인할 수 있다.
- 당연하게도 히스토리 내역이 조작되므로 커밋 내역이 원격저장소에 push된 상태라면 강제푸시를 사용해야 한다.
    ```sh
    $ git push --force-with-lease
    ```