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
## 4. 数组的遍历
- for-range
```angularjs
intArr := [...]int{100, 200, 300}
for i, v := range intArr {
    fmt.Println(i, v)
}
```
## 5. 数组的特点
- 数组是多个相同类型数据的组合。
- 其长度是固定的，不能变化。
- 数组中的元素可以是任意数据类型，包括值类型和引用类型，但不能混用。
- 数组在创建后，如果没有赋值则有默认值。
- go的数组是值类型，在默认情况下是值传递，因此会进行值拷贝。
```angularjs
func test01(arr [3]int) {
	arr[0] = 500
}

func main() {
	intArr := [...]int{100, 200, 300}
	test01(intArr)
	fmt.Println(intArr)
}
--------------------
[100 200 300]
```
- go数组也可以是引用传递
```angularjs
func test01(arr *[3]int) {
	(*arr)[0] = 500
}

func main() {
	intArr := [...]int{100, 200, 300}
	test01(&intArr)
	fmt.Println(intArr)
}
--------------------
[500 200 300]
```
## 6. 数组的事例


1>. 随机生成5个数，并将其反转
```angularjs
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main() {
	var intArr [3]int
	rand.Seed(time.Now().UnixNano())
	for i := 0; i < len(intArr); i++ {
		intArr[i] = rand.Intn(100)
	}
	fmt.Println(intArr)

	// 反转打印，交换次数是len(intArr / 2)
	temp := 0 // 做一个临时变量
	for i := 0; i < len(intArr)/2; i++ {
		temp = intArr[len(intArr)-1-i]
		intArr[len(intArr)-1-i] = intArr[i]
		intArr[i] = temp
	}
	fmt.Println(intArr)
}
----------------------
[82 98 38 37]
[37 38 98 82]
```

2>. 求出一个数组的最大值，并打印其下标
```angularjs
package main

import "fmt"

func main() {
	//1. 假定第一个元素就是最大值，下标为0
	//2. 然后从第二个元素循环比较，如果发现更大则交换
	var intArr = [5]int{1, -1, 9, 99, 11}
	maxVal := intArr[0]
	maxValIndex := 0
	for i := 1; i < len(intArr); i++ {
		if intArr[i] > maxVal {
			maxVal = intArr[i]
			maxValIndex = i
		}
	}
	fmt.Printf("maxVal=%v maxValIndex=%v", maxVal, maxValIndex)
}
--------------------
maxVal=99 maxValIndex=3
```







