## http파일을 이용한 restApi 테스트
- .http파일을 이용하여 restApi를 테스트 할수 있다.
- 물론 인텔리제이라는 우수한 IDE에서만 지원하는 것이다.
- 사용방법 ### ~ ###
~~~ javascript
### 직접 JSON 사용
GET http://localhost:8080/custList
Content-Type: application/json

{
  "trxDate": "20190814"
}

###
~~~

## 참조
https://jojoldu.tistory.com/266