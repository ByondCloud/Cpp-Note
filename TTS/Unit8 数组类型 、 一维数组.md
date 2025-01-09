### 一、 数学知识

#### 1. 乘阶

例如5的乘阶就是 5 * 4 * 3 * 2 * 1 = 120，3的乘阶就是 3 * 2 * 1 = 6，0的乘阶为1

乘阶的表示方法为！，例如5的乘阶表示为【5！】，3的乘阶表示为【3！】

#### 2. 水仙花数

特殊的三位数，将三位数的个十百位分别做三次方，叠加的结果为原本的数就是水仙花数

例如153就是个水仙花数公式 $1^3 + 5^3 + 3^3 = 153$， 还有类似的数有370,371,407等等   pow(5, 3)

#### 3. 斐波那契数列

数列的第一位和第二位都是1，之后的数等于前两位数之和，例如1、1、2、3、5、8、13

### 二、复习for循环 & 学习数组

```C++
// 循环输出0-9
#include <iostream>
using namespace std;
int main()
{   
	for (int i = 0; i < 10; i++)
	{
		cout << i << endl;
	}
    return 0;
}
```

```C++
// 数组的使用
#include <bits/stdc++.h>
using namespace std;
int main()
{   
	int arr[8] = { 10, 20, 30, 40, 50, 60, 70, 80 };
	cout << arr[0] << endl; // 10
	cout << arr[5] << endl; // 60
	cout << arr[7] << endl; // 80
	cout << arr[8] << endl; // -858993460【初始化的数/栈中的垃圾数】
    return 0;
}
```

```C++
// 数组的4种初始化方式
// 方式1 确定数组长度并赋值
int arr1[5] = {1, 2, 3, 4, 5}
// 方式2 确定数组长度但不赋值，默认值为0
int arr2[5] = {} 
// 方式3 确定数组长度，赋值从开头的个元素，其余元素都为0
int arr3[5] = {1, 2};
// 方式4 确定数组长度，不初始化,元素的值不确定，可能是垃圾数，也可能是-858993460，具体看编译器版本
int arr4[5];
```

### 三、码到成功

#### 1. 水仙花数

输出100-999之间所有的水仙花数

```C++
// 输出样例
153 370 371 407
```

```C++
#include <bits/stdc++.h>
using namespace std;
int main()
{   
	int single_digit, ten_digit, hundred_digit, result;
	for (int i = 100; i <= 999; i++)
	{
		single_digit = i % 10;     // 个位
		ten_digit = i / 10 % 10;   // 十位
		hundred_digit = i / 100;   // 百位
		result = pow(single_digit, 3) + pow(ten_digit, 3) + pow(hundred_digit, 3);
		if (i == result)
		{
			cout << i << " ";
		}
	}
    return 0;
}
```

#### 2. 测血压

监护室每小时测量一次病人的血压，若收缩压在90 - 140 之间并舒张压在60 - 90 之间（包含端点值）则称之为正常，现给出某病人若干次测量的血压值，计算病人保持正常血压的最长小时数

```C++
// 输入样例
4
100 80 // T
90 50  // F
120 60 // T
140 90 // T
```

```C++
// 输出样例
2
```

```C++
#include <bits/stdc++.h>
using namespace std;
int main()
{   
	int count, hour = 0, max_hour = 0;
	cin >> count;
	for (int i = 0; i < count; i++)
	{
		int systolic, diastolic; // 收缩压   舒张压
		cin >> systolic >> diastolic;
		if (systolic >= 90 and systolic <= 140 and diastolic >= 60 and diastolic <= 90)
		{
			hour += 1;
			if (hour > max_hour)
			{
				max_hour = hour;
			}
		}
		else {
			hour = 0;
		}
	}
	cout << max_hour;
    return 0;
}
```



#### 3. 定义数组，输出下标为6的元素

定义数组并存入1 - 10之间的数，输出下标为6的数组元素

```C++
// 输出样例
7
```

```C++
#include <iostream>
using namespace std;
int main()
{   
	int arr[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
	cout << arr[6];
    return 0;
}
```

#### 4. 输出N个数中最大值

定义一个数组，向数组中输入N个数（1 <= N <= 100 ），输出N个数中的最大值和最小值，用空格隔开

```C++
// 输入样例
6              // 数组中有6个数
4 8 7 3 12 6   // 从控制台输入，就是cin
```

```C++
// 输出样例
12 3          // 最大值和最小值，用空格隔开
```

