# ch2 基础语法（1）

## 1. 变量定义

`auto` 变量：由编译器根据上下文自动确定变量的类型，如：

```cpp
auto i = 3;					// i 是 int 型变量
auto f = 4.0f;				// f 是 float 型变量
```

指针变量的动态生成与删除：

```cpp
int *ptr = new int;			// 单个变量
int *array = new int[10];	// 10 元素数组
delete ptr;					// 删除单个内存单元
delete[] array;				// 删除多个单元组成的内存块
```

左值引用：是一个具名变量的别名

- **引用必须在定义时进行初始化**
- 被引用变量名可以是结构体变量成员
- 函数参数可以是引用类型，表示函数的形式参数与实际参数是同一个变量，改变形参将改变实参
- 函数返回值可以是引用类型，但不得是函数的临时变量

```cpp
int v0;
int &v1 = v0;				// v1 是变量 v0 的引用，它们在内存中是同一个单元
```

右值引用：不能取地址的、没有名字的就是右值，如：

```cpp
int &&sum = 3 + 4;
float &&res = ReturnRvalue(f1, f2);

// 一般应用在函数参数中，目的是减少临时变量拷贝的开销
void AcceptRvalueRef(T && s) {...}
```

## 2. 初始化列表

用花括号 `{}` 括起来的元素序列，可以用来对变量进行初始化，称为初始化列表：

```cpp
int a[] = {1, 2, 3};
int a[]{1, 3, 5};

int a = 3 + 5;
int a = {3 + 5};
int a(3 + 5);
int a{3 + 5};
int *i = new int(10);
double *d = new double{1.2f};
```

## 3. 变量的类型推导

使用 `decltype` 可以对变量或表达式结果的类型进行推导：

```cpp
struct { char *name; } anon_u;		// 匿名 struct 变量
struct {
    int d;
    decltype(anon_u) id;
} anon_s[100];						// 匿名 struct 数组

int main()
{
    decltype(anon_s) as;
    cin >> as[0].id.name;
    ...
}
```

## 4. 范围 `for` 语句

```cpp
int arr[3] = {1, 2, 3};
for (int e : arr) {			// e 是迭代变量，arr 是迭代范围
    cout << e << " ";
}

for (auto k : arr) {
    cout << k << " ";
}
```

## 5. 函数重载

同一名称的函数，有两个以上不同的实现，称为 “函数重载”。**函数重载必须保证函数参数不一样**（**数量**或**类型**不一样）。编译器将根据函数调用语句的实参来决定调用哪一个函数。

```cpp
void print(char *msg) {
    cout << "message: " << msg << endl;
}

void print(int score) {
    cout << "score = " << score << endl;
}
```

## 6. 默认值参数

函数参数可以在定义时设置默认值（缺省值），这样在调用该函数时，若不提供相应的实参，则编译器自动将相应形参设置成默认值。注意默认值参数必须定义在位置参数之后。

```cpp
void print(char *msg = "hello")
{
    cout << msg << "#";
}

void print(char *name, int score, char *msg = "pass") 
{
    cout << name << ": " << score << ", " << msg << endl;
}

int main()
{
    print("Beijing...");		// 输出 Beijing...#
    print();					// 输出 hello#
    return 0;
}
```

## 7. 追踪返回类型的函数

可以将函数返回类型的声明信息放到函数参数列表的后面进行声明，在原本函数返回值的位置使用 `auto`。

```cpp
auto func(char *ptr, int val) -> int;
```

## 8. 类的定义

与结构体类似，类也是一种自定义数据类型。类中包含的函数，称为 “成员函数”，包含的数据，称为 “数据成员”。类中的函数既可以在类中给出定义，也可以在类外给出定义。类的成员可以根据需要分组，不同组设置不同的访问权限：

- `public`：公有属性
- `private`：私有属性，这是 `class` 中成员的默认属性
- `protected`：保护属性

定义类后，可以像语言内建的类型一样，用类来定义变量，该变量通常被称为 “对象”。通过 `对象名.成员名` 的形式，可以使用对象的数据成员，或调用对象的成员函数，但仅限于访问 `public` 权限的成员。在类外定义成员函数时，函数名前要加上类名限定，格式为：`类名::函数名`，`::` 称为**域运算符**。

```cpp
// matrix.h
#ifndef MATRIX_H
#define MATRIX_H

class Matrix {
    int data[6][6];
public:
    void fill(char dir);
};

#endif
```

所有成员函数的参数中，隐含着一个指向当前对象的指针变量，名称为 `this`。

```cpp
// matrix.cpp
#include "matrix.h"

// 函数实现
void Matrix::fill(char dir)
{
    this->data[0][0] = 1;		// 等价于 data[0][0] = 1;
    ...
}
```

不允许用 `.` 操作符访问对象的私有成员和保护成员，对象只能访问它的公有成员。

```cpp
// main.cpp
#include "matrix.h"

int main()
{
    Matrix obj;					// 定义对象
    obj.fill('u');				// 访问公有成员
    obj.data[1][2] = 23;		// ERROR!
    
    Matrix *ptr = new Matrix;	// 定义对象指针
    ptr->fill('u');				// 访问公有成员
    ptr->data[1][1] = 23;		// ERROR!
    delete ptr;
    
    return 0;
}
```

## 9. 友元

有时需要允许某些函数访问对象的私有成员，可以通过声明该函数为类的 “友元” 来实现。

```cpp
#include <iostream>
using namespace std;

class Test {
    int id;
public:
    friend void print(Test obj);	// 声明友元函数 print
    ...
};

void print(Test obj)
{
    cout << obj.id << endl;
}
```