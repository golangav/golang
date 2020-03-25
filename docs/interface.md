## 1. 接口的概念





## 2. 接口的注意事项

1>. 接口本省不能创建实例，但可以指向一个实现了该接口的自定义类型的变量。
```
package main

import "fmt"

// 声明一个usb 接口类型
type Usb interface {
	start()
}

type Phone struct {

}

func (p Phone) start()  {
	fmt.Println("手机开始工作")
}


func main()  {
	var phone Phone
	var u Usb = phone   // 接口指向了一个实现了Usb接口类型的变量
	u.start()
}
```
2>.接口中所有的方法都没有方法体，即都是没有实现的方法。

3>.一个自定义类型需要将接口中所有的方法都实现，我们说该自定义类型实现了该接口。

4>.只要是自定义数据类型都可以实现接口，而不仅仅是结构体。

5>.一个自定义类型可以实现多个接口。
```
package main

import "fmt"


type A interface {      // 接口A
	start()
}

type B interface {      // 接口B
	stop()
}

type C struct {         // struct C 实现接口A 和 接口B

}

func (c C) start()  {
	fmt.Println("手机开始工作")
}

func (c C) stop()  {
	fmt.Println("手机停止工作")
}


func main()  {
	var c C
	var a A = c
	var b B = c
	a.start()
	b.stop()
}
```
6>.golang接口中不能有各种变量。

7>.接口中可以继承。
```
package main

import "fmt"


type A interface {
	test01()
}

type B interface {
	test02()
}

type C interface {
	A
	B
	test03()
}

type Student struct {

}

func (stu Student) test01()  {
	fmt.Println("test01")
}

func (stu Student) test02()  {
	fmt.Println("test02")
}

func (stu Student) test03()  {
	fmt.Println("test03")
}


func main() {
	var stu Student
	var c C = stu    // C继承A和B, 所以有A，B，C的方法
	c.test01()
	c.test02()
	c.test03()

	var b B = stu
	b.test02()

	var a A = stu
	a.test01()
}
```

8>.interface默认是一个指针(引用类型)，如果没有初始化，就为nil

9>.空接口没有interface{}没有任何方法，所以所有类型都实现了空接口。所以可以指向任何类型的变量。


## 3. 对 struct切片 排序

>1. 开放一些接口给开发者用，然后核心的由内部去实现。

```
package main

import (
	"fmt"
	"math/rand"
	"sort"
)

// 声明 Hero 结构体
type Hero struct {
	name string
	age int
}

// 声明 HeroSlice 结构体切片
type HeroSlice []Hero

// 实现sort.sort(data interface) 的三个方法
func (hs HeroSlice) Len() int {
	return len(hs)
}

func (hs HeroSlice) Less(i, j int) bool {
	if hs[i].age < hs[j].age {
		return true
	}
	return false
}

func (hs HeroSlice) Swap(i, j int) {
	hs[i],hs[j] = hs[j],hs[i]
}



func main()  {

	// 组装 HeroSlice 数据
	var heros HeroSlice

	for i :=0; i<=10; i++ {
		hero := Hero {
			name: fmt.Sprintf("zero%d",rand.Intn(100)),
			age:rand.Intn(100),
		}
		heros = append(heros,hero)
	}

	// 打印排序前的数据
	for _,v := range heros{
		fmt.Println(v.name,v.age)
	}

	sort.Sort(heros)

	fmt.Println("----------排序后----------")

	// 打印排序后的数据
	for _,v := range heros{
		fmt.Println(v.name,v.age)
	}

}

--------------------结果--------------------
zero81 87
zero47 59
zero81 18
zero25 40
zero56 0
zero94 11
zero62 89
zero28 74
zero11 45
zero37 6
zero95 66
----------排序后----------
zero56 0
zero37 6
zero94 11
zero81 18
zero25 40
zero11 45
zero47 59
zero95 66
zero28 74
zero81 87
zero62 89

```

## 4. 接口体现多态的两种形式:

>1. Usb接口案例，usb Usb即可以接收手机变量，又可以接收相机变量，就体现了接口多态。

```
package main

import (
	"fmt"
)

type Usb interface {
	start()
}

type Phone struct {

}

func (p Phone) start()  {
	fmt.Println("手机开始工作")
}

type Camera struct {

}

func (c Camera) start() {
	fmt.Println("相机开始工作")
}

type Computer struct {

}

func (c Computer) Working(usb Usb)  {  // usb变量会根据传入的实参，来判断是Phone还是Camera
	usb.start()
}


func main()  {
	computer := Computer{}
	phone := Phone{}
	camera := Camera{}

	computer.Working(phone)
	computer.Working(camera)
}
```
2>.数组中只可以存放一种数据类型，接口数据类型即可以存放phone结构体又可以存放camera结构体。

```
package main

import (
	"fmt"
)

type Usb interface {
	start()
}

type Phone struct {

}

func (p Phone) start()  {
	fmt.Println("手机开始工作")
}

type Camera struct {

}

func (c Camera) start() {
	fmt.Println("相机开始工作")
}

func main()  {
	var usbArr [3]Usb   // 此时数组可以接收实现了usb接口的类型

	phone := Phone{}
	camera := Camera{}

	usbArr[0] = phone
	usbArr[1] = camera
	fmt.Println(usbArr)
}


-------------------------------------------
[{} {} <nil>]
```