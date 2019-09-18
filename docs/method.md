### 1. 概念
golang中的方法是作用在指定的数据类型上的（即：和指定的数据类型绑定），因此自定义类型都可以有方法，而不仅仅是struct。

### 2. 方法的声明和调用
```
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



案例一：给Person结构体增加speak方法，输出 xxx是一个好人

package main

import (
	"fmt"
)

type Persion struct {
	Name string
}

func (p Persion)speak()  {
	fmt.Println(p.Name,"是一个好人")
}

func main()  {
	var p Persion
	p.Name = "tom"
	p.speak()
}

--------------------
tom 是一个好人

```
### 3. 变量使用的注意事项