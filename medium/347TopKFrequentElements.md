## [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

#### 题目大意

给定数组，求前k个出现次数最多的数字。

先用map统计出现的次数，再将map转换成vector用于排序，map里面是pair类型。其实可以简单一点，直接用priority_queue，只是要将map里面的first和second反过来会将出现次数多的排到前面，并且题目没有要求相同次数小的数在前面。

```
class Solution {
public:
    static bool cmp(pair<int, int> a, pair<int, int>b){
            if(a.second != b.second){
                return a.second > b.second;
            }else{
                return a.first < b.first;
            }
    }
    vector<int> topKFrequent(vector<int>& nums, int k) {
        map<int, int> mp;
        for(auto num : nums){
            mp[num]++;
        } 
        vector<pair<int, int>> vc(mp.begin(), mp.end());
        sort(vc.begin(), vc.end(), cmp);
        vector<int> ans;
        for(int i = 0; i < k; ++i){
            ans.push_back(vc[i].first);
        }
        return ans;
    }
};
```

```
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int,int> m;
        for(auto x: nums) m[x]++;
        priority_queue<pair<int,int>>pq;
        for(auto x: m) {
            pq.push({x.second, x.first});
        }
        vector<int> ans;
        for(int i = 0; i < k; i++) {
            ans.push_back(pq.top().second);
            pq.pop();
        }
        return ans;
    }
};
```
