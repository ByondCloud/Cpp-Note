### 一、复习

#### 1. 打印乘法表（必做）

用for循环实现输出1至9的乘法表

```C++
// 输出用例
1*1=1
1*2=2 2*2=4
1*3=3 2*3=6 3*3=9
1*4=4 2*4=8 3*4=12 4*4=16
1*5=5 2*5=10 3*5=15 4*5=20 5*5=25
1*6=6 2*6=12 3*6=18 4*6=24 5*6=30 6*6=36
1*7=7 2*7=14 3*7=21 4*7=28 5*7=35 6*7=42 7*7=49
1*8=8 2*8=16 3*8=24 4*8=32 5*8=40 6*8=48 7*8=56 8*8=64
1*9=9 2*9=18 3*9=27 4*9=36 5*9=45 6*9=54 7*9=63 8*9=72 9*9=81
```

```C++
#include <iostream>
using namespace std;
int main()
{
	for (int i = 1; i <= 9; i++)
	{
		for (int j = 1; j <= i; j++)
		{
			cout << j << "*" << i  << "=" << i * j << " ";
		}
		cout << endl;
	}
	return 0;
}
```

#### 2. 矩阵交换（必做）

一给定一个5*5的矩阵（数学上，一个r×c的矩阵是一个由r行c列元素排列成的矩形阵列），将第n列和第m列交换，输出交换后的结果。

输入：输入共6行，前5行为矩阵的每一行元素,元素与元素之间以一个空格分开。第6行包含两个整数m、n（1 <= m,n< = 5），以一个空格分开

输出：输出交换之后的矩阵，矩阵的每一行元素占一行，元素之间以一个空格分开。

```C++
// 输入样例
1 2 2 1 2
5 6 7 8 3
9 3 0 5 3
7 2 1 4 6
3 0 8 2 4
1 5
```

```C++
// 输出样例
2 2 2 1 1
3 6 7 8 5
3 3 0 5 9
6 2 1 4 7
4 0 8 2 3
```

```C++
#include <iostream>
using namespace std;
int main()
{
	int arr[5][5];
	for (int i = 0; i < 5; i++)
	{
		for (int j = 0; j < 5; j++)
		{
			cin >> arr[i][j];
		}
	}
	int m, n;
	cin >> m >> n;
	m -= 1;
	n -= 1;
	for (int i = 0; i < 5; i++)
	{
		for (int j = 0; j < 5; j++)
		{
			if (j == m)
			{
				int temp = arr[i][m];
				arr[i][m] = arr[i][n];
				arr[i][n] = temp;
			}
		}
	}
	for (int i = 0; i < 5; i++)
	{
		for (int j = 0; j < 5; j++)
		{
			cout << arr[i][j] << " ";
		}
		cout << endl;
	}
	return 0;
}
```

#### 3. 打印杨辉三角形

打印杨辉三角的前10行

```C++
// 输出样例
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
1 5 10 10 5 1
1 6 15 20 15 6 1
1 7 21 35 35 21 7 1
1 8 28 56 70 56 28 8 1
1 9 36 84 126 126 84 36 9 1
```

```C++
#include <iostream>
using namespace std;
int main()
{
	int arr[11][11];
	for (int i = 1; i <= 10; i++)
	{
		for (int j = 1; j <= i; j++)
		{
			if (j == 1 || j == i)
			{
				arr[i][j] = 1;
			}
			else {
				arr[i][j] = arr[i - 1][j - 1] + arr[i - 1][j];
			}
		}
	}
	for (int i = 1; i <= 10; i++)
	{
		for (int j = 1; j <= i; j++)
		{
			cout << arr[i][j] << " ";
		}
		cout << endl;
	}
	
	return 0;
}
```

#### 4. 正立的三角形

```C++
// 输出用例
1110111
1100011
1000001
0000000
```

```C++
#include <iostream>
using namespace std;
int main()
{
	for (int i = 1; i <= 4; i++)
	{
		for (int j = 1; j <= 4 - i; j++)
		{
			cout << 1;
		}
		for (int j = 1; j <= 2 * i - 1; j++)
		{
			cout << 0;
		}
		for (int j = 1; j <= 4 - i; j++)
		{
			cout << 1;
		}
		cout << endl;
	}
	return 0;
}
```

