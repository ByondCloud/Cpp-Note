### 1. 根据年月，算出该月的天数

闰年：能被4整除但不能被100整除，或者是能被400整除的数，就是闰年，闰年2月有29天

```C++
#include <iostream>
using namespace std;
int main()
{
	int year, month, total_day = 0;
	cin >> year >> month;
	if (month == 1 || month == 3 || month == 5 || month == 7 || month == 8 || month == 10 || month == 12)
	{
		cout << 31;
	}
	else if (month == 2)
	{
		if (year % 4 == 0 && year != 100 || year % 400 == 0)
		{
			cout << 29;
		}
		else
		{
			cout << 28;
		}
	}
	else
	{
		cout << 30;
	}
	return 0;
}
```



### 1.1 拓展 根据年月，算出该年从一月到该月一共有多少天

例如输入`2020 2`输出60，`2019 2`输出59

```C++
#include <iostream>
using namespace std;
int main()
{
	int year, month, total_day = 0;
	cin >> year >> month;
	for (int i = 1; i <= month; i++)
	{
		if (i == 1 || i == 3 || i == 5 || i == 7 || i == 8 || i == 10 || i == 12)
		{
			total_day += 31;
			continue;
		}
		if (i == 2)
		{
			if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) 
			{
				total_day += 29;
			}
			else 
			{
				total_day += 28;
			}
			continue;
		}
		total_day += 30;
	}
	cout << total_day;

	return 0;
}
```

### 2. 数字口袋

小 A 有一个口袋，里面可以装整数。他从 1 开始，按从小到大的顺序，依次将每个整数装入口袋。但是口袋是有限的，大小为 n，这就是说，口袋里所有的数字的和不能够超过 n。 



如果你知道循环的次数，就用for循环

如果你知道循环退出的条件，就用while循环

如果你知道循环退出条件，又要先执行一次，用do while

```C++
#include <iostream>
using namespace std;
int main()
{
	int n, total = 0, num = 1;
	cin >> n;
	while (total < n) 
	{
		cout << num << endl;
		total += num;
		num++;
	}


	return 0;
}
```

### 3. 成绩等级转换

A，90-100		B，77-89		C，67-76		D，60-66		E，0-59

```C++
#include <iostream>
using namespace std;
int main()
{
	// A，90-100		B，77-89		C，67-76		D，60-66		E，0-59
	int score;
	cin >> score;
	if (score >= 90 && score <= 100)
	{
		cout << 'A';
	}
	else if (score >= 77)
	{
		cout << 'B';
	}
	else if (score >= 67)
	{
		cout << 'C';
	}
	else if (score >= 60)
	{
		cout << 'D';
	}
	else
	{
		cout << 'E';
	}
	return 0;
}
```

### 4. 累计相加

输入一个正整数n，求形如：1+(1+2)+(1+2+3)+(1+2+3+4)+…(1+2+3+4+5+…n)的累计相加。 

```C++
// 做法1    当前的数 = 前一个数 + i
#include <iostream>
using namespace std;
int main()
{
	int n, total = 0, pre_total = 0;
	cin >> n;
	for (int i = 1; i <= n; i++)
	{
		total = total + pre_total + i;
		pre_total = pre_total + i;
	}
	cout << total;
	return 0;
}
```

```C++
// 做法2
#include <iostream>
using namespace std;
int main()
{
	int n, total = 0;
	cin >> n;
	for (int i = 1; i <= n; i++)
	{                               // 1 2 3 4  5
		total += (1 + i) * i / 2;   // 1 3 6 10 15
	}
	cout << total;
	return 0;
}
```

```C++
//做法3
#include <iostream>
using namespace std;
int main()
{
	int n, total = 0;
	cin >> n;
	for (int i = 1; i <= n; i++)
	{                           
		for (int j = 1; j <= i; j++)
		{
			total += j;
		}
	}
	cout << total;
	return 0;
}
```



