## [31. Next Permutation](https://leetcode.com/problems/next-permutation/)

#### 题目大意

给定数字数组，求他的下一个字典序。

首先找到nums[i] < nums[i+1]的位置，这个i是用来往后交换的，比较相邻的两个是因为我们是从后往前依次比较，所以后面的都是交换过的。
再找到nums[i] < nums[j]，j是从最后向前找到第一个大于i的，交换i和j，然后将i之后的所有数组颠倒顺序就是结果。

```
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int size = nums.size() - 1;
        int pos;
        for(pos = size - 1; pos >= 0; --pos){
            if(nums[pos] < nums[pos+1]){
                break;
            }
        }
        int k;
        if(pos < 0) reverse(nums.begin(), nums.end());
        else{
            for(k = size; k > pos; --k){
                if(nums[k] > nums[pos])
                    break;
            }
            swap(nums[k], nums[pos]);
            reverse(nums.begin() + pos + 1, nums.end());
        }
    }
};
```
