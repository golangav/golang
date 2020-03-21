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




### 1. 方法
golang中的方法是作用在指定的数据类型上的（即：和指定的数据类型绑定），因此自定义类型都可以有方法，而不仅仅是struct。

### 2. 方法的声明和调用
```
声明：

func (recevier type) methodName(参数列表) (返回值列表){
	方法体
	return 返回值
}

事例：

package main

import (
	"fmt"
)

type Persion struct {
	Name string
}

func (p Persion)test()  {
	fmt.Println( p.Name)
}

func main()  {
	var p Persion
	p.Name = "tom"
	p.test()
}

```

### 3. 方法快速案例

1>. 给Persion结构体增加一个speak方法，输出 xxx是一个好人

```
package main

import (
	"fmt"
)

type Persion struct {
	name string
}

func (persion Persion) test() {
	fmt.Print(persion.name, " is a good man")
}

func main()  {
	var p Persion
	p.name = "tom"
	p.test()
}
```

2>. 给Persion结构体增加一个test方法，计算1+++1000的结果

```
package main

import (
	"fmt"
)

type Persion struct {
	name string
}

func (persion Persion) test() {
	res := 0
	for i :=1; i <= 1000; i++ {
		res +=i
	}

	fmt.Print(persion.name, "计算结果为 ", res)
}

func main()  {
	var p Persion
	p.name = "tom"
	p.test()
}
```
3>. 给Persion结构体增加一个test方法，该方法可以接受一个数n，计算从1++n的结果

```
package main

import (
	"fmt"
)

type Persion struct {
	name string
}

func (persion Persion) test(n int) {
	res := 0
	for i :=1; i <= n; i++ {
		res +=i
	}

	fmt.Print(persion.name, "计算结果为 ", res)
}

func main()  {
	var p Persion
	p.name = "tom"
	p.test(3)
}
```
4>. 给Persion结构体增加一个test方法，可以计算两个数的和，并返回结果

```
package main

import (
	"fmt"
)

type Persion struct {
	name string
}

func (persion Persion) test(x int,y int) int {
		return x + y
}

func main()  {
	var p Persion
	res := p.test(1,2)
	fmt.Println("result=", res)
}
```

### 4. 方法的调用和传参机制原理

说明：方法的调用和传参机制和函数基本一样，不一样的地方是方法调用时，会将调用方法的变量当做实参也传递给方法。


### 5. 方法的练习

1>. 编写结构体(MethodUtils)，编写一个方法，方法不需要参数，在方法中打印一个10*8的矩形，在main方法中调用该方法。

```
package main

import (
	"fmt"
)

type MethodUtils struct {

}

func (mu *MethodUtils) print() {
	for i := 1; i <= 10; i++{
		for j := 1; j <= 8; j++ {
			fmt.Print("*")
		}
		fmt.Println()
	}
}

func main()  {
	var mu = MethodUtils{}
	mu.print()

}

--------------------------

********
********
********
********
********
********
********
********
********
********

```

2>. 编写一个方法，提供m和n两个参数，方法中打印一个m*n的矩形

```

package main

import (
	"fmt"
)

type MethodUtils struct {

}

func (mu *MethodUtils) print(m int, n int) {
	for i := 1; i <= m; i++{
		for j := 1; j <= n; j++ {
			fmt.Print("*")
		}
		fmt.Println()
	}
}

func main()  {
	var mu = MethodUtils{}
	mu.print(2,6)

}

--------------------------

******
******

```
3>. 编写一个方法算该矩形的面积(可以接收长len，宽width)，将其作为方法的返回值。在main方法中调用该方法，接收返回的面积值并打印。

```
package main

import (
	"fmt"
)

type MethodUtils struct {
	len int
	width int
}

func (mu *MethodUtils) area(len int, width int) (int) {
	return len * width
}

func main()  {
	var mu MethodUtils

	res := mu.area(2,6)
	fmt.Print("矩形面积：",res)

}

--------------------------

矩形面积：12

```
4>. 编写方法：判断一个数是奇数还是偶数

```
package main

import (
	"fmt"
)

type MethodUtils struct {
	len int
	width int
}

func (mu *MethodUtils) judgeNum(num int) {
	if num % 2 == 0{
		fmt.Print(num,"是偶数")
	}else {
		fmt.Print(num,"是奇数")
	}
}

func main()  {
	var mu MethodUtils

	mu.judgeNum(6)

}

--------------------------

6是偶数

```

