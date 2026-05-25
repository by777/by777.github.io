---
layout: post
title: runoob_30_cassert
permalink: /runoob/runoob_30_cassert/
date: 2017-01-30 10:57:00 +0800
description: runoob_30_cassert
img: post-6.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 20:24:01
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 20:24:09
     * @FilePath: /cxx_stl/runoob_30.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-cassert.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <cassert> // C++ 标准库中的一个头文件，它提供了断言功能，用于在程序运行时检查条件是否为真
    int main(int argc, const char** argv) {
        int x = 10;
        int y = 0;
    
        // 使用自定义错误信息
        assert(y != 0 && "Division by zero error");
    
        int result = x / y; // 这行代码将不会执行，因为断言已经失败
        return 0;
    }
    
