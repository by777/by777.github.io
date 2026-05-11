---
layout: post
title: runoob_07_vector
date: 2017-01-07 10:40:00 +0800
description: runoob_07_vector
img: post-3.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-21 17:31:14
     * @LastEditors: by777
     * @LastEditTime: 2025-03-21 17:33:23
     * @FilePath: /cxx_stl/runoob_07.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-vector.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <vector>
    int main(int argc, const char** argv) {
        std::vector<int> vec;
        vec.push_back(10);
        vec.push_back(20);
        vec.push_back(30);
    
        std::cout << "Vector size: " << vec.size() << std::endl;
        std::cout << "Vector capacity: " << vec.capacity() << std::endl;
    
        // 删除最后一个元素
        vec.pop_back();
        for(const auto& value: vec){
            std::cout<<value<<" ";
        }
        std::cout<<std::endl;
        std::cout << "After pop_back, size: " << vec.size() << std::endl;
        return 0;
    }
    
