### 1. sort用法

sort(first, last, comp);

`first`：排序范围的起始迭代器（包含）。

`last`：排序范围的结束迭代器（不包含）。

`comp`：可选的比较函数，用于定义排序规则。如果省略，默认按升序排序。

#### 升序排序

```C++
#include <bits/stdc++.h>
using namespace std;
int main() {
	// 升序排序
	int a[] = { 3, 1, 2, 5, 4 };
	sort(a, a + 5);
	for (int i = 0; i < 5; i++) cout << a[i] << " ";
	return 0;
}
```

#### 降序排序

```C++
#include <bits/stdc++.h>
using namespace std;
int main() {
	// 升序排序
	int a[] = { 3, 1, 2, 5, 4 };
	sort(a, a + 5, greater<int>());  // 使用比较器
	for (int i = 0; i < 5; i++) cout << a[i] << " ";
	return 0;
}
```

#### 自定义比较器

```C++
#include <bits/stdc++.h>
using namespace std;

bool compare(int a, int b) {
	// 该比较器中填写你认为需要的程序
	return  a > b; // 降序：当 a > b 时，a 排在 b 前面
}

int main() {
	// 升序排序
	int a[] = { 3, 1, 2, 5, 4 };
	sort(a, a + 5, compare);
	for (int i = 0; i < 5; i++) cout << a[i] << " ";
	return 0;
}
```

