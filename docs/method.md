### 1. 概念
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

### 3. 快速案例

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


