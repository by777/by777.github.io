---
layout: post
title: const与static易错点
date: 2024-01-08 21:30:00 +0800
description: const与static易错点
img: post-4.jpg
tags: [cnblogs]
author: Bai Qi
---

# static

1.static 局部变量 将一个变量声明为函数的局部变量，那么这个局部变量在函数执行完成之后不会被释放，而是继续保留在内存中  
2.static 全局变量 表示一个变量在当前文件的全局内可访问  
3.static 函数 表示一个函数只能在当前文件中被访问  
4.static 类成员变量 表示这个成员为全类所共有  
5.static 类成员函数 表示这个函数为全类所共有，而且只能访问静态成员变量

## 作用

（1）函数体内static变量的作用范围为该函数体，该变量的内存只被分配一次，因此其值在下次调用时仍维持上次的值；  
（2）在模块内的static全局变量和函数可以被模块内的函数访问，但不能被模块外其它函数访问；  
（3）在类中的static成员变量属于整个类所拥有，对类的所有对象只有一份拷贝；  
（4）在类中的static成员函数属于整个类所拥有，这个函数不接收this指针，因而只能访问类的static成员变量。

# const

1.const 常量：定义时就初始化，以后不能更改。  
2.const 形参：func(const int a){};该形参在函数里不能改变  
3.const修饰类成员函数：该函数对成员变量只能进行只读操作

## 作用

（1）阻止一个变量被改变  
（2）声明常量指针和指针常量  
（3）const修饰形参，表明它是一个输入参数，在函数内部不能改变其值；  
（4）对于类的成员函数，若指定其为const类型，则表明其是一个常函数，不能修改类的成员变量；  
（5）对于类的成员函数，有时候必须指定其返回值为const类型，以使得其返回值不为”左值”。

> 以上来自https://www.cnblogs.com/wml-it/p/14777414.html

# 易错点

const int *p指针常量，而int *const p常量指针。

  * const int *p：指向常量的指针。


    
    
    #include <iostream>
    using namespace std;
    
    int main()
    {
    	//const int i = 123;
    	int i = 123;
    	const int *ptr = &i; // 指向一个具体类型的常量
    	cout << *ptr << endl;	
    	//*ptr = 321; // 不可通过ptr来修改i的值
    	cout << i << endl;		
    	i = 321; // 若i本身被const限定，则不能修改
    	cout << *ptr << endl;	
    	return 0;
    }
    

  * int *const p：本身是常量的指针  
p本身是const常量（const就近修饰p），不能修改p的内容，但是能通过p来修改它所指向的内容。有点绕是不是？  
这里重新说明一下指针p。p：指针指向的地址 *p：p所指向地址的内容。  
举个栗子，把指针p比作藏宝图：  
p本身是const常量，不能修改p的内容：藏宝图上面具体说明了宝藏藏在什么地方，这个位置不能修改对吧。  
通过p来修改它所指向的内容：但是你不知道宝藏究竟是什么对吧(谁能确保你用藏宝图挖出来的一定是高必而不是高神迹呢[doge])。盗墓贼把真的宝贝(高必)盗走了，把替代品(高神迹)放上去也是可以的吧。（也就是p指向的地址不可以改变，但地址里存放的东西可以改变）


    
    
    #include <iostream>
    using namespace std;
    
    int main()
    {
    	int i = 123;
    	int *const p = &i; // 指针(藏宝图)必须要初始化(有地址)	
    	cout << *p << endl;
    	cout << i << endl;
    	cout << "-----------------" << endl;
    	*p = 321; // 修改指针指向地址的内容
    	cout << *p << endl;
    	cout << i << endl;
    	return 0;
    }
    

> 以上内容来自https://blog.csdn.net/weixin_45045906/article/details/122628644

# const和static
    
    
    #include <iostream>
    using namespace std;
    // 表示常量的几种方式
    // 1. 宏
    // #define VALUE 100
    
    // 2. const
    // const int value = 100;
    
    // 3. 下面等价：指针指向的内容不能透过这个指针来修改它
    // const int * p_int;
    // int const * p_int;
    
    // 4. 指针指向的内容可以被修改，但指针指向的地址不能变 
    // int * const p_int;
    
    // 常常通过这种方式保证指针指向的内容不变
    // void func(const int &);
    // void func(const int *);
    
    // 5. 类里面的const member
    class Student{
        private:
            const int BMI = 24;
            int born = 0;
            // 静态成员和函数是不绑定某一个实例上的
            // 无论有多少个对象，即使是0个，都会有静态成员
            static size_t student_total; //  只声明
            // inline static size_t student_total = 0; 
    // 更方便的写法，C++17标准，可以防止报链接错误
    
        public:
            Student(){
                // BMI = 25 ; const成员变量不能修改，会报错
                student_total ++;
                cout<<"+++"<< student_total<<endl;
            }
            ~Student(){
                student_total --;
                cout<<"---"<< student_total<<endl;
            }
            static size_t getTotal(){
                // born = 0; 私有变量born可能没有生成，不能在静态函数里操作，会编译报错
                return student_total;}
            int getBorn() const{ // const 放到这里为了不和返回值混淆
                // born ++;// const 员函数不能修改成员变量，会报错
                return born;
            }
    };
    // 在这里定义
    size_t Student::student_total = 0;// 如果这里忘记写，可能会报链接错误
    int main(){
        Student *class1 = new Student[3];
        size_t total = Student::getTotal();
        cout<<total<<endl;
        delete [] class1;
    
        total = Student::getTotal();
        cout<<total<<endl;
    
        return 0;
    }
    
