# ch7 文本数据处理

## 1. 文件操作

```cpp
#include <iostream>
#include <fstream>					// 包含文件操作的头文件
using namespace std;

int main()
{
    // 创建一个输入文件的操作对象 fin，并打开名为 log.txt 的文本文件
    // 如果需要写入文件，则用 ofstream 定义输出文件的操作对象
	ifstream fin("log.txt");		// ifstream 表示 input file stream
    // 也可以用 fin.open("log.txt"); 打开文件
	int count = 0;					// 记录数，初始值为0
	while (!fin.eof())				// eof 表示 end of file
	{
		int year, month, day, hour, minute, second;
		char tmp, id[20], operation[10];
		// 通过 fin 获取文本文件中的内容
		fin >> year >> tmp >> month >> tmp >> day;		// 2015/4/21
		fin >> hour >> tmp >> minute >> tmp >> second;	// 11:16:16
        fin >> id;										// 40dbae14f777cdd
		fin >> operation;								// LOGIN
        count++;					// 读到一行，记录数加1
    }
    fin.close();					// 关闭文件
    cout << count << endl;			// 输出记录数
    return 0;
}

```

## 2. 字符串

字符数组的两种等价的初始化方法：

```cpp
char str[10] = "Hello";
char str[10] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

字符串可以整体输入输出：

```cpp
cin >> str;
cout << str << endl;
```

常用字符串操作函数：

```cpp
#include <cstring>		// 需要包含字符串操作相关头文件

int len = strlen(str);	// 求字符串 str 的长度，注意不是数组长度
strcpy(str1, str2);		// 将字符串 str2 复制到 str1 中
strcmp(str1, str2);		// 比较字符串 str1 和 str2 的大小，按照字典序进行比较
strcat(str1, str2);		// 将字符串 str2 拼接到 str1 后面
```

字符串数组：

```cpp
char strs[4][10] = {
    "Hello",
    "world",
    "C++",
    "!"
}

cout << strlen(strs[2]);	// 输出结果为 3
```

## 3. 结构体

结构体实际上是一种自定义数据类型。

```cpp
struct Time_t {
    int year, month, day;
    int hour, minute, second;
};

Time_t a;					// 定义了一个类型为 Time_t 的变量 a
Time_t b = { 
    2024, 10, 8, 8, 0, 0	// 按顺序做初始化
};
Time_t c[20];				// 也可以定义数组

a.year = 2015;				// 访问变量 a 中的成员变量 year 并赋值
cout << a.year;
cin >> a.year;
int x = b.year - a.year;
```

