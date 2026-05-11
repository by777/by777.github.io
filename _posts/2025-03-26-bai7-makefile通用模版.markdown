---
layout: post
title: makefile通用模版
date: 2025-03-26 14:49:00 +0800
description: makefile通用模版
img: post-5.jpg
tags: [cnblogs]
author: Bai Qi
---

来源：[知乎](<https://zhuanlan.zhihu.com/p/618350718>)
    
    
    ROOT := $(shell pwd)
    
    SUBDIR := $(ROOT)
    
    # func里是子函数和其头文件
    SUBDIR += $(ROOT)/func
    
    TARGET := $(ROOT).exe
    OUTPUT := ./output
    
    # INCS变量生成包含路径选项，用于指定头文件的搜索路径。这里使用foreach循环为每个子目录生成-I选项。
    INCS := $(foreach dir,$(SUBDIR),-I$(dir))
    
    # SRCS变量收集所有子目录下的C源文件。wildcard函数用于匹配每个子目录下的*.c文件。
    SRCS := $(foreach dir,$(SUBDIR),$(wildcard $(dir)/*.c))
    
    # OBJS变量将源文件路径转换为输出目录中的目标文件路径。
    # 例如，$(ROOT)/func/example.c将转换为$(OUTPUT)/func/example.o。
    OBJS := $(patsubst $(ROOT)/%.c,$(OUTPUT)/%.o,$(SRCS))
    
    # DEPS变量生成依赖文件的列表，这些文件用于存储每个目标文件的依赖关系。
    DEPS := $(patsubst %.o,%.d,$(OBJS))
    
    $(TARGET) : $(OBJS)
    		@gcc $(OBJS) -o $@
    
    
    # gcc -MMD -MP -c命令编译源文件并生成目标文件，同时生成依赖文件（.d文件）
    # 可以有效避免删除头文件时，Makefile 因找不到目标来更新依赖所报的错
    # 在 Makefile 中，这些依赖文件会被包含进来，以便在头文件更新时自动触发相应的源文件重新编译。
    
    # $<：Makefile中的自动变量，表示规则中的第一个源文件。
    # $@： 表示当前规则的目标文件名
    
    # %：用于Makefile中的规则和模式匹配，如 patsubst 和规则中的目标和依赖项。
    # *：用于Shell命令和文件路径匹配，如 wildcard 函数中的文件名匹配
    
    # $(dir $@) 是一个Makefile函数，用于提取目标文件的目录部分。
    # 例如，如果目标文件是 ./output/src/example.o，那么 $(dir $@) 的值将是 ./output/src/
    
    $(OUTPUT)/%.o : %.c
    		@mkdir -p $(dir $@)
    		@gcc -MMD -MP -c $(INCS) $< -o $@
    
    .PHONY : clean
    clean:
    		@rm -r $(OUTPUT)
    
    # -include 是 Makefile 中的一个指令，用于包含其他文件的内容。
    # 如果指定的文件不存在，Makefile不会报错，只是简单地跳过。
    # 在 Makefile 中，这行代码通常用于支持增量编译。
    # 通过包含依赖文件，Makefile 可以知道哪些文件需要重新编译，从而提高编译效率。
    -include $(DEPS)
    
