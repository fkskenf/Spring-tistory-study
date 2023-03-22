# 예시
```java
package cdw.controller.CatalogProTest;

import com.google.gson.Gson;
import lombok.Getter;
import lombok.Setter;
import lombok.ToString;

import org.junit.Test;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;

public class MakePmsCreateQueryTest {

	@Test
	public void PMS_PRO_고도화_쿼리만들기() throws Exception {

		jsonStr jsonStr = new jsonStr(); // 최상위
		jsonStr.setVersion("1");

		tableNode leftTableNode = new tableNode(); // left - table
		leftTableNode.setUuid("1");
		leftTableNode.setType("table");

		colC colc = new colC();
		colc.setCtp("C");
		colc.setTid("10005");
		colc.setId("100021947");
		colc.setAs("ptno_1");
		colc.setNm("환자번호1");
		colc.setCd("ptno");
		leftTableNode.getCols().add(colc);

		colc = new colC();
		colc.setCtp("C");
		colc.setTid("10005");
		colc.setId("100021947");
		colc.setAs("age_1");
		colc.setNm("나이1");
		colc.setCd("age");
		leftTableNode.getCols().add(colc);

		cond cond = new cond();
		cond.setLeft("ptno");
		cond.setOp("not null");
		cond.setRight("");
		leftTableNode.getFilters().add(cond);

		jsonStr.getNodes().add(leftTableNode); // 삽입

		tableNode rightTableNode = new tableNode(); // right - table
		rightTableNode.setUuid("2");
		rightTableNode.setType("table");

		colc = new colC();
		colc.setCtp("C");
		colc.setTid("10005");
		colc.setId("100021947");
		colc.setAs("ptno_2");
		colc.setNm("환자번호2");
		colc.setCd("ptno");
		rightTableNode.getCols().add(colc);

		colc = new colC();
		colc.setCtp("C");
		colc.setTid("10005");
		colc.setId("100021947");
		colc.setAs("age_2");
		colc.setNm("나이2");
		colc.setCd("age");
		rightTableNode.getCols().add(colc);

		colc = new colC();
		colc.setCtp("C");
		colc.setTid("10005");
		colc.setId("100021947");
		colc.setAs("address_1");
		colc.setNm("주소1");
		colc.setCd("address");
		rightTableNode.getCols().add(colc);

		cond = new cond();
		cond.setLeft("age");
		cond.setOp("equals");
		cond.setRight("20");
		rightTableNode.getFilters().add(cond);

		rightTableNode.getJob_nodes().add(3);

		jsonStr.getNodes().add(rightTableNode); // 삽입

		groupNode groupNode = new groupNode(); // groupby
		groupNode.setUuid("3");
		groupNode.setType("groupby");

		colc = new colC();
		colc.setCtp("C");
		colc.setTid("10005");
		colc.setId("100021947");
		colc.setAs("ptno_2");
		colc.setNm("환자번호2");
		colc.setCd("ptno");
		groupNode.setGroupby(colc);

		colF groups = new colF();
		groups.setF("MAX");
		groups.setAs("MAX_age");
		groups.setNm("최대_환자번호");
		colc = new colC();
		colc.setTid("10005");
		colc.setId("100021947");
		colc.setAs("age_2");
		colc.setNm("나이2");
		colc.setCd("age");
		groups.getFp().add(colc);
		groupNode.getGroups().add(groups);

		groups = new colF();
		groups.setF("COUNT");
		groups.setAs("COUNT_address");
		groups.setNm("카운트_주소");
		colc = new colC();
		colc.setTid("10005");
		colc.setId("100021947");
		colc.setAs("address_1");
		colc.setNm("주소1");
		colc.setCd("address");
		groups.getFp().add(colc);
		groupNode.getGroups().add(groups);

		groupNode.setOrigin_node("2");

		jsonStr.getNodes().add(groupNode); // 삽입

		joinNode joinNode = new joinNode(); // join
		joinNode.setUuid("4");
		joinNode.setType("join");

		joinNode.setNode_left("1");
		joinNode.setNode_right("3");
		joinNode.setJoin_method("LO");

		colc = new colC();
		colc.setCtp("C");
		colc.setTid("10005");
		colc.setId("100021947");
		colc.setAs("ptno_1");
		colc.setNm("각 컬럼이 어떤 테이블에서 나왔는지 알아야합니다.");
		colc.setCd("join-Col에 어떤값이 들어갈지 정의가 필요합니다.");
		joinNode.getCols().add(colc);

		cond = new cond();
		cond.setLeft("ptno_1");
		cond.setOp("equals");
		cond.setRight("ptno_2");
		joinNode.getJoin_cond().add(cond);

		jsonStr.getNodes().add(joinNode); // 삽입

		// 변환 & 출력
		Gson gson = new Gson();
		String print = gson.toJson(jsonStr);
		System.out.print(print);
	}
}

/*
 * json_str 클래스 선언부
 */

@Getter
@Setter
@ToString
class jsonStr {
	private String version = "";
	private List nodes = new ArrayList();
}

@Getter
@Setter
@ToString
class comm {
	private String uuid = "";
	private String type = "";
	private HashMap<String, Object> position = new HashMap<String, Object>() {
		{
			put("x", 1);
			put("y", 2);
		}

	};
}

@Getter
@Setter
@ToString
class tableNode extends comm {
	private List<colC> cols = new ArrayList<colC>();
	private List<cond> filters = new ArrayList<cond>();
	private List job_nodes = new ArrayList();
}

@Getter
@Setter
@ToString
class groupNode extends comm {
	private colC groupby = new colC();
	private List<colF> groups = new ArrayList<colF>();
	private String origin_node = "";
}

@Getter
@Setter
@ToString
class joinNode extends comm {
	private String node_left = "";
	private String node_right = "";
	private String join_method = "";
	private List<colC> cols = new ArrayList<colC>();
	private List<cond> join_cond = new ArrayList<cond>();
}

@Getter
@Setter
@ToString
class colC {
	private String ctp = "C";
	private String tid = "";
	private String id = "";
	private String as = "";
	private String nm = "";
	private String cd = "";
}

@Getter
@Setter
@ToString
class colV {
	private String ctp = "V";
	private String val = "";
	private String as = "";
	private String nm = "";
}

@Getter
@Setter
@ToString
class colF {
	private String ctp = "F";
	private String f = "";
	private List<colC> fp = new ArrayList<colC>();
	private String as = "";
	private String nm = "";
}

@Getter
@Setter
@ToString
class cond {
	private String left = "";
	private String op = "";
	private String right = "";
}
```

