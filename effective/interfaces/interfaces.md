## 接口

## 类型转换

## 接口转换与类型断言

[类型选择](https://go-zh.org/doc/effective_go.html#类型选择)是类型转换的一种形式：它接受一个接口，在选择 （`switch`）中根据其判断选择对应的情况（`case`）， 并在某种意义上将其转换为该种类型。

如果明知道一个确定的值，可以使用类型断言将 value 直接转换为对应类型的值

```go
value.(typeName)
str := value.(string)
```

若不能完全确定该类型，或者说使用更为安全的做法，即使用 逗号,ok 的方式来安全的判断该值类型是否为字符串

```go
str, ok := value.(string)
if ok {
	fmt.Printf("字符串值为 %q\n", str)
} else {
	fmt.Printf("该值非字符串\n")
}
```

若类型断言失败，`str` 将继续存在且为字符串类型，但它将拥有零值，即空字符串。

## 通用性

## 接口和方法

定义一个函数类型 F，并且实现接口 A 的方法，然后在这个方法中调用自己。这是 Go 语言中将其他函数（参数返回值定义与 F 一致）转换为接口 A 的常用技巧。