```C++
#include <iostream>
using namespace std;
int main()
{
    int count, arr[101], min = 0, max = 0;
    cin >> count;
    for (int i = 0; i < count; i++)
    {
        int temp;
        cin >> temp;
        arr[i] = temp;
        // 上面三行也可以这么写  cin >> arr[i];
        // 后续的所有temp换成arr[i]
        if (i == 0)
        {
            min = arr[0]; // min = temp;
            max = arr[0]; // max = temp;
            continue;
        }
        if (temp > max)
        {
            max = temp;
        }
        if (temp < min)
        {
            min = temp;
        }
        
        
    }
    cout << max << " " << min;
    return 0;
}
```

#### 5.斐波那契数列   

给出一个正整数k，输出斐波那契数列第k个数是多少，k的范围为【1 <= k <= 46】

```C++
// 输入样例
19
```

```C++
// 输出样例
4181
```

```C++
#include <iostream>
using namespace std;
int main()
{
    int k, arr[47];
    cin >> k;
    arr[0] = 1;
    arr[1] = 1;
    for (int i = 2; i < k; i++)
    {
        arr[i] = arr[i - 2] + arr[i - 1];
    }
    cout << arr[k - 1];
    return 0;
}
```

#### 6. 斐波那契数列问题2

 有一个分数序列是$\LARGE \frac{1}{2} 、\frac{2}{3} 、\frac{3}{5}、\frac{5}{8}、\frac{8}{13}、\frac{13}{21} ...$

 输出第n项，n的范围为【2 <= n <= 20】（1/2 2/3 3/5 5/8 8/13 13/21...）

```C++
#include <iostream>
using namespace std;
int main()
{
    int k, arr[22];
    cin >> k;
    arr[0] = 1;
    arr[1] = 1;
    // 也可以在定义数组的时候这么写  arr[22] = {1, 1};
    for (int i = 2; i < k + 2; i++)
    {
        arr[i] = arr[i - 2] + arr[i - 1];
    }
    for (int i = 0; i < k; i++)
    {
        cout << arr[i + 1] << "/" << arr[i + 2] << " ";
    }
    return 0;
}
```

#### 7. 灯的开关问题

有N盏灯，开始时所有灯都亮着，每个灯都有一个开关控制，现按其顺序编号为1,2,3,4,5...N,（1 <= N <= 30）然后将编号为2的倍数的灯拉一下，其次将编号为3的倍数的灯拉一下，然后是4的倍数，最后是5的倍数，拉完这4次灯之后，哪些灯还亮着？

```C++
// 输入样例
10
```

```C++
// 输出样例
1 4 6 7 8 10
```

```C++
// 写法1
#include <bits/stdc++.h>
using namespace std;
int main()
{
	int n, arr[31]; // 
	cin >> n;
	for (int i = 1; i <= n; i++)
	{
		arr[i] = 1;  // 1代表就是
	}
    
	for (int i = 1; i <= n; i++)
	{
		if (i % 2 == 0) {
			arr[i] = 1 - arr[i];
		}
		if (i % 3 == 0) {
			arr[i] = 1 - arr[i];
		}
		if (i % 4 == 0) {
			arr[i] = 1 - arr[i];
		}
		if (i % 5 == 0) {
			arr[i] = 1 - arr[i];
		}
	}
	for (int i = 1; i <= n; i++)
	{
		if (arr[i] == 1)
		{
			cout << i << " ";
		}
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
    int n;
    bool arr[31];
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        arr[i] = true;  // true是开灯，false是关灯
        if (i % 2 == 0)
        {
            arr[i] = !arr[i];
        }
        if (i % 3 == 0)
        {
            arr[i] = !arr[i];
        }
        if (i % 4 == 0)
        {
            arr[i] = !arr[i];
        }
        if (i % 5 == 0)
        {
            arr[i] = !arr[i];
        }
        // 判断灯是否亮着
        if (arr[i]) {
            cout << i << " ";
        }
    }
    return 0;
}
```



#### 8. 排队向后转

n名同学在操场上面向老师排队，现将其顺序编号为1,2,3...n（1 <= N <= 50），然后让编号为2的倍数的同学向后转（不能再向前转），再让编号为5的倍数的同学向后转（不能再向前转），问最后面向老师的都有哪些同学？

```C++
// 输入用例
15
```

```C++
// 输出用例
1 3 7 9 11 13
```

```C++
// 写法1
#include <bits/stdc++.h>
using namespace std;

int main()
{
	int n, arr[51];
	cin >> n;
	for (int i = 1; i <= n; i++)
	{
		arr[i] = 1;
	}
	for (int i = 1; i < n; i++)
	{
		if (i % 2 == 0 || i % 5 == 0)
		{
			arr[i] = 0;
		}	
	}
	for (int i = 1; i < n; i++)
	{
		if (arr[i] == 1) {
			cout << i << " ";
		}
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
    int n, arr[50];
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        arr[i] = 1; // 1代表正面，0代表反面
        if (i % 2 == 0 || i % 5 == 0)
        {
            arr[i] = 0;
            continue;
        }
        cout << i << " ";
    }
    return 0;
}
```

