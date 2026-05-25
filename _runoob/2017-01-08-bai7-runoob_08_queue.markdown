---
layout: post
title: runoob_08_queue
permalink: /runoob/runoob_08_queue/
date: 2017-01-08 10:41:00 +0800
description: runoob_08_queue
img: post-5.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-21 17:48:04
     * @LastEditors: by777
     * @LastEditTime: 2025-03-21 17:57:24
     * @FilePath: /cxx_stl/runoob_08.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-priority_queue.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <queue>
    struct compare {
        bool operator()(int a, int b) {
            return a > b; // 定义最小堆 当 a > b 时，返回 true，表示 a 应该排在 b 后面
        }
    };
    int main(int argc, const char** argv) {
        // 创建一个自定义类型的优先队列，使用最小堆
        std::priority_queue<int, std::vector<int>, compare> pq_min;
    
        // 向优先队列中添加元素
        pq_min.push(30);
        pq_min.push(10);
        pq_min.push(50);
        pq_min.push(20);
    
        // 输出队列中的元素
        std::cout << "最小堆中的元素：" << std::endl;
        while (!pq_min.empty()) {
            std::cout << pq_min.top() << std::endl;
            pq_min.pop();
        }
        return 0;
    }
    
