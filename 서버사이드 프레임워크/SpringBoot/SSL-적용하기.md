### 스프링 부트에 local ssl 적용
- 참조
  - https://jojoldu.tistory.com/350

~~~ sh
keytool -genkey -alias bns-ssl -storetype PKCS12 -keyalg RSA -keysize 2048 -keystore keystore.p12 -validity 3650
~~~
- alias bns-ssl
    key alias를 bns-ssl로 지정합니다.
- keystore keystore.p12
    key store 이름을 keystore.p12로 지정합니다.

~~~ yml
spring:
  profiles: local # 로컬환경에서만 사용하기

server:
  ssl:
    enabled: true
    key-store: keystore.p12
    key-store-password: 123456
    key-store-type: PKCS12
    key-alias: bns-ssl
  port: 8443
~~~