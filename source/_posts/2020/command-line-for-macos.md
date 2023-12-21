---
layout: post
title: Command Line for macOS
date: 2020-10-20 09:20:06
tags:
  - os
  - cheatsheet
---

# Command Line for macOS

> 常用命令行

## Folder Operation

```bash
mkdir #创建一个目录
rmdir # 删除一个目录
mvdir # 移动或重命名一个目录
cd # 改变当前目录
pwd # 显示当前目录的路径名
ls # 显示当前目录的内容
dircmp # 比较两个目录的内容
```

## File Operation

```bash
cat # 显示或链接文件
pg # 分页格式化显示文件内容
more # 分屏显示文件内容
od # 显示非文本文件的内容
cp # 复制文件或目录
rm # 删除文件或目录
mv # 改变文件或所在目录
ln # 联接文件
find # 使用匹配表达式查找文件
file # 显示文件类型
open # 使用默认的程序打开文件
```

## Selection Operation

```bash
head # 显示文件的最初几行
tail # 显示文件的最后几行
cut # 显示文件每行中的某些域
colrm # 从标准输入中删除若干列
paste # 横向连接文件
diff # 比较并显示两个文件的差异
sed # 非交互方式流编辑器
grep # 在文件中按模式查找
awk # 在文件中查找并处理模式
sort # 排序或归并文件
uniq # 去掉文件中的重复行
comm # 显示两有序文件的公共和非公共行
wc # 统计文件的字符数、词数和行数
nl # 给文件加上行号
```

## Auth Operation

```bash
passwd #修改用户密码
chmod #改变文件或目录权限
umask #定义创建文件的权限掩码
chown #改变文件或目录的属主
chgrp #改变文件或目录的所属组
xlock #给终端上锁
```

## Programmer Operation

```bash
make #维护可执行程序的最新版本
touch #更新文件的访问和修改时间
dbx #命令行界面调试工具
xde #图形用户界面调试工具
```

## Process Operation

```bash
ps #显示进程当前状态
kill #终止进程
nice #改变待执行命令的优先级
renice #改变已运行进程的优先级
```

## Timing Operation

```bash
date #显示系统的当前日期和时间
cal #显示日历
time #统计程序的执行命令
```

## Network & Socket Operation

```bash
telnet #远程登录
rlogin #远程登录
rsh #在远程主机执行指定命令
ftp #在本地主机与远程主机之间传输文件
rcp #在本地主机与远程主机之间复制文件
ping #给一个网络主机发送回应请求
mail #阅读和发送电子邮件
write #给另一用户发送报文
mesg #允许或拒绝接受报文
```

## Korn Shell Operation

```bash
history #列出最近执行过得几条命令及编号
r #重复执行最近执行过的某条命令
alias #给某个命令定义别名
unalias #取消对某个别名的定义
```

## Other Operation

```bash
uname #显示操作系统的有关信息
clear #清楚屏幕或窗口内容
env #显示当前所有设置过的环境变量
who #列出当前登录的所有用户
whoami #显示当前正在进行操作的用户名
tty #显示冲段或伪终端的名称
stty #显示或充值控制键定义
du #查询磁盘使用情况
df #显示文件系统的总空间和可用空间
w #显示当前系统活动的总信息
```
