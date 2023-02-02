# 이론
1. 비동기/ 동기
2. 블록/ 논 블록


# 비동기 적용 테스트
1. AsyncConfig.java
```java
@EnableAsync
@Configuration
public class AsyncConfig {

	@Bean("name")
	public ThreadPoolTaskExecutor threadPoolTaskExecutor() {
		ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
		executor.setCorePoolSize(5);
		executor.setMaxPoolSize(30);
		executor.setQueueCapacity(50);
		executor.setThreadNamePrefix("async-");
		executor.initialize();
		return executor;
	}
}
```
<br>

2. serviceImpl1.java (결과값이 있는경우)
```java
CompletableFuture<LuluResult> futureAgeResult = dataPmsService.asyncService(q); //데이터 없을 경우 204, 있을 경우 200 그대로 반환하기
while (!(futureAgeResult.isDone()) {
  break;
  }

LuluResult pmsresult2 = futureAgeResult.get(); // 해당 부분 에러
```
- LuluResult pmsresult2 = futureAgeResult.get(); // 해당 부분 에러
- 좀 더 공부해보자 : 스레드 이슈인듯
<br>

3. serviceImpl2.java
```java
	/*
	 * [SMC_PMS] 조인 데이터 조회 - 비동기
	 */
	@Async("name")
	@Override
	public CompletableFuture asyncService(HashMap<String, Object> param) {
		LuluResult result = new LuluResult();
		HashMap<String,Object> resultData = new HashMap<String,Object>();
		result.setResultData(resultData);

		return CompletableFuture.supplyAsync(() -> CompletableFuture.completedFuture(result)); // 비동기에러 예외처리
	}

	/*
```
