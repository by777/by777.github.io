---
layout: post
title: runoob_06_array
date: 2017-01-06 10:39:00 +0800
description: runoob_06_array
img: post-6.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-21 17:18:39
     * @LastEditors: by777
     * @LastEditTime: 2025-03-21 17:29:08
     * @FilePath: /cxx_stl/runoob_06.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-array.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <array>
    using namespace std;
    int main(int argc, const char** argv) {
        array<int, 5> myArray = {1, 2, 3, 4, 5};
        int i = 0;
        for(const auto& value: myArray){
            i ++;
            cout<<value<<" ";
    
        }
        cout<<endl;
    
        // at和[]从0开始
        cout<<myArray.at(2)<<endl;
        cout<<myArray.size()<<endl;
        myArray[3] = 10;
        for(const auto& value: myArray){
            i ++;
            cout<<value<<" ";
    
        }
        cout<<"首元素: "<<myArray.front()<<" 尾元素: "<<myArray.back()<<endl;
    
        // catch exception
        try{
            myArray.at(10);
        }catch(const std::out_of_range& e){
            cerr<<"Error: "<<e.what()<<endl;
        }
        // fill
        myArray.fill(100);
        for(const auto& value: myArray){
            i ++;
            cout<<value<<" ";
        }
        // swap
        array<int, 5> myArray2 = {101, 102, 103, 104, 105};
        myArray.swap(myArray2);
        cout<<"myArray"<<endl;
        for(const auto& value: myArray){
            i ++;
            cout<<value<<" ";
        }
        cout<<"myArray2"<<endl;
    
        for(const auto& value: myArray2){
            i ++;
            cout<<value<<" ";
        }
        return 0;
    }
    
