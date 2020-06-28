### Kerberos란
- kerberos는 네트워크 인증 protocol이다.
- 네트워크 보안에서 Username과 password를 계속해서 보낸다는 것은 매번 password를 가로챌 수 있는 기회를 제공하는 것과 동일하다. 그리하여 Kerberos에서는 이러한 Username과 password의 전송을 최소화로 만들도록 지원한다.
- 신뢰하는 제 3의 컴퓨터가 서비스를 이용하려는 클라이언트의 사용자를 인증함으로써 가능해진다. 인증을 함으로써 서버는 클라이언트의 사용자가 올바른 사용자 인지를 확인하게 되고 서로간에는 비밀통신이 가능해진다. 이것으로 Spoofing이나 Sniffing을 막을수 있다 .

### Kerberos 구성요소 
3가지 Components로 구성되어 있다.
 - Client
 - Authentication Server or Key Distribution Server (KDC)
 - Server

3가지 주요 활동이 있다.
 - Authentication Service (AS) Exchange
 - Ticket Grating Service (TGS) Exchange
 - Client Server (CS) Exchange