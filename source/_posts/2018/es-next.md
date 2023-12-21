---
layout: post
title: ECMAScript Next
date: 2018-07-1
tags:
  - lang/js
---

# ECMAScript Next

## ECMAScript 2016(ES7)

- Array.prototype.includes()
- \*\* 运算符
- 等效于 Math.pow()

## ECMAScript 2017(ES8)

- async/await
- Object.values()
- Object.entries()
- String padding
- String.prototype.padStart
- String.prototype.padEnd
- Function Args Semi Close
- 函数参数列表允许逗号结尾；方便 git 协同
- Object.getOwnPropertyDescriptors()
- SharedArrayBuffer 对象
- Atomics 对象

## ECMAScript 2018(ES9)

- 异步迭代
- Promise.finally()
- Rest/Spread 属性
- 正则表达式命名捕获组
- 正则表达式反向断言
- 正则表达式dotAll模式
- 正则表达式 Unicode 转义
- 非转义序列的模板字符串

## ECMAScript 2019(ES10)

- 行分隔符（U + 2028）和段分隔符（U + 2029）符号现在允许在字符串文字中，与JSON匹配
- JSON.stringify
- Array.prototype.flat()
- Array.prototype.flatMap()
- 新增了String的trimStart()方法和trimEnd()方法
- Object.fromEntries()
- Symbol.prototype.description
- String.prototype.matchAll
- matchAll可以更好的用于分组
- Function.prototype.toString()现在返回精确字符，包括空格和注释
- 修改 catch 绑定
- 新的基本数据类型BigInt

## ECMAScript 2020(ES11)

- Optional Chaining
- Nullish Coalescing
- Private Fields
- Static Fields
- Top Level Await
- Promise.allSettled
- Dynamic Import
- MatchAll
- globalThis
- BigInt

## ECMAScript 2021(ES12)

- String.prototype.replaceAll
- Private Method & Private Accessors
- Promise.any & AggregateError
- WeakRefs
- 逻辑赋值操作符
- ||=、&&=、??=
- 数字分隔符

## ECMAScript 2022(ES13)

- New members of classes
  - Properties (public slots)
  - Private slots
  - Static initialization blocks
- Private slot checks
- `#privateSlot` in obj
- Top-level await in modules
- error.cause
- new Error(‘something went wrong’, { cause: otherError })
- Array.propertye.at()
- RegExp match indices
- Object.hasOwn(obj, propKey)

## ECMAScript 2023(ES14)
