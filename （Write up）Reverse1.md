# （Write up）Reverse1

## Step 1. IDA 查找字符串



![](C:\Users\zhangsiyu\Pictures\Screenshots\屏幕截图(119).png)

发现了{hello_world}字符串，尝试以此作为flag，发现并不对。接下来发现了  
```cmp     eax, 6Fh ; 'o'```
以及
``` mov     byte ptr [rcx+rax], 30h ; '0' ``` 
应该是将o字符替换为数字0.输入flag{hell0_w0rld},成功。

