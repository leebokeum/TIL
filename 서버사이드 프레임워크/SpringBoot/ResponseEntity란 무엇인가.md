## 스프링 Controller에서 return 할때 2가지
- View(HTML or JSP)
- Data(Rest API)

## ResponseEntity는 Rest Api에서 사용
- 서버에서 HTTP 프로토콜의 상태값을 헤더에 담아서 리턴한다.
- 서버에서 예외상황을 분기하여 상황에 따라 헤더에 상태값을 리턴할 수 있다.

~~~java
@RequestMapping(value = "/barcode", method = RequestMethod.POST)
    ResponseEntity<Map<String, Object>> index(@RequestBody Map<String, String> pramMap) {
        String barcode = pramMap.get("barcode");
        return new ResponseEntity<>(restApiService.findDeliveryData(barcode), HttpStatus.OK);
    }
~~~
<br>

> 서버에서 API를 리턴할때 http상태를 분기하여 리턴 가능하다.

## 수정이력
2019.08.12 최초작성
2019.08.14 다시작성