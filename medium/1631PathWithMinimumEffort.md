## [1631. Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/)

#### 题目大意

给一个二维数组，从左上角到右下角，求最小绝对落差值的路径落差值。

一条路径每次移动的绝对落差是两点的差值，而这条路径的值是最大的那个落差。

发现没人用dfs去做，自己写的也跑不出来。换个思路。

用一个数组存放到每个位置的落差值，比如v[i][j]存放的是从左上角到这里的最小落差。从头出发，循环四个方向，如果新位置的落差小于当前位置落差就直接返回，更新新位置落差--->(新位置位置的旧落差)和(新位置与当前位置的落差，和当前位置落差的最大值，这里就是所有到新位置的最大落差)的最小值。

```
class Solution {
public:
 int minimumEffortPath(vector<vector<int>>& a) {
  int n=a.size();
  int m=a[0].size();

  int v[n+1][m+1];
  for(int i=0;i<n;i++)
  {
   for(int j=0;j<m;j++)
   {
    v[i][j]=INT_MAX;
   }
  }
  v[0][0]=0;
  queue<pair<int,int> > q;
  q.push({0,0});
  int d[5]={0,-1,0,1,0};
  while(!q.empty())
  {
   pair<int,int> u =q.front();
   q.pop();
   for(int i =0;i<4;i++)
   {
    int x=u.first+d[i];
    int y=u.second +d[i+1];

    if(x<0||y<0||y>=m||x>=n) continue;

    if(v[x][y]<=v[ u.first ][ u.second ] ) continue;

    int p=max(v[ u.first ][ u.second ], abs(a[x][y]-a[ u.first ][ u.second ] ) );
    v[x][y]=min(p,v[x][y]);
    q.push({x,y});
   }

  }
  return v[n-1][m-1];
 }
};
```
