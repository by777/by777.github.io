---
layout: post
title: runoob_05_sstream
permalink: /runoob/runoob_05_sstream/
date: 2017-01-05 10:38:00 +0800
description: runoob_05_sstream
img: post-6.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-21 17:01:06
     * @LastEditors: by777
     * @LastEditTime: 2025-03-21 17:13:15
     * @FilePath: /cxx_stl/runoob_05.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-sstream.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <sstream>
    using namespace std;
    int main(int argc, const char** argv) {
        cout<<"sstream提供了方便的方式处理字符串流"<<endl;
        string data = "10 20.5";
        // istringstream用于从字符串中读取数据
        // ostringstream将数据写入字符串
        // stringstream二者组合，可同时写和读
    
        std::istringstream iss(data);
    
        int i;
        double d;
        iss>>i>>d;
        cout<<"Inter: "<<i<<endl;
        cout<<"Float: "<<d<<endl;
    
    
        std::ostringstream oss;
        i=100;
        d=200.5;
        oss<<i<<" "<<d;
        string result = oss.str();
        cout<<"result: "<<result<<endl;
    
        data = "30 40.555";
        std::stringstream ss(data);
        // 从stringstream中读取数据
        ss>>i>>d;
        cout<<"Read integer: "<<i<<", Double: "<<d<<endl;
    
        // 向stringstream中写入数据
        ss.str("55 60.7"); // 清空stringstream
        // ss<<"New data: "<<50<<" "<<60.7;
    
        string newData=ss.str();
        cout<<"newData: "<<newData<<endl;
    
    
        return 0;
    }
    
