### View Resolver
- 컨트롤러가 논리적인 이름으로 모델을 랜더링하기 위해 구현되어있는 뷰를 결정하는 것
- View 이름으로부터 사용할 View Object를 매핑하는 역할.
- 특정 ViewResolver를 Bean으로 등록하지 않으면, DispatcherServlet은 기본 viewResolver인 InternalResourceView를 사용한다.

### 사용법
~~~ java
// 웹 애플리케이션 뷰 리소스의 물리적인 Path를 결정하기 위해 접두사(prefix)와 접미사(suffix)를 뷰 이름에 붙이는 규칙을 따른다.
@Bean
public ViewResolver viewResolver () 
{
    InternalResourceViewResolver resolver = new InternalResourceViewResolver();
    resolver.setPrefix("/WEB-INF/views/");
    resolver.setSuffix(".jsp");
    return resolver;
}

~~~

### 종류
|  뷰 리졸버                      |  설 명                                                                                                         |
|---------------------------------|----------------------------------------------------------------------------------------------------------------|
|  BeanNameViewResolver           |  뷰 이름과 같은 아이디를 갖는 스프링의 애플리케이션 컨텍스트의 빈으로 뷰를 결정한다.                           |
|  ContentNegotiatingViewResolver |  클라이언트가 원하는 컨텐츠 타입을 고려하여 뷰를 결정하고,   그 타입을 만들 수 있는 다른 뷰 리졸버로 위임한다. |
|  FreeMarkerViewResolver         |  FreeMarker 템플릿으로 뷰를 결정한다.                                                                          |
|  InternalResourceViewResolver   |  웹 애플리케이션 내부의 리로스로 뷰를 결정한다. 일반적으로 JSP                                                 |
|  JasperReportsViewResolver      |  Jasper Reports 정의로 뷰를 결정한다.                                                                          |
|  ResourceBundleViewResolver     |  리소스 번들(프로퍼피 파일)로 뷰를 결정한다.                                                                   |
|  TilesViewResolver              |  뷰 이름과 같은 아이디를 가진 아파치 타일즈로 뷰를 결정한다.  별도의 TilesViewResolver가 있다.                 |
|  UrlBasedViewResolver           |  뷰 이름과 일치하는 물리적인 뷰 정의로 직접 뷰를 결정한다.                                                     |
|  VelocityLayoutViewResolver     |  벨로시티 템플릿들로 페이지를 구성하는 벨로시티 레이아웃을 뷰로 결정한다.                                      |
|  VelocityViewResolver           |  벨로시티 템플릿으로 뷰를 결정한다.                                                                            |
|  XmlViewResolver                |  XML 파일로부터의 빈 정의 뷰를 결정한다.                                                                       |
|  XsltViewResolver               |  XLST 변형 결과로 렌더링되는 뷰를 결정한다.                                                                    |
