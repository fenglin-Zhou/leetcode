## [763. Partition Labels](https://leetcode.com/problems/partition-labels/)

#### 题目大意

给定一个字符串，求其中的相同字符组成的片段。

首先求出每个字母的最后出现位置，然后循环，取当前位置字母的最后出现位置和前面所有字母最后出现的位置的最大值。如果当前位置正好是最大值，说明子串的所有字母只在这个子串中出现，那么这就是一个片段。

```
class Solution {
public:
    vector<int> partitionLabels(string s) {
        vector<int> ans;
        vector<int> last(128, 0);
        for(int i = 0; i < s.size(); ++i){
            last[s[i]] = i;
        }
        int left = 0;
        int right = 0;
        for(int i = 0; i < s.size(); ++i){
            right = max(last[s[i]], right);
            if(right == i){
                ans.emplace_back(right-left+1);
                left = i+1;
                right = left;
            }
        }
        return ans;
    }
};
```
