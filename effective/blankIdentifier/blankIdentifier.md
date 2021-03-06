空白标识符可被赋予或者申明为任何类型的任何值，而这些值将会被无害的丢弃。

## 多重赋值中的空白标识符

若某次赋值需要匹配多个左值，但其中某个变量不会被程序使用， 那么用空白标识符来代替该变量可避免创建无用的变量，并能清楚地表明该值将被丢弃。

```go
if _, err := os.Stat(path); os.IsNotExist(err) {
	fmt.Printf("%s does not exist\n", path)
}
```

## 未使用的导入和变量

若导入某个包或声明某个变量而不使用它就会产生错误。未使用的包会让程序膨胀并拖慢编译速度， 而已初始化但未使用的变量不仅会浪费计算能力，还有可能暗藏着更大的Bug。 然而在程序开发过程中，经常会产生未使用的导入和变量。虽然以后会用到它们， 但为了完成编译又不得不删除它们才行，这很让人烦恼。空白标识符就能提供一个工作空间。

```go
package main

import (
    "fmt"
    "io"
    "log"
    "os"
)

var _ = fmt.Printf // For debugging; delete when done. // 用于调试，结束时删除。
var _ io.Reader    // For debugging; delete when done. // 用于调试，结束时删除。

func main() {
    fd, err := os.Open("test.go")
    if err != nil {
        log.Fatal(err)
    }
    // TODO: use fd.
    _ = fd
}
```

## 为副作用而导入

有些时候为了执行某个包的init方法，可以使用空白标识符引入，而不做其他操作

## 接口检查

一个类型无需显式的声明它实现了某个接口，取而代之，若类型只要实现了某个接口的方法，就认为实现了该接口。

若只需要判断某个类型是否是实现了某个接口，而不需要实际使用接口本身 （可能是错误检查部分），就使用空白标识符来忽略类型断言的值：

```go
if _, ok := val.(json.Marshaler); ok {
	fmt.Printf("value %v of type %T implements json.Marshaler\n", val, val)
}
```

若需要强制实现某个接口，若没实现在编译期就报错。

```go
var _ json.Marshaler = (*RawMessage)(nil)
```

在此声明中，我们调用了一个 `*RawMessage` 转换并将其赋予了 `Marshaler`，以此来要求 `*RawMessage` 实现 `Marshaler`，这时其属性就会在编译时被检测。 若 `json.Marshaler` 接口被更改，此包将无法通过编译， 而我们则会注意到它需要更新。

在这种结构中出现空白标识符，即表示该声明的存在只是为了类型检查。 不过请不要为满足接口就将它用于任何类型。作为约定， 仅当代码中不存在静态类型转换时才能这种声明，毕竟这是种罕见的情况