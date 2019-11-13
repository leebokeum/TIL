# 오라클 성능을 확인하는 유용한 SQL 모음

## 11 테이블에 LOCK이 걸렸는지를 보기
~~~ sql
SELECT    A.SID
         ,A.SERIAL#
         ,SUBSTRB(A.USERNAME, 1, 16) AS USERNAME
         ,SUBSTRB(A.MACHINE, 1, 30) AS MACHINE
         ,A.TERMINAL
         ,A.OSUSER
         ,A.PROGRAM
         ,SUBSTRB(TO_CHAR(A.LOGON_TIME, 'MM/DD HH24:MI:SS'), 1, 14) AS LOGON_TIME
         ,SUBSTRB(C.OBJECT_NAME, 1, 58) AS OBJECT_NAME
FROM      V$SESSION A
         ,V$LOCK B
         ,DBA_OBJECTS C
WHERE     A.SID = B.SID
AND       B.ID1 = C.OBJECT_ID
AND       B.TYPE = 'TM'
AND       C.OBJECT_NAME LIKE UPPER('&테이블명');
~~~ 

## 12 Lock을 잡고있는 세션과 기다리는 세션 조회

~~~ sql
SELECT    DECODE(B.LOCKWAIT, NULL, ' ', 'w') AS WW
         ,B.SID
         ,B.SERIAL# AS SER#
         ,SUBSTR(B.MACHINE, 1, 10) AS MACHINE
         ,SUBSTR(B.PROGRAM, 1, 15) AS PROGRAM
         ,SUBSTR(A.OBJECT_NAME, 1, 17) AS OBJ_NAME
         ,SUBSTR(B.STATUS, 1, 1) AS S
         ,DECODE(B.COMMAND,  0, NULL,  2, 'INSERT',  6, 'UPDATE',  7, 'DELETE',  B.COMMAND) AS SQLCMD
         ,B.PROCESS AS PGM_PSS
FROM      V$SESSION B
         ,(SELECT    A.SID, DECODE(B.OWNER, NULL, A.TYPE || '..ing', B.OWNER || '.' || B.OBJECT_NAME) AS OBJECT_NAME
           FROM      V$LOCK A
                    ,DBA_OBJECTS B
           WHERE     A.ID1 = B.OBJECT_ID(+)
           GROUP BY  A.SID, DECODE(B.OWNER, NULL, A.TYPE || '..ing', B.OWNER || '.' || B.OBJECT_NAME)) A
WHERE     B.SID = A.SID
AND       B.TADDR IS NOT NULL;
~~~

## 13 테이블에 걸린 비정상적 LOCK 풀기
~~~ sql
ALTER SYSTEM KILL SESSION '&SID,&SERIAL';
~~~ 

## 14 연결되어 있는 OS 사용자 및 프로그램 조회
~~~ sql
SELECT    SID
         ,SERIAL#
         ,OSUSER
         ,SUBSTRB(USERNAME, 1, 10) AS USER_NAME
         ,SUBSTRB(PROGRAM, 1, 30) AS PROGRAM_NAME
         ,STATUS
         ,TO_CHAR(LOGON_TIME, 'YYYY/MM/DD HH:MI') AS LOGON_TIME
FROM      V$SESSION
WHERE     TYPE != ‘BACKGROUND’
AND       STATUS = ‘ACTIVE’;
~~~


## 16 DB Link 보기

~~~ sql
SELECT    SUBSTRB(U.NAME, 1, 10) AS OWNER
         ,SUBSTRB(L.NAME, 1, 20) AS DB_LINK
         ,SUBSTRB(L.HOST, 1, 10) AS HOST
         ,SUBSTRB(L.USERID || '/' || L.PASSWORD, 1, 15) AS USERPASS
FROM      SYS.LINK$ L
         ,SYS.USER$ U
WHERE     L.OWNER# = U.USER#;
~~~
 

## 18 테이블의 크기 및 블록 보기

~~~ sql 
SELECT    SUBSTR(SEGMENT_NAME, 1, 20), BYTES, BLOCKS
FROM      USER_SEGMENTS
WHERE     SEGMENT_NAME = UPPER('&테이블명');
~~~

## 23 동일한 자료 삭제 방법

~~~ sql
DELETE
FROM   EMP E
WHERE  E.ROWID > ( SELECT MIN(X.ROWID)
 FROM   EMP X
WHERE  X.EMPNO = E.EMPNO );
~~~
 

## 24 1시간 이상 유휴 상태인 세션

