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
