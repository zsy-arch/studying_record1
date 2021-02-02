# KMP算法

```c++
#include <iostream>
#include <string>

void get_next(const std::string& str, int* next_val)
{
	int i = 0, j = -1, n = str.size();
	next_val[0] = -1;

	while (i < n)
	{
		if (j == -1 || str[i] == str[j])
		{
			i++, j++;
			next_val[i] = j;
		}
		else
		{
			j = next_val[j];
		}
	}
}

int KMP(std::string str1, std::string str2)
{
	int i = 0, j = 0;
	int m = str1.size();
	int n = str2.size();
	int* next_val = new int[n];
	get_next(str2, next_val);

	while (i < m && j < n)
	{
		if (j == -1 || str1[i] == str2[j])
		{
			i++, j++;
		}
		else
		{
			j = next_val[j];
		}
	}
	if (j == n)
		return i - j;
	return -1;
}

int main()
{
	std::string str1;
	std::string str2;
	std::cin >> str1;
	std::cin >> str2;
	int res = KMP(str1, str2);
	std::cout << res << '\n';
}
```