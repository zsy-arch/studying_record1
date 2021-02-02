# unique 保留集合中各不相同的数
```c++
#include <iostream>
#include <algorithm>

void my_unique(int* arr, int n)
{
	int j = 0;
	for (int i = 0; i < n; i++)
	{
		if (!i || arr[i] != arr[i - 1])
		{
			arr[j++] = arr[i];
		}
	}
}

int main(int argc, const char* argv[])
{
	int n = 0;
	std::cin >> n;
	int* arr = new int[n];
	for (int i = 0; i < n; i++)
		std::cin >> arr[i];
	std::sort(arr, arr + n);
	for (int i = 0; i < n; i++)
		std::cout << arr[i] << ' ';
	std::cout << '\n';
	my_unique(arr, n);
	for (int i = 0; i < n; i++)
		std::cout << arr[i] << ' ';
	return 0;
}

```