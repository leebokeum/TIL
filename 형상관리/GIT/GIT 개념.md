### 깃 개념 정리
1. Git은 파일을 Commited, Modified, Staged 세가지 상태로 관리한다.
  - commited : 데이터가 로컬 저장소에 안전하게 저장됐다는 것을 의미함
  - modified : 수정한 파일을 아직 로컬 저장소에 commit하지 않은 것을 의미함
  - staged : 현재 수정한 파일을 곧 Commit할 것이라고 표시한 상태를 의미함.

2. Git은 Git Directory, Working Directory, Staging Area 세가지 영역으로 분리된다. 
  - Git Directory : Git이 프로젝트의 메타데이터와 객체 데이터베이스를 저장하는 곳을 말한다.  (.git)
  - Working Directory : 수정할 파일들이 있는 디렉토리
  - Staging Area : Git Directory에 있으며, 단순한 파일이고 곧 commit할 파일에 대한 정보를 저장한다. 
 
3. Working Directory의 모든 파일은 Tracked와 Untracked로 나뉜다.
  - Tracked 파일은 이미 Snapshot에 포함돼 있던 파일이며, Unmodified, Modified, Staged 상태중 하나의 상태를 갖는다. 
  - Tracked 파일이 아닌 모든 파일은 Untracked 파일이다.

4. Git에서 branch는 커밋 사이를 가볍게 이동할 수 있는 어떤 포인터 같은 것이다. git은 기본적으로 master 브랜치를 만든다.  Git은 최초로 커밋하면 master라는 이름의 브랜치를 만들고, 자동으로 master 브랜치가 가장 마지막 커밋을 가리키게 한다.

5. Git은 HEAD라는 특수한 포인터를 갖고 있다. 이 포인터는 지금 작업하고 있는 로컬 브랜치를 가리킨다. "git branch <brnach명>" 명령은 브랜치를 만들기만 하고 브랜치를 옮기지는 않는다. "git checkout <branch명>"명령으로 HEAD가 가리키는 브랜치로 이동할 수 있다

## 출처
출처: https://dimdim.tistory.com/entry/GIT에-대한-내용정리-정리중 [딤딤이의 블로그]