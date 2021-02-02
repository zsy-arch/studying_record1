# （BUUOJ）Reverse 3

## 查找字符串
在IDA的strings windows发现不规则字符串“e3nifIH9b_C@n@dH”，但是还不能确定flag。


## 程序大致流程：
1. 输入flag
2. 加密输入的flag（Base64加密）
3. 将所得加密字符串每个字符加上其索引值（也就是修改字符串中每个字符的ASCII）得到最终结果
4. 将第三步所得字符串与正确结果比对，并输出。

## Base64加密算法的发现
```
.text:002C5758
.text:002C5758 loc_2C5758:
.text:002C5758 push    offset aPleaseEnterThe ; "please enter the flag:"
.text:002C575D call    sub_2C132F
.text:002C5762 add     esp, 4
.text:002C5765 lea     eax, [ebp+Str]
.text:002C5768 push    eax             ; char
.text:002C5769 push    offset a20s     ; "%20s"
.text:002C576E call    sub_2C1375
				^ 由“%20”以及对程序流程的判断可知此处为scanf函数的调用
.text:002C5773 add     esp, 8
.text:002C5776 mov     esi, esp
.text:002C5778 push    28h ; '('       ; Count
.text:002C577A lea     eax, [ebp+var_C]
.text:002C577D push    eax
.text:002C577E lea     ecx, [ebp+Str]
.text:002C5781 push    ecx             ; Str
.text:002C5782 call    j_strlen
.text:002C5787 add     esp, 4
.text:002C578A push    eax
.text:002C578B lea     edx, [ebp+Str]
.text:002C578E push    edx
.text:002C578F call    sub_2C10BE
				^ 可疑的函数调用
.text:002C5794 add     esp, 0Ch
.text:002C5797 push    eax             ; Source
.text:002C5798 lea     eax, [ebp+Destination]
.text:002C579E push    eax             ; Destination
.text:002C579F call    ds:strncpy
.text:002C57A5 add     esp, 0Ch
.text:002C57A8 cmp     esi, esp
.text:002C57AA call    j___RTC_CheckEsp
.text:002C57AF lea     eax, [ebp+Destination]
.text:002C57B5 push    eax             ; Str
.text:002C57B6 call    j_strlen
.text:002C57BB add     esp, 4
.text:002C57BE mov     [ebp+var_A0], eax
.text:002C57C4 mov     [ebp+var_AC], 0
.text:002C57CE jmp     short loc_2C57DF
```
在```.text:002C578F call    sub_2C10BE```发现了一个可疑函数sub_2C10B，进入函数内部发现了大段字符串操作，并且看见“ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=”字样，由此怀疑是进行Base64加密的函数。


## 加密后的字符串操作

```
.text:002C57B5                 push    eax             ; Str
.text:002C57B6                 call    j_strlen
.text:002C57BB                 add     esp, 4
.text:002C57BE                 mov     [ebp+var_A0], eax
										^ 存放字符串长度
.text:002C57C4                 mov     [ebp+var_AC], 0
										^ 从第0个字符开始
.text:002C57CE                 jmp     short loc_2C57DF
								^ 进入循环
.text:002C57D0 ; ---------------------------------------------------------------------------
.text:002C57D0
.text:002C57D0 loc_2C57D0:                             ; CODE XREF: _main_0+12E↓j
.text:002C57D0                 mov     eax, [ebp+var_AC]
.text:002C57D6                 add     eax, 1
.text:002C57D9                 mov     [ebp+var_AC], eax
.text:002C57DF
.text:002C57DF loc_2C57DF:                             ; CODE XREF: _main_0+EE↑j
.text:002C57DF                 mov     eax, [ebp+var_AC]
.text:002C57E5                 cmp     eax, [ebp+var_A0]
.text:002C57EB                 jge     short loc_2C5810
								^ 索引超出范围则跳出循环
.text:002C57ED                 mov     eax, [ebp+var_AC]
.text:002C57F3                 movsx   ecx, [ebp+eax+Destination]
								^ ecx => Destination[eax]
.text:002C57FB                 add     ecx, [ebp+var_AC]
								^ Destination[eax] += [ebp+var_AC];
.text:002C5801                 mov     edx, [ebp+var_AC]
.text:002C5807                 mov     [ebp+edx+Destination], cl
.text:002C580E                 jmp     short loc_2C57D0
```
此操作即为将所得加密字符串每个字符加上其索引值（也就是修改字符串中每个字符的ASCII）。

## 利用python脚本解密flag
```
import base64

str1 = "e3nifIH9b_C@n@dH"
str2 = ""
i = 0

while i < len(str1):
    a = ord(str1[i])
    a -= i
    str2 += chr(a)
    i += 1

print(base64.b64decode(str2).decode())

```


![image-20210106210713185](C:\Users\zhangsiyu\AppData\Roaming\Typora\typora-user-images\image-20210106210713185.png)



flag： flag{i_l0ve_you}

END