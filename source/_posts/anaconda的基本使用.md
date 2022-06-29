---
banner_img: /images/uploads/8bae1430db59bca62d3ccda98242f461.jpeg
index_img: /images/uploads/cd05476802a88985d31b554e5be3b5fa.jpeg
title: Anaconda的基本使用
date: 2022-06-29 20:39:40
updated: 2022-06-29 20:39:40
tags:
  - Python
  - Anaconda
categories:
  - Python
comments: true
---


Anaconda是Python第三方ide工具，其集成了一系列的Python优秀的库和工具，其优点有

+ 开源免费的
+ 支持800个第三方库
+ 包含多个主流工具
+ 适合数据计算领域开发
+ 跨平台，Windows、Linux、OS X

## Conda

conda是anaconda的工具之一，其作用有：

+ 用于包管理和环境管理
+ 包管理和pip类似，管理python第三方库
+ 环境管理能允许用户使用不同版本python，并能灵活切换

> anaconda是一个集合，包括conda、某版本python、一批第三方库
>
> conda将工具，第三方库、python版本、conda都当作包同等对待。

在cmd下可以使用`conda --version`获取conda的版本号，使用`conda updata conda`更新conda，也可在anaconda的图形管理界面管理环境和包

## Spyder

非常优秀的python第三方编写、调试工具，窗体包含：

+ 编辑区：用户编写代码的区域
+ 文件导航和帮助：可以查看相关路径的文件信息
+ IPython：对运行结果或运行输入进行相关响应

## IPython

IPython是一个功能强大的交互式shell，适合进行交互式数据可视化和GUI相关应用。

+ 在变量，函数名称后加上`?`可以获得这个变量或函数的通用信息，比如类型，值，描述信息，文件位置，长度，函数源代码等
+ IPython包含了In和Out，两个输入输出字段，后面的方括号代表输入的命令序号
+ IPython使用`%run <filename> `运行python文件，文件路径在IPython目录下可以直接运行，否则需要相对路径
+ IPython的%魔术命令

| 常用命令            | 说明                                      |
| ------------------- | ----------------------------------------- |
| `%magic`            | 显示所有魔术命令                          |
| `%hist`             | IPython命令的输入历史                     |
| `%pdb`              | 异常发生后自动进入调试器                  |
| `%reset`            | 删除当前命名空间中的全部变量或名称        |
| `%who`              | 显示IPython当前命名空间中已经定义的变量   |
| `%time statement`   | 给出代码的执行时间，statement表示一段代码 |
| `%timeit statement` | 多次执行代码，计算综合平均执行时间        |

