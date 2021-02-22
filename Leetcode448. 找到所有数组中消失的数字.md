# 448. 找到所有数组中消失的数字

```
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int> &nums) {
        for (int i = 0; i < nums.size(); i++) {
            int j = abs(nums[i]) - 1;
            if (nums[j] > 0) nums[j] *= -1;
        }
        int n = nums.size();
        vector<int> res;
        for (int i = 0; i < n; i++) {
            if (nums[i] > 0) res.push_back(i + 1);
        }
        return res;
    }
};
```