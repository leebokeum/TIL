### trigger
- .trigger( eventType [, extraParameters] )
- 특정 이벤트 유형에 대해 선택된 요소에 연결된 모든 핸들러와 동작(behavior)을 실행
- .trigger() 함수는 이벤트가 발생할 때 실행될 함수나 .bind() 함수로 연결된 어떤 이벤트 핸들러를 강제로 실행시켜 준다.

~~~ js
$('#foo').bind('click', function() {
     alert($(this).text()); 
}); 

$('#foo').trigger('click');
~~~

### 참조
https://api.jquery.com/trigger/