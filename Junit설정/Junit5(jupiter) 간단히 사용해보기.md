
# Intellij에서 Junit5 사용하는 방법 (Spring)

1. Junit dependency 추가 (Junit5의 jupiter 사용)
```xml
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter</artifactId>
  <version>5.8.2</version>
  <scope>test</scope>
</dependency>

<!-- (위 적용) --> 
<!-- 또는 --> 

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

2. test 폴더 생성 (src.test.java.prj.class)
> 경로 : test > java > prj > test.class


3. test Class 작성
```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.DisplayName;

import static org.junit.jupiter.api.Assertions.assertEquals;

public class junitTest {

	@DisplayName("테스트 1번")
	@Test
	public void test(){
		System.out.println("성공!!!");
		assertEquals("1", "1");
	}

	@DisplayName("테스트 2번")
	@Test
	public void test2(){
		System.out.println("성공!!!");
		assertEquals("1", "1");
	}
}

```

4. Junit 설정 확인
> - Project Setting > Modules > Tests에 test 폴더가 포함되어 초록에 메세지가 뜨는지 확인

5. 실행
> 1. 마우스 우클릭 > Run 'test()' 클릭 

6. 이슈
> 1. intellij에서 Maven프로젝트에 @Display가 적용이 안된다면, import org.junit.jupiter.api.Test;, import org.junit.jupiter.api.DisplayName; 맞는지 확인 

