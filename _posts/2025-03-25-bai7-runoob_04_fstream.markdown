---
layout: post
title: runoob_04_fstream
date: 2025-03-25 10:37:00 +0800
description: runoob_04_fstream
img: post-3.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-21 16:30:18
     * @LastEditors: by777
     * @LastEditTime: 2025-03-21 16:37:38
     * @FilePath: /cxx_stl/runoob_04.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-fstream.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <fstream>
    int main(int argc, const char** argv) {
        std::fstream file;
        auto mode = std::ios::out; // 以输出模式打开文件
        file.open("myfile", mode);
        if(!file){
            std::cerr<<"unable to open file"<<std::endl;
            return 1;
        }
        file<<"Hello fstream!"<<std::endl;
        file.close();
    
        mode = std::ios::in; // 以输入模式打开文件
        file.open("myfile", mode);
        std::string line;
        std::cout<<"-------------------"<<std::endl;
        while(getline(file, line)){
            // 逐行读取
            std::cout<<line<<std::endl;
        }
        file.close();
    
        mode = std::ios::app; // 以输入模式打开文件
        file.open("myfile", mode);
        std::cout<<"-------------------"<<std::endl;
        file<<"this is append mode"<<std::endl;
        file.close();
    
    
    
        return 0;
    }
    
