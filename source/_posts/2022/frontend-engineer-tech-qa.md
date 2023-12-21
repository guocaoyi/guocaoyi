---
layout: post
title: 前端工程师 Tech Q&A
date: 2021-11-22
tags:
  - article
  - frontend
---

# 前端工程师 Tech Q&A

## 级别标准

- P3：实习开发、功能开发
- P4：主要开发、功能模块独立开发
- P5：项目负责人、核心开发、技术问题总结者、技术分享、人员培养
- P6：团队负责人、问题终结者、跨组沟通&协调资源、团队培养提升

## References

> 如下所列前端工程师所涉及**领域**；
> 领域（子领域）设置**题目**若干；
> 题中包含**标签**（涉及深度、提问触发词）& **答题点**（必知 **M**ust know、应知 **S**hould to know、可知 **P**osibility）

- 语言：JavaScript、ECMAScript、TypeScript、HTML、CSS
- 框架&环境：浏览器、研发工具、容器、框架通识
- 类库&库生态：React、Libs Ecosystem、数据流、SSR & SSG、BFF
- 跨端技术：微信小程序、多端统一、Node、Electron、Native、Hybrid
- 研发链路：初始化、包管理、规范标准、调试、编译、构建、测试、发布、监控
- 性能&安全：性能指标、性能评估、性能优化、源码安全、Web 安全
- 工程化：工程体系、微前端、低代码、Bundleless、CI\CD、综合能力

<!-- more -->

## 语言（Lang & DSL）

### JavaScript

- 简单聊聊 JavaScript 这门语言？
  - `#了解#`
  1. 「M」在实现层面：分为语言标准（ECMAScript 是语言标准，JavaScript 只是标准的实现）+ 语言宿主环境（对象模型、WebAPI、Node Api、WX）；
  2. 「S」语言标准提供语法、词法、基本类型、表达式、语句等；宿主环境提供内置对象、标准模块；
  3. 「P」语法借鉴 C & Java、数据结构借鉴 Java、原型借鉴 Self、函数用法借鉴 Schema、正则借鉴 Perl ；
- JavaScript 中有那些常见的内置对象，由谁提供?
  - `#了解#`
  1. 「M」值：NaN、undefined、null、Infinity；函数：eval、parseInt、parseFloat；对象：Object、Function、Boolean、Symbol、Error；数字和日期：Math、Date、Number；字符串：String、RegExp；集合：Array、Map、WeakMap、Set、WeakSet；控制对象：Promise、Generator；反射：Proxy、Reflect；
  2. [S] 内置对象是在程序执行时存在全局作用域的一些 JS 定义的值、函数、对象；
- JavaScript 代码在运行时，有那些常见的执行上下文？
  - `#熟练#`
  1. 「M」函数执行上下文；
  2. [S] 全局执行上下文、eval 执行上下文；
- JavaScript 通用模块规范，并描述其基本的区别？
  - `#熟练#` `#模块化#`
  1. 「M」CommonJS、AMD、CMD、UMD、ESM；
  2. 「M」CommonJS 通过 require 引入模块、module.export 输出对象和接口。运行时加载，输出值的拷贝；
  3. 「M」ESM 通过 import 引入模块，export 输出模块；编译期输出接口，输出值的引用；浏览器支持原生 ESM ，但只能在 `<script type="module" />` 内使用；
  4. [S] AMD 和 CMD 均为异步加载模块，分别由 require.js 和 sea.js 提供实现；AMD 依赖前置，CMD 就近依赖；
  5. [S] UMD 是对 CommonJS、AMD 的整合；
- JavaScript 这门语言是否有反射能力？ES6 为了增强这种能力又推出那些新特性？
  - `#精通#` `#编程范式#` `#元编程#` `#反射#` `#Proxy#` `#Reflect#` `#数据劫持#`
  1. [S] 反射是实现元编程的一种方式；JS 诞生之初就有反射能力；eval、Object.{create|defineProperties|defineProperty}、Function.{apply|bind} 均属于反射的一些实现；
  2. [S] ES6 Proxy & Reflect 作为反射的两个分支（Self-Modification & Intercession）实现；defineProperty 数据劫持有缺陷；规范语言，对之前 Object & Function 原型链上的方法进行规范化；
  3. [S] 为 JS 之后更多的反射行为提供良好支撑；
  4. [P] ES7 推出了 Reflect MetaData 提案，增强了反射覆盖场景；
