### build.gradle 파일 구조

1. repositories 
    - Maven 중앙 저장소 - mavenCentral()
    - JCenter 저장소 - jcenter()
2. Dependencies
    - 저장소에서 필요한 라이브러리를 사용하기위한 문장
    - implementation 
        - 컴파일시에 의존하는(사용) 라이브러리를 지정
    - testCompile
        - 테스트 컴파일(단위테스팅)에 사용하는 라이브러리를 지정
    - classpath 
        - 컴파일부터 실행시까지 의존하는 라이브러리 지정에 사용된다
