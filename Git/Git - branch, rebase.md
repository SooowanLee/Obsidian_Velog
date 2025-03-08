### 브랜치 생성 git branch 브랜치명
### 브랜치 이동 git switch 브랜치명
### 브랜치 합치기는 기준 브랜치 이동 후 git merge 브랜치명
### 충돌 해결은 코드고치고 git add & git commit

### git merge를 하고 나면 사용한 branch는 삭제한다.
git branch -d 브랜치명

**보통 merge**는 **3-way-merge**가 된다. 

**rebase**는 **브랜치 이동이 가능**하다. **A라는 브랜치**를  **main 브랜치**의 **제일 최근 commit에 이동** 시키고 **merge를 하면 fase-forward merge**를 할 수 있다.

### rebase를 사용하는 이유
