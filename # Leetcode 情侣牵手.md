# Leetcode 情侣牵手
```c++
#include <iostream>

int minSwapsCouples(int *row, int rowSize) {
    int res = 0;
    for (int i = 0; i < rowSize - 1; i += 2) {
        int p1 = row[i];
        int p2 = (p1 % 2 == 0 ? p1 + 1 : p1 - 1);
        if (row[i + 1] != p2) {
            for (int j = i + 2; j < rowSize; j++) {
                if (row[j] == p2) {
                    int t = row[j];
                    row[j] = row[i + 1];
                    row[i + 1] = t;
                    break;
                }
            }
            res++;
        }
    }
    return res;
}

int main() {
    int row[] = {2, 0, 5, 4, 3, 1};
    int i = minSwapsCouples(row, 6);
    std::cout << i << "\n";
    return 0;
}

```