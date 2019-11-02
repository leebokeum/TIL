### Oracle Instant client
- Toad나 오렌지, PLSQL DEVELOPER 등으로 접속하고자 하나 오라클이 설치되어 있지 않을 때


### 설치방법
1. 먼저 오라클에 접속하여 해당 클라이언트 다운 받기
2. 한글이 없는 경로에 클라이언트 압축해제
3. 환경설정 추가하기
4. Tnsnames.ora 파일 설정하기

### 환경설정(경로는 상황에 맞추어)
PATH = C:\oracle\instantclient-basic-nt-11.2.0.4.0\instantclient_11_2;
ORACLE_HOME = C:\oracle\instantclient-basic-nt-11.2.0.4.0\instantclient_11_2
TNS_ADMIN = C:\oracle\instantclient-basic-nt-11.2.0.4.0\instantclient_11_2\network
NLS_LANG = KOREAN_KOREA.KO16MSWIN949