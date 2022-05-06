## [1209. Remove All Adjacent Duplicates in String II](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/)

#### 题目大意

给一个字符串和k，删除所有k个连续相等的字符串，保证最后的字符串不存在连续k个相等的。

用一个栈保存中间字符串，每次遇到k个相等的就pop出来，那么最后的结果肯定不会有k个相等的。

```
class Solution {
public:
    string removeDuplicates(string s, int k) {
        vector<pair<int, char>> stack = {{0, '#'}};
        for(char c : s){
            if(stack.back().second != c){
                stack.push_back({1, c});
            }else if(++stack.back().first == k){
                stack.pop_back();
            }
        }
        string str = "";
        for(auto &p : stack){
            str.append(p.first, p.second);
        }
        return str;
    }
};
```
