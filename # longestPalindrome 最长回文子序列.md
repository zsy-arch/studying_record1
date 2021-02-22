# longestPalindrome 最长回文子序列 
```c++
#include <stdio.h>
#include <string.h>

char *longestPalindrome(char *str) {
    if (strlen(str) < 2) return str;
    int start = 0, maxLen = 0;
    int length = strlen(str);

    for (int i = 0; i < length;) {
        if (length - i <= maxLen / 2) break;
        int left = i, right = i;
        while (right < length - 1 &&
               str[right + 1] == str[right]) {
            ++right;
        }
        i = right + 1;
        while (right < length - 1 &&
               left > 0 &&
               str[right + 1] == str[left - 1]) {
            ++right, --left;
        }
        if (right - left + 1 > maxLen) {
            start = left;
            maxLen = right - left + 1;
        }
    }

    *(str + start + maxLen) = '\0';
    return str + start;
}

char str[100];

int main() {
    scanf("%s", str);
    printf("%s\n", longestPalindrome(str));
    return 0;
}

```