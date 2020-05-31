```go
//Return two variables
package main

import "fmt"

func swap(x ,y string)(string,string)  {
	return y,x
}

func main() {
	a,b := swap("hello","world")
    fmt.Println(a,b)
}
```
```go
//Naked Return

package main

import "fmt"

func split(sum int)(x,y int)  {
	x= sum *4/9
	y=sum - x
	return	//known as naked return, not good for using in long functions
}

func main() {
	fmt.Println(split(17))
}
```

```go
// var can be used as packages or in functions
package main

import "fmt"

var c, python, java bool

func main() {
	var i int
	fmt.Println(i, c, python, java)
}

```

```go
// if a initializer is present , type can be omitted
package main

import "fmt"

var i, j int = 2, 4

func main() {
	var c, python, java = true, false, "no!"
	fmt.Println(i, j, c, python, java)
}

```
```go
// the := the short assignment statement can be used in place of var, inside a function only
package main

import "fmt"

func main() {
	var i, j int = 1, 2
	k := 3
	c, python, java := true, false, "no!"
	fmt.Println(i, j, k, c, python, java)
}

```
```go
//go basic types
package main

import (
	"fmt"
	"math/cmplx"
)

var (
	ToBe   bool       = false
	MaxInt uint64     = 1<<64 - 1
	Z complex128 = cmplx.Sqrt(-5 + 12i)
)

func main() {
	fmt.Printf("Type: %T Value: %v\n", ToBe, ToBe)
	fmt.Printf("Type: %T Value: %v\n", MaxInt, MaxInt)
	fmt.Printf("Type: %T Value: %v\n", Z, Z)
}

```

```go
// variables without and explicit value initialized are given their zero value 
package main

import "fmt"

func main() {
	var i int
	var f float64
	var b bool
	var s string
	fmt.Printf("%v %v %v %q\n", i, f, b, s)
}

```

```go
//Expression T(v) change the type of v
package main

import (
	"fmt"
	"math"
)

func main() {
	var x, y int = 3, 4
	var f float64 = math.Sqrt(float64(x*x + y*y))
	var z uint = uint(f)
	fmt.Println(x, y, z)
}

```

```go
//when declaring a variable without a specific type the default right side will be considered
package main

import (
	"fmt"
)

func main() {
	v := 2546546546464
	fmt.Printf("v is of type %T\n", v)
}

```

```go
// const can be declared as var but with const keyword
package main

import "fmt"

const Pi = 3.14

func main() {
	const word = "fwefwe"
	fmt.Println("Hello", word)
	fmt.Println("Happy", Pi, "Day")

	const Truth = true
	fmt.Println("Go Rules?", Truth)
}

```
```go
//for loop
package main

import "fmt"

func main() {
	sum := 0
	for i:=0; i<100;i++ {
		sum += i
	}
	fmt.Println(sum)
}
// init and post statements are optional

func main() {
	sum := 1
	for ; sum<1000; {
		sum += sum
	}
	fmt.Println(sum)
}
// can remove the semicolon as well, for is Go's while
func main() {
	sum := 1
	for sum < 1000{
		sum += sum
	}
	fmt.Println(sum)
}
```
```go
//if loop
package main

import (
	"fmt"
	"math"
)

func sqrt(x float64) string {
	if x < 0 {
		return sqrt(-x) + "i"
	}
	return fmt.Sprint(math.Sqrt(x))
}

func main() {
	fmt.Println(sqrt(2), sqrt(-4))
}
```
```go
//if with a short statement
package main

import (
	"fmt"
	"math"
)
//if
func pow(x, n, lim float64) float64 {
	if v := math.Pow(x, n); v < lim {
		return v
	}
	return lim
}
//if-else
func pow(x, n, lim float64) float64 {
	if v := math.Pow(x, n); v < lim {
		return v
	} else {
		fmt.Printf("%g >= %g\n", v, lim)
	}
	return lim
}

func main() {
	fmt.Println(
		pow(3, 2, 10),
		pow(3, 3, 20),
	)
}

```
```go
// implementation
package main

import (
	"fmt"
)

func Sqrt(x float64) float64 {
	z := float64(1)
	fmt.Printf("Sqrt approximation of %v:\n",x)
	for i:=1;i<=10;i++ {
		z -= (z*z -x)/(2*z)
		fmt.Printf("Iteration %v,value = %v\n",i,z)
	}
	return z
}

func main() {
	fmt.Println(Sqrt(2))
}
```
```go
//switch
package main

import (
	"fmt"
	"runtime"
    "time"
)

func main()  {
	switch os:= runtime.GOOS; os {

	case "darwin":
		fmt.Println("OS x.")
	case "linux":
		fmt.Println("Linux")
	default:
		fmt.Printf("%s.\n",os)
	}
}

func main() {
	today := time.Now().Weekday()
	switch time.Sunday {

	case today + 0:
		fmt.Println("Today")
	case today + 1:
		fmt.Println("Tomorrow")
	case today + 2:
		fmt.Println("In two days")
	default:
		fmt.Println("Too far away")
	}
}
// switch with no condition, same as switch true
func main() {
	t := time.Now()
	switch  {
	case t.Hour()<12:
		fmt.Println("Good morning")
	case t.Hour()<17:
		fmt.Println("Good afternoon")
	default:
		fmt.Println("Good evening")
	}
}
```
```go
// defer statement defers the execution until surrounding function returns
package main

import (
	"fmt"
)

func main() {
	defer fmt.Println("World")
	fmt.Println("Hello")
}

//Deferred function calls are pushed onto a stack. When a function returns, its deferred calls are executed in last-in-first-out order.
func main() {

	fmt.Println("counting")
	for i:=0;i<10;i++ {
		defer fmt.Println(i)
	}
	fmt.Println("done")
}

```