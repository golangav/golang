##1. 为什么需要切片
当数组中的元素不确定个数时候使用切片

##2. 切片的基本介绍
1. 切片是一个数组的引用，所以切片是引用类型。
2. 切片的长度是可以变化的。

##3. 切片的创建
1>. 数组创建
```angularjs
var intArr = [5]int{1, 2, 3, 4, 5}
slice := intArr[2:5]
```

2>. make创建

- 通过make创建可以指定大小和容量
- 如果没有指定值会有默认值
```angularjs
package main
import (
	"fmt"
)

func main() {
	var slice []float64 = make([]float64, 5, 10)
	fmt.Println(slice)
}

# go run main.go
    [0 0 0 0 0]
```
3>. 定义一个切片，直接指定具体数组
```angularjs
package main

import "fmt"

func main() {
	var slice []int = []int{1, 2, 3, 4, 5}
	fmt.Println(slice)
}
```

##4. 切片的遍历

1>.for循环遍历
```angularjs
package main

import "fmt"

func main() {
	var intArr = [5]int{1, 2, 3, 4, 5}
	slice := intArr[1:4]
	for i := 0; i < len(slice); i++ {
		fmt.Printf("slice[%v]=%v\n", i, slice[i])
	}
}

----------
slice[0]=2
slice[1]=3
slice[2]=4
```

2>. for range遍历
```angularjs
package main

import "fmt"

func main() {
	var intArr = [5]int{1, 2, 3, 4, 5}
	slice := intArr[1:4]
	for i, v := range slice {
		fmt.Printf("slice[%v]=%v\n", i, v)
	}
}

----------
slice[0]=2
slice[1]=3
slice[2]=4
```
##5. 斐波那契数列

- 函数接收一个数字n，打印斐波那契数列

```angularjs
package main

import "fmt"

func fbn(n int) []uint64 {
	// 声明一个切片，切片大小 n
	fbnslice := make([]uint64, n)
	fbnslice[0] = 1
	fbnslice[1] = 1
	for i := 2; i < n; i++ {
		fbnslice[i] = fbnslice[i-1] + fbnslice[i-2]
	}
	return fbnslice
}

func main() {
	fbnslice := fbn(10)
	fmt.Println(fbnslice)
}

--------------
[1 1 2 3 5 8 13 21 34 55]
```

