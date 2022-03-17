## [856. Score of Parentheses](https://leetcode.com/problems/score-of-parentheses/)

#### 题目大意

给定一个只有（和）的字符串，根据三种规则计算出值的大小，详见题目。

通过一个栈来解决，每次（直接压栈，遇到）的时候通过栈顶判断是数字还是（，这里我们栈用int，因为值可能大于256，char存不下。如果是数字就需要不断取出栈顶是数字的相加，遇到（就*2再把结果压栈，再循环直到遇到）的时候再判断。

```
class Solution {
public:
    int scoreOfParentheses(string s) {
        int ans = 0;
        stack<int> st;
        st.push(-1);
        int i = 1;
        while(i < s.size()){
            if(s[i] == ')'){
                int ch = st.top();
                if(ch == -1){
                    st.pop();
                    st.push(1);
                }else if(ch != -1){
                    int temp = ch;
                    st.pop();
                    while((ch = st.top()) != -1){
                        temp += ch;
                        st.pop();
                    }
                    temp *= 2;
                    st.pop();
                    st.push(temp);
                }
            }else{
                st.push(-1);
            }
            i++;
        }
        while(!st.empty()){
            ans += st.top();
            st.pop();
        }
        return ans;
    }
};
```
