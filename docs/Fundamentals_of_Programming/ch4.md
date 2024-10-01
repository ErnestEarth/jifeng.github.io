# ch4 筛法与查找

## 1. 函数初探

**函数**是一个具有特定功能的、相对独立的模块，能够被多次使用。

函数设计的要素：

- 功能：函数的定义

    ```cpp
    /* 
     * bool: 	函数的返回值类型
     * isPrime: 函数的名字
     * int n: 	函数的参数为 n，类型为 int
     */
    bool isPrime(int n)
    {
        bool bPrime = true;
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                bPrime = false;
                break;
            }
        }
        return bPrime;		// 返回一个 bool 类型的值
    }
    ```

- 模块：函数的声明

    ```cpp
    bool isPrime(int);
    ```

    有一个函数，名字叫 `isPrime`，有一个 `int` 的输入，输出为 `bool` 类型。函数的声明必须出现在函数调用之前，一般写在 `main` 函数前面。

- 使用：函数的调用

    ```cpp
    isPrime(n);
    ```

    调用名字为 `isPrime` 的函数，判断 $n$ 是否为素数。

    ![函数](img/%E5%87%BD%E6%95%B0.png)

## 2. 数组

- 数组的定义

    ```cpp
    int number[10];
    ```

    定义了一个大小为 $10$，名称为 `number`，存储 `int` 型数据的数组，相当于定义了 $10$ 个 `int` 类型的变量。

    中括号里面的数必须是整数，并且建议使用常量。**视频中说的必须使用常量，是因为 C++ 标准的不同，较新的标准（比如 C++11）均支持使用变量来定义数组大小，称为变长数组，但是我个人还是建议使用常量。**

- 数组的初始化

    ```cpp
    int number[10] = {0, 21, 2, 13, 4, 7, 9, 7, 8, 15};
    
    // 下面的写法是正确的，编译器会自动计算并补全数组大小
    int number[] = {0, 21, 2, 13, 4, 7, 9, 7, 8, 15};
    
    // 下面的写法是错误的，因为在定义数组时要让编译器知道变量占多少空间
    int number[];
    ```

- 数组的赋值

    数组中的每一项都可以作为独立的变量使用、赋值。

    ```cpp
    number[0] = 5;
    cin >> number[1];
    cout << number[x];
    
    // 下面的写法是错误的，因为除了初始化之外，不能对数组进行直接批量赋值
    number = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
    
    // 下面的写法是正确的，可以利用循环进行批量赋值
    for (int x = 0; x < 10; x++)
        number[x] = x;
    ```

## 3. 埃氏筛流程

1. “筛子” 系统的初始化

2. 枚举 $2$ 到 $\sqrt {100}$ 的每个数 $d$
    - 如果 $d$ 没有被筛掉
        - 用 $d$ 筛掉 $100$ 以内除了 $d$ 之外 $d$ 的倍数

3. 输出所有没有被筛掉的数

```cpp
const int N = 100;		// const 表示定义符号常量
bool seive[N + 1];
for (int i = 2; i <= N; i++)
    seive[i] = true;

for (int d = 2; d * d <= N; d++)
    if (seive[d])
        for (int x = d * d; x <= N; x += d)
            seive[x] = false;

for (int i = 2; i <= N; i++)
    if (seive[i])
        cout << i << " ";
```

## 4. 线性查找

- 扑克牌查找

    1. 初始化 $13$ 张
    2. 假设没有黑桃 $Q$
    3. 依次枚举每一张牌
        - 如果是黑桃 $Q$
            - 记下位置
            - 停止枚举
    4. 如果找到
        - 输出位置
    5. 否则
        - 输出没找到

    ```cpp
    int cards[13] = {101, 113, 303, 206, 405, 208, 311,
                     304, 410, 309, 112, 207, 402};
    int pos = -1;
    for (int i = 0; i < 13; i++) {
        if (cards[i] == 112) {
            pos = i;
            break;
        }
    }
    
    if (pos != -1)
        cout << "黑桃 Q 是第 " << pos + 1 << "张" << endl;
    else
        cout << "没找到" << endl;
    ```

- 最小值查找

    1. 初始化当前最小值及位置
    2. 依次枚举每一张牌
        - 如果比 $7$ 大
            - 如果比最小值还小
                - 更新最小值及位置

    ```cpp
    int min = 100, pos = -1;
    for (int i = 0; i < 13; i++)
        if (cards[i] % 100 > 7 && cards[i] % 100 < min)
            min = cards[i] % 100, pos = i;
    ```

不管是找特定的值，还是找满足特定条件的元素，基本思想还是一个一个依次枚举，比较的次数和总元素的个数呈线性关系，我们称这种查找方法为**线性查找**，也称**顺序查找**。

## 5. 折半查找

在待查序列有序的情况下，可以采用**折半查找**，也称**二分查找**。

1. 初始化查找范围，假设没有黑桃 $Q$
2. 如果范围内有牌，则一直做
    - 选取中间一张
    - 如果中间的牌是黑桃 $Q$
        - 记下位置
        - 停止查找
    - 否则，如果中间的牌比黑桃 $Q$ 大
        - 更新范围，在左侧寻找
    - 否则
        - 更新范围，在右侧寻找

```cpp
int id = -1, low = 0, high = 12;
while (low <= high) {
    int mid = (low + high) / 2;
    if (cards[mid] == 112) {
        id = mid;
        break;
    }
    else if (cards[mid] > 112)
        high = mid - 1;
    else
        low = mid + 1;
}
```

## 6. 排序问题

- 插入排序

    以下插入排序的思路为简化之后的思路，代码更加简介，推荐使用。

    - 枚举每张待插入的牌
        - 枚举从空位置到第一个位置的每一个位置
            - 如果当前位置的元素比待插入的牌大
                - 把当前位置的牌向后挪
            - 否则
                - 把待插入的牌插入到当前位置的后继位置
                - 结束当前插入过程

    ```cpp
    void InsertionSort(int cards[], int n)
    {
        for (int i = 1; i < n; i++) {
            int tag = cards[i];
            for (int j = i-1; j >= 0; j--) {
                if (cards[j] > tag) {
                    cards[j+1] = cards[j];
                }
                else {
                    cards[j+1] = tag;
                    break;
                }
            }
        }
    }
    ```

- 选择排序

    - 枚举每个位置 $i$
        - 假设第 $i$ 个元素最小
        - 枚举位置 $i$ 以后的每个元素 $j$
            - 如果比最小值小
                - 标记最小值为元素 $j$
        - 将最小的牌交换到位置 $i$ 处

    ```cpp
    void SelectionSort(int cards[], int n)
    {
        // 最后一个元素没必要再选择了，因为后面没元素了
        // 换句话讲，单个元素默认有序，这与插入排序中的第一个元素不参与枚举是一致的
    	for (int i = 0; i < n - 1; i++) {
            int min = cards[i], min_id = i;
            for (int j = i + 1; j < n; j++) {
                if (cards[j] < min) {
                    min = cards[j];
                    min_id = j;
                }
            }
            cards[mid_id] = cards[i];
            cards[i] = min;
        }
    }
    ```

    