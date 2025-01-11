### 1. 选择排序

先从整个数组中找到最小的，放在第一位

从第二位到最后这个范围找小的，放在第二位

以此类推

| 原数组 |  7   |  4   |  2   |  5   |  1   |
| :----: | :--: | :--: | :--: | :--: | :--: |
| 第一次 |  1   |  4   |  2   |  5   |  7   |
| 第二次 |  1   |  2   |  4   |  5   |  7   |
| 第三次 |  1   |  2   |  4   |  5   |  7   |
| 第四次 |  1   |  2   |  4   |  5   |  7   |

```C++
// 一本通写法
#include<bits/stdc++.h>
using namespace std;

const int MAXN = 10001;
int main() {
	int n, k, i, j;
	float temp, a[MAXN];
	cin >> n;
	for (int i = 1; i <= n; i++)
	{
		cin >> a[i];
	}
	for (int i = 1; i <= n; i++)
	{
		k = i;
		for (int j = i + 1; j <= n; j++)
		{
			if (a[j] < a[k]) k = j;
		}
		if (k != i)
		{
			temp = a[i];
			a[i] = a[k];
			a[k] = temp;
		}
	}
	for (int i = 1; i <= n; i++)
	{
		cout << a[i] << " ";
	}
	
	return 0;
}
```

```C++
// 常规写法
#include<bits/stdc++.h>
using namespace std;

int main() {
	int n, a[100] = {};
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> a[i];
	}
	for (int i = 0; i < n - 1; i++)  // 只需要遍历到倒数第二位就好
	{
		int min = a[i];
		int minIndex = i;
		for (int j = i; j < n ; j++)
		{
			if (min > a[j])
			{
				min = a[j];
				minIndex = j;
			}
		}
		if (minIndex != i) 
		{
			a[minIndex] = a[i];
			a[i] = min;
		}
	}

	for (int i = 0; i < n; i++)
	{
		cout << a[i] << " ";
	}
	
	return 0;
}
```



### 2. 冒泡排序

依次与所有数进行比较，时间复杂度是$O(n^2)$

冒泡用上了双重for循环，外层循环第一次循环找到最大的数，第二次找第二大的数，依次类推

内层循环每次都和后一位进行比较，如果需要就交换。

|       原数组       |  7   |  4   |  2   |  5   |  1   |
| :----------------: | :--: | :--: | :--: | :--: | :--: |
| 第一次冒泡7和4比较 |  4   |  7   |  2   |  5   |  1   |
| 第二次冒泡7和2比较 |  4   |  2   |  7   |  5   |  1   |
| 第三次冒泡7和5比较 |  4   |  2   |  5   |  7   |  1   |
| 第四次冒泡7和1比较 |  4   |  2   |  5   |  1   |  7   |
| 第五次冒泡4和2比较 |  2   |  4   |  5   |  1   |  7   |
| 第六次冒泡4和5比较 |  2   |  4   |  5   |  1   |  7   |
| 第七次冒泡5和1比较 |  2   |  4   |  1   |  5   |  7   |
| 第八次冒泡2和4比较 |  2   |  4   |  1   |  5   |  7   |
| 第九次冒泡4和1比较 |  2   |  1   |  4   |  5   |  7   |
| 第十次冒泡2和1比较 |  1   |  2   |  4   |  5   |  7   |

结束

```C++
#include<bits/stdc++.h>
using namespace std;

int main() {
	int n, a[100] = {};
	cin >> n;
	for (int i = 0; i < n; i++) cin >> a[i];

	for (int i = 0; i < n - 1; i++)  // -1是因为交换只需要到倒数第二位
	{
		for (int j = 0; j < n - i - 1; j++)
		{
			if (a[j] > a[j + 1])
			{
				/*int temp = a[j];
				a[j] = a[j + 1];
				a[j + 1] = temp;*/
				swap(a[j], a[j + 1]);
			}
		}
	}

	for (int i = 0; i < n; i++)
	{
		cout << a[i] << " ";
	}
	
	return 0;
}
```

```C++
// 改进
#include<bits/stdc++.h>
using namespace std;

int main() {
	int n, a[100] = {};
	cin >> n;
	for (int i = 0; i < n; i++) cin >> a[i];

	bool flag = true; // 设定一个bool，如果有交换就false
	for (int i = 0; i < n - 1; i++)  // -1是因为交换只需要到倒数第二位
	{

		for (int j = 0; j < n - i - 1; j++)
		{
			if (a[j] > a[j + 1])
			{
				swap(a[j], a[j + 1]);
				flag = false;
			}
		}
		if (flag) break;
	}

	for (int i = 0; i < n; i++)
	{
		cout << a[i] << " ";
	}

	return 0;
}
```





