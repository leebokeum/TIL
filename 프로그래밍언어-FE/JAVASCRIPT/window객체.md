### Window 객체
-  javascript(자바스크립트) window 객체는 모든 객체가 포함된 최상위 객체이며, 전역 객체(Global Object)이다. 전역 객체는 해당 객체의 프로퍼티(property), 메서드를 호출할 때 이름을 명시할 필요가 없다.
![alt text](https://t1.daumcdn.net/cfile/tistory/222EDF435496DA7532)


### window load후 자바스크립트 실행
1.
~~~ javascript
function init(){
    ...
}

window.onload = init;
~~~
2.
~~~ javascript
window.onload = function (){
    ...
}
~~~
위 onload함수는 스크립트 파일이 중첩될때 문제가 발생할 수 있다.
3.
~~~ javascript
window.addEventListener("load", function(){
    ...
});
~~~
위와 같이 쓰면 추가해서 누적해서 쓸 수 있기 때문에 안전하다.