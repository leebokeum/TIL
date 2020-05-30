### 스프링부트 테스트
- 스프링부트에서는 @SpringBootTest 어노테이션을 통해 스프링부트 어플리케이션 테스트에 필요한 거의 모든 의존성을 제공해 준다. 또한 @SpringBootTest 어노테이션 내에 어떠한 테스트 환경으로 테스트를 실행할 것인지를 따로 지정할 수 있다.

### 예제
``` java
import org.junit.jupiter.api.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultHandlers.print;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.MOCK)
@AutoConfigureMockMvc
public class SampleSpringBootTest {

    @Autowired
    MockMvc mockMvc;

    @Test
    public void hello() throws Exception {
        mockMvc.perform(get("/hello"))
                .andExpect(status().isOk())
                .andExpect(content().string("hello saelobi"))
                .andDo(print());
    }
}

```
- @SpringBootTest는 스프링 부트 어플리케이션 테스트 시 테스트에 필요한 거의 모든 의존성을 제공 어노테이션이다. @SpringBootApplication을 기준으로 스프링 빈을 등록함과 동시에 Maven 같은 빌드 툴에 의해 추가된 스프링부트 의존성도 제공해 준다. @SpringBootTest 어노테이션에는 webEnvironment라는 값을 통해 웹 어플리케이션 테스트시 Mock으로 테스트할 것인지 실제 톰캣 같은 서블릿 컨테이너를 구동해서 테스트할 것인지를 정할 수 있다.
- AutoConfigureMockMvc는 Mock 테스트시 필요한 의존성을 제공해준다.
- MockMvc 객체를 통해 실제 컨테이너가 실행되는 것은 아니지만 로직상으로 테스트를 진행할 수 있다. (DispatcherServlet은 로딩되어 Mockup으로서 기능한다.)
- print() 함수를 통해 좀 더 디테일한 테스트 결과를 볼 수 있다.


### 참조
https://engkimbs.tistory.com/768