- 简单描述闭包及其使用场景？
  - `#熟练#` `#语言特性#` `#模块化#`
  1. [M] 指有权限访问另外一个函数作用域中变量的函数；其本质是作用域链的特殊应用；
  2. [S] 创建私有变量；通过闭包对上下文中变量的引用，防止其被 GC 回收（易引发内存溢出）；

### ECMAScript

- ECMAScript2017（ES8） 中新增的 Symbol 有何用处？
  - `#熟练#`
  1. [M] 用来表示一个独一无二的变量防止命名冲突
- ECMAScript2015（ES6） 之后的版本有那些新特性？
  - `#熟练#` `#语言特性#` `#ESNext#`
  1. [S] ES7：Reflect MetaData（提案）、Array includes、`**`运算符；
  2. [S] ES8：async&await、Object values|entries、String padding、Object.getOwnPropertyDescriptors、SharedArrayBuffer；
  3. [S] ES9：异步迭代、Promise.finally、正则；
  4. [S] ES10：Array flat、String trim 函数、Symbol Description、catch 绑定、Function toString 支撑转注释、BigInt；
  5. [M] ES11：Option Chaining(`?.`)、Nullish Coalescing(`??`)、Private Fields(`#`)、Top Level Await、Dynamic Import、globalThis；
  6. [S] ES12：String replaceAll、Promise.any、`??= ||= &&=`、WeakRefs、`123_456_789` 数字分隔符；
- ECMAScript Next（ESNext）中的新特性？
  - `#精通#` `#ECMA#` `#ESNext#` `#前沿#` `#语言新特性#`
  1. [S] Class instance fields、Static class fields、Private instance methods、Private instance fields、Private static methods、Private static fields、Ergonomic brand checks、Import assertions、Class static blocks
  2. [P] Hashbang grammar、Top-level await、Arbitrary module namespace identifiers、
- 简单列出目前 ECMAScript 处于 Stage（4 & 3 & 2） 阶段的提案？
  - `#精通#` `#ECMA#`
  1. [P] Error Cause（首个由中国团队”阿里淘宝”提出并进入 state-4 阶段的提案）
  2. [P] ESNext：Record、Tuple

### TypeScript

- 简单描述下 TypeScript 在项目中的作用？
  - `#了解#`
  1. [M] 是 JS 的超集，可以提前体验 ES Next 提案中的语法糖和特性
  2. [M] 为 JS 添加类型支撑、JS 的语言超集、利于团队协作；极其强大的类型系统
- 简单描述下 TypeScript 中常用的工具类型？
  - `#了解#`
  1. [S] `Partial<T>` `Required<T>` `Readonly<T>` `Pick<T, K>` `Omit<T, K>`
- 简单描述下 tsconfig.json 中常用的配置项？
  - `#熟练#`
  1. [M] `compilerOptions.targer` `module` `lib` `outDir` `types` `paths` `sourceMap` `include` `exclude`
- TypeScript 是名义类型还是结构类型？
  - `#熟练#`
  1. [S] 结构类型
- 简单描述下 TypeScript 中 Interface 和 Type 的区别？
  - `#熟练#`
  1. [M] 均支持拓展（extends），interface 使用 `extends` 而 type 使用 `&` 类型合并；支持互相拓展；
  2. [S] type 支持类型别名，联合类型，元组；interface 支持声明合并；在使用过程中尽可能先使用 interface；

### HTML

- 简单列出项目中 HTML 常用的 Meta 标签？
  - `#了解#` `#浏览器#` `#HTML#`
  1. [M] `<meta charset="utf-8" />`
  2. [S] SEO 优化 `<meta name=“description" contents=“xx,xx”/>`
  3. [S] SEO 优化 `<meta name=“keywords" contents=“xx,xx”/>`
  4.
