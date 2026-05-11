---
layout: post
title: runoob_31_climits
date: 2017-01-31 11:02:00 +0800
description: runoob_31_climits
img: post-5.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 20:25:52
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 20:27:06
     * @FilePath: /cxx_stl/runoob_31.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-climits.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    
    #include <climits>
    // C++ 标准库中的一个头文件，提供了与整数类型相关的限制和特性。它定义了一组常量，描述了各种整数类型（如 char、int、long 等）的最小值、最大值和其他相关属性。
    //  这些常量来自 C 标准库的 <limits.h> 头文件
    int main(int argc, const char** argv) {
        // 打印整型的最大值和最小值
        std::cout << "int 的最大值是：" << INT_MAX << std::endl;
        std::cout << "int 的最小值是：" << INT_MIN << std::endl;
    
        // 打印长整型的最大值和最小值
        std::cout << "long 的最大值是：" << LONG_MAX << std::endl;
        std::cout << "long 的最小值是：" << LONG_MIN << std::endl;
    
        // 打印无符号长整型的最大值
        std::cout << "unsigned long 的最大值是：" << ULONG_MAX << std::endl;
    
        // 打印字符类型的最大值和最小值
        std::cout << "char 的最大值是：" << CHAR_MAX << std::endl;
        std::cout << "char 的最小值是：" << CHAR_MIN << std::endl;
        return 0;
    }
    
