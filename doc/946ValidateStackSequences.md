## [946. Validate Stack Sequences](https://leetcode.com/problems/validate-stack-sequences/)

#### 题目大意

给定两个数组，分别是push队列和pop队列，判断是否可行。

思路一：同时向后顺序扫描，push进栈，栈顶==pop头就出栈,循环判断是否相等，不等继续push再判断，最后看栈是否为空。

```
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        stack<int> stk;
        int n = popped.size();
        int i = 0, j = 0;
        while (i < n && j < n) {   
            while (i < n && (stk.empty() || stk.top() != popped[j])) {
                stk.push(pushed[i]);
                i++;
            }
            while (j < n && !stk.empty() && stk.top() == popped[j]) {
                stk.pop();
                j++;
            }
        }
        
        return stk.empty();
    }
};
```
