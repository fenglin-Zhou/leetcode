## [410. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)

#### 题目大意

给定一个没有顺序的数组和一个目标分组数x，求分成x个数组后最小的最大值情况，要求分的数组是连续的。

首先我们找到数组中的最大值和总值，那么这个最大值肯定在这个范围内，然后我们在这个范围里二分查找每个值作为最大值的情况。

对于每一个可能的值，从头开始累加，如果加上还是小于最大值就加上，如果大于了那么就要分片，如果我们分片的次数小于0了，但是还没循环结束，那么这个值是不可能的。

```
class Solution {
private:
    bool doable (const vector<int>& nums, int cuts, long long max) {
        int acc = 0;
        for (num : nums) {
            // This step is unnecessary for this problem. I didn't discard this line because I want doable function more generalized.
            if (num > max) return false;
            else if (acc + num <= max) acc += num;
            else {
                --cuts;
                acc = num;
                if (cuts < 0) return false;
            }
        }
        return true;
    }
public:
    int splitArray(vector<int>& nums, int m) {
        long long left = 0, right = 0;
        for (num : nums) {
            left = max(left, (long long)num);
            right += num;
        }
        
        while (left < right) {
            long long mid = left + (right - left) / 2;
            if (doable(nums, m - 1, mid)) right = mid;
            else left = mid + 1;
        }
        return left;
    }
};
```
