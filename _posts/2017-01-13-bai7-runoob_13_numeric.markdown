---
layout: post
title: runoob_13_numeric
date: 2017-01-13 10:46:00 +0800
description: runoob_13_numeric
img: post-5.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 11:22:18
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 11:54:13
     * @FilePath: /cxx_stl/runoob_13.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-numeric.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <algorithm>
    #include <vector>
    #include <numeric> // <numeric> 头文件提供了一组用于数值计算的函数模板，这些函数可以对容器中的元素进行各种数值操作
    using namespace std;
    int main(int argc, const char** argv) {
        vector<int> v = {1, 2, 3, 4, 5};
        // accumulate 函数用于计算容器中所有元素的总和。它接受三个参数：容器的开始迭代器、结束迭代器和初始值。
        int sum = std::accumulate(v.begin(), v.end(), 0);
        cout<<"Sum: "<<sum<<endl;
    
        // inner_product 函数用于计算两个容器中对应元素乘积的总和。
        vector<int > v1 = {1, 2, 3};
        vector<int > v2 = {4, 5, 6};
    
        int product_sum = std::inner_product(v1.begin(), v1.end(), v2.begin(), 0);
        cout<<"Product_sum: "<<product_sum<<endl;
    
        cout<<"partial_sum 函数用于计算容器中元素的部分和，并将结果存储在另一个容器中"<<endl;
        cout<<"adjacent_difference 函数用于计算容器中相邻元素的差值，并将结果存储在另一个容器中"<<endl;
        cout<<"使用 std::gcd 计算两个整数的最大公约数"<<endl;
        cout<<"使用 std::lcm 计算两个整数的最小公倍数"<<endl;
        cout<<"使用 std::iota 填充范围内的序列值"<<endl;
        cout<<"min_element 和 max_element 函数用于找到容器中的最大值和最小值"<<endl;
        return 0;
    }
    
