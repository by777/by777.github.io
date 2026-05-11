---
layout: post
title: runoob_26_utility
date: 2017-01-26 10:54:00 +0800
description: runoob_26_utility
img: post-1.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 17:56:04
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 18:15:28
     * @FilePath: /cxx_stl/runoob_26.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-utility.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <vector>
    #include <utility> // 文件定义了多种工具类和函数，它们主要用于简化编程任务，提高代码的可读性和可维护性
    using namespace std;
    
    /*
     *pair：一个包含两个元素的容器，通常用于存储和返回两个相关联的值。
     *make_pair：一个函数模板，用于创建 pair 对象。
     *swap：一个函数模板，用于交换两个对象的值。
     *forward 和 move：用于完美转发和移动语义的函数模板
    */
    void process(int& i) {
        std::cout << "Lvalue reference to " << i << std::endl;
    }
    
    void process(int&& i) {
        std::cout << "Rvalue reference to " << i << std::endl;
    }
    
    template <typename T>
    void forward_example(T&& t) {
        process(std::forward<T>(t));
    }
       
    int main(int argc, const char** argv) {
        
        {
            auto p = std::make_pair(10, 20);
            // 输出 pair 对象的元素
            std::cout << "First element: " << p.first << std::endl;
            std::cout << "Second element: " << p.second << std::endl;
        }
        {
            int a = 5;
            int b = 10;
            std::cout << "Before swap: a = " << a << ", b = " << b << std::endl;
            // 使用 swap 函数交换 a 和 b 的值
            std::swap(a, b);
            std::cout << "After swap: a = " << a << ", b = " << b << std::endl;
        }
        {
            // std::move 将一个对象转换为右值引用（rvalue reference），从而允许移动操作而不是拷贝操作。
            std::vector<int> v1 = {1, 2, 3, 4, 5};
            std::vector<int> v2 = std::move(v1);
            std::cout << "v1 size: " << v1.size() << std::endl; // v1 现在为空
            std::cout << "v2 size: " << v2.size() << std::endl; // v2 拥有 v1 的元素
            /*
            关键点
    
            移动语义：
                std::move 允许将资源从一个对象转移到另一个对象，而不是进行深拷贝。
                移动操作通常比拷贝操作更高效，因为它只是转移资源的所有权，而不是复制资源。
            右值引用：
                std::move 将对象转换为右值引用，从而启用移动构造函数或移动赋值运算符。
                右值引用是临时值，可以被移动但不能被拷贝。
            性能优化：
                在处理大型对象（如字符串、向量、映射等）时，移动语义可以显著提高性能，减少不必要的内存分配和拷贝。
    
            常见应用场景
    
            返回大型对象：
                在函数返回大型对象时，使用 std::move 可以避免拷贝，提高性能。
            */
    
        }
    
        {
            // 使用 forward 函数
            int x = 10;
            // orward_example(x)：x 是一个左值，T 被推导为 int&，std::forward<int&>(x) 保持左值引用，调用左值 process 函数
            forward_example(x);           // Lvalue reference
            // orward_example(20)：20 是一个右值，T 被推导为 int，std::forward<int>(20) 转换为右值引用，调用右值 process 函数。
            forward_example(20);          // Rvalue reference
            // orward_example(std::move(x))：std::move(x) 将 x 转换为右值，T 被推导为 int，
            // std::forward<int>(std::move(x)) 转换为右值引用，调用右值 process 函数。
            forward_example(std::move(x));// Rvalue reference
            /**
            “如果有变量名就是左值，如果是立即数就是右值”，这种规则在某些情况下是成立的，但并不是完全准确的。
            例如，变量名通常代表左值，因为它们有持久的生命周期，而立即数（如字面量）通常是右值，因为它们是临时的。
            然而，这种判断方式有例外，比如当变量被std::move处理后，它也会被视为右值。
            在 C++ 中，值类别（value category）是用于区分表达式是左值（lvalue）还是右值（rvalue）的概念。你的理解在大多数情况下是正确的，但有一些例外和更细致的规则。
            左值：
            
                定义：左值是指具有名称的变量，其生命周期通常超过表达式的作用域。
                特点：
                    可以出现在赋值运算符的左侧。
                    有固定的内存地址。
                    生命周期较长，通常直到变量的作用域结束。
                    右值（rvalue）
                        int x = 10;
                        process(x); // x 是左值
            右值：
                定义：右值是指临时对象或字面量，其生命周期通常仅限于表达式的作用域。
                特点：
                不能出现在赋值运算符的左侧。
                没有固定的内存地址。
                生命周期较短，通常在表达式结束时销毁。
                process(20); // 20 是右值
    
            例外情况
    
                1. std::move：可以将一个左值转换为右值引用，从而使其在表达式中被视为右值。
                2. 函数返回值：函数返回的临时对象通常是右值。
                3. 字面量：如 42、3.14、"hello"，通常是右值
            总结：
                1. 有变量名的通常是左值：如果一个表达式有名称（如变量名），它通常是左值。
                2. 立即数通常是右值：字面量和临时对象通常是右值。
                3. std::move 可以改变值类别：std::move 可以将左值转换为右值引用。
            */
        }
        return 0;
    }
    
    
