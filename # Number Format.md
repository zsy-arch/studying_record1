# Number Format
```c++
#include <stdio.h>

void formatNumber(int n, char *str, int sep) {
    int str_len = 0;
    int nums[1000];
    int nums_len = 0;

    if (!n) {
        str[0] = '0';
        str[1] = '\0';
        return;
    }
    if (n < 0) {
        n = -n;
        str_len++;
        str[0] = '-';
    }

    while (n > 0) {
        nums[nums_len++] = n % 10;
        n /= 10;
    }

    int offset = str_len;

    if (nums_len > sep) {
        if (nums_len % sep != 0) {
            str[offset + nums_len % sep] = ',';
            str_len += nums_len / sep + nums_len;
        } else {
            str[offset + sep] = ',';
            str_len += nums_len / sep + nums_len - 1;
        }
    } else {
        str_len += nums_len;
    }

    int j = nums_len - 1;
    for (int i = 0 + offset; i < str_len; ++i) {
        if (str[i] != ',') {
            str[i] = nums[j--] + '0';
        } else {
            str[i + sep + 1] = ',';
        }
    }
    str[str_len] = '\0';
}

int main() {
    int n = 0;
    scanf("%d", &n);
    char str[1000];
    formatNumber(n, str, 3);
    printf("%s\n", str);
    return 0;
}

```