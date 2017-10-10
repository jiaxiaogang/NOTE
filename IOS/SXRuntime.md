## 替换方法

```c
[self swizzleInstanceMethodWithOriginSel:@selector(setLeftBarButtonItem:)
                                 swizzledSel:@selector(sx_setLeftBarButtonItem:)];
```
