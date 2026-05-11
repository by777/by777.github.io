---
layout: post
title: Python数据分析 - numpy
date: 2017-09-27 00:00:00 +0800
description: 介绍 NumPy 在 Python 数据分析中的核心功能，包括数据集操作、多维数组运算和常用方法。
img: post-4.jpg
tags: [segmentfault, python]
author: Bai Qi
---

NumPy 是 Python 数据分析必不可少的第三方库，在一定程度上解决了 Python 运算性能不佳的问题，并提供了更精确的数据类型。NumPy 被其他科学计算包作为基础包，是 SciPy、Pandas 等库最基本的函数功能库。

NumPy 提供的主要功能包括：N 维数组对象 ndarray、广播功能函数、整合 C/C++/Fortran 代码的工具，以及线性代数、傅里叶变换、随机数生成等功能。

## 使用 NumPy 操作数据集

### 什么是维度

维度是一组数据的组织形式，一维数据由对等关系的有序或无序数据构成，可用数组表示。例如 `1, 2, 3, 4` 是一维数据，折叠成两行两列就成为二维数据（矩阵）。

### 什么是数据集

数据集的集合，一般是二维或多维数表。可以手工新建文本文件作为数据集，使用逗号作为分隔符的称为 CSV（逗号分隔值）数据集，类似 Excel 表格。

### 生成数据集

使用 `np.savetxt()` 可将数组写入文件，参数包括文件名、数组、格式（如 `%d`）和分隔符。示例代码生成一个 4×5 矩阵保存为 demo.csv。

### 读取数据集

使用 `np.loadtxt()` 读取 CSV 文件，可指定数据类型和分隔符。

### CSV 文件的局限

只能有效存储一维和二维数组。`tofile()` 和 `fromfile()` 方法会将数组展平为一维，丢失维度信息，需要手动 reshape 恢复。

### 保存/读取高维度数据

`np.save()` 和 `np.load()` 可保存和读取高维度数据，文件扩展名为 `.npy`（压缩版为 `.npz`）。

## 附录：常用方法及注释

### np 数组定义

通过 `np.array()` 创建，可获取 shape（行列）、ndim（维数）、dtype（数据类型）、itemsize（每个元素字节数）、size（元素总数）等属性。

### 初始化数组

`np.zeros()` 和 `np.ones()` 可初始化全 0 或全 1 数组。

### 随机序列

- `np.random.rand()` 生成 0~1 均匀分布随机数
- `np.random.randint()` 生成指定范围内的随机整数
- `np.random.randn()` 生成标准正态随机数
- `np.random.choice()` 从指定序列中随机选取
- `np.random.beta()` 生成 Beta 分布随机数

### 多维数组运算

`np.arange()` 配合 `reshape()` 可生成并重定义数组形状。常用运算包括 `exp`（自然指数）、`sqrt`、`log`、`sin`、`sum`、`max` 等。`sum()` 可通过 axis 参数指定求和维度，axis 值越大运算深入程度越大。

### 相加运算

NumPy 数组支持直接进行元素级加减运算（如 `list1 + list2`），与 Python 原生 list 只能追加不同。矩阵运算可通过 `np.dot()` 实现矩阵乘法。NumPy 数组有明确的数据类型：

| 类型 | 说明 |
|------|------|
| bool | 布尔型 |
| int8/16/32/64/128 | 有符号整数 |
| uint8/16/32/64/128 | 无符号整数 |
| float16/32/64 | 浮点型 |
| complex64/128 | 复数型 |
| string | 字符串 |

维护成本低于原生 list。

## 总结

Python 作为弱类型语言有其不足，而 NumPy 弥补了这些缺点，使其具备了构造复杂数据类型的能力，为 Python 数据分析提供了基础。
