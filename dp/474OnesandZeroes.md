## [474. Ones and Zeroes](https://leetcode.com/problems/ones-and-zeroes/)

#### 题目大意

给定一个字符串集合，里面只有0和1，给定m，n。求最多m个0，和n个1的最大子集数量。

还是dp题目，直接二维数组，m*n。遍历每一个子串，统计出0的数量和1的数量，再更新dp，更新后半段。

```
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
        int ones, zeroes;
        for(auto s:strs){
            ones = zeroes = 0;
            for(auto c:s){
                if(c=='0') zeroes++;
                else if(c=='1')ones++;
            }
            for(int i = m; i >= zeroes; i--){
                for(int j = n; j >= ones; j--){
                    dp[i][j] = max(dp[i][j], dp[i-zeroes][j-ones] + 1);
                }
            }
        }
        return dp[m][n];
    }
};
```
