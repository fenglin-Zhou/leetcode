## [71. Simplify Path](https://leetcode.com/problems/simplify-path/)

#### 题目大意

给定一个串字符，是文件目录，要求返回正确格式。

思路是读取每个非"/"的子串，然后加到list中，最后再统一取出来。

优秀代码，思路基本一样，就是它使用了getline读数据，这个确实方便很多。

```
class Solution {
public:
    string simplifyPath(string path) {
        string res, tmp;
        vector<string> stk;
        stringstream ss(path);
        while(getline(ss,tmp,'/')) {   //getline用法
            if (tmp == "" or tmp == ".") continue;
            if (tmp == ".." and !stk.empty()) stk.pop_back();
            else if (tmp != "..") stk.push_back(tmp);
        }
        for(auto str : stk) res += "/"+str;
        return res.empty() ? "/" : res;
        
    }
};
```

我自己的代码

```
class Solution {
public:
    string simplifyPath(string path) {
        string ans = "";
        list<string> lis;
        string name = "";
        for(int i = 0; i < path.size(); ++i){
            if(path[i] == '/'){
                if(name.size() != 0){
                    if(name == ".."){
                        if(!lis.empty())
                            lis.pop_back();
                    }else if(name == "."){
                    }else{
                        lis.push_back(name);
                    }
                }
                name = "";
            }else {
                name += path[i];
            }
        }
        if(name.size() != 0){
            if(name == ".."){
                if(!lis.empty())
                    lis.pop_back();
            }else if(name == "."){
            }else{
                lis.push_back(name);
            }
        }
        while(!lis.empty()){
            ans += "/";
            ans += lis.front();
            lis.pop_front();
        }
        if(ans == "")
            return "/";
        return ans;
    }
};
```