#### 9. 求比平均数大的数

定义一个数组arr，并赋值，输出数组中比所有元素平均数都大的元素，数组的长度不超过100

```C++
// 输入样例
6
12 10 9 15 22 28
```

```C++
// 输出样例
22 28
```

```C++
#include <bits/stdc++.h>
using namespace std;

int main()
{
	int n, total = 0;
	cin >> n;
	int arr[101];
	for (int i = 0; i < n; i++)
	{
		int temp;
		cin >> temp;
		arr[i] = temp;
		total += temp;
	}
	float avg = (float)total / n;          // 平均数
	for (int i = 0; i < n; i++)
	{
		if (arr[i] > avg) {
			cout << arr[i] << " ";
		}
	}
	return 0;
}
```

#### 10. 输出比平均数大的数和对应的下标

定义一个数组arr（1 <= arr <= 100），并赋值，输出数组中比所有元素平均数大的元素和下标

```C++
// 输入用例
6
12 10 9 15 22 28
```

```C++
// 输出用例
22 4
28 5
```

```C++
#include <bits/stdc++.h>
using namespace std;

int main()
{
	int n, total = 0;
	cin >> n;
	int arr[101];
	for (int i = 0; i < n; i++)
	{
		int temp;
		cin >> temp;
		arr[i] = temp;
		total += temp;
	}
	int avg = (float)total / n;          // 平均数
	for (int i = 0; i < n; i++)
	{
		if (arr[i] > avg) {
			cout << arr[i] << " " << i << endl;
		}
	}
	return 0;
}
```

### 四、作业

#### 1. 评委评分（必做）

某中学要举办一场“校园歌手”大赛，邀请全校学生积极参加，踊跃报名，校方还邀请了10位评委，对参赛选手的表演进行打分点评。现在要求输入10位评委的打分成绩（打分成绩在1-10的范围内），并把成绩中的最大值和最小值输出，最后去掉最大值和最小值，然后再输出一个平均值。

```C++
// 输入用例（10位评委的打分）
1 2 3 4 5 6 7 8 9 10
```

```C++
// 输出用例
最高分: 10
最低分: 1
平均分: 5.50
```

#### 2. 输出序列前N项的数据和（必做）

有一组序列的数是：1、2、9、33、126、477，……，请同学们认真观察数值的规律。现要求：指定项数为任意的N项，计算：

1）第N项的数据（1 <= N <= 15）；

2）输出前N项数据的和。

```C++
// 输入用例
6
```

```C++
// 输出用例
477
648
```

#### 3. 歌手投票（选做） 

校园歌手大赛进入总决赛，进入总决赛的选手有3名学生，校学生会想知道这3名学生歌手受欢迎的程度，设计一个投票箱，让每一个同学给自己喜欢的歌手投票，为了方便，学生会把3名歌手用1，2 , 3进行编号，这样，同学们只要用编号进行投票就可以了，现在，学生会找到你，帮助统计一下每个歌手获得的票数。

【输入】两行。第一行是一个整数n，表示参加投票的人数，第二行是n个整数，每个数的取值范围为[1-3]，表示喜欢的歌手。

【输出】两行。第一行是1 2 3 三个数字，表示选手编号，第二行3个数字，表示各个编号选手获得的票数。

```C++
// 输入用例
10
1 2 3 1 2 3 1 2 3 2
```

```C++
// 输出用例
1 2 3
3 4 3
```

#### 4. 与指定数字相同的数的个数（选做）

输出一个整数序列中与指定数字相同的数的个数。

【输入】

  输入包含三行:

  第1行是n(n<=100)，表示整数序列的长度；

  第2行是n个整数，整数之间以一个空格分开；

  第3行包含一个整数，为指定的数字m。

【输出】

输出为n个数中与m相同的数的个数。

```C++
// 输入用例
3
2 3 2
2
```

```C++
// 输出用例
2
```

#### 5. 数组逆序重放（选做）

将一个数组中的值按逆序重新存放。例如，原来的顺序为8,6,5,4,1。

要求改为1,4,5,6,8。

【输入】

 两行：第1行为数组中元素的个数n(1<n<100);第2行是n个整数，每两个

整数之间用空格隔开。

【输出】

一行：逆序后数组的整数，每两个整数之间用空格隔开。

```C++
// 输入用例
5
8 6 5 4 1
```

```C++
// 输出用例
1 4 5 6 8
```



