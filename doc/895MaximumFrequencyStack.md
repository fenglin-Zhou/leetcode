## [895. Maximum Frequency Stack](https://leetcode.com/problems/maximum-frequency-stack/)

#### 题目大意

实现一个最频繁使用栈，pop出使用次数最多的值。

一个map1保存<val， count>, 另一个map2保存<count, stack \<int>>,这是对应出现次数的数字有哪些，一个maxcount记录当前最多使用次数。存都是直接加。取的时候先去map2[maxcount]拿出栈，然后栈pop元素，就是要的值，map1[val]--,如果栈空了，说明最大count的值没了，maxcount--。

```
class FreqStack {
    map<int, int> map1;
    map<int, stack<int> > map2;
    int maxcount;
public:
    FreqStack() {
        maxcount = 0;
    }
    
    void push(int val) {
        int count = ++map1[val];
        if(count > maxcount) maxcount = count;
        map2[count].push(val);
    }
    
    int pop() {
        if(maxcount == 0) return -1;
        stack<int> &st = map2[maxcount];
        int val = st.top();
        st.pop();
        if(st.empty()) maxcount--;
        map1[val]--;
        return val;
    }
    
};
```
