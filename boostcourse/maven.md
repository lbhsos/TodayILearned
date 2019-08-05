Maven이란??
====

애플리케이션을 개발하기 위해 반복적으로 진행해왔던 작업들을 지원하기 위하여 등장한 도구
Maven을 사용하면 빌드(Build), 패키징, 문서화, 테스트와 테스트 리포팅, git, 의존성관리, svn등과 같은 형상관리서버와 연동(SCMs), 배포 등의 작업을 손쉽게 할 수 있다.
  
CoC(Convention over Configuration)란 일종의 관습을 말하는데, 예를 들자면 프로그램의 소스파일은 어떤 위치에 있어야 하고, 소스가 컴파일된 파일들은 어떤 위치에 있어야 하고 등을 미리 정해놨다는 것입니다.
Maven을 사용한다는 것은 어쩌면 이러한 관습 즉 CoC에 대해서 알아나가는 것이라고도 말할 수 있습니다. 

Maven 사용할 경우 얻게 되는 이점
------
편리한 의존성 라이브러리 관리
Maven을 사용하면 설정 파일에 몇 줄 적어줌으로써 직접 다운로드 받거나 하는 것을 하지 않아도 라이브러리를 사용할 수 있습니다.
Maven을 사용하게 되면 Maven에 설정한 대로 모든 개발자가 일관된 방식으로 빌드를 수행할 수 있게 됩니다.
Maven은 또한 다양한 플러그인을 제공해줘서, 굉장히 많은 일들을 자동화시킬 수 있습니다.

Maven 기본
---
Archetype을 이용하여 Maven 기반 프로젝트를 생성할 경우 생성된 프로젝트 하위에 pom.xml 파일이 생성됩니다.

* project : pom.xml 파일의 최상위 루트 엘리먼트(Root Element)입니다.
* modelVersion : POM model의 버전입니다. 
* groupId : 프로젝트를 생성하는 조직의 고유 아이디를 결정합니다. 일반적으로 도메인 이름을 거꾸로 적습니다.
* artifactId : 해당 프로젝트에 의하여 생성되는 artifact의 고유 아이디를 결정합니다. Maven을 이용하여  pom.xml을 빌드할 경우 다음과 같은 규칙으로 artifact가 생성됩니다. artifactid-version.packaging. 위 예의 경우 빌드할 경우 examples-1.0-SNAPSHOT.jar 파일이 생성됩니다.
* packaging : 해당 프로젝트를 어떤 형태로 packaging 할 것인지 결정합니다. jar, war, ear 등이 해당됩니다.
* version : 프로젝트의 현재 버전. 추후 살펴보겠지만 프로젝트가 개발 중일 때는 SNAPSHOT을 접미사로 사용합니다. Maven의 버전 관리 기능은 라이브러리 관리를 편하게 합니다.
* name : 프로젝트의 이름입니다.
* url : 프로젝트 사이트가 있다면 사이트 URL을 등록하는 것이 가능합니다.

   
 dependencies/ 엘리먼트가 Dependency Management 기능의 핵심

Maven project 생성
-----
  
아키타입이란 일종의 프로젝트 템플릿(Template)이라고 말할 수 있습니다.  
어떤 아키타입을 선택했느냐에 따라서 자동으로, 여러 가지 파일들을 생성하거나 라이브러리를 셋팅해주거나 등의 일을 해줍니다.  
Maven을 이용하여 웹 어플리케이션을 개발하기 위해서 maven-archetype-webapp 사용  

 
Group Id: 보통 프로젝트를 진행하는 회사나 팀의 도메인 이름을 거꾸로 적음 
Artifact Id: 해당 프로젝트의 이름을 적는다.
버전은 보통 기본값(0.0.1-SNAPSHOT)으로 설정합니다.  
package: group id와 Artifact Id가 조합된 이름이 됩니다. 
Group Id를 kr.or.connect이고 Artifact Id가 mavenweb으로 설정하면, package이름은 kr.or.connect.mavenweb이 됩니다.
finish버튼을 클릭합니다.

Maven으로 생성된 프로젝트의 경우 자바 소스는 **src/main/java** 폴더에 생성됩니다.  
웹 어플리케이션과 관련된 html, css등은 src/main/webapp 폴더에서 작성  