### 3. 插入排序

我们把前面的几位看成顺序数组

|                       原数组                       |  7   |  4   |  2   |  5   |  1   |
| :------------------------------------------------: | :--: | :--: | :--: | :--: | :--: |
|                  把7看成顺序数组                   |  7   |  4   |  2   |  5   |  1   |
| 7和4进行比较，需要调换，调换完成把4和7看做顺序数组 |  4   |  7   |  2   |  5   |  1   |
|      2和7比较，需要调换，把2的位置直接替换成7      |  4   |  7   |  7   |  5   |  1   |
|       4和2比较，同样需要调换，把7的位置换成4       |  4   |  4   |  7   |  5   |  1   |
|         把0的位置替换成2，把2,4,7看成整体          |  2   |  4   |  7   |  5   |  1   |
|                 5和7比较，需要调换                 |  2   |  4   |  7   |  7   |  1   |
| 4和5比较，不需要替换，把7换成5，把2,4,5,7看成整体  |  2   |  4   |  5   |  7   |  1   |
|                 1和7比较，需要替换                 |  2   |  4   |  5   |  7   |  7   |
|                 1和5比较，需要替换                 |  2   |  4   |  5   |  5   |  7   |
|                 1和4比较，需要替换                 |  2   |  4   |  4   |  5   |  7   |
|                 1和2比较，需要替换                 |  2   |  2   |  4   |  5   |  7   |
|                  把0的位置替换成1                  |  1   |  2   |  4   |  5   |  7   |

完成

难点就是把本位的位置替换成前一个数，这个想明白了就很清楚了

```C++
#include<bits/stdc++.h>
using namespace std;

int main() {
	int n, a[100] = {};
	cin >> n;
	for (int i = 0; i < n; i++) cin >> a[i];

	for (int i = 1; i < n; i++) // 从1开始，1才是我们要判断的数
	{
		int insertVal = a[i]; // 指需要排序的数
		int sortIndex = i - 1; // 指排好序的最后一位数的下标
		while (sortIndex >= 0 && insertVal < a[sortIndex])
		{
			a[sortIndex + 1] = a[sortIndex];
			sortIndex--;  // 向后走一位，如果需要插入的值是在排好序的中间部分
		}
		// 如果找到了需要插入的位置
		a[sortIndex+1] = insertVal;
	}
	
	for (int i = 0; i < n; i++)
	{
		cout << a[i] << " ";
	}

	return 0;
}
```



### 4. 桶排序





### 5. 快速排序

```C++
#include <iostream>
using namespace std;
// 快速排序函数声明
void qsort(int arr[], int l, int r);

int main() {
  
    int n;
    cin >> n;

    // int* a = new int[n];
    int a[1000] = {};

    for (int i = 0; i < n; i++) cin >> a[i];

    qsort(a, 0, n - 1);

    for (int i = 0; i < n; i++) cout << a[i] << " ";


    // delete[] a;
    return 0;
}

// 快速排序函数定义
void qsort(int arr[], int l, int r) {
    int i, j, mid, temp;
    i = l;
    j = r;
    mid = arr[(l + r) / 2];

    do {
        while (arr[i] < mid) i++;
        while (arr[j] > mid) j--;
        if (i <= j) {
            temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;
            j--;
        }
    } while (i <= j);

    if (l < j) qsort(arr, l, j);
    if (i < r) qsort(arr, i, r);
}
```



### 6. 归并排序

