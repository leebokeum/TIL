### package-lock.json 이란?
- package-lock.json은 npm을 사용하여package.json 파일을 또는 node_modules 트리를 수정하면 자동으로 생성되는 파일이다. 한마디로 파일이 생성되는 시점의 의존성 트리에 대한 정보를 가지고 있다. 
- 간혹 업데이트된 버전이 오류를 발생시키는 경우가 있기 때문에 안정성을 위해package-lock.json은 매우 중요하다.

### 결론
- package-lock.json 파일은 의존성 트리에 대한 정보를 가지고 있으며, 작성된 시점의 의존성 트리가 다시 생성될 수 있도록 보장해준다.
- package-lock.json 파일은 저장소에 꼭 같이 커밋해야 한다.
- package-lock.json 파일은 node_modules 없이 배포하는 경우 반드시 필요하다.