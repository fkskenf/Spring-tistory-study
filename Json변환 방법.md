# Map -> Json
```java
JSONObject jsonObject = new JSONObject(map);
System.out.println(jsonObject);
```

# String(json구조) -> Json
```java
Gson gson = new Gson();
String jsonObject = gson.toJson(str);
System.out.print(jsonObject);
```

# String(json구조) -> Map
```java
JsonParser parser = new JsonParser();
JsonObject obj = (JsonObject)parser.parse(jsonStr.toString());

//json -> hashmap으로 변환
//Gson : java Object > JSON, JSON > java Object로 변환을 도와주는 라이브러리
Gson gson =new Gson();
Map map =new HashMap();
map = (Map)gson.fromJson(obj, map.getClass());
```
