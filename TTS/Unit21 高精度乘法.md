```C++
#include <iostream>
#include <cstring>

using namespace std;

int main() {
    char a1[1001] = {};  
    int a[1001] = {}, c[2002] = {};  
    int n;  

    cin >> a1 >> n;  

    int lena = strlen(a1);  

    // 将字符数组 a1 转换为整数数组 a，从后往前存储
    for (int i = 0; i < lena; ++i) {
        a[i] = a1[lena - 1 - i] - '0';  // 将字符转换为对应的整数
    }

    n *= 365;  

    // 进行高精度乘法运算
    int s, x;  // s 用于存储 n 的当前位数字，x 用于存储进位
    int index = 0;  // 用于记录当前处理的是 n 的哪一位

    while (n) {
        x = 0;  // 每次处理 n 的新的一位时，将进位 x 重置为 0
        s = n % 10;  // 取出 n 的当前位数字（个位）

        // 将 a 数组中的每一位与 n 的当前位数字相乘，并加上进位
        for (int i = 0; i < lena; ++i) {
            int sum = a[i] * s + x + c[index + i];  // 计算当前位的乘积、进位和之前结果的和
            c[index + i] = sum % 10;  // 更新当前位的结果
            x = sum / 10;  // 计算新的进位
        }

        // 处理乘法运算中可能产生的额外进位
        while (x > 0) {
            c[index + lena] += x;  // 将进位加到结果数组的下一位
            x = c[index + lena] / 10;  // 计算新的进位
            c[index + lena] %= 10;  // 更新结果数组的下一位
        }

        index++;  // 处理完 n 的当前位，移动到下一位
        n /= 10;  // 去掉 n 的当前位（个位）
    }

    // 找到结果数组 c 的有效长度
    int lenc = lena + index;
    while (lenc > 1 && c[lenc - 1] == 0) {
        lenc--;  // 去掉前导 0
    }

    // 输出最终的乘法结果
    for (int i = lenc - 1; i >= 0; --i) {
        cout << c[i];
    }

    return 0;
}
```