- 简单列出项目中 HTML 常用的 Link 标签？
  - `#了解#` `#浏览器#` `#HTML#`
  2. [M] `<link rel="shortcut icon" type="image/x-icon" href="..">`
  3. [M] CSS 外链 `<link rel="stylesheet" href="...">`
  4. [S] 域名 DNS 预请求 `<link rel="dns-prefetch" href="..." />`
- 简单描述下 DOM 和 BOM 对象？
  - `#了解#` `#浏览器#` `#宿主对象#`
  1. [M] DOM 是文档对象模型，把文档当做为一个对象，定义和处理文档内容的方法和接口；比如 `document`
  2. [M] BOM 对浏览器对象模型，将浏览器作为一个对象，定义和处理与浏览器交互的方法和接口；比如 `window` `location` `navigator` `screen`
- 简单描述下事件委托，及其优势和运用场景？
  - `#熟练#` `#浏览器原理#` `#事件#`
  1. [M] 利用浏览器事件冒泡机制；在父节点定义监听事件，由父节点监听函数统一处理多个子元素冒泡传过来的事件；
  2. [S] 减少内存消耗，实现事件的动态绑定；常常运用在各种 UI 事件绑定类库和数据埋点；

### CSS

- 常用单位以及其区别？

  - `#了解#`

  [M] px、em、rem、%、vw、vh

2. [M] px 为屏幕的像素点，em 是父元素的 font-size（默认 16px），vw 为视窗宽度的 1%，vh 为视窗高度的 1%；

- 常用的 CSS 预处理库？
- `#了解#`

1. [M] Less、Sass
2. [P] PostCSS、Stylus

- Less & Sass(SCSS) 的区别和各自的优缺点？
- `#了解#`

1. [M] 区别：在与变量的声明、实现方式（语言不同，Less 基于 JS，Sass 基于 Ruby，当然也有 node-sass 的实现）
2. [S] Less 兼容性好，但是不支持循环判断等；Sass 用户基础大，支持函数对象循环判断等，但是依赖于 Ruby 安装容易报错；

- 常用的 CSS 架构、规范？
- `#熟练#`

1. [S] BEM、CSS Modules

- 常用的 CSS in JS？
- `#熟练#`

1. [S] styled-components、TailwindCSS

- 通用的浏览器 CSS 差异标准化方案？
- `#熟练#` `#兼容性#` `#初始化#`

1. [S] 引入 normalize.css 或者 reset.css

---

## 框架&环境（Frame & VM）

### 浏览器

- 浏览器事件触发时，其传播的阶段？
  - `#了解#`
  1. [M] Capturing（捕获） > Target（目标触发） > Bubbling（冒泡）
- Cookie、localStorage 以及 sessionStorage 之间的区别？
  - `#了解#`
  1. [M] Cookie：保存在客户端的数据，记录你在网页的一些行为数据。 sessionStorage：保存在客户端的数据，生命周期是同源同窗口，只要该窗口没有关闭就一直可用共享。 localStorage：保存在客户端的数据，一直有效；
  2. [S] Cookie size <= 4Kb；Storage size <= 5Mb；
- 浏览器出于安全提出了同源策略，何种情况下会引发跨域以及通用解决办法？
  - `#了解#`
  1. [M] 域名、子域名、端口号、协议不同均不属于一个域；
  2. [S] jsonp、documents.domain + iframe、CORS、iframe + postMessage、websocket；
  3. [S] 处于一级域名下的应用可以设置 document.domain 在相同父域，可以获取 cookie；
- 简单说明 JSONP 的原理，及其局限性？
  - `#了解#`
  1. [M] 利用了`<script>`标签没有跨域限制，可以发起 get 请求；
  2. [S] 兼容性较好，但仅限于 Get 请求；
