---
layout: post
title: runoob_03_iostream
permalink: /runoob/runoob_03_iostream/
date: 2017-01-03 10:35:00 +0800
description: runoob_03_iostream
img: post-5.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-20 20:18:41
     * @LastEditors: by777
     * @LastEditTime: 2025-03-20 20:33:19
     * @FilePath: /cxx_stl/runoob_03.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-iostream.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    // 对输出格式化，例如设置宽度精度和对齐方式
    #include <iomanip>
    int main(int argc, const char** argv) {
        int age;
        std::string name;
        // std::cout<<"Enter your name: ";
        // std::cin>>name;
        // std::cout<<"Enter your age: ";
        // std::cin>>age;
        // std::cout<<"Hello! "<<name<<", you are " <<age<<" years old."<<std::endl;
    
        std::cerr<<"Error: this is an error message"<<std::endl;
        std::clog<<"Log: this is a log message"<<std::endl;
    
    
        double pi = 3.14159;
        // 设置输出精度
        std::cout<<std::setprecision(3)<<pi<<std::endl;
    
        // 设置宽度和对齐方式
        std::cout<<std::setw(20)<<std::left<<pi<<std::endl;
        std::cout<<std::setw(20)<<std::right<<pi<<std::endl;
    
        // 检查流的状态
        std::cout<<"Enter your name: ";
        std::cin>>name;
        if(std::cin.fail()){
    
            std::cerr<<"Invalid input!"<<std::endl;
        }else{
            std::cout<<"You entered: "<<name<<std::endl;
        }
    
        // 处理字符串输入: getline可以读取包含空格的整行输入
        std::string fullName;
        std::cout << "Enter your full name: ";
        std::getline(std::cin, fullName);
        std::cout << "Hello， " <<fullName<< "!"<<std::endl;
    
    
    
        return 0;
    }
    
