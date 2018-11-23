| 安装gcc >> |  |
| --- | --- |
| 1 | 成功后,在终端`gcc -v` 可以显示出版本4.2.1 |

| helloWorld >> |  |
| --- | --- |
| 1 | vim创建helloworld.c |
| 2 | 输入代码段A |
| 3 | 保存 `:wq` |
| 4 | 编译 `gcc helloworld.c` 生成a.out |
| 5 | 执行 `./a.out helloworld.c` |
| 6 | 打出 `helloWorld\n` |

```c
//代码段A
#include<stdio.h>
int main(){
  printf("helloWorld\n");
  return 0;
}
```
