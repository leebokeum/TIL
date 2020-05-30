### MessageSource 다국어 처리
- SpringBoot가 알아서 텍스트를 다국어 처리 할 수 있게끔 해주는 것이 MessageSource 이다.

### 방법
- SpringBoot에서는 src/main/resources/messages.properties를 찾았을 때 자동으로 MessageSource를 구성하고,
해당 파일에 다국어를 작성해주기만 하면, SpringBoot가 알아서 사용자 언어를 확인한 후 메시지를 변환해준다.