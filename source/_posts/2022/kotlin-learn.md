---
layout: post
title: 菜鸟《Kotlin 教程》笔记
date: 2022-05-15
tags:
  - lang/kotlin
---

# 菜鸟《Kotlin 教程》笔记

## Kotlin 基础

### 背景

- 由 JetBrians 设计并开源
- Kotlin 不仅仅是一门 JVM 方言（分为 Kotlin Native \ Kotlin JS \ Kotlin JVM）
- Google I/O 2017 年作为 Android 官方首选开发语言
- 文件以 `.kt` 结尾（其中脚本 DSL 以 `.kts` 结尾）
- 无需匹配目录和包（不同于 Java 一个文件一个类），可以放在任何文件和目录

### 优势

- 简洁：大大减少样板代码的数量
  - 结构性的 get/set、构造函数、单例
  - 字面量创建 List/Map
- 安全：语法层面避免空指针异常
- 互操作性：充分利用 JVM 、 Android 和浏览器的现有库
- 体验一致的开发工具链
- 支持拓展（类似与 Swift 的 extension）；操作符重载
- 语法糖很多
  - 通过语法糖实现了一下基本设计模式（单例、委托、策略、观察者等）

<!-- more -->

### 劣势

- 语法糖太多（软性关键字被占用），导致语义复杂；而要理解这些语法糖，需要了解 Java 的实现
- 包体积变大（Kotlin 库文件）
- 编译时略长（涉及到往 Java 字节码的转译）
- 开源不彻底；命令行工具链不完善（深度绑定IDE）

### CLI

```bash
# -d 设置输出名称
# -include-runtime .jar 文件包含 Kotlin 运行库
kotlinc hello.kt -include-runtime -d hello.jar
java -jar hello.jar
```

```bash
# 生成的 jar 给其他 Kotlin 代码使用，无需包含 Kotlin 运行时库
kotlinc hello.kt -d hello.jar

# HelloKit 默认类名
kotlin -classpath hello.jar HelloKit
```

### REPL

`bin/kotlinc-jvm`

### 脚本语言 .kts

```kotlin
// list_folders.kts

import java.io.File

val folders = File(args[0]).listFiles { file -> file.isDirectory() }
folders?.forEach { folders -> println(folder) }
```

```bash
kotlinc -script list_folders.kts ./
```

## 基础语法

### ::默认:: 导入到每个 Kotlin 文件的包

```kotlin
import kotlin.*
import kotlin.annotation.*
import kotlin.collections.*
import kotlin.comparisons.*
import kotlin.io.*
import kotlin.ranges.*
import kotlin.sequences.*
import kotlin.text.*

/* if target jvm */
import java.lang.*
import kotlin.jvm.*

/* if target js */
import kotlin.js.*
```

### Kotlin 的代码结构

不同于 Java；Kotlin 函数是一等公民；可以在文件内（TOP Level）定义变量、函数、匿名函数、类、object 、data 类、enum 类、Sealed Class、Extensions等

- Kotlin 是大小写敏感的

```kotlin
import cn.yalda.main
import java.util.*

// cn.yalda.main.test
fun test(args: Array<String>) {}

// cn.yalda.main.Text
class Test {}

val a: Int = 123
val sumLambda: (Int, Int) -> Int = { x, y -> x + y }

public fun main(args: Array<String>): Unit {}
public fun main(args: Array<String>) {}
fun main(args: Array<String>) {}
```

### 函数的定义和类型声明

```kotlin
fun sum(a: Int, b: Int): Int {
	return a + b
}
// 返回类型自动推断（函数单一表达式）
fun sum(a: Int, b: Int) = a + b // single expression

// 无返回值，声明 Unit 类型（类似 Java 和 TS 的 void）
fun printSum(a: Int, b: Int): Unit {
	println(a + b)
}

// public 必须明确声明返回值类型
public fun sum(a: Int, b: Int): Int = a + b

// 返回值是 Unit 类型，则可以省略
public fun printSum(a: Int, b: Int) {
	print(a + b)
}
```

### 函数的调用

```kotlin
fun sum(a: Int, b: Int, c: Int):Int {
	println("a = $a,b =  $b,c = $c")
    return a + b + c
}

sum(0, 1, 2) // a = 0, b = 1, c = 2
sum(a = 0, b = 1, 2) // a = 0, b = 1, c = 2
sum(a = 0, 1, c = 2) // a = 0, b = 1, c = 2
sum(0, b = 1, c = 2) // a = 0, b = 1, c = 2
sum(c = 2, b = 1, a = 0) // a = 0, b = 1, c = 2
sum(c = 0, b = 1, 2) // Error
```

### :: 操作符

```kotlin
class Person(val nickName: String) {
    fun foo(a: Int): Int {
        println("$a")
        return a
    }

    fun getFun(age: Int, function: (Int) -> Int) {
        function(age)
    }
}

val p = Persion("musk")
p.getFun(10, p::foo) // 10
```