- 简单描述下浏览器的渲染机制？
  - `#熟练#`
  1. [S] 处理 HTML 文档构建 DOM 树、处理 CSS 文档构建 CSSOM 树、DOM 与 CSSOM 合并为渲染树；
- 简单描述下浏览器的缓存机制？
  - `#熟练#`
  1. [S] 浏览器缓存分为强缓存和协商缓存；
  2. [P] 强缓存直接从浏览器中获取资源，通过请求头 `Cache-Control` 控制；协商缓存先访问服务缓存是否过期，在决定是否使用本地资源，通过请求头控制；

### 研发工具

- 如何将项目的格式化进行统一？
  - `#熟练#`
  1. [S] 使用 .editorconfig 定义代码格式化风格；或者提交 .vscode settings.json 约束项目；
- 常用的 VS Code Editor 配置？
  - `#熟练#`
  1. [S] .vscode 文件下通常使用 extensions.json 声明项目依赖插件；launch.json 配置 Debug 相关的配置；settings.json 用来覆盖本地用户的基本配置（文件隐藏、文件编码、格式化风格）

### 容器

---

## 类库&生态（Libs & Ecosystem）

### React

- React 在 16.x 具体推出那些新特性？
  - `#熟练#`
  1. [M] (16.1) render 返回新增支持字符串和数组类型、Error Boundaries、React Dom Portal、Fiber、React.Fragment
  2. [M] (16.3) createContext、createRef、forwardRef、生命周期函数更新
  3. [M] (16.6) React.memo、React.lazy、React.Suspense、static getDerivedStateFromError、
  4. [M] (16.7) React Hooks（useState、useEffect、useMemo、useCallBack、useContext）
  5. [M] (16.8) React Concurrent Rendering
- React 在 17.x 推出的新特性？
  - `#熟练#`
- React 在目前的 18.x 推出的新特性？
  - `#熟练#`
- 简单说明下为何两个不同版本的 React 不能运行在一个全局上下文？
  - `#熟练#`

### Ecosystem

- React 运行时生态类库？
  - `#熟练#` `#Ecosystem#` `#初始化#`
  1. [M] Official：react、react-dom、react-update、react-refresh、react-reconciler
  2. [M] State & Flow：@reduxjs/toolkit、redux、redux-saga、mobx、iflux2 & plume2、dva
  3. [M] Hooks：ahooks、react-use、react-query
  4. [M] UI：antd、rc-\*(antd core)、antd-mobile、antd-pro
  5. [M] Styles：styled-components、classnames
  6. [M] Router：react-router、react-router-dom、redux-router
  7. [S] Framework：umi
  8. [S] CLI & Layer：vite、create-react-app
  9. [S] Analytics：react-ga、@sentry/react
  10. [S] Draggable：react-dnd、react-draggable
  11. [S] Charts：echarts、AntV
  12. [P] SSR & SSG：next.js、gatsby
  13. [P] I18n：react-intl
  14. [P] Async Load：react-loadable、react-script
  15. [P] Long List：react-virtualized、react-windows、react-scroll、react-infinite-scroller
  16. [P] Docs：storybook、huge
- Taro 生态类库？
  1. Official：@tarojs/ taro、@tarojs/ runtime、@tarojs/ react、@tarojs/ components
  2. [M] Tracing：umtrack-alipay、umtrack-wx
  3. [M] CLI：@tarojs/ cli、@tarojs/ mini-runner、@tarojs/ plugin-inject、@tarojs/ webpack-runner
- Electron 生态类库？
  1. [M] Official：electron、electron-log
  2. [M] Release & Deploy：electron-builder、electron-packager、electron-updater、electron-reload、electron-notarize
  3. [M] Development：electron-debug
  4. [S] Compiler：electron-rebuild、node-gyp
  5. [M] System：getmac、systeminformation、ip
  6. [S] Devices：usb、escpos
  7. [S] Version Manage：semver
