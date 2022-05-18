## [1192. Critical Connections in a Network](https://leetcode.com/problems/critical-connections-in-a-network/)

#### 题目大意

给定一个网络，找出所有的桥连接，也是没了这条路网络会被隔离开。

首先我们保存每个节点的相邻节点。timestamp存储每个节点被访问的时间。
dfs从0开始遍历，如果这个节点已经被访问过，也就是timestamp不为0，那么直接返回这个节点被访问的时间。对于当前节点，我们遍历他的所有相邻边（除了他的前序节点），找到到达当前节点的最快时间。如果到该节点的最快时间大于等于当前节点的时间戳，说明没有别的路可以到达这个节点，那么也就是说当前节点和前序节点是一个桥，那么加入ans。

```
class Solution {
public:
    int t = 1;
    vector<vector<int>> criticalConnections(int n, vector<vector<int>>& con) {
        vector<vector<int>> mp(n);
        vector<vector<int>> ans;
        for(auto c : con){
            mp[c[0]].push_back(c[1]);
            mp[c[1]].push_back(c[0]);
        }
        vector<int> timestamp(n, 0);
        dfs(mp, timestamp, 0, -1, ans);
        return ans;
    }
    int dfs(vector<vector<int>>& mp, vector<int> &time, int now, int pre, vector<vector<int>> &ans){
        if(time[now] != 0) return time[now];
        time[now] = t++;
        int minit = INT_MAX;
        for(auto &m : mp[now]){
            if(m == pre) continue;
            int nei = dfs(mp, time, m, now, ans);
            minit = min(nei, minit);
        }
        if(minit >= time[now]){
            if(pre >= 0) ans.push_back({pre, now});
        }
        return min(minit, time[now]);
    }
};
```
