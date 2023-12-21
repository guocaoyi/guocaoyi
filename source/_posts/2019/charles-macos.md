---
layout: post
title: Charles macOS 抓包实践
date: 2019-07-15
tags:
  - os
  - charles
---

# Charles macOS 抓包实践

> Tag：Proxy、macOS、iOS、WeChat Client、微信公众号文章

[MAC版:Charles根证书(Charles Root Certificates)的安装\_Cyangdaowei的博客-CSDN博客\_mac安装Charles证书](https://blog.csdn.net/Cyangdaowei/article/details/119362002)

## 准备

- Charles

```bash
brew install --cask charles
```

- 信用证书
- 桌面端应用（浏览器或者客户端）
- 移动端设备 & 应用

<!-- more -->

## Mac 应用设置步骤

- 1. 证书下载
  - Charles > Help > SSL Proxying > Install Charles Root Certificate
- 2. 添加证书
- 3. Mac 证书信任设置（默认不受信任，请求无法拦截）
  - 打开证书，在 Trust 一列（使用此证书时），设置为始终信任
- 4. Charles 设置 SSL Proxying
  - Charles > Proxy > SSL Proxying Settings
  - Enable SSL Proxying
  - Include add a location (host = `*` port = `443`)

## iOS 设备设置步骤

在 **Mac 应用设置步骤的第 3步后**，加入下步骤

- Charles 证书安装到移动设备上
  - Charles > Help > SSL Proxying > Install Charles Root Certificate on a Mobile Device or Remote Browser
- 移动设备信任 Charles 证书

## 测试

1. 使用 Charles 抓取 微信桌面客户端中公众号历史文章列表；
2. 通过 Charles 代理，查看手机微信公众号历史文章列表；
