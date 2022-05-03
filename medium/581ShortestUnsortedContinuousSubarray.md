## [581. Shortest Unsorted Continuous Subarray](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/)

#### 题目大意

给定一个数组，寻找重新排序多少个数字就可以让整个数字排序。

遍历所有寻找最大值大于当前值的位置，[1,3,2,2,2]为例，3是最大值，他大于最后的2，说明到最后一个位置是重新排序的终点。
寻找最小值小于当前位置，从右到左，一开始是2，2小于3，找到了index 1，而1作为最小值没有比他小的，说明不动。

```
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        int n=nums.size();
        int maxi=INT_MIN,begin=-1,end=-1,mini=INT_MAX;
        for(int i=0;i<n;i++)
        {
            maxi=max(maxi,nums[i]);
            if(maxi>nums[i])
            {
                end=i;
            }
        }
        cout << end << " ";
        for(int i=n-1;i>=0;i--)
        {
            mini=min(mini,nums[i]);
            if(mini<nums[i])
            {
                begin=i;
            }
        }
        cout << begin << " ";
        if(begin==end)
            return 0;
        return end-begin+1;    
    }
};
```
