

### 码到成功

#### 1. 高精度减法（被减数小于减数）

```C++
#include <bits/stdc++.h>
using namespace std;

int main() {
	
	char a[1001] = {}, b[1001] = {}, c[1001] = {}; //  c1用于交换
	int a1[1001] = {}, b1[1001] = {}, c1[1001] = {};
	cin >> a >> b;
	
	// 如果【a比b小】 或者【长度相等并且a小】
	if (strlen(a) < strlen(b) || strlen(a) == strlen(b) && strcmp(a, b) < 0)
	{
		// 除数被除数交换，输出负号
		strcpy_s(c, a);
		strcpy_s(a, b);
		strcpy_s(b, c);
		cout << '-';
	}
	// 计算除数被除数的长度
	int lena = strlen(a), lenb = strlen(b);

	// 将a和b倒序并转换为int数组元素
	for (int i = 0; i < lena; i++) a1[i] = a[lena - i - 1] - '0';
	for (int i = 0; i < lenb; i++) b1[i] = b[lenb - i - 1] - '0';

	// 计算
	int x = 0;
	for (int i = 0; i < lena; i++)
	{
		c1[i] = a1[i] - b1[i] - x; // 计算当前位，记得减借位
		if (c1[i] < 0) // 如果不够减，就借位
		{
			c1[i] += 10;
			x = 1;
		}
		else {
			x = 0;
		}
	}

	// 计算位数
	for (int i = lena - 1; i > 0; i--)
	{
		if (c1[i] == 0) lena--;
		else break;
	}

	// 输出结果，记得要倒回来
	for (int i = 0; i < lena; i++) cout << c1[lena - i - 1];

    return 0;
}

```