### 可增参数（可变长参数函数）

```kotlin
fun vars(vararg v: Int){
	for(vi in v) println(vi)
}

vars(1,2,3,4) // 1234
```

### Lambda（匿名函数 \ 闭包表达式）

```kotlin
fun main(args: Array<String>) {
	val sumLambda: (Int, Int) -> Int = { x, y -> x + y }
	println(sumLambda(1, 2))
}

val sumLambda: (Int, Int) -> Int = { x, y -> x + y }
fun main(args: Array<String>) {
	println(sumLambda(1, 2))
}

// Named arguments are not allowed for function types
```

### 定义常量和变量

```kotlin
// 变量 var <标识符>: <类型><可选> = <初始化知>
val name: String
name = "xx"
name = "yalda" // Val cannot be reassigned
// 常量与变量都可以没有初始化值,但是在引用前必须初始化

// 常量 val <标识符>: <类型><可选> = <初始化知>
var age: Int = 1
var age1: Int // 声明时未初始化，必须声明类型
var age = 0 // 编译器支持自动类型判断
```

### 注释

```kotlin
// single row command
/*
	multiple row commands */
/*
 	multiple row commands
	/* kotlin support nest commands*/
*/
```

### 字符串模板

```kotlinchr

val str: String = "single string"
val temp: String = "$str"
val temp2: Strig = "$str length is ${str.length}"
```

### Null 检查机制

```kotlin
var age: String? = "23" // ? means optional

var age = age!!.toInt() // 23 or null-point-exceptions
val age1 = age?.toInt() // 23 or null
val age2 = age?.toInt() ?: -1 // 23
```

### 类型检测&自动类型转换

```kotlin
fun getStringLength(obj: Any): Int? {
	if (obj is String) return obj.length
	if (obj !is String) return null // or

	if (obj is String && obj.length > 0) return obj.length //

	return nulll
}
```

### 区间（Range）

由 `..` 的 rangeTo 函数 & in & ~!in 形成

```kotlin
for (i in 1..4) print(i) // [1, 4]
for (i in 1 until 4) print(n) // [1, 4)
for (i in 4..1) print(i) //
for (i in 1..4 step 2) print(i) // 13
for (i in 4 downTo 1) print(i) // 4321
```

## 基本数据类型

### 基本数值

Byte \ Short \ Int \ Long
Float \ Double

#### 字面常量

```kotlin
val oneMillion = 1_000_000
val ID = 321023_1999_1212_0000L
val bigD = 123.5e10
val f= 123213f // 123213F 123213.0
val hexBytes = 0xCCCCCC // 13421772
val bytes = 0b111111_00000000_111111_000000 // 66064320
```

#### 比较

```kotlin
val a: Int = 123
a == 123 // true
a === 123 // true
val b: Int = 123
a == b // true
a === b // true
val c: Int? = a
a == c // true
a === c // false
```

```kotlin
// 发现一个有趣的现象
val a: Int = 127
val c: Int? = a
val d: Int? = a
c === d // true

val b: Int = 128
val c1: Int? = b
val d1: Int? = b
c1 === d1 // false
// 个人怀疑，kotlin 对代码做了优化；小于 2^8 时使用数值对象，超过则创建新对象
```

#### 类型转换

- 较小的类型不是较大类型的子类型；在不进行显式转换下是违法的

```kotlin
val b: Byte = 1
val i: Int = b // error
val i: Int = b.toInt()

// 有些情况会做自动类型转化
val l = 1L + 3 // Long + Int -> Long
```

```kotlin
toByte(): Byte
toShort(): Short
toInt(): Int
toLong(): Long
toFloat(): Float
toDouble(): Double
toChar(): Char
```

#### 位操作符

```kotlin
shl // << ; 8 shl 1 == 16
shr // >> ; 8 shr 1 == 4
ushr // >>>
and // &
or // |
xor // ^
inv // 反向
```

### 字符

```kotlin
val c: Char = 'c' // 必须是单引号
val c: Char = '\u2354' // \t \n \b \r \' \" \\ \$

if(c !in '0'..'9') // range
```

### 布尔 Boolean

```kotlin
val b: Boolean = false // false or true
false || true // true
false && true // false
!false // true
```

### 数组

由类 Array 实现，拥有 size \ get \ set 方法；Kotlin 中的数组是不协变的（invariant）；
创建方式：1、arrayOf() 2、工厂函数

```kotlin
// [1,2,3] arrayOf 函数
val a = arrayOf(1, 2, 3)
a[0]
a[0] = 1

// [2,4,6] array 工厂函数
val a1: Array = Array(3, { x -> x * 2 })
val ia: IntArray = intArrayOf(1,2,3)
val ba: ByteArray = byteArrayOf(1,2,3)
val sa: ShortArray = shortArrayOf(1,2,3)
```

