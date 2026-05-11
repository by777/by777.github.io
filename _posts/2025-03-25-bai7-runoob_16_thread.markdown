---
layout: post
title: runoob_16_thread
date: 2025-03-25 10:48:00 +0800
description: runoob_16_thread
img: post-5.jpg
tags: [cnblogs]
author: Bai Qi
---


    /*
     * @Author: by777
     * @Date: 2025-03-24 11:55:22
     * @LastEditors: by777
     * @LastEditTime: 2025-03-24 14:45:32
     * @FilePath: /cxx_stl/runoob_16.cpp
     * @Description: https://www.runoob.com/cplusplus/cpp-libs-thread.html
     * 
     * Copyright (c) 2025 by by777, All Rights Reserved. 
     */
    #include <iostream>
    #include <thread>
    #include <mutex>
    #include <condition_variable>
    #include <future> // std::future 和 std::promise 用于线程间的结果传递。
    
    using namespace std;
    void print_id(int id){
        cout<<"ID: "<<id<<" | Thread ID: "<<std::this_thread::get_id()<<endl;
    }
    int sum = 0;
    
    void add(int a, int b) {
        sum += a + b;
    }
    // 简单的函数，在线程中执行
    void print_message(const std::string& message, int delay) {
        std::this_thread::sleep_for(std::chrono::milliseconds(delay));
        std::cout << message << std::endl;
    }
    
    std::mutex mtx; // 全局mutex对象 用于同步对共享资源的访问。
    int shared_resource = 0;
    
    // 线程函数
    void increment() {
        std::lock_guard<std::mutex> lock(mtx); // 上锁，保证线程安全
        ++shared_resource;
        // std::lock_guard 是一个 RAII 风格的锁管理器，用于自动管理锁的生命周期。
        std::cout << "Incremented shared_resource to " << shared_resource << std::endl;
        // lock 在 lock_guard 离开作用域时自动释放
    }
    void print_thread_id(int id) {
        std::unique_lock<std::mutex> lock(mtx);
        std::cout << "Thread ID: " << id << std::endl;
        lock.unlock(); // 可以手动解锁
        // ... 其他操作
    }
    // std::condition_variable 用于线程间的等待和通知。
    std::mutex mtx2;
    std::condition_variable cv;
    bool ready = false;
    void print_id_2(int id){
        std::unique_lock<std::mutex> lock(mtx2);
        cv.wait(lock, []{return ready;});
        std::cout<<"Thread ID: "<<id<<std::endl;
    }
    void set_ready(){
        std::unique_lock<std::mutex> lock(mtx2);
        ready = true;
        cv.notify_all();
    }
    // std::future 和 std::promise 用于线程间的结果传递。
    void calculate_square(std::promise<int> &&p, int x){
        p.set_value(x * x);
    }
    // std::async 用于启动异步任务，并返回一个 std::future。
    int calculate_square_2(int x){
        return x * x;
    }
    int main(int argc, const char** argv) {
        /*
         * <thread> 库是 C++ 标准库的一部分，提供了创建和管理线程的基本功能，它包括以下几个关键组件：
         * std::thread：表示一个线程，可以创建、启动、等待和销毁线程。
         * std::this_thread：提供了一些静态成员函数，用于操作当前线程。
         * std::thread::id：线程的唯一标识符。
         * g++ runoob_16.cpp -lpthread
        */
        std::thread t1(print_id, 1);
        std::thread t2(print_id, 2);
        // 创建 std::thread 对象后，线程会立即开始执行，你可以调用 join() 方法来等待线程完成。 
        // join() 方法会阻塞当前线程，直到被调用的线程完成执行。
        t1.join();
        t2.join();
        // ID: 1 | Thread ID: 139677280528128
        // ID: 2 | Thread ID: 139677272135424
        int a = 5;
        int b = 10;
    
        std::thread t01(add, a, b);
        std::thread t02(add, a, b);
    
        t01.join();
        t02.join();
    
        std::cout << "Sum: " << sum << std::endl; // 输出结果：Sum: 30
    
    
        std::thread tA1(print_message, "Hello from thread 1", 1000);
        std::thread tA2(print_message, "Hello from thread 2", 500);
        /*
        * detach(): 将线程置于后台运行，不再等待线程结束
        * join(): 等待线程结束
        * joinable(): 检查线程是否可被 join 或 detach
        */
        // 等待线程 t1 完成
        if (tA1.joinable()) {
            tA1.join();
        }
    
        // 等待线程 t2 完成
        if (tA2.joinable()) {
            tA2.join();
        }
    
        std::cout << "Main thread finished." << std::endl;
    
        {
            std::thread t1(increment);
            std::thread t2(increment);
        
            t1.join(); // 等待线程 t1 完成
            t2.join(); // 等待线程 t2 完成
    
            std::cout << "Final value of shared_resource: " << shared_resource << std::endl;
    
        }
    
        // std::condition_variable用于线程之间的等待和通知
        cout<<"condition_variable用于线程之间的等待和通知"<<endl;
        {
            std::thread t1(print_id_2, 1);
            std::thread t2(print_id_2, 2);
            std::this_thread::sleep_for(std::chrono::seconds(1));
            set_ready();
            t1.join();
            t2.join();
        }
    
        {
            // promise 用于设置值，future 用于获取值，二者通过共享状态连接
            std::cout<<"std::future 和 std::promise 用于线程间的结果传递。"<<std::endl;
            std::promise<int > p; // 创建一个 promise 对象，用于存储计算结果
            std::future<int> f = p.get_future(); // 从 promise 中获取一个 future 对象
            // future 用于等待并获取 promise 设置的值。
            // 线程函数接收一个右值引用的 promise 和一个整数 x
            std::thread t(calculate_square, std::move(p), 5); // 将 promise 对象的所有权转移给线程，因为 promise 不可复制
            std::cout<<"Squre: "<<f.get()<<std::endl;
            // 这种模式常用于异步任务，比如在后台线程中进行耗时计算，然后在主线程中获取结果。
            t.join();
    
        }
    
        {
            cout<<"std::async 用于启动异步任务，并返回一个 std::future。"<<endl;
            std::future<int> result = std::async(calculate_square_2, 5);
            std::cout<<"Square: "<<result.get()<<std::endl;
    
            /*
             * 
             * std::async 是一个高层次的工具，用于简化异步任务的启动和管理。它自动管理线程的创建和同步，适合简单的异步操作。
             * 1. std::async 的使用场景
             * 适用场景：
             * + 简单的异步任务：当你只需要启动一个任务并获取结果时，std::async 是最简单的选择。
             * + 不需要直接管理线程：如果你不想手动创建和管理线程，std::async 会自动处理这些细节。
             * + 任务的启动策略灵活：std::async 允许你指定任务的启动策略（如立即在新线程中执行或稍后在当前线程中执行）。
             * 2. std::future 和 std::promise 的使用场景
             * std::future 和 std::promise 是低层次的工具，提供了更细粒度的控制。它们适合复杂的异步通信场景，尤其是需要多个线程之间协作的情况。
             * 适用场景：
             * + 复杂的异步通信：当你需要在多个线程之间传递数据或协调操作时，std::future 和 std::promise 提供了更灵活的机制。
             * + 手动管理线程：如果你需要显式创建和管理线程，std::future 和 std::promise 是更好的选择。
             * + 异步任务的取消或超时处理：std::future 提供了 wait_for 和 wait_until 方法，可以用于处理超时或取消任务。
             * 总结和选择依据:
             * + 简单任务：如果任务简单，不需要复杂的线程管理，使用 std::async 更加方便。
             * + 复杂任务：如果任务复杂，需要手动管理线程或进行复杂的异步通信，使用 std::future 和 std::promise 更加灵活。
             * + 线程控制：如果你需要对线程的创建和销毁进行精细控制，std::future 和 std::promise 是更好的选择。
             * + 启动策略：如果你需要灵活的启动策略（如延迟执行），std::async 更加适合。
            */
    
        }
        return 0;
    }
    