- React Native 生态类库？
  1. [M] Official：react、react-native
  2. [M] Navigator：react-navigation、native-navigation
  3. [M] Data Storage：realm、sqlite3、react-native-storage
  4. [M] Scrollable：react-native-scrollable-tab-view、
  5. [M] Devices：react-native-camera
  6. [M] Logs：
  7. [M] UI：ant-design-mobile
  8. [M] Performance：sentry、
  9. [M] Debugging：chrome-dev-tools、flipper
  10. [M] Testing：enzyme、detox、jest
  11. [S] Notification：jpush
- CSS 类库（CSS Tools）？
  1. [S] Resets：normalize.css、reset.css、reset-css
  2. [S] Animate：animate.css
  3. [S] Charts：charts.css
  4. [S] Productor：ant.design、semi.design
- 前端项目运行时生态类库？
  1. [S] Validator：joi、async-validator、yup
  2. [S] Testing：mocha、jest、cypress、enzyme
  3. [S] Assertion：chai
- 前端项目开发时生态类库？
  1. [M] Request：axios、isomorphic-fetch
  2. [M] Polyfill：core-js
  3. [S] Data：immutable、immer、deepmerge
  4. [M] Date：moment、day.js
  5. [S] Testing：jest、mocha、jasmine
  6. [S] Assertion：chai、assert
  7. [S] Utils：lodash、underscore
  8. [S] E2E：cypress、enzyme
  9. [S] Command：commander
- 前端项目编译时生态类库？
  1. [S] Compiler：babel、tsc、esbuild
  2. [S] Bundled：webpack、rollup、parser
  3. [S] Unbundled：snowpack、vite
  4. [S] Mangler & Compressor：terser、javascript-obfuscator、uglify-js、babel-minify
  5. [S] CLI & Boilerplate：create-react-app、vite

### 数据流

- 简单描述下单向数据流（flux）？
  - `#熟练#`
- 如何简单实现一个不可变数据类型？
  - `#熟练#`
  1. [M] 采用 ES6 Proxy & Reflect 代理 get | set | apply 行为，以及 DeepCopy

### SSR & SSG

- CSR、SSR、BSR 以及 SSG 之间的区别与优劣？
  - `#了解#` `#SEO#` `#前后端同构#` `#白屏#` `#性能优化#`
  1. [M] CSR（Client Side Rendering）客户端渲染；
  2. [M] SSR（Server Side Rendering）服务端渲染；
  3. [M] SSG（Static Site Generation）静态站点生成；
- 有那些常用的 SSR & SSG 框架，如何简单实现 SSR？
  - `#熟练#`
  1. [S] Next.js、Gatsby

### Node BFF

- 简单描述下对 Egg 的理解？
  - `#了解#`
  1. [M] Egg 是已 Koa 为内核，遵循约定大于配置的 Web 框架；所有功能基于插件形式完成拓展；
- 简单描述下 Koa 洋葱模型的实现原理？
  - `#熟练#`
- 简单描述下 Egg Loader 的加载顺序？
  - `#熟练#`
  1. [M] framework > middleware > plugin > app（router > service > controller）
- NestJS 中 IoC 的实现机制？
  - `#熟练#`
  1. [M] 基于 reflect-metadata 的提供的 definedMetadata | getMetadata & Decorator 的能力对类、类的成员、类的方法、类方法参数进行的注释；并在编译器提取了对应 meta 信息并实例化 ；

---

## 跨端技术

### 微信小程序

- 简述一下常用的生命周期
  - `#了解#`
  1. [M] onLoad：页面加载，调一次；onShow：页面显示，每次打开页面都调用；onReady：初次渲染完成，调一次；onHide：页面隐藏，当 navigateTo 或底部 tab 切换时调用；onUnload：页面卸载，当 redirectTo 或 navigateBack 时调用；
- 简单描述下小程序的工作原理？
  - `#熟练#`
  1. [S] 小程序分为两个部分 webview 和 appService，webview 用来展现 UI，appService 用来处理业务逻辑、数据及接口调用，它们在两个进程中运行，通过系统层 JSBridge 实现通信，完成 UI 渲染、事件处理。
