# Branch
1. git 또는 sourceTree를 통해 branch 추가

# Profile
1. pom.xml에 profile 추가
2. resources하위에 해당 profile 파일 생성
> 1. DB 접속정보 변경
> 2. property값 변경

# Endpoint 변경
1. pom.xml의 finalName 변경
> 변경 후 빌드하면, tomcat > webapps > 변경된 finalName.war로 생성되고, tomcat 빌드시 자동으로 압축해제
```xml
<profile>
  <id>dev-g</id>
  <properties>
    <env>dev-g</env>
    <spring.profiles.active>dev-g</spring.profiles.active>
  </properties>
  <build>
    <finalName>g</finalName> <!-- war파일명 -->
  </build>
</profile>
```
> finalName을 설정하지 않고, maven package goal로 빌드를 하면 artifactId-version.war 로 war 파일이 생성된다.

2. Tomcat내 war파일 경로 설정 (endpoint)
> - 수동 설정시
>> 1. tomcat > conf > server.xml > < Host > 태그 > < Context > 태그 추가
>> 2. < Path, docBase = war파일명 > 수정
> - 젠킨스 사용시
>> 1. profile 관련 설정 적용 필요 

3. IP:포트/war파일명 호출하여 테스트
