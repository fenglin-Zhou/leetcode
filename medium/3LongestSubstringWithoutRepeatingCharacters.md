## [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

#### 题目大意

给定字符串求最长子串。
遍历每个字符，每次记录当前字符的位置，如果这个字符记录过了就更新start，ans就是当前位置减start。

```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> dis(256, -1);
        int len = s.size();
        int start = -1, ans = 0;
        for(int i = 0; i < len; ++i){
            if(dis[s[i]] > start)
                start = dis[s[i]];
            dis[s[i]] = i;
            ans = max(ans, i - start); 
        }
        return ans;
    }
};
```
