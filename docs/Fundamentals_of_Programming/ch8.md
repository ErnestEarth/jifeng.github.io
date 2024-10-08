# ch8 非文本数据处理

## 1. 链表

对于数据量事先无法预知的情况，可以用链式结构进行数据的组织，称为**链表**。

```cpp
struct Node {
    Time_t tm;
    char id[20], op[20];
    Node* next;
}

// 链表的创建过程
Node *head = NULL;				// 建立链表头指针
while (...) {
    Node *data = new Node;		// 从内存中动态申请新结点空间

    cin >> data->tm.year;		// 注意结构体指针与结构体访问成员变量的运算符不一样

    data->next = head;			// 采用头插法将新结点插入链表表头
    head = data;
}

// 遍历链表
int cnt = 0;
while (head) {
    cout << cnt << " " << head->id << endl;
    cnt++;
    head = head->next;
}

// 释放链表
while (head) {
    Node *p = head;
    head = head->next;
    delete p;
}
```

## 2.  哈希算法

一种将字符串映射成整数的简单哈希算法。

```cpp
// 累加异或得到哈希值
int Hash(const char *str)
{
	int sum = 0;
	for (int i = 0; i < strlen(str); i++)
		sum ^= str[i];
    return sum;
}
```

## 3. 二进制文件的操作

```cpp
// 文件对象的定义
ifstream fin(filename, ios::binary);
ofstream fout(filename, ios::binary);

// 数据的读取与写入操作
fin.read((char*) &(data), sizeof(data));
fout.write((char*) &(data), sizeof(data));

// 以下为示例代码
void SaveHashTab(Node *hash_tab[], const char *filename) {
	ofstream fout(filename, ios::binary);

	for (int i = 0; i < 256; i++) {
		Node *p = hash_tab[i];
		while (p) {
			fout.write((char*)&(p->log), sizeof(p->log));
			p = p->next;
		}
	}
	fout.close();
}

void LoadHashTab(Node *hash_tab[], const char *filename) {
	ifstream fin(filename, ios::binary);
	while(fin) {
		Node data;
		fin.read((char*) &(data.log), sizeof(data.log));
		if (fin.eof()) {
			break;
		}
		Insert(hash_tab, data);
	}
	fin.close();
}
```