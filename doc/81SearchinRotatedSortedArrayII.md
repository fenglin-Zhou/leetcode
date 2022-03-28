## [81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

#### 题目大意

给定排好序的数组，从不确定的位置旋转了一下，求目标值是否存在。

首先判断第一个值是否相等，大于目标值那我们就从最后一个值往前判断，如果小于就从头往后。结束的标准就是不小于了或者不大于了，再判断当前位置是否相等。

```
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        int size = nums.size();
        if(nums[0] == target) return true;
        if(nums[0] > target){
            int i = size -1;
            while(i >= 0 && nums[i] > target){
                i--;
            }
            if(i < 0 || nums[i] != target) return false;
            else return true;
        }
        if(nums[0] < target){
            int i = 1;
            while(i < size-1 && nums[i] < target){
                i++;
            }
            if(i > size -1 || nums[i] != target) return false;
            else return true;
        }
        return false;
    }
};
```
