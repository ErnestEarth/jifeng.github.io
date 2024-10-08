# ch9 可配置的程序设计

## 1. 程序设计

设计程序时可以先设计大功能，然后逐步细化每一个功能，称为**自顶向下，逐步求精**。

可以借助一些编程语言之外的特性辅助程序编写。

编写程序时要注意增强程序的**健壮性**。

```cpp
#include <cstdlib>			// Windows 命令行指令工具

system("pause");			// 暂停，按任意键继续
system("cls");				// 清屏
```

## 2. 命令行参数

```cpp
int main(int argc, char *argv[]);
int main(int argc, char **argv);
```

用命令行参数实现加法。

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

int main(int argc, char *argv[])
{
    if (argc != 3) {
        cout << "Usage: " << argv[0] << " op1 op2" << endl;
        cout << "op1 and op2 are integers." << endl;
        return 0;
    }
    int a, b;
    a = atoi(argv[1]);
    b = atoi(argv[2]);
    cout << a + b < <endl;
    
    return 0;
}
```