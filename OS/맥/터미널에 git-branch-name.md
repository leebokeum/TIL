### MAC의 터미널 프롬프트에 Git의 Branch 이름 추가
~~~ bash
# Git branch in prompt.
vi ~/.bash_profile

## 아래내용 추가
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \W\[\033[32m\]\$(parse_git_branch)\[\033[00m\] $ "

### 적용
source ~/.bash_profile
~~~

＊ \[\033[32m\] 부분은 branch 텍스트 부분의 색깔을 설정하는 부분. 다른 색깔을 원하시면 선호하는 색상의 값을 검색하여 입력한다.
＊ \$(parse_git_branch)에서 \은 프롬프트가 보여질때마다 호출되는것을 보장해준다. 이부분이 없다면 branch의 이름이 지속적으로 업데이트 되지 않을것.