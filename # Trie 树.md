# Trie 树
```c++
#pragma warning(disable:4996)
#include <iostream>
#include <cstring>

const int N = 1E4 + 10;

int trie[N][26];
int end[N];
int tot = 1;

void insert(char* str)
{
	int len = strlen(str);
	int p = 1;

	int ch = 0;

	for (int i = 0; i < len; i++)
	{
		ch = str[i] - 'a';
		if (trie[p][ch] == 0) trie[p][ch] = ++tot;
		p = trie[p][ch];
	}

	end[p] = true;
}

bool search(char* str)
{
	int len = strlen(str);
	int p = 1;

	int ch = 0;

	for (int i = 0; i < len; i++)
	{
		ch = str[i] - 'a';
		if (trie[p][ch] == 0) return false;
		p = trie[p][ch];
	}

	return end[p];
}

int main(int argc, const char* argv[])
{
	int n = 0;
	std::cin >> n;
	for (int i = 0; i < n; i++)
	{
		char str[100];
		std::cin >> str;
		insert(str);
	}
	int m = 0;
	std::cin >> m;
	for (int i = 0; i < m; i++)
	{
		char str[100];
		std::cin >> str;
		if (search(str))
		{
			std::cout << "Yes\n";
		}
		else
		{
			std::cout << "No\n";
		}
	}
	return 0;
}

```