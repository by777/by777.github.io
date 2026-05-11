---
layout: post
title: runoob_27_random
date: 2025-03-25 10:55:00 +0800
description: runoob_27_random
img: post-4.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 18:20:23
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 18:22:58
     * @FilePath: /cxx_stl/runoob_27.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-random.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <random> // 涵盖了从简单的均匀分布到复杂的离散分布
    using namespace std;
       /*
        * <random> 库由以下三个主要组件构成：
        * 随机数引擎：生成伪随机数的核心，用于控制生成过程的可重复性和随机性。
        * 随机数分布：控制生成的数值遵循的概率分布类型。
        * 随机数适配器：允许调整引擎行为，如 discard_block 等适配器。
        * 常用随机数引擎
        * 引擎	描述
        * std::default_random_engine	默认随机数引擎，实现依赖于具体编译器。
        * std::minstd_rand	线性同余引擎，产生均匀的伪随机数序列。
        * std::mt19937	梅森旋转算法，适合通用随机数生成。
        * std::mt19937_64	64 位的梅森旋转算法。
        * std::ranlux24_base	简化的减法进位引擎，用于高质量生成。
        * std::knuth_b	Knuth shuffle 随机数生成器。
        * 
        * 常用引擎如 std::mt19937 因为生成速度快且生成质量高，是普遍推荐的随机数生成引擎。生成器还可以使用 seed() 方法指定种子，便于生成可重复的伪随机序列。
        */
    int main(int argc, const char** argv) {
        {
            std::mt19937 gen(seed);
            std::uniform_int_distribution<int> dist(1, 100); // 生成 1 到 100 间的整数
            int random_int = dist(gen);
        }
        return 0;
    }
    
