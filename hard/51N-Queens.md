## [51. N-Queens](https://leetcode.com/problems/n-queens/)

#### 题目大意

n皇后问题,之前还挺熟练，现在忘了一些了。

遍历每一列，如果这行没被使用，那么就假定棋子在当前列的当前行，然后判断前面的列和当前列是否有冲突，有的话就不合理下一行。没冲突就到下一列去了，同时更新当前行被访问了已经，下一列不能使用当前行。

主要是判断是否冲突，如果当前列与前面列的差值 == 当前列棋子所在行与前面列棋子所在的行，那么就是有冲突。比如第一列的棋子在第一行，第二列的棋子在第二行，也就是判断对角线，因为同一行我们在开头判断过了不存在。

```
class Solution {
public:
    vector<vector<string>> ans;
    int num;
    bool hashtable[10] = {0};
    int p[10];
    vector<vector<string>> solveNQueens(int n) {
        num = n;
        string str = "";
        for(int i = 0; i < n; ++i){
            str += ".";
        }
        vector<string> t(n, str);
        dfs(0);
        return ans;
    }
    void dfs(int index){
        if(index == num){
            string str = "";
            for(int i = 0; i < num; ++i){
                str += ".";
            }
            vector<string> t(num, str);
            for(int i = 0; i < num; ++i){
                t[i][p[i]] = 'Q';
            }
            ans.push_back(t);
            return;
        }
        for(int i = 0; i < num; ++i){
            if(hashtable[i] == false){
                bool flag = true;
                for(int pre = 0; pre < index; ++pre){
                    if(abs(index - pre) == abs(i - p[pre])){
                        flag = false;
                        break;
                    }
                }
                if(flag){
                    p[index] = i;
                    hashtable[i] = true;
                    dfs(index+1);
                    hashtable[i] = false;
                }
            }
        }
    }
};
```
