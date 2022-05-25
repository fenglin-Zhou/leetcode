## [354. Russian Doll Envelopes](https://leetcode.com/problems/russian-doll-envelopes/)

#### 题目大意

给定一堆长宽已知的信封，求最大的套娃数量，必须长宽大于才能套。
dp思路，要是当前信封长宽大于，则选择大的那个数量值。但是这个会超时，思路是对的。

```
class Solution {
public:
    int maxEnvelopes(vector<vector<int>>& env) {
        if(env.empty()) return 0;
        sort(env.begin(), env.end());
        vector<int> bp(env.size(), 1);
        int ans = 1;
        for(int i = 1; i < env.size(); ++i){
            for(int j = 0; j < i; ++j){
                if(env[i][0] > env[j][0] && env[i][1] > env[j][1]){
                    bp[i] = max(bp[i], bp[j]+1);
                }
            }
            if(bp[i] > ans) ans = bp[i];
        }
        return ans;
    }
};
```

vector<int> 更慢我是没想到的，转换成pair。。。
首先排序，先按照第一个元素升序，第二个元素降序，因为我们后面要判断第一个不小于当前信封的元素。然后依次取出每个信封，找出当前套娃中第一个不小于当前信封宽的信封的宽，如果找不到不小于的（大于等于）那么说明当前信封很大，可以塞进去，如果找到的信封大于当前信封，那么说明可以替换。最后统计数量。

```
class Solution {
public:
    int maxEnvelopes(vector<vector<int>>& envelopes) {
        vector<pair<int, int> > temp;
        int n = envelopes.size();
        for (int i = 0; i < n; i++) {
            pair<int, int> p;
            p.first = envelopes[i][0];
            p.second = envelopes[i][1];
            temp.push_back(p);
        }
        sort(temp.begin(), temp.end(), [](pair<int, int> a, pair<int, int>b){
  return a.first < b.first || (a.first==b.first && a.second > b.second);
     });
        vector<int> collector;
        for(auto& pair: temp)
        {
            auto iter = lower_bound(collector.begin(), collector.end(), pair.second);
            if(iter == collector.end()) collector.push_back(pair.second);
            else if(*iter > pair.second) *iter = pair.second;
        }
        return collector.size();
    }
};
```
