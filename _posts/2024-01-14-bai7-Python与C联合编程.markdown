---
layout: post
title: Python与C++联合编程
date: 2024-01-14 19:26:00 +0800
description: Python与C++联合编程
img: post-6.jpg
tags: [cnblogs]
author: Bai Qi
---

# 什么是库

库是写好的现有的，成熟的，可以复用的代码。现实中每个程序都要依赖很多基础的底层库，

本质上来说库是一种可执行代码的二进制形式，可以被操作系统载入内存执行。库有两种：静态库（.a、.lib）和动态库（.so、.dll）。 windows上对应的是.lib .dll linux上对应的是.a .so

# 静态库

在链接阶段，会将汇编生成的目标文件.o与引用到的库一起链接打包到可执行文件中。因此对应的链接方式称为静态链接。  
**静态库特点**

  * 静态库与汇编生成的目标文件一起链接为可执行文件，那么静态库必定跟.o文件格式相似。
  * 其实一个静态库可以简单看成是一组目标文件（.o/.obj文件）的集合。
  * 静态库对函数库的链接是放在编译时期完成的。
  * 程序在运行时与函数库再无关系，移植方便。
  * 浪费空间和资源，因为所有相关的目标文件与牵涉到的函数库被链接合成一个可执行文件。
  * Linux静态库命名规范，必须是"lib[your_library_name].a"：lib为前缀，中间是静态库名，扩展名为.a。



## 创建静态库（.a）

通过上面的流程可以知道，Linux创建静态库过程如下：

  1. 首先，将代码文件编译成目标文件.o（StaticMath.o）


    
    
    g++ -c main_c.cpp
    

注意带参数-c，否则直接编译为可执行文件

2.通过ar工具将目标文件打包成.a静态库文件
    
    
    ar -crv libmain_c.a main_c.o
    

  3. 生成静态库libmain_c.a。



## 动态库

静态库对程序的更新、部署和发布页会带来麻烦。如果静态库liba.lib更新了，所以使用它的应用程序都需要重新编译、发布给用户（对于玩家来说，可能是一个很小的改动，却导致整个程序重新下载，全量更新）。  
动态库在程序编译时并不会被连接到目标代码中，而是在程序运行是才被载入。不同的应用程序如果调用相同的库，那么在内存里只需要有一份该共享库的实例，规避了空间浪费问题。动态库在程序运行是才被载入，也解决了静态库对程序的更新、部署和发布页会带来麻烦。用户只需要更新动态库即可，增量更新。

**动态库特点**

  * 动态库把对一些库函数的链接载入推迟到程序运行的时期
  * 可以实现进程之间的资源共享。共享库
  * 程序升级变得简单
  * 链接载入完全由程序员在程序代码中控制（显式调用



## C++中创建动态库和C的区别

如果是cpp还要加上extern "C"，因此C编译器编译后在符号库中的名字为_foo，而C++编译器为了实现重载则会产生像_foo_int_int之类的名称，因此如果使用g++或者cpp编译动态链接库，则会找不到对应函数出现Segmentation fault。同时要注意编译器的选择，虽然都不会报错，但是执行逻辑不一样。

  1. g++ 会把 .c 文件当做是 C++ 语言 (在 .c 文件前后分别加上 -xc++ 和 -xnone, 强行变成 C++), 从而调用 cc1plus 进行编译
  2. 遇到 .cpp 文件也会当做是 C++, 调用 cc1plus 进行编译
  3. 还会默认告诉链接器, 让它链接上 C++ 标准库
  4. gcc 会把 .c 文件当做是 C 语言. 从而调用 cc1 进行编译
  5. gcc 遇到 .cpp 文件, 会处理成 C++ 语言. 调用 cc1plus 进行编译
  6. gcc 默认不会链接上 C++ 标准库



> 以上内容来自https://blog.csdn.net/weixin_43953700/article/details/124890088

  * shared该选项指定生成动态连接库（让连接器生成T类型的导出符号表，有时候也生成弱连接W类型的导出符号），不用该标志外部程序无法连接。相当于一个可执行文件
  * fPIC：表示编译为位置独立的代码，不用此选项的话编译后的代码是位置相关的所以动态载入时是通过代码拷贝的方式来满足不同进程的需要，而不能达到真正代码段共享的目的。
  * L.：表示要连接的库在当前目录中
  * -ltest：编译器查找动态连接库时有隐含的命名规则，即在给出的名字前面加上lib，后面加上.so来确定库的名称
  * LD_LIBRARY_PATH：这个环境变量指示动态连接器可以装载动态库的路径。  
当然如果有root权限的话，可以修改/etc/ld.so.conf文件，然后调用 /sbin/ldconfig来达到同样的目的，不过如果没有root权限，那么只能采用输出LD_LIBRARY_PATH的方法了。  
可以使用makefile


    
    
    foo.so: foo.cc
    	g++ -fPIC -shared -o $@ $<
    clean:
    	rm -rf *.o *.so
    .PHONY: clean
    

编译指令
    
    
    # 编译指令
    # gcc -o test.so -shared -fPIC test.c
    g++ -o test.so -shared -fPIC test.cc #for c++
    

C++ 动态库代码
    
    
    #include <iostream>
    using namespace std;
    // windows和linux有不同的方案
    #ifdef _WIN32
    #define XLIB __declspec(dllexport) // for windows
    #else
    #define XLIB
    #endif
    extern "C"{
    int foo(int a, int b){
        cout<<"a: "<<a<<" b: "<<b<<endl;
        printf("C++和Python联合编程\n");
        return a+b;
    }
    
    }
    extern "C"{
        XLIB void testCtypes(int x, float y, bool z){
        printf("func: %s\n", __func__);
        printf("x: %d y: %f z: %d\n", x, y, z);
    }
    }
    // 不需要main
    int main(){
    
        return 0;
    }
    

main.py
    
    
    import ctypes
    from ctypes import c_bool, c_int, c_float
    
    if __name__ == "__main__":
        loader = ctypes.cdll.LoadLibrary
        lib = loader("./foo.so")
        r = lib.foo(1, 2)
        print(r)
        r = lib.testCtypes();
        # ctypes.ArgumentError: argument 2: 
        # TypeError: Don't know how to convert parameter 2
        # 也就是说整型是可以直接转换的，浮点不可以
        try:
            r = lib.testCtypes(1, 2.0, True);
        except Exception as ex:
            print(ex)
        r = lib.testCtypes(c_int(1), c_float(2.0), True)
        p2 = c_int(2)
        print(p2)
        print(type(p2))
        print(p2.value)
    
    
