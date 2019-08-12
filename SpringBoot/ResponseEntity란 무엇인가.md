## 스프링 Controller에서 return 할때 2가지
- View(HTML or JSP)
- Data(Rest API)

## ResponseEntity는 Rest Api에서 사용
- Data와 HTTP 프로토콜의 상태값을 함께 반환할 수 있다.
- 받는 쪽에서는 상태를 확인하여 분기처리하기 용이하다.

~~~java
@RequestMapping(value = "/barcode", method = RequestMethod.POST)
    ResponseEntity<Map<String, Object>> index(@RequestBody Map<String, String> pramMap) {
        String barcode = pramMap.get("barcode");
        return new ResponseEntity<>(restApiService.findDeliveryData(barcode), HttpStatus.OK);
    }
~~~
<br>

> API를 요청한 클라이언트는 응답상태를 쉽게 파악하여 데이터를 핸들링 할 수 있다.

## 수정이력
2019.08.12 최초작성