### 字符串

同 Java 一样 String 是不可变的

```kotlin
for (c in "str") println(c)

val text = """
	  |multiple str1
    |multiple str2
    |multiple str3
"""
text // some pre space(include |)
text.trimMargin() // default use | for replace pre space
text.trimMargin(">") // use > for replace pre space
```

### 字符串模板

```kotlin
val i = "10"
val s = "len = ${i.length}" // len = 2
val ms = """
	|price is $$i
""" // price is $10
```

## 条件控制

Kotlin 里的 `if` 和 `when` 均可以作为条件控制语句，也可以作为表达式

### IF 表达式

```kotlin
// condition is a statement return Boolean; ex. i in 1..8
if (condition) ..

var max = a
if (a < b) max = b
if (a < b) max = 2 else max = 1
if (a < b) {
	max = b
}

// 作为表达式返回结果
val max = if (a > b) a else b // Kotlin 没有三元表达式
val max = if (a > b) {
	println("Choose a value")
	a
} else {
	println("$b")
	b
}
```

### When 表达式

类似于 C & Java 的 switch 语句

```kotlin
// 作为表达式使用时，符合的分支的值就是表达式的值
// 也可以作为语句（条件控制语句）使用
when (x) {
	1 -> println("11")
	2 -> println("22")
	3, 4 -> println("3344")
	in 5..10 -> println("5 to 10")
	!in 11..20 -> println("no in 11 to 20")
	else -> {
		println("default")
	}
}

// use is or !is
fun hasPrefix(x: Any) = when(x) {
	// Any 是 Kotlin 所有类的基类
	is String -> println("is String")
	is Int -> println("is Int")
	else -> {
		println("else")
	}
}

// replace if-elseif chain
fun String.isInTen() = this in "1".."10"
fun String.isInHundred() = this in "1".."100"
var a = "50"
when {
	a.isInTen() -> println("a in [1, 10]")
	a.isInHundred() -> println("a in [1, 100]")
	else -> println("a not in range")
}

// use in
val items = setOf("apple", "huawei")
when {
	"xiaomi" in items -> println("mi")
	"vivo" in items -> println("mi")
}
```

## 循环控制

### for 循环

对提供迭代器的对象进行遍历：`for (item in collection) statement`

```kotlin
// array & array.indices & array.withIndex()
for (v in arrayOf(1,2,3)) print(v)  // 123
for (i in arrayOf(1,2,3).indices) print(i) // 012
for (v in Array(3, { x -> x * 2 })) print(v) // 024
for ((i,v) in arrayOf(1,2,4).withIndex()) println("$i $v")

// list & & list.indices list.withIndex()
for (v in listOf(1,2,3)) print(v) // 123
for(i in listOf(1,2,3).indices) print("$i") // 012
for ((index, value) in listOf(1,2,3).withIndex()) println(v)

// set & set.withIndex()
for (v in setOf("aa", "bb")) println("$v")
for ((i, v) in setOf("aa", "bb").withIndex()) println("$i $v")

// map & map destruct
for (v in mapOf("a" to "xx", "b" to "yy")) println(v) // a=xx \n b =yy
for ((k, v) in mapOf("a" to "xx", "b" to "yy")) println("$k $v") // a xx \n b yy

// range
for (v in 1..10) print("$v") // 12345678910
for (v in 1 until 10) print(v) // 123456789
for (v in 1..10 step 2) print(v) // 13579
for (v in 10 downTo 1) print(v) // 10987654321
```

### while & do…while 循环

```kotlin
while ( /* Boolean expression */) {}
do { /* logic */ } while ( /* Boolean expression */)
```

### 返回和跳转

- return 从循环体的包装函数 & Lambda 返回
- break 终止循环体
- continue 跳出本次循环，进入下一次循环

```kotlin
while(i < 10) {
	i += 1
  if (i == 2) continue
	if (i ==5 ) break
  print(i)
} // 134
```

### Break & Continue & Label

任何表达式都可以使用标签（label@）来标记

```kotlin
myloop@ for(i in 1..10) {
	if(i == 3) break@myloop
	print(i)
} // 12

fun main(args: Array<String>) {
	val ints = listOf(1,2,3,4,5)
	ints.forEach {
        if(it == 2) return
        print(it)
	} // 1 (直接从 main 函数返回)

	// 给 forEach 添加 label；return 到 forEach 函数（如不加，则直接从 main 函数返回）
	ints.forEach lit@ {
        if(it == 2) return@lit
        print(it)
	}

	// 等效；Lambda 表达式（隐式标签，与 lambda 函数同名）
	ints.forEach {
		if(it == 2) return@forEach
		print(it)
	}

	// 等效；使用匿名函数替代 lambda 表达式
	ints.forEach(fun(value: Int){
		if(value == 2) return
		print(it)
	})
} // 1345
```

