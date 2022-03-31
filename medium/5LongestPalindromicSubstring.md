## [5LongestPalindromicSubstring](https://leetcode.com/problems/longest-palindromic-substring/)

```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

#### 题目大意

大致就是求一个字符串的最长回文串。

思路就是从从第一个字符串开始向后遍历，对每个位置向左向右对比，单个字符不一样下一个位置对比。只需要注意每次循环先判断是否和下一个相等，因为相同的可以直接判定为回文，也就是中间连续相同位置是奇数偶数。

[](../img/5.jpeg)

时间超过了99.62%，内存82.13%。

```
class Solution {
public:
    string longestPalindrome(string s) {
        int len = s.size();
        if(len <= 1) return s;
        int left = 0;
        int maxlen = 0;
        for(int i = 0; i < len;){
            if(len - i <= maxlen/2-1) break;
            int l = i;
            while(s[i] == s[i+1] && i < (len-1)) i++;
            int r = i;
            while(l >= 0 && r <= (len-1)){
                if(s[l] == s[r]){
                    l--;
                    r++;
                }else{
                    break;
                }
            }
            l++;
            r--;
            if((r-l+1) > maxlen){
                maxlen = r - l + 1;
                left = l;
            }
            i++;
        }
        return s.substr(left, maxlen);
    }
};
```