- 小程序双线程架构原理？
  - `#精通#`
  1. [S] 小程序应用是基于双线程模型的，渲染层通过 Webview 作为渲染载体；逻辑层则通过 JsCore 来作为 JS 运行时；

### 多端统一

- 简单描述下 Taro3.0 原理？
  - `#熟练#`
  1. [S] Taro3.0 从编译型转向了运行时架构
  2. [S] 在运行时模拟实现了 DOM、BOM API，使得前端架构可以运行在小程序运行时环境中

### Node

- require 的模块加载机制？
  - `#熟练#`
  1. [M] 先计算模块路径；如果模块在缓存里面，取出缓存；加载模块的输出模块的 exports 属性即可
- 线上如何排查问题？
  - `#熟练#`
  1. [M] Sentry 监控；
  2. [S] 全链路式日志，需要借助 apm 工具，opentracing，zipkin 等；
  3. [S] 阿里云 alinode；

### Electron

- 简单描述下对 Electron 的理解？
  - `#了解#`
  1. [S] Electron 是一个可以使用 Web 技术（JS、HTML、CSS）来创建跨平台原生桌面应用的框架。借助 Node API 可以使用纯 JS 来调用丰富的原生 API。
- 简单描述下 Electron 的进程模型和以及各自的职责？
  - `#了解#`
  1. [S] Main Process 主进程：进程间通信（IpcMain、webContent）、窗口管理、Node Add-on 暴露、全局事务（应用生命周期、session）；
  2. [S] Renderer Process 渲染进程：负责 web 页面容器构建渲染、业务处理；
- 解释下 Electron 构建时为何需要 Rebuild？
  - `#熟练#`
  1. [P] Electron 内置了 V8 和 Node，而部分 Node 能力是通过 C++ Add-on 实现的；在构建 Electron 应用时，需要针对这些 Add-on 按 Node 版本、Electron 版本、OS Platform、CPU Arch 重新进行编译；

### Native

### Hybrid Web APP

- 如何解决移动端 Web 点击时间的延迟？
  - `#了解#`
  1. [M] `<meta />` 标签禁用网页缩放、FastClick

---

## 研发链路（Lint & Compile & Builder & Package）

### 初始化

- 如何重装 Node 环境（以 Mac 环境为例）？
  1. [P] 借助 npkill 对本地 node_modules 进行清理

### 包管理

- 简单列出一些常用的 CLI 工具或者 Boilerplate？
  - `#熟练#`
  1. [S] create-react-app、vite
- 简单列出常用的包管理工具？
  - `#熟练#`
  1. [M] npm（.npmrc、.npmignore、package.json、package-lock.json）、yarn（.yarnrc、yarn.lock）、pnpm（pnpm-lock.yaml）、tnpm；
  2. [S] nvm、npx（npm 5.2+ 内置；相当于提供两个 bin）
- 简单列出常用的 NPM 命令？
  - `#熟练#` `#工程化#` `#脚手架#` `#命令行#`
  1. [M] `npm i|install|uninstall` `npm run` `npm help` `npm init` `npm publish|unpublish` `npm start|restart` `npm info` `npm list` `npm view|version`
  2. [S] `npx` `npm config` `npm link` `npm rebuild` `npm clean` `npm run-script` `npm whoami` `npm login|logout` `npm docs` `npm adduser`
  3. [S] run-scripts hook `pre & post`
- 简单描述下 NPM 安装依赖的大致过程？
  - `#熟练#`
  1. [S] 检查配置（项目 .npmrc、全局用户 .npmrc）;
  2. [S] 确定依赖版本，构建依赖树；package.json 优先 package-lock.json；
  3. [S] 下载包资源；首先查询本地是否存在缓存版本，如没有则下载并添加本地缓存，并将包解压到项目 node_modules 下；
  4. [S] 生成 lockfile 文件（npm 5.x+）；
- 简单描述下 NPX 的大致流程？
  - `#熟练#` `#脚手架#` `#命令行#`
  1. [M] `npx` 命令是 `npm i xx --global & .bin/xx` 的快捷方式