## 类和对象

### 类的结构 & 声明

Kotlin 类包含：构造函数、初始化代码块、内部类、函数、属性、对象声明

```kotlin
class EmptyClass // 空类
val e = EmptyClass() // 实例化时无需 new 关键字

class Demo {
	val name: String? = "yalda" // 属性（成员变量）
	val website: String? = "yalda.cn" // 属性（成员变量）
	fun foo() = print("${this.website}") // 函数（成员方法）
}
val d = Demo()
d.name // yalda access property name
d.foo() // yalda.cn access & run foo method

// 主构造器以及一个或多个次构造器；主构造器写在类头部（类名后）
class Person constructor(firstName: String) {}
// 如果构造器没有注解、以及修饰符可省略 constructor 关键字
class Person(firstName: String) {}
class Student (val nickName: String) {}
```

### Getter & Setter

```kotlin
val <propertyName>[: <PropertyType>] [= <initializer>]
	[<getter>]
	[<setter>]

var name: String = "" // 实现 getter & setter
val name: String // Error, getter & must init in constructor
val name: String = "" // 实现 getter

class Person {
	var name: String? = "yalda"
    	get() = field!!.toUpperCase()
      set

	var site: String? = ""
	    get() = field // equals get or no defined
		set(s) {
			field = "https://$s"
		}

	var heiht: Float = 145.0f
    	get
    	private set
}
```

### Late init

非空属性必须在定义时初始化；延迟初始化需要用到 `lateinit` 关键字

```kotlin
public class MyTest {
	lateinit var subject: TestSubject

	@Setup fun setup() {
		subject = TextSubject()
	}

	@Setup fun test() {
		subject.method()
	}
}
```

### 主构造器 & 初始化代码块 & 实例化

```kotlin
class Person constructor(nickName: String) {
	init {
		println(nickName)
	}
}

// 简约语法，通过主构造器定义属性和初始化属性值
class Person(val nickName: String = "jok")
class Person(val nickName: String = "jok") {
	init {
		println("nick is $nickName")
	}
}

val p = Person("king") // nick is king
p.nickName // king
```

### 次构造函数

```kotlin
class Person {
    constructor(parent: Person) { // prefix constructor
        parent.children.add(this)
    }
}

// 如果有主构造器，每个次构造器都要（直接或间接）代理主构造器；并使用 this 代理主
class Person(val nickName: String) {
	constructor(name: String, site: String): this(name){
	}
}
class Person(val nickName: String) {
  var site: String = ""
	// this(name, site) 代表 主构造器
	constructor(name: String, site: String): this(name){
		this.site = site
		println("1> name $name, site $site")
	}

	// this(name, site) 代表 1> 次构造器
  constructor(name: String, site: String, fields: Int): this(name, site){
		println("2> name $name, site $site, fields $fields")
	}
}

// 如果构造器参数有默认值，编译器会生成一个附加的无参构造器，这个构造函数会直接使用默认值；从而达到无参构造函数创建实例
class Customer(val customerName: String = "")
```

### 抽象类

抽象是 OOP 的特征之一，采用 `abstract` 来声明

```kotlin
// 不必对抽象类标注 open
abstract class Person {
	abstract fun walk(distance: Double): Unit
	abstract fun step(): Double
}

open class Base {
	open fun f() {}
}

abstract class Derived: Base() {
	override abstract fun f()
}
```

### 嵌套类

```kotlin
class Outer {
	val name = "outer name"
	class Inner {
		val name = "inner name"
	}
}
Outer().name // outer name
Outer.Inner().name // inner name
```

### 内部类

内部类采用 `this@<class-name>` 来访问外部类上下文

```kotlin
class Outer {
	private val name = "outer name"
  	val nickName = "nike man"
	inner class Inner {
		fun name() = name // 可以直接访问外部类成员（包括私有）
		fun nick() = nickName
		fun foo(): String {
			val cxt = this@Outer // 外部类引用
          return cxt.nickName
       }
	}
}
Outer().Inner().name() // outer name
Outer().Inner().nick() // nike man
Outer().Inner().foo() // nike man
```

### 匿名内部类

```kotlin
class Test {
    val v = "viv"
    fun setInterFace(test: TestInterFace) {
        test.foo()
    }
}

interface TestInterFace {
    fun foo()
}

val test = Test()
test.setInterFace(object: TestInterFace {
	override fun foo() {
		println(">>foo print 匿名内部类")
	}
})
 // >>foo print 匿名内部类
```

### 类修饰符

- class modifier
  - abstract // 抽象类
  - final // 类不可继承，默认属性
  - enum // 枚举类
  - open // 父类（基类、可继承类），类默认 final
  - annotation 注解类
  - enum // 枚举类
  - data // 数据类
  - sealed // 密封类
