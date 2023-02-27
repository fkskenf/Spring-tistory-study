# maven dependency 추가
> 아래 test class 작성 후 필요한 dependency 

# Test Class 작성
```java
package ***;

import com.***.controller.**Controller;;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.MediaType;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.test.context.web.WebAppConfiguration;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import org.springframework.web.context.WebApplicationContext;

import java.io.FileNotFoundException;

import static org.springframework.test.web.servlet.result.MockMvcResultHandlers.print;

@RunWith(SpringJUnit4ClassRunner.class)
@WebAppConfiguration
@ContextConfiguration(locations = {"file:src/main/webapp/WEB-INF/dispatcher-servlet.xml",
	"file:src/main/resources/spring/context-common.xml",
	"file:src/main/resources/spring/context-datasource.xml",
	"file:src/main/resources/spring/context-interceptor.xml",
	"file:src/main/resources/spring/context-mapper.xml",
	"file:src/main/resources/spring/context-redis.xml",
	"file:src/main/resources/spring/context-scheduler.xml",
	"file:src/main/resources/spring/context-transaction.xml"
})

public class junitTest {
	@Autowired
	private WebApplicationContext context;
	private MockMvc mock;

	@Autowired
	private ***Controller ***Controller;

	@Before
	public void setup() throws FileNotFoundException {
		mock = MockMvcBuilders.webAppContextSetup(context).build();
	}

	@Test
	public void test1() throws Exception {
		System.out.println("성공!!!");

		mock.perform(MockMvcRequestBuilders
				.get("/catalogs/groupcols")
				.header("Authorization", "Bearer 21MSPnnyUWNEAluz0SwYQUGaFNs95u")
				.param("cno", "10051")
				.param("tree_grp_list", "10022,10026")
				.accept(MediaType.APPLICATION_JSON_UTF8))
			.andDo(print());
	}

	@Test
	public void test12() throws Exception {
		System.out.println("성공!!!");

		mock.perform(MockMvcRequestBuilders
				.get("/catalogs/groupcols")
				.header("Authorization", "Bearer 21MSPnnyUWNEAluz0SwYQUGaFNs95u")
				.param("cno", "10051")
				.param("tree_grp_list", "10022")
				.accept(MediaType.APPLICATION_JSON_UTF8))
			.andDo(print());
	}

//	@DisplayName("테스트 2번")
	@Test
	public void test2(){
		System.out.println("성공!!!");
//		assertEquals("1", "1");
	}

//	@DisplayName("테스트 1번")
	@Test
	public void test3(){
		System.out.println("성공!!!");
//		assertEquals("1", "1");
	}
}
```
