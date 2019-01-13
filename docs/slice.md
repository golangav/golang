## 为什么需要切片
当数组中的元素不确定个数时候使用切片

## 切片的基本介绍
1. 切片是一个数组的引用，所以切片是引用类型。
2. 切片的长度是可以变化的。

## 切片的使用
1. make创建
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
2. 定义一个切片，直接指定具体数组
```angularjs

```