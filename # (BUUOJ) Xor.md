# (BUUOJ) Xor

打开IDA，程序入口为```_main```函数，查看反汇编代码。根据```lea rax, aInputYourFlag```指令，大致知道该程序为输入并判断flag的程序。接下来查找可以字符串：

<img src="C:\Users\zhangsiyu\Pictures\Screenshots\屏幕截图(126).png" style="zoom:50%;" />

<img src="C:\Users\zhangsiyu\Pictures\Screenshots\屏幕截图(127).png" style="zoom:50%;" />

初步怀疑图中所选中的字符串可能与flag有关。查看main函数的汇编代码，出现21h（十进制的33，与所怀疑的字符串长度相等），且发现调用了```_strlen```函数，应该是为了避免直接查找到flag而对flag字符串进行了加密，将操作字符串部分的代码找到并解释清楚，便可破解出flag。

<img src="C:\Users\zhangsiyu\Pictures\屏幕截图 2021-01-05 231924.png" style="zoom:50%;" />

此处为一个循环，21h就是字符串的长度，变量```[rbp+var_124]``` 初始化为1（由```mov [rbp+var_124], 1```知）。这里我们将```[rbp+var_124]```记作```i```。可知该循环每次对字符串第``` i ```个元素和``` i - 1```个元素进行```xor```运算，最后得到真正的flag字符串。
此时可将字符串放到python脚本中进行处理。

![image-20210106094137290](C:\Users\zhangsiyu\AppData\Roaming\Typora\typora-user-images\image-20210106094137290.png)

最后根据输出，flag是```{QianQiuWanDai_YiTongJiangHu}```，完成。
