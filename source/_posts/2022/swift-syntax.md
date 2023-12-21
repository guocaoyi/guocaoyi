---
layout: post
title: 《Swift 核心技术与实现》— 01.语言基础
date: 2022-01-15
tags:
  - lang/swift
---

# 《Swift 核心技术与实现》— 01.语言基础

## Reference

- 第一章：Swift简介
- 第二章：基本数据类型
- 第三章：运算符
- 第四章：流程控制

## 第一章：Swift简介

### 历史版本 & 新增特性

Swift2

- Error handing \ guard 语法 \ 协议支持扩展

Swift3

- 新的 GCD 、 Core Graphics
- NS 从老的 Foundation 类型去除
- sequence
- 权限控制 fileprivate \ open （open > public > fileprivate > private）
- 废弃（++ 、- -）

Swift4

- extension 访问 private
- 类型和协议组合类型（and 运算符）
- Associated Type 可以追加 Where 约束语句
- Key Paths
- 下标支持泛型
- 字符串增强

Swift5

- 新增关键字 some
- ABI 稳定
- Raw strings
- Result
- 定义 Python 或 Ruby 等脚本语言互操作

### Swift vs Objective-C

1. 编程范式
   1. Swift 可以面向协议、面向对象、函数式编程
   2. Objective-C 面向对象为主；
2. 类型安全
   1. Swift 类型安全，编译期做检查；OC 则不然
3. 值的类型增强
   1. Swift struct ( Int\Double\Float\String\Array\Dictionary\Set) \ enum \ tuple 都是值类型
   2. NSString\NSNumber 指针类型（引用类型）
4. 枚举增强
   1. Swift 枚举支持：整型、浮点、字符串；拥有属性、方法、泛型、扩展
5. 泛型
   1. OC 的泛型仅在编译期
6. 协议和扩展
7. 函数和闭包
   1. Swift 一等公民
   2. OC 下函数次等公民；需要 Selector 封装；或者 block

### 编译 & SwiftC

C -> Clang -> LLVM IP -> LLVM compiler (x86 \ ARM …)
Swift -> Parse -> (AST) -> Sema -> SILGen -> (SIL) -> Analysis -> IRGen -> (IR) -> LLVM -> (\*.o)

```bash
swiftc -o *.out *.swift # 可执行文件
swiftc *.swift -dump-ast # 生成 Swift AST
swiftc *.swift -emit-sil # 生成 SIL Swift IL
swiftc *.swift -emit-ir # 生成 LLVM IR 中间语言
```

### REPL 交互式解释器

`$R*` 是对应行的返回值
`:quit` 退出
`:help` 帮助

### Playground

## 第二章：基本数据类型

### 变量和常量的定义

Syntax

```swift
let a = 10 // 常量
var a = 10, b = 100; // 变量

var s:String = ""

var 契丹 = "古中国人"
var 🐱 = "cat"
print("契丹 是\(契丹), 不养\(🐱)")

let x = 0.0, y = 0.2, z = 0.1
let x1 = 0.0, y1 = 0.2, z1 = ""
```

### 数值类型

- 数字

Swift 提供 8、16、32、64 有符号（Int32）和无符号（UInt8）类型
Int 类型与当前平台原生字相同长度
.min & .max 访问最小和最大值

- 浮点数

Double 64位浮点数，15位数字的精度；推荐
Float 32位浮点数，6位数字的精度

- Bool

Swift 类安全机制会阻止用非布尔类型 替换 Bool

```swift
let i = 0
if i { } // error
if i == 1 { } // success
```

- 类型别名：更具有业务意义

```swift
typealias AudioSample = UInt8
let sample: AudioSample = 21
```

### Tuple

```swift
let error = (1, "error msg")
let error:(Int, String) = (errorCode: 1, errorMsg: "error msg")
func witeTo(num1: Int) -> (erroCode: Int, errorMsg: String) {
    return (num1, "errrorxxx")
}
let (_, errorMsg) = witeTo(num1: 1)

func witeTo(num1: Int) -> (Int, String) {
    return (num1, "errrorxxx")
}
let result = witeTo(num1: 1)
print(result.1)
let (_, msg) = witeTo(num1: 1)
```

简单实用；不必要使用类

### Optional 类型&原理

ObjC

- ObjC 里的 nil 是无类型的指针，不存在的指针；
- ObjC 里的数组、字典、集合不允许 nil
- ObjC 所有对象变量都可以为 nil
- ObjC 只能用在对象上；NSNotFound 表示值的缺失

Swift

- nil 不指针，是 缺失的一种特殊类型
- 任何类型可选项都可以设置为 nil

Optional-If 语句

- 不可以直接使用
- `!` 展开才能使用

Unwrapped 展开方式

```swift
// 判断展开、强制展开、隐式展开、可选链

var catchPhrase: String?
catchPhrase = "optional string"

// 强制展开 Forced binding
let op = catchPhrase!.count

// 判断展开 Optional binding
if let actualStr = cachePhrase {
    let count = actualStr.count
}

// 隐式展开
var str: String! = "xxx"
let count = str.count

// 可选链 Chaining operator
var str: String? = "abc"
let count = str?.count // count 仍然为 optinal 类型
let count = str?.count ?? 0 // Coalescing operator

```

Optional 其实是标准库里的一个 enum 类型；是用标准库实现语言特性的典型

