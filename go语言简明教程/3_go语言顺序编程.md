# Go语言顺序编程

## 流程控制

Go 语言提供的流程控制语句包括 `if`、`switch`、`for`、`goto`、`select`

#### if 语句

语法：

```go
if optionalStatement1; booleanExpression1 {
    block1
} else if optionalStatement2; booleanExpression2 {
    block2
} else {
    block3
}
```

其中 `optionalStatement` 是可选的表达式，真正决定分支走向的是 `booleanExpression1` 的值。

#### for 语句

Go 语言的 `for` 语句可以遍历数组，切片，映射等类型，也可以用于无限循环。以下是其语法：

```go
for { // 无限循环
    block
}

for booleanExpression { // while循环，在Go语言中没有while关键字

}

for index, char := range aString { // 迭代字符串

}

for item := range aChannel { // 迭代通道

}
```

#### 跳转语句 goto

Go 语言中使用 `goto` 关键字实现跳转。`goto` 语句的语义非常简单，就是跳转到本函数内的某个标签，例如：

```go
func myfunc(){
    i := 0
    THIS: //定义一个THIS标签
    fmt.Println(i)
    i++
    if i < 1 {
        goto THIS //跳转到THIS标签
    }
}
```

### switch

- Go 语言的 `switch` 语句不会自动贯穿，相反，如果想要贯穿需要添加 `fallthrough` 语句
-  没有表达式，默认为True值，匹配分支中值为

```go
switch optionalStatement; optionalExpression {
    case expression1: block1
    ...
    case expressionN: blockN
    default: blockD
}
```

类型断言

```go
switch optionalStatement; typeSwitchGuard {
    case type1: block1
    ...
    case typeN: blockN
    default: blockD
}
```

go

```go
switch {        // 没有表达式，默认为True值，匹配分支中值为True的分支
    case value < minimum:
        return minimum
    case value > maximum:
        return maximum
    default:
        return value
}
```

示例

```go
package main

import (
	"fmt"
)

// classchecker 类型检测
// 创建函数，该函数可以接受任意多的任意类型的参数
func classchecker(items ...interface{}){
	for i, x := range items{ // 创建影子变量
		switch x := x.(type){
		case bool:
			fmt.Printf("param #%d is a bool, value %t\n", i, x)
		case float64:
			fmt.Printf("param #%d is a float64, value %f\n", i, x)
		case int, int8, int16, int32, int64:
			fmt.Printf("param #%d is a int, value %d\n", i, x)
		case uint, uint8, uint16, uint32, uint64:
			fmt.Printf("param #%d is a uint, value %d\n", i, x)
		case nil:
			fmt.Printf("param #%d is a nil\n", i)
		case string:
			fmt.Printf("param #%d is a string, value %s\n", i, x)
		default:
			fmt.Printf("param #%d's type is unknown\n", i)
		}
		
	}
}
func main(){
	classchecker(5, -17.98, "AIDEN", nil, true, complex(1,1))
}
```

## 函数

### 特殊的函数：main函数

- `main` 函数必须出现在 `main` 包里，且只能出现一次。
- 当 Go 程序运行时候会自动调用 `main` 函数开始整个程序的执行。
- `main` 函数不可接收任何参数，也不返回任何结果。

### 其他：创建目录

>  GO会自动到GOPATH下自动寻找模块，所以必须配置GOPATH

```shell
# linux下添加到环境配置文件

# 查看当前用户
pwd

# 查看当前用户的工作目录的环境配置文件,一般是
ls home/<user>/.zshrc

cd home/<user>/

# 添加以下变量到环境
echo "export GOROOT=/usr/local/go" >>.zshrc       #Golang安装目录
echo "export PATH=$GOROOT/bin:$PATH" >> .zshrc
echo "export GOPATH=/home/go" >> .zshrc  #自己的Golang项目目录

# 让配置文件生效
source .zshrc

#关闭GOMODULE
go env -w GO111MODULE=off
```



## 类型转换

## 类型断言

## error

## defer

## panic

