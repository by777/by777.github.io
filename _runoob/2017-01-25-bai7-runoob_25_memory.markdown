---
layout: post
title: runoob_25_memory
permalink: /runoob/runoob_25_memory/
date: 2017-01-25 10:54:00 +0800
description: runoob_25_memory
img: post-3.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 17:25:45
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 17:53:55
     * @FilePath: /cxx_stl/runoob_25.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-memory.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <memory> // 包含了用于动态内存管理的模板和函数
    using namespace std;
    
    class MyClass{
        public:
            void doSomething(){
                cout<<"Doing something ..."<<endl;
            }
    };
    
    class Node {
    public:
        std::shared_ptr<Node> next; // next 是一个 std::shared_ptr
        std::weak_ptr<Node> prev; // prev 是一个 std::weak_ptr，用于指向前一个节点
        // std::weak_ptr 用于 prev 指针是为了避免循环引用导致的内存泄漏。
        Node() : next(nullptr), prev() {}
    };
    
    int main(int argc, const char** argv) {
    
        /*
         * 智能指针是 <memory> 头文件中的核心内容。它们是 C++11 引入的特性，用于自动管理动态分配的内存。
         * 智能指针的主要类型有：
         * std::unique_ptr：独占所有权的智能指针，同一时间只能有一个 unique_ptr 指向特定内存。
         * std::shared_ptr：共享所有权的智能指针，多个 shared_ptr 可以指向同一内存，内存在最后一个 shared_ptr 被销毁时释放。
         * std::weak_ptr：弱引用智能指针，用于与 shared_ptr 配合使用，避免循环引用导致的内存泄漏。
         */
        std::unique_ptr<MyClass> myPtr(new MyClass());
        myPtr->doSomething();
    
        {
            std::shared_ptr<MyClass> myPtr1(new MyClass());
            std::shared_ptr<MyClass> myPtr2 = myPtr1;
            myPtr1->doSomething();
            myPtr2->doSomething();
            // 当 myPtr1 和 myPtr2 都被销毁时，MyClass 对象的内存才会被释放
        }
        {
            std::shared_ptr<Node> node1 = std::make_shared<Node>();
            std::shared_ptr<Node> node2 = std::make_shared<Node>();
            // node1->next 被设置为指向 node2，这是一个 std::shared_ptr，会增加 node2 的引用计数。
            node1->next = node2;
            // node2->prev 被设置为指向 node1，这是一个 std::weak_ptr，不会增加 node1 的引用计数
            node2->prev = node1;
            // 循环引用，但使用 weak_ptr 避免了内存泄漏
            // 由于 node2->prev 是一个 std::weak_ptr，它不会增加 node1 的引用计数。
            // 当 node1 和 node2 的 std::shared_ptr 超出作用域时，它们的引用计数会正确减少到零，从而释放内存。
            /*关键点：
             * 循环引用问题：如果两个 std::shared_ptr 互相引用，它们的引用计数永远不会降到零，导致内存泄漏。
             * std::weak_ptr 的作用：std::weak_ptr 不增加引用计数，用于打破循环引用，避免内存泄漏。
             * 内存管理：std::shared_ptr 和 std::weak_ptr 配合使用可以安全地管理动态分配的对象的生命周期。*/
        }
        {
    
            // std::allocator 是标准分配器，提供了基本的内存分配和释放功能。
            // 创建一个 std::allocator<int> 对象 alloc，用于分配和管理 int 类型的内存。
            std::allocator<int> alloc;
            int *p = alloc.allocate(1);//分配的内存大小是 sizeof(int) * 1 字节，而不是 1 字节
            // 使用 alloc.construct(p, 42) 在分配的内存位置 p 上构造一个 int 对象，并初始化为 42。
            alloc.construct(p, 42);
            // std::align 用于调整指针的对齐方式，以确保所分配内存满足特定对齐要求。
            std::cout<<*p<<endl;
            alloc.destroy(p);//销毁对象 调用其析构函数
            alloc.deallocate(p, 1);//释放内存
    
        }
        {
            // std::align 用于调整指针的对齐方式，以确保所分配内存满足特定对齐要求。
            // alignas(16) 指定缓冲区 buffer 按 16 字节对齐。
            alignas(16) char buffer[64];
            void *p = buffer;
            size_t space = sizeof(buffer);
            // std::align 尝试将指针 p 按 16 字节对齐，并确保对齐后的指针指向的空间足够存储一个 int 大小的对象。
            // 如果对齐成功，aligned_ptr 将指向对齐后的地址；否则，返回 nullptr
            void * aligned_ptr = std::align(16, sizeof(int), p, space);
            if (aligned_ptr) {
            std::cout << "Memory aligned\n";
            } else {
                std::cout << "Memory alignment failed\n";
            }
        }
        return 0;
    }
    
