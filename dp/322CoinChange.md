## [322. Coin Change](https://leetcode.com/problems/coin-change/)

#### 题目大意

给定一个数组表示硬币面值，和一个目标值。求正好拼出目标值的最少硬币数量，可以重复使用每个硬币。

这里需要使用bp，我们计算机从0到目标值每个值采用给定硬币的拼凑的最大硬币数量。对于每一个值，我们依次遍历每个硬币，如果硬币值小于每个值，那么我们选择减去硬币的dp+1。因为之前值已经保证是最少的了。

```
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int dp[amount+1];
        dp[0]=0;
        for(int i=1;i<=amount;i++){
            dp[i]=1e9;
            for(auto it:coins){
                if(i-it>=0)
                dp[i]=min(dp[i],dp[i-it]+1);
            }
        }
        
        return dp[amount]==1e9?-1:dp[amount];
    }
};
```
