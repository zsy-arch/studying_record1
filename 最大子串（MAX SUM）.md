# 最大子串（MAX SUM）

### CPP

```cpp
#include <cstdio>

const int minn = -19260817;

int arr[200200];
int n;

inline int max(int a, int b)
{
    return (a > b ? a : b);
}

int max_sum(int left, int right)
{
    if (left == right) return arr[left];
    int mid = (left + right) >> 1;
    int sum = 0, sum1 = minn, sum2 = minn;
    for (int i = mid; i >= left; i--)
    {
        sum += arr[i];
        sum1 = max(sum1, sum);
    }
    sum = 0;
    for (int i = mid + 1; i <= right; i++)
    {
        sum += arr[i];
        sum2 = max(sum2, sum);
    }
    return max(max( max_sum(left, mid), max_sum(mid + 1, right)), sum1 + sum2);
}


int main()
{
    scanf("%d", &n);
    for (int i = 1; i <= n; i++)
    {
        scanf("%d", arr + i);
    }
    printf("%d", max_sum(1, n));
}

// ====================

#pragma warning(disable:4996)
#include <iostream>
#include <algorithm>

int res_left, res_right;

int max_sub(int* arr, int left, int right)
{
	if (left == right) return arr[left];
	int mid = (left + right) >> 1;
	int sum = 0;
	int sum_l = -999;
	int sum_r = -999;

	for (int i = mid; i >= left; i--)
	{
		sum += arr[i];
		sum_l = std::max(sum, sum_l);
	}
	sum = 0;
	for (int i = mid + 1; i <= right; i++)
	{
		sum += arr[i];
		sum_r = std::max(sum, sum_r);
	}

	int max1 = max_sub(arr, left, mid);
	int max2 = max_sub(arr, mid + 1, right);
	int max = std::max(max1, max2);
	max = std::max(max, sum_l + sum_r);

	if (max == max1)
	{
		res_left = left;
		res_right = mid;
	}
	else if (max == max2)
	{
		res_left = mid + 1;
		res_right = right;
	}
	else
	{
		res_left = left;
		res_right = right;
	}

	return max;
}

int main(int argc, const char* argv[])
{
	int n = 0;
	std::cin >> n;
	int arr[100];
	for (int i = 0; i < n; i++)
		std::cin >> arr[i];

	int res = max_sub(arr, 0, n - 1);

	std::cout << res << "\n";
	std::cout << res_left << "\n";
	std::cout << res_right << "\n";
	return 0;
}


```

```
输入 
4 
2 3 -1 -2
输出
5
```

## HDU MAX SUM
```c++
#pragma warning(disable:4996)
#include<stdio.h>
int a[100010];

int main()
{
	int T, i, k, n, sum, max, p, q, t;
	scanf("%d", &T);
	for (k = 1; k <= T; k++)
	{
		scanf("%d", &n);
		for (i = 1; i <= n; i++)
			scanf("%d", &a[i]);
		sum = 0;
		max = -99999999;
		t = p = q = 1;
		for (i = 1; i <= n; i++)
		{
			sum += a[i];
			if (sum > max)
			{
				max = sum;
				p = t;
				q = i;
			}
			if (sum < 0)
			{
				sum = 0;
				t = i + 1;
			}
		}
		printf("Case %d:\n%d %d %d\n", k, max, p, q);
		if (k != T)
			printf("\n");
	}
	return 0;
}


// ==============================

#pragma warning(disable:4996)
#include <iostream>

int main(int argc, const char* argv[])
{
    int n = 0;
    int arr[1000];
    std::cin >> n;
    for (int i = 0; i < n; i++)
    {
        std::cin >> arr[i];
    }

    int sum = 0;
    int max = -1E3;
    int t = 0, p = 0, q = 0;

    for (int i = 0; i < n; i++)
    {
        sum += arr[i];
        if (sum < 0)
        {
            sum = 0;
            t = i + 1;
        }
        
        if (sum > max)
        {
            max = sum;
            p = t;
            q = i;
        }
    }

    std::cout << "SUM: " << max << " FROM: " << p << " to " << q << "\n";
    return 0;
}

```

