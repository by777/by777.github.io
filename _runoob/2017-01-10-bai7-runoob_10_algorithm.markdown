---
layout: post
title: runoob_10_algorithm
permalink: /runoob/runoob_10_algorithm/
date: 2017-01-10 10:42:00 +0800
description: runoob_10_algorithm
img: post-6.jpg
tags: [cnblogs, runoob]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-21 18:17:39
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 11:54:01
     * @FilePath: /cxx_stl/runoob_10.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-algorithm.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <algorithm>
    #include <vector>
    using namespace std;
    int main(int argc, const char** argv) {
        cout<<"=========1. sort========="<<endl;
        vector<int> numbers = {5, 2, 9, 1, 5, 6};
        sort(numbers.begin(), numbers.end());
        // partial_sort 对部分区间排序，前 n 个元素为有序。|| stable_sort 稳定排序，保留相等元素的相对顺序。
        for(int num: numbers){
            cout<<num<<" ";
        }
    
        cout<<"=========2. find========="<<endl;
        auto it = find(numbers.begin(), numbers.end(), 3);
        // binary_search: 对有序区间进行二分查找。 || find_if: 查找第一个满足特定条件的元素。
        if(it!=numbers.end()){
            cout<<"Found: "<<*it<<endl;
        }else{
            cout<<"Not Found"<<endl;
        }
    
        cout<<"=========3. copy========="<<endl;
    
        cout<<"=========4. equal========="<<endl;
        std::vector<int> v1 = {1, 2, 3, 4, 5};
        std::vector<int> v2 = {1, 2, 3, 4, 5};
    
        bool are_equal = std::equal(v1.begin(), v1.end(), v2.begin());
        std::cout << (are_equal ? "Vectors are equal." : "Vectors are not equal.") << std::endl;
    
        cout<<"=========5. reverse========="<<endl;//反转区间内的元素顺序
        cout<<"=========6. fill========="<<endl;//将指定区间内的所有元素赋值为某个值
        cout<<"=========7. replace========="<<endl;//将区间内的某个值替换为另一个值
        cout<<"=========8. copy========="<<endl;
        cout<<"=========9. next_permutation========="<<endl; // 生成字典序的下一个排列
        std::vector<int> vec = {1, 2, 3};
        do {
            for (int n : vec) std::cout << n << " ";
            std::cout << std::endl;
        } while (std::next_permutation(vec.begin(), vec.end()));
        cout<<"=========10. merge========="<<endl; // 把两个有序区间合并到一个有序区间
        std::vector<int> vec1 = {1, 3, 5};
        std::vector<int> vec2 = {2, 4, 6};
        std::vector<int> result(6);
        std::merge(vec1.begin(), vec1.end(), vec2.begin(), vec2.end(), result.begin());
        cout<<"=========11. inplace_merge========="<<endl; // 在单个区间中合并两个有序子区间
        // std::vector<int> middle(6);
        // std::inplace_merge(vec1.begin(), middle, vec1.end());
        cout<<"=========12. accumulate========="<<endl; // 计算范围内的元素累加和
        cout<<"=========13. for each========="<<endl; // 对区间内每个元素执行操作
        std::for_each(vec.begin(), vec.end(), [](int &x){x += 1;});
        cout<<"=========14. min_element/max_element========="<<endl; // 查找区间内的最小值和最大值
    
        return 0;
    }
    
