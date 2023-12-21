---
layout: post
title: Swift 常见语法错误
date: 2022-01-30
tags:
  - lang/swift
---

# Swift 常见语法错误

- 无效的重复声明

```swift
let (_, errMsg) = httpError
...
let (_, errMsg) = httpError

/**
Error:
Invalid redeclaration of ‘errMsg‘
*/
```

- 强制类型

```swift
var notFountError = (404, "Not Found Error")
notFountError = (404, "Server Side", "Not Fount Error", "Http Error")

/**
Error:
Cannot assign value of type ‘(Int, String, String, String)’ to type
*/
```

- 类型推导 & 可选类型

```swift
var catchphrase: String?
catchphrase = "Hey guys, what's up"

let count1: Int = catchphrase.count

/**
Error:
Value of optional type 'String?' must be unwrapped to refer to member 'count' of wrapped base type 'String'
*/

// Fixed:
let count1: Int? = catchphrase?.count
or
var count1 =. catchphrase?.count
```

- 语法错误，for-in 语句

```swift
for index 1...5 {
  // ...
}

/**
Error:
Expected 'in' after for-each pattern
*/

// Fixed:
for index in 1...5 {
  // ...
}
```

- immutable collection 不可变

```swift
let immutableArray: [String] = ["a1", "a2"]
immutableArray.insert("bb", at: 2)

/**
Error:
Cannot use mutating member on immutable value: 'immutableArray' is a 'let' constant
*/
```

- 类型推导 & 可选类型

```swift
var mutatingDic = ["name": "yuntianming", "age": "29"]
var yAge: String = mutatingDic["age"]

/**
Error:
Value of optional type 'String?' must be unwrapped to a value of type 'String'
*/
```

- 方法只有在单执行语句时，才不需要 `return` 关键字

```swift
func multipyExp(x: Int,y: Int) -> Int {
    print("x \(x)")
    print("y \(y)")
    x + y
}
multipyExp(x: 11, y: 99)

/**
Error:
Missing return in a function expected to return 'Int'; did you mean to return the last expression?
*/
```

- 函数参数位置问题

```swift
func addx1(x :Int,y :Int) -> Int {
    x*10 + y
}
addx(y: 1, x: 6)

/**
Error:
Argument 'x' must precede argument 'y'
*/
```

- Final Class 不可被继承

```
final class Child: Person {}

class Children: Child{
    override var isHappy: Bool{
        return false
    }
}

/**
Error:
Inheritance from a final class 'Child'
*/
```

- 构造器参数标注丢失

```swift
class ios: ModeOfTransportation {
    let wheels: Int
    init(name: String, wheels: Int) {
        self.wheels = wheels
        super.init(name: name)
    }

    override convenience init(name: String) {
        self.init(name: name, wheels: 4)
    }
}

let lang = ModeOfTransportation("python")
print(lang.name)

/**
Error:
Missing argument label 'name:' in call
*/
```

- 空集合字面量生成时，明确类型

```swift
let array = []

Error:
empty collection literal requires an explicit type

Fixed:
let array: [Int] = []
var arrayStr: [String] = []
```

- Let 定义常量不可变

```swift
let age = 10
age = 9

Error:
cannot assign to value: 'age' is a 'let' constant
```
