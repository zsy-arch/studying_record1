# (Write up) hello_world_go

## Step 1. IDA打开

![](C:\Users\zhangsiyu\Pictures\屏幕截图 2021-01-03 231053.png)

此文件为ELF64格式,初步怀疑是在Linux平台上的go语言程序(因为名字里有go)

## Step 2. 找到程序入口(main函数)

![屏幕截图 2021-01-03 231410](C:\Users\zhangsiyu\Pictures\屏幕截图 2021-01-03 231410.png)

程序入口为main_main函数, 右键切换到Graph View

## Step 3. 寻找程序主体

## ![](C:\Users\zhangsiyu\Pictures\屏幕截图 2021-01-03 232229.png)

画箭头处为程序主体开始的地方,虚线右侧可以先不用管.

## Step 4. 寻找字符串

![](C:\Users\zhangsiyu\Pictures\屏幕截图 2021-01-03 232617.png)

双击这些以 **unk_** 开头的地方, 挨个寻找.

![](C:\Users\zhangsiyu\Pictures\屏幕截图 2021-01-03 232935.png)

这里便是flag: flag{hello world gogogo}