- visibility modifier
  - private // 仅同一个文件内可见
  - protected // 同一个文件或者子类可见
  - public // 所有调用方可见
  - internal // 同一个模块可见

```kotlin
// main.kt
private fun foo() {} // 文件 mian.kt 内可见
public var: MAX_LAVEL = 24 // 所有调用方均可见
internal val baz = 0 // 想通模块内可见
```

## 继承

- Kotlin 所有类都隐式继承 Any 类；Any 类是所有类的超类包含了 `equals()` `hashCode()` `toString()` 三个函数
- Any类 不是 java.lang.Object
- 如果一个类需要可继承需 `open` 关键字修饰
- 子类有构造函数，则基类必须要主构造函数立即初始化

```kotlin
open class Response(value: Int, msg: String)
class ErrRes(value: Int, msg: String): Response(value, msg) {
	init {
		println("$value, $msg")
	}
}
ErrRes(value = 500, msg = "server err") // 500, server err
```

### 子类是否有主构造函数

```kotlin
// 子类无主构造函数，需要在每个次构造函数中用 super 来初始化基类
// 而基类也可以提供多种构造函数，供子类初始化
class ErrRes: Response {
	constructor(): super(200, "ok") {
		println("200")
  }
	constructor(value: Int): super(value, "error") {
   	println(value)
  }
	constructor(value: Int, msg: String): super(value, msg) {
		println("$value $msg")
	}
	constructor(value: Int, errorCode: Int, msg: String): 	super(value,msg) {
		println("$value $errorCode $msg")
   }
}
```

### 重写 override

open class 函数默认 final 修饰，如果提供重写能力需添加 `open` 修饰

```kotlin
open class Response {
	fun getErrCode() {} // final can not be overrided
	open fun redirect() {} // can be overrided
}
```

如果有多个相同方法，则必须重写，可使用 `super<Type>` 选择性调用

```kotlin
open class Response {
	open fun getCode(): Int {
		println("response code = 200")
      return 200
  }
}

interface IRes {
	fun getCode(): Int {
		return 500
	}
}

class HomeRes: Response(), IRes {
	override fun getCode(): Int {
  		super<Response>.getCode()
		super<IRes>.getCode()
		return 302
	}
}
HomeRes().getCode() // 302
```

### 属性重写 property override

```kotlin
interface Badge {
	val count: Int
}
class Game(override val count: Int): Badge
Game(count = 1).count // 1

// 可以使用 var 重写 val property; 反之不行
class Game: Badge {
	override var count: Int = 1
}
```

## 接口

- Kotlin 接口和 Java 的接口类似
- 使用 `interface` 关键字定义
- 允许有默认实现

### 实现接口

```kotlin
interface MyInterface {
	fun boo() // 未实现，抽象方法
	fun foo(): String {
		return "interface foo"
	}
}

class MyClass: MyInterface {
	// 未实现的接口函数，必须实现
	override fun boo() = println("class boo")
}
class MyClass1: MyInterface {
	override fun boo() = println("class1 boo")
  override fun foo() = "class1 foo"
}
```

### 接口中的属性

接口的属性只能是抽象的，不允许初始化值；实现接口必须重写属性

### 函数重写

继承多个接口时， 实现类可以通过 `super<Interface>` 来选择性调用接口函数（未实现的抽象方法可以忽略）

## 扩展

- Kotlin 可以对一个类（属性、方法）进行扩展且不需要继承或者装饰器模式（Decorator）
- 扩展是一种静态行为
- 对被扩展的类代码本身不会造成任何影响（有点类似 JS 的 Reflect）

### 扩展函数

```kotlin
// receiverType 函数的扩展对象
// functionName 扩展函数名
// params 参数 or NULL
fun receiverType.functionName(params) {
	/* body */
}

// Kotlin 内置对象
fun String.trimLength(): Int {
	return this.trim().length
}
"   ccc".trimLength() // 3

// custom class
class User(var name: String)
fun User.nickName() = "taylor ${this.name}"
User(name = "swift").nickName() // taylor swift

// Kotlin 集合对象
fun MutableList<Int>.replaceItem(pre: Int, post: Int) {
    val tmp = this[pre]
    this[pre] = this[post]
    this[post] = tmp
}
mutableListOf(1,2,3).replaceItem(0, 2) // [3,2,1]
```

### 扩展函数 & 扩展属性

- **扩展函数是静态解析，不是接收者类型的虚拟成员**
- 扩展函数和成员函数一致时，优先使用成员函数
- 扩展属性允许定义在类和 Kotlin 文件中，但是不允许在函数中定义
- 只能显示定义 getter / setter，所以不允许被初始化
- 扩展属性只能被声明为 `val`

