---
layout: post
title: runoob_11_iterator
permalink: /runoob/runoob_11_iterator/
date: 2017-01-11 10:43:00 +0800
description: runoob_11_iterator
img: post-6.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 10:44:36
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 11:53:39
     * @FilePath: /cxx_stl/runoob_11.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-iterator.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <vector>
    #include <iterator>
    using namespace std;
    int main(int argc, const char** argv) {
        vector<int> vec = {1, 2, 3, 4, 5};
        // 使用迭代器遍历Vector
        for(vector<int>::iterator it = vec.begin(); it!= vec.end(); ++it){
            cout<<*it<<" ~";
        }
        // 使用auto关键字简化迭代器类型
        for(auto it=vec.begin(); it!=vec.end(); it++){
            cout<<*it<<" @";
        }
        // 使用c++11范围for循环
        for(int elem: vec){
            cout<<elem<<" #";
        }
        return 0;
    }
    
