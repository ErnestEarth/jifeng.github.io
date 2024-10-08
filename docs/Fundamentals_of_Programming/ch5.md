# ch5 分治思想与递归

## 1. 递归

**递归**是一种函数自己调用自己的方式。递归函数需要有**递归边界**（终止条件）。

递归算法的出发点不是在初始条件上，而是在求解目标上，即：从待求的未知项出发，逐次调用本身直到递归边界的求解过程。有许多实际问题往往不可能或很难找到显而易见的递推关系，这时，递归算法就表现出明显的优越性。递归算法比较符合人的思维方式，逻辑性强，可将问题描述得简单扼要，代码可读性强，易于理解。

```cpp
/* 递归算法求 n!
 * n! = n * (n-1)!
 */
int fact(int n)
{
    if (n == 1)				// 递归边界
        return 1;			// 直接返回结果
    return n * fact(n-1);	// n * (n-1)!
}
```

## 2. 分治法

分治法的**设计思想**是：将一个难以直接解决的大问题，分割成一些规模较小的相同问题，以便各个击破，分而治之。

**分治策略**是：对于一个规模为 $n$ 的问题，若该问题可以容易地解决（比如说规模 $n$ 较小）则直接解决，否则将其分解为 $k$ 个规模较小的子问题，这些子问题互相独立且与原问题形式相同，递归地解这些子问题，然后将各子问题的解合并得到原问题的解。

分治法的**精髓**：

- 分 -- 将问题分解为规模更小的子问题；

- 治 -- 将这些规模更小的子问题逐个击破；

- 合 -- 将已解决的子问题合并，最终得出 “母” 问题的解。

分治法所能解决的问题一般具有以下几个**特征**：

1. 该问题的规模缩小到一定的程度就可以容易地解决。
2. 该问题可以分解为若干个规模较小的相同问题，即该问题具有最优子结构性质。
3. 利用该问题分解出的子问题的解可以合并为该问题的解。
4. 该问题所分解出的各个子问题是相互独立的，即子问题之间不包含公共的子问题。

**归并排序**

```cpp
// 对 a 数组下标范围在 [start, end) 的元素进行排序
void MergeSort(int *a, int start, int end)
{
    // 递归终止条件
    if (start == end - 1)
        return;
    // 将两个子数组分开排序
    int mid = (start + end) / 2;
    MergeSort(a, start, mid);
    MergeSort(a, mid, end);
    // 分配临时空间存放合并元素
    int *tmp = new int[end - start];
    // 依次取出子数组的元素，进行合并
    int left = start, right = mid, i = 0;
    while (left < mid && right < end) {
        if (a[left] < a[right])
            tmp[i++] = a[left++];
        else
            tmp[i++] = a[right++];
    }
    // 如果有子数组元素没有取完，则全部并入临时空间
    while (left < mid)
        tmp[i++] = a[left++];
    while (right < end)
        tmp[i++] = a[right++];
    // 从临时空间复制回返回数组中
    for (int i = 0, idx = start; i < end-start; i++, idx++)
        a[idx] = tmp[i];
    // 释放临时空间
    delete[] tmp;
}
```

**快速排序**

```cpp
// 对 a 数组下标范围在 [start, end) 的元素进行排序
void QuickSort(int *a, int start, int end)
{
    if (start == end - 1)
        return;
    // 1. 拆分 -- 选择基准值
    int key = a[start];
    int left = start, right = end - 1;
    while (left < right) {
        // 从右向左找到第一个小于 key 的数
        while (left < right && a[right] > key)
            right--;
        // 将该数存放在 left 的位置
        if (left < right) 
            a[left++] = a[right];
       	// 从左向右找到第一个大于 key 的数
        while (left < right && a[left] < key)
            left++;
        // 将该数存放在 right 的位置
        if (left < right)
            a[right--] = a[left];
    }
    // 2. 将基准值放在 left 的位置
    a[left] = key;
    // 3. 对子数组进行排序
    QuickSort(a, start, left);
    QuickSort(a, left + 1, end);
}
```

## 3. 二维数组

二维数组定义的语法形式：`类型名 数组名[行数][列数];`

```cpp
char message[3][10];		// 用字面值常量定义二维数组

const int M = 5;
const int N = 5;
int matrix[M][N];			// 用符号常量定义二维数组

int like[5][5] = {			// 定义的同时初始化
    {0, 0, 1, 1, 0},
    {1, 1, 0, 0, 1},
    {0, 1, 1, 0, 1},
    {0, 0, 0, 1, 0},
    {0, 1, 0, 0, 1}};
```