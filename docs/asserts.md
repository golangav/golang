### 1.基本介绍

类型断言，由于接口是一般类型，不知道具体类型，如果要转成具体类型，就需要使用类型断言。

### 2. 示例

```
package main

import (
	"fmt"
)

func main()  {
	var x interface{}
	var y float32 = 1.1
	x = y					//空接口可以接收任意类型
	var z = x.(float32)		//因为x -> float32，所以可以成功

	fmt.Printf("z的类型: %T",z)
}

------------------------------
z的类型: float32

```

### 3.断言的案例