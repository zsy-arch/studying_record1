# A加B问题(HDU ACM)

```cpp
//
// Created by zhangsiyu on 2020/12/23.
//
#include <cstdio>
#include <cstring>

static const int LEN = 1000;

void getint(int *num) {
    for (int i = 0; i < LEN; ++i) {
        num[i] = 0;
    }
    char str[LEN];
    scanf("%s", str);
    int len = strlen(str);
    for (int i = 0; i < len; ++i) {
        num[len - i - 1] = str[i] - '0';
    }
}

void add(int *num1, int *num2, int *sum) {
    for (int i = 0; i < LEN; ++i) {
        sum[i] = 0;
    }
    for (int i = 0; i < LEN; ++i) {
        sum[i] += num1[i] + num2[i];
        if (sum[i] >= 10) {
            sum[i + 1]++;
            sum[i] -= 10;
        }
    }
}

void print(int *num) {
    int i;
    for (i = LEN - 1; num[i] == 0; i--) {}
    for (int j = i; j >= 0; j--) {
        printf("%d", num[j]);
    }
}

int main(int argc, char *argv[]) {
    int n = 0;
    int num1[LEN], num2[LEN], sum[LEN];
    scanf("%d", &n);

    for (int i = 1; i <= n; ++i) {
        getint(num1);
        getint(num2);
        add(num1, num2, sum);
        printf("Case %d:\n", i);
        print(num1);
        printf(" + ");
        print(num2);
        printf(" = ");
        print(sum);
        if (i != n) { printf("\n\n"); } else { printf("\n"); }
    }
    return 0;
}
```