---
layout: post
title: runoob_18_condition_variable
date: 2017-01-18 10:50:00 +0800
description: runoob_18_condition_variable
img: post-4.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 15:41:26
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 16:08:05
     * @FilePath: /cxx_stl/runoob_18.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-condition_variable.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    // 提供了一种机制，允许线程在某些条件不满足时挂起，直到其他线程通知它们条件已经满足
    #include <condition_variable>
    
    #include <mutex>
    #include <queue>
    #include <thread>
    
    using namespace std;
    mutex mtx;
    condition_variable cv;
    queue<int> product;
    void producer(int id){
        for(int i=0; i<5;++i){
            unique_lock<std::mutex> lck(mtx);
            product.push(id*100+1);
            std::cout<<"Producer "<<id<<" produced "<<product.back()<<endl;
            // cv.notify_one(); 会唤醒一个等待在该条件变量上的线程。如果多个线程在等待，只会唤醒其中一个
            // 如果需要唤醒所有等待的线程，可以使用 cv.notify_all();
            cv.notify_one();
            lck.unlock();
            std::this_thread::sleep_for(std::chrono::milliseconds(100));
        }
    }
    
    void consumer(int id){
        while(true){
            std::unique_lock<std::mutex> lck(mtx);
            // std::condition_variable 的 wait 方法的一个重载版本，它接受一个互斥量和一个谓词（predicate）
            /***
             * 作用：
             * 1. 等待条件满足：
             * 当一个线程调用 cv.wait(lck, predicate) 时，它会释放互斥量 lck 并进入等待状态，直到被通知（notify_one 或 notify_all）或者超时。
             * predicate 是一个布尔表达式，用于检查条件是否满足。如果条件满足，线程将继续执行；否则，线程会重新获取互斥量并再次检查条件。
             * 2. 避免虚假唤醒：
             * 即使没有通知，cv.wait 也可能因为其他原因（如信号中断）而返回。predicate 用于确保线程只在条件真正满足时才继续执行。
             * 参数说明：
             * lck：一个 std::unique_lock<std::mutex> 对象，用于保护共享资源。
             * predicate：一个布尔表达式，用于检查条件是否满足。[]{return !product.empty();} 是一个 lambda 表达式，检查共享队列 product 是否不为空。
            ***/
            cv.wait(lck, []{return !product.empty();});
            if(!product.empty()){
                int prod = product.front();
                product.pop();
                std::cout<<"Consumer "<<id<<" consumed "<<prod<<std::endl;
            }
            lck.unlock();
        }
    }
    int main(int argc, const char** argv) {
        std::thread producers[2];
        std::thread consumers[2];
        for(int i=0; i<2; i++){
            producers[i] = std::thread(producer, i+1);
        }
        for(int i=0; i<2; i++){
            consumers[i] = std::thread(consumer, i+1);
        }
          for(int i=0; i<2; i++){
            producers[i].join();
            consumers[i].join();
        }
        return 0;
    }
    
