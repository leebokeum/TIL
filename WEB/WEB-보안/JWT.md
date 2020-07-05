### jwt(JSON Web Token)토큰이란?


#### Claim 기반 토큰의 개념
- OAuth에 의해서 발급되는 access_token은 random string으로 토큰 자체에는 특별한 정보를 가지고 있지 않는 일반적인 스트링 형태이다.

- JWT는 Claim 기반이라는 방식을 사용하는데, Claim이라는 사용자에 대한 프로퍼티나 속성을 이야기 한다. 토큰 자체가 정보를 가지고 있는 방식인데, JWT는 이 Claim을 JSON을 이용해서 정의 한다.

ex)
~~~ json
{    
    "id":"terry",
    "role":["admin","user"],
    "company":"pepsi" 
}
~~~

- 토큰을 이용해서 요청을 받는 서버나 서비스 입장에서는 이 서비스를 호출한 사용자에 대한 추가 정보는 이미 토큰 안에 다 들어가 있기 때문에 다른 곳에서 가져올 필요가 없다.
 

#### jwt
~~~ json
{    
    "id":"terry",
    "role":["admin","user"],
    "company":"pepsi" 
}

문자열을 BASE64 인코딩 한 결과는 다음과 같다.
ew0KICAiaWQiOiJ0ZXJyeSINCiAgLCJyb2xlIjpbImFkbWluIiwidXNlciJdDQogICwiY29tcGFueSI6InBlcHNpIg0KfQ0K
~~~
JWT는 Claim를 JSON형태로 표현하는 것인데, JSON은 "\n"등 개행문자가 있기 때문에, REST API 호출시 HTTP Header등에 넣기가 매우 불편합니다. 그래서, JWT에서는 이 Claim JSON 문자열을 BASE64 인코딩을 통해서 하나의 문자열로 변환한다.

- 변조 방지

위의 Claim 기반의 토큰을 봤으면, 첫번째 들 수 있는 의문이 토큰을 받은 다음에 누군가 토큰을 변조해서 사용한다면 어떻게 맞느냐? 이다. 이렇게 메세지가 변조되지 않았음을 증명하는 것을 무결성(Integrity)라고 하는데, 무결성을 보장하는 방법 중 많이 사용되는 방법이 서명(Signature)이나 HMAC을 사용하는 방식이다. 즉 원본 메시지에서 해쉬값을 추출한 후, 이를 비밀 키를 이용해서 복호화 시켜서 토큰의 뒤에 붙인다. 이게 HMAC방식인데, 누군가 이 메시지를 변조를 했다면, 변조된 메시지에서 생성한 해쉬값과 토큰 뒤에 붙어있는 HMAC 값이 다르기 때문에 메시지가 변조되었음을 알 수 있다. 다른 누군가가 메시지를 변조한 후에, 새롭게 HMAC 값을 만들어내려고 하더라도, HMAC은 앞의 비밀키를 이용해서 복호화 되었기 때문에, 이 비밀키를 알 수 없는 이상 HMAC을 만들어 낼 수 없다.

- 서명 생성 방식
그러면 무결성 보장을 위해서 사용할 수 있는 알고리즘이 SHA1-256 HMAC 뿐일까? 보안요건에 따라서 SHA1-256,384,512. 그리고 공인 인증서(Certification)을 이요한 RS256 등등 다양한 서명 방식을 지원한다. 그렇다면 JWT 토큰이 어떤 방식으로 서명되어있는지 어떻게 알 수 있을까? 그래서 JWT 토큰의 맨 앞부분에는 서명에 어떤 알고리즘을 사용했는지를 JSON형태로 정의한 후, 이 JSON을 다시 BASE64 방식으로 인코딩한 문자열을 붙인다.

- 전체 메시지 포맷
[![alt text](https://t1.daumcdn.net/cfile/tistory/214BE54B5927D69D3C)]


### 출처
https://12bme.tistory.com/130