### 二、二维数组的输入和输出

从控制台输入到二维数组可以用双重for循环实现，本质就是上周学习的顺序赋值

```C++
#include <iostream>
using namespace std;
int main()
{
	int arr[2][3];
	for (int i = 0; i < 2; i++)
	{
		for (int j = 0; j < 3; j++)
		{
			cin >> arr[i][j];     // 等同于arr[2][3] = {1, 2, 3, 4, 5}，只不过12345是从控制台输入
		}
	}
	return 0;
}
```

#### 1. 求矩阵中的最大值的行号和列号

有一个3 × 4 的矩阵，求出最大值，还有行号和列号

```C++
// 输入用例
1 2 3 4
5 6 7 8
9 10 11 12
```

```C++
// 输出样例
12
3 4
```

```C++
#include <iostream>
using namespace std;
int main()
{
	int arr[3][4], max, max_i = 0, max_j = 0;
	for (int i = 0; i < 3; i++)
	{
		for (int j = 0; j < 4; j++)
		{
			cin >> arr[i][j];
			if (i == 0 && j == 0)
			{
				max = arr[0][0];
				continue;
			}
			if (max < arr[i][j])
			{
				max = arr[i][j];
				max_i = i;
				max_j = j;
			}
		}
	}
	cout << max << endl << max_i + 1 << " " << max_j + 1;
	return 0;
}
```

#### 2. 乾坤大挪移

将一个5 × 5 的二维数组，每个元素都向右移动一列，最右列移动到最左列，效果如下

```C++
// 输入样例
1 2 3 4 5
6 7 8 9 10
11 12 13 14 15
16 17 18 19 20
21 22 23 24 25
```

```C++
// 输出样例
5 1 2 3 4
10 6 7 8 9
15 11 12 13 14
20 16 17 18 19
25 21 22 23 24
```

```C++
// 写法1
#include <iostream>
using namespace std;
int main()
{
	int arr[5][5];
	for (int i = 0; i < 5; i++)
	{
		for (int j = 0; j < 5; j++)
		{
			cin >> arr[i][j];
		}
	}

	for (int i = 0; i < 5; i++)
	{
		int temp = arr[i][4];
		for (int j = 4; j > 0; j--)
		{
			arr[i][j] = arr[i][j - 1];
		}
		arr[i][0] = temp;
	}

	for (int i = 0; i < 5; i++)
	{
		for (int j = 0; j < 5; j++)
		{
			cout << arr[i][j] << " ";
		}
		cout << endl;
	}
	return 0;
}
```

```C++
// 写法2
#include <iostream>
using namespace std;
int main()
{
	int arr[5][5], temp;
	for (int i = 0; i < 5; i++)
	{
		for (int j = 1; j < 5; j++)
		{
			cin >> arr[i][j];
		}
		cin >> arr[i][0];
	}
	for (int i = 0; i < 5; i++)
	{
		for (int j = 0; j < 5; j++)
		{
			cout << arr[i][j] << " ";
		}
		cout << endl;
	}
	return 0;
}
```

#### 3. 二维数组部分输出

按行顺序为一个5 × 5的二维数组赋值，然后输出该数组的左下半三角

```C++
// 样例输入
1 2 3 4 5
1 2 3 4 5
1 2 3 4 5
1 2 3 4 5
1 2 3 4 5
```

```C++
// 输出样例
1
1 2
1 2 3
1 2 3 4
1 2 3 4 5
```

```C++
#include <bits/stdc++.h>
using namespace std;
int main()
{
	int arr[5][5];
	for (int i = 0; i < 5; i++)
	{
		for (int j = 0; j < 5; j++)
		{
			cin >> arr[i][j];
		}
	}
	for (int i = 0; i < 5; i++)
	{
		for (int j = 0; j <= i; j++)
		{
			cout << arr[i][j] << " ";
		}
		cout << endl;
	}
	return 0;
}
```

