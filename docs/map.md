## 1. map介绍
map是key-value数据结构，又称为字段或者关联数组，类似其它编程语言中字典。

注意：声明是不会分配内存的，初始化需要make，分配内存后才能赋值和试用。

```angularjs
package main

import "fmt"

func main() {
	var a map[string]string
	a = make(map[string]string, 10)
	a["name"] = "Tom"
	fmt.Print(a)
}

-------------
map[name:Tom]
```

## 2. map的使用方式

1>. 先声明再make
```angularjs
var a map[string]string
a = make(map[string]string, 10)
a["name"] = "Tom"
```
2>. 不用声明大小
```angularjs
a := make(map[string]string)
a["name"] = "tom"
a["sex"] = "男"
```
3>. 声明并赋值
```angularjs
obj := map[string]int{
	"水笔": 18,
	"铅笔": 20,
}
```