---
layout: post
title: runoob_17_mutex
permalink: /runoob/runoob_17_mutex/
date: 2017-01-17 10:49:00 +0800
description: runoob_17_mutex
img: post-3.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 14:47:17
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 14:57:52
     * @FilePath: /cxx_stl/runoob_17.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-mutex.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <thread>
    #include <mutex> // 用于在多线程程序中实现线程间的同步和互斥
    using namespace std;
    
    // 1. std::mutex 基本的互斥锁
    std::mutex mtx;
    int shared_resource = 0;
    void increment(){
        for(int i=0; i< 10000; i++){
            mtx.lock();
            ++shared_resource;
            mtx.unlock();
        }
    }
    // 2. std:;recursive_mutex: 递归互斥锁，允许同一线程多次锁定
    std::recursive_mutex rmtx;
    int shared_resource_2 = 0;
    void recursive_increment(int count){
        if(count<0) return;
        std::lock_guard<std::recursive_mutex> lock(rmtx);
        ++shared_resource_2;
        cout<<"Increment shared_resource_2 to "<<shared_resource_2<<" (count="<<count<<")"<<endl;
        //递归调用
        recursive_increment(count-1);
    }
    // 3. std::timed_mutex：具有超时功能的互斥锁
    // 4. std::recursive_timed_mutex:具有超时功能的递归互斥锁
    
    int main(int argc, const char** argv) {
        // 1. std::mutex 基本的互斥锁
        {
            thread t1(increment);
            thread t2(increment);
            t1.join();
            t2.join();
            cout<<"Final value: "<<shared_resource<<endl;        
    
        }
    
    
        // 2. std:;recursive_mutex: 递归互斥锁，允许同一线程多次锁定
        {
            thread t1(recursive_increment, 3);
            thread t2(recursive_increment, 3);
            t1.join();
            t2.join();
            cout<<"Final value: "<<shared_resource_2<<endl;        
    
    
        }
        // 3. std::timed_mutex：具有超时功能的互斥锁
        // 4. std::recursive_timed_mutex:具有超时功能的递归互斥锁
    
        return 0;
    }
    
