---
layout: post
title: runoob_14_valarray
date: 2017-01-14 10:46:00 +0800
description: runoob_14_valarray
img: post-1.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 11:34:22
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 11:54:18
     * @FilePath: /cxx_stl/runoob_14.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-valarray.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <valarray> //<valarray> 库是一个用于数值计算的库，它提供了一种高效的方式来处理数值数组
    #include <vector>
    
    int main(int argc, const char** argv) {
    
        std::valarray<double> va1(5), va2(5);
        va1 = {1.0, 2.0, 3.0, 4.0, 5.0};
        va2 = {2.0, 3.0, 4.0, 5.0, 6.0};
    
        std::valarray<double> sum = va1 + va2; // 加法
        std::valarray<double> diff = va1 - va2; // 减法
        std::valarray<double> prod = va1 * va2; // 乘法
        std::valarray<double> quot = va1 / va2; // 除法
    
        std::cout << "Sum: ";
        for (auto i : sum) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
    
        std::cout << "Difference: ";
        for (auto i : diff) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
    
        std::cout << "Product: ";
        for (auto i : prod) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
    
        std::cout << "Quotient: ";
        for (auto i : quot) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
    
        {
            std::valarray<double> va1(5), va2(5);
            va1 = {1.0, 2.0, 3.0, 4.0, 5.0};
            va2 = {2.0, 3.0, 4.0, 5.0, 6.0};
    
            std::valarray<double> sum = va1 + va2; // 加法
            std::valarray<double> diff = va1 - va2; // 减法
            std::valarray<double> prod = va1 * va2; // 乘法
            std::valarray<double> quot = va1 / va2; // 除法
    
            std::cout << "Sum: ";
            for (auto i : sum) {
                std::cout << i << " ";
            }
            std::cout << std::endl;
    
            std::cout << "Difference: ";
            for (auto i : diff) {
                std::cout << i << " ";
            }
            std::cout << std::endl;
    
            std::cout << "Product: ";
            for (auto i : prod) {
                std::cout << i << " ";
            }
            std::cout << std::endl;
    
            std::cout << "Quotient: ";
            for (auto i : quot) {
                std::cout << i << " ";
            }
            std::cout << std::endl;
        }
    
        return 0;
    }
    
