---
layout: post
title: Python数据分析
date: 2017-08-28 00:00:00 +0800
description: 介绍 Python 数据处理常用技巧，包括数组解压、定长列表、元素查找、多值映射、有序字典和字典运算。
img: post-2.jpg
tags: [segmentfault, python]
author: Bai Qi
---

Python 作为弱类型语言，虽身带高效开发的 BUFF，但同时也有着不出众的运行性能。因为每次变量操作后解释器需重新判断数据类型，这会增加负担。NumPy 因此诞生，底层代码用 C 编写，运行性能不错，在数据分析、机器学习等领域应用广泛。

在介绍 NumPy 之前，先补充几项 Python 数据处理技巧：

## 1. 数组解压（Array Unpacking）

可以用多个变量同时接收一个列表或元组的元素。使用星号加变量名可将多余元素聚合成一个列表，星号变量总是在最后被分配。

例如，对于字符串 `By777:20:Python:Linux:Web`，可用以下方式提取信息：

```python
name, age, *tools = str.split(':')
# name = "By777"
# age = "20"
# tools = ["Python", "Linux", "Web"]
```

## 2. 定长列表（Fixed-Length List）

通过 `collections.deque` 实现，可设置最大长度。当元素超过限制时，新加入的元素会将最旧的元素"挤出"。

```python
from collections import deque

dq = deque(maxlen=10)
for i in range(12):
    dq.append(i)
# deque([2, 3, 4, 5, 6, 7, 8, 9, 10, 11])
```

还可用 `appendleft` 方法逆向构建。

## 3. 元素查找（Element Lookup）

借助 `heapq` 库，使用 `nlargest` 可提取序列中最大的若干元素。还可以传入 `key` 参数自定义排序依据函数。

```python
import heapq

nums = [1, 8, 2, 23, 7, -4, 18, 23, 42, 37, 2]
heapq.nlargest(3, nums)  # [42, 37, 23]

# 自定义排序依据
heapq.nlargest(3, nums, key=lambda x: x**0.5 if x > 50 else x)
```

## 4. 多值映射（Multi-Value Mapping）

用 `collections.defaultdict` 可构建默认值为列表或集合的字典，从而使一个键对应多个值。

```python
from collections import defaultdict

d = defaultdict(list)
d['a'].append(1)
d['a'].append(2)
# d = {'a': [1, 2]}

d_set = defaultdict(set)
d_set['a'].add(1)
d_set['a'].add(2)
# d_set = {'a': {1, 2}}
```

## 5. 有序字典（Ordered Dictionary）

`OrderedDict` 会按键的添加顺序保持排列，而原生的 `dict` 则不保证顺序。

## 6. 字典运算（Dictionary Operations）

字典与 OrderedDict 不能直接做数学运算，需通过 `items()`、`keys()` 等方法实现。

```python
# 找出仅存在于前者的键值对
d_cm.items() - od.items()

# 找出最小值对应的键
min(d_cm, key=lambda k: d_cm[k])

# 用 zip 配合 min 实现
min(zip(d_cm.values(), d_cm.keys()))
```
