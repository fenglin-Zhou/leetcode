## [456. 132 Pattern](https://leetcode.com/problems/132-pattern/)

#### 题目大意

给你一个数组，判断是否存在132的情况，也就是 i < j < k, nums[i] < nums[k] < nums[j]。

首先找到每个位置左侧的最小值，然后从右侧遍历，依次将值压入栈中，如果当前位置的值比栈顶大，并且左侧最小值小，那么就返回true

```
class Solution {
public:
    bool find132pattern(vector<int>& nums) {
        int n = nums.size();
        vector<int> cmin(n);
        cmin[0] = nums[0];
        for(int i = 1; i < n; ++i) {
            cmin[i] = min(cmin[i - 1], nums[i]);
        }
        stack<int> stack;
        for(int i = n - 1; i >= 1; --i) {
            while(stack.size() && stack.top() < nums[i]) {
                if(cmin[i - 1] < stack.top())
                    return true;
                stack.pop();
            }
            stack.push(nums[i]);
        }
        return false;
        
    }
};
```
