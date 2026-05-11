---
layout: post
title: runoob_09_bitset
date: 2025-03-25 10:41:00 +0800
description: runoob_09_bitset
img: post-1.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-21 18:09:55
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 11:54:45
     * @FilePath: /cxx_stl/runoob_09.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-bitset.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <bitset>
    
    int main(int argc, const char** argv) {
        
        std::bitset<8> bits("10101010");
        std::cout<<"Count of 1 is: "<<bits.count()<<std::endl;// 
        std::cout<<"Size: "<<bits.size()<<std::endl;
        std::cout<<"bits[3] == 1? "<<bits.test(3)<<std::endl;
        std::cout<<"all bits == 1? "<<bits.all()<<std::endl;
    
    
        unsigned long num = bits.to_ulong();
        std::string str = bits.to_string();
    
        std::cout<<"num: "<<num<<std::endl;
        std::cout<<"str: "<<str<<std::endl;
    
        return 0;
    }
    