- NPM Package Version 遵循了什么协议，并简单说明该协议？
  - `#熟练#`
  1. [M] 遵循了 SemVer2.0 协议规范；x.y.z-{pre-release}；
  2. [S] `{major}.{minor}.{patch}` Major 表示不兼容的修改，Minor 表示向下兼容的新增特性，Patch 表示向下兼容的问题修复；
  3. [P] NPM 命令在不满足 SemVer2.0 规范的 Package.json 下无法执行；
- 公共类库如何处理即将弃用的功能（API、组件、模块、依赖）？
  - `#熟练#` `#组件化#` `#开源项目#`
  1. [M] 更新说明文档以及类型描述文件让使用者知道这个 Break Change；
  2. [S] 在某个阶段的 Minor 版本持续进行 Warning 级别提示（一般跨域一整个 Major），然后在下个 Major 版本移除；
- 封装一个类库时应该遵循哪条基本原则？
  - `#熟练#` `#开源项目#`
  1. DRY

### 规范标准

- JavaScript 基本编码规范
  - `#熟练#` `#代码洁癖#` `#强迫症#`
  1. [M] `=== !==` 代替 `== !=`；不要在对象原型（`Array.prototype|Date.prototype`）上添加自定义方法；for | if 语句使用大括号；代码中的地址时间等使用常量替代；不使用 `var` 声明变量；
  2. [M] 使用大驼峰法对组件&类命名，使用小驼峰法来对变量&函数名命名

### 调试

- H5 页面的调试手段？
  - `#了解#`
  1. [M] 微信开发者工具
  2. [S] vsconsole

### 编译&构建

- 前端项目常用构建工具
  - `#了解#`
  1. [M] Webpack、Babel；
  2. [S] Vite、Parcel、Rollup、TSC；
  3. [P] EsBuild、Snowpack；
- Webpack 基本原理以及构建流程
  - `#熟练#` `#实现原理#`
  1. [M] Webpack 是一个静态模块打包工具；讲所需要的模块组合成一个或多个 bundles 用与浏览器、Node 或者 Electron 使用；
  2. [S] 代码字符串 > AST > Transform > AST(Low) > 代码字符串；
- 简单描述下 Vite 的特性原理，为何快？
  - `#熟练#` `#实现原理#`
  1. [S] Vite 在开发时采用 Esbuild 作为 模块构建器

### 测试

- 常用的测试框架？
  - `#了解#`
  1. [M] UT：Jest、Mocha
  2. [S] E2E：Selenium、Cypress、Puppeteer

### 发布

- 前端项目如何构建一个标准包？
  - `#了解#`
  1. [S] 在配置的依赖均倒置，运行时通过宿主来提供环境注入（global 对象、script 提供 config）；

### 监控

- 简单列出常用的前端数据监控的类库？
  - `#了解#`
  1. [S] @sentry/react、fundebug、ARMS、umeng
- 简单描述下前端数据采集及其基本原理？
  - `#了解#`
  1. [S] 数据采集通常分为：环境信息、性能信息、异常信息、业务信息（交互数据、业务异常）
  2. [S] 事件委托

---

## 性能&安全（Performance & Security）

### 性能指标

- 简单列出常用的前端 Web 应用的性能指标？
  - `#熟练#`
  1. [S] First Contentful Paint(FCP) 首次内容绘制、Largest Contentful Paint (LCP) 最大内容绘制、First Input Delay(FID) 首次输入延迟；
  2. [P] First Paint(FP) 首次绘制、First Meaningful Paint(FMP) 首次有效绘制、Cumulative Layout Shift(CLS) 累积布局偏移、Time to Interactive(TTI) 可交互时间、DOMContentLoaded(DCL)、Load(L)；
- 简单描述下性能指标的采集原理（exp. FCP、LCP、FID）？
  - `#精通#` `#性能优化#` `#实现原理#`
  1. [S] 通过 Performance Observer API 采集；
  2. [S] 性能监测相关 API：Paint Timing、Event Timing、Navigation Timing、Paint Timing；