#### 4. 矩阵加法（减法）

输入2个n行m列的矩阵A和B，输出它们的和A + B

输入第一行包含2个整数n和m，表示矩阵的行数和列数，1 <= n <= 100，1<= m <= 100

接下来的n行，每行m个整数，表示矩阵A的元素

接下来的n行，每行m个整数，表示矩阵B的元素

相邻两个整数之间用单个空格隔开，每个元素均在1~1000之间

输出n行，每行m个整数，表示矩阵加法的结果，相邻2个整数之间用单个空格隔开

```C++
// 样例输入
2 3
1 2 3
4 5 6
1 2 3
3 2 1
```

```C++
// 样例输出
2 4 6
7 7 7
```

```C++
// 写法1
#include <bits/stdc++.h>
using namespace std;
int main()
{
	int m, n, arr[100][100];
	cin >> m >> n;
	for (int i = 0; i < 2; i++)
	{
		for (int j = 0; j < m; j++)
		{
			for (int k = 0; k < n; k++)
			{
				if (i == 0)
				{
					cin >> arr[j][k];
				}
				else
				{ 
					int temp;
					cin >> temp;
					arr[j][k] += temp;
				}
			}
		}
	}

	for (int i = 0; i < m; i++)
	{
		for (int j = 0; j < n; j++)
		{
			cout << arr[i][j] << " ";
		}
		cout << endl;
	}
	return 0;
}
```

```C++
// 写法2
#include <bits/stdc++.h>
using namespace std;
int main()
{
	int m, n, arrA[100][100], arrB[100][100];
	cin >> m >> n;
	for (int i = 0; i < m; i++)
	{
		for (int j = 0; j < n; j++)
		{
			cin >> arrA[i][j];
		}
	}
	for (int i = 0; i < m; i++)
	{
		for (int j = 0; j < n; j++)
		{
			cin >> arrB[i][j];
		}
	}
	for (int i = 0; i < m; i++)
	{
		for (int j = 0; j < n; j++)
		{
			arrA[i][j] += arrB[i][j];
		}
	}

	for (int i = 0; i < m; i++)
	{
		for (int j = 0; j < n; j++)
		{
			cout << arrA[i][j] << " ";
		}
		cout << endl;
	}
	return 0;
}
```

### 三、作业

#### 1. 平均成绩（必做）

一个学习小组有4个人，每个人有三门课的考试成绩。将各个数据保存到二维数组a\[3][4]中，并求全组分科的平均成绩和总平均成绩（结果保留两位小数）。

|       |  王  |  李  |  赵  |  周  |
| :---: | :--: | :--: | :--: | :--: |
| 数学  |  80  |  61  |  59  |  85  |
| C语言 |  75  |  65  |  63  |  87  |
| 物理  |  92  |  71  |  70  |  90  |

```C++
// 输出样例
71.25 72.50 80.75 224.50
```

#### 2. 行最大值（必做）

在3*4的二维数组a中选出各行最大的元素组成一个一维数组b并输出。

```C++
// 样例输入
3 16 87 65
4 32 11 108
10 25 12 37
```

```C++
// 输出样例
87 108 37
```

#### 3. 极值差（选做）

输入一个m*n的矩阵，找到矩阵中的最大值和最小值，并输出他们的差。

```C++
// 输入样例
2 3
1 23 2
3 4 5
```

```C++
// 输出样例
22
```

#### 4. 列最小值（选做）

在3*4的二维数组a中选出各列最小的元素组成一个一维数组b并输出。

```C++
// 输入样例
3 16 87 65
4 32 11 108
10 25 12 37
```

```C++
// 输出样例
3 16 11 37
```

#### 5. 数组对称（选做）

输入一个4行4列的数组，判断其是否为对称二维数组，对称是指每行第一个元素和最后一个元素相同，第二个元素和倒数第2个元素相同。如果为对称数组输出yes 不是输出no.

```C++
// 输入样例
1 2 2 1
2 3 3 2
3 4 4 3
4 5 5 4
```

```C++
// 输出样例
yes
```

