## [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)

#### 题目大意

给定一个数组，里面只有两个一样的值，找出这个值是多少。

两次循环，每次循环一个快指针（一次移动一个单位）一个慢指针（一次两个），都是从头出发，因为只有两个一样的，所以他们一定会在某一时刻到达相同位置，我们不必考虑这个位置是否是那个相同的值。

第二次循环，一个指针不动，另一个指针从头开始，那么下次遇到的就是相同值了。

```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int size = nums.size();
        if(size == 2) return nums[0];
        int slow = nums[0];
        int fast = nums[nums[0]];
        while(slow != fast){
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        slow = 0;
        while(slow != fast){
            slow =  nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
};
```
