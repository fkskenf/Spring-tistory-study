
# Intellij에서 Junit 간단히 사용하는 방법

1. Junit dependency 추가
```xml
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.12</version>
</dependency>
```

2. test 폴더 생성 (src.test.java.prj.class)
> 1. src 하위에 Directory 생성 : test.java
> 2. java 하위에 package 생성 : test.java.prj 
> 3. prj 하위에 class 생성

3. test Class 작성
```java
import static org.junit.Assert.assertEquals;

public class junitTest {

  @Test
  public void test(){
    System.out.println("성공");
    assertEquals("1", "1");
  }
}
```

4. Junit 설정 확인
> - Project Setting > Modules > Tests에 test 폴더가 포함되어 초록에 메세지가 뜨는지 확인

5. 실행
> 1. 마우스 우클릭 > Run 'test()' 클릭 

<br>

# Spring에서 Junit을 활용한 TDD 방법론 
1. dependency 추가
```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.junit</groupId>
            <artifactId>junit-bom</artifactId>
            <version>5.8.2</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.assertj</groupId>
        <artifactId>assertj-core</artifactId>
        <version>3.22.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

또는

```xml
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter</artifactId>
  <version>5.8.2</version>
  <scope>test</scope>
</dependency>
```

