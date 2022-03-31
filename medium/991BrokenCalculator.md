## [991. Broken Calculator](https://leetcode.com/problems/broken-calculator/)

#### 题目大意

给一个初始值和目标值，只能通过乘以2和减一操作到达目标值，求最少步骤。
数学题了属于是。
一开始我的思路也是从目标值反推到初始值，但是dfs跑太慢了。

反推就是除以2和加1的操作，Y <= X的时候我们肯定不会/2只会加1。如果Y是奇数我们只会+1，因为(Y + 1 + 1) / 2 = (Y / 2) + 1， 少一次操作到了相同数字，所以我们偶数只/2。最后Y < X差值也是操作的一部分。

Intuition:
Considering how to change Y to X
Operation 1: Y = Y / 2 if Y is even
Operation 2: Y = Y + 1

Explanation:
Obviously,
If Y <= X, we won't do Y / 2 anymore.
We will increase Y until it equals to X

So before that, while Y > X, we'll keep reducing Y, until it's smaller than X.
If Y is odd, we can do only Y = Y + 1
If Y is even, if we plus 1 to Y, then Y is odd, we need to plus another 1.
And because (Y + 1 + 1) / 2 = (Y / 2) + 1, 3 operations are more than 2.
We always choose Y / 2 if Y is even.

Why it's right
Actually, what we do is:
If Y is even, Y = Y / 2
If Y is odd, Y = (Y + 1) / 2

We reduce Y with least possible operations, until it's smaller than X.

And we know that, we won't do Y + 1 twice in a row.
Becasue we will always end with an operation Y / 2.

2N times Y + 1 and once Y / 2 needs 2N + 1 operations.
Once Y / 2 first and N times Y + 1 will end up with same result, but needs only N + 1 operations.

Time complexity
We do Y/2 all the way until it's smaller than X,
time complexity is O(log(Y/X)).

```
class Solution {
public:
    int brokenCalc(int X, int Y) {
        int res = 0;
        while (Y > X) {
            Y = Y % 2 > 0 ? Y + 1 : Y / 2;
            res++;
        }
        return res + X - Y;
    }
};
```
