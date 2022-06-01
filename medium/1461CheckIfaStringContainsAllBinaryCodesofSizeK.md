## [1461. Check If a String Contains All Binary Codes of Size K](https://leetcode.com/problems/check-if-a-string-contains-all-binary-codes-of-size-k/)

#### 题目大意

给定一个只有01的字符串和一个int k，求这个字符串时候包含了所有k长度的01编码，比如k为2，就是00，01，10，11。

从左向右遍历每一个k长度的子串，记录他们的十进制大小，保存他们是否被访问，对于k来说应该是十进制0-(2^k-1)。通过左移操作和于操作保证每个子串的长度为k，对于当前数字如果已经访问过那个计数不减一，否则减一。最后如果计数器为0则说明所有的数字都包括。

```
class Solution {
public:
    bool hasAllCodes(string s, int k) {
        int n = s.size();
        if(k >= n) return 0;
        int total = (1 << k) - 1;
        int flag = total+1;;
        vector<bool> isv(total+1, 0);
        int curr = 0;
        for(int i = 0; i < k; ++i){
            curr <<= 1;
            curr += (s[i] - '0');
        }
        isv[curr] = 1;
        flag--;
        for(int i = k; i < s.size(); ++i){
            curr <<= 1;
            curr += (s[i] - '0');
            curr &= total;
            flag -= !isv[curr];
            isv[curr] = 1;
        }
        return !flag;
    }
};
```
