---
layout: post
title: runoob_20_atomic
date: 2025-03-25 10:51:00 +0800
description: runoob_20_atomic
img: post-1.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 16:18:40
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 16:58:47
     * @FilePath: /cxx_stl/runoob_20.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-atomic.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <atomic> // 提供了一组原子操作，用于保证在多线程环境下对单个数据的访问是原子的，即不可分割的
    #include <thread>
    using namespace std;
    std::atomic<int> counter(0); // 初始化原子计数器
    
    void increment(){
        for(int i=0; i<10000; i++){
            // counter.fetch_add 是 C++ 中 std::atomic 类的一个成员函数，
            // 用于以原子方式对变量进行增加操作。它确保在多线程环境中对共享变量的访问是安全的
            // memory_order_relaxed指定了内存顺序为宽松顺序，这意味着操作可以与其他线程中的操作重排序，但仍然保证原子性
            counter.fetch_add(1, std::memory_order_relaxed);// 原子增加
        }
    }
    
    int main(int argc, const char** argv) {
        std::thread t1(increment);
        std::thread t2(increment);
    
        t1.join();
        t2.join();
    
        std::cout << "Final counter value: " << counter << std::endl; // 输出最终的计数器值
        return 0;
    }
    