~~~ sql
SELECT    SID
         ,SERIAL#
         ,USERNAME
         ,TRUNC(LAST_CALL_ET / 3600, 2) || ' HR' LAST_CALL_ET
FROM      V$SESSION
WHERE     LAST_CALL_ET > 3600
AND       USERNAME IS NOT NULL;
~~~
 

## 29 Active Session 중 Idle Time이 긴 작업

~~~ sql
SELECT    VS.SID || ',' || VS.SERIAL# " SID"
         ,VP.SPID
         ,VS.MACHINE
         ,VS.PROGRAM
         ,VS.MODULE
         ,VS.STATUS
         ,TO_CHAR(VS.LOGON_TIME, 'MM/DD HH24:MI') LOGIN_TIME
         ,ROUND(VS.LAST_CALL_ET / 60) "IDLE"
FROM      V$SESSION VS
         ,V$PROCESS VP
WHERE     VS.STATUS = 'ACTIVE'
AND       VS.SID NOT IN (1, 2, 3, 4, 5, 6, 7)
AND       VS.PADDR = VP.ADDR
ORDER BY  8;
~~~


## 36 잠금 발생 유형 조회

~~~ sql
SELECT    A.SID
         ,DECODE(A.TYPE
                ,'MR', 'MEDIA RECOVERY'
                ,'RT', 'REDO THREAD'
                ,'UN', 'USER_NAME'
                ,'TX', 'TRANSACTION'
                ,'TM', 'DML'
                ,'UL', 'PL/SQL USER LOCK'
                ,'DX', 'DISTRIBUTED XACTION'
                ,'CF', 'CONTROL FILE'
                ,'IS', 'INSTANCE STATE'
                ,'FS', 'FILE SET'
                ,'IR', 'INSTANCE RECOVERY'
                ,'FS', 'FILE SET'
                ,'ST', 'DISK SPACE TRANSACTION'
                ,'TS', 'TEMP SEGMENT'
                ,'IV', 'LIBRARY CACHE INVAILDATION'
                ,'LS', 'LOG START OR SWITCH'
                ,'RW', 'ROW WAIT'
                ,'SQ', 'SEQUENCE NUMBER'
                ,'TE', 'EXTEND TABLE'
                ,'TT', 'TEMP TABLE'
                ,A.TYPE
                )
            AS "LOCK_TYPE"
         ,DECODE(A.LMODE
                ,0, 'NONE'
                ,1, 'NULL'
                ,2, 'ROW-S(SS)'
                ,3, 'ROW-X(SX)'
                ,4, 'SHARE'
                ,5, 'S/ROW-X(SSX)'
                ,6, 'EXCLUSIVE'
                ,TO_CHAR(A.LMODE)
                )
            AS "MODE_HELD"
         ,DECODE(A.REQUEST
                ,0, 'NONE'
                ,1, 'NULL'
                ,2, 'ROW-S(SS)'
                ,3, 'ROW-X(SX)'
                ,4, 'SHARE'
                ,5, 'S/ROW-X(SSX)'
                ,6, 'EXCLUSIVE'
                ,TO_CHAR(A.REQUEST)
                )
            AS "MODE_REQUESTED"
         ,TO_CHAR(A.ID1) AS "LOCK_ID1"
         ,TO_CHAR(A.ID2) AS "LOCK_ID2"
         ,DECODE(BLOCK,  0, 'NOT BLOCKING',  1, 'BLOCKING',  2, 'GLOBAL',  TO_CHAR(BLOCK)) AS "BLOCKING_OTHERS"
FROM      V$LOCK A
WHERE     (ID1, ID2) IN (SELECT    B.ID1, ID2
                         FROM      V$LOCK B
                         WHERE     B.ID1 = A.ID1);
~~~


## 39 잠금 상태 오브젝트 조회

~~~ sql
SELECT    A.SESSION_ID
         ,B.SERIAL#
         ,A.OS_USER_NAME
         ,A.ORACLE_USERNAME
         ,C.OBJECT_NAME
         ,A.LOCKED_MODE
         ,A.XIDUSN
FROM      V$LOCKED_OBJECT A
         ,V$SESSION B
         ,DBA_OBJECTS C
WHERE     A.OBJECT_ID = C.OBJECT_ID
AND       A.SESSION_ID = B.SID;
~~~

 
## 40 잠금 SQL 구문 조회

