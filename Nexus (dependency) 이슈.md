# 메이븐 의존성 Nexus 와 Central 에서 가져오기(로컬전용) 

## 1.의존성 문제
- 스프링(메이븐)을 사용하면서 해결하기 까다로운 문제중 하나.
- 메이븐 중앙저장소에서 의존성을 내려받을 경우 보통 연계된 의존성을 모두 받아오기때문에 크게 문제가 발생하지 않지만 사내 Nexus에는 최신버전의 jar가 없는경우도 많고 연계된 의존성들이 없는경우가 종종있어 의존성 문제에 직면하기 쉬움.
- 의존성 문제가 발생하게 되면 보통 Central에서 jar를 다운받아 프로젝트에 추가하고 System Scope로 pom에 추가해서 사용하게되는데 여 러가지 단점이 있다.
> - 단점1. 연계된 의존성을 직접 다 찾아서 계속 추가해줘야 한다.
> - 단점2. 라이브러리를 직접 관리해야 한다.(연계된 의존성이 많을 수록 관리해야할 포인트가 더 많아진다.)
> - 단점3. System Scope로 추가해도 플러그인 설정 등에서 추가한 로컬 라이브러리를 바라보지 않아 빌드조차 못하는 경우가 있음.
- 이러한 의존성 문제들을 해결하느라 개발은 시작도 못하고 시간을 낭비하게된다.

## 2.Nexus와 Central을 동시에 사용
- 의존성을 내려받을 원격저장소를 Nexus 와 Central 두개 모두 설정해준다.
- 아래와 같이 설정 할 경우 먼저 Nexus에서 추가한 의존성들을 찾고 없으면 중앙저장소에서 찾는다.(해당 설정 사용 시 m2 폴더의 settings. xml 파일을 삭제하거나 이름을 변경해야함)
```xml
<repositories>
  <repository>
    <id>Nexus</id>
    <name>Nexus Public Server</name> 
    <url>http://172.**.***.***:8081/nexus/content/groups/public</url>
  </repository>
  <repository>
    <id>central</id>
    <name>Central Repository</name>
    <url>https://repo.maven.apache.org/maven2</url> 
  </repository>
</repositories>
```
- 위와 같은 방법으로 로컬에서 빠르게 라이브러리 테스트를 하고 Nexus에 없는건 추가 요청한다.
- 반드시 로컬 환경에서 테스트용으로만 사용되어야함(profile local 에 적용).

## 3.Nexus에 추가된 jar가 내려받아지지 않을때.
- Nexus에 jar가 추가되었고 검색도 되는 상태에서 로컬로 내려받아지지 않을때.
- m2의 로컬 레파지토리 폴더를 삭제하고 다시 빌드해도 jar를 못찾거나 pom에서는 에러가 안나지만 빌드 시 에러날 경우.
> - m2의 settings.xml 의 updatePolicy를 always로 변경 후 로컬 레파지토리 폴더 삭제 후 재빌드
