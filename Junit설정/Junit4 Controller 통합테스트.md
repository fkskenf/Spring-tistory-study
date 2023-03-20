## 1. Maven Dependency 추가
> 아래 test class 작성 후 필요한 dependency 

## 2. Test Class 작성
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

## 3. 결과
![image](https://user-images.githubusercontent.com/60438691/221479720-78de7e2d-d499-434e-9598-6ebf38e1fa1d.png)

## 4. 적용
```java
package cdw.controller.***Test;

import com.***.***.common.constants.CommCode;
import com.***.***.dataselector.controller.***Controller;
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
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
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@RunWith(SpringJUnit4ClassRunner.class)
@WebAppConfiguration
@ContextConfiguration(locations = {
	"file:src/main/webapp/WEB-INF/dispatcher-servlet.xml",
	"file:src/main/resources/spring/context-common.xml",
	"file:src/main/resources/spring/context-datasource.xml",
	"file:src/main/resources/spring/context-interceptor.xml",
	"file:src/main/resources/spring/context-mapper.xml",
	"file:src/main/resources/spring/context-redis.xml",
	"file:src/main/resources/spring/context-scheduler.xml",
	"file:src/main/resources/spring/context-transaction.xml"
})
public class CatalogCommControllerTest {
	protected Logger logger = LogManager.getLogger(this.getClass());

	@Autowired
	private WebApplicationContext context;
	private MockMvc mock;

	@Autowired
	private ***Controller ***Controller;

	// 세션체크 필수 값
	private static String cno = "10051";
	private static String Authorization = "Bearer WieOfqon070OM0qrFkwkHsXQegMzCs";

	@Before
	public void setup() throws FileNotFoundException {
		mock = MockMvcBuilders.webAppContextSetup(context).build();
	}

	@Test
	public void 필드_라디오_셀렉트_목록조회() throws Exception {
		System.out.println("#################### 필드_라디오_셀렉트_목록조회 #################### ");
		mock.perform(MockMvcRequestBuilders
				.get("/***/comm/data/cols/radio-sel")
				.header("Authorization", Authorization)
				.param(CommCode.CNO, cno)
				.param(CommCode.TABL_SNO, "10079")
				.param(CommCode.CLMN_SNO, "100004335")
				.param(CommCode.DMAN, "POPUP")
				.param(CommCode.PAGE_NO, "1")
				.param(CommCode.PAGE_SIZE, "50")
				.accept(MediaType.APPLICATION_JSON_UTF8))
			.andDo(print())
			.andExpect(status().isCreated());
	}

	@Test
	public void 데이터셋_필터_필드_팝업1_2_선택컬럼_정보조회() throws Exception {
		System.out.println("#################### 데이터셋_필터_필드_팝업1_2_선택컬럼_정보조회 #################### ");
		mock.perform(MockMvcRequestBuilders
				.post("/***/comm/data/cols/popup/names")
				.header("Authorization", Authorization)
				.param(CommCode.CNO, cno)
				.param(CommCode.TABL_SNO, "10079")
				.param(CommCode.CLMN_SNO, "100004335")
				.param(CommCode.DMAN, "POPUP")
				.param(CommCode.V1, "1")
				.accept(MediaType.APPLICATION_JSON_UTF8))
			.andDo(print())
			.andExpect(status().isCreated());
	}

	@Test
	public void 팝업_계층트리목록_조회() throws Exception {
		System.out.println("#################### 팝업_계층트리목록_조회 #################### ");
		mock.perform(MockMvcRequestBuilders
				.get("/***/comm/code-tree")
				.header("Authorization", Authorization)
				.param(CommCode.CNO, cno)
				.accept(MediaType.APPLICATION_JSON_UTF8))
			.andDo(print())
			.andExpect(status().isCreated());
	}

	@Test
	public void 팝업_선택그룹_하위코드목록_조회() throws Exception {
		System.out.println("#################### 팝업_선택그룹_하위코드목록_조회 #################### ");
		mock.perform(MockMvcRequestBuilders
				.get("/***/comm/code-tree/codes")
				.header("Authorization", Authorization)
				.param(CommCode.CNO, cno)
				.param(CommCode.PAGE_NO, "1")
				.param(CommCode.PAGE_SIZE, "50")
				.accept(MediaType.APPLICATION_JSON_UTF8))
			.andDo(print())
			.andExpect(status().isCreated());
	}

	@Test
	public void 필드_선택을_위한_조회() throws Exception {
		System.out.println("#################### 필드_선택을_위한_조회 #################### ");
		mock.perform(MockMvcRequestBuilders
				.get("/***/comm/data/groupcol-info")
				.header("Authorization", Authorization)
				.param(CommCode.CNO, cno)
				.param(CommCode.TREE_SNO_LIST, "10079,10029")
				.accept(MediaType.APPLICATION_JSON_UTF8))
			.andDo(print())
			.andExpect(status().isCreated());
	}
}
```