```C++
#include <iostream>
int a[100];
int r[100];

// 归并排序函数
// s - 开始下标   t - 结束下标
void msort(int s, int t) {
    
    if (s == t) return; // 如果只有一个数字则返回，无须排序
    int mid = (s + t) / 2;     // 计算中间位置

    msort(s, mid); // 递归地对左半部分序列进行排序
    msort(mid + 1, t); // 递归地对右半部分序列进行排序

    // i -左边的开始下标    j-右边的开始下标    k-临时数组r的开始下标
    int i = s, j = mid + 1, k = s;

    // 当左半部分和右半部分都有未处理的元素时
    // i - 左边的开始下标  mid - 左边的结束下标
    // j - 右边的开始下标  t - 右边的结束下标（刷组的结束下标）
    while (i <= mid && j <= t) {
        // 如果左半部分当前元素小于等于右半部分当前元素
        if (a[i] <= a[j]) {
            // 将左半部分当前元素放入临时数组 r 中
            r[k] = a[i];
            // 移动临时数组 r 的索引和左半部分的索引
            k++;
            i++;
        }
        else {
            // 将右半部分当前元素放入临时数组 r 中
            r[k] = a[j];
            // 移动临时数组 r 的索引和右半部分的索引
            k++;
            j++;
        }
    }


    // 如果左边下标走完或者右边下标走完
    // 上方的while循环进不去了，说明有一边的有序数组完成
    
    // 复制左边子序列剩余的元素
    while (i <= mid) {
        r[k] = a[i];
        k++;
        i++;
    }

    // 复制右边子序列剩余的元素
    while (j <= t) {
        r[k] = a[j];
        k++;
        j++;
    }

    // 将临时数组 r 中的元素复制回原数组 a
    for (int i = s; i <= t; i++) {
        a[i] = r[i];
    }

    return;
}

int main() {
    // 示例数组初始化
    int n = 5;
    a[0] = 3;
    a[1] = 1;
    a[2] = 4;
    a[3] = 2;
    a[4] = 5;

    // 调用归并排序函数
    msort(0, n - 1);

    // 输出排序后的数组
    for (int i = 0; i < n; ++i) {
        std::cout << a[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

#### 6.1. 逆序对



### 7. 基数排序

```C++
#include <iostream>
#include <cmath>

using namespace std;

// 获取数组中的最大值
int getMax(int arr[], int n) {
    int max = arr[0];
    for (int i = 1; i < n; ++i) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

// 基数排序的辅助函数，对数组按指定数位进行排序
void countingSort(int arr[], int n, int exp) {
    // 使用动态内存分配创建输出数组
    int* output = new int[n];
    int count[10] = { 0 };

    // 统计每个数位上的数字出现的次数
    for (int i = 0; i < n; ++i) {
        count[(arr[i] / exp) % 10]++;
    }

    // 计算累计计数
    for (int i = 1; i < 10; ++i) {
        count[i] += count[i - 1];
    }

    // 构建输出数组
    for (int i = n - 1; i >= 0; --i) {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }

    // 将输出数组复制回原数组
    for (int i = 0; i < n; ++i) {
        arr[i] = output[i];
    }

    // 释放动态分配的内存
    delete[] output;
}

// 基数排序主函数
void radixSort(int arr[], int n) {
    int max = getMax(arr, n);

    // 对每一位进行计数排序
    for (int exp = 1; max / exp > 0; exp *= 10) {
        countingSort(arr, n, exp);
    }
}

int main() {
    int arr[] = { 170, 45, 75, 90, 802, 24, 2, 66 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "原始数组: ";
    for (int i = 0; i < n; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;

    radixSort(arr, n);

    cout << "排序后的数组: ";
    for (int i = 0; i < n; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```



### 8. 计数排序

```C++
#include <iostream>

using namespace std;

// 计数排序函数
void countingSort(int arr[], int n) {
    // 找到数组中的最大值和最小值
    int maxVal = arr[0];
    int minVal = arr[0];
    for (int i = 1; i < n; ++i) {
        if (arr[i] > maxVal) {
            maxVal = arr[i];
        }
        if (arr[i] < minVal) {
            minVal = arr[i];
        }
    }

    // 计算计数数组的范围
    int range = maxVal - minVal + 1;
    int* count = new int[range]();

    // 统计每个元素的出现次数
    for (int i = 0; i < n; ++i) {
        count[arr[i] - minVal]++;
    }

    // 计算累计计数
    for (int i = 1; i < range; ++i) {
        count[i] += count[i - 1];
    }

    // 创建输出数组
    int* output = new int[n];

    // 构建输出数组  反向保证稳定性
    for (int i = n - 1; i >= 0; --i) {
        output[count[arr[i] - minVal] - 1] = arr[i];
        count[arr[i] - minVal]--;
    }

    // 将输出数组复制回原数组
    for (int i = 0; i < n; ++i) {
        arr[i] = output[i];
    }

    // 释放动态分配的内存
    delete[] count;
    delete[] output;
}

int main() {
    int arr[] = {4, 2, 2, 8, 3, 3, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "原始数组: ";
    for (int i = 0; i < n; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;

    countingSort(arr, n);

    cout << "排序后的数组: ";
    for (int i = 0; i < n; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```



### 9. 希尔排序



### 10. 堆排序

