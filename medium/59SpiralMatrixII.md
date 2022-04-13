## [59. Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/)

#### 题目大意

给定一个n，写一个n*n的二维数组，要求螺旋加一。
那就循环加一呗。

```
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> ans(n, vector<int>(n));
        int num = 1;
        bool isv[n][n];
        memset(isv, false, n*n);
        int i = 0, j = 0;
        ans[i][j] = num;
        isv[i][j] = true;
        while(num < n*n){
            while(j+1 < n && !isv[i][j+1]){
                ans[i][++j] = ++num;
                isv[i][j] = true;
            }
            while(i+1 < n && !isv[i+1][j]){
                ans[++i][j] = ++num;
                isv[i][j] = true;
            }
            while(j-1 >= 0 && !isv[i][j-1]){
                ans[i][--j] = ++num;
                isv[i][j] = true;
            }
            while(i-1 >= 0 && !isv[i-1][j]){
                ans[--i][j] = ++num;
                isv[i][j] = true;
            }
        }
        return ans;
    }
};
```
