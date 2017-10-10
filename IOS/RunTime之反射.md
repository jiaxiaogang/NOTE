


## 可以直接调用消息方式有三种：
1. performSelector:withObject；

  ```
  完成简单的调用。对于>2个的参数或者有返回值的处理不友好
  ```
2. NSInvocation。

  ```
  使用NSInvocation来进行相对复杂,支持>2个参数和返回值;
  ```
3. objc_msgsend

## performSelector:withObject:用法

  ```objective-c
  @property (strong,nonatomic) id clickTarget;
  @property (assign, nonatomic) SEL clickAction;

  if (self.clickTarget && self.clickAction && [self.clickTarget respondsToSelector:self.clickAction]) {
        [self.clickTarget performSelector:self.clickAction withObject:self];
  }
  ```

## NSInvocation的基本使用

1. 根据方法来初始化NSMethodSignature

  ```objective-c
  //根据方法签名来创建NSInvocation对象//有可能返回nil;
  NSMethodSignature  *signature = [ViewController instanceMethodSignatureForSelector:@selector(run:)];
  ```

2. 创建NSInvocation对象

  ```objective-c
  NSInvocation *invocation = [NSInvocation invocationWithMethodSignature:signature];
  //设置方法调用者
  invocation.target = self;

  //注意：这里的方法名一定要与方法签名类中的方法一致
  invocation.selector = @selector(run:);

  //这里的Index要从2开始，以为0跟1已经被占据了，分别是self（target）,selector(_cmd)
  NSString *way = @"byCar";
  [invocation setArgument:&way atIndex:2];
  ```

3. 执行

  ```objective-c
  [invocation invoke];
  ```

## 进阶

1. check实参形参个数

  ```c
  //通过numberOfArguments方法获取的参数数(含self和_cmd),后比较，取MIN(a,b)
  NSUInteger argsCount = signature.numberOfArguments - 2;
  NSUInteger arrCount = objects.count;
  NSUInteger count = MIN(argsCount, arrCount);
  for (int i = 0; i < count; i++) {
      id obj = objects[i];
      // 判断需要设置的参数是否是NSNull, 如果是就设置为nil
      if ([obj isKindOfClass:[NSNull class]]) {
          obj = nil;
      }
  [invocation setArgument:&obj atIndex:i + 2];
  }
  ```

2. check是否有返回值

  ```c
  //方法一：
  id res = nil;
  if (signature.methodReturnLength != 0) {//有返回值
      //将返回值赋值给res
      [invocation getReturnValue:&res];
  }
  return res;

  //方法二：
  //可以通过signature.methodReturnType获得返回的类型编码，因此可以推断返回值的具体类型
  ```

## objc_msgsend用法

1. 它处使用
  ```c
  if ([self respondsToSelector:@selector(pickerView:didSelectRow:inComponent:)]) {
                void (*objc_msgSendTyped)(id target, SEL _cmd, id pickerView, NSInteger row, NSInteger component) = (void *) objc_msgSend; // sending Integers as params
                objc_msgSendTyped(self, @selector(pickerView:didSelectRow:inComponent:), picker, buttonValue, 0);
  }
  ```

2. smg系统直接使用

  ```c
  @try {
           ((void(*)(id,SEL, id,id))objc_msgSend)(self.funcClass, self.funcSel, nil, nil);

            int returnInt = ((int (*)(id, SEL, NSString *, id))objc_msgSend)((id)self.funcClass, self.funcSel, @"参数1",nil);
        } @catch (NSException *exception) {} @finally {}
  ```

3. smg封装方法使用

  ```c
    - (void *)invokeClassMethodTuple:(id)param,...
  {
      @try {
          va_list params;
          va_start(params, param);
          void *first = va_arg(params, void*);
          void *result = ((int (*)(id, SEL, ...))objc_msgSend)((id)self.funcClass, self.funcSel, first,params);
          va_end(params);
          return result;
      } @catch (NSException *exception) {} @finally {}
      return nil;
  }

  typedef void*(*ObjcMsgSend)(id, SEL, ...);

  - (void *)invokeObjMethodTuple:(id)param,...
  {
      @try {
          IMP imp = [self.funcClass instanceMethodForSelector:self.funcSel];
          ObjcMsgSend objcMsgSend = (void *)imp;
          va_list params;
          va_start(params, param);
          void *first = va_arg(params, void*);
          void *result = objcMsgSend(self.funcClass, self.funcSel, first, params);
          va_end(params);
          return result;
      } @catch (NSException *exception) {} @finally {}
      return nil;
  }
  ```