```kotlin
// 扩展空对象
fun Any?.toString(): String {
    if(this == null) return "nil"
    return ">> ${this.toString()}"
}

1?.toString() // 1 优先使用成员函数
null.toString() // null

// 扩展属性
val <T> List<T>.lastIndex: Int
	get() = site - 1

// 初始化
val Foo.var = 1 // Error 初始化属性没有后端字段（backing field）
```

### 伴生对象的扩展

- 伴生对象内的成员相当于 Java 中的静态成员，其生命周期伴随类始终
- 伴生对象内的成员和函数可以直接用类名引用
- 伴生对象扩展分为：类内扩展 和 类外扩展
  - 两者（可以同名）互不影响
  - 类外扩展的伴生对象函数可以被伴生对象内的函数引用

```kotlin
class MyClass {
	companion object { // MyClass 伴生对象
		val field1 = 1 // 类内伴生对象类成员
		val field2 = "field2" // 类内伴生对象类成员

		// 类内伴生对象函数 cFun
		fun cFun() {
			println("companion cfun")
			foo() // 伴生对象可以引用，类外扩展的伴生对象
		}

		fun cFun2() {
			println("companion cfun2")
			cFun() //
		}
	}

	// 类内扩展
	fun MyClass.Companion.foo() = println("伴生对象类内扩展函数")
	fun test() {
		MyClass.foo()
	}
	init {

	}
}
```

### 扩展的作用域

- 函数扩展和属性定义在顶级包下 `package cn.yalda`

```kotlin
// cn/yalda/main.kt
package cn.yalda

fun Yalda.foo() {}

// cn/yalda/models/home
package cn.yalda.models.home

import cn.yalda.foo // or import cn.yalda.*

val y: Yalda = Yalda()
y.foo() // ...
```

### 扩展声明为成员

- 在一个类（分发接受者）内部可以为另一个类（扩展接受者）声明扩展
- 假如某个函数，分发接收者和扩展接收者均存在，扩展接收者优先；
- 可以使用 `this` 关键字类使用分发接受者函数

```kotlin
class Student {
	fun study() = println("day day up")
}
class Classmeta {
	fun study() = println("meta study")

	fun Student.learn() {
		study() // class Student(扩展接受者优先)
		this@Classmeta.study() // Classmeta.study
	}
	fun caller(s: Student) = s.learn()
}
val s = Student()
val m = Classmeta()
m.caller(s) // day day up \n meta study
```

## 数据类 & 密封类 & 枚举类

### 数据类定义 & 复制 & 实例化

- 数据类创建一个只包含数据的类，`data` 关键字来修饰 class
- 编译器从主构造器中所声明的提取（?定义）了 `equals()/hashCode()`、`toString()`、`componentN()`、`copy()` 等函数；已经明确定义，不会再生成
- 条件
  - 主构造器至少包含一个参数
  - 主构造器参数必须标识 `val` or `var`
  - 类不可声明 `abstract` `open` `sealed` `inner`
  - 不能继承其他类（但可以实现接口）

```kotlin
data class User(val name: String, var price: Int)

// 复制使用 copy 函数，可以复制对象且修改部分属性
val nike = User(name = "nick", price = 899)
val ig = nike.copy(name = "ig") // User(name=ig, price=899)

// destruct 类结构
val (name, price) = ig
println("$name is ￥$price") // ig is ￥899
```

### 标准数据类

- Kotlin 内置 了 `Pair` 以及 `Triple` 数据类
- 命名数据类是更好的设计选择
- 代码可读性更强而且提供了有意义的名字和属性

### 密封类

- 表示受限的类结构
- 等同于枚举类的拓展（一个值为有限的几种类型，而不能有其他类型）
- 使用 `sealed` 来修饰类
- 密封类可以有子类，但是所有子类均内嵌在密封类的文件中
- sealed 不能修饰 `interface` `abstract class`

```kotlin
sealed class Expr
data class Const(val number: Double) : Expr()
data class Sum(val e1: Expr, val e2: Expr) : Expr()
object NotANumber : Expr()

fun eval(expr: Expr): Double = when (expr) {
    is Const -> expr.number
    is Sum -> eval(expr.e1) + eval(expr.e2)
    NotANumber -> Double.NaN
}

fun eval(expr: Expr): Double = when(expr) {
    is Expr.Const -> expr.number
    is Expr.Sum -> eval(expr.e1) + eval(expr.e2)
    Expr.NotANumber -> Double.NaN
    // 不再需要 `else` 子句，因为已经覆盖了所有的情况
}
```

### 枚举类

- 基本用法是实现一个类型安全的枚举
- 都好分隔，每个枚举常量都是一个对象
- 每个枚举都是枚举类的实例（可以被初始化）

### 枚举初始化

