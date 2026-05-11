---
layout: post
title: runoob_01_Vector&Iterator
date: 2017-01-01 10:24:00 +0800
description: runoob_01_Vector&Iterator
img: post-2.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-20 19:54:01
     * @LastEditors: by777
     * @LastEditTime: 2025-03-20 20:13:27
     * @FilePath: /cxx_stl/runoob_01.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-stl-tutorial.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <vector>
    using namespace std;
    
    // g++ -std=c++23 -fmodules-ts -o program main.cpp
    int main(int argc, const char** argv) {
        
        vector <int> vec;
        int i;
        cout<<"vector size: "<<vec.size()<<endl;
        for(int i=0; i<5; i++){
            vec.push_back(i);
        }
        cout<<"vector size: "<<vec.size()<<endl;
        for(int i=0; i<5; i++){
            cout<<vec[i]<<endl;
        }
    
        //使用迭代器iterator
        vector<int>::iterator v = vec.begin();
        while(v != vec.end()){
            std::cout << "value of v:" << *v << std::endl;
            v++;
        }
        
        return 0;
    }
    
