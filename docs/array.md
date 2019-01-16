## 1. 数组介绍
数组可以存放多个同一类型数据，数组也是一种数据类型，在go中数组是值类型。

当定义好数组后数组会有默认值。

## 2. 数组定义
- var intArr [3]int
- var intArr [3]int = [3]int{1, 2, 3}
- var intArr = [3]int{1, 2, 3}
- var intArr = [...]int{1, 2, 3}
- var intArr = [...]int{0: 100, 1: 200, 2: 300}  # 指定下标赋值


## 3. 数组的内存地址
- 数组的地址可以通过数组名获取    &数组
- 数组的第一个元素的地址，就是数组的地址
```angularjs
var intArr [3]int
fmt.Printf("intArr地址=%p", &intArr)
fmt.Printf("intArr[0]地址=%p", &intArr[0])

-------------
intArr地址=0xc000078020
intArr[0]地址=0xc000078020
```
- 数组的各个元素的地址间隔是依据数组的类型决定，比如 int64->8 int32->4
```angularjs
第二个元素的地址就是第一个元素的地址加上元素所占用的内存
var intArr [3]int      # 整数占8个字节
fmt.Printf("intArr[0]地址=%p", &intArr[0])
fmt.Printf("intArr[1]地址=%p", &intArr[1])
--------------
intArr[0]地址=0xc00007a020
intArr[1]地址=0xc00007a028

```
145
