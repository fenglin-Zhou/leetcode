## [63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)

#### 题目大意

给定一个二维数组，求左上角到右下角的路径条数，只能向下向右。

dfs会超时，用dp，申请一个m+1 * n+1大小的数组保存路径条数，(m, n)就是答案。1，1就是保存只有一个值的时候的路径条数，

```
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int> > &obstacleGrid) {
        int m = obstacleGrid.size() , n = obstacleGrid[0].size();
        vector<vector<int>> dp(m+1,vector<int>(n+1,0));
        dp[0][1] = 1;
        for(int i = 1 ; i <= m ; ++i)
            for(int j = 1 ; j <= n ; ++j)
                if(!obstacleGrid[i-1][j-1])
                    dp[i][j] = dp[i-1][j]+dp[i][j-1];
        return dp[m][n];
    }
};
```
