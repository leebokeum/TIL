### eval() 함수
- eval 함수를 사용하면 String 형태의 JavaScript 소스 코드를 동적으로 실행할 수 있다.
- 하지만 대부분의 경우 eval 함수를 사용하지 않고서도 충분히 동일한 동작을 구현할 수 있는 경우가 많고 또 보안상 위험한JavaScript 코드를 바로 실행할 수 있다는 위험때문에 eval 함수 사용은 권장되지 않는 분위기다. 
- JSON 데이터의 경우, JSON.parse 함수를 사용하여 JSON(JavaScript Object Notation) 텍스트를 deserialize 하는 것이 eval 함수보다 안전하고 실행 속도도 빠르다.

~~~ javascript
var dateFn = "Date(1971,3,8)";
var myDate;
eval("myDate = new " + dateFn + ";");

document.write(myDate);

// Output: Thu Apr 8 00:00:00 PDT 1971
~~~
