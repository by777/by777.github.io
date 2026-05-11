---
layout: post
title: python map/filter/reduce的用法示例
date: 2024-08-21 14:28:00 +0800
description: python map/filter/reduce的用法示例
img: post-2.jpg
tags: [cnblogs]
author: Bai Qi
---


    from functools import reduce
    
    def func0(a):
        """
        a: 可迭代对象的迭代元素
        将function 应用于可迭代对象的对应元素，并返回一个迭代器，其中包含了所有映射后的结果
        map(function, iterable, ...)
        function：要应用于可迭代对象的函数。
        iterable：要进行映射操作的可迭代对象
        """
        return "❤☆❤" + a + "☆❤☆"
    
    def func1(a):
        '''
        a: 可迭代对象的迭代元素
        用于筛选可迭代对象中满足指定条件的元素，然后返回一个包含筛选结果的新可迭代对象。
        filter(function, iterable)
        function：用于筛选元素的函数，该函数返回 True 或 False。
        iterable：要进行筛选操作的可迭代对象。
        '''
        if(a.startswith('w')):
            return True
        else:
            return False
    
    def func2(a,b):
        """
        a: 可迭代对象的迭代元素
        b: 可迭代对象的下一个迭代元素
        对可迭代对象中的元素进行累积操作，从左到右依次应用指定的函数，将结果汇总为一个值
        functools.reduce(function, iterable[, initializer])
        function：用于累积操作的函数，该函数接受两个参数，并返回一个结果。
        iterable：要进行累积操作的可迭代对象。
        initializer（可选）：累积的初始值。
        reduce() 函数将 function 应用于 iterable 中的元素，从左到右依次累积，将
        结果传递给下一个元素。如果提供了 initializer，它将作为累积的初始值。否则，iterable 的第一个元素将作为初始值。
        """
        return a + ', ' + b
    
    if __name__ == "__main__":
        # 1.map(function, iterable)
        words = ["hello", 'world', "blingbling!"]
        print(list(map(func0, words)))
        
        # 2.filter筛选可迭代对象中满足指定条件的元素，然后返回一个包含筛选结果的新可迭代对象
        print(list(filter(func1, words)))
        
        # 3.reduce 从左到右依次累积
        print(reduce(func2, words))
        
        # ['❤☆❤hello☆❤☆', '❤☆❤world☆❤☆', '❤☆❤blingbling!☆❤☆']
        # ['world']
        # hello, world, blingbling!
    
    