```swift
public enum Optional<Wrapped> : ExpressibleByNilLiteral {
	case none
	case some
	public init(_ soome: Wrapped)
	@inliable public var unsafelyUnwrapped: Wrapped { get }
}

// Optional.none  = nil
// Optional.some = wrapped
```

### String

```swift
let str = "some string" // 字面量
let multipLineStr = """
The white rabbit on his\
Begin at th
""" // 多行字面量

// 结尾 \ 不会将 \n 计入多行字符串
let nums = """
1\
2\
"""

// unicode
let blackHeart = "\u{2665}"
```

扩展字符串分隔符 Row String

```swift
let str = #"1\n2\n"#
// 1\n2\n

let str = #"1\#n2\n"#
// 1
// 2\n

let str = #"1"\n2\n"#
// 1"\n2\n

let str = #"1"\#n2\n"#
// 1"
// 2\n

let str = ##"1"\#n2\n"##
// 1"\#n2\n

let str = ##"1\##n2\##n"##
// 1
// 2
```

### String 的常见操作

ObjC （NSString, NSMutableString）
Swift 编译器优化了字符串使用的资源，实际上拷贝只会在确定需要的时候才会进行

操作字符

```swift
//
for character in "Dog" { }
// Character array
let catCharacters: [Character] =["C", "a", "t"]
let str = String(["S", "t", "r"])

// 拼接
str.append("xxxxx") // eq. + , +=

// 插值 类似 NSString.stringWithFormat
let msg = "\(str)"

// row string insert
print(#"\(6+7)"#) // \(6+7)
print(#"\#(6+7)"#) // 13
```

### 索引访问和修改字符串

每一个 String 值都有相关的索引类型；相当于 Character 在字符串中的位置

```swift
// a position of a character or code unit in a string
public struct Index {}
```

字符串索引

```swift
var title = "development"
title[title.startIndex] // d
title[1] // [error]
title[title.endIndex] // [error]
title[title.index(title.endIndex, offsetBy: -1)] // t
"title"["title".startIndex] // d

title.index(after: title.startIndex)
let index = title.index(title.startIndex, offsetBy: 2)
title[index] // v
```

插入
移除字符：`remove(at:)`、移除范围：`removeSubrange(_:)`

```swift
title.insert("!", at: title.endIndex) // development!
title.remove(at: title.index(before: title.endIndex)) // !

let range = title.index(title.endIndex, offsetBy: -4)..<title.endIndex
title.removeSubrange(range) // develop
```

### 获取字符串&字符串比较

下标或者 prefix(:\_) 获取 Substring 类型；Substring 拥有 String 大部分方法，并可以转成 String 类型
子字符串：

- Substring 可以重用一部分内存；不需要花费拷贝内存的代价
- String 和 Substring 遵循 StringProtocol 协议

```swift
let slogen = "Hello, swift!"
let index = slogen.index(of: ",") ?? slogen.endIndex
String(slogen[..<index]) // hello
```

比较

```swift
var welcome = "hello, world!"
welcome == "hello" // false
slogen.hasPrefix("He") // true
slogen.hasSuffix("swi") // false
```

## 第三章：运算符

### 赋值和算数运算符

```swift
!b b!
a + b
a ? b : c

let b = 1 // 没有返回值；防止用于 == 意图
+ - * / % // 可以检测并阻止溢出

a % b == a % -b // - 会忽略
```

### 处理算术结果溢出

```swift
&+ // 溢出加法
&- // 溢出减法
&* // 溢出乘法

let aa: UInt8 = 0
aa &- 1 // 255

let a: UInt8 = 255
a &+ 1 // 0

let a1: Int8 = 125
a1 &+ 11 // -120

let a1: Int8 = 127
a1 &* 2 // -2
```

### Optional 合并空运算符

a ?? b 等同于 a !=. nil ? a : b

```swift
func addTow(num: Int?, num1: Int?) -> Int {
	return (num ?? 0) + (num1 ?? 0)
}
```

### Range & 区间运算符

… 闭区间；..< 开区间

```swift
1...5 // {lowerBound 1, upperBound 5}
1..<5

let arr = ["a", "b", "c"]
for i in 1..<5 { // arr[2...] | arr[..<2]
    print("index is \(i)")
}

let range = ..<5 // PartialRangeUpTo<Int>
let range = ...5 // PartialRangeThrough<Int>
range.contains(4) // true
range.contains(7) // false

let str = "cc"
var range = str.startIndex..<str.endIndex
// {{_rawBits 1}, {_rawBits 131073}}
range = str.index(str.endIndex, offsetBy: -1)..<str.endIndex
// {{_rawBits 65793}, {_rawBits 131073}}

// reversed
for i in (0..<10).reversed() { }
```

Comparable 区间

```swift
let range = "a"..."z" // {lowerBound "a", upperBound "z"}
for char in "hello!" {
    if !range.contains(String(char)) {
        print("\(char) 不是字母")
    }
}
// ! 不是字母
```

### 位运算符

```swift
~ // 位取反运算符
& // 位与运算符
| // 位或运算符
^ // 位异或运算符
<< // 位左移
>> // 位右移
```

### 运算符优先级和结合性

```swift

```

### Struct & Class 自定义运算符

```swift

```

### 自定义运算符

```swift

```

## 流程控制

### 循环控制

```swift

```

### Switch

```swift

```

### Guard 条件判断

```swift

```

### 模式和匹配模式

```swift

```

## 第四章：流程控制
