## [1202. Smallest String With Swaps](https://leetcode.com/problems/smallest-string-with-swaps/)

#### 题目大意

给定一个字符串和一些可交换的位置集合，要求通过交换位置使得字符串的字典序最小。

首先把每个交换位置的集合计算出来，比如[0,1],[1,2]就是0，1，2这三个位置随便交换，那么就可以直接进行排序，再放回原来的位置。

```
class Solution {
public:
    int find(vector<int>& ds, int i) {
        return ds[i] < 0 ? i : ds[i] = find(ds, ds[i]);
    }
    string smallestStringWithSwaps(string s, vector<vector<int>>& pairs) {
        vector<int> ds(s.size(), -1);
        vector<vector<int>> m(s.size());
        for (auto& p : pairs) {
            auto i = find(ds, p[0]), j = find(ds, p[1]);
            if (i != j) 
                ds[j] = i;
        }
        for (auto i = 0; i < s.size(); ++i) 
            m[find(ds, i)].push_back(i);
        for (auto &ids : m) {
            string ss = "";
            for (auto id : ids) 
                ss += s[id];
            sort(begin(ss), end(ss));
            for (auto i = 0; i < ids.size(); ++i) 
                s[ids[i]] = ss[i];
        }
        return s;
    }
};
```