```kotlin
// defined
enum class Color { BLACK, RED, BLUE }
// Color.BLACK 0 ；默认从 0 开始

// initiailized
enum class Color(val hex: Int) {
	BLACK(0x000000),
	GREY(0xCCCCCC),
	BLUE(0x232323)
}

// 声明自己的匿名类和方法、以及覆盖基类的方法
enum class ProtocolState {
	PADDING {
		override fun state() = OK
	},
	OK {
		override fun state() = PADDING
	};
	// 枚举累定义成员，需要用 ; 将成员定义中枚举常量分隔开来
	abstract fun state(): ProtocolState
}
```

### 枚举类的使用

```kotlin
// values() -> Arrau<EnumClass>
for(en in Color.values()) println(en)
// valueOf(value: String) -> EnumClass
Color.valueOf("BLACK") // BLACK

Color.valueOf("BLACK").name // BLACK
Color.valueOf("BLACK").ordinal // 0

// kotlin@1.1 support enumValues<T>() & enumValueOf<T>()
enumValues<Color>().joinToString { it.name }
for(v in enumValues<Color>()) println("${v.name}")
```

## 泛型

- 泛型即『参数化类型』，类型参数化作用于接口、类、方法

```kotlin
// 泛型类的声明
class Box<T>(var value: T)
val box: Box<Double> = Box<Double>(1.0)
val triple = Box<Int>(value = 199)

// 泛型函数的声明
fun<T> boxOf(value: T) = Box(value)

// 可以完整写出类型，也可以省略有编译器推断
boxOf<Double>(1.00).value // 1.0
boxOf(1).value // 编译器类型推断
```

### 泛型约束

使用泛型约束来设定一个给定参数允许的类型

```kotlin
// Comoparable 的子类型可以替代 T
fun <T : Comparable<T>> sort(list: List<T>) {
}
sort(listOf(1,2)) // ok
sort(listOf(HashMap<Int, String>())) // error
// HashMap<Int, String> 不是 Comparable<HashMap<Int, String>> 的子类型（没搞明白）

fun <T> copyWhenGreater(list: List<T>, threshold: T): List<String>
    where T : CharSequence,
          T : Comparable<T> {
    return list.filter { it > threshold }.map { it.toString() }
}
```

### 型变

- Kotlin 没有通配符类型
- 声明处型变（declaration-site variance） 与 类型投射（type projections）
- 声明处型变：注解修饰符 in（消费者）、out（生产者）
  - out 使得参数协变；只能用于输出，可以作为返回值类型，但无法作入参类型
  - in 使得参数逆变；只能用于输入，可以作为入参类型，但无法作返回值类型

```kotlin
// 参数协变
class Student<out U>(val klass: U) {
	fun learn(): U = klass
}
val stua: Student<Int> = Student(22) // .learn() 22
val stub: Student<Double> = Student(22.99) // .learn() 22.99

// 参数逆变
class Student<in I>(klass: I) {
	fun learn(a: I) = println(a)
}
var stua = Student<Double>("xxx")
val stub = Student<Double>(22.99)
stua = stub // Error inferred type is String but Double...
```

### 星号投射

- Kotlin 提供语法了 star-projection 来约束泛型类型的所有实体实例都是投射的子类型
- `*` 指代了所有类型，相当于 `Any?`

```kotlin
Foo<out T>; Foo<> 等价于 Foo<out TUpper>
Foo<in T> T 是反向协变的类型参数; Foo<> 等价于 Foo<in Nothing>
所以 Foo<*> 对于读取值的场景，等价于 Foo<out TUpper>
			  对于写入值的场景，等价于 Foo<in Nothing>

// ex.
interface Function<in T, out U>
// 可以出现一下几种星号投射
Function<*, String> 等价于 Function<in Nothing, String>
Function<Int, *> 等价于 Function<Int, Out Any?>
Function<,> 等价于 Function<in Nothing, Out Any?>
```

```kotlin
class Student<T>(val name: T, val age: T)

val s1: Student<Int> = Student(782351, 17)
val s2: Student<*> = Student("sily", 18)
val s3: Student<Any?> = Student("sily", "20")
val l: ArrayList<*> = arrayListOf(s1, s2, s3)
```

## 对象

### 对象表达式

- 实现一个匿名内部类的对象用于方法的参数
- 通过对象表达式可以直接得到一个对象
- 在对象表达式中可以方便的访问的作用域中的其他变量

```kotlin
val site = object {
	var name = "yalda"
	val site = "yalda.cn"
}

class Student {
	val name = "yalda"
	// return 匿名对象类型
	private fun learn() = object {
		val course = "$name 偷偷学 math"
	}

	// return Any type
	fun study() = object {
		val course = "$name english"
  }

	fun find(): String {
		study().course // Unresolved reference: course
		return learn().course // math
  }
}

// 为 object 表达式声明类型
interface Factory {
	abstract val course: String
}
fun study() = object: Factory {
	override val course = "$name english"
}
```

### 对象声明

- 使用 `object` 关键字声明一个对象
- 对象可以简化一个单例的声明

