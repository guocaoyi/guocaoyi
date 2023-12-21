---
layout: post
title: Kotlin & Java 语法对比
date: 2022-05-20
tags:
  - lang/kotlin
  - lang/java
---

# Kotlin & Java 语法对比

## null safe

```kotlin
val userName = a?.b?.c?.d ?: ""
```

## 对象实例化

```kotlin
class User(val name: String, val age: Int)
val user = User("yalda", 31)
```

<!-- more -->

```java
public class User {
	private String name;
	private int age;

	public User(String name, int age) {
		this.name = name;
		this.age = age;
	}
}

// main
User user = new User("xxx", 10)
```

## 属性访问

```kotlin
class User {
	val name: String? = null
}
```

```java
public class User {
	private String name;

	public String getName() {
		return name;
 	}

	public void setName(String name) {
		this.name = name;
	}
}
```

## 默认的构造函数

```kotlin
class User(var name: String)
```

```java
public class User {

    private String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name.toUpperCase();
    }

    public void setName(String name) {
        this.name = name.toUpperCase();
    }
}
```

## 快输创建 List/Map 集合类型

```kotlin
// list
val list = listOf(1, 2, 3) // 不可变
val mlist = mutableListOf(1, 2, 3) // 可变

// map
val map = mapOf("a" to "aa", "b" to "bb") // 不可变
val mmap = mutableMapOf("a" to "aa", "b" to "bb") // 可变
```

```java
// list
ArrayList list = new ArrayList();
list.add(0);
list.add(1);
list.add(2);

//
Map<String, String> map = new HashMap<String, String>();
map.put("key1", "a");
map.put("key2", "b");
```

## 对象属性调用（with\apply\let）

```kotlin
val user = User()
with (user) {
	name = "yalda"
	age = 10
}
```

```java
User user = new User();
user.setName("yalda");
user.setAge(10);
```

## Android 自动绑定 XML 文件控件定义

```kotlin
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        .....
        textView.text = "hello"
    }
}
```

## 简化 Parcelable 实现

```kotlin
import android.os.parcelable
import kotlinx.android.parcel.Parcelize

@Parcelize
class User(var age: Int, var name: String): Parcelable
```

## 协程 coroutines

```kotlin
GlobalScope.launch {
	doSomething()
	withContext(Dispatchers.Main) {
		textView.text = "coroutines done"
		Toast.makeText(this@MainActivity, "coroutines hooray", Toast.LENGTH_SHORT).show()
	}
}
```

## 简化单例（类似与 Swift 的 struct）

```kotlin
object User {
	fun test() { }
}
```

```java
public final class User {
	public static final User instance = new User();

	public void test() {}

	public static User getInstance() {
		return instance;
	}

	private User() {
	}
}
```

## 使用字符串模板简化字符串操作

```kotlin
fun getInfo():String = ">> $name; and age is ${age}"
```

```java
public String getInfo() {
	String info = ">>" + this.name + "; and age is" + this.age;
	return info;
}
```

## 使用 when 替代 switch & case

```kotlin
var id = 1
when(id) {
	1 -> println("is one")
	2 -> println("is two")
	else -> {
		println("is not one and two")
	}
}
```

```java
int id = 1;
switch(id) {
	case 1:
		System.out.println("is one");
		break;
	case 2:
        System.out.println("is two");
        break;
	default:
		System.out.println("is not one and two");
		break;
}
```

## 解构对象（Destructing declarations）类似 JS 中的 rest

```kotlin
data class User(val userName: String, val age: Int)
fun main() {
	val user = User("yalda", 31)
	val (userName, age) = user
	println("name: $userName, age: $age")
}
```
