## [647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)

#### 题目大意

给定一个字符串，求所有的回文串。
从第一个开始判断，如果向左右遍历相等就结果加一，再判断相邻位置相等的情况。

```
class Solution {
public:
    int countSubstrings(string s) {
        int n = (int) s.size();
        int res = 0;
        for(int i=0;i<n;i++){
            int l=i,r=i;
            res++;
            while(l-1>=0 && r+1<n && s[l-1] == s[r+1]){
                res++,l--,r++;
            }
            if(i>0 && s[i-1] == s[i]){
                res++;
                l=i-1, r = i;
                while(l-1>=0 && r+1<n && s[l-1] == s[r+1]){
                    res++,l--,r++;
                }
            }
        }
        return res;
    }
};
```
