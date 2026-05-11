---
layout: post
title: runoob_21_type_traits
date: 2025-03-25 10:52:00 +0800
description: runoob_21_type_traits
img: post-2.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 17:01:21
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 17:02:58
     * @FilePath: /cxx_stl/runoob_21.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-type_traits.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <type_traits> // 包含了一组编译时检查类型特性的工具,可以用于查询和操作类型属性
    int main(int argc, const char** argv) {
        std::cout << "int is integral: " << std::is_integral<int>::value << std::endl;
        std::cout << "float is integral: " << std::is_integral<float>::value << std::endl;
        std::cout << "char is integral: " << std::is_integral<char>::value << std::endl;
        int a = 10;
        int* p = &a;
        std::cout << "int* is a pointer: " << std::is_pointer<int*>::value << std::endl;
        std::cout << "int is a pointer: " << std::is_pointer<int>::value << std::endl;
        return 0;
    }
    
