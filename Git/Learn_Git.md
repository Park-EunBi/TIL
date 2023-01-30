# Learn_Git

## HEAD

현재 체크아웃된 커밋 (현재 작업 중인 커밋)

항상 작업트리의 가장 최근 커밋을 가리킨다

- HEAD를 분리한다

HEAD를 브랜치 대신 커밋에 붙인다

`git checkout 해당커밋`

## relative ref

### `^` (캐럿 연산자)

: 한번에 한 커밋 위로 이동

참조할 곳에 하나씩 추가할 때마다 명시한 커밋의 부모를 찾음

예) `main^`: main의 부모, main^^: main의 조부모

main 위에 있는 부모를 체크아웃 한다면?

-> `git checkout main^`

=> HEAD를 이동시키는 것

### ~< num >

: 한번에 여러 커밋 위로 이동

`git checkout HEAD~4`

브랜치를 특정 커밋에 직접적으로 재지정 하는 방법

`git branch -f main HEAD~3`

강제로 main 브랜치를 HEAD에서 3번 뒤로 옮김

## 작업 되돌리기 (실제 변경이 복구되는 방법)

### `git reset`

예전의 커밋을 가리키도록 이동시키는 방법

"히스토리를 고쳐쓴다" 라고 할 수 있다

애초에 커밋하지 않은 것 처럼 예전 커밋으로 브랜치를 옮기는 것

로컬 브랜치에서는 괜찮지만 다른 사람과 작업하는 리모트 브랜치에서는 사용할 수 없다

### `git revert`

변경된 내용을 되돌리고 다른 사람과 공유할 때 사용

| git reset | git revert |
| --- | --- |
| commit tree에서 앞으로 이동하는 거 | 변경된 커밋을 만드는 거
(변경 내용이 새로운 커밋으로 만들어짐) |
| 원격 브랜치에는 적합하지 않음 | 원격 브랜치에서도 사용 가능 |
|  | 변경내용 push 가능 |

============= 여기까지가 기초 ============

## cherry-pick

`git cherry-pick <Commit1> <Commit2> <...>`

현재 위치 (HEAD) 아래에 있는 커밋들에 대한 복사본을 만든다는 이야기

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18089947-cba7-4c85-ba40-fe8fccdd4b9d/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/75aa4451-a298-4598-a4ca-81df34561776/Untitled.png)

원하는 부분만 복사본을 만듦

## git interactive rebase

체리픽은 원하는 커밋 (해시값)을 알 때 유용

원하는 커밋을 모를 땐 interactive rebase를 사용

rebase 할 일련의 커밋들을 검토할 수 있는 방법

`git rebase -i`

rebase에 i 옵션을 주면 rebase의 목적지가 되는 곳 아래에 복사될 커밋을 보여주는 ui (사실은 vi 창) 띄움 (해시, 메시지 들도 보여줌)

interactive rebase 창에서 할 수 있는 것들

1. 적용할 커밋들의 순서를 변경 가능
2. 원하지 않는 커밋 빼기 가능 (pick으로 지정)
3. 커밋을 squash 할 수 있음 (커밋 합치기)

### 참고자료

[Learn Git Branching](https://learngitbranching.js.org/?locale=ko)
