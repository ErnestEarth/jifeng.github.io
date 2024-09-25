# 一、编程初步

#### [返回](./index.md)

1. 什么是程序？什么是语言？

    为了得到某种结果，通过计算机**语言**表达的指令序列。

    计算机语言是为了与计算机进行沟通而设计出来的语言。

2. **计算思维**解题的特点？

    - 满足计算机程序执行的规则约束
    - 发挥计算机的特长

3. 冯诺依曼体系结构

    ![image-20240921224440003](https://gitee.com/clancisa/pictures/raw/master/image-20240921224440003.png)

4. 数学运算

    ![image-20240921225344631](https://gitee.com/clancisa/pictures/raw/master/image-20240921225344631.png)

5. 数学函数

    ![image-20240921225813449](https://gitee.com/clancisa/pictures/raw/master/image-20240921225813449.png)

    ![image-20240921230156596](https://gitee.com/clancisa/pictures/raw/master/image-20240921230156596.png)

6. 程序基本结构中的含义

    ![image-20240921231021671](https://gitee.com/clancisa/pictures/raw/master/image-20240921231021671.png)

    - 包含库函数
        - 以符号 `#` 开头的行，称为预编译行
        - `#include` 称为文件包含命令
        - `#include <iostream>` 这条命令是让文件 `iostream` 的内容包含到新建的程序中去
        - `iostream` 是 C++ 语言提供的一个头文件，在这个头文件中设置了 C++ 的输入 / 输出相关环境，只有包含了这个头文件才能使用 `cout` 对象
    - 命名空间
        - `using namespace` 称为使用命名空间命令，是为避免同名冲突而引入的
        - `std` 是 `iostream` 文件中定义的一个命名空间，由它定义了 C++ 的库标识符，比如 `cout` 等
        - 有了 `using namespace std;` 这句话，程序就可以直接使用 `std` 命名空间里面的标识符了
    - 主函数
        - `int main()` 是每一个 C++ 程序都必须有的，称为主函数，可以把它看成是程序的入口
        - 符号 `{`  和 `}` 之间的部分是主函数的内容，分别表示主函数开始和结束
        - 在 `main` 前面的 `int` 是标准 C++ 所规定的，对应于在主函数结束前的 `return 0;`
    - 标准输出
        - `cout` 为标准输出流对象，与显示器关联
        - `cout` 允许使用操作符 `<<` 将数据交给标准输出进行输出
        - `endl` 表示换行
    - 语句
        - 每条语句结尾必须有 `;`，表示语句结束

7. 格式与风格

    ![image-20240921232212765](https://gitee.com/clancisa/pictures/raw/master/image-20240921232212765.png)

    ![image-20240921232300313](https://gitee.com/clancisa/pictures/raw/master/image-20240921232300313.png)

8. 怎样学好程序设计？

    - 重思路
    - 勤动手
    - 敢于提问
    - 学会阅读

#### [返回](./index.md)