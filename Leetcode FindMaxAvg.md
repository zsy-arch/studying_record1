# Find Max Average
```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
public:
    double findMaxAverage(vector<int> &nums, int k, int left, int right) {
        /*
         * 1. 获取数组前K个总和
         * 2. 从nums[k]开始，使用递推公式
         */
        int sum = 0;
        int max_sum = 0;
        for (int i = left; i < k; i++) {
            sum += nums[i];
        }
        max_sum = sum;
        for (int i = k; i <= right; i++) {
            sum = sum - nums[i - k] + nums[i];
            max_sum = max(max_sum, sum);
        }
        return max_sum / (double )k;
    }

    double findMaxAverage(vector<int> &nums, int k) {
        return findMaxAverage(nums, k, 0, nums.size() - 1);
    }
};

int main() {
    /*
6 4
1 12 -5 -6 50 3

     [1,12,-5,-6,50,3]
    4
     */
    int n = 0;
    int k = 0;
    std::cin >> n >> k;
    vector<int> v;

    for (int i = 0; i < n; i++) {
        int tmp;
        std::cin >> tmp;
        v.push_back(tmp);
    }

    Solution s;
    double res = s.findMaxAverage(v, k);

    std::cout << res << "\n";

    return 0;
}

```