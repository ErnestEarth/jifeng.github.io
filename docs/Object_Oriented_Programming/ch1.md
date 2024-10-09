# ch1 课程简介与编程环境

## 1. 教学定位与内容

前驱课程：《程序设计基础》

后继课程：《数据结构》、《软件工程》

编程需要的基础：

- 算法基础：问题的分析、表示、求解的方法，变量、判断、循环、函数的应用
- 语言基础：如何定义和实现算法中的元素，语法规范
- 系统基础：操作系统运作的内在机制，操作系统提供的底层功能调用库
- 特定技术：网络通信、硬件接口
- 设计的方法论：结构化，基于对象、面向对象，泛型，组件，越是复杂的任务，设计的方法越重要

学习方法：

- 多查、多看相关书籍、网站等
- 多练习，多用程序验证自己的理解
- 自己始终理解不了的就多问
- 多思考和理解高层的抽象方法，以及底层的运行机制
- 多归纳和整理自己所得

## 2. 编译程序

源程序 $\to$ 编译器 $\to$ 链接器 $\to$ 可执行程序（与平台相关的机器指令）

以 Mac 系统为例，相关指令如下：

```sh
g++ -c ex1.cpp;			# 编译，生成 .o 文件
g++ -o ex1.out ex1.o	# 链接，指定生成 .out 文件
./ex1.out				# 运行
```

## 3. 编译多文件

当源程序文件很大时，我们可以将其拆分成多个源文件，并且将声明与定义分开到不同的文件。

```cpp
// main.cpp
#include <iostream>
#include <cstdio>
#include "func.h"		// ADD()

int main(int argc, char** argv)
{
    if (argc != 3) {
        std::cout << "Usage: " << argv[0] << " op1 op2" << std::endl;
        return 1;
    }
    int a, b;
    a = atoi(argv[1]);
    b = atoi(argv[2]);
    std::cout << ADD(a, b) << std::endl;
    
    return 0;
}
```

```cpp
// func.h
// 增加预编译指令，放置重复包含导致的编译错误
#ifndef FUNC_H
#define FUNC_H
int ADD(int, int);
#endif
```

```cpp
// func.cpp
#include "func.h"
int ADD(int a, int b)
{
	return a + b;
}
```

可以使用 `make` 工具进行多个源文件的编译和链接。下面是一个 `Makefile` 文件示例：

```sh
# Makefile
# Example for C++ Course							# 注释

all: main.exe test.exe								# 冒号前面是任务

main.exe: main.cpp student.cpp						# 冒号后面是任务条件
	g++ -o main.exe main.cpp student.cpp			# 缩进只能用制表符

test.exe: student.cpp student_test.cpp
	g++ -o test.exe student_test.cpp student.cpp

clean:
	del *.obj *.exe
```

执行 `Makefile` 的基本方法：

```sh
make						# 默认执行第一个任务

make clean					# 执行 clean 任务
make test.exe

make -f my_mkfile			# 指定 Makefile 文件为 my_mkfile

make -f my_mkfile test.exe	# 指定 Makefile 与任务
```