# 결과
```json
{
  "version": "1",
  "nodes": [
    {
      "cols": [
        {
          "ctp": "C",
          "tid": "10005",
          "id": "100021947",
          "as": "ptno_1",
          "nm": "환자번호1",
          "cd": "ptno"
        },
        {
          "ctp": "C",
          "tid": "10005",
          "id": "100021947",
          "as": "age_1",
          "nm": "나이1",
          "cd": "age"
        }
      ],
      "filters": [
        {
          "left": "ptno",
          "op": "not null",
          "right": ""
        }
      ],
      "job_nodes": [],
      "uuid": "1",
      "type": "table",
      "position": {
        "x": 1,
        "y": 2
      }
    },
    {
      "cols": [
        {
          "ctp": "C",
          "tid": "10005",
          "id": "100021947",
          "as": "ptno_2",
          "nm": "환자번호2",
          "cd": "ptno"
        },
        {
          "ctp": "C",
          "tid": "10005",
          "id": "100021947",
          "as": "age_2",
          "nm": "나이2",
          "cd": "age"
        },
        {
          "ctp": "C",
          "tid": "10005",
          "id": "100021947",
          "as": "address_1",
          "nm": "주소1",
          "cd": "address"
        }
      ],
      "filters": [
        {
          "left": "age",
          "op": "equals",
          "right": "20"
        }
      ],
      "job_nodes": [
        3
      ],
      "uuid": "2",
      "type": "table",
      "position": {
        "x": 1,
        "y": 2
      }
    },
    {
      "groupby": {
        "ctp": "C",
        "tid": "10005",
        "id": "100021947",
        "as": "ptno_2",
        "nm": "환자번호2",
        "cd": "ptno"
      },
      "groups": [
        {
          "ctp": "F",
          "f": "MAX",
          "fp": [
            {
              "ctp": "C",
              "tid": "10005",
              "id": "100021947",
              "as": "age_2",
              "nm": "나이2",
              "cd": "age"
            }
          ],
          "as": "MAX_age",
          "nm": "최대_환자번호"
        },
        {
          "ctp": "F",
          "f": "COUNT",
          "fp": [
            {
              "ctp": "C",
              "tid": "10005",
              "id": "100021947",
              "as": "address_1",
              "nm": "주소1",
              "cd": "address"
            }
          ],
          "as": "COUNT_address",
          "nm": "카운트_주소"
        }
      ],
      "origin_node": "2",
      "uuid": "3",
      "type": "groupby",
      "position": {
        "x": 1,
        "y": 2
      }
    },
    {
      "node_left": "1",
      "node_right": "3",
      "join_method": "LO",
      "cols": [
        {
          "ctp": "C",
          "tid": "10005",
          "id": "100021947",
          "as": "ptno_1",
          "nm": "각 컬럼이 어떤 테이블에서 나왔는지 알아야합니다.",
          "cd": "join-Col에 어떤값이 들어갈지 정의가 필요합니다."
        }
      ],
      "join_cond": [
        {
          "left": "ptno_1",
          "op": "equals",
          "right": "ptno_2"
        }
      ],
      "uuid": "4",
      "type": "join",
      "position": {
        "x": 1,
        "y": 2
      }
    }
  ]
}
```
