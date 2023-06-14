## Map의 value가 배열 또는 리스트 처럼 보일경우

- 리스트 형태로 추출해보자
- HashMap<String, List<String>> data = (HashMap<String, List<String>>) ((HashMap<String, Object>) result.getResultData()).get(CommCode.DATA);

```json
{
  "status": 200,
  "message": "success",
  "data": {
    "P00000000001": [
      "http://172.16.~~~be10937368540917",
      "http://172.16.~~~be10937368540917",
      "http://172.16.~~~be10937368540917"
    ]
  }
}
```


  
## RequestParam으로 List < map > 전달받아 사용하는 방법
  
- parameter
```json
{
  "data": [
    {
      "tableName": "aAaA_bB",
      "column": 90,
      "record": 5245,
      "size": "2342912",
      "totalSize": "2375680",
      "imgType": 0,
      "updateDate": "20230519"
    }
  ]
}  
```
  
- controller
```java
@PatchMapping("/catal/meta")
	public ResponseEntity<?> updateCatalMeta(HttpServletRequest request) throws Exception {
		HashMap<String, Object> param = RequestUtil.paramToHashMap(request);
    result result = service.updateCatalMeta(param);
		return ResponseUtil.response(result);
	}
```
  
- service parsing
```java
String dataSt = StringUtil.fixNull(param.get(CommCode.DATA));
List<HashMap<String, Object>> data = new ArrayList<HashMap<String, Object>>();

//-- List parsing
try {
  ObjectMapper mapper = new ObjectMapper();
  data = (List) mapper.readValue(dataSt, List.class);
}
catch (Exception e){
  result.setResultCode(ResultCode.CONFLICT.getValue());
  result.setResultMsg("data를 Parsing하는 과정에서 오류가 발생했습니다.");
  return result;
}
```
