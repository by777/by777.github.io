---
layout: post
title: runoob_29_codecvt
date: 2017-01-29 10:56:00 +0800
description: runoob_29_codecvt
img: post-2.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 20:21:37
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 20:23:00
     * @FilePath: /cxx_stl/runoob_29.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-codecvt.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <codecvt>
    
    #include <locale>
    // <codecvt> 是 C++ 标准库中的一个头文件，提供了字符转换的工具。
    // 这个头文件主要包含 std::codecvt 类模板及其特化，支持字符编码之间的转换，例如从 UTF-8 到 UTF-16
    using namespace std;
    
    int main(int argc, const char** argv) {
            // 创建一个 UTF-8 到 UTF-16 的转换器
        std::wstring_convert<std::codecvt_utf8_utf16<wchar_t>> converter;
    
        // 原始的 UTF-8 字符串
        std::string narrow_string = "Hello, World!";
    
        // 转换为 UTF-16 宽字符串
        std::wstring wide_string = converter.from_bytes(narrow_string);
    
        // 输出宽字符串
        std::wcout << L"Wide string: " << wide_string << std::endl;
    
        // 将宽字符串转换回 UTF-8 字符串
        std::string converted_string = converter.to_bytes(wide_string);
    
        // 输出转换后的字符串
        std::cout << "Converted string: " << converted_string << std::endl;
        return 0;
    }
    
