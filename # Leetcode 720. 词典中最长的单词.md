# Leetcode 720. 词典中最长的单词
## 题目描述：
给出一个字符串数组words组成的一本英语词典。从中找出最长的一个单词，该单词是由words词典中其他单词逐步添加一个字母组成。若其中有多个可行的答案，则返回答案中字典序最小的单词。若无答案，则返回空字符串。
 **示例 1：**
输入：
words = ["w","wo","wor","worl", "world"]
输出："world"
解释： 
单词"world"可由"w", "wo", "wor", 和 "worl"添加一个字母组成。
**示例 2：**
输入：
words = ["a", "banana", "app", "appl", "ap", "apply", "apple"]
输出："apple"
解释：
"apply"和"apple"都能由词典中的单词组成。但是"apple"的字典序小于"apply"。

```c++
class Solution {
public:
	int dic[301000][26] = { 0 };
	int end[100000] = { 0 };
	int tot = 1;
	int max_len = 0;
	int m = 0;

	void insert(string str)
	{
		int p = 1;
		for (int i = 0; i < str.size(); i++)
		{
			int ch = str[i] - 'a';
			if (dic[p][ch] == 0)
				dic[p][ch] = ++tot;
			p = dic[p][ch];
		}
		end[p] = true;
	}

	bool search(string str)
	{
		int p = 1;
		for (const auto& c : str)
		{
			if (dic[p][c - 'a'] == 0) return false;
			p = dic[p][c - 'a'];
			if (!end[p]) return false; //根据题目要求：逐步增加一个字母的单词。
		}

		return end[p];
	}

	string longestWord(vector<string>& words) {
		memset(dic, 0, sizeof(dic));
		memset(end, 0, sizeof(end));

		for (const auto& str : words)
		{
			insert(str);
		}

		string res;

		for (const auto& str : words)
		{
			if (search(str))
			{
				if (res.size() < str.size())
				{
					res = string(str);
				}
				else if (res.size() == str.size() && res > str)
				{
					res = string(str);
				}
			}
		}

		return res;
	}
};
```