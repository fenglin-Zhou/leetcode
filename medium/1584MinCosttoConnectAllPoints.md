## [1584. Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/)

#### 题目大意

给定size个二维点坐标，求可以连接所有点的最短距离，两个点的距离由x和y的差和组成。|xi - xj| + |yi - yj|。

申请一个点数量的数组保存这个点到最近点的距离。循环size-1次就可以保证连接所有，每判断完一个点就抹去一个点，每次循环计算剩余点到该点的距离，如果计算点位到该点距离近了就更新距离值，并保存一个最近点和最近点index，下一个循环的点就是最近点。

```
class Solution {
public:
    int minCostConnectPoints(vector<vector<int>>& ps) {
    int n = ps.size(), res = 0, i = 0, connected = 0;
    vector<int> min_d(n, 10000000);
    while (++connected < n) {
        min_d[i] = INT_MAX;
        int min_j = i;
        for (int j = 0; j < n; ++j)
            if (min_d[j] != INT_MAX) {
                min_d[j] = min(min_d[j], abs(ps[i][0] - ps[j][0]) + abs(ps[i][1] - ps[j][1]));
                min_j = min_d[j] < min_d[min_j] ? j : min_j;
            }
        res += min_d[min_j];
        i = min_j;
    }
    return res;
}
};
```
