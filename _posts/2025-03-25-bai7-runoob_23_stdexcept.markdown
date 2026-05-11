---
layout: post
title: runoob_23_stdexcept
date: 2025-03-25 10:53:00 +0800
description: runoob_23_stdexcept
img: post-4.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 17:16:03
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 17:16:12
     * @FilePath: /cxx_stl/runoob_23.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-stdexcept.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <stdexcept>
    void riskyFunction(int x) {
        if (x < 0) {
            throw std::invalid_argument("Negative value not allowed");
        }
        std::cout << "Processing " << x << std::endl;
    }
    int main(int argc, const char** argv) {
    
    /***
        <stdexcept> 头文件定义了以下异常类：
        std::exception：所有标准异常类的基类。
        std::bad_exception：当异常处理过程中发生错误时抛出。
        std::bad_alloc：当内存分配失败时抛出。
        std::bad_cast：当类型转换失败时抛出。
        std::bad_typeid：当 typeid 操作失败时抛出。
        std::logic_error：当逻辑错误发生时抛出，例如无效的输入参数。
        std::domain_error：当函数调用的参数不在有效范围内时抛出。
        std::invalid_argument：当函数调用的参数无效时抛出。
        std::length_error：当容器操作因为长度限制而失败时抛出。
        std::out_of_range：当访问容器的非法索引时抛出。
        std::overflow_error：当算术运算导致溢出时抛出。
        std::range_error：当函数返回值不在期望的范围内时抛出。
        std::underflow_error：当算术运算导致下溢时抛出。
    */
    
    
        try {
            riskyFunction(-1);
        } catch (const std::invalid_argument& e) {
            std::cerr << "Caught an exception: " << e.what() << std::endl;
        }
        return 0;
    }
    
