---
layout: post
title: runoob_12_functional
permalink: /runoob/runoob_12_functional/
date: 2017-01-12 10:43:00 +0800
description: runoob_12_functional
img: post-6.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 11:07:00
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 11:54:07
     * @FilePath: /cxx_stl/runoob_12.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-functional.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <functional>
    #include <algorithm>
    #include <vector>
    using namespace std;
    void greet(){
        cout<<"Hello world"<<endl;
    }
    int add(int a, int b){
        return a+b;
    }
    bool compare(int a, int b){
        return a<b;
    }
    int main(int argc, const char** argv) {
        // std::function 是一个模板类，可以存储、调用和复制任何可调用对象，比如函数、lambda 表达式或函数对象。
        std::function<void()> f = greet; // 使用函数
        f(); // 输出Hello world
        std::function<void()> lambda = [](){
            cout<<"Hello lambda"<<endl;
        };
        lambda();
    
        // std::bind bind 允许我们创建一个可调用对象，它在调用时会将给定的参数绑定到一个函数或函数对象。
        // std::placeholders::_1 是一个占位符，它在调用 bound_add 时会被实际的参数替换。
        auto bound_add = std::bind(add, 5, std::placeholders::_1);
        std::cout<<bound_add(10)<<endl;
    
        // 使用比较函数
        vector<int> v = {5, 3, 9, 1, 4};
        std::sort(v.begin(), v.end(), compare);
        for(int i: v){
            cout<<i<<" ";//输出: 1 3 4 5 9
        }
        std::cout<<endl;
    
            std::sort(v.begin(), v.end(), std::less<int>()); // 使用标准库比较
        for(int i: v){
            cout<<i<<" ";//输出: 1 3 4 5 9
        }
        return 0;
    }
    
    
