# （Leetcode）KthLargest
```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <queue>

using namespace std;

class KthLargest {
private:
    priority_queue<int, vector<int>, greater<>> pq;
    int k;
public:
    KthLargest(int k, vector<int> &nums) {
        this->k = k;
        for (auto &i : nums) {
            add(i);
        }
    }

    int add(int val) {
        pq.push(val);
        if (pq.size() > k) {
            pq.pop();
        }
        return pq.top();
    }
};

int main() {

    return 0;
}

```