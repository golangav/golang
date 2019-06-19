##1. 结构体和结构体变量（实例）的区别
- 结构体是自定义的数据类型，结构体是值类型。
- 结构体变量(实例)实具体的，实际的，代表一个具体变量。

##2. 创建结构体变量和访问结构体字段
1>.直接创建 var p1 Persion
```angularjs

package main

import (
	"fmt"
)

type Persion struct {
	Name string
	Age  int
}

func main() {
	var p1 Persion

	p1.Name = "mimi"
	p1.Age = 18
	fmt.Println(p1)

}


```
2>.{} var p1 = Persion{}
```angularjs
package main

import (
	"fmt"
)

type Persion struct {
	Name string
	Age  int
}

func main() {
	var p1 = Persion{"mimi", 18}
	fmt.Println(p1)
}
```
3>.&  返回结构体指针
```angularjs
package main

type Persion struct {
	Name string
	Age  int
}

func main() {
	var p1 *Persion = new(Persion)
	(*p1).Name = "mimi" //因为p1是指针类型 标准写法
	p1.Name = "xx"      // 简写
}

```
4>.{}  返回结构体指针
```angularjs
package main

type Persion struct {
	Name string
	Age  int
}

func main() {
	var p1 *Persion = &Persion{}
	(*p1).Name = "mimi" //标准写法
	p1.Name = "xx"      // 简写
}

```

##3. 声明结构体
```angularjs
package main

import (
	"fmt"
	"sort"
)

type Cat struct {
	Name string
	Age int
	Color string
}

func main() {
	var cat1 Cat
	cat1.Name = "mimi"
	cat1.Age = 18
	cat1.Color = "yellow"
}
```
##4. 创建结构体注意事项：

1>. slice，指针，map 需要先make
```angularjs
package main

import (
	"fmt"
)

// 如果结构体的字段类型是：slice，指针，map的零值都是nul，即还没有分配空间
// 如果需要试用这样的字段，需要先make才能试用

type Persion struct {
	Name   string
	Age    int
	Scores [5]float64
	ptr    *int              //指针
	slice  []int             //切片
	map1   map[string]string //map
}

func main() {
	var p1 Persion

	// 使用slice  先make
	p1.slice = make([]int, 10)
	p1.slice[0] = 100

	// 使用map  先make
	p1.map1 = make(map[string]string)
	p1.map1["key1"] = "tom"

	fmt.Println(p1)

}

--------------------
{ 0 [0 0 0 0 0] <nil> [100 0 0 0 0 0 0 0 0 0] map[key1:tom]}
```
##5. 结构体的使用细节和注意事项
1>. 结构体的字段在内存中都是连续的
