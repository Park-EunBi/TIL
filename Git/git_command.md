# git_command

자주 사용하는 git command 

1. `git fectch`

리모트에 있는 거 모두 다운 받기

2. `git rebase`

최신 브랜치로 업데이트

3. `git log`

깃 로그들 확인 가능

4. `git commit  -> git push origin HEAD:refs/for/…`

변경하고 gs (git status의 alias, 등록 되어있어야 작동. 업다면 git status 치기)

변경된 거 확인

git add 파일 -> stage 로  올라감 -> commit 될 준비가 됨

커밋 에 추가 하고싶으면 (커밋 변경)

5. `git commit --amend`

fetch set이 만들어지게 된다

새로운거 ammend하고 fetch 하면 게리에 올라가게 된다

(게리에서) patch set (우측 상단) 누르면 패치 셋에 관한 내용들을 볼 수 있다

commit 할 때 parent가 중요하다

커밋 할 때 바로 위에 물려있는 커밋

체리픽을 해서 따라오기 

6. `git checkout master`

(마스터로 이동)

7. `git rebase`

(게리에서)

로컬에 받고 싶으면 우측에 다운로드 하고

체크아웃 하고 싶으면

복사 해서 붙여넣기 하면 된다

체크아웃하면 브랜치 이름도 바뀌게 된다

8. `git commit --ammend`

9. 체리픽
- 체크아웃과 유사한데
- 다운로드 해서 가져오는 것이아니라
- 수정한 내용만 따오는 것
- 체리픽 복붙하고 -n 옵션 넣으면 커밋 그대로 생성됨

이후에 git status 봐야 한다 

10. `git reset HEAD^`

커밋 사라지고 modify가 변경된다 

11. `git reset --head`

head 로 reset

다른 사람 커밋에 내 것이 들어가지 않으려면 change id를 지우면된다

체리픽 할 때 는 반드시 다른 사람의 change id를 지우면 된다

12. `git push`

(브랜치 명명 규칙 - task/<signum>/<알맞은 이름>)

git checkout -b 브랜치이름

브랜치로 체크아웃 됨 (생성)

13. `git branch -D 브랜치 이름`

체크아웃 할 땐 parent가 중요함

브랜치를 하는 이유 중에 하나가 parent 따오는 것

14. `git chechkout -b 브래치_이름 커밋_아이디`

다운로드 -> 체리픽

15. `git mergetool (충돌 해결 툴)`

로컬에서 수정된 거, 베이스 - 원래 버전, 리모트에서 수정한 거

저장하고 나가고

gs (git status)

git cherry-pick --continue 

git log

- n 옵션안하면 커밋 해야 한다.  안하면 바로 창이 뜸

16. 최신으로 만들고 싶으면 체크아웃 -> 리베이스 (마스터 - 최신이 마스터이면)

머지를 할 땐 무조건 최신으로 바꿔야 한다

머지 컴플릭트 나온건 최신이 아니기 때문

리베이스 반드시 하기