~~~ sql
SELECT    B.USERNAME AS USERNAME
         ,C.SID AS SID
         ,C.OWNER AS OBJECT_OWNER
         ,C.OBJECT AS OBJECT
         ,B.LOCKWAIT
         ,A.PIECE
         ,A.SQL_TEXT AS SQL
FROM      V$SQLTEXT A
         ,V$SESSION B
         ,V$ACCESS C
WHERE     A.ADDRESS = B.SQL_ADDRESS
AND       A.HASH_VALUE = B.SQL_HASH_VALUE
AND       B.SID = C.SID
AND       C.OWNER != 'SYS';
~~~


## 42 CPU를 많이 사용하는 세션의 식별

~~~ sql
SELECT    A.SID
         ,C.SERIAL#
         ,A.VALUE
         ,C.USERNAME
         ,C.STATUS
         ,C.PROGRAM
FROM      V$SESSTAT A
         ,V$STATNAME B
         ,V$SESSION C
WHERE     A.STATISTIC# = B.STATISTIC#
AND       A.SID = C.SID
AND       B.NAME = 'CPU used by this session'
AND       A.VALUE > 0
ORDER BY  A.VALUE DESC;
~~~ 


## 44 Disk Read 가 많은 SQL문 찾기

~~~ sql 
SELECT    DISK_READS, SQL_TEXT
FROM      V$SQLAREA
WHERE     DISK_READS > 100
ORDER BY  DISK_READS DESC;
~~~ 


## 46 Index가 없는 Table 조회

~~~ sql
SELECT    OWNER, TABLE_NAME
FROM      (SELECT    OWNER, TABLE_NAME
           FROM      DBA_TABLES
           MINUS
           SELECT    TABLE_OWNER, TABLE_NAME
           FROM      DBA_INDEXES)
WHERE     OWNER NOT IN ('SYS', 'SYSTEM')
ORDER BY  OWNER, TABLE_NAME;
~~~


## 47 오래도록 수행되는 Full Table Scan를 모니터링

~~~ sql
SELECT    SID
         ,SERIAL#
         ,OPNAME
         ,TO_CHAR(START_TIME, 'HH24:MI:SS') AS "START"
         ,(SOFAR / TOTALWORK) * 100 AS "PERCENT_COMPLETE"
FROM      V$SESSION_LONGOPS;
~~~


## 55 특정 테이블의 스키마 구조 확인

~~~ sql
/*
     보통 토드나 기타 오라클 클라이언트 툴을 이용해서 테이블 구조를 확인 해도 됩니다.
     하지만 수많은 테이블을 전체 보고 싶을 경우 아래 쿼리를 이용하면 한번에 확인이 가능합니다.
*/
 
 
--: 관리자용
SELECT    OWNER
         ,TABLE_NAME
         ,COLUMN_NAME
         ,PK
         ,COLUMN_NAME
         ,DATA_TYPE || '( ' || NVL(DATA_TYPE_2, DATA_LENGTH) || ' )' DATA_TYPE
         ,NULLABLE
         ,COMMENTS
FROM      (SELECT    A.OWNER
                    ,A.TABLE_NAME
                    ,A.COLUMN_ID
                    ,B.POSITION PK
                    ,A.COLUMN_NAME
                    ,A.DATA_TYPE
                    ,A.DATA_PRECISION || DECODE(A.DATA_SCALE, NULL, NULL, ',' || A.DATA_SCALE) DATA_TYPE_2
                    ,A.DATA_LENGTH
                    ,A.DATA_PRECISION
                    ,A.DATA_SCALE
                    ,A.NULLABLE
                    ,A.COMMENTS
                    ,ROW_NUMBER() OVER (PARTITION BY A.OWNER, A.TABLE_NAME, A.COLUMN_ID 
                      ORDER BY A.COLUMN_ID, B.POSITION) RN
           FROM      (SELECT    COL.OWNER
                               ,COL.TABLE_NAME
                               ,COL.COLUMN_ID
                               ,COL.COLUMN_NAME
                               ,COL.DATA_TYPE
                               ,COL.DATA_LENGTH
                               ,COL.DATA_PRECISION
                               ,COL.DATA_SCALE
                               ,COL.NULLABLE
                               ,COM.COMMENTS
                      FROM      DBA_TAB_COLUMNS COL
                               ,DBA_COL_COMMENTS COM
                      WHERE     COL.COLUMN_NAME = COM.COLUMN_NAME
                      AND       COL.OWNER = COM.OWNER
                      AND       COL.TABLE_NAME = COM.TABLE_NAME
                      AND       COM.OWNER = :IN_OWNER
                      AND       COM.TABLE_NAME LIKE :IN_TABLE_NAME || '%') A
                    ,DBA_CONS_COLUMNS B
           WHERE     B.TABLE_NAME(+) = A.TABLE_NAME
           AND       B.COLUMN_NAME(+) = A.COLUMN_NAME) X
