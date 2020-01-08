### ApplicationContext
- Web Application 최상단에 위치하고 있는 Context
- Spring에서 ApplicationContext란 BeanFactory를 상속받고 있는 Context
- Spring에서 root-context.xml, applicationContext.xml 파일은 ApplicationContext 생성 시 필요한 설정정보를 담은 파일 (Bean 선언 등..)
- Spring에서 생성되는 Bean에 대한 IoC Container (또는 Bean Container)
- Application Context에 정의된 Bean은 Servlet Context에 정의 된 Bean을 사용할 수 없다.
- 공통 기능을 할 수 있는 Bean설정 (Datasource, Service 등..)