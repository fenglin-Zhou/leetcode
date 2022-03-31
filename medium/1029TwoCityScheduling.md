## [1029. Two City Scheduling](https://leetcode.com/problems/two-city-scheduling/)

#### 题目大意

给2*n个包含两个数的数组，求一边n个数的和最小。

我的思路是先排序，两个数差最大的排在前面，取小的那个作为要的值，后面差小的就随便了。

时间短的思路是排序直接按照第一个比第二小的更多排在前面，相当于取得时候取前面n个第一个值就行了，后面n个直接取第二个值。就是对我自己的思路的优化。

```
class Solution {
public:
    int twoCitySchedCost(vector<vector<int>>& costs){
        sort(costs.begin(), costs.end(), [](vector<int>& a, vector<int>& b){
            return (a[0] - a[1]) < (b[0] - b[1]);
        });

        int n = costs.size() / 2;
        int res = 0;
        for (int i = 0; i < n; i++){
            res += costs[i][0] + costs[i + n][1];
        }
        return res;
    }
};
```