WHERE     X.RN = 1
ORDER BY  X.TABLE_NAME, X.COLUMN_ID;
 
 
 
--: 일반 사용자 용
 
SELECT    TABLE_NAME
         ,COLUMN_NAME
         ,PK
         ,COLUMN_NAME
         ,DATA_TYPE || '( ' || NVL(DATA_TYPE_2, DATA_LENGTH) || ' )' DATA_TYPE
         ,NULLABLE
         ,COMMENTS
FROM      (SELECT    A.TABLE_NAME
                    ,A.COLUMN_ID
                    ,B.POSITION PK
                    ,A.COLUMN_NAME
                    ,A.DATA_TYPE
                    ,A.DATA_PRECISION || DECODE(A.DATA_SCALE, NULL, NULL, ',' || A.DATA_SCALE) DATA_TYPE_2
                    ,A.DATA_LENGTH
                    ,A.DATA_PRECISION
                    ,A.DATA_SCALE
                    ,A.NULLABLE
                    ,A.COMMENTS
                    ,ROW_NUMBER() OVER (PARTITION BY A.TABLE_NAME, A.COLUMN_ID 
                    ORDER BY A.COLUMN_ID, B.POSITION) RN
           FROM      (SELECT    COL.TABLE_NAME
                               ,COL.COLUMN_ID
                               ,COL.COLUMN_NAME
                               ,COL.DATA_TYPE
                               ,COL.DATA_LENGTH
                               ,COL.DATA_PRECISION
                               ,COL.DATA_SCALE
                               ,COL.NULLABLE
                               ,COM.COMMENTS
                      FROM      USER_TAB_COLUMNS COL
                               ,USER_COL_COMMENTS COM
                      WHERE     COL.COLUMN_NAME = COM.COLUMN_NAME
                      AND       COL.TABLE_NAME = COM.TABLE_NAME
                      AND       COM.TABLE_NAME LIKE :IN_TABLE_NAME || '%') A
                    ,USER_CONS_COLUMNS B
           WHERE     B.TABLE_NAME(+) = A.TABLE_NAME
           AND       B.COLUMN_NAME(+) = A.COLUMN_NAME) X
WHERE     X.RN = 1
ORDER BY  X.TABLE_NAME, X.COLUMN_ID;
~~~



## 59 해당 테이블의 세션을 제거하는 쿼리

~~~ sql
/*
   특정 테이블이 락을 발생하고 있으면 세션을 찾아서 중단시킨다.
*/
SELECT 'ALTER SYSTEM KILL SESSION ''' || S.SID||','||S.SERIAL# ||''';'
FROM   V$LOCK L, DBA_OBJECTS O, V$SESSION S
WHERE  L.ID1  = O.OBJECT_ID
AND    S.SID = L.SID
AND    O.OWNER = 'ESTDBA'
AND    O.OBJECT_NAME = 'TMP_GSYM2'
~~~


## 60 CPU를 많이 사용하는 세션의 식별(SQL TEXT 조회)

~~~ sql
SELECT    A.*
         ,(SELECT   SS.SQL_TEXT
           FROM     V$SQLAREA SS
           WHERE    SS.ADDRESS = A.SQL_ADDRESS
           AND      ROWNUM <= 1
          ) AS SQL_TEST
FROM      (
          SELECT    A.SID
                   ,C.SERIAL#
                   ,A.VALUE
                   ,C.USERNAME
                   ,C.STATUS
                   ,C.PROGRAM
                   ,C.SQL_ADDRESS
                   ,ROW_NUMBER() OVER (ORDER BY A.VALUE DESC) RN
          FROM      V$SESSTAT A
                   ,V$STATNAME B
                   ,V$SESSION C
          WHERE     A.STATISTIC# = B.STATISTIC#
          AND       A.SID = C.SID
          AND       B.NAME = 'CPU used by this session'
          AND       A.VALUE > 0
          AND       C.STATUS = 'ACTIVE'
          AND       C.USERNAME IS NOT NULL
          ) A
WHERE     A.RN <= 10;
~~~

### 참조
https://epthffh.tistory.com/entry/SQL-Oracle-필수-스크립트-모음딕셔너리-SQL-문법-성능-분석