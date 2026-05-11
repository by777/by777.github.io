---
layout: post
title: runoob_35_templates
date: 2025-03-25 11:05:00 +0800
description: runoob_35_templates
img: post-6.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-25 09:36:42
     * @LastEditors: by777
     * @LastEditTime: 2025-03-25 10:18:37
     * @FilePath: /cxx_stl/runoob_35.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-templates.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <string>
    #include <vector>
    #include <cstdlib>
    #include <stdexcept>
    
    using namespace std;
    // 模板是创建泛型类或函数的蓝图或公式。库容器
    // template <typename type> ret-type func-name(parameter list)
    // {
    //    // 函数的主体
    // }
    
    // 1. 函数模版
    
    // 模板函数 Max 可以接受任何类型（只要该类型支持 < 运算符）。
    // 使用常量引用可以避免拷贝大型对象，提高性能 [类型 const &引用名 = 变量名;]
    
    template <typename T> // ... T const & 返回值和参数都是常量引用
    inline T const& Max(T const& a, T const& b){
        return a < b ? b : a;
    }
    
    // 2. 类模版
    // template <class T> 表示这个类可以接受任何类型 T
    template <class T>
    class Stack{
        private:
            vector<T> elems;
        public:
            void push(T const&); //入栈
            void pop(); //出栈
            T top() const; //返回栈顶元素
            bool empty() const{// 如果栈为空返回true
                return elems.empty();
            }
    };
    template <class T>
    void Stack<T>::push(T const & elem){
        elems.push_back(elem);
    }
    template <class T>
    void Stack<T>::pop () 
    { 
        if (elems.empty()) { 
            throw out_of_range("Stack<>::pop(): empty stack"); 
        }
        // 删除最后一个元素
        elems.pop_back();         
    } 
     
    template <class T>
    T Stack<T>::top () const 
    { 
        if (elems.empty()) { 
            throw out_of_range("Stack<>::top(): empty stack"); 
        }
        // 返回最后一个元素的副本 
        return elems.back();      
    } 
    
    // 通用模板
    template <typename T>
    void print(T value) {
        cout << "General template: " << value << endl;
    }
    
    // 特例化模板，针对 int 类型
    template <>
    void print<int>(int value) {
        cout << "Specialized template for int: " << value << endl;
    }
    
    // 特例化模板，针对 double 类型
    template <>
    void print<double>(double value) {
        cout << "Specialized template for double: " << value << endl;
    }
    
    int main(int argc, const char** argv) {
        int i = 39;
        int j = 20;
        cout<<"Max(i,j)"<<Max(i,j)<<endl;
        double f1 = 13.5;
        double f2 = 20.7;
        cout<<"Max(f1,f2)"<<Max(f1,f2)<<endl;
        string s1 = "Hello";
        string s2 = "World";
        cout<<"Max(s1,s2)"<<Max(s1,s2)<<endl;
        {
            try { 
            Stack<int>         intStack;  // int 类型的栈 
            Stack<string> stringStack;    // string 类型的栈 
     
            // 操作 int 类型的栈 
            intStack.push(7); 
            cout << intStack.top() <<endl; 
     
            // 操作 string 类型的栈 
            stringStack.push("hello"); 
            cout << stringStack.top() << std::endl; 
            stringStack.pop(); 
            stringStack.pop(); 
        } 
        catch (exception const& ex) { 
            cerr << "Exception: " << ex.what() <<endl; 
            // return -1;
        } 
        }
        {
            print(10);    // 调用特例化模板 for int
            print(3.14);  // 调用特例化模板 for double
            print("Hello"); // 调用通用模板
        }
        return 0;
    }
    
