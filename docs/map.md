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
## 3. map切片
```angularjs
package main

import "fmt"

func main() {
	var monsters []map[string]string
	monsters = make([]map[string]string, 2)

	// 第一个赋值
	monsters[0] = make(map[string]string, 2)
	monsters[0]["name"] = "牛魔王"
	monsters[0]["age"] = "500"

	// 动态增加一个monster
	newMonster := map[string]string{
		"name": "xx",
		"age":  "18",
	}
	monsters = append(monsters, newMonster)
	fmt.Println(monsters)
}
```
## 4. map排序
```angularjs
package main

import (
	"fmt"
	"sort"
)

func main() {
	map1 := make(map[int]int, 10)
	map1[3] = 2
	map1[1] = 3
	map1[2] = 10
	fmt.Println(map1)

	// 先按key排序
	var keys []int
	for k, _ := range map1 {
		keys = append(keys, k)
	}
	sort.Ints(keys)
	fmt.Println(keys)

	// map 排序
	for _, v := range keys {
		fmt.Printf("map1[%v]=%v \n", v, map1[v])
	}
}

-------------------
map[3:2 1:3 2:10]
[1 2 3]
map1[1]=3
map1[2]=10
map1[3]=2
```

## 5. map试用细节

- map是引用类型
- map的容量到达后，再想map增加元素会自动扩容
- map的value也经常使用struct类型，更适合管理复杂的数据












