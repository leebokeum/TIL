### @ModelAttribute와 @RequestBody 차이
- @ModelAttribute는 파라미터 값으로 DTO객체에 바인딩을 하는 방식이기 때문에 바인딩하려는 DTO객체에 Setter메소드가 반드시 있어야 하고, @RequestBody는 요청 본문의 body에 json이나 xml값으로 요청을 하여 HttpMessageConveter를 반드시 거쳐 DTO객체에 맞는 타입으로 바꿔서 바인딩을 시켜준다. 
- @ModelAttribute와 @RequestBody를 보다 극단적으로 설명하자면, @ModelAttribute는 바인딩시키는 어떤 데이터를 set해주는 Setter함수가 없다면 매핑이 되지 않는다. 하지만 @RequestBody는 요청받은 데이터를 변환시키는 것이기 때문에, Setter함수가 없어도 값이 매핑이 된다.
