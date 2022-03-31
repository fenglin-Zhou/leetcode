## [1249. Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)

#### 题目大意

给定字符串里面有多余（或者），去除多余的，规则是匹配远的去除。

用个栈装多余的（在s串中的位置，匹配到）就pop，否则最后拿出来给s[pos] = '-', 而）如果没匹配到（直接当前位置'-'，最后循环，'-'都不拷贝。

```
class Solution {
public:
    string minRemoveToMakeValid(string s) {
        stack<int> st;
        for(int i = 0; i < s.size(); i++){
            if(s[i] == '('){
                st.push(i);
            }else if(s[i] == ')'){
                if(!st.size()) s[i] = '-';
                else{
                    st.pop();
                }
            }
        }
        while(st.size()){
            s[st.top()] = '-';
            st.pop();
        }
        string str = "";
        for(auto ch : s){
            if(ch != '-')
                str += ch;
        }
        return str;
    }
};
```
