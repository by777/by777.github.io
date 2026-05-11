---
layout: post
title: runoob_15_chrono
date: 2025-03-25 10:47:00 +0800
description: runoob_15_chrono
img: post-4.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 11:46:51
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 11:52:12
     * @FilePath: /cxx_stl/runoob_15.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-chrono.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <chrono> // 是 C++ 标准库中处理时间相关操作的核心部分。
    
    using namespace std;
    void someFunction() {
        // 模拟一些操作
        // std::this_thread::sleep_for(std::chrono::seconds(1));
    }
    int main(int argc, const char** argv) {
        auto start = std::chrono::high_resolution_clock::now();
        someFunction();
        auto end = std::chrono::high_resolution_clock::now();
        auto duration = std::chrono::duration_cast<std::chrono::milliseconds>(end - start);
        std::cout << "Function took " << duration.count() << " milliseconds to execute." << std::endl;
    
        auto now = std::chrono::system_clock::now();
        std::time_t now_c = std::chrono::system_clock::to_time_t(now);
    
        std::cout << "Current date and time: " << std::ctime(&now_c);
        return 0;
    }
    
