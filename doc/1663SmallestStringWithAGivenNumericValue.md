## [1663. Smallest String With A Given Numeric Value](https://leetcode.com/problems/smallest-string-with-a-given-numeric-value/)

#### 题目大意

给n和k，求n个字母组成的字符串值正好是k，a=1，b=2...以此类推。

先给n个a，从后往前给剩余的空间。

```
class Solution {
public:
    string getSmallestString(int n, int k) {
        string ans(n, 'a');
        int cnt = n - 1;
        k -= n;
        while(k > 0){
            int val = min(k, 25);
            ans[cnt] += val;
            k -= val;
            cnt--;
        }
        return ans;
    }
};
```
