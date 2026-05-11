---
layout: post
title: runoob_19_future
date: 2017-01-19 10:51:00 +0800
description: runoob_19_future
img: post-1.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 16:18:40
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 16:46:52
     * @FilePath: /cxx_stl/runoob_19.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-future.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <future> // 提供了一种异步编程的机制，允许程序在等待某个操作完成时继续执行其他任务
    #include <cmath>
    using namespace std;
    
    int compute_square_root(double x){
        return std::sqrt(x);
    }
    
    int main(int argc, const char** argv) {
        /**
         * std::future：表示异步操作的结果，可以查询操作的状态，获取结果或等待操作完成。
         * std::promise：用于与 std::future 配对，用于设置异步操作的结果。
         * std::packaged_task：封装一个函数或可调用对象，使其可以作为异步任务执行。
         **/
        std::promise<int> prom;
        std::future<int> fut = prom.get_future();
    
        // 在另一个线程中设置结果
        // 在 lambda 表达式中捕获 prom 是按值捕获的，这会导致线程中拥有一个 std::promise 的拷贝。
        // 而 std::promise 是不可拷贝的（它的拷贝构造函数是删除的），这会导致编译错误。
        std::thread t([&prom]() {
            /**
             * + [prom]:
             * 这是 lambda 表达式的捕获列表，表示将 prom 对象捕获到 lambda 表达式中。
             * 捕获方式可以是按值捕获（[prom]）或按引用捕获（[&prom]）。
             * + () { ... }:
             * 定义 lambda 表达式的参数列表（这里没有参数）和函数体。    
             * 捕获列表：用于将外部变量带入 lambda 表达式的作用域中，这些变量在 lambda 定义时就已经确定。
             * 参数列表：用于定义 lambda 表达式接收的参数，这些参数在调用 lambda 时传入。   
             * 常见的捕获方式：
             * 按值捕获：
             *     [x]：捕获变量 x 的值，lambda 表达式中拥有 x 的一份拷贝。
             *     [=]：捕获所有外部变量按值。
             * 按引用捕获：
             *     [&x]：捕获变量 x 的引用，lambda 表达式中直接操作原始变量。
             *     [&]：捕获所有外部变量按引用。
             * 混合捕获：
             *     [x, &y]：捕获变量 x 按值，捕获变量 y 按引用。 
             *  */
            prom.set_value(10);
        });
    
        // 等待结果
        std::cout << "Future value: " << fut.get() << std::endl;
    
        t.join();
    
    
        // std::packaged_task 封装一个函数或可调用对象，使其可以作为异步任务执行。
        // double(double) 表示任务接受一个 double 参数并返回一个 double
        std::packaged_task<double(double)> task(compute_square_root);
        std::future<double> result = task.get_future();
        std::thread th(std::move(task), 9.0);
        std::cout<<"Result: "<<result.get()<<std::endl;
        th.join();
    
        // std::async 是一个方便的函数，用于启动异步任务。它可以立即返回一个 std::future 对象。
        std::future<int> fut1 = std::async(std::launch::async, [](int x){return x * x ;}, 5);
        std::cout<<"Result: "<<fut1.get()<<std::endl;
        return 0;
    }
    
