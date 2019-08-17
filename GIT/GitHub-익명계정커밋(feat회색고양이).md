#### 1. GitHub 모내기 사건의 발단
1. 내 GitHub 계정의 황무한 농경지를 보고 개발자로서 자괴감 느낌.
2. 이제부터라도 열심히 농사지어보기로 결심 후 모내기 시작.
3. GitHub에 TIL Repository를 생성 후 회사와 집 컴퓨터에 클론. 틈틈히 모내기 시작.
4. 주중에는 **`회사`** 에서 업무중 학습한 것을 토대로 TIL에 commit.
5. GitHub의 모판이 하루하루 채워져가는 모습에 뿌듯함을 느낌.
<br>

#### 2. GitHub 모내기 사건의 발생
2019년 08월 15일 휴무일에 **`집`** 에서 작성한 TIL이 commit은 되었지만 모가 심겨지지 않았음을 발견함.
![alt text](/image/GIT/깃허브-모내기실패_LI.jpg )
<br>

#### 3. GitHub 모내기 사건의 분석
1. GitHub의 commit history를 통해 **`회사`** 와 **`집`** 의 history를 비교.
2. 계정명은 **`leebokeum`** 으로 동일함.
3. history의 commit 계정 사진이 상이하다는 것을 발견. 집에서 commit한 것은 계정사진이 **`회색고양이`** 사진으로 되어 있음.<br>
    `회사에서 commit한 것의 계정 사진`
    ![alt text](/image/GIT/회사사진.png) 
    `집에서 commit한 것의 계정 사진`
    ![alt text](/image/GIT/집-commit.png) 
<br>

#### 4. 원인 파악
1. 회사와 집 컴퓨터의 git user name 확인
    ~~~ shell 
    $ git config user.name
    ~~~
- leebokeum으로 회사와 집 동일함.
2. 회사와 집 컴퓨터의 git user email 확인
    ~~~ shell
    $ git config user.email
    ~~~
- 회사는 **`leebokeum87@gmail.com`** 이고 집은 **`leebokeu87@gmail.com`**
    - 차이가 보이는가? 집에서 쓰는 git email에 m이 하나 빠져 있었음. 
- 결론적으로 계정명은 같지만 email이 서로 다른 두 계정이 각각 commit을 하고 있었던 것임.

###### 그렇다면 GitHub에 허락되지 않은 다른계정이 내 repository에 commit이 가능하다는 이야기?(이것은 나중에 따로 포스팅 하도록 하겠음)
<br>

#### 5. 근본적 문제 해결
1. 우선 집에 있는 git config의 이메일을 정상으로 돌려 놓으면 아주 간단하게 해결완료
    ~~~ shell
    $ git config --global user.email leebokeum87@gmail.com
    ~~~
2. 이메일을 변경 후 집에서 commit을 해보니 비로서 정상적인 계정으로 commit이 되고 모도 심겨지는것을 확인
<br>

#### 6. 사라진 모는 어떻게 복구할 것인가?
- 검색결과 git rebase를 통해 해결 가능(rebase에 대해서는 나중에 따로 포스팅 하도록 하겠음)
    - 뜻을 있는그대로 해석해보면 base(기초)를 다시 한다는 의미니까 납득은 간다.
<br>

#### 7. git rebase 과정
1. 우선 git history를 통해 어디서부터 잘못된 계정으로 commit이 되었는지 확인한다.
2. 히스토리를 보면 `마지막 회사커밋` > **`집 커밋1(회색고양이)`** > **`집 커밋2(회색고양이)`** > **`집 커밋3(회색고양이)`** > `집 커밋4(메일변경 후 정상)` 순서로 되어 있다.
    - rebase해야 할 것이 눈에 보인다.
3. rebase를 하기위해서는 rebase할 대상 바로 직전에 commit한 `해시값` 을 알아야한다. 그렇다면 회사에서 마지막 커밋한 history의 해시값을 찾아서 복사한다.(GitHub 히스토리에서 확인 후 복사할 수 있다.)
    ~~~ shell
    마지막 회사 commit의 해시값 : b50da1ffc0f223854b9c56dbdfcbe6e2cc52cf68
    ~~~
4. 위 해시값을 기준으로 rebase를 시작한다.
    ~~~ shell
    $ git rebase -i b50da1ffc0f223854b9c56dbdfcbe6e2cc52cf68
    ~~~
5. 위 명령어를 치면 터미널에 vim환경으로 수정 가능한 editor환경이 나온다.(아래사진 참고)
![alt text](/image/GIT/rebase-1.PNG)
6. rebase할 커밋내용을 확인후 노란색 pick을 edit로 변경하고 wq로 저장한다.(아래사진 참고)
![alt text](/image/GIT/rebase-2.PNG)
7. 아래 명령어를 3번 반복한다.
    ~~~ shell
    $ git commit --amend --author="leebokeum <leebokeum87@gmail.com>"
    $ git rebase continue
    ~~~
    - git의 계정명과 이메일을 변경후 commit하고 rebase를 계속하겠다는 의미
    - 변경할 commit 히스토리가 3개니까 3번 반복한다.
8. 3번이 끝나면 successfull이라는 메시지가 나오면서 rebase가 정상적으로 되었다는 메시지가 나온다.
9. 마지막으로 GitHub 마스터에 강제 push를 해준다.
    ~~~ shell
    $ git push -f
    ~~~
10. GitHub에 들어가 확인해보면 회색고양이가 없어지고 정상적인 계정으로 커밋된 히스토리를 볼 수 있다. 그리고 사라졌던 모가 복구된것을 확인할 수 있다!!
![alt text](/image/GIT/모내기복구.PNG)
<br>

#### 8. 마무리
깃을 쓰면서 아직도 깃에 대해 많이 모르고 있다는것을 깨달았다. 깃을 알면 알수록 학습곡선이 매우 높다. 이번 사건을 통해 rebase라는 것에 대해서 깊이 생각해볼 수 있었다. 그리고 GitHub 권한 정책에 대해 더 자세히 알아봐야 될거 같다. 다음 포스팅에서..comming soon
<br>

#### 참조
https://hyesun03.github.io/2017/07/13/github-unknown-user/  

https://eminentstar.github.io/2017/03/01/example-content.html