```kotlin
// single instance
object Student {
    val name: String = ""
}
val s = Student
val s1 = Student
s === s1 // true

// 对象可以有超类型
open class Person {
    open fun work() = println("job")
}
object Student: Person() { // 必须对 Class 进行初始化
    val name: String = ""
    override fun work() = println("study")
}

//
object Student {
	var name = "yalda"
	object ClassRoom {
		val position = "L4"
		fun showName() = println("$name@N24432")
	}
}
val s = Student
s.ClassRooo.position //'ClassRoom' accessed via instance refer
Student.ClassRoom.showName() // yalda@N24432
```

### 伴生对象

- 一个类里面只能声明一个内部关联对象
- 伴生对象的成员类似其他语言的静态成员，但是在运行时仍然是真实对象的实例成员

```kotlin
class Student {
	companion object ClassRoom {
		fun stds(): List<Student> = listOf<Student>(Student())
	}
}
val intance = Student.stds() // [Student@23421c3]

// 如果伴生对象未命名，则通过 <class>.Companion 访问
class Student {
	companion object {}
}
Student.Companion

// 伴生对象还可以实现接口
interface Talent<out T> {
	fun create(): T
}
class Student {
	companion object: Talent<Student> {
		override fun create(): Student = Student()
	}
}
Student.Companion.create() // Student@20ad9418
```

### 对象表达式和伴生对象的语义差异

- 对象表达式在使用他们的地方立即执行
- 对象声明在第一次被访问时延迟初始化（懒人单例模式）
- 伴生对象的初始化在相应的类被加载（解析）时；与 Java 的静态初始化器语义相匹配

## 委托

### 类委托

- Kotlin 直接支持委托模式。优雅、简介；通过关键字 `by` 实现委托

```kotlin
interface IPrint {
	fun print(): Unit
	fun connect() = println("connect...")
}
class GPrint(val ip: String): IPrint {
    override fun print() = print("gprint run...")
}
class JiaBooPrint(val ip: String): IPrint {
    override fun print() = print("jiaboo run...")
}
// by 子句表示，将 p 保存在 Device 的对象实例内部，编译器将会生产继承自 IPrint 接口的所有，并将调用转发给 p
class Device(p: IPrint): IPrint by p // by 建立委托

Device(GPrint("127.0.0.10")).print() // gprint run...
Device(JiaBooPrint("127.0.0.1")).print() // jiaboo run...
```

### 属性委托

- 将一个类的某个属性委托给一个代理类，实现对该类属性的统一管理
- 该属性的 get / set 将被委托给代理类的 getValue() / setValue()

`val/var <属性名>: <类型> by <表达式>`

```kotlin
import kotlin.reflect.KProperty

class Student {
	var credit: Double by Query()
}
// 委托的类
class Query {
	operator fun getValue(thisRef: Any?, property: KProperty<*>): Double {
		return 99.91
	}
	// 如果是 val 声明则不需要提供 setValue 函数
	operator fun setValue(thisRef: Any?, property: KProperty<*>, value: Double): Double {
		//
	}
}
Student().credit // 99.91
```

### 标准委托

Kotlin 内置很多工厂方法来实现属性的委托

- 延迟属性 Lazy
  - `Lazy<T>: by lazy`
- 可观察属性 Observable
  - `by Delegates.observable()`
- 属性存储在映射中
  - `by map`
  - 常用于 JSON 解析，或者其他动态事情
- Not Null
  - `by Delegates.notNull<String>()`
  - 常用于初始化时无法确定属性值的场景
- 局部委托属性
  - `val memorizedFoo by lazy(computeFoo)`

### 委托的翻译规则

- thisRef 必须于属性所有者类型相同或其超类型
- property 必须是类型 `KProperty<*>` 或其超类型
- 对于 mutable 属性，除 getValue() 函数还必须提供 setValue()
  - property 必须是类型 `KProperty<*>` 或其超类型
  - new value 必须和属性类型相同或其超类型

```kotlin
class Student {
	var prop: Type by MyDelegate()
}

// java
class Student {
	val prop$delegate = MyDelegate()
	var prop: Type
		get() = prop$delegate.getValue(this,  this::prop)
		set(value: Type) = prop$delegate.setValue(this, this::prop, value)
}
```

### 提供委托

通过定义 `provideDelegate` 操作符

```kotlin
class ResourceLoader<T>(id: ResourceID<T>) {
    operator fun provideDelegate(
            thisRef: MyUI,
            prop: KProperty<*>
    ): ReadOnlyProperty<MyUI, T> {
        checkProperty(thisRef, prop.name)
        // 创建委托
    }

    private fun checkProperty(thisRef: MyUI, name: String) { …… }
}

fun <T> bindResource(id: ResourceID<T>): ResourceLoader<T> { …… }

class MyUI {
    val image by bindResource(ResourceID.image_id)
    val text by bindResource(ResourceID.text_id)
}
```
