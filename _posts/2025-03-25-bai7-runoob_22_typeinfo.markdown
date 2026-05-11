---
layout: post
title: runoob_22_typeinfo
date: 2025-03-25 10:52:00 +0800
description: runoob_22_typeinfo
img: post-4.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 17:06:23
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 17:11:44
     * @FilePath: /cxx_stl/runoob_22.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-typeinfo.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <typeinfo>// 提供了运行时类型识别（RTTI，Run-Time Type Identification）功能。
    // RTTI 允许程序在运行时确定对象的类型。这是通过使用 typeid 运算符和 type_info 类实现的
    using namespace std;
    
    class Base{
    public:
        virtual void show(){
            std::cout<<"Base show"<<std::endl;
        }
    };
    
    class Derived: public Base{
    public:
        void show() override{ std::cout<<"Derived show"<<std::endl;}
    };
    
    int main(int argc, const char** argv) {
        Base *basePtr = new Derived();
        Base *basePtr2 = new Base();
        std::cout<<"Type of basePtr: "<<typeid(*basePtr).name()<<std::endl;
        std::cout<<"Type of basePtr2: "<<typeid(*basePtr2).name()<<std::endl;
        if(typeid(*basePtr) == typeid(Derived)){
            cout<<"basePtr is of type Derived"<<endl;
        }else{
            cout<<"basePtr is not of type Derived"<<endl;
        }
        delete basePtr;
        delete basePtr2;
        return 0;
    }
    
