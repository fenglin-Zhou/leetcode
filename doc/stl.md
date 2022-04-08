## 常见stl

#### priority_queue<T>

只有push pop top这些基本操作，和栈很像。
这是优先队列，每次push会自动排序，将最大值放在上面，小的放在下面。
priority_queue<int, vector<int>, greater<int> >反过来。
