### SSL인증서 발행과 설정의 흐름
1. 적용할 (웹)서버에서 CSR과 KEY를 작성
2. CSR을 CA에 송신해서 인증서의 발행을 신청
3. CA로부터 전자서명된 CRT와 중간CA인증서를 수령
4. 수령한 인증서류를 웹서버에 설치

### certbot
- Certbot이라는 툴을 사용하여 Let’s Encrypt의 SSL인증서를 발행하고, HTTP통신을 HTTPS로 암호화한다.
- 간단하게 정리하면 환경에 맞춰 Let’s Encrypt 인증서를 자동으로 발급/갱신해주는 봇이다. Let’s Encrypt의 인증서 발급 방식을 간단하게 이야기하자면, 인증서 요청 -> 도메인에 대한 소유권 확인 챌린지 -> 발급과 같은 절차를 밟는다. certbot은 이러한 부분의 처리를 자동으로 수행해준다.


### Let’s Encrypt
미국의 ISRG(Internet Security Research Group)가 운영하는 무료 SSL인증 서명 및 발행하는 기관이며,
Cisco, OVH, Mozilla, Google Chrome, Electronic Frontier Foundation, Internet Society, facebook 등 유명기업이 지원하는 비영리단체
Let’s Encrypt 인증서의 유효기간이 90일인데, 스크립트설정을 통해서 자동으로 갱신 가능하므로 반영구적으로 유지가능한 인증서라고 할 수 있다.

### 설치 참고
https://puzji.tistory.com/entry/Certbot-SSL%EC%9D%B8%EC%A6%9D%EC%84%9C-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0

### certbot 설치
~~~ sh
wget https://dl.eff.org/certbot-auto
chmod a+x certbot-auto 
./certbot-auto
~~~

만약 안되면 아래참고
- https://github.com/certbot/certbot/issues/1680#issuecomment-358728515

### 갱신
~~~ sh
./certbot-auto --debug
./certbot-auto renew --quiet --no-self-upgrade
~~~

~~~
Which names would you like to activate HTTPS for?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: leebokeum.com
2: www.leebokeum.com
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate numbers separated by commas and/or spaces, or leave input
blank to select all options shown (Enter 'c' to cancel):
Cert is due for renewal, auto-renewing...
Renewing an existing certificate
Performing the following challenges:
http-01 challenge for leebokeum.com
http-01 challenge for www.leebokeum.com
Waiting for verification...
Cleaning up challenges
Deploying Certificate to VirtualHost /etc/nginx/nginx.conf
Deploying Certificate to VirtualHost /etc/nginx/nginx.conf
Redirecting all traffic on port 80 to ssl in /etc/nginx/nginx.conf
Redirecting all traffic on port 80 to ssl in /etc/nginx/nginx.conf

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Your existing certificate has been successfully renewed, and the new certificate
has been installed.

The new certificate covers the following domains: https://leebokeum.com and
https://www.leebokeum.com

You should test your configuration at:
https://www.ssllabs.com/ssltest/analyze.html?d=leebokeum.com
https://www.ssllabs.com/ssltest/analyze.html?d=www.leebokeum.com
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/leebokeum.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/leebokeum.com/privkey.pem
   Your cert will expire on 2020-09-25. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot-auto
   again with the "certonly" option. To non-interactively renew *all*
   of your certificates, run "certbot-auto renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le

~~~

### 인증서 유효기간 확인
~~~ sh
echo | openssl s_client -servername leebokeum.com -connect leebokeum.com:443 2>/dev/null | openssl x509 -noout -dates
~~~