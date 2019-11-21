##### 此代码,可以使:
1. guava在更新实现异步; (refreshAfterWrite)
2. guava的过期保持同步; (expireAfterWrite)

```java
public static void main(String[] args) throws ExecutionException, InterruptedException{

		final long startT = System.currentTimeMillis();
		final ListeningExecutorService backgroundRefreshPools = MoreExecutors
				.listeningDecorator(Executors.newFixedThreadPool(20));
		LoadingCache<String, Object> cache = CacheBuilder.newBuilder().maximumSize(100).refreshAfterWrite(2, TimeUnit.SECONDS).expireAfterWrite(4, TimeUnit.SECONDS).build(new CacheLoader<String, Object>() {
					@Override
					public Object load(String key) throws Exception {
						RcmdUtils.printInfo("------S",System.currentTimeMillis() - startT);
						for (int i = 0; i < 1000000; i++) {
							int a = 288 * 822 / 1992 / 2888;
							int b = a / 100;
						}
						RcmdUtils.printInfo("------E",System.currentTimeMillis() - startT);
						return 3;
					}

					@Override
					public ListenableFuture<Object> reload(final String key, Object oldValue) throws Exception {
						return backgroundRefreshPools.submit(new Callable<Object>() {

							@Override
							public Object call() throws Exception {
								return load(key);
							}
						});
					}
				});

		cache.put("key", "100");
		Thread.sleep(2100);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		Thread.sleep(1100);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		Thread.sleep(2000);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		Thread.sleep(4100);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		RcmdUtils.printInfo(cache.get("key"),System.currentTimeMillis() - startT);
		//打印内容
		//2019.11.21 19:34:23 INFO  com.ddgs.host.Host - jiadeMacBook-Pro-2.local is LOCAL
		//2019.11.21 19:34:23 INFO  com.ddgs.recommendation.RcmdUtils - ------S 2149
		//2019.11.21 19:34:23 INFO  com.ddgs.recommendation.RcmdUtils - 100 2165
		//2019.11.21 19:34:23 INFO  com.ddgs.recommendation.RcmdUtils - 100 2183
		//2019.11.21 19:34:23 INFO  com.ddgs.recommendation.RcmdUtils - 100 2183
		//2019.11.21 19:34:23 INFO  com.ddgs.recommendation.RcmdUtils - ------E 2187
		//2019.11.21 19:34:24 INFO  com.ddgs.recommendation.RcmdUtils - 3 3285
		//2019.11.21 19:34:24 INFO  com.ddgs.recommendation.RcmdUtils - 3 3285
		//2019.11.21 19:34:24 INFO  com.ddgs.recommendation.RcmdUtils - 3 3285
		//2019.11.21 19:34:26 INFO  com.ddgs.recommendation.RcmdUtils - ------S 5290
		//2019.11.21 19:34:26 INFO  com.ddgs.recommendation.RcmdUtils - 3 5290
		//2019.11.21 19:34:26 INFO  com.ddgs.recommendation.RcmdUtils - 3 5291
		//2019.11.21 19:34:26 INFO  com.ddgs.recommendation.RcmdUtils - ------E 5291
		//2019.11.21 19:34:26 INFO  com.ddgs.recommendation.RcmdUtils - 3 5292
		//2019.11.21 19:34:30 INFO  com.ddgs.recommendation.RcmdUtils - ------S 9398
		//2019.11.21 19:34:30 INFO  com.ddgs.recommendation.RcmdUtils - ------E 9406
		//2019.11.21 19:34:30 INFO  com.ddgs.recommendation.RcmdUtils - 3 9406
		//2019.11.21 19:34:30 INFO  com.ddgs.recommendation.RcmdUtils - 3 9406
		//2019.11.21 19:34:30 INFO  com.ddgs.recommendation.RcmdUtils - 3 9407
	}
```
