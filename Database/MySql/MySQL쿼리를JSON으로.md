### mysql 쿼리를 Json으로 출력하기
~~~ sql
SELECT JSON_OBJECT('key1',col1 , 'key2',col2 , 'key3','col3') as myobj;
SELECT JSON_ARRAY(col1,col2,'col3') as myarray;
~~~