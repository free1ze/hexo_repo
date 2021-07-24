---
title: venv 笔记
date: 2021-01-12 00:41:52
tags:
---

 venv-----用来建立一个虚拟的python环境，一个专属于项目的python环境。用venv 来保持一个干净的环境非常有用.

<!--more-->

在学习过程中，经常需要尝试某些软件，但又经常碰到安完了难以卸载/环境配置不兼容/想胡求搞完一删的情况。这时候就需要虚拟环境venv。

  

## 1、基本使用

在当前目录创建虚拟环境

```python3
python -m venv my_env
```

激活虚拟环境

```python3
cd my_env
scripts\activate #注意斜线方向！
```

退出当前的`venv`环境，使用`deactivate`命令：

```bash
deactivate
```

删除虚拟环境

```python3
$ rm -rf venv my_env
```

## 2.原理解释

virtualenv是如何创建“独立”的Python运行环境的呢？

原理很简单，就是把系统Python复制一份到virtualenv的环境，用命令`source venv/bin/activate`进入一个virtualenv环境时，virtualenv会修改相关环境变量，让命令`python`和`pip`均指向当前的virtualenv环境。



virtualenv和venv使用细节略有不同，但功能大致相同。

