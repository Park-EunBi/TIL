# cherry-pick.md

cherry-pick: 다른 브랜치의 커밋 하나만 내 브랜치에 반영하기 

## parent 지정해서 cherry-pick 하는 방법
체크아웃 원하는 커밋의 parent와 동일한 parent로 cherry-pick 하는 방법 

1. master(main)으로 `checkout`
2. `git branch -b (branch_name) (parent_commit_hash)`
3. 체크아웃 진행 
  게릿 사용하면 체크아웃 코드 다운 받아서 복붙 + `-n` 옵션 
  새로 커밋을 만든다는 옵션
4. `git commit`
    커밋할 때 커밋 아이디를 삭제하지 않으면 기존 작업자가 커밋을 올린 것이 된다 
    커밋 아이디 반드시 삭제하기 
5. `git log` 
    커밋 아이디가 변경 되었는지 확인하기 
6. `git push origin HEAD:refs/for/master`
7. `git push (저장소명) (브랜치명)`
    브랜치의 변경 사항을 저장소에 push
8. (게릿 사용시) 게릿 메일 확인 
