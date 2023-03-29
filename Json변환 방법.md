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
