## [2216. Minimum Deletions to Make Array Beautiful](https://leetcode.com/problems/minimum-deletions-to-make-array-beautiful/)

#### 题目大意

[1,1,2,2,3,3]给你一个数组，保证长度是偶数，并且在i为偶数位时nums[i] != nums[i+1]，求要删除的数量。
注意不需要去删除，一开始加了删除结果一直超时。。。

```
class Solution {
public:
    int minDeletion(vector<int>& nums) {
        vector<int>::iterator it;
        int cnt = 0;
        for(it = nums.begin(); it < nums.end();){
            vector<int>::iterator pos = it + 1;
            while(pos!=nums.end() && *it == *pos){
                pos++;
                cnt++;
            }
            it = pos + 1;
        }
        if((nums.size()-cnt) % 2){
            nums.pop_back();
            cnt++;
        }
        return cnt;
    }
};
```
