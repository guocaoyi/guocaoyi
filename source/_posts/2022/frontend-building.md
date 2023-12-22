---
layout: post
title: 前端项目构建（演变与编译原理）
date: 2022-01-21
tags:
  - frontend
---

# 前端项目构建（演变与编译原理）

```txt
.
├── 前端的目的、手段与发展
│   ├── 目的
│   ├── 手段
│   └── 发展
├── 编译原理
│   ├── 语法编译（GPL \ DSL Compiler）
│   ├── 模块打包（Module bundler）
│   └── 代码压缩（Mangle）
├── 总结
│   ├── 总结
│   └── 总结
└── 任务
    └── 任务
```

## 前端的目的与现状

### 目的

开发时：开发效率高效、降低心智负担、生态丰富、职责分明&边界清晰
编译时：编译速度快、环境稳定、语法兼容
运行时：低延迟、运行稳定

### 手段

开发时：多语言、DSL、类型检查、代码兼容性、尝试不同的编程范式
编译时：模块化、视图模型抽象（组件化）、DCE & LCI、代码压缩、
代码逻辑按需加载、模块编译、

### 现状

- 模块化方案之变
  - SystemJS
    - 提高生产环境模块的性能的
    - Web Online Code Editor：Stackbliz \ CodeSandBox \ CodePen
    - Webpack 的 Bundle \ Chunk 的实现借鉴了 systemjs 的能力
  - AMD & UMD
    - requirejs AMD 规范
    - UMD = AMD + CommonJS 在浏览器端提供模块化
    - webpack chunk
  - CommonJS
    - sea.js
    - CMD
    - Node 环境
  - ESM
    - 建议使用
    - ES6 提出、ES11 dynamic import
- 模型之变
  - 视图模型抽象
    - React.Component \ React.PureComponent
    - Vue SFC
  - 数据模型抽象
    - React Hook
    - Vue setup \ Composition API
    - MobX: observable
    - Redux \ Store
  - 业务模型抽象
    - 微前端子应用
- 编程范式之变
  - IP vs FP vs OOP vs RP
    - SwiftUI vs Android
    - React Component vs React Hooks
  - Composition API vs Options API
  - Composition over inheritance
- 架构之变
  - MVC vs MVP vs MVVM
  - CSR vs SSR vs SSG vs ISR
    - 千米云活动采用了 SSR + SSG
    - admin-web 采用了 CSR + SSR
    - ISR：增量式的渲染，是 SSG 的一种 Lazy render 方案，在请求时生成页面并缓存；解决了 SSG 无法更新的问题；
    - DPR \ SPR
  - MPA vs SPA vs 微前端
    - MPA 可以平滑迁移
    - 微前端架构
- 工程化方案之变
  - 配置 vs 约定
  - 中心化 vs 去中心化
  - 前后端分离 -> 前后端一体化（Taro \ UniApp \ Modern.js \ Rax）

## 编译原理

### 语法编译（GPL \ DSL Compiler）

- Vue（DSL -> JS）
  - 基于 状态机 的 Vue Parser 实现原理以及 AST 的生成
  - AST 转化以及目标代码的生成
  - DSL 在千米建站项目中的应用
- TypeScript（GPL -> JS）
  - BNF 范式 & EBNF 范式
  - TypeScript 编译流程概览
  - 在建站 3.0 项目中的运用

### 模块打包（Module bundler）

Webpack

- Dependency Graph 的基本作用
- Tree Shaking 的实现原理
  - 代码静态分析（词法层、语法层分析；不涉及到语义）
- 基于 Tapable 的流程管理系统

### 代码压缩（Mangle）

代码压缩常见的思路：Compress、Mangle、Rename

```typescript
// sum to numbers
function towSum(pre, next) {
  return pre + next
}
console.info(towSum(10, 2))
```

```typescript
// compress
function towSum(pre, next) {
  return pre + next
}
console.info(towSum(10, 2))
```

```typescript
// rename
function t(p, n) {
  return p + n
}
console.info(t(10, 2))
```

```typescript
// 基于语义分析的压缩
console.info(12)
```

- Terser
  - 基于语义分析的代码压缩

## 前沿以及未来

### 前沿

- Bundle less | Unbundled
- ESM next
- DX & UX
- Micro-FrontEnd
- Pro Code vs Low / No Code
- 跨端技术\前后端一体化
  - 字节 Modern.js
  - 淘宝 dove

## 总结

不是指做 UI 的技术，而是由 Web 原生语言、Web Runtime、Web 技术生态组成的技术栈，不是只在浏览器里才有前端技术，而是有 Web Runtime、有 Web 语言的地方，就有前端技术

传统前端开发不是成熟的软件研发体系，缺乏足够的抽象和基建，导致 DX 和 UX 始终存在矛盾，此消彼涨。以往的产品开发中，习惯更重视 UX，这有两方面的原因，一来是因为产品是由产品主导，因此更重视 UX， 不会过多关注开发者体验，再就是缺乏足够的抽象和基建，导致 DX 和 UX 之间必须牺牲一个。
