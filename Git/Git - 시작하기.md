### Git이 왜 필요한가? 
- 내 소스 코드를 저장(버전 관리)
- 소스코드 공유
- 협업하는 공간

### Git 사용법
git 명령어 -option 으로 이루어졌다.
ex) git add, git commit, git push 등

**git init**을 하면 **.git**이라는 폴더와 함께 깃이 관리하는 폴더가 되는것을 알 수 있다.
여기서 **.** 은 숨겨진 폴더라는 의미이다. 생성된 **.git** 폴더를 삭제하고 싶다면 **rm -rf .git** 명령어를 사용하면 된다.

### Git Workflow
총 세가지의 작업 환경으로 나누어져 있다.
- **working directory**: 프로젝트의 파일들을 수정하는 곳
- **staging area**: 버전 히스토리에 저장할 준비된 파일들이 있는 곳
- **.git directory**: 버전의 히스토리를 가지고 있는 git repository나 git directory가 있다.

#### working directory
**working directory**에는 **untracked** | **tracked** 이 있다. 그 중에 **tracked**안에는 **unmodified** | **modified** 이 있다.


### History(.git directory)에 어느정도 주기로 Commit 하는 것이 좋을까?
1. 프로젝트를 초기화 하는 커밋
2. 