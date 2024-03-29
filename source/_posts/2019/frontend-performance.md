---
layout: post
title: 前端性能优化
date: 2019-12-21
tags:
  - frontend
---

# 前端性能优化

- 前端性能优化
  - 移动端
    - 保持单个文件小于25KB
    - 打包内容为分段multipar文档
  - 图片
    - 优化图片
    - 优化CSS Sprite
    - 不要在HTML中缩放图片
    - 使用体积小、可缓存的 favicon.ico
  - 渲染层面
    - 服务端渲染的探索和实践
    - 浏览器的渲染机制解析
      - CSS性能方案
      - JS性能方案
    - DOM优化
      - 原理与基本思路
      - 事件循环与异步更新
      - 回流与重绘
    - 首屏渲染提速
      - 懒加载初探
  - 页面内容
    - 减少HTTP请求数
    - 减少DNS查询
    - 避免重定向
    - 缓存Ajax请求
    - 延迟加载
    - 预加载
    - 减少DOM元素数量
    - 划分内容到不用域名
    - 尽量减少iframe使用
    - 避免404错误
  - 服务器
    - 使用CDN
    - 添加Expires或Cache-Control响应头
    - 启用Gzip
    - 配置Etag
    - 尽早输出缓冲
    - Ajax请求使用GET方法
    - 避免图片src为空
  - Cookie
    - 减少Cookie大小
    - 静态资源使用Cookie域名
  - CSS
    - 样式表放在<head/>中
    - 不要使用CSS表达式
    - 使用<link/>替代@import
    - 不要使用filter
  - Javascript
    - 把脚本放在页面底部
    - 使用外部Javascript&CSS
    - 压缩Javascript&CSS
    - 移除重复脚本
    - 减少DOM操作
    - 使用高效的事件处理
  - 网络层
    - 请求过程的优化
      - HTTP请求优化
        - 构建工具性能调优
        - Gzip压缩原理
        - 图片优化
    - 减少网路请求
      - 本地存储（存储篇）
        - 浏览器的缓存机制
        - 利离线存储技术
    - 性能检测
      - 可视化工具
        - Performance
        - LightHouse
      - W3C性能API
