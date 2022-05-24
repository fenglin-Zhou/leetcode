## [32. Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/)

#### 题目大意

给定一个字符串只有（和），求最长的合理子串。就是（（）（））差不多。

遍历字符串，找到每个不合理的位置，用栈保存位置，遇到（）我们直接pop（），那么剩的都是不合理的位置，找到最长的就是合理的。

```
class Solution {
public:
    int longestValidParentheses(string s) {
        int ans = 0;
        int size = s.size();
        if(s.size() <= 1) return 0;
        stack<int> st;
        for(int i = 0; i < size; ++i){
            if(s[i]=='('){
                st.push(i);
            }else {
                if(!st.empty()){
                    if(s[st.top()] == '(') st.pop();
                    else st.push(i);
                }else{
                    st.push(i);
                }
            }
        }
        if(st.empty()) return size;
        int right = size, left = 0;
        while(!st.empty()){
            left = st.top();
            st.pop();
            ans = max(ans, right-left-1);
            right = left;
        }
        ans = max(ans, right);
        return ans;
    }
};
```

第二个方法是两次遍历，从左向右的时候，如果）的数量大于（，那么说明合理的范围结束了，那么久计数归零。如果（和）数量相等，说明是合理的，那么就记录（和）的数量和。从右向左相反，（的数量大于）说明不合理了。

```
class Solution {
public:
    int longestValidParentheses(string s) {
        int cntl=0,cntr=0,ansl=0,ansr=0;
        for(int i=0;i<s.size();i++){
            if(s[i]=='(')
                cntl++;
            if(s[i]==')')
                cntr++;
            if(cntr>cntl)
            {
                cntr=0;
                cntl=0;
            }
            else if(cntr==cntl)
              ansl=max(ansl,cntl+cntr);
        }
        cntl=0;
        cntr=0;
        for(int i=s.size()-1;i>=0;i--){
            if(s[i]=='(')
                cntl++;
            if(s[i]==')')
                cntr++;
            if(cntl>cntr){
                cntl=0;
                cntr=0;
                }
            else if(cntl==cntr)
              ansr=max(ansr,cntl+cntr);
        }
        return max(ansl,ansr);
    }
};
```
