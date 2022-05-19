## [329. Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)

#### 题目大意

给定二维数组，求最长的递增序列，只能上下左右走。

采用dfs，遍历每一个点位。增加一个相同大小的数组用来保存当前位置的最长路径值，可以肯定的是我们一次遍历，被遍历的所有点位的路径值已经是准确的了，因为他一定是走完了所有的递增点，那么我们每次遍历的时候只需要遍历路径值没被更新的点，在dfs中比较最大值保存下来就是答案了。

```
class Solution {
public:
    int ans;
    int next[5] = {-1, 0, 1, 0, -1};
    int m, n;
    int longestIncreasingPath(vector<vector<int>>& ma) {
        m = ma.size();
        n = ma[0].size();
        ans = 0;
        vector<vector<int>> vc(m, vector<int>(n, 0));
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(vc[i][j] == 0){
                    dfs(i, j, vc, ma);
                }
            }
        }
        return ans;
    }
    int dfs(int i, int j, vector<vector<int>> &vc, vector<vector<int>>& ma){
        int maxway = 1;
        for(int k = 0; k < 4; ++k){
            int sum = 0;
            int newi = i+next[k];
            int newj = j+next[k+1];
            if(newi >= 0 && newi < m && newj >= 0 && newj < n && ma[newi][newj] > ma[i][j]){
                if(vc[newi][newj] != 0){
                    // 有值的一定是最长的，不需要遍历。
                    sum = vc[newi][newj];
                }else{
                    sum = dfs(newi, newj, vc, ma);
                }
                // 大于等于是因为如果下一个节点的路径为1，也就是说下一个节点是终点，那么当前节点应该是2，又因为我们初始化maxway是1（因为如果没有节点可以走，这个点的路径是1）
                if(sum >= maxway){
                    maxway = sum + 1;
                }
            }
        }
        //这个值就是当前位置出发的递增路径长度，当有更小的点到达这里时只需要加上这个值。
        vc[i][j] = maxway;
        if(maxway > ans) ans = maxway;
        return maxway;
    }
};
```
