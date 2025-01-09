## 高精度数

### 讲一讲

```C++
#include <bits/stdc++.h>
using namespace std;

int main() {
	
	char a[1001] = {};
	int a1[1001] = {};

	cin >> a;
	int lena = strlen(a);
	for (int i = 0; i < lena; i++)
	{
		a1[i] = a[i] - '0';
		cout << a1[i];
	}

    return 0;
}
```



### 码到成功

#### 1. 输出大数

```C++
#include <bits/stdc++.h>
using namespace std;

int main() {
	
	char a[1001] = {};
	int a1[1001] = {};

	cin >> a;
	int lena = strlen(a);
	for (int i = 0; i < lena; i++)
	{
		a1[i] = a[i] - '0';
		cout << a1[i];
	}

    return 0;
}

```



### 练一练

#### 1. 求大数的首末位

```C++
#include <bits/stdc++.h>
using namespace std;

int main() {
	
	char a[1001] = {};

	cin >> a;
	int lena = strlen(a);
	
	cout << lena << " " << a[0] << " " << a[lena - 1];

    return 0;
}
```



### 亲自出码

#### 1. 倒序输出

```C++
#include <bits/stdc++.h>
using namespace std;

int main() {
	
	char a[1001] = {};
	int a1[1001] = {};
	cin >> a;
	int lena = strlen(a);
	for (int i = 0; i < lena; i++)
	{
		a1[i] = a[lena - i - 1] - '0';
		cout << a1[i];
	}
	
    return 0;
}

```



## 高精度加法

### 讲一讲

#### 1. 位数相同且无进位

![image-20250109000047131](image/Unit19%20%E9%AB%98%E7%B2%BE%E5%BA%A6%E5%8A%A0%E6%B3%95/image-20250109000047131.png)

总结：转换为int类型后，对应位直接相加即可

```C++
#include <bits/stdc++.h>
using namespace std;

int main() {
	
	char a[1001] = {}, b[1001] = {};
	int a1[1001] = {}, b1[1001] = {}, c1[1001] = {};
	cin >> a >> b;
	int len = strlen(a);
	for (int i = 0; i < len; i++)
	{
		a1[i] = a[i] - '0';
		b1[i] = b[i] - '0';
		c1[i] = a1[i] + b1[i];
	}

	for (int i = 0; i < len; i++) cout << c1[i];
	
    return 0;
}

```



#### 2. 位数不一定相同且无进位

![image-20250109000436136](image/Unit19%20%E9%AB%98%E7%B2%BE%E5%BA%A6%E5%8A%A0%E6%B3%95/image-20250109000436136.png)

将两个数倒序后对应位相加，最后输出要记得倒回来

```C++
#include <bits/stdc++.h>
using namespace std;

int main() {
	
	char a[1001] = {}, b[1001] = {};
	int a1[1001] = {}, b1[1001] = {}, c1[1001] = {};
	cin >> a >> b;
	int lena = strlen(a);
	int lenb = strlen(b);
	int max_len = (lena > lenb ? lena : lenb);
	// 将a和b倒序并转换为int数组元素
	for (int i = 0; i < lena; i++) a1[i] = a[lena - i - 1] - '0';
	for (int i = 0; i < lenb; i++) b1[i] = b[lenb - i - 1] - '0';

	// 计算
	for (int i = 0; i < max_len; i++) c1[i] = a1[i] + b1[i];

	// 输出结果，记得要倒回来
	for (int i = 0; i < max_len; i++) cout << c1[max_len - i - 1];


    return 0;
}

```



### 码到成功

#### 1. 加法实例一

```C++
```

#### 2. 加法实例二

```C++
```



### 练一练

#### 1. 加法幽探

```C++
```



## 高精度加法（进位）

### 讲一讲

#### 1. 逆序后的加法进位

实例：逆序后的a，b，从左到右依次相加，x表示进位

![image-20250109001838825](image/Unit19%20%E9%AB%98%E7%B2%BE%E5%BA%A6%E5%8A%A0%E6%B3%95/image-20250109001838825.png)

总结：将各个位数对齐相加后，还需要考虑进位

#### 2. 带进位的加法步骤

1. 倒序，输入进int[]
2. 对应位相加
3. 计算进位
4. 处理最高位进位
5. 倒序输出

```C++
#include <bits/stdc++.h>
using namespace std;

int main() {
	
	char a[1001] = {}, b[1001] = {};
	int a1[1001] = {}, b1[1001] = {}, c1[1001] = {};
	cin >> a >> b;
	int lena = strlen(a), lenb = strlen(b);
	int max_len = (lena > lenb ? lena : lenb);
	// 将a和b倒序并转换为int数组元素
	for (int i = 0; i < lena; i++) a1[i] = a[lena - i - 1] - '0';
	for (int i = 0; i < lenb; i++) b1[i] = b[lenb - i - 1] - '0';

	// 计算
	int lenc = 0, x = 0;     // lenc - 结果的位数   x为进位
	while (lenc < max_len) // 用while因为会出现例如 666 + 777，连续进位的情况
	{
		c1[lenc] = a1[lenc] + b1[lenc] + x; // 计算当前位，记得加进位
		x = c1[lenc] / 10; // 更新进位
		c1[lenc] %= 10; // 更新当前位
		lenc++; // 更新结果的位数
	}
	if (x) c1[lenc] = x;
	else lenc--;

	// 输出结果，记得要倒回来
	for (int i = 0; i <= lenc; i++) cout << c1[lenc - i];

    return 0;
}

```

