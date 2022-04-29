## [785. Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/)

#### 题目大意

给定一个图，判断是否是二分图。
没理解二分图是啥所以没做出来。二分图不是说分成两个图，[二分图](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E5%9B%BE)。

col用来存放每个节点的颜色，如果相邻的颜色相同，那么就不是二分图。

循环每个节点，节点中相邻节点全部分别判断。

```
class Solution {
public:
    vector<int>vis,col;
    bool dfs(int v, int c, vector<vector<int>>& graph){
        vis[v]=1;
        col[v]=c;
        for(int child:graph[v]){
            if(vis[child]==0){
                // here c^1 is for flipping 1 by 0 or 0 by 1, that is flip the current color
                if(dfs(child,c^1,graph)==false) 
                    return false;
            }
            else{
                if(col[v]==col[child])
                    return false;
            }
        }
        return true;
    }
    
    bool isBipartite(vector<vector<int>>& graph) {
        int n=graph.size();
        vis.resize(n);
        col.resize(n);

        for(int i=0;i<n;++i){
            if(vis[i]==0 && dfs(i,0,graph)==false){ 
                return false;
            }
        }
        
        return true;
    }
};
```
