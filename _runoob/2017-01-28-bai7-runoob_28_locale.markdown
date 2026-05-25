---
layout: post
title: runoob_28_locale
permalink: /runoob/runoob_28_locale/
date: 2017-01-28 10:56:00 +0800
description: runoob_28_locale
img: post-6.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 20:17:40
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 20:20:43
     * @FilePath: /cxx_stl/runoob_28.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-locale.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <locale> //locale 类提供了一种机制来控制程序的本地化行为，特别是与语言和文化相关的格式设置和转换操作
    using namespace std;
    int main(int argc, const char** argv) {
        std::locale loc("en_US.UTF-8"); //设置为美国英语
        std::cout.imbue(loc);//设置cout的locale
        double num = 1234567.89;
        std::cout<<"Formatted num: "<<num<<endl;
        {
            std::locale loc("en_US.UTF-8");
            std::cout.imbue(loc);
    
            std::time_t now = std::time(nullptr);
            std::tm* timeinfo = std::localtime(&now);
    
            char buffer[100];
            std::strftime(buffer, sizeof(buffer), "%A, %B %d, %Y", timeinfo);
            std::cout << "Current date: " << buffer << std::endl;
        }
        return 0;
    }
    
