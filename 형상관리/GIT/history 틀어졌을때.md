### master와 branch의 history가 틀어터졌을때
```
There isn't anything to compare
```

### 해결방법
- 강제로 pull 해서 덮어버린다
- 그리고 master 기준 branch 만들고 신규 branch를 딴다.
```
git pull origin dev_master --allow-unrelated-histories
```