### 性能评估

- 简单列出常用的 Web 应用性能评估（采集）工具？
  - `#了解#`
  1. [M] Chrome DevTools、React DevTools
  2. [P] Lighthouse、WebPageTest、Relyzer
- 如果使用 React 开发的页面响应慢，有那些检测手段？
  - `#了解#`
  1. [M] console.time、timeEnd 埋点
  2. [M] 借助 React DevTools 可以查看每个组件的渲染和重绘耗时

### 性能优化

- 常用的性能优化手段？
  - `#熟练#`
  1. [M] 代码压缩：Code Splitting、Tree-Shaking、Gzip
  2. [M] 修改加载策略
  3. [M] 执行自定义渲染
  4. [S] 体验优化（加载动画、骨架图）
  5. [S] DNS 预获取
- 常见的 JS 代码压缩工具及其简单原理？
  - `#熟练#` `#性能优化#` `#页面优化#` `#构建优化#`
  1. [M] uglifyjs、terser
- 简单描述下 Tree-Shaking 及其原理和使用建议？
  - `#熟练#` `#性能优化#` `#页面优化#`
- 常见的 JS 延迟加载方式？
  - `#熟练#`
  1. [M] `<script defer/>` defer 属性、`<script async />` async 属性、动态创建 DOM、使用 setTimeout 延迟、JS 写在 DOM 文档底部
- 微信小程序常用的优化手段？
  - `#熟练#`
  1. [M] 代码包大小优化分包，独立包，分包预下载；
  2. [M] 首页渲染优化，预加载，骨架图避免白屏；
  3. [M] 渲染优化，setData 增量更新，延迟加载，避免一个原子操作大量计算阻塞 ui；
- 如何优化一个前端巨石应用（）；
  - `#熟练#` `#前端架构#` `#性能优化#`
  - [M] Code Splitting、Lazy Loader；
  - [S] 微前端架构；

### 源码安全

- 保护前端 JS 的源码的常见手段？
  - `#熟练#`
  1. [M] 代码压缩（uglifyjs）；
  2. [M] 生产环境不得上传 SourceMap；
  3. [S] 代码混淆 （Terser）；
- CSRF / XSRF（跨站请求伪造）
  - `#熟练#`
  1. [S] HTTP 协议中使用 Referer 属性来确定请求来源进行过滤（禁止外域）
  2. [S] 请求地址添加 token ，使黑客无法伪造用户请求
  3. [S] HTTP 头自定义属性验证（类似上一条）
  4. [S] 敏感操作显示验证方式：添加验证码、密码等

### Web 安全

---

## 工程化

### 工程体系

- 前后端分离的本质？
  - `#熟练#`
  1. [M] 职责分明，将服务端业务逻辑和前端视觉进行分离，互设边界；
  2. [M] 前端项目越来越复杂，需要规范流程和引入标准的工程体系。

### 微前端

- 业界常用的微前端框架？
  - `#了解#` `#前端框架#`
  1. [M] single-spa、蚂蚁 qiankun.js
  2. [S] 京东 micro-app、字节 garfish
  3. [P] modern.js、magix、飞冰 icestark、WidgetJS、ara framework、luigi、emp
- 简单描述下 Qiankun 的工作原理？
  - `#熟练#`
  1. [M] single-spa、蚂蚁的 qiankun.js
- Qiankun 的子应用配置，为何需要构建 UMD 包？
  - `#熟练#`
  1. [M] 子应用 webpack entry 提供 `target:umd` 以及
  2. [S] 子应用
- 微前端框架常用的 CSS 隔离方式？
  - `#熟练#`
  1. [P] 自定义标签，以及标签 name 配合选择器

### 低代码

- 简单描述下对 JSON-Schema 协议的理解？
- 如何处理表单的关联逻辑？

### Bundleless

### CI\CD

- 简单列出前端常用的构建平台？
  - `#了解#`
  1. [M] Jenkins、Travis CI

### 综合能力
