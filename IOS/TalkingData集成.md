| 注意 >> |
| --- |

|  |  |
| --- | --- |
| 1 | ios7.0及以上 |
| 2 | 后台30秒内不算启动次 |
| 3 | 灵动分析,可以动态添加event事件(不限个数) |
| 4 | event分析,限默认1000个自动分析,可手动添加到10000个; |
| 5 |  |

| 集成步骤 >> |
| --- |

|  |  |
| --- | --- |
| 1 | 导入.h和.a |
| 2 | 依赖 |
|  | AdSupport.framework |
|  | CoreTelephony.framework |
|  | CoreMotion.framework |
|  | Security.framework |
|  | SystemConfiguration.framework |
|  | libz.tbd |
|  | libc++.tbd |
| 3 | Other Linker Flags中添加“-ObjC” |
| 4 | 见:集成 >> |
| 5 | 其它见:捕获异常 >> 经纬度 >>等|


| 两种事件对比 >> |
| --- |

|  | 灵动 | event |
| --- | --- | --- |
| label | false | true |
| kv | false | true |
| count | 无限 | 1k-10k条 |
| 灵活性 | 随时添加 | 需发版 |
| 控件范围 | 点击(btn checkbox input) | 不限 |
| 维护人员 | 不限 | 开发者 |




| 集成 >> |
| --- |
```c
#import "TalkingData.h"
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions{
    [TalkingData sessionStarted:@"您的 App ID" withChannelId:@"渠道 ID"];
}
```

| 捕获异常 >> |
| --- |
```c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions{
  [TalkingData setExceptionReportEnabled:YES];
}
```

| 经纬度 >> |
| --- |
```c
[TalkingData setLatitude:纬度 longitude:经度];
```

| 页面 >> |
| --- |
```c
1. 在 viewWillAppear 或viewDidAppear方法里调用 trackPageBegin方法：
+ (void)trackPageBegin:(NSString *)pageName;
2. viewWillDisappear 或者 viewDidDisappear方法里调用trackPageEnd方法：
+ (void)trackPageEnd:(NSString *)pageName;
//注:必须成对调用
```

| Event调用 >> |
| --- |

```c
[TalkingData trackEvent:@"eventID"];
[TalkingData trackEvent:@"eventID" label:@"event_label"];
[TalkingData trackEvent:@"eventID" label:@ "label" parameters:Your_dictionary];
```

| 全局kv >> |
| --- |
```c
[TalkingData setGlobalKV:key value:value];
[TalkingData removeGlobalKV:key];
```

| 用户质量分析开关: >> |
| --- |
```c
[TalkingData setAntiCheatingEnabled:NO];
```
