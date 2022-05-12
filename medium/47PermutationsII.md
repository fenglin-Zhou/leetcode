## [47. Permutations II](https://leetcode.com/problems/permutations-ii/)

#### 题目大意

求给定数组的所有排列，不同的是这个里面有重复的元素，要保证重复元素的序列不被重复添加。

在判断的时候如果相邻两个元素相等，那么就不需要交换位置。

```
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> ans;
        sort(nums.begin(), nums.end());
        gp(nums, 0, nums.size(), ans);
        return ans;
    }
    void gp(vector<int> nums, int i, int j, vector<vector<int>>& ans){
        if(i == j-1){
            ans.push_back(nums);
            return;
        }
        for(int k = i; k < j; k++){
            if(k != i && nums[k] == nums[i]) continue;
            swap(nums[i], nums[k]);
            gp(nums, i+1, j, ans);
        }
    }
};
```
