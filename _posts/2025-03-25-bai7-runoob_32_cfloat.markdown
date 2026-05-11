---
layout: post
title: runoob_32_cfloat
date: 2025-03-25 11:03:00 +0800
description: runoob_32_cfloat
img: post-5.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-25 09:08:23
     * @LastEditors: by777
     * @LastEditTime: 2025-03-25 09:24:49
     * @FilePath: /cxx_stl/runoob_32.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-cfloat.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <cfloat>
    // C++ 标准库中的一个头文件，用于定义浮点数相关的宏和常量。
    // 这些宏和常量提供了关于浮点数表示的精度、范围等信息，
    // 主要来自 C 标准库的 <float.h> 头文件
    using namespace std;
    int main(int argc, const char** argv) {
        std::cout << "float:\n";
        std::cout << "Min: " << FLT_MIN << '\n';
        std::cout << "Max: " << FLT_MAX << '\n';
        std::cout << "Epsilon: " << FLT_EPSILON << '\n';
        std::cout << "Digits: " << FLT_DIG << '\n';
    
        // 输出 double 类型的范围和精度
        std::cout << "\ndouble:\n";
        std::cout << "Min: " << DBL_MIN << '\n';
        std::cout << "Max: " << DBL_MAX << '\n';
        std::cout << "Epsilon: " << DBL_EPSILON << '\n';
        std::cout << "Digits: " << DBL_DIG << '\n';
    
        // 输出 long double 类型的范围和精度
        std::cout << "\nlong double:\n";
        std::cout << "Min: " << LDBL_MIN << '\n';
        std::cout << "Max: " << LDBL_MAX << '\n';
        std::cout << "Epsilon: " << LDBL_EPSILON << '\n';
        std::cout << "Digits: " << LDBL_DIG << '\n';
        return 0;
    }
    
    
