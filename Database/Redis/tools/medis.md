### medis
- Medis는 Node.js, React, Electron으로 만들어진 오픈소스 Redis 클라이언트 어플리케이션입니다. 키와 config의 조회 및 수정, SSH 터널링, 커맨드 입력을 위한 터미널 등 기본적인 기능과 많은 고급 기능들을 지원한다.
- macOS용 클라이언트는 직접 빌드해서 사용해야 합니다. Mac App Store에서 $4.99에 유료 버전이 판매되고 있지만 직접 빌드한 것과 기능상의 차이는 없다.ㄴ
~~~ sh
git clone https://github.com/luin/medis.git
cd medis
npm i
npm run pack
# webpack analyzer가 뜨고 난 후 프로세스를 종료하세요 (^C)

node bin/pack.js
# No identity found for signing 에러는 무시하세요
cd dist/out/Medis-mas-x64/
open .
# Finder가 열리고 Medis.app이 보일 겝니다.
~~~