## [316. Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters/)

#### 题目大意

给一个字符串，要求删除他重复的字母，并且保证新字符串字典序最小。

先遍历一边保存每个字母出现的次数，第二次遍历，首先减少字母出现的次数，如果这个字母被访问过了，就不再处理。如果我们新的字符串最后一个字母比当前这个字母大并且后面还会出现新字符串中的最后一个字母，那就说明我们可以在后面才放进来，这个删除新字符串的最后一个并且设置这个字母没被访问过后面再处理。新字符串加上当前字母，并且设置当前字母被访问过。遍历完第二次就可以拿到最终结果了。

```
class Solution {
public:
    string removeDuplicateLetters(string s) {
        bool vis[256] = {false};
        int num[256] = {0};
        string str = "0";
        for(char c : s){
            num[c]++;
        }
        for(char c : s){
            num[c]--;
            if(vis[c]) continue;
            while(c < str.back() && num[str.back()]){
                vis[str.back()] = false;
                str.pop_back();
            }
            str += c;
            vis[c] = true;
        }
        return str.substr(1);
    }    
};
```
