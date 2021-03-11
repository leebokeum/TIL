### JSON과 JSONP 
- JSON 이란?
1. JSON은 경량(Lightweight)의 DATA-교환 형식
2. Javascript에서 객체를 만들 때 사용하는 표현식을 의미한다.
3. JSON 표현식은 사람과 기계 모두 이해하기 쉬우며 용량이 작아서, 최근에는 JSON이 XML을 대체해서 데이터 전송 등에 많이 사용한다.
4. 특정 언어에 종속되지 않으며, 대부분의 프로그래밍 언어에서 JSON 포맷의 데이터를 핸들링 할 수 있는 라이브러리를 제공한다

- JSONP 이란?
1. CORS가 활성화 되기 이전의 데이터 요청 방법으로, 다른 도메인으로부터 데이터를 가져오기 위해 사용하는 방법입니다.
2. 자바스크립트는 서로 다른 도메인에 대한 요청을 보안상 제한하는데, 이 정책은 Same-Origin Policy, SOP라고 합니다.
3. SOP 정책으로 인해 생기는 이슈를 Cross-domain issue라고 하는데 JSONP는 이 이슈를 우회해서 데이터 공유를 가능하게 하였습니다.

### 차이
jQuery v.1.2 이상부터 jsonp 형태가 지원되며. 
$.ajax 옵션에서 dataType: "jsonp" 를 설정해야한다. type은 GET으로 해야한다.
현재는 다양한 타입을지원하는 CORS가 대중적으로 사용되나 이전에는 JSONP 를 사용함

``` js
json
{'home' : '대전', 'author':'park'};

jsonp
callback({'home' : '대전', 'author' : 'park'})

$.ajax({
   type: "GET",
   async: "false",
   url: "http://{server_ip}/jsp/domain/registrationInfo/jsonp.jsp",
   dataType: "jsonp",
   data: { },
   callback : "list" ,
   success : function(data) {
         $(data.addr).each(function(key, val){
              alert(val.apt); 
         });
   },
   error : function(){
          alert("Fail");
   }
});

이렇게 Ajax 요청을 보내면
callback 파라미터가 무작위 생성되어 같이 보내진다.
받는 쪽에서 callback 파라미터 값을 받아 json 데이터 앞에 명시해 주어 응답해야 한다.

<%
 System.out.println("jsonp test");
 String callback = request.getParameter("callback");
 System.out.println("calback::" + callback);
%>
<%=callback%>({"people" : [{"home": "대전", "author" : "park"} ],
"addr" : [{"apt" : "uneed apt", "floors" : 11 }] })

이것을 제외하면 json 과 똑같다.

```