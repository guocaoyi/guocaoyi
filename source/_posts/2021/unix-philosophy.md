---
layout: post
title: Unix 哲学
date: 2021-02-20 12:49:06
tags:
  - article
---

# Unix 哲学

> 拿不准就穷举 — Ken Thompson（Unix \ Go 作者之一）

- 模块原则(Modularity): 写简单的程序，并用好的接口连接它们
- 清晰原则(Clarity): 清楚透明的算法比“高明”的算法更好
- 组装原则(Composition): 写能够跟其他程序一起工作的程序
- 隔离原则(Separation): 分离接口（使用引擎的方法）和引擎
- 简单原则(Simplicity): 尽量简化算法，不到必要的时候不要增加复杂度
- 简约原则(Parsimony): 只要在必要的时候才写大型程序，通常小程序已经足够了
- 透明原则(Transparency): 写容易测试和纠错的代码
- 健壮原则(Robustness): 这是简单和简约的副产物
<!-- more -->
- 表达原则(Representation): 用数据结构表达逻辑，而不是用过程表达逻辑
- 传统原则(Least) Surprise: 用最常识的方法设计借口
- 安静原则(Silence): 如果程序没什么特别事情要表达，应该保持安静！
- 经济原则(Economy): 程序员的时间比机器的时间更加宝贵
- 生成原则(Generation): 尽量写代码来生成代码，而不是手工输入代码
- 修复原则(Repair): 当程序出现异常，应该明确的抛出异常，而且约早越好！
- 优化原则(Optimization): 先让程序工作，在考虑优化的事情
- 多样性原则(Diversity): 一个问题有很多好的解决方案，没有最好的解决方案！
- 拓展性原则(Extensible): 设计程序时应该考虑到未来的拓展，因为未来